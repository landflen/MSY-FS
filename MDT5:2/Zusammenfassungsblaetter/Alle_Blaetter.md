# MDT5/2 — Alle Zusammenfassungsblätter (Gesamtdokument)

> Zusammengeführte Version aller 7 Blätter zum Durchscrollen/Suchen.
> Die Einzeldateien sind die Originale — bei Änderungen dort dieses Dokument neu erzeugen.
> Klammer-Regel (23.7.): VAE, PCA, k-Means, LOF, Matrix Profiles = nicht klausurrelevant, entfernt.

## Farbschema — was beim Suchen zuerst ins Auge springt

| Farbe | Bedeutung | beim Abschreiben von Hand |
|---|---|---|
| <span style="color:#c0182c;font-weight:700">rot fett</span> | **Ankerbegriff** — Verfahren oder Thema, nach dem du im Aufgabentext suchst | dick unterstreichen / Rand-Marker |
| <span style="background:#fde3f1;color:#b3187a;font-weight:600">rosa</span> | **Stellgröße** — was man einstellt (Metaparameter) | einkreisen |
| <span style="color:#1057a8;font-weight:600">blau</span> | **Index** — Aufgabentyp-Nummer und Folienverweis | an den Rand schreiben |
| <span style="color:#b35c00;font-weight:700">orange</span> | **Falle / Verbot / typischer Fehler** | Ausrufezeichen an den Rand |

**Rot steht nur da, wo der Begriff auch erklärt wird** — an der ersten Stelle je Blatt, an der eine
Erklärung danebensteht (Tabellenzeile mit dem Begriff in der ersten Spalte, Abschnitt mit dem Begriff
in der Überschrift, oder „Begriff: / Begriff — …"). Bloße Erwähnungen bleiben schwarz; ein rotes Wort
ist damit die Zusage, dass die Antwort genau dort steht. Rosa: erstes Vorkommen pro Abschnitt.
Blau und Orange stehen überall, weil sie selten sind.

**Inhalt:**
1. Blatt ① Verfahrensübersicht + Grundbegriffe (Kap. 1/2)
2. Blatt ②③ Shapes & Keras (Kap. 3)
3. Blatt Abstand: kNN, iForest (Kap. 4)
4. Blatt ⑥ Evaluierung + Leakage (Kap. 5)
5. Blatt Probabilistisch: Mahalanobis, KDE, GMM (Kap. 6)
6. Blatt ⑤ Rekonstruktion: AE, CAE, GAN, AnoGAN (Kap. 7)
7. Blatt ④ SVM, OCSVM, Deep SVDD, GOAD (Kap. 8/8a)

---

# Blatt ① — Verfahrensübersicht (alle Kapitel) + Grundbegriffe

> Die wichtigste Tabelle für <span style="color:#1057a8;font-weight:600">Aufgabentypen 8</span> und 12 (Verfahrenswahl zu Daten-Plot begründen).
> Quellen: alle Foliensätze; Taxonomie nach <span style="color:#1057a8;font-weight:600">Folie 01</span>/33. Zielumfang: 2 A4-Seiten (Tabelle quer!).

---

## Grundbegriffe (Kap. 1 — für MC)

- **Anomalie**: "Patterns in data that do not conform to a well defined notion of normal behavior" (Chandola et al.)
- **Punktanomalie**: isolierter Punkt weicht ab. **Kontextanomalie**: nur im Kontext (Bsp. hohe Ausgaben an Weihnachten = normal)
- **Anomalieerkennung ≠ überwachtes Lernen!** Warum: kaum/keine Anomalien im Training; Ausprägungen unbekannt; auch das „unbekannte Unbekannte" soll erkannt werden
- **<span style="color:#c0182c;font-weight:700">Novelty</span> Detection** (= OOD Detection, Ein-Klassen-Problem): Training NUR mit Normaldaten; gelernt wird, was normal ist; Anomalien höchstens für Fine-Tuning/Test. **→ Schwerpunkt des Kurses!**
- **<span style="color:#c0182c;font-weight:700">Outlier</span> Detection**: Training mit ungelabelten Daten (Anomalien unerkannt drin). 2 Hauptanwendungen: **KDD** (neue Einblicke) + **Trainingsdaten-Bereinigung** (z. B. pro Klasse). Annahmen: Ausreißer selten, „anders"/weiter weg, niedrigere Dichte
- Expertensystem / ML (kein DL) / DL: Merkmale manuell/manuell/gelernt; Klassifikation manuell/gelernt/gelernt; Datenbedarf gering/mittel/sehr hoch; Nachvollziehbarkeit hoch/meist gegeben/kaum
- **Merkregel Deep vs. Shallow**: Deep = tiefes neuronales Netz steckt im Verfahren

## Taxonomie (Folie 01/33 — nachzeichnen!)

| | Distanz | Probabilistisch | Rekonstruktion | Klassifikation |
|---|---|---|---|---|
| **Deep** | — | — | Autoencoder, (VAE), f-AnoGAN | Deep SVDD, GOAD, CutPaste |
| **Shallow** | kNN, (LOF), iForest, (Matrix Profiles) | Histogramm, Mahalanobis, KDE, GMM | (PCA), (k-Means) | OC-SVM, SVDD |

**Eingeklammert auf der Folie = <span style="color:#b35c00;font-weight:700">NICHT</span> klausurrelevant — ALLES in Klammern** (Ansage Prof., geklärt 23.7.). Beim Nachzeichnen mitklammern, aber nicht lernen. **LOF, Matrix Profiles, VAE, PCA, k-Means** sind deshalb aus allen Blättern/Übungen entfernt (Blatt Clustering/PCA komplett gestrichen, VAE-Teil aus Blatt ⑤ und Übungsblatt 6 entfernt).

## Die große Verfahrenstabelle

| Verfahren | Score | Wichtigste <span style="background:#fde3f1;color:#b3187a;font-weight:600">Metaparameter</span> | Norm.? | Geeignet | Ungeeignet / Schwäche |
|---|---|---|---|---|---|
| **<span style="color:#c0182c;font-weight:700">kNN</span>-Abstand** | mittl. Abstand zu k Nachbarn | k, Abstandsmaß | JA | einfach, wenig Daten | langsam; hohe Dim. (Curse of Dim.); Rauschen |
| **<span style="color:#c0182c;font-weight:700">iForest</span>** | s = 2^(−E(h)/c(n)) ∈ [0;1], →1 Ausreißer | <span style="background:#fde3f1;color:#b3187a;font-weight:600">n_estimators</span> (100), max_samples (256), <span style="background:#fde3f1;color:#b3187a;font-weight:600">contamination</span> | **NEIN** | hohe Dim., große Daten, schnell | einzelne Bäume instabil (→ Ensemble) |
| **<span style="color:#c0182c;font-weight:700">Mahalanobis</span> / EllipticEnvelope** | (neg.) Mahalanobis-Abstand (Ellipse) | contamination | (robust ggü. Skala) | korrelierte Merkmale, **unimodal** | **multimodale Daten!** |
| **<span style="color:#c0182c;font-weight:700">KDE</span>** | log-Dichte | <span style="background:#fde3f1;color:#b3187a;font-weight:600">Bandbreite</span> h (GridSearch auf Train-log-Dichte) | JA | **beliebige/multimodale Verteilungen** | h-Wahl; alle Trainingspunkte nötig |
| **<span style="color:#c0182c;font-weight:700">GMM</span>** | Dichte der Mischverteilung | Modenzahl k, Init | JA | multimodal, wenn k bekannt | EM langsam, lokale Minima |
| **<span style="color:#c0182c;font-weight:700">Autoencoder</span>** | Rekonstruktionsfehler | Architektur, dim(z) < dim(x)! | JA (z. B. [0;1]) | Bilder/hochdim., viele Daten | Fehler instabil (→ Ensemble/RandNet); braucht viele Daten |
| **<span style="color:#c0182c;font-weight:700">AnoGAN</span>** | L = (1−<span style="background:#fde3f1;color:#b3187a;font-weight:600">λ</span>)L_res + λL_disc nach z-Optimierung | λ (0,1), Iterationen (500), z_dim | JA | Bilder, gute Datenqualität | **langsam: z-Optimierung pro Sample!**; GAN-Training heikel |
| **<span style="color:#c0182c;font-weight:700">f-AnoGAN</span>** | wie AnoGAN, aber via Encoder G(E(x)) | wie AnoGAN + Encoder | JA | wie AnoGAN, schnelles Scoring | 3-stufiges Training |
| **<span style="color:#c0182c;font-weight:700">OC-SVM</span>** | Abstand zur Trennebene (vom Ursprung) | **<span style="background:#fde3f1;color:#b3187a;font-weight:600">ν</span>** (Ausreißeranteil), **<span style="background:#fde3f1;color:#b3187a;font-weight:600">γ</span>** (RBF) | **JA! (Standardis.)** | wenig Daten, hohe Dim. | große Datenmengen (Training langsam); braucht RBF |
| **<span style="color:#c0182c;font-weight:700">SVDD</span>** | Abstand zur Kugeloberfläche | ν, Kernel | JA | wie OC-SVM (Gauß-Kernel: äquivalent!) | wie OC-SVM |
| **<span style="color:#c0182c;font-weight:700">Deep SVDD</span>** | ‖φ(x)−c‖² − R² (>0 = Anomalie) | ν, λ (Weight Decay), Architektur | JA | Bilder/hochdim., viele Daten | **<span style="color:#b35c00;font-weight:700">Verbotsliste</span>!** (Bias, gedeckelte Akt., c) |
| **<span style="color:#c0182c;font-weight:700">GOAD</span>** | −Σ log P(richtige Transformation) | M Transformationen, λ₁=0,1, λ₂=10, s=1 | JA | Bilder + allgemeine Daten (affine T.) | Wahl der Transformationen |
| **<span style="color:#c0182c;font-weight:700">CutPaste</span>** | Gauß-Dichte im Merkmalsraum | Patch-Parameter | JA | **kleine lokale Defekte** (Fertigung) | globale Anomalien |

## Entscheidungsbaum für Verfahrenswahl-Aufgaben (Typ 8/12)

1. **Plot ansehen: eine kompakte Punktwolke (unimodal)?** → Mahalanobis/Elliptic Envelope ok
2. **Mehrere Cluster (multimodal)?** → KDE, GMM; Elliptic Envelope FALSCH (Ellipse über alles)
3. **Cluster nicht kugelig / verschachtelt (Ringe, Bänder)?** → KDE, OCSVM (RBF) ok
4. **Hochdimensional (Bilder)?** → Deep-Verfahren (AE, Deep SVDD, GOAD, f-AnoGAN); Abstand/KDE leiden unter Curse of Dim.; iForest ok
5. **Wenige Trainingsdaten?** → OCSVM stark, Deep-Verfahren FALSCH (Datenhunger)
6. **Kleine lokale Bilddefekte?** → CutPaste
7. Bei Begründung IMMER nennen: passt die Modellannahme (Verteilungsform/Clusterform/Linearität) zum Plot + Datenmenge/Dimension

## Merkzettel Normalisierung (Kap. 2)

- Min-Max → [0;1]: x′ = (mᵢ − minᵢ)/(maxᵢ − minᵢ); empfindlich ggü. Ausreißern; `MinMaxScaler`
- <span style="color:#c0182c;font-weight:700">Standardisierung</span> (Z-Transf.): x′ = (mᵢ − μᵢ)/σᵢ → μ=0, σ=1; robuster, kein fester Bereich; `StandardScaler`
- min/max/μ/σ IMMER nur aus Trainingsdaten (fit auf Train, transform auf Train+Test) → sonst Data Leakage
- Nötig bei allem, was Abstände/Skalarprodukte rechnet (kNN, KDE, SVM/OCSVM, NN-Eingaben); <span style="color:#b35c00;font-weight:700">NICHT</span> nötig bei iForest (nur Splits)

**Kontrastpaar (nicht mischen!):** <span style="color:#c0182c;font-weight:700">Min-Max</span> = **fester Bereich**, Default [0;1], [−1;1] nur mit
`feature_range=(-1,1)`; Test kann den Bereich verlassen (Trainings-Max). Z-Transf. = **kein**
fester Bereich, nur μ=0/σ=1. „Min-Max-Standardisierung" gibt es nicht.

## Kleingedrucktes zu Scores & sklearn (S2-Nachtrag)

- **iForest-Grenzfälle:** E(h)→0 ⇒ s→1 (Anomalie); E(h)=c(n) ⇒ s=0,5 (unauffällig);
  E(h)→n−1 ⇒ s→0 (sicher normal). Baumtiefe log₂(n_sub), weil Anomalien **kurze** Pfade haben.
- **<span style="background:#fde3f1;color:#b3187a;font-weight:600">contamination</span> = erwarteter Anteil an Ausreißern in den Daten** (Anteil, keine Anzahl) ⇒ legt
  den **Schwellwert** der ±1-Entscheidung fest, kein Formparameter. `'auto'` = feste Schwelle aus
  der Score-Definition. **AUC ändert sich dadurch nicht** (schwellwertunabhängig).
- **sklearn-Dreizeiler:** `fit` lernt (bei Novelty **nur auf Normaldaten**) — `predict` liefert
  **+1 = normal, −1 = Anomalie** — `score_samples` gibt den kontinuierlichen Score (iForest:
  negiert in [−1;0], niedriger = anomaler).

---

# Blatt ②+③ — Shapes & Keras-Spickzettel (Kap. 3)

> Vorlage zum handschriftlichen Übertragen. Quelle: Foliensatz 03 (S. 24, 35–45, 47–55).
> Zielumfang: 2 handgeschriebene A4-Seiten.

---

## ② Shape-Rechenregeln

Eingabe pro Schicht: H × W × C (Höhe × Breite × Kanäle)

| Schicht | Ausgabe-Shape | Merke |
|---|---|---|
| Conv2D, padding='same', strides=1 | H × W × **filters** | räumlich gleich, Kanäle = Filteranzahl |
| Conv2D, padding='same', strides=2 | ⌈H/2⌉ × ⌈W/2⌉ × filters | halbiert + neue Kanalzahl |
| Conv2D, padding='valid' (= ohne), strides=1 | (H−k+1) × (W−k+1) × filters | pro Seite ⌊k/2⌋ Rand weg (k = Kernelgröße) |
| MaxPool2D 2×2 | H/2 × W/2 × C | halbiert, **Kanäle unverändert!** |
| Flatten | H·W·C (Vektor) | z. B. 2×2×256 → 1024 |
| Dense(units=n) | n | |
| <span style="color:#c0182c;font-weight:700">Dropout</span> / <span style="color:#c0182c;font-weight:700">BatchNorm</span> / RandomTranslation | unverändert | ändern <span style="color:#b35c00;font-weight:700">NIE</span> die Shape |

**Kontrollfragen bei Shape-Aufgaben (<span style="color:#1057a8;font-weight:600">Typ 2/5</span>):**
- Kanalzahl nach Conv = filters, nach Pooling = unverändert
- Räumliche Größe darf nie < Kernelgröße werden → „zu viel Pooling" = Architekturfehler
- Letzte Dense: units = Klassenanzahl (Softmax) bzw. 1 (binär, Sigmoid)

**Auflösung halbieren — zwei Wege (<span style="color:#1057a8;font-weight:600">Folie 42</span>), beide H/2 × W/2:**
| | MaxPool2D 2×2 | Conv2D(strides=2) |
|---|---|---|
| Parameter | **keine** (feste Vorschrift) | Kernelgewichte (Zahl unabhängig von strides) |
| Auswahl | Maximum je 2×2-Fenster, pro Kanal getrennt → stärkste Aktivierung bleibt | **gelernt**: Kernelgewichte entscheiden |
| Rechenweg | Faltung erst auf voller Auflösung, dann ausdünnen | Kernel springt um 2 → Zwischenpositionen gar nicht berechnet (billiger) |
| Kanalzahl | unverändert | = filters |

**Gewichte zählen (<span style="color:#1057a8;font-weight:600">Folie 45</span>):**
- Conv2D: C_in · k · k · filters   (Bias: + filters)
- Dense: n_in · n_out   (Bias: + n_out)
- Bsp. 1. Schicht VGG: 3·3·3·32 = 864;  2. Schicht: 32·3·3·32 = 9 216

**Beispiel-Kette (mod. VGG16, <span style="color:#1057a8;font-weight:600">Folie 43</span>):**
32×32×3 → 32×32×32 → 16×16×64 → 8×8×128 → 4×4×256 → 2×2×256 → Flatten → 1024 → 1024 → 7 (Softmax)

---

## Aktivierung + Kostenfunktion nach Aufgabe (Folien 11–21)

**Warum überhaupt eine (nicht-lineare) Aktivierung in JEDER Schicht?**
Ohne Aktivierung ist eine Schicht nur eine lineare Abbildung (W·x + b). Mehrere lineare
Abbildungen hintereinander ergeben wieder **eine einzige** lineare Abbildung → das ganze tiefe
Netz lässt sich durch eine Schicht ersetzen, die Tiefe ist wertlos, nur linear trennbare
Probleme lösbar. **Nicht** mit Vanishing/Exploding Gradient verwechseln: das ist die Frage,
**welche** Nichtlinearität (Sigmoid/tanh → ReLU), nicht **ob** eine nötig ist.



| Aufgabe | Ausgabeneuronen | Aktivierung am Ausgang | Loss (Keras-Name) |
|---|---|---|---|
| Regression | 1 pro Wert | **keine** | MSE: C = 1/(2N) · Σᵢ ‖z(xᵢ) − yᵢ‖² |
| Binäre Klassifikation | 1 | Sigmoid σ | binary_crossentropy: C = −1/N · Σᵢ [yᵢ·log a(xᵢ) + (1−yᵢ)·log(1−a(xᵢ))] |
| Multi-Klasse (genau 1 richtig) | 1 pro Klasse | **Softmax** | categorical_crossentropy: C = −1/N · Σᵢ log a_k (k = richtige Klasse); Labels als One-Hot |
| Multi-Label (mehrere möglich) | 1 pro Klasse | Sigmoid **pro Neuron** | Summe der binären Kreuzentropien |
| Hidden Layers (immer) | — | **ReLU** | — |

<span style="color:#c0182c;font-weight:700">Softmax</span>: a_j = e^(z_j) / Σ_k e^(z_k)  → Summe aller Ausgaben = 1 (echte Wahrscheinlichkeitsverteilung; Sigmoid pro Neuron leistet das <span style="color:#b35c00;font-weight:700">NICHT</span>)

---

## ③ Keras-Grundgerüst (Folie 24 + 48–54, alles in einem)

```python
import tensorflow as tf
lmbda = 1e-4       # Weight Decay
drop_rate = 0.5

net = tf.keras.Sequential([
    tf.keras.layers.Input((32, 32, 3)),          # Dense-Netz: Input((32*32*3,))
    tf.keras.layers.RandomTranslation(            # Data Augmentation (nur im Training aktiv)
        height_factor=0.1, width_factor=0.1,
        fill_mode='reflect'),                     # Spiegeln statt Zero-Padding!
    tf.keras.layers.Conv2D(filters=8, kernel_size=7,
        strides=2, padding='same',                # strides=2 = Subsampling-Alternative zu MaxPool
        kernel_regularizer=tf.keras.regularizers.L2(lmbda),
        activation='relu'),
    tf.keras.layers.MaxPool2D(),                  # 2x2, halbiert H und W
    tf.keras.layers.BatchNormalization(),
    tf.keras.layers.Flatten(),
    tf.keras.layers.Dense(units=200, activation='relu'),
    tf.keras.layers.Dropout(drop_rate),           # wirkt auf Schicht DAVOR
    tf.keras.layers.Dense(units=7, activation='softmax'),
])

net.compile(optimizer=tf.keras.optimizers.SGD(learning_rate=0.1),
            loss='categorical_crossentropy',
            metrics='accuracy')

net.fit(x=train_x, y=train_y, batch_size=128, epochs=10,
        validation_data=(valid_x, valid_y), shuffle=True)

predictions = net.predict(test_x)
```

1D-Varianten: Conv1D, MaxPool1D (Zeitreihen statt Bilder)

**<span style="color:#b35c00;font-weight:700">⚠</span> Welche Zahlen im Gerüst sind BEISPIELWERTE?** Beim Abschreiben in der Klausur nur die Struktur
übernehmen, die Zahlen kommen aus der Aufgabenstellung:
`Input((32,32,3))` = Bildgröße · `filters=8`, `kernel_size=7` = frei gewählt (Kurs sonst 3 oder 5) ·
`units=200` = frei · **`units=7` = ANZAHL DER KLASSEN** · `activation='softmax'` nur bei
Mehrklassen (2 Klassen ⇒ sigmoid, Regression ⇒ keine) · `drop_rate`, `lmbda`, `learning_rate`,
`batch_size`, `epochs` = frei.
**Argumentnamen immer ausschreiben** (`filters=`, `kernel_size=`, `units=`) — sonst vertauscht man
unter Zeitdruck die ersten beiden Positionen: `Conv2D(filters, kernel_size, …)`, `Dense(units, …)`.

---

## Schnellfakten (Nachschlagen in <10 s)

**Vanishing/Exploding Gradient (<span style="color:#1057a8;font-weight:600">Folien 28–33</span>):**
- Backprop = Kettenregel rückwärts; pro Schicht ein Faktor σ'(z)·w ins Produkt
- max σ' = **0,25** → 4 Schichten: 0,25⁴ ≈ 0,004; 10 Schichten: 0,25¹⁰ ≈ 10⁻⁶
- tanh: max Ableitung 1,0 → schwächer, Problem bleibt
- vordere Schichten lernen kaum → Netz lernt fast nur in letzten Schichten
- große Gewichte (Faktor > 1) → Exploding; beides = „Unstable Gradient"

**ReLU (<span style="color:#1057a8;font-weight:600">Folie 34</span>):** max(0, z); Ableitung 1 (z>0) oder 0 (z≤0) → Gradient stabil.
Gefahr: Dead Neurons bei z≤0 → gute Initialisierung nötig: **He-Initialisierung** (= doppelte Varianz der Xavier-Init.)

**Regularisierung — die 4 Techniken (<span style="color:#1057a8;font-weight:600">Folien 47–55</span>):**
| Technik | Kernidee | <span style="background:#fde3f1;color:#b3187a;font-weight:600">Metaparameter</span> | Keras |
|---|---|---|---|
| L2 / Weight Decay | Strafterm C + <span style="background:#fde3f1;color:#b3187a;font-weight:600">λ</span>/(2n_w)·Σw² → hohe Gewichte nur bei echtem Vorteil | λ | regularizers.L2 als kernel_regularizer |
| Dropout | implizites Ensemble; pro Trainingsschritt zufällig Neuronen deaktiviert; nach Training ALLE aktiv | Drop-Rate | layers.Dropout(rate) |
| Data Augmentation | Daten zufällig transformieren (Translation, Rotation, Helligkeit, Rauschen); an Problem anpassen! | Transformationen | layers.RandomFlip/-Translation/-Rotation |
| <span style="color:#c0182c;font-weight:700">Batch Normalization</span> | Covariate Shift: Verteilungen verschieben sich schichtweise → Eingaben je Schicht über Batch standardisieren; <span style="background:#fde3f1;color:#b3187a;font-weight:600">γ</span> (Skalierung), β (Shift) mitgelernt: x_BN = γ·x_std + β | — | layers.BatchNormalization |

**Training (<span style="color:#1057a8;font-weight:600">Folien 22–23</span>):**
- <span style="background:#fde3f1;color:#b3187a;font-weight:600">Learning Rate</span> zu groß → Minimum übersprungen / divergiert; zu klein → langsam, bleibt in lokalem Minimum
- SGD: Gradient nur auf Batch (Teilmenge) → schneller
- **Schritt** = 1 Optimierung mit 1 Batch; **Epoche** = alle Trainingsdaten 1× verwendet

**Metaparameter (nicht gelernt, vom Entwickler):** Schichten, Neuronen/Filter pro Schicht, Kernelgröße, Aktivierung, Learning Rate, Batchgröße, λ, Drop-Rate, Augmentierungen.
**Gelernte Parameter:** Gewichte W, Biases b (+ γ, β bei BatchNorm)

---

## Fehlerfinder-Checkliste (Aufgabentyp 4/5)

1. Loss passt nicht zur Ausgabe-Aktivierung? (softmax ↔ categorical, sigmoid ↔ binary, Regression ↔ keine + MSE)
2. units der letzten Dense ≠ Klassenanzahl?
3. Zu viel Pooling → räumliche Größe kleiner als Kernel / Faktor passt nicht zur Eingabegröße?
4. Reshape/Flatten-Größe stimmt nicht mit H·W·C überein?
5. **`Flatten()` fehlt ganz vor der ersten Dense?** Dense wirkt nur auf die **letzte Achse** —
   aus 1×1×64 wird dann 1×1×5 statt (5,) und passt nicht zu den Labels. Kein Crash beim Bauen,
   deshalb leicht zu übersehen.
6. **Klassenanzahl vs. Loss:** 5 Klassen mit `binary_crossentropy` ist <span style="color:#b35c00;font-weight:700">falsch</span> — ab 3 Klassen
   `categorical_crossentropy` (One-Hot) bzw. `sparse_categorical_crossentropy` (Integer-Labels).
7. <span style="color:#c0182c;font-weight:700">Data Leakage</span>: scaler.fit() / fit_transform() auf Testdaten? → fit nur auf Train, transform auf beide
8. Augmentation, die das Label zerstört (z. B. 6 ↔ 9 bei Rotation)?

---

# Blatt Kap. 4 — Abstandsbasierte Verfahren (kNN, iForest)

> Vorlage zum handschriftlichen Übertragen. Quelle: Foliensatz 04 (kNN, iForest).
> Zielumfang: ~1 handgeschriebene A4-Seite.
> **Foliensatz 03a (LOF, Matrix Profiles) ist optional und nicht klausurrelevant** — auf der
> Übersichts-Folie eingeklammert, deshalb hier bewusst weggelassen.

---

## k-Nearest-Neighbor (Folien 04/5–6)

- **Training = nur Speichern** aller Trainingspunkte (Normaldaten). Kein echtes Lernen!
- **Score:** z. B. mittlerer Abstand zu den k nächsten Nachbarn → hoher Abstand = Anomalie
- <span style="background:#fde3f1;color:#b3187a;font-weight:600">Metaparameter</span>: **k**, **Abstandsmaß** (z. B. euklidisch)
- Schwächen (klausurrelevant für Verfahrenswahl!):
  - langsam (alle Abstände rechnen)
  - anfällig für Ausreißer in Normaldaten + Rauschen
  - **Curse of Dimensionality**: je höher die Dimension, desto ähnlicher alle Abstände
- sklearn: `sklearn.neighbors.NearestNeighbors` (unüberwacht, Abstände);
  `KNeighborsClassifier` nur für überwachtes Lernen

## Isolation Forest (Folien 04/8–13)

**Idee:** Anomalien lassen sich leichter isolieren. Zufällige Splits (zufälliges Merkmal, zufälliger Wert) → Baum bis alle Punkte isoliert. **Anomalien = kurze Pfade** h(x).

- Ensemble aus vielen Bäumen → mittlere Pfadlänge E(h(x)); Normalisierung mit c(n) = mittlere Pfadlänge erfolgloser Suche im Binärbaum:
  **s(x,n) = 2^(−E(h(x))/c(n))**
- Score-Interpretation:
  | E(h(x)) | s | Bedeutung |
  |---|---|---|
  | → 0 | → 1,0 | wahrscheinlich Ausreißer |
  | → c(n) | → 0,5 | unauffällig |
  | → n−1 | → 0,0 | sicher Normalpunkt |
- **Cluster-Problem:** dichte Cluster erschweren Isolation → **Subsampling pro Baum** (ohne Zurücklegen)
- Standardwerte (Zahlen fürs Nachschlagen): **n_sub = 256**, max. Baumtiefe **log₂(n_sub)**, **100 Bäume**
- Keine Abstandsberechnung → **Normalisierung <span style="color:#b35c00;font-weight:700">NICHT</span> nötig**, gut bei hohen Dimensionen, schnell
- sklearn: `sklearn.ensemble.IsolationForest`
  - `n_estimators` (Bäume), `max_samples` (Subsampling), `contamination`, `random_state`
  - `fit` trainiert, `predict` klassifiziert

---

## Schnellvergleich fürs Verfahrenswahl-Blatt ①

| | kNN-Abstand | iForest |
|---|---|---|
| Idee | Abstand zu k Nachbarn | Isolierbarkeit (Pfadlänge) |
| Stärke | einfach, intuitiv | schnell, hohe Dim., Cluster ok (Subsampl.) |
| Schwäche | langsam, Curse of Dim., Rauschen | zufällige Schwankungen (→ Ensemble) |
| <span style="color:#c0182c;font-weight:700">Normalisierung</span> | JA (abstandsbasiert) | NEIN (nur Splits) |
| <span style="background:#fde3f1;color:#b3187a;font-weight:600">Metaparameter</span> | k, Abstandsmaß | <span style="background:#fde3f1;color:#b3187a;font-weight:600">n_estimators</span> (100), max_samples (256), <span style="background:#fde3f1;color:#b3187a;font-weight:600">contamination</span> |

---

# Blatt ⑥ — Evaluierung, Metriken, Data-Leakage-Checkliste (Kap. 5)

> Vorlage zum handschriftlichen Übertragen. Quelle: Foliensatz 05.
> Zielumfang: ~2 handgeschriebene A4-Seiten. Deckt <span style="color:#1057a8;font-weight:600">Aufgabentyp 4</span> (Leakage finden) + MC ab.

---

## Metriken-Formelblock (Folien 16–21) — mit Confusion Matrix

<span style="color:#c0182c;font-weight:700">Confusion Matrix</span> (Zeile = tatsächlich, Spalte = erkannt):

|  | erkannt K | erkannt K̄ |
|---|---|---|
| **wirklich K** | TP | FN |
| **wirklich K̄** | FP | TN |

| Metrik | Formel | Frage, die sie beantwortet |
|---|---|---|
| Sensitivität / TPR / **<span style="color:#c0182c;font-weight:700">Recall</span>** | TP / (TP+FN) | Welcher Anteil der Klasse K wurde gefunden? |
| Spezifizität / TNR | TN / (TN+FP) | Welcher Anteil der anderen Klasse richtig? |
| Accuracy | (TP+TN) / alle | Anteil richtig insgesamt — **nur bei balancierten Daten!** |
| Balanced Accuracy | ½·(TPR + TNR) | Mittel über beide Klassen |
| **<span style="color:#c0182c;font-weight:700">Precision</span>** | TP / (TP+FP) | Welcher Anteil der als K Erkannten ist wirklich K? |
| F1 | 2·(prec·rec)/(prec+rec) | harmonisches Mittel |
| F_β | (1+β²)·(prec·rec)/(β²·prec+rec) | β=0,5 → Precision wichtiger; β=2 → Recall wichtiger |

**Merkbeispiel (<span style="color:#1057a8;font-weight:600">Folie 19</span>/20, unbalanciert, K selten):**
- K wird nie erkannt → acc 0,90 aber bal. acc 0,50 → Accuracy lügt!
- K wird doppelt so oft erkannt wie vorhanden → bal. acc 0,95, aber Precision 0,50 → auch bal. acc kann lügen, erst Precision deckt auf

**ROC & <span style="color:#c0182c;font-weight:700">AUC</span> (<span style="color:#1057a8;font-weight:600">Folie 25</span>):**
- <span style="color:#c0182c;font-weight:700">ROC</span> = Plot **TPR gegen FPR** für alle möglichen Schwellwerte
- AUC = Fläche darunter, Interpretation (MC-Klassiker!): **Wahrscheinlichkeit, dass eine zufällige Anomalie einen höheren Score bekommt als ein zufälliger Normalpunkt**
- AUC = 0,5 → Raten; AUC = 1,0 → perfekte Trennung
- sklearn: `roc_curve(true_y, scores, pos_label=1)` → fpr, tpr, thresholds; `roc_auc_score(true_y, scores)`

## Schwellwert wählen (Praktikum 07)

**<span style="color:#c0182c;font-weight:700">Schwellwert</span> = Score-Wert (y-Achse). Ausreißeranteil = Anteil der Punkte (x-Achse). Nicht dasselbe!**
Der **sortierte Score-Plot** ist die Übersetzung zwischen beiden.

Drei Wege, je nach Vorwissen:

| Vorwissen | Methode |
|---|---|
| nichts (blind) | sortierten Score-Plot: dort schneiden, wo die Kurve **senkrecht** wird |
| Ausreißeranteil bekannt | **Quantil**: `sorted_scores[int((1−ratio)·n)]` |
| Labels vorhanden | **ROC-Knie**: `best = np.argmin(fpr**2 + (1−tpr)**2)` → `thr[best]` |

- **Pflicht-Gegenprobe:** Schwelle → Indexposition ablesen → `n − Index` = Anzahl Alarme → ist dieser **Anteil** als Ausreißeranteil plausibel? (35 % geflaggt ist keine Outlier Detection.)
- Im sortierten Plot: **Schulter** (flacht ab, steigt weiter) = zweite **Normal**gruppe; erst die **Senkrechte** sind die Ausreißer. Das Histogramm taugt dafür **nicht** — die interessante Region ist genau die, wo die Balken schon fast 0 sind.
- **Knie = OBERES Ende eines senkrechten ROC-Stücks** (senkrecht heißt: gleiche FPR, mehr TPR ⇒ gratis). Danach prüfen, was der letzte TPR-Rest kostet.
- **Fallstrick Quantil:** unterstellt, die Ausreißer seien die **höchsten** Scores. Bei schwerem **Oberschwanz der Normaldaten** (im Boxplot: Ausreißerpunkte der Normal-Box reichen über den Median der Outlier-Box) liegen die Anomalien in einem **mittleren Band** → Quantil schneidet darüber ab, TPR bricht ein **trotz guter AUC**.
- **Diagnoseregel:** hohe AUC + schlechte TPR ⇒ falsche **Schwelle**. Niedrige AUC ⇒ schlechtes **Modell**. Immer AUC **und** Boxplot ansehen, nie nur die TPR eines Betriebspunkts.

## Bias-Variance (Folie 3)

- **Bias** = falsche Modellannahmen → <span style="color:#b35c00;font-weight:700">Underfitting</span> (auf Trainingsdaten sichtbar)
- **Varianz** = Anfälligkeit für Rauschen → <span style="color:#b35c00;font-weight:700">Overfitting</span> (erst auf Validierungs-/Testdaten sichtbar)
- Beide nicht gleichzeitig minimierbar; Overfitting-Maß = Differenz Trainings- vs. Validierungsergebnis

## Datenaufteilung (Folien 4–9)

- Train / Validierung / Test: **disjunkt!** Trennung beginnt schon bei der Vorverarbeitung
- Abhängigkeiten beachten: z. B. alle Samples eines Probanden in NUR eine Teilmenge (sklearn: Parameter `groups`)
- Validierung → <span style="background:#fde3f1;color:#b3187a;font-weight:600">Metaparameter</span> einstellen; **Test → nur einmal ganz am Ende** (bei Fehlschlag „verbraucht")
- Wenig Daten → **k-Fold Cross Validation**: Testdaten zuerst abspalten, Rest in k Teilmengen, jede 1× Validierung; Ergebnis = Mittelwert ± Std
- sklearn nutzt standardmäßig **stratified** CV (Klassenverhältnisse bleiben in jedem Fold erhalten)
- Metaparameter-Suche: `GridSearchCV(pipe, param_grid, cv=5, refit=False)` → pro Kombination eine komplette CV

**Sonderfall Novelty Detection (<span style="color:#1057a8;font-weight:600">Folien 12–14</span>, klausurtypisch!):**
Standard-CV verteilt Anomalien auch in die Trainingsfolds — bei Novelty Detection dürfen dort aber NUR Normaldaten sein. Lösung: eigene cv-Liste an GridSearchCV übergeben:
1. Indizes in Normal / Anomalie trennen
2. Normal-Indizes mischen (`np.random.shuffle`)
3. `KFold().split()` NUR auf Normal-Indizes
4. Anomalie-Indizes per `np.concatenate` **jeder Validierungsmenge** hinzufügen
→ Form: Liste von Tupeln `[(train_idx, valid_idx), …]`

## Korrekte Evaluierungs-Pipeline (Folie 11 — auswendig können!)

```python
pipe = Pipeline([('scaler', MinMaxScaler()), ('clf', KNeighborsClassifier())])

train_data, test_data, train_labels, test_labels = train_test_split(
    data, labels, test_size=0.2, random_state=123)   # 1. Split ZUERST

grid_search = GridSearchCV(estimator=pipe,
    param_grid={'clf__n_neighbors': [5, 10, 15, 20]},
    cv=5, refit=False, n_jobs=-2)
grid_search.fit(train_data, train_labels)             # 2. Suche NUR auf Train

pipe.set_params(**grid_search.best_params_)
pipe.fit(train_data, train_labels)                    # 3. Finale Pipeline auf Train
np.mean(pipe.predict(test_data) == test_labels)       # 4. Test EINMAL am Ende
```

Warum Pipeline? Scaler + Klassifikator werden als **eine Einheit** behandelt → bei jeder CV-Teilung wird der Scaler nur auf dem jeweiligen Trainings-Fold gefittet. Testdaten werden mit Trainings-Statistik skaliert.

## Data-Leakage-Checkliste (Aufgabentyp 4 — Code-Fehler finden)

1. `scaler.fit()` oder `fit_transform()` auf **Gesamtdaten oder Testdaten**? → <span style="color:#c0182c;font-weight:700">Leakage</span>! (fit nur Train)
2. `train_test_split` **nach** der Normalisierung? → Leakage! (Split muss zuerst kommen)
3. GridSearchCV/CV **ohne Pipeline**, aber mit vorab global skalierten Daten? → Leakage in jeden Fold
4. Testdaten mehrfach benutzt (nach Metaparameter-Anpassung nochmal getestet)? → Testdaten verbraucht
   - auch: Metaparametersuche und finale Bewertung auf **derselben** Datenmenge? → die „beste" Parameterwahl ist an genau diese Daten angepasst, Testergebnis zu optimistisch
5. Abhängige Samples (gleicher Proband/gleiche Serie) in Train UND Test? → verstecktes <span style="color:#b35c00;font-weight:700">Overfitting</span>
6. Novelty Detection: Anomalien in Trainingsfolds der CV? → falsche Aufteilung (s. o.)
7. Accuracy bei stark unbalancierten Daten als einzige Metrik? → falsche Metrik (bal. acc / Precision+Recall / AUC)
8. Benutzt die **Vorverarbeitung die Labels**? (z. B. Imputation mit `median` getrennt nach Klasse) → schwerste Form von Leakage: Das Label steckt danach im Merkmal selbst. Bei neuen Daten ist das Label unbekannt → Modell wirkt im Test gut, bricht im Feld ein. Korrekt: **ein** Median pro Merkmal, nur auf den Trainingsdaten berechnet.

**<span style="color:#b35c00;font-weight:700">Achtung</span>, kein Fehler:** Beim Novelty-CV-Rezept (s. o.) stehen in jedem Fold **dieselben** Anomalien — das ist methodenbedingt so gewollt, nicht <span style="color:#b35c00;font-weight:700">falsch</span>. Als Einschränkung formulieren: Streuung über die Folds wird dadurch unterschätzt.

## Keras-Metriken (Folie 24)

```python
net.compile(optimizer=tf.keras.optimizers.Adam(),
            loss='categorical_crossentropy',
            metrics=[tf.keras.metrics.CategoricalAccuracy(),
                     tf.keras.metrics.Precision(),
                     tf.keras.metrics.Recall()])
```

---

# Blatt — Probabilistische Verfahren (Mahalanobis, Histogramm, KDE, GMM) (Kap. 6)

> Vorlage zum handschriftlichen Übertragen. Quelle: Foliensatz 06.
> Zielumfang: 1–1,5 handgeschriebene A4-Seiten.

---

## Grundprinzip (Folien 2–5)

- Schätze **Wahrscheinlichkeitsdichtefunktion (PDF)** der Normaldaten → **Dichte = Anomalie-Score** (niedrige Dichte = Anomalie)
- Wahrscheinlichkeiten nur **relativ** aussagekräftig → deshalb Scores statt absoluter Schwellen
- PDF (stetig): kann Werte > 1 annehmen; Fläche = genau 1; P(exakter Punkt) = 0, Wahrscheinlichkeit nur als Integral
- Kursannahme: Daten sind normalverteilt oder Mischung aus Normalverteilungen

## 3σ-Daumenregel → Mahalanobis (Folien 12–18)

**Stufe 1 — Daumenregel:** Ausreißer = weiter als 3σ vom Mittelwert. Pro Merkmal einzeln → implizite Annahme unabhängiger Merkmale → ignoriert Korrelationen (achsenparalleles Rechteck/Kreuz statt Ellipse)

**Stufe 2 — Mahalanobis-Abstand** (multivariate Normalverteilung, log der PDF):
- D_M = √( (x−μ)ᵀ · Σ⁻¹ · (x−μ) )
- Interpretation: **Abstand in Standardabweichungen** unter Berücksichtigung der Kovarianzen → Schwelle D_M ≤ 3 definiert eine **Ellipse**
- Σ = Kovarianzmatrix (Diagonale: Varianzen, sonst Kovarianzen)
- sklearn: `EmpiricalCovariance` (naiv, ausreißeranfällig) vs. `MinCovDet` (robust); Methode `mahalanobis` liefert **quadrierten** Abstand

**Stufe 3 — <span style="color:#c0182c;font-weight:700">Elliptic Envelope</span>:** Schwelle nicht fix bei 3, sondern an Daten angepasst
```python
from sklearn.covariance import EllipticEnvelope  # nutzt robuste Kovarianz-Schätzung
clf = EllipticEnvelope(contamination=0.1)        # Anteil "Ausreißer" in Normaldaten
clf.fit(train_pts); clf.predict(test_pts)        # score_samples: negative Mahalanobis-Abstände
```
- **Grenze (Verfahrenswahl!): funktioniert NUR bei unimodalen Verteilungen** — bei zwei Clustern legt er die Ellipse über beide → Mitte fälschlich normal

## Histogramm (Folie 20)

- Verteilungsunabhängig; Skalierung mit 1/(#Samples · Binbreite) → Fläche 1
- Probleme: Bin-Anzahl entscheidend, Dichtefunktion nicht stetig

## Kernel Density Estimation — KDE / Parzen-Fenster (Folien 21–23)

- Auf **jeden Trainingspunkt** tᵢ wird ein Kernel gelegt, Summe = Dichteschätzung:
  <span style="color:#c0182c;font-weight:700">KDE</span>(x) = 1/(N·h) · Σᵢ k( (x−tᵢ)/h )
- Kursweit nur **Gauß-Kernel**
- **<span style="background:#fde3f1;color:#b3187a;font-weight:600">Bandbreite</span> h = wichtigster <span style="background:#fde3f1;color:#b3187a;font-weight:600">Metaparameter</span>**: zu klein → zackig/<span style="color:#b35c00;font-weight:700">Overfitting</span>, zu groß → verschmiert
- h unüberwacht einstellen: **GridSearchCV, maximiere mittlere log-Dichte der Trainingspunkte**
- Funktioniert bei **beliebigen Verteilungen** (auch multimodal) — Vorteil ggü. Elliptic Envelope
- sklearn: `sklearn.neighbors.KernelDensity`, `score_samples` liefert **log-Dichten** als Scores; Schwellwert für Klassifikation selbst definieren

## Gaussian Mixture Models — GMM (Folien 24–26)

- Mischverteilung aus k unimodalen Normalverteilungen; Training = **Expectation-Maximization (EM)**:
  1. Anzahl Cluster/Moden wählen (<span style="background:#fde3f1;color:#b3187a;font-weight:600">Metaparameter</span>!)
  2. Initiale Parameter je Verteilung (z. B. per k-Means-Vorlauf)
  3. Wiederholen bis **Konvergenz oder max. Iterationszahl**:
     **E-Schritt**: P(Punkt | jede Verteilung) berechnen;
     **M-Schritt**: Verteilungsparameter per Maximum-Likelihood aktualisieren
- Novelty Detection: <span style="color:#c0182c;font-weight:700">GMM</span> auf Normaldaten fitten → neue Punkte bekommen Dichte der Mischverteilung als Score
- Schwächen: EM ist **langsam**, kann in **lokalen Minima** landen; Modenzahl muss gewählt werden
- sklearn: `sklearn.mixture.GaussianMixture`

---

## Schnellvergleich fürs Verfahrenswahl-Blatt ①

| | Mahalanobis / Ell.Env. | KDE | GMM |
|---|---|---|---|
| Annahme | EINE Normalverteilung (unimodal) | keine (Kernel-Summe) | Mischung aus k Normalvert. |
| multimodale Daten | ✗ versagt | ✓ | ✓ (k passend) |
| <span style="background:#fde3f1;color:#b3187a;font-weight:600">Metaparameter</span> | <span style="background:#fde3f1;color:#b3187a;font-weight:600">contamination</span> | <span style="background:#fde3f1;color:#b3187a;font-weight:600">Bandbreite</span> h | Modenzahl k, Init |
| Score | (neg.) Mahalanobis-Abstand | log-Dichte | Dichte der Mischverteilung |
| <span style="color:#b35c00;font-weight:700">Achtung</span> | Ellipse über allen Daten; contamination = Schwellwert, **unüberw. nicht schätzbar** (Grid flach, AUC invariant) → nur überwacht / bekannter Anteil | h via GridSearch auf Train-log-Dichte | langsam, lokale Minima |

---

# Blatt ⑤ — Rekonstruktionsbasierte Verfahren: AE, CAE, GAN, AnoGAN, f-AnoGAN (Kap. 7)

> Vorlage zum handschriftlichen Übertragen. Quelle: Foliensatz 07 (AE, GAN, AnoGAN, f-AnoGAN).
> **VAE entfällt (Klammer-Regel, geklärt 23.7.) — nicht klausurrelevant.**
> Deckt <span style="color:#1057a8;font-weight:600">Aufgabentyp 3</span> (AE-Code schreiben) + <span style="color:#1057a8;font-weight:600">Typ 9</span> (AnoGAN komplett) ab. Zielumfang: ~3 A4-Seiten.

**Beim Übertragen: die drei Code-Gerüste am Rand markieren (⚑) — das wird in der Klausur gesucht.**

| gefragt ist … | Gerüst |
|---|---|
| <span style="color:#c0182c;font-weight:700">Autoencoder</span> / CAE schreiben | ⚑ **CAE-Gerüst** |
| <span style="color:#c0182c;font-weight:700">Generator</span> + <span style="color:#c0182c;font-weight:700">Discriminator</span> schreiben | ⚑ **G/D-Gerüst** |
| <span style="color:#c0182c;font-weight:700">f-AnoGAN</span>-Encoder schreiben | ⚑ **Encoder-Gerüst** |
| Training / Score **beschreiben** | AnoGAN-Ablauf, f-AnoGAN 3 Phasen (Text, kein Code) |

---

## Grundidee Rekonstruktion (Folien 2–4)

- Curse of Dimensionality: benötigte Datenmenge steigt exponentiell, Abstände werden untereinander immer ähnlicher → nutzlos → **Dimensionsreduktion**
- Novelty Detection per Rekonstruktion: Modell (auf Normaldaten trainiert) kann nur Ähnliches rekonstruieren → **<span style="color:#c0182c;font-weight:700">Rekonstruktionsfehler</span> = Anomalie-Score** (hoch = Anomalie)

## Autoencoder (Folien 8–11)

- Encoder → **Code z (Latent Variable)** → Decoder; Ausgang rekonstruiert Eingang
- Loss = Abstand Eingabe ↔ Rekonstruktion (MSE) → **unüberwacht, keine Labels nötig**
- z hat **niedrigere Dimension** als Eingabe — sonst lernt das Netz nur die Identität! (MC-Klassiker)
- Architektur: Encoder verjüngt sukzessive, Decoder = **gespiegelter** Encoder
- Traditionelle Anwendungen: Schicht-Initialisierung (heute selten); **Feature-Descriptor** (Encoder liefert Merkmale → z. B. AE auf Normaldaten + OCSVM auf encodierten Merkmalen)

## Convolutional Autoencoder — CAE (Folien 12–16)

- **Warum CAE statt Dense-AE für Bilder — zwei Gründe (beide nennen!):** (1) Dense-AE verliert Nachbarschaft/2D-Struktur; (2) **<span style="color:#c0182c;font-weight:700">Weight Sharing</span>** — derselbe Filter gilt an jeder Bildposition ⇒ drastisch weniger Gewichte (Blatt ②: 222 gegen 157 000) ⇒ weniger <span style="color:#b35c00;font-weight:700">Overfitting</span>
- **Downsampling im Encoder**: Pooling oder Conv mit strides=2
- **Upsampling im Decoder** — 2 Möglichkeiten:
  1. `UpSampling2D` + Interpolation (nearest/bilinear) → wird nicht gelernt, „verschmiert"
  2. **Transponierte Faltung** `Conv2DTranspose` (= Deconvolution, fractionally-strided conv) → gelerntes Upsampling; strides=2 **verdoppelt** H und W; padding='same'
- Typischer Aufbau: Eingabe → [Conv strides=2]×n → Flatten → Dense = z → Dense → Reshape → [Conv2DTranspose strides=2]×n → Rekonstruktion

**Shape-Regel für Blatt ②:** Conv2DTranspose, strides=2, padding='same' → 2H × 2W × filters

**CAE-Gerüst (<span style="color:#1057a8;font-weight:600">Aufgabentyp 3</span>) — Beispiel 32×32×3, zwei Halbierungen, z = 20:**
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
- <span style="color:#c0182c;font-weight:700">RandNet</span> variiert **3 Dinge**: (1) zufällige **Verbindungsmaske** je Schicht, (2) zufällige **Trainings-Untermenge** je Netz, (3) Initialisierung
- RandNet-Schicht = Dense mit zufälliger 0/1-**Maske auf den Gewichten** (elementweise Multiplikation); Maske wird 1× bei Erstellung gezogen (m·n Ziehungen **mit Zurücklegen** → Duplikate ⇒ ≈ 37 % der Verbindungen nie gezogen, ≈ 63 % überleben), bleibt dann konstant
- **Maske ≠ <span style="color:#c0182c;font-weight:700">Dropout</span>:** Maske einmalig fest, auf **Verbindungen**, immer aktiv — Dropout pro Schritt neu, auf **Neuronen**, in der Inferenz aus. (Nie „Neuronen werden rausgenommen" für RandNet schreiben!)
- Architektur: Encoder halbiert Neuronen je Schicht, Decoder verdoppelt; max. 7 Schichten; Code ≥ 3 Neuronen; **erste Encoder- und letzte Decoder-Schicht: Sigmoid, Rest ReLU**
- Training: 100 Netze, 300 Epochen, RmsProp, je 1/10 der Daten (Subsampling), Sample-Anzahl wächst ×1,01 pro Epoche
- Score: quadrat. Fehler je Netz → normalisieren mit Std der Trainingsfehler des Netzes → **Median** über alle Netze

## GAN (Folien 27–36)

- **Generator** G: Eingabe Latent-Vektor z (feste Verteilung, z. B. Normal) → generiertes Sample; Architektur ≈ Decoder
- **Discriminator** D: Eingabe Sample → binär echt/generiert
- **Minimax-Game**: min_G max_D V = E_x[log D(x)] + E_z[log(1 − D(G(z)))]
- Training: **abwechselnd** pro Schritt; Kosten bleiben idealerweise beidseitig ~konstant
- **Trainingsende (<span style="color:#1057a8;font-weight:600">Folie 28</span>)** — für „Beschreiben Sie das Training": *eigentlich* fertig, wenn D
  keinen Unterschied mehr sieht ⇒ **Kosten von D dauerhaft hoch, Kosten von G niedrig**. Dieses
  Bild ist aber **nicht eindeutig**: es entsteht genauso, wenn G nur **schneller gelernt** hat als
  D und mit unrealistischen Strukturen „betrügt". Deshalb reicht der Fehlerverlauf nicht — die
  **generierten Daten ansehen**.
- Vorteile (<span style="color:#1057a8;font-weight:600">Folie 34</span>): (1) A-priori-Verteilung von z wird **implizit** gelernt (G bekommt Eingaben
  aus fester Verteilung und lernt, dazu passend zu generieren); (2) Qualitätsprüfung nicht durch
  ein festes Maß, sondern durch ein **Netz** — D prüft auch **lokale** Information ⇒ Daten wirken
  auch für Netze echt; (3) beste Datenqualität unter den Generatoren (heute von Diffusionsmodellen
  abgelöst)
- Nachteile (MC!): Netze müssen gleich schnell lernen (D zu schnell → G lernt nie; G zu schnell → G „betrügt"); Trainingsfortschritt schwer beurteilbar → generierte Daten inspizieren; kein direkter Einfluss auf Generierung

---

### G und D bauen (Aufgabentyp 9)

**DCGAN** = Deep Convolutional <span style="color:#c0182c;font-weight:700">GAN</span>: G und D sind Faltungs- statt Dense-Netze. Der Name meint auch
die Rezeptliste selbst.

**① Rezeptliste (<span style="color:#1057a8;font-weight:600">Folie 36</span>)** — wird bei „Empfehlungen aus der Vorlesung" wörtlich abgefragt:
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
  `BatchNormalization()` → `ReLU()` → `Reshape`. <span style="color:#1057a8;font-weight:600">Aufg. 9a</span> sagt „**immer** ReLU", Ausnahme ist nur
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
aus der Klassifikationsaufgabe" (so in <span style="color:#1057a8;font-weight:600">Aufg. 9b</span>), ist **sigmoid** gemeint: ein Neuron, Ausgabe als
Wahrscheinlichkeit. **Weglassen** darf man sie nur, wenn der Loss
`tf.keras.losses.BinaryCrossentropy(from_logits=True)` benutzt wird — diese Option **zieht die
Sigmoid in die Kostenfunktion** (<span style="color:#1057a8;font-weight:600">Folie 30</span>), deshalb darf D dann und nur dann ohne
Ausgabe-Aktivierung bleiben. Also sigmoid hinschreiben **und den Halbsatz dazu**; das deckt beide
Lesarten ab.

Gilt genauso für Klassifikationsnetze (Ausgabe: softmax bei mehreren Klassen / sigmoid bei zwei /
keine bei Regression) — dieselbe Frage, anderes Netz.

- **Argumentnamen ausschreiben** (`filters=`, `kernel_size=`, `units=`), sonst vertauscht man die
  ersten beiden Positionen: `Conv2D(filters, kernel_size, …)`, `Dense(units, …)`.
- „Keine Fully-Connected-Layers" meint **dazwischen**; die zwei Dense bleiben (Eingang G, Ausgang D).

---

**GAN-Training beschreiben (<span style="color:#1057a8;font-weight:600">Folien 30–33</span>) — <span style="color:#1057a8;font-weight:600">Aufg. 9c</span> verlangt ausdrücklich KEINEN Code.**
Antwortgerüst in Worten, pro Batch — rechts steht, woran man den Schritt im Code erkennt
(zum Wiedererkennen in Praktikum 08, nicht zum Abschreiben):

| Schritt (so hinschreiben) | im Code erkennbar an |
|---|---|
| 1. **z ziehen**, standardnormalverteilt, ein Vektor pro Bild des Batches | `noise = tf.random.normal([batch, z_dim])` |
| 2. **G erzeugt daraus Fakes** (Vorwärtsrechnung durch G) | `generated = generator_model(noise)` |
| 3. **D bewertet zweimal**: echte Bilder des Batches und die Fakes | zwei Aufrufe `discriminator_model(images)` / `(generated)` |
| 4. **D-Kosten**: binäre <span style="color:#c0182c;font-weight:700">Kreuzentropie</span> mit Ziel **echt = 1, fake = 0**, beide Anteile gemittelt | `ones_like(real_out)` + `zeros_like(fake_out)`, `0.5*(…+…)` |
| 5. **G-Kosten**: dieselbe Kreuzentropie, aber Ziel **fake = 1** — G will, dass D die Fälschung für echt hält (der Minimax-Gegensatz) | `ones_like(fake_out)` auf den **fake**-Ausgang |
| 6. beide Netze **abwechselnd** aktualisieren, je ein **eigener Optimierer** (Adam 2e-4); **kein `fit`**, weil zwei Netze mit gegenläufigen Zielen → eigene Schleife | zwei `GradientTape`, zwei `apply_gradients` |

- Merkanker zu 4./5.: **Nur das Ziel-Label unterscheidet die beiden Kosten** — derselbe fake-Ausgang, für D „ist 0", für G „soll 1 sein".
- Ende: Kosten bleiben beidseitig ungefähr konstant ⇒ **generierte Bilder ansehen** (s. o.)

## AnoGAN (Folien 37–42) — Ablauf komplett (Aufgabentyp 9!)

**Warum Optimierung? (<span style="color:#1057a8;font-weight:600">Folie 37</span> — erster Satz jeder Antwort)** Ein GAN kennt nur **z → Sample**, **kein inverses Mapping**. Das passende z muss **gesucht** werden; wie gut es am Ende passt = Score.

**Training:** GAN normal mit Normaldaten.

**Scoring von x** (G und D **eingefroren**):
1. z zufällig initialisieren
2. n Iterationen (z. B. 500): L(x, z) nach **z** ableiten, z per Gradient Descent anpassen
3. finale Kosten L(x, z_n) = **Anomalie-Score**

**Kosten** (<span style="background:#fde3f1;color:#b3187a;font-weight:600">λ</span> ≈ 0,1): **L = (1−λ)·L_res + λ·L_disc**
- **L_res:** Abstand x ↔ G(z) — **Pixelraum**, „sehen sie gleich aus?"
- **L_disc:** Abstand D_k(x) ↔ D_k(G(z)) — **Merkmalsraum**, vorletzte D-Schicht (`layers[-2]`, `feature_model`), „wirken sie für D gleich?"

**<span style="color:#b35c00;font-weight:700">⚠</span> L_disc ist KEINE Klassifikationsentscheidung.** Beide messen **Ähnlichkeit**, nur in verschiedenen Räumen. D ist **Merkmalsextraktor**, sein Echt/Fake-Urteil wird nicht ausgewertet — daher `layers[-2]`.

**Kein Code nötig** (9d = Fließtext), aber sagen: **z ist die einzige optimierte Größe** (`tf.Variable`, eines pro Sample), **D nur bis zur vorletzten Schicht**.

**Nachteil:** z-Optimierung pro Sample → langsam im Einsatz.

## f-AnoGAN (Folien 43–49)

**Idee:** Encoder E berechnet z **direkt** aus x → Score in **einem** Durchlauf, keine Iterationen.

**3 Phasen:**
1. GAN mit Normaldaten trainieren
2. **E** trainieren (GAN eingefroren, gleiche Daten), Aufbau als Autoencoder **`E → G`** (G als Decoder), RMSprop
3. Score(x) = L_res + L_disc mit **G(E(x))** — eine Vorwärtsrechnung

- Gleiche zwei Anteile wie <span style="color:#c0182c;font-weight:700">AnoGAN</span>, nur **MSE** statt Betrag und G(E(x)) statt G(z) (<span style="color:#1057a8;font-weight:600">Folie 44</span> gewichtet mit Κ, Code <span style="color:#1057a8;font-weight:600">Folie 46</span> addiert **ungewichtet**)

**Encoder = Generator rückwärts** (wird als Code verlangt): gleich viele Faltungen wie G **ohne** dessen Ausgabeschicht, gleiche Feature-Map-Zahlen, `Conv2D` statt `Conv2DTranspose`, sonst wie G. Ende: `Flatten` → `Dense(latent_dim, activation='tanh')`.

<span style="color:#b35c00;font-weight:700">⚠</span> Filterzahlen **in Gs Reihenfolge** (hier 64, 32) ⇒ Encoder hat **fallende** Filterzahlen, anders als D. Sieht <span style="color:#b35c00;font-weight:700">falsch</span> aus, ist richtig (Praktikum 08). Nicht „korrigieren".

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

---

# Blatt ④ — SVM, OCSVM, Deep SVDD, GOAD, CutPaste (Kap. 8)

> Vorlage zum handschriftlichen Übertragen. Quelle: Foliensatz 08.
> Foliensatz **08a (Contrastive Learning / SimCLR / CSI) ist nicht klausurrelevant** — wie 03a
> und 07a ein „Zusätzliche Verfahren"-Satz ohne Übung und ohne Praktikum; am 29.7. entfernt.
> Deckt <span style="color:#1057a8;font-weight:600">Aufgabentypen 6/7</span> (SVM/OCSVM zeichnen) + 10 (Deep-SVDD-Code beurteilen) ab. Zielumfang: ~2,5 A4-Seiten.

---

## SVM überwacht (Folien 5–30) — fürs Zeichnen (Typ 6)

- Trennebene h₀ in der Mitte, Parallelebenen h₁/h₂ durch die nächsten Punkte
- **Optimale Ebene = maximaler Abstand (Margin) zu den nächsten Punkten beider Klassen = Support Vektoren**; Ebene hängt NUR von den SV ab
- **<span style="color:#c0182c;font-weight:700">Margin</span> = Streifen zwischen h₁ und h₂**; ±1 ist nur **Normierung** (w, b frei skalierbar) ⇒ Breite 2/‖w‖ ⇒ **Margin max = ‖w‖ min**
- **<span style="color:#c0182c;font-weight:700">Nebenbedingung</span>:** kein Punkt zwischen h₁/h₂, jeder auf seiner Seite. Fesselt die Ebene an die Daten — ohne sie wäre w = 0 die Lösung (vgl. <span style="color:#b35c00;font-weight:700">triviale Lösung</span> Deep SVDD)

**Zeichenregeln (<span style="color:#1057a8;font-weight:600">Typ 6</span>):**
1. SV = die Punkte beider Klassen, die der Trennlinie am nächsten liegen (meist 2–3 Stück)
2. Trennlinie mittig zwischen den SV, Margin symmetrisch
3. Nicht-SV dürfen sich bewegen/entfallen — Ebene bleibt; entfernt man einen **SV**, ändert sie sich

**Soft Margin / <span style="background:#fde3f1;color:#b3187a;font-weight:600">Straffaktor</span> C (<span style="color:#1057a8;font-weight:600">Folie 10</span>):**
- Schlupfvariablen ξᵢ erlauben Punkte im Margin / auf der falschen Seite; C = Strafgewicht dafür
- **C groß → wenig Verletzungen erlaubt, schmaler Margin** (Tendenz <span style="color:#b35c00;font-weight:700">Overfitting</span>); **C klein → mehr Verletzungen, breiter Margin** (robuster)
- **<span style="color:#1057a8;font-weight:600">Typ 6b</span> („C wird reduziert"):** 1. Ausreißer-SV darf **in die Margin / auf die falsche Seite** rutschen. 2. Ebene richtet sich nach der **Masse** → breiterer Margin, **robuster**. 3. **C zu klein ⇒ Lage beliebig, viele Fehlklassifikationen** (<span style="color:#b35c00;font-weight:700">Underfitting</span>)
- C in logarithmischen Intervallen testen
- Alternative ν-SVM: <span style="background:#fde3f1;color:#b3187a;font-weight:600">ν</span> ∈ (0;1] = untere Schranke für Anteil der SV, obere Schranke für Margin-Verletzer (intuitiver als C)

**<span style="color:#c0182c;font-weight:700">Kernel-Trick</span> (<span style="color:#1057a8;font-weight:600">Folien 15–27</span>):**
- **Welche Rechnung?** Beide: **duales Problem** (Training, Skalarprodukt xᵢ·xⱼ zweier Trainingspunkte) und **Entscheidungsfunktion** (Anwendung, x·xᵢ = neuer Punkt mit jedem SV)
- Beide brauchen die Daten **nur als Skalarprodukte**, nie die Koordinaten selbst → jedes Skalarprodukt wird k(·,·). Dass w herausfällt, ist die Folge, nicht der Ort
- → implizite Transformation in höherdim. Raum, ohne ihn zu berechnen; dort linear = nichtlinear im Original
- Kernels: **linear**, **polynomial** (erst Skalarprodukt, dann potenzieren), **RBF/Gauß** (über den **Abstand** — nicht verwechseln!)
- **<span style="color:#c0182c;font-weight:700">RBF</span>:** Ähnlichkeit zweier Punkte über ihren **Abstand** (Gauß-Glocke: 1 bei a = b, fällt gegen 0). Legt **jeden** Punkt auf die **Einheitskugel in ∞ Dim** ⇒ Abstand 1 vom Ursprung — Basis der OCSVM
- **<span style="background:#fde3f1;color:#b3187a;font-weight:600">γ</span> groß** → schmale Glocke ⇒ Grenze zerfällt in **Inseln** (<span style="color:#b35c00;font-weight:700">Overfitting</span>); **γ klein** → glatte, fast kreisförmige Grenze, schließt Leerraum ein (<span style="color:#b35c00;font-weight:700">Underfitting</span>). Log. testen, alt. `gamma='scale'`

**SVM-Eigenschaften (<span style="color:#1057a8;font-weight:600">Folie 30</span>, für Verfahrenswahl):**
+ stark bei wenig Trainingsdaten, eindeutige globale Lösung, robust ggü. Rauschen, gut bei hohen Dimensionen (sogar dim > n), schnelle Klassifikation, wenig Speicher
− Training langsam, <span style="background:#fde3f1;color:#b3187a;font-weight:600">Metaparameter</span> unintuitiv, Probleme bei starker Klassenüberlappung, **Skalierung essenziell (v. a. RBF → Standardisierung!)**
- sklearn: `sklearn.svm.SVC`, `NuSVC`

## OCSVM (Folie 31) — Typ 7

- Problem: nur EINE Klasse (Normaldaten) → keine zweite Klasse für Margin
- **Idee: Trenne Normaldaten vom URSPRUNG, maximiere Abstand der Ebene zum Ursprung**

**Warum Kernel-Trick nötig? (<span style="color:#1057a8;font-weight:600">Aufg. 6d</span> + 7c — in 4 Schritten:)**
1. Keine zweite Klasse ⇒ Trennung **vom Ursprung**.
2. **Linear wertlos:** eine Ebene halbiert nur den Raum — jenseits der Wolke gilt alles weiter als **normal**, die Daten werden nicht umschlossen.
3. **RBF legt alles auf die Einheitskugel.** Erst dort ist „max. Ursprungsabstand" sinnvoll: Ebene schneidet die **Kappe** mit den dichten Normaldaten heraus.
4. Im Originalraum ⇒ **geschlossene, krumme Grenze**, bei passendem <span style="background:#fde3f1;color:#b3187a;font-weight:600">γ</span> auch **Inseln**.
- Ohne Trick **unmöglich** (nicht nur teurer): φ_RBF hat unendlich viele Komponenten

**Zeichenregeln (<span style="color:#1057a8;font-weight:600">Typ 7</span>):**
1. **Linear:** Gerade **vom Ursprung weg** schieben, bis sie an den **ursprungsnächsten** Punkten anliegt = SV. **Normaldaten ursprungsfern, Anomalien ursprungsseitig**
2. <span style="background:#fde3f1;color:#b3187a;font-weight:600">ν</span> sehr klein (0,001) ⇒ auch der ursprungsnächste **Ausreißer** muss mit hinein → Gerade weit rausgedrückt
3. **RBF:** geschlossene, krumme Grenze **um die Wolke**; liegt umso enger an, je passender ν

- <span style="background:#fde3f1;color:#b3187a;font-weight:600">Metaparameter</span>: **ν = Anteil erlaubter Ausreißer in den Normaldaten** (steuert, wie eng die Grenze anliegt); **γ = Einfluss der Nachbarschaft** (Form der Grenze)
- **<span style="color:#1057a8;font-weight:600">Typ 7b</span> (ν):** **zu klein** → Ausreißer mit eingeschlossen, Normalbereich zu groß = **<span style="color:#b35c00;font-weight:700">Overfitting</span>**. **passend** → Ausreißer draußen, Grenze eng an der Wolke. **zu groß** (0,5) → halbe Wolke fälschlich als Anomalie = **<span style="color:#b35c00;font-weight:700">Underfitting</span>**
- ν = **untere** Schranke SV-Anteil, **obere** Schranke Verletzer
- **<span style="color:#1057a8;font-weight:600">Typ 8/12</span>:** <span style="color:#c0182c;font-weight:700">OCSVM</span>+RBF beschreibt auch **mehrere Cluster als Inseln** ⇒ gut bei mehrmodalen Normaldaten; Mahalanobis/EE (eine Ellipse) deckt den Leerraum dazwischen mit ab
- γ-Wirkung auf die Grenze und `gamma='scale'` → siehe **Kernel-Trick-Block oben**
- sklearn: `sklearn.svm.OneClassSVM`
- **<span style="color:#c0182c;font-weight:700">SVDD</span>** (<span style="color:#1057a8;font-weight:600">Folie 35</span>): findet die **kleinste Kugel** (Radius R, Zentrum c), die die Normaldaten umschließt; ν erlaubt wieder Ausreißer. **Mit Gauß-Kernel: SVDD ≡ OCSVM**

## Deep SVDD (Folien 40–52) — Verbotsliste! (Typ 10)

**Ziel:** Netz φ(x) bildet Normaldaten in eine Kugel (c, R) mit minimalem Volumen ab.
**Loss = mittlerer quadratischer Abstand zu c** (+ Weight Decay <span style="background:#fde3f1;color:#b3187a;font-weight:600">λ</span>).

**<span style="color:#b35c00;font-weight:700">⚠</span> <span style="color:#b35c00;font-weight:700">Verbotsliste</span> — jede Verletzung ermöglicht die TRIVIALE LÖSUNG (Netz kollabiert alles auf einen Punkt, R=0, Kosten 0, nutzlos):**
| <span style="color:#b35c00;font-weight:700">Verbot</span> | Warum |
|---|---|
| **c darf <span style="color:#b35c00;font-weight:700">NICHT</span> mitoptimiert werden / c ≠ 0** | sonst c=0 + Nullgewichte → φ(x)=0 ∀x. Lösung: c = Mittel der Abbildungen mit initialen Gewichten VOR dem Training, danach fix; Komponenten nahe 0 auf ±ε (0,1) setzen |
| **Keine Biases** (`use_bias=False` überall) | Nullgewichte + Biases → φ(x)=c ∀x konstant |
| **Keine beschränkten („gedeckelten") Aktivierungen** (kein Sigmoid/tanh) → ReLU/LeakyReLU | gesättigte Aktivierung ≈ konstante 1 → wirkt wie Bias |
| **<span style="color:#c0182c;font-weight:700">BatchNorm</span> ist KEIN Fehler** | steht in <span style="color:#1057a8;font-weight:600">Aufg. 10</span>.2 drin und gilt dort als „Netz in Ordnung"; Paulus nutzt sie auch im Praktikum. Nicht anstreichen! |

**Alle drei durchgehen:** (1) `use_bias` in **jeder** Schicht (fehlt es, ist Default `True` = Fehler!), (2) Aktivierungen auf Sigmoid/tanh, (3) `transform_center` — außerhalb des Trainings und ≠ 0? **Ein Ausschnitt kann mehrere Fehler haben**; „alles korrekt" ist eine zulässige Antwort.

**Ablauf:**
1. **Vortraining als Autoencoder** (Encoder = Deep-SVDD-Netz + Wegwerf-Decoder, MSE-Loss)
   – **Ohne Vor-Training?** Zwei Wege, den Loss klein zu machen: (a) gute Merkmale lernen, (b) alles auf einen Punkt legen. (b) ist leichter, denn der Loss misst nur den **Abstand zu c** — nicht, ob die Abbildung noch etwas über das Bild aussagt. Also klumpen Normaldaten **und** Anomalien zusammen: alle Scores gleich, **AUC ≈ 0,5**. Der AE-Loss verlangt, das Bild **zurückzubauen** — konstant geht das nicht.
     (Bias/Sigmoid/c ≠ 0 verbieten nur „**exakt** auf c", fast konstant bleibt erlaubt.)
   – **Decoder, `Dense`→`Reshape`:** muss nur die **Auflösung** treffen (7×7, damit 2× Upsampling wieder 28 gibt); die **Kanalzahl ist frei** (Praktikum: 7·7·2 statt 7·7·4), weil die nächste `Conv2DTranspose` sie neu setzt. Exakt die letzte Encoder-Shape nur, wenn die Aufgabe „spiegeln" verlangt (Orig.-<span style="color:#1057a8;font-weight:600">Aufg. 3</span>).
2. Decoder verwerfen; c = Mittel der Encodierungen (get_center)
3. Encoder als <span style="color:#c0182c;font-weight:700">Deep SVDD</span> trainieren: Loss = mittlerer quadrat. Abstand zu c
4. **Radius NACH dem Training**: R = **(1 − <span style="background:#fde3f1;color:#b3187a;font-weight:600">ν</span>)-Quantil** der Abstände zu c → `np.quantile(np.sqrt(dists), 1-nu)` (ν = erlaubter Ausreißeranteil)
   – **Warum kommt R im Loss nicht vor?** Der Loss zieht alle Normaldaten so nah wie möglich an c; R ist danach nur das Quantil genau dieser Abstände ⇒ kleine Abstände = kleines R = **minimales Kugelvolumen**. (Der Weight Decay ist nur Regularisierung, kein Volumen-Argument.)

**Score & Klassifikation:** score(x) = ‖φ(x) − c‖² − R² → **negativ = in Kugel = normal; positiv = Anomalie** (sgn)

## GOAD (Folien 55–60)

- **Selbstüberwacht:** Hilfsaufgabe „Welche Transformation wurde angewendet?" liefert Pseudo-Labels
- Bilder: Rotation (4) × Translation (9) × Spiegelung (2) = **M = 72 Transformationen** (inkl. Identität); allgemeine Daten: **zufällige affine Transformationen** Ax+b (Anzahl = <span style="background:#fde3f1;color:#b3187a;font-weight:600">Metaparameter</span>, mehr = stabiler)
- Netz f bildet jede transformierte Version in Latent Space; Ziel: **pro Transformation ein dichtes Cluster** (Zentren cⱼ = Mittel)
- **<span style="color:#c0182c;font-weight:700">Triplet Center Loss</span>**: Abstand zum **eigenen** Zentrum klein, zum nächsten **fremden** groß (Marge s ≈ 1). Gesamtloss = Kreuzentropie „welche Transformation?" (Stabilisierung) + λ₁·L_tc + λ₂·L2-Norm der **Latent-Vektoren z** (kein Weight Decay!) — **λ₁ = 0,1; λ₂ = 10**
- **Score(x) = −Σⱼ log P(Tⱼ | Tⱼ(x))** — landet jede transformierte Version im richtigen Cluster? Niedrige P → hoher Score → Anomalie

**Die drei Warum-Fragen:**
- **Warum Transformationen?** Sie **erzeugen die Labels** (man hat nur Normaldaten, sonst kein Lernsignal) und machen aus **einer** Kugel **M Cluster**.
- **Warum die Transformations-Vorhersage?** Der Triplet Center Loss ist **pro Batch instabil** (Zentren aus dem Batch geschätzt, schwanken) ⇒ Kreuzentropie **stabilisiert**. Nebeneffekt: eine konstante Abbildung kann die Transformationen nicht unterscheiden ⇒ **<span style="color:#b35c00;font-weight:700">triviale Lösung</span> ausgeschlossen**.
- **Warum dichte, getrennte Cluster?** Der Score misst **Abstände zu den Zentren** — überlappende Cluster ⇒ nichtssagende P ⇒ unbrauchbarer Score.

**<span style="color:#c0182c;font-weight:700">GOAD</span> vs. Deep SVDD (Typ-10-Vergleichsfrage):**
| | Deep SVDD | GOAD |
|---|---|---|
| Normaldaten | **eine** Kugel (c, R) | **M Cluster**, eines je Transformation |
| Lernsignal | nur Abstand zu c ⇒ braucht **AE-Vortraining** | selbstüberwachte **Hilfsaufgabe** |
| Triviale Lösung | nur per **<span style="color:#b35c00;font-weight:700">Verbotsliste</span>** verhindert | durch die Klassifikation ausgeschlossen |
| Score | ‖φ(x)−c‖² − R² | Summe der neg. Log-Wahrscheinlichkeiten |

## CutPaste (Folien 62–65)

- Für **kleine, lokale Defekte** (Kratzer in Fertigung) — bisherige Verfahren sehen eher globale Anomalien
- Selbstüberwacht mit Pseudo-Anomalien: Rechteck aus dem Bild kopieren + woanders einfügen
- 3 Klassen: **unverändert / normales <span style="color:#c0182c;font-weight:700">CutPaste</span> / CutPaste Scar** (sehr klein + dünn)
- Nach Training: Klassifikationsschicht abschneiden → CNN = Merkmalsextraktor f
- Score = Gauß-Dichte im Merkmalsraum, μ/Σ aus Normaldaten — also **Mahalanobis auf f(x)** (vgl. Elliptic Envelope)

---
