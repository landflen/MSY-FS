# Blatt ⑤ — Rekonstruktionsbasierte Verfahren: AE, CAE, VAE, GAN, AnoGAN, f-AnoGAN (Kap. 7 + VAE aus 7a)

> Vorlage zum handschriftlichen Übertragen. Quellen: Foliensatz 07 (AE, GAN, AnoGAN, f-AnoGAN) + 07a Folien 28–35 (VAE).
> Deckt Aufgabentyp 3 (AE-Code schreiben) + Typ 9 (AnoGAN komplett) ab. Zielumfang: ~3 A4-Seiten.

---

## Grundidee Rekonstruktion (Folien 2–4)

- Curse of Dimensionality: benötigte Datenmenge steigt exponentiell; (dist_max−dist_min)/dist_min → 0 → Abstände werden nutzlos → **Dimensionsreduktion**
- Novelty Detection per Rekonstruktion: Modell (auf Normaldaten trainiert) kann nur Ähnliches rekonstruieren → **Rekonstruktionsfehler = Anomalie-Score** (hoch = Anomalie)

## Autoencoder (Folien 8–11)

- Encoder → **Code z (Latent Variable)** → Decoder; Ausgang rekonstruiert Eingang
- Loss: min Σᵢ ‖xᵢ − decoder(encoder(xᵢ))‖ → **unüberwacht, keine Labels nötig**
- z hat **niedrigere Dimension** als Eingabe — sonst lernt das Netz nur die Identität! (MC-Klassiker)
- Architektur: Encoder verjüngt sukzessive, Decoder = **gespiegelter** Encoder
- Traditionelle Anwendungen: Schicht-Initialisierung (heute selten); **Feature-Descriptor** (Encoder liefert Merkmale → z. B. AE auf Normaldaten + OCSVM auf encodierten Merkmalen)

## Convolutional Autoencoder — CAE (Folien 12–16)

- Dense-AE verliert Nachbarschaft/2D-Struktur → Faltungen verwenden
- **Downsampling im Encoder**: Pooling oder Conv mit strides=2
- **Upsampling im Decoder** — 2 Möglichkeiten:
  1. `UpSampling2D` + Interpolation (nearest/bilinear) → wird nicht gelernt, „verschmiert"
  2. **Transponierte Faltung** `Conv2DTranspose` (= Deconvolution, fractionally-strided conv) → gelerntes Upsampling; strides=2 **verdoppelt** H und W; padding='same'
- Typischer Aufbau: Eingabe → [Conv strides=2]×n → Flatten → Dense = z → Dense → Reshape → [Conv2DTranspose strides=2]×n → Rekonstruktion

**Shape-Regel für Blatt ②:** Conv2DTranspose, strides=2, padding='same' → 2H × 2W × filters

## Ensembles von AE / RandNet (Folien 17–25)

- Problem: Rekonstruktionsfehler einzelner AE instabil → Ensemble (vgl. iForest!)
- RandNet variiert: Initialisierung, Trainings-Untermenge, Verbindungen der Neuronen
- RandNet-Schicht = Dense mit zufälliger 0/1-**Maske auf den Gewichten** (elementweise Multiplikation); Maske wird 1× bei Erstellung gezogen (m·n Ziehungen mit Zurücklegen), bleibt dann konstant — Unterschied zu Dropout: nicht pro Schritt neu!
- Architektur: Encoder halbiert Neuronen je Schicht, Decoder verdoppelt; max. 7 Schichten; Code ≥ 3 Neuronen; **erste Encoder- und letzte Decoder-Schicht: Sigmoid, Rest ReLU**
- Training: 100 Netze, 300 Epochen, RmsProp, je 1/10 der Daten (Subsampling), Sample-Anzahl wächst ×1,01 pro Epoche
- Score: quadrat. Fehler je Netz → normalisieren mit Std der Trainingsfehler des Netzes → **Median** über alle Netze

## Variational Autoencoder — VAE (Folien 7a/28–35)

**Warum nicht normaler AE?** (Folie 28) Keine Kontrolle über die Verteilung des Latent Space; z lässt sich nicht zufällig ziehen → Decoder nicht als Datengenerator nutzbar.

**Idee:** Modelliere **Verteilungen** statt direkter Encodierung. A-priori-Verteilung p(z) wird vorgegeben (meist Standard-Normalverteilung N(0, 1)).

- **Encoder** lernt Verteilungsparameter: zwei parallele **lineare** Dense-Layers am Encoder-Ende liefern μ und Σ → z wird daraus **gesampelt**
- **Decoder** dekodiert das gesampelte z; Ausgabe ist ebenfalls eine Verteilung p(x|z), aus der gesampelt wird
- **Kosten**: Rekonstruktionsanteil + **Kullback-Leibler-Divergenz** zwischen erzeugter Verteilung und A-priori-Verteilung; hergeleitet über **ELBO** (Evidence Lower Bound): maximiere ELBO = minimiere −ELBO
  - KL gegen N(0, I) vereinfacht: D_KL = −½ · Σᵢ ( log σᵢ² + 1 − σᵢ² − μᵢ² )
- **Reparameterisierungs-Trick** (MC-Klassiker!): z ~ N(μ, σ²) ist nicht (stabil) differenzierbar → schreibe **z = μ + σ ⊙ ε mit ε ~ N(0, I)** → Zufall steckt in ε, Pfad durch μ/σ ist differenzierbar
- **Novelty Detection mit VAE** (Folie 35): z für dasselbe Sample x **mehrfach ziehen**, Rekonstruktionen mitteln → **Reconstruction Probability** p(x) als Score (je niedriger, desto eher Anomalie)
- Datengenerierung: z_g ~ N(0,1) ziehen → decoder(z_g) = neues Sample (→ Data Augmentation)

## GAN (Folien 27–36)

- **Generator** G: Eingabe Latent-Vektor z (feste Verteilung, z. B. Normal) → generiertes Sample; Architektur ≈ Decoder
- **Discriminator** D: Eingabe Sample → binär echt/generiert
- **Minimax-Game**: min_G max_D V = E_x[log D(x)] + E_z[log(1 − D(G(z)))]
- Training: **abwechselnd** pro Schritt; Kosten bleiben idealerweise beidseitig ~konstant
- Nachteile (MC!): Netze müssen gleich schnell lernen (D zu schnell → G lernt nie; G zu schnell → G „betrügt"); Trainingsfortschritt schwer beurteilbar → generierte Daten inspizieren; kein direkter Einfluss auf Generierung

**DCGAN-Empfehlungen (Folie 36) — Checkliste für Architektur-Aufgaben:**
1. G und D architektonisch ähnlich (gleiche Lerngeschwindigkeit)
2. KEINE Pooling-Layers → D: Conv strides=2; G: Conv2DTranspose strides=2
3. 5×5-Filter
4. BatchNorm in G und D
5. keine Fully-Connected-Layers
6. G: ReLU (Output: **tanh**); D: **Leaky ReLU** (0,2·x für x ≤ 0)

**GAN-Keras-Muster (Folien 30–33):**
```python
cross_entropy = tf.keras.losses.BinaryCrossentropy(from_logits=True)
# from_logits=True → D braucht KEINE Sigmoid am Ausgang!

def get_discr_loss(real_output, fake_output):
    real_loss = cross_entropy(tf.ones_like(real_output), real_output)   # echt = 1
    fake_loss = cross_entropy(tf.zeros_like(fake_output), fake_output)  # fake = 0
    return 0.5 * (real_loss + fake_loss)

def get_gen_loss(fake_output):
    return cross_entropy(tf.ones_like(fake_output), fake_output)  # G will D täuschen

@tf.function
def train_step(images):
    noise = tf.random.normal([tf.shape(images)[0], z_dim])   # z_dim z.B. 100
    with tf.GradientTape() as gen_tape, tf.GradientTape() as discr_tape:
        generated = generator_model(noise, training=True)
        real_out = discriminator_model(images, training=True)
        fake_out = discriminator_model(generated, training=True)
        gen_loss = get_gen_loss(fake_out)
        discr_loss = get_discr_loss(real_out, fake_out)
    # je Netz: tape.gradient(...) + eigener Optimizer.apply_gradients(...)
```
- kein `fit` möglich (2 Netze abwechselnd) → eigene train-Schleife über Epochen/Batches
- je Modell ein eigener Optimierer (z. B. `Adam(2e-4)`)

## AnoGAN (Folien 37–42) — Ablauf komplett (Aufgabentyp 9!)

**Training:** GAN ganz normal mit Normaldaten trainieren.

**Scoring eines neuen Samples x** (GAN-Parameter bleiben eingefroren!):
1. z zufällig initialisieren (aus A-priori-Verteilung)
2. n Iterationen (z. B. 500): L(x, z) nach **z** ableiten, z per Gradient Descent anpassen
3. finale Kosten L(x, z_n) = **Anomalie-Score**

**Kostenfunktion** (gewichtete Summe, λ z. B. 0,1):
- Residual Loss: L_res = Σ |x − G(z)| (Ähnlichkeit Sample ↔ generiertes Sample)
- Discrimination Loss: L_disc = Σ |D_k(x) − D_k(G(z))| — D_k = Ausgabe der k-ten Discriminator-Schicht (im Code: vorletzte Schicht als feature_model)
- L = (1−λ)·L_res + λ·L_disc

```python
generator_model.trainable = False
feature_model = tf.keras.Model(inputs=discriminator_model.input,
                               outputs=discriminator_model.layers[-2].output)
z = tf.Variable(tf.random.normal([samples.shape[0], latent_dim]))  # 1 z pro Sample
# train_step: loss = latent_loss(x, generator_model(z));
#             gradient nach [z], optimizer.apply_gradients auf [z]; 500 Iterationen
```

**Nachteil AnoGAN:** pro neuem Sample eigene z-Optimierung → langsam im Einsatz.

## f-AnoGAN (Folien 43–49)

**Idee:** Encoder E lernt, z direkt aus x zu berechnen → Scoring in einem Durchlauf, keine Iterationen.

**3 Trainingsphasen:**
1. GAN mit Normaldaten trainieren
2. **Encoder** trainieren (GAN eingefroren, gleiche Normaldaten; E am besten = „gespiegelter" Generator). Aufbau als Autoencoder: `E → G` (G als Decoder)
3. Scoring: Score(x) = L(x) = L_res + L_disc mit G(E(x)) — **eine** Vorwärtsrechnung

- Losses jetzt mit MSE: L_res = 1/n_x · ‖x − G(E(x))‖²; L_disc analog auf feature_model
- Encoder-Training: RMSprop, Loss = Mittel der Gesamtkosten über Batch

```python
autoencoder = tf.keras.Model(inputs=autoencoder_input,
                             outputs=generator_model(encoder_model_output))
def score_samples(samples):
    return latent_loss(samples, autoencoder(samples))
```

**Merksatz AnoGAN vs. f-AnoGAN:** AnoGAN optimiert z pro Sample zur Laufzeit; f-AnoGAN verlagert die Arbeit ins Encoder-Training — Score dann per Forward-Pass.
