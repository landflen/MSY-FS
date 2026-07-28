# Blatt ⑤ — Rekonstruktionsbasierte Verfahren: AE, CAE, GAN, AnoGAN, f-AnoGAN (Kap. 7)

> Vorlage zum handschriftlichen Übertragen. Quelle: Foliensatz 07 (AE, GAN, AnoGAN, f-AnoGAN).
> **VAE entfällt (Klammer-Regel, geklärt 23.7.) — nicht klausurrelevant.**
> Deckt Aufgabentyp 3 (AE-Code schreiben) + Typ 9 (AnoGAN komplett) ab. Zielumfang: ~3 A4-Seiten.

**Beim Übertragen: die drei Code-Gerüste am Rand markieren (⚑) — das wird in der Klausur gesucht.**

| gefragt ist … | Gerüst |
|---|---|
| Autoencoder / CAE schreiben | ⚑ **CAE-Gerüst** |
| Generator + Discriminator schreiben | ⚑ **G/D-Gerüst** |
| f-AnoGAN-Encoder schreiben | ⚑ **Encoder-Gerüst** |
| Training / Score **beschreiben** | AnoGAN-Ablauf, f-AnoGAN 3 Phasen (Text, kein Code) |

---

## Grundidee Rekonstruktion (Folien 2–4)

- Curse of Dimensionality: benötigte Datenmenge steigt exponentiell, Abstände werden untereinander immer ähnlicher → nutzlos → **Dimensionsreduktion**
- Novelty Detection per Rekonstruktion: Modell (auf Normaldaten trainiert) kann nur Ähnliches rekonstruieren → **Rekonstruktionsfehler = Anomalie-Score** (hoch = Anomalie)

## Autoencoder (Folien 8–11)

- Encoder → **Code z (Latent Variable)** → Decoder; Ausgang rekonstruiert Eingang
- Loss = Abstand Eingabe ↔ Rekonstruktion (MSE) → **unüberwacht, keine Labels nötig**
- z hat **niedrigere Dimension** als Eingabe — sonst lernt das Netz nur die Identität! (MC-Klassiker)
- Architektur: Encoder verjüngt sukzessive, Decoder = **gespiegelter** Encoder
- Traditionelle Anwendungen: Schicht-Initialisierung (heute selten); **Feature-Descriptor** (Encoder liefert Merkmale → z. B. AE auf Normaldaten + OCSVM auf encodierten Merkmalen)

## Convolutional Autoencoder — CAE (Folien 12–16)

- **Warum CAE statt Dense-AE für Bilder — zwei Gründe (beide nennen!):** (1) Dense-AE verliert Nachbarschaft/2D-Struktur; (2) **Weight Sharing** — derselbe Filter gilt an jeder Bildposition ⇒ drastisch weniger Gewichte (Blatt ②: 222 gegen 157 000) ⇒ weniger Overfitting
- **Downsampling im Encoder**: Pooling oder Conv mit strides=2
- **Upsampling im Decoder** — 2 Möglichkeiten:
  1. `UpSampling2D` + Interpolation (nearest/bilinear) → wird nicht gelernt, „verschmiert"
  2. **Transponierte Faltung** `Conv2DTranspose` (= Deconvolution, fractionally-strided conv) → gelerntes Upsampling; strides=2 **verdoppelt** H und W; padding='same'
- Typischer Aufbau: Eingabe → [Conv strides=2]×n → Flatten → Dense = z → Dense → Reshape → [Conv2DTranspose strides=2]×n → Rekonstruktion

**Shape-Regel für Blatt ②:** Conv2DTranspose, strides=2, padding='same' → 2H × 2W × filters

**CAE-Gerüst (Aufgabentyp 3) — Beispiel 32×32×3, zwei Halbierungen, z = 20:**
```python
net = tf.keras.Sequential([
  tf.keras.layers.InputLayer((32, 32, 3)),
  tf.keras.layers.Conv2D(filters=8,  kernel_size=3, strides=2, padding='same',
                         activation='relu'),                                     # 16x16x8
  tf.keras.layers.Conv2D(filters=16, kernel_size=3, strides=2, padding='same',
                         activation='relu'),                                     # 8x8x16
  tf.keras.layers.Flatten(),                                                     # 1024
  tf.keras.layers.Dense(units=20,     activation='relu'),                        # Code z
  tf.keras.layers.Dense(units=8*8*16, activation='relu'),                        # aufweiten!
  tf.keras.layers.Reshape((8, 8, 16)),
  tf.keras.layers.Conv2DTranspose(filters=8, kernel_size=3, strides=2, padding='same',
                                  activation='relu'),                            # 16x16x8
  tf.keras.layers.Conv2DTranspose(filters=3, kernel_size=3, strides=2, padding='same',
                                  activation='sigmoid')])                        # 32x32x3 -> filters=3!
net.compile(optimizer='adam', loss='mse')
net.fit(x=train_data, y=train_data, ...)   # x = y, s. u.
```

**Vier Fallen beim Decoder (26.7. alle getroffen):**
1. Nach dem Code z **erst `Dense(H·W·C)`, dann `Reshape((H,W,C))`** — aus 20 Werten lässt sich keine 8×8×16-Karte formen. `Reshape()` **nie ohne Ziel-Shape**. (Praktikum 06: `Dense(7*7*8)` → `Reshape((7,7,8))`.)
2. **`padding='same'` bei JEDER `Conv2DTranspose`** — sonst 8 → 17 → 35 statt 8 → 16 → 32.
3. Die **Ausgabe ist die letzte transponierte Faltung**, keine nachgestellte Dense: `Conv2DTranspose(filters = Kanalzahl des Bildes, activation='sigmoid')` (MNIST 1, Farbe 3). Danach kein weiteres Reshape.
4. Schreibweise: **`tf.keras.layers.…`** — `tf.keras.Conv2D` gibt es nicht.

**Warum `fit(x=train_data, y=train_data)`?** Der AE soll seine **eigene Eingabe** rekonstruieren, das Ziel ist also das Eingangsbild selbst. Genau deshalb ist das Verfahren **unüberwacht**: es gibt keine Labels — das Label **ist** die Eingabe.

**Anomalie-Score für neue Samples:** durch das Netz schicken → Rekonstruktion → **MSE über alle Pixel je Sample** → Vergleich mit dem **vorher auf Normaldaten festgelegten Schwellwert** (Quantil oder ROC-Knie). Der AE selbst klassifiziert nichts.

## Ensembles von AE / RandNet (Folien 17–25)

- Problem: Rekonstruktionsfehler einzelner AE instabil → Ensemble (vgl. iForest!)
- RandNet variiert **3 Dinge**: (1) zufällige **Verbindungsmaske** je Schicht, (2) zufällige **Trainings-Untermenge** je Netz, (3) Initialisierung
- RandNet-Schicht = Dense mit zufälliger 0/1-**Maske auf den Gewichten** (elementweise Multiplikation); Maske wird 1× bei Erstellung gezogen (m·n Ziehungen **mit Zurücklegen** → Duplikate ⇒ ≈ 37 % der Verbindungen nie gezogen, ≈ 63 % überleben), bleibt dann konstant
- **Maske ≠ Dropout:** Maske einmalig fest, auf **Verbindungen**, immer aktiv — Dropout pro Schritt neu, auf **Neuronen**, in der Inferenz aus. (Nie „Neuronen werden rausgenommen" für RandNet schreiben!)
- Architektur: Encoder halbiert Neuronen je Schicht, Decoder verdoppelt; max. 7 Schichten; Code ≥ 3 Neuronen; **erste Encoder- und letzte Decoder-Schicht: Sigmoid, Rest ReLU**
- Training: 100 Netze, 300 Epochen, RmsProp, je 1/10 der Daten (Subsampling), Sample-Anzahl wächst ×1,01 pro Epoche
- Score: quadrat. Fehler je Netz → normalisieren mit Std der Trainingsfehler des Netzes → **Median** über alle Netze

## GAN (Folien 27–36)

- **Generator** G: Eingabe Latent-Vektor z (feste Verteilung, z. B. Normal) → generiertes Sample; Architektur ≈ Decoder
- **Discriminator** D: Eingabe Sample → binär echt/generiert
- **Minimax-Game**: min_G max_D V = E_x[log D(x)] + E_z[log(1 − D(G(z)))]
- Training: **abwechselnd** pro Schritt; Kosten bleiben idealerweise beidseitig ~konstant
- **Trainingsende (Folie 28)** — für „Beschreiben Sie das Training": *eigentlich* fertig, wenn D
  keinen Unterschied mehr sieht ⇒ **Kosten von D dauerhaft hoch, Kosten von G niedrig**. Dieses
  Bild ist aber **nicht eindeutig**: es entsteht genauso, wenn G nur **schneller gelernt** hat als
  D und mit unrealistischen Strukturen „betrügt". Deshalb reicht der Fehlerverlauf nicht — die
  **generierten Daten ansehen**.
- Vorteile (Folie 34): (1) A-priori-Verteilung von z wird **implizit** gelernt (G bekommt Eingaben
  aus fester Verteilung und lernt, dazu passend zu generieren); (2) Qualitätsprüfung nicht durch
  ein festes Maß, sondern durch ein **Netz** — D prüft auch **lokale** Information ⇒ Daten wirken
  auch für Netze echt; (3) beste Datenqualität unter den Generatoren (heute von Diffusionsmodellen
  abgelöst)
- Nachteile (MC!): Netze müssen gleich schnell lernen (D zu schnell → G lernt nie; G zu schnell → G „betrügt"); Trainingsfortschritt schwer beurteilbar → generierte Daten inspizieren; kein direkter Einfluss auf Generierung

---

### G und D bauen (Aufgabentyp 9)

**DCGAN** = Deep Convolutional GAN: G und D sind Faltungs- statt Dense-Netze. Der Name meint auch
die Rezeptliste selbst.

**① Rezeptliste (Folie 36)** — wird bei „Empfehlungen aus der Vorlesung" wörtlich abgefragt:
1. G und D architektonisch ähnlich (**G = gespiegelter D**) ⇒ gleiche Lerngeschwindigkeit
2. KEINE Pooling-Layers → D: `Conv2D` strides=2; G: `Conv2DTranspose` strides=2
3. 5×5-Filter
4. BatchNorm in G und D
5. keine Fully-Connected-Layers
6. G: ReLU (Output: **tanh**); D: **Leaky ReLU** (0,2·x für x ≤ 0)

**② Drei Rechenschritte, in dieser Reihenfolge:**
1. **Anzahl Faltungen:** strides=2 verdoppelt (G) bzw. halbiert (D) H und W — mehr nicht.
   Zielkante ÷ Startkante = Faktor. Faktor 4 ⇒ 2, **Faktor 8 ⇒ 3**, Faktor 16 ⇒ 4 Faltungen.
2. **Dense = Produkt des Reshape-Ziels.** (8,8,64) ⇒ `Dense(8*8*64)`. Das Reshape bestimmt die
   Dense, nie umgekehrt.
3. **Filter:** G halbiert pro Verdopplung (64 → 32), D verdoppelt pro Halbierung (16 → 32 → 64).
   **Ausgabeschicht von G = Kanalzahl des Zielbilds.**

**③ BatchNorm und Aktivierung:**
- Aktivierung als **eigene Schicht**, damit BN davor passt: Faltung ohne `activation=` →
  `BatchNormalization()` → `ReLU()` / `LeakyReLU()`.
- **Auch das `Dense` in G bekommt BN + Aktivierung**: `Dense(..., use_bias=False)` →
  `BatchNormalization()` → `ReLU()` → `Reshape`. Aufg. 9a sagt „**immer** ReLU", Ausnahme ist nur
  die Ausgabeschicht — und Praktikum 08 macht es genauso. (`use_bias=False` vor BN, weil BN den
  Bias ohnehin ersetzt.)
- Zählregel: **kein BN nur in der Ausgabeschicht des Netzes** — und die ist in G und D **nicht
  dieselbe Schichtart**:
  - **G:** Ausgabe = letzte `Conv2DTranspose` ⇒ bei n Faltungen **(n−1)× BN**.
  - **D:** Ausgabe = `Dense(1)` ⇒ **alle n Faltungen** bekommen BN.

**④ Gerüst (Muster Übungssammlung 9a/9b): z = 100 → 64×64×3**
```python
generator = tf.keras.Sequential([          # z -> Bild, wie ein Decoder
  tf.keras.layers.InputLayer((100,)),
  tf.keras.layers.Dense(units=8*8*64, use_bias=False),                 # Produkt des Reshape-Ziels
  tf.keras.layers.BatchNormalization(), tf.keras.layers.ReLU(),
  tf.keras.layers.Reshape((8, 8, 64)),
  tf.keras.layers.Conv2DTranspose(filters=64, kernel_size=5, strides=2,
                                  padding='same'),                     # 16x16
  tf.keras.layers.BatchNormalization(), tf.keras.layers.ReLU(),
  tf.keras.layers.Conv2DTranspose(filters=32, kernel_size=5, strides=2,
                                  padding='same'),                     # 32x32
  tf.keras.layers.BatchNormalization(), tf.keras.layers.ReLU(),
  tf.keras.layers.Conv2DTranspose(filters=3, kernel_size=5, strides=2, padding='same',
                                  activation='sigmoid')])   # 64x64x3 -> filters=3, kein BN

discriminator = tf.keras.Sequential([      # Bild -> EINE Zahl
  tf.keras.layers.InputLayer((64, 64, 3)),
  tf.keras.layers.Conv2D(filters=16, kernel_size=5, strides=2, padding='same'),  # 32x32
  tf.keras.layers.BatchNormalization(), tf.keras.layers.LeakyReLU(),
  tf.keras.layers.Conv2D(filters=32, kernel_size=5, strides=2, padding='same'),  # 16x16
  tf.keras.layers.BatchNormalization(), tf.keras.layers.LeakyReLU(),
  tf.keras.layers.Conv2D(filters=64, kernel_size=5, strides=2, padding='same'),  # 8x8
  tf.keras.layers.BatchNormalization(), tf.keras.layers.LeakyReLU(),
  tf.keras.layers.Flatten(),
  tf.keras.layers.Dense(units=1, activation='sigmoid')])   # binäre Klassifikation: 1 Neuron
  # Bei from_logits=True im Loss: Argument ersatzlos weglassen -> Dense(units=1),
  # Ausgabe ist dann ein Logit (beliebige reelle Zahl). Halbsatz dazuschreiben! (Folie 30)
```

**⑤ Aktivierungen — versteckte Schichten und Ausgabeschicht sind IMMER zwei verschiedene Fragen:**

| | versteckt | Ausgabe |
|---|---|---|
| **G** | ReLU | **sigmoid** bei Daten in [0,1], **tanh** bei [−1,1] |
| **D** | Leaky ReLU | `Dense(units=1, activation='sigmoid')` — **binäre** Klassifikation |
| **E** | ReLU | `Dense(units=latent_dim, activation='tanh')` |

**Sonderfall D — beide Antworten in einem Satz.** Steht in der Aufgabe „die Aktivierung ergibt sich
aus der Klassifikationsaufgabe" (so in Aufg. 9b), ist **sigmoid** gemeint: ein Neuron, Ausgabe als
Wahrscheinlichkeit. **Weglassen** darf man sie nur, wenn der Loss
`tf.keras.losses.BinaryCrossentropy(from_logits=True)` benutzt wird — diese Option **zieht die
Sigmoid in die Kostenfunktion** (Folie 30), deshalb darf D dann und nur dann ohne
Ausgabe-Aktivierung bleiben. Also sigmoid hinschreiben **und den Halbsatz dazu**; das deckt beide
Lesarten ab.

Gilt genauso für Klassifikationsnetze (Ausgabe: softmax bei mehreren Klassen / sigmoid bei zwei /
keine bei Regression) — dieselbe Frage, anderes Netz.

- **Argumentnamen ausschreiben** (`filters=`, `kernel_size=`, `units=`), sonst vertauscht man die
  ersten beiden Positionen: `Conv2D(filters, kernel_size, …)`, `Dense(units, …)`.
- „Keine Fully-Connected-Layers" meint **dazwischen**; die zwei Dense bleiben (Eingang G, Ausgang D).

---

**GAN-Training beschreiben (Folien 30–33) — Aufg. 9c verlangt ausdrücklich KEINEN Code.**
Antwortgerüst in Worten, pro Batch — rechts steht, woran man den Schritt im Code erkennt
(zum Wiedererkennen in Praktikum 08, nicht zum Abschreiben):

| Schritt (so hinschreiben) | im Code erkennbar an |
|---|---|
| 1. **z ziehen**, standardnormalverteilt, ein Vektor pro Bild des Batches | `noise = tf.random.normal([batch, z_dim])` |
| 2. **G erzeugt daraus Fakes** (Vorwärtsrechnung durch G) | `generated = generator_model(noise)` |
| 3. **D bewertet zweimal**: echte Bilder des Batches und die Fakes | zwei Aufrufe `discriminator_model(images)` / `(generated)` |
| 4. **D-Kosten**: binäre Kreuzentropie mit Ziel **echt = 1, fake = 0**, beide Anteile gemittelt | `ones_like(real_out)` + `zeros_like(fake_out)`, `0.5*(…+…)` |
| 5. **G-Kosten**: dieselbe Kreuzentropie, aber Ziel **fake = 1** — G will, dass D die Fälschung für echt hält (der Minimax-Gegensatz) | `ones_like(fake_out)` auf den **fake**-Ausgang |
| 6. beide Netze **abwechselnd** aktualisieren, je ein **eigener Optimierer** (Adam 2e-4); **kein `fit`**, weil zwei Netze mit gegenläufigen Zielen → eigene Schleife | zwei `GradientTape`, zwei `apply_gradients` |

- Merkanker zu 4./5.: **Nur das Ziel-Label unterscheidet die beiden Kosten** — derselbe fake-Ausgang, für D „ist 0", für G „soll 1 sein".
- Ende: Kosten bleiben beidseitig ungefähr konstant ⇒ **generierte Bilder ansehen** (s. o.)

## AnoGAN (Folien 37–42) — Ablauf komplett (Aufgabentyp 9!)

**Warum überhaupt eine Optimierung? (Folie 37 — erster Satz jeder Antwort auf „wie scort AnoGAN?")**
Gefragt ist: Könnte der Generator dieses Sample erzeugt haben? Dazu bräuchte man das passende z —
aber ein GAN kennt nur den Weg **z → Sample**, **kein inverses Mapping** Sample → z. Das passende z
muss also **gesucht** werden, und wie gut es am Ende passt, ist der Score.

**Training:** GAN ganz normal mit Normaldaten trainieren.

**Scoring eines neuen Samples x** (GAN-Parameter bleiben eingefroren!):
1. z zufällig initialisieren (aus A-priori-Verteilung)
2. n Iterationen (z. B. 500): L(x, z) nach **z** ableiten, z per Gradient Descent anpassen
3. finale Kosten L(x, z_n) = **Anomalie-Score**

**Kostenfunktion** (gewichtete Summe, λ z. B. 0,1):
- Residual Loss L_res: Abstand **x ↔ G(z)** im Bild selbst
- Discrimination Loss L_disc: Abstand **D_k(x) ↔ D_k(G(z))** — D_k = Ausgabe der vorletzten Discriminator-Schicht (im Code `feature_model`)
- L = (1−λ)·L_res + λ·L_disc

**⚠ L_disc ist KEINE Klassifikationsentscheidung.** Beide Anteile messen **Ähnlichkeit**, nur in
verschiedenen Räumen:

| | L_res | L_disc |
|---|---|---|
| verglichen | x ↔ G(z) | D_k(x) ↔ D_k(G(z)) |
| Raum | **Pixelraum** | **Merkmalsraum** (vorletzte D-Schicht) |
| Frage | sehen die Bilder gleich aus? | wirken sie für D gleich? |

D ist hier **Merkmalsextraktor, kein Klassifikator** — sein Echt/Fake-Urteil wird nicht ausgewertet,
daher `layers[-2]`. „Kosten für die Klassifikation als Fälschung" ist falsch.

**Kein Code nötig** (Musterlösung zu 9d ist Fließtext). Zwei Punkte, die man trotzdem sagen sollte:
**z ist die einzige optimierte Größe** (als `tf.Variable`, ein z pro Sample; G und D bleiben
eingefroren), und **D wird nur bis zur vorletzten Schicht benutzt** (`layers[-2]` = feature_model).

**Nachteil AnoGAN:** pro neuem Sample eigene z-Optimierung → langsam im Einsatz.

## f-AnoGAN (Folien 43–49)

**Idee:** Encoder E lernt, z direkt aus x zu berechnen → Scoring in einem Durchlauf, keine Iterationen.

**3 Trainingsphasen:**
1. GAN mit Normaldaten trainieren
2. **Encoder** trainieren (GAN eingefroren, gleiche Normaldaten; E am besten = „gespiegelter" Generator). Aufbau als Autoencoder: `E → G` (G als Decoder)
3. Scoring: Score(x) = L(x) = L_res + L_disc mit G(E(x)) — **eine** Vorwärtsrechnung

- Dieselben zwei Anteile wie AnoGAN, nur mit **MSE** statt Betrag und mit G(E(x)) statt G(z)
  (Folie 44 gewichtet zusätzlich mit Κ; der Code auf Folie 46 addiert beide **ungewichtet**)
- Encoder-Training: RMSprop, Loss = Mittel der Gesamtkosten über Batch

**Encoder-Architektur = Generator rückwärts** (Aufgabentyp 9, wird als Code verlangt): gleich viele
Faltungen wie G **ohne** dessen Ausgabeschicht, gleiche Feature-Map-Zahlen wie Gs mittlere
Schichten, `Conv2D` statt `Conv2DTranspose`, sonst alles wie in G. Ende: `Flatten` →
`Dense(units=latent_dim, activation='tanh')`. Zum Generator-Beispiel oben (z=100, 64×64×3):

⚠ Die Filterzahlen werden **in Gs Reihenfolge übernommen** (hier 64, 32) — der Encoder hat also
**fallende** Filterzahlen, anders als der Discriminator. Sieht falsch aus, ist es nicht: genau so
macht es Praktikum 08 (G: 32, 16 ⇒ E: 32, 16). Nicht „korrigieren".

```python
encoder = tf.keras.Sequential([
  tf.keras.layers.InputLayer((64, 64, 3)),
  tf.keras.layers.Conv2D(filters=64, kernel_size=5, strides=2, padding='same'),   # 32x32
  tf.keras.layers.BatchNormalization(), tf.keras.layers.ReLU(),
  tf.keras.layers.Conv2D(filters=32, kernel_size=5, strides=2, padding='same'),   # 16x16
  tf.keras.layers.BatchNormalization(), tf.keras.layers.ReLU(),
  tf.keras.layers.Flatten(),
  tf.keras.layers.Dense(units=100, activation='tanh')])       # = latent_dim

generator.trainable = False                                   # GAN einfrieren!
fanogan_autoencoder = tf.keras.Model(inputs=encoder.input,
                                     outputs=generator(encoder.output))
def score_samples(samples):
    return latent_loss(samples, fanogan_autoencoder(samples))
```

**Merksatz AnoGAN vs. f-AnoGAN:** AnoGAN optimiert z pro Sample zur Laufzeit; f-AnoGAN verlagert die Arbeit ins Encoder-Training — Score dann per Forward-Pass.
