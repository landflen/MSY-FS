# MDT5/2 — Alle Zusammenfassungsblätter (Gesamtdokument)

> Zusammengeführte Version aller 7 Blätter zum Durchscrollen/Drucken.
> Die Einzeldateien sind die Originale — bei Änderungen dort dieses Dokument neu erzeugen.
> Klammer-Regel (23.7.): VAE, PCA, k-Means, LOF, Matrix Profiles = nicht klausurrelevant, entfernt.

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

> Die wichtigste Tabelle für Aufgabentypen 8 und 12 (Verfahrenswahl zu Daten-Plot begründen).
> Quellen: alle Foliensätze; Taxonomie nach Folie 01/33. Zielumfang: 2 A4-Seiten (Tabelle quer!).

---

## Grundbegriffe (Kap. 1 — für MC)

- **Anomalie**: "Patterns in data that do not conform to a well defined notion of normal behavior" (Chandola et al.)
- **Punktanomalie**: isolierter Punkt weicht ab. **Kontextanomalie**: nur im Kontext (Bsp. hohe Ausgaben an Weihnachten = normal)
- **Anomalieerkennung ≠ überwachtes Lernen!** Warum: kaum/keine Anomalien im Training; Ausprägungen unbekannt; auch das „unbekannte Unbekannte" soll erkannt werden
- **Novelty Detection** (= OOD Detection, Ein-Klassen-Problem): Training NUR mit Normaldaten; gelernt wird, was normal ist; Anomalien höchstens für Fine-Tuning/Test. **→ Schwerpunkt des Kurses!**
- **Outlier Detection**: Training mit ungelabelten Daten (Anomalien unerkannt drin). 2 Hauptanwendungen: **KDD** (neue Einblicke) + **Trainingsdaten-Bereinigung** (z. B. pro Klasse). Annahmen: Ausreißer selten, „anders"/weiter weg, niedrigere Dichte
- Expertensystem / ML (kein DL) / DL: Merkmale manuell/manuell/gelernt; Klassifikation manuell/gelernt/gelernt; Datenbedarf gering/mittel/sehr hoch; Nachvollziehbarkeit hoch/meist gegeben/kaum
- **Merkregel Deep vs. Shallow**: Deep = tiefes neuronales Netz steckt im Verfahren

## Taxonomie (Folie 01/33 — nachzeichnen!)

| | Distanz | Probabilistisch | Rekonstruktion | Klassifikation |
|---|---|---|---|---|
| **Deep** | — | — | Autoencoder, (VAE), f-AnoGAN | Deep SVDD, GOAD, CutPaste |
| **Shallow** | kNN, (LOF), iForest, (Matrix Profiles) | Histogramm, Mahalanobis, KDE, GMM | (PCA), (k-Means) | OC-SVM, SVDD |

**Eingeklammert auf der Folie = NICHT klausurrelevant — ALLES in Klammern** (Ansage Prof., geklärt 23.7.). Beim Nachzeichnen mitklammern, aber nicht lernen. **LOF, Matrix Profiles, VAE, PCA, k-Means** sind deshalb aus allen Blättern/Übungen entfernt (Blatt Clustering/PCA komplett gestrichen, VAE-Teil aus Blatt ⑤ und Übungsblatt 6 entfernt).

## Die große Verfahrenstabelle

| Verfahren | Score | Wichtigste Metaparameter | Norm.? | Geeignet | Ungeeignet / Schwäche |
|---|---|---|---|---|---|
| **kNN-Abstand** | mittl. Abstand zu k Nachbarn | k, Abstandsmaß | JA | einfach, wenig Daten | langsam; hohe Dim. (Curse of Dim.); Rauschen |
| **iForest** | s = 2^(−E(h)/c(n)) ∈ [0;1], →1 Ausreißer | n_estimators (100), max_samples (256), contamination | **NEIN** | hohe Dim., große Daten, schnell | einzelne Bäume instabil (→ Ensemble) |
| **Mahalanobis / EllipticEnvelope** | (neg.) Mahalanobis-Abstand (Ellipse) | contamination | (robust ggü. Skala) | korrelierte Merkmale, **unimodal** | **multimodale Daten!** |
| **KDE** | log-Dichte | Bandbreite h (GridSearch auf Train-log-Dichte) | JA | **beliebige/multimodale Verteilungen** | h-Wahl; alle Trainingspunkte nötig |
| **GMM** | Dichte der Mischverteilung | Modenzahl k, Init | JA | multimodal, wenn k bekannt | EM langsam, lokale Minima |
| **Autoencoder** | Rekonstruktionsfehler | Architektur, dim(z) < dim(x)! | JA (z. B. [0;1]) | Bilder/hochdim., viele Daten | Fehler instabil (→ Ensemble/RandNet); braucht viele Daten |
| **AnoGAN** | L = (1−λ)L_res + λL_disc nach z-Optimierung | λ (0,1), Iterationen (500), z_dim | JA | Bilder, gute Datenqualität | **langsam: z-Optimierung pro Sample!**; GAN-Training heikel |
| **f-AnoGAN** | wie AnoGAN, aber via Encoder G(E(x)) | wie AnoGAN + Encoder | JA | wie AnoGAN, schnelles Scoring | 3-stufiges Training |
| **OC-SVM** | Abstand zur Trennebene (vom Ursprung) | **ν** (Ausreißeranteil), **γ** (RBF) | **JA! (Standardis.)** | wenig Daten, hohe Dim. | große Datenmengen (Training langsam); braucht RBF |
| **SVDD** | Abstand zur Kugeloberfläche | ν, Kernel | JA | wie OC-SVM (Gauß-Kernel: äquivalent!) | wie OC-SVM |
| **Deep SVDD** | ‖φ(x)−c‖² − R² (>0 = Anomalie) | ν, λ (Weight Decay), Architektur | JA | Bilder/hochdim., viele Daten | **Verbotsliste!** (Bias, gedeckelte Akt., c) |
| **GOAD** | −Σ log P(richtige Transformation) | M Transformationen, λ₁=0,1, λ₂=10, s=1 | JA | Bilder + allgemeine Daten (affine T.) | Wahl der Transformationen |
| **CutPaste** | Gauß-Dichte im Merkmalsraum | Patch-Parameter | JA | **kleine lokale Defekte** (Fertigung) | globale Anomalien |

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
- Standardisierung (Z-Transf.): x′ = (mᵢ − μᵢ)/σᵢ → μ=0, σ=1; robuster, kein fester Bereich; `StandardScaler`
- min/max/μ/σ IMMER nur aus Trainingsdaten (fit auf Train, transform auf Train+Test) → sonst Data Leakage
- Nötig bei allem, was Abstände/Skalarprodukte rechnet (kNN, KDE, SVM/OCSVM, NN-Eingaben); NICHT nötig bei iForest (nur Splits)

**Kontrastpaar (nicht mischen!):** Min-Max = **fester Bereich**, Default [0;1], [−1;1] nur mit
`feature_range=(-1,1)`; Test kann den Bereich verlassen (Trainings-Max). Z-Transf. = **kein**
fester Bereich, nur μ=0/σ=1. „Min-Max-Standardisierung" gibt es nicht.

## Kleingedrucktes zu Scores & sklearn (S2-Nachtrag)

- **iForest-Grenzfälle:** E(h)→0 ⇒ s→1 (Anomalie); E(h)=c(n) ⇒ s=0,5 (unauffällig);
  E(h)→n−1 ⇒ s→0 (sicher normal). Baumtiefe log₂(n_sub), weil Anomalien **kurze** Pfade haben.
- **contamination = erwarteter Anteil an Ausreißern in den Daten** (Anteil, keine Anzahl) ⇒ legt
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
| Dropout / BatchNorm / RandomTranslation | unverändert | ändern NIE die Shape |

**Kontrollfragen bei Shape-Aufgaben (Typ 2/5):**
- Kanalzahl nach Conv = filters, nach Pooling = unverändert
- Räumliche Größe darf nie < Kernelgröße werden → „zu viel Pooling" = Architekturfehler
- Letzte Dense: units = Klassenanzahl (Softmax) bzw. 1 (binär, Sigmoid)

**Auflösung halbieren — zwei Wege (Folie 42), beide H/2 × W/2:**
| | MaxPool2D 2×2 | Conv2D(strides=2) |
|---|---|---|
| Parameter | **keine** (feste Vorschrift) | Kernelgewichte (Zahl unabhängig von strides) |
| Auswahl | Maximum je 2×2-Fenster, pro Kanal getrennt → stärkste Aktivierung bleibt | **gelernt**: Kernelgewichte entscheiden |
| Rechenweg | Faltung erst auf voller Auflösung, dann ausdünnen | Kernel springt um 2 → Zwischenpositionen gar nicht berechnet (billiger) |
| Kanalzahl | unverändert | = filters |

**Gewichte zählen (Folie 45):**
- Conv2D: C_in · k · k · filters   (Bias: + filters)
- Dense: n_in · n_out   (Bias: + n_out)
- Bsp. 1. Schicht VGG: 3·3·3·32 = 864;  2. Schicht: 32·3·3·32 = 9 216

**Beispiel-Kette (mod. VGG16, Folie 43):**
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

Softmax: a_j = e^(z_j) / Σ_k e^(z_k)  → Summe aller Ausgaben = 1 (echte Wahrscheinlichkeitsverteilung; Sigmoid pro Neuron leistet das NICHT)

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

**⚠ Welche Zahlen im Gerüst sind BEISPIELWERTE?** Beim Abschreiben in der Klausur nur die Struktur
übernehmen, die Zahlen kommen aus der Aufgabenstellung:
`Input((32,32,3))` = Bildgröße · `filters=8`, `kernel_size=7` = frei gewählt (Kurs sonst 3 oder 5) ·
`units=200` = frei · **`units=7` = ANZAHL DER KLASSEN** · `activation='softmax'` nur bei
Mehrklassen (2 Klassen ⇒ sigmoid, Regression ⇒ keine) · `drop_rate`, `lmbda`, `learning_rate`,
`batch_size`, `epochs` = frei.
**Argumentnamen immer ausschreiben** (`filters=`, `kernel_size=`, `units=`) — sonst vertauscht man
unter Zeitdruck die ersten beiden Positionen: `Conv2D(filters, kernel_size, …)`, `Dense(units, …)`.

---

## Schnellfakten (Nachschlagen in <10 s)

**Vanishing/Exploding Gradient (Folien 28–33):**
- Backprop = Kettenregel rückwärts; pro Schicht ein Faktor σ'(z)·w ins Produkt
- max σ' = **0,25** → 4 Schichten: 0,25⁴ ≈ 0,004; 10 Schichten: 0,25¹⁰ ≈ 10⁻⁶
- tanh: max Ableitung 1,0 → schwächer, Problem bleibt
- vordere Schichten lernen kaum → Netz lernt fast nur in letzten Schichten
- große Gewichte (Faktor > 1) → Exploding; beides = „Unstable Gradient"

**ReLU (Folie 34):** max(0, z); Ableitung 1 (z>0) oder 0 (z≤0) → Gradient stabil.
Gefahr: Dead Neurons bei z≤0 → gute Initialisierung nötig: **He-Initialisierung** (= doppelte Varianz der Xavier-Init.)

**Regularisierung — die 4 Techniken (Folien 47–55):**
| Technik | Kernidee | Metaparameter | Keras |
|---|---|---|---|
| L2 / Weight Decay | Strafterm C + λ/(2n_w)·Σw² → hohe Gewichte nur bei echtem Vorteil | λ | regularizers.L2 als kernel_regularizer |
| Dropout | implizites Ensemble; pro Trainingsschritt zufällig Neuronen deaktiviert; nach Training ALLE aktiv | Drop-Rate | layers.Dropout(rate) |
| Data Augmentation | Daten zufällig transformieren (Translation, Rotation, Helligkeit, Rauschen); an Problem anpassen! | Transformationen | layers.RandomFlip/-Translation/-Rotation |
| Batch Normalization | Covariate Shift: Verteilungen verschieben sich schichtweise → Eingaben je Schicht über Batch standardisieren; γ (Skalierung), β (Shift) mitgelernt: x_BN = γ·x_std + β | — | layers.BatchNormalization |

**Training (Folien 22–23):**
- Learning Rate zu groß → Minimum übersprungen / divergiert; zu klein → langsam, bleibt in lokalem Minimum
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
5. Data Leakage: scaler.fit() / fit_transform() auf Testdaten? → fit nur auf Train, transform auf beide
6. Augmentation, die das Label zerstört (z. B. 6 ↔ 9 bei Rotation)?

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
- Metaparameter: **k**, **Abstandsmaß** (z. B. euklidisch)
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
- Keine Abstandsberechnung → **Normalisierung NICHT nötig**, gut bei hohen Dimensionen, schnell
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
| Normalisierung | JA (abstandsbasiert) | NEIN (nur Splits) |
| Metaparameter | k, Abstandsmaß | n_estimators (100), max_samples (256), contamination |

---

# Blatt ⑥ — Evaluierung, Metriken, Data-Leakage-Checkliste (Kap. 5)

> Vorlage zum handschriftlichen Übertragen. Quelle: Foliensatz 05.
> Zielumfang: ~2 handgeschriebene A4-Seiten. Deckt Aufgabentyp 4 (Leakage finden) + MC ab.

---

## Metriken-Formelblock (Folien 16–21) — mit Confusion Matrix

Confusion Matrix (Zeile = tatsächlich, Spalte = erkannt):

|  | erkannt K | erkannt K̄ |
|---|---|---|
| **wirklich K** | TP | FN |
| **wirklich K̄** | FP | TN |

| Metrik | Formel | Frage, die sie beantwortet |
|---|---|---|
| Sensitivität / TPR / **Recall** | TP / (TP+FN) | Welcher Anteil der Klasse K wurde gefunden? |
| Spezifizität / TNR | TN / (TN+FP) | Welcher Anteil der anderen Klasse richtig? |
| Accuracy | (TP+TN) / alle | Anteil richtig insgesamt — **nur bei balancierten Daten!** |
| Balanced Accuracy | ½·(TPR + TNR) | Mittel über beide Klassen |
| **Precision** | TP / (TP+FP) | Welcher Anteil der als K Erkannten ist wirklich K? |
| F1 | 2·(prec·rec)/(prec+rec) | harmonisches Mittel |
| F_β | (1+β²)·(prec·rec)/(β²·prec+rec) | β=0,5 → Precision wichtiger; β=2 → Recall wichtiger |

**Merkbeispiel (Folie 19/20, unbalanciert, K selten):**
- K wird nie erkannt → acc 0,90 aber bal. acc 0,50 → Accuracy lügt!
- K wird doppelt so oft erkannt wie vorhanden → bal. acc 0,95, aber Precision 0,50 → auch bal. acc kann lügen, erst Precision deckt auf

**ROC & AUC (Folie 25):**
- ROC = Plot **TPR gegen FPR** für alle möglichen Schwellwerte
- AUC = Fläche darunter, Interpretation (MC-Klassiker!): **Wahrscheinlichkeit, dass eine zufällige Anomalie einen höheren Score bekommt als ein zufälliger Normalpunkt**
- AUC = 0,5 → Raten; AUC = 1,0 → perfekte Trennung
- sklearn: `roc_curve(true_y, scores, pos_label=1)` → fpr, tpr, thresholds; `roc_auc_score(true_y, scores)`

## Schwellwert wählen (Praktikum 07)

**Schwellwert = Score-Wert (y-Achse). Ausreißeranteil = Anteil der Punkte (x-Achse). Nicht dasselbe!**
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

- **Bias** = falsche Modellannahmen → Underfitting (auf Trainingsdaten sichtbar)
- **Varianz** = Anfälligkeit für Rauschen → Overfitting (erst auf Validierungs-/Testdaten sichtbar)
- Beide nicht gleichzeitig minimierbar; Overfitting-Maß = Differenz Trainings- vs. Validierungsergebnis

## Datenaufteilung (Folien 4–9)

- Train / Validierung / Test: **disjunkt!** Trennung beginnt schon bei der Vorverarbeitung
- Abhängigkeiten beachten: z. B. alle Samples eines Probanden in NUR eine Teilmenge (sklearn: Parameter `groups`)
- Validierung → Metaparameter einstellen; **Test → nur einmal ganz am Ende** (bei Fehlschlag „verbraucht")
- Wenig Daten → **k-Fold Cross Validation**: Testdaten zuerst abspalten, Rest in k Teilmengen, jede 1× Validierung; Ergebnis = Mittelwert ± Std
- sklearn nutzt standardmäßig **stratified** CV (Klassenverhältnisse bleiben in jedem Fold erhalten)
- Metaparameter-Suche: `GridSearchCV(pipe, param_grid, cv=5, refit=False)` → pro Kombination eine komplette CV

**Sonderfall Novelty Detection (Folien 12–14, klausurtypisch!):**
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

1. `scaler.fit()` oder `fit_transform()` auf **Gesamtdaten oder Testdaten**? → Leakage! (fit nur Train)
2. `train_test_split` **nach** der Normalisierung? → Leakage! (Split muss zuerst kommen)
3. GridSearchCV/CV **ohne Pipeline**, aber mit vorab global skalierten Daten? → Leakage in jeden Fold
4. Testdaten mehrfach benutzt (nach Metaparameter-Anpassung nochmal getestet)? → Testdaten verbraucht
   - auch: Metaparametersuche und finale Bewertung auf **derselben** Datenmenge? → die „beste" Parameterwahl ist an genau diese Daten angepasst, Testergebnis zu optimistisch
5. Abhängige Samples (gleicher Proband/gleiche Serie) in Train UND Test? → verstecktes Overfitting
6. Novelty Detection: Anomalien in Trainingsfolds der CV? → falsche Aufteilung (s. o.)
7. Accuracy bei stark unbalancierten Daten als einzige Metrik? → falsche Metrik (bal. acc / Precision+Recall / AUC)
8. Benutzt die **Vorverarbeitung die Labels**? (z. B. Imputation mit `median` getrennt nach Klasse) → schwerste Form von Leakage: Das Label steckt danach im Merkmal selbst. Bei neuen Daten ist das Label unbekannt → Modell wirkt im Test gut, bricht im Feld ein. Korrekt: **ein** Median pro Merkmal, nur auf den Trainingsdaten berechnet.

**Achtung, kein Fehler:** Beim Novelty-CV-Rezept (s. o.) stehen in jedem Fold **dieselben** Anomalien — das ist methodenbedingt so gewollt, nicht falsch. Als Einschränkung formulieren: Streuung über die Folds wird dadurch unterschätzt.

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

**Stufe 3 — Elliptic Envelope:** Schwelle nicht fix bei 3, sondern an Daten angepasst
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
  KDE(x) = 1/(N·h) · Σᵢ k( (x−tᵢ)/h )
- Kursweit nur **Gauß-Kernel**
- **Bandbreite h = wichtigster Metaparameter**: zu klein → zackig/Overfitting, zu groß → verschmiert
- h unüberwacht einstellen: **GridSearchCV, maximiere mittlere log-Dichte der Trainingspunkte**
- Funktioniert bei **beliebigen Verteilungen** (auch multimodal) — Vorteil ggü. Elliptic Envelope
- sklearn: `sklearn.neighbors.KernelDensity`, `score_samples` liefert **log-Dichten** als Scores; Schwellwert für Klassifikation selbst definieren

## Gaussian Mixture Models — GMM (Folien 24–26)

- Mischverteilung aus k unimodalen Normalverteilungen; Training = **Expectation-Maximization (EM)**:
  1. Anzahl Cluster/Moden wählen (Metaparameter!)
  2. Initiale Parameter je Verteilung (z. B. per k-Means-Vorlauf)
  3. Wiederholen bis **Konvergenz oder max. Iterationszahl**:
     **E-Schritt**: P(Punkt | jede Verteilung) berechnen;
     **M-Schritt**: Verteilungsparameter per Maximum-Likelihood aktualisieren
- Novelty Detection: GMM auf Normaldaten fitten → neue Punkte bekommen Dichte der Mischverteilung als Score
- Schwächen: EM ist **langsam**, kann in **lokalen Minima** landen; Modenzahl muss gewählt werden
- sklearn: `sklearn.mixture.GaussianMixture`

---

## Schnellvergleich fürs Verfahrenswahl-Blatt ①

| | Mahalanobis / Ell.Env. | KDE | GMM |
|---|---|---|---|
| Annahme | EINE Normalverteilung (unimodal) | keine (Kernel-Summe) | Mischung aus k Normalvert. |
| multimodale Daten | ✗ versagt | ✓ | ✓ (k passend) |
| Metaparameter | contamination | Bandbreite h | Modenzahl k, Init |
| Score | (neg.) Mahalanobis-Abstand | log-Dichte | Dichte der Mischverteilung |
| Achtung | Ellipse über allen Daten; contamination = Schwellwert, **unüberw. nicht schätzbar** (Grid flach, AUC invariant) → nur überwacht / bekannter Anteil | h via GridSearch auf Train-log-Dichte | langsam, lokale Minima |

---

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

---

# Blatt ④ — SVM, OCSVM, Deep SVDD, GOAD, CutPaste, Contrastive (Kap. 8 + 8a)

> Vorlage zum handschriftlichen Übertragen. Quellen: Foliensatz 08 + 08a.
> Deckt Aufgabentypen 6/7 (SVM/OCSVM zeichnen) + 10 (Deep-SVDD-Code beurteilen) ab. Zielumfang: ~2,5 A4-Seiten.

---

## SVM überwacht (Folien 5–30) — fürs Zeichnen (Typ 6)

- Trennebene h₀ in der Mitte, Parallelebenen h₁/h₂ durch die nächsten Punkte
- **Optimale Ebene = maximaler Abstand (Margin) zu den nächsten Punkten beider Klassen = Support Vektoren**; Ebene hängt NUR von den SV ab
- Margin = 2/‖w‖ ⇒ **Margin maximieren = ‖w‖ minimieren**

**Zeichenregeln (Typ 6):**
1. SV = die Punkte beider Klassen, die der Trennlinie am nächsten liegen (meist 2–3 Stück)
2. Trennlinie mittig zwischen den SV, Margin symmetrisch
3. Punkte, die keine SV sind, dürfen sich bewegen/entfallen ohne Änderung der Ebene
4. Entfernt man einen SV → Ebene ändert sich!

**Soft Margin / Straffaktor C (Folie 10):**
- Schlupfvariablen ξᵢ erlauben Punkte im Margin / auf der falschen Seite; C = Strafgewicht dafür
- **C groß → wenig Verletzungen erlaubt, schmaler Margin** (Tendenz Overfitting); **C klein → mehr Verletzungen, breiter Margin** (robuster)
- C in logarithmischen Intervallen testen
- Alternative ν-SVM: ν ∈ (0;1] = untere Schranke für Anteil der SV, obere Schranke für Margin-Verletzer (intuitiver als C)

**Kernel-Trick (Folien 15–27):**
- Die Rechnung braucht die Daten nur als **Skalarprodukte** → ersetzbar durch einen Kernel
- → implizite Transformation in höherdimensionalen Raum, ohne ihn je zu berechnen; linear dort = nichtlinear im Original
- Kernels: **linear**, **polynomial**, **RBF/Gauß** (Kurs-Standard)
- RBF: bildet auf Einheitskugel in ∞ Dimensionen ab; **γ groß → schmale Glocke, enge Anpassung; γ klein → glatter**; logarithmisch testen

**SVM-Eigenschaften (Folie 30, für Verfahrenswahl):**
+ stark bei wenig Trainingsdaten, eindeutige globale Lösung, robust ggü. Rauschen, gut bei hohen Dimensionen (sogar dim > n), schnelle Klassifikation, wenig Speicher
− Training langsam, Metaparameter unintuitiv, Probleme bei starker Klassenüberlappung, **Skalierung essenziell (v. a. RBF → Standardisierung!)**
- sklearn: `sklearn.svm.SVC`, `NuSVC`

## OCSVM (Folie 31) — Typ 7

- Problem: nur EINE Klasse (Normaldaten) → keine zweite Klasse für Margin
- **Idee: Trenne Normaldaten vom URSPRUNG, maximiere Abstand der Ebene zum Ursprung**
- **Warum Kernel (RBF) nötig?** Linear: Anomalien dürften nur auf der Ursprungsseite liegen — meist unbrauchbar. Mit RBF liegen alle Daten auf der Einheitskugel → Ebene „schneidet" den dichten Normaldaten-Bereich heraus (Klausur-Klassiker!)
- Metaparameter: **ν = Anteil erlaubter Ausreißer in den Normaldaten** (steuert, wie eng die Grenze anliegt); **γ = Einfluss der Nachbarschaft** (Form der Grenze)
- sklearn: `sklearn.svm.OneClassSVM`
- **SVDD** (Folie 35): findet die **kleinste Kugel** (Radius R, Zentrum c), die die Normaldaten umschließt; ν erlaubt wieder Ausreißer. **Mit Gauß-Kernel: SVDD ≡ OCSVM**

## Deep SVDD (Folien 40–52) — Verbotsliste! (Typ 10)

**Ziel:** Netz φ(x) bildet Normaldaten in eine Kugel (c, R) mit minimalem Volumen ab.
**Loss = mittlerer quadratischer Abstand zu c** (+ Weight Decay λ).

**⚠ Verbotsliste — jede Verletzung ermöglicht die TRIVIALE LÖSUNG (Netz kollabiert alles auf einen Punkt, R=0, Kosten 0, nutzlos):**
| Verbot | Warum |
|---|---|
| **c darf NICHT mitoptimiert werden / c ≠ 0** | sonst c=0 + Nullgewichte → φ(x)=0 ∀x. Lösung: c = Mittel der Abbildungen mit initialen Gewichten VOR dem Training, danach fix; Komponenten nahe 0 auf ±ε (0,1) setzen |
| **Keine Biases** (`use_bias=False` überall) | Nullgewichte + Biases → φ(x)=c ∀x konstant |
| **Keine beschränkten („gedeckelten") Aktivierungen** (kein Sigmoid/tanh) → ReLU/LeakyReLU | gesättigte Aktivierung ≈ konstante 1 → wirkt wie Bias |
| BatchNorm kritisch prüfen | der lernbare Shift β wirkt wie ein Bias (in Übungsaufgaben als Fehler gewertet) |

**Ablauf:**
1. **Vortraining als Autoencoder** (Encoder = Deep-SVDD-Netz + Wegwerf-Decoder, MSE-Loss)
2. Decoder verwerfen; c = Mittel der Encodierungen (get_center)
3. Encoder als Deep SVDD trainieren: Loss = mittlerer quadrat. Abstand zu c
4. **Radius NACH dem Training**: R = (1−ν)-Quantil der Abstände: `np.quantile(np.sqrt(dists), 1-nu)` (ν = erlaubter Ausreißeranteil)

**Score & Klassifikation:** score(x) = ‖φ(x) − c‖² − R² → **negativ = in Kugel = normal; positiv = Anomalie** (sgn)

## GOAD (Folien 55–60)

- **Selbstüberwacht:** Hilfsaufgabe „Welche Transformation wurde angewendet?" liefert Pseudo-Labels
- Bilder: Rotation (4) × Translation (9) × Spiegelung (2) = **M = 72 Transformationen** (inkl. Identität); allgemeine Daten: **zufällige affine Transformationen** Ax+b (Anzahl = Metaparameter, mehr = stabiler)
- Netz f bildet jede transformierte Version in Latent Space; Ziel: **pro Transformation ein dichtes Cluster** (Zentren cⱼ = Mittel)
- **Triplet Center Loss**: Abstand zum **eigenen** Zentrum klein, zum nächsten **fremden** groß (Marge s ≈ 1). Dazu Kreuzentropie „welche Transformation?" als Stabilisierung + Weight Decay — **λ₁ = 0,1; λ₂ = 10**
- **Score(x) = −Σⱼ log P(Tⱼ | Tⱼ(x))** — landet jede transformierte Version im richtigen Cluster? Niedrige P → hoher Score → Anomalie

## CutPaste (Folien 62–65)

- Für **kleine, lokale Defekte** (Kratzer in Fertigung) — bisherige Verfahren sehen eher globale Anomalien
- Selbstüberwacht mit Pseudo-Anomalien: Rechteck aus dem Bild kopieren + woanders einfügen
- 3 Klassen: **unverändert / normales CutPaste / CutPaste Scar** (sehr klein + dünn)
- Nach Training: Klassifikationsschicht abschneiden → CNN = Merkmalsextraktor f
- Score = Gauß-Dichte im Merkmalsraum, μ/Σ aus Normaldaten — also **Mahalanobis auf f(x)** (vgl. Elliptic Envelope)

## Contrastive Learning / SimCLR (Foliensatz 08a)

- Contrastive: Encoder lernt, ähnliche von unähnlichen Samples zu trennen; Ähnlichkeitsmaß = **Cosinus-Ähnlichkeit**; Contrastive Loss mit **Temperaturfaktor τ**
- SimCLR: positive Paare = 2 Augmentierungen desselben Bilds (t, t′ aus 𝒯), negative = alle anderen; Architektur: f(·) (z. B. ResNet ohne finale Schicht) → h, dann Projektionskopf g(·) (FC+ReLU, dann lineare FC) → z; optimiere f und g

---
