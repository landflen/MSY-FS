# MDT5/2 — Alle Zusammenfassungsblätter (Gesamtdokument)

> Zusammengeführte Version aller 8 Blätter zum Durchscrollen/Drucken.
> Die Einzeldateien sind die Originale — bei Änderungen dort dieses Dokument neu erzeugen.

**Inhalt:**
1. Blatt ① Verfahrensübersicht + Grundbegriffe (Kap. 1/2)
2. Blatt ②③ Shapes & Keras (Kap. 3)
3. Blatt Abstand: kNN, iForest (Kap. 4)
4. Blatt ⑥ Evaluierung + Leakage (Kap. 5)
5. Blatt Probabilistisch: Mahalanobis, KDE, GMM (Kap. 6)
6. Blatt ⑤ Rekonstruktion: AE, VAE, GAN, AnoGAN (Kap. 7/7a)
7. Blatt Clustering/PCA (Kap. 7a)
8. Blatt ④ SVM, OCSVM, Deep SVDD, GOAD (Kap. 8/8a)



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

**Eingeklammert auf der Folie = optional, NICHT klausurrelevant** — beim Nachzeichnen mitklammern, aber nicht lernen. LOF + Matrix Profiles (Foliensatz 03a) sind deshalb aus allen Blättern/Übungen entfernt.

## Die große Verfahrenstabelle

| Verfahren | Score | Wichtigste Metaparameter | Norm.? | Geeignet | Ungeeignet / Schwäche |
|---|---|---|---|---|---|
| **kNN-Abstand** | mittl. Abstand zu k Nachbarn | k, Abstandsmaß | JA | einfach, wenig Daten | langsam; hohe Dim. (Curse of Dim.); Rauschen |
| **iForest** | s = 2^(−E(h)/c(n)) ∈ [0;1], →1 Ausreißer | n_estimators (100), max_samples (256), contamination | **NEIN** | hohe Dim., große Daten, schnell | einzelne Bäume instabil (→ Ensemble) |
| **Mahalanobis / EllipticEnvelope** | (neg.) Mahalanobis-Abstand (Ellipse) | contamination | (robust ggü. Skala) | korrelierte Merkmale, **unimodal** | **multimodale Daten!** |
| **KDE** | log-Dichte | Bandbreite h (GridSearch auf Train-log-Dichte) | JA | **beliebige/multimodale Verteilungen** | h-Wahl; alle Trainingspunkte nötig |
| **GMM** | Dichte der Mischverteilung | Modenzahl k, Init (k-Means) | JA | multimodal, wenn k bekannt | EM langsam, lokale Minima |
| **k-Means** | Abstand zum nächsten Zentrum | k (Elbow/Silhouette), k-means++ | JA | gruppierte Daten, kugelige Cluster | **nicht-kugelförmige Cluster** |
| **PCA** | Rekonstruktionsfehler | k bzw. Varianzerhalt 95–99 % | JA | lineare Strukturen, Dim.-Reduktion | **nichtlineare Strukturen** (→ Kernel PCA) |
| **Autoencoder** | Rekonstruktionsfehler | Architektur, dim(z) < dim(x)! | JA (z. B. [0;1]) | Bilder/hochdim., viele Daten | Fehler instabil (→ Ensemble/RandNet); braucht viele Daten |
| **VAE** | Reconstruction Probability (mehrfach sampeln) | Architektur, A-priori N(0,1) | JA | wie AE + Datengenerierung | Aufwand |
| **AnoGAN** | L = (1−λ)L_res + λL_disc nach z-Optimierung | λ (0,1), Iterationen (500), z_dim | JA | Bilder, gute Datenqualität | **langsam: z-Optimierung pro Sample!**; GAN-Training heikel |
| **f-AnoGAN** | wie AnoGAN, aber via Encoder G(E(x)) | wie AnoGAN + Encoder | JA | wie AnoGAN, schnelles Scoring | 3-stufiges Training |
| **OC-SVM** | Abstand zur Trennebene (vom Ursprung) | **ν** (Ausreißeranteil), **γ** (RBF) | **JA! (Standardis.)** | wenig Daten, hohe Dim. | große Datenmengen (Training langsam); braucht RBF |
| **SVDD** | Abstand zur Kugeloberfläche | ν, Kernel | JA | wie OC-SVM (Gauß-Kernel: äquivalent!) | wie OC-SVM |
| **Deep SVDD** | ‖φ(x)−c‖² − R² (>0 = Anomalie) | ν, λ (Weight Decay), Architektur | JA | Bilder/hochdim., viele Daten | **Verbotsliste!** (Bias, gedeckelte Akt., c) |
| **GOAD** | −Σ log P(richtige Transformation) | M Transformationen, λ₁=0,1, λ₂=10, s=1 | JA | Bilder + allgemeine Daten (affine T.) | Wahl der Transformationen |
| **CutPaste** | Gauß-Dichte im Merkmalsraum | Patch-Parameter | JA | **kleine lokale Defekte** (Fertigung) | globale Anomalien |

## Entscheidungsbaum für Verfahrenswahl-Aufgaben (Typ 8/12)

1. **Plot ansehen: eine kompakte Punktwolke (unimodal)?** → Mahalanobis/Elliptic Envelope ok
2. **Mehrere Cluster (multimodal)?** → KDE, GMM, k-Means; Elliptic Envelope FALSCH (Ellipse über alles)
3. **Cluster nicht kugelig / verschachtelt (Ringe, Bänder)?** → k-Means FALSCH, PCA (linear) FALSCH; KDE, OCSVM (RBF) ok
4. **Hochdimensional (Bilder)?** → Deep-Verfahren (AE, Deep SVDD, GOAD, f-AnoGAN); Abstand/KDE leiden unter Curse of Dim.; iForest ok
5. **Wenige Trainingsdaten?** → OCSVM stark, Deep-Verfahren FALSCH (Datenhunger)
6. **Kleine lokale Bilddefekte?** → CutPaste
7. Bei Begründung IMMER nennen: passt die Modellannahme (Verteilungsform/Clusterform/Linearität) zum Plot + Datenmenge/Dimension

## Merkzettel Normalisierung (Kap. 2)

- Min-Max → [0;1]: x′ = (mᵢ − minᵢ)/(maxᵢ − minᵢ); empfindlich ggü. Ausreißern; `MinMaxScaler`
- Standardisierung (Z-Transf.): x′ = (mᵢ − μᵢ)/σᵢ → μ=0, σ=1; robuster, kein fester Bereich; `StandardScaler`
- min/max/μ/σ IMMER nur aus Trainingsdaten (fit auf Train, transform auf Train+Test) → sonst Data Leakage
- Nötig bei allem, was Abstände/Skalarprodukte rechnet (kNN, k-Means, KDE, SVM/OCSVM, PCA, NN-Eingaben); NICHT nötig bei iForest (nur Splits)


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

**Gewichte zählen (Folie 45):**
- Conv2D: C_in · k · k · filters   (Bias: + filters)
- Dense: n_in · n_out   (Bias: + n_out)
- Bsp. 1. Schicht VGG: 3·3·3·32 = 864;  2. Schicht: 32·3·3·32 = 9 216

**Beispiel-Kette (mod. VGG16, Folie 43):**
32×32×3 → 32×32×32 → 16×16×64 → 8×8×128 → 4×4×256 → 2×2×256 → Flatten → 1024 → 1024 → 7 (Softmax)

---

## Aktivierung + Kostenfunktion nach Aufgabe (Folien 11–21)

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
5. Abhängige Samples (gleicher Proband/gleiche Serie) in Train UND Test? → verstecktes Overfitting
6. Novelty Detection: Anomalien in Trainingsfolds der CV? → falsche Aufteilung (s. o.)
7. Accuracy bei stark unbalancierten Daten als einzige Metrik? → falsche Metrik (bal. acc / Precision+Recall / AUC)

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
  3. Wiederholen bis Konvergenz:
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
| Achtung | Ellipse über allen Daten | h via GridSearch auf Train-log-Dichte | langsam, lokale Minima |


---

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


---

# Blatt — k-Means, Elbow/Silhouette, PCA, Kernel PCA (Kap. 7a)

> Vorlage zum handschriftlichen Übertragen. Quelle: Foliensatz 07a (Folien 2–26; VAE-Teil → Blatt ⑤).
> Deckt Aufgabentyp 11 (Clustering) ab. Zielumfang: 1,5 A4-Seiten.

---

## k-Means (Folien 20–26)

**Algorithmus:**
1. Anzahl Cluster k wählen (+ max. Iterationen)
2. Cluster-Zentren initialisieren
3. Wiederholen bis keine Änderung / max. Iterationen:
   I. Abstand jedes Punkts zu allen Zentren
   II. Punkt → Cluster mit nächstem Zentrum
   III. Zentren neu berechnen (Mittelwert)

**Initialisierung — k-means++ (Standard):** 1. Zentrum zufällig gleichverteilt; dann wiederholt: Abstände zum nächsten Zentrum berechnen, neues Zentrum ziehen mit Wahrscheinlichkeit ∝ quadriertem Abstand. (Rein zufällige Initialisierung → evtl. schlechte, „festgefahrene" Cluster)

**k bestimmen — zwei Verfahren (Plots lesen können!):**
1. **Elbow-Methode**: Summe der quadrierten Abstände zum nächsten Zentrum (sklearn: `inertia_` nach fit) gegen k plotten → „Knick" wählen, bevor Kurve abflacht. Intuitiv, aber subjektiv/nicht eindeutig
2. **Silhouetten-Analyse**: S(p) = (b − a) / max(a, b) ∈ [−1; 1]
   - a = mittlerer Abstand von p zu Punkten im **eigenen** Cluster
   - b = mittlerer Abstand von p zu Punkten im **nächsten** Cluster
   - Silhouettenkoeffizient = Mittel über alle Punkte; **je höher, desto dichter die Cluster**
   - sklearn: `silhouette_score` (Mittel), `silhouette_samples` (einzeln)
   - Achtung: Cluster-Nummern zwischen Läufen nicht vergleichbar (zufällige Init.)
- In der Praxis: mehrere Verfahren kombinieren

**k-Means zur Anomalieerkennung:**
- Novelty Detection: Clustering auf Normaldaten → Score = **Abstand zum nächsten Cluster-Zentrum** (hoch = Anomalie)
- Grenze (Verfahrenswahl!): Cluster sind **kugelförmig** → Probleme bei länglichen/verschachtelten Formen
- Outlier Detection: eher schwierig; Hinweise = kleine Cluster, Punkte mit hohem Abstand zum Zentrum
- **Normalisierung nötig** (abstandsbasiert!)
- sklearn: `sklearn.cluster.KMeans`

## PCA — Hauptachsentransformation (Folien 3–11)

**Idee:** Finde orthogonale Hauptachsen mit größter Varianz der Daten → neues Koordinatensystem; Achsen mit kleinster Varianz weglassen = Projektion.

**Anwendungsrezept (Folie 9):**
1. Daten **zentrieren**: x̃ᵢ = xᵢ − x̄
2. Datenmatrix X aufstellen
3. Eigenvektoren/Eigenwerte der Kovarianzmatrix C = 1/(n−1)·XXᵀ via **SVD**(X) = USVᵀ (quadrierte Singulärwerte = Eigenwerte)
4. Auf k Dimensionen projizieren: k größte Eigenwerte + zugehörige Eigenvektoren
- **Faustregel: k so, dass 95–99 % der Varianz erhalten** (Summe der k größten Eigenwerte / Summe aller)
- **Vorher normalisieren!** Sonst überdeckt ein Merkmal mit großem Wertebereich die anderen
- sklearn: `sklearn.decomposition.PCA`, `n_components` = ganze Zahl k ODER Wert ∈ (0,1) = Varianzerhalt

**Grenzen von PCA (Folie 11, Verfahrenswahl!):**
- Daten müssen sich durch Mittelwert + Varianz beschreiben lassen (≈ Normalverteilung)
- Variabilität muss **linear** sein → bei nichtlinearen Strukturen keine gute Trennung

**Kernel PCA (Folien 12–16):** Kernel-Trick (Kernels wie bei SVM) → PCA im hochdimensionalen nichtlinearen Raum; Eigenvektorproblem auf Kernel-Matrix K̃ (zentriert); Projektion über Σⱼ αᵢⱼ·k(x, xⱼ)

**PCA zur Novelty Detection (Folie 17):**
- PCA nur mit Normaldaten trainieren; Dimensionsreduktion „kapselt" die Normaldaten
- **Rekonstruktionsfehler** neuer Daten = Anomalie-Score (deshalb zählt PCA zu den rekonstruktionsbasierten Verfahren!)

---

## Schnellvergleich fürs Verfahrenswahl-Blatt ①

| | k-Means | PCA | Kernel PCA |
|---|---|---|---|
| Score | Abstand zum nächsten Zentrum | Rekonstruktionsfehler | Rekonstruktionsfehler |
| Grenze | kugelförmige Cluster | nur linear, ~Normalvert. | Kernelwahl nötig |
| Metaparameter | k (Elbow/Silhouette), Init | k bzw. Varianzerhalt 95–99 % | Kernel + Parameter, k |
| Normalisierung | JA | JA | JA |


---

# Blatt ④ — SVM, OCSVM, Deep SVDD, GOAD, CutPaste, Contrastive (Kap. 8 + 8a)

> Vorlage zum handschriftlichen Übertragen. Quellen: Foliensatz 08 + 08a.
> Deckt Aufgabentypen 6/7 (SVM/OCSVM zeichnen) + 10 (Deep-SVDD-Code beurteilen) ab. Zielumfang: ~2,5 A4-Seiten.

---

## SVM überwacht (Folien 5–30) — fürs Zeichnen (Typ 6)

- Hyperebene h₀: wᵀx + b = 0; Parallelebenen h₁/h₂: wᵀx + b = ±1
- **Optimale Ebene = maximaler Abstand (Margin) zu den nächsten Punkten beider Klassen = Support Vektoren**; Ebene hängt NUR von den SV ab
- Margin zwischen h₁ und h₂ = 2/‖w‖ → min ½‖w‖² unter yᵢ(wᵀxᵢ + b) ≥ 1
- Klassifikation: y = sgn(wᵀx − d) bzw. f(x) = sgn(Σ yᵢαᵢ·k(x, xᵢ) + b), Summe nur über SV

**Zeichenregeln (Typ 6):**
1. SV = die Punkte beider Klassen, die der Trennlinie am nächsten liegen (meist 2–3 Stück)
2. Trennlinie mittig zwischen den SV, Margin symmetrisch
3. Punkte, die keine SV sind, dürfen sich bewegen/entfallen ohne Änderung der Ebene
4. Entfernt man einen SV → Ebene ändert sich!

**Soft Margin / Straffaktor C (Folie 10):**
- Schlupfvariablen ξᵢ erlauben Verletzungen: yᵢ(wᵀxᵢ+b) ≥ 1 − ξᵢ; L = ½‖w‖² + C·Σξᵢ
- **C groß → wenig Verletzungen erlaubt, schmaler Margin** (Tendenz Overfitting); **C klein → mehr Verletzungen, breiter Margin** (robuster)
- C in logarithmischen Intervallen testen
- Alternative ν-SVM: ν ∈ (0;1] = untere Schranke für Anteil der SV, obere Schranke für Margin-Verletzer (intuitiver als C)

**Kernel-Trick (Folien 15–27):**
- Duales Problem enthält Daten NUR als Skalarprodukte xᵢᵀxⱼ → ersetze durch Kernel k(a,b) = φ(a)ᵀφ(b)
- → implizite Transformation in höherdimensionalen Raum, ohne ihn je zu berechnen; linear dort = nichtlinear im Original
- Kernels: **linear** aᵀb; **polynomial** (c + aᵀb)^p; **RBF/Gauß** e^(−γ‖a−b‖²)
- RBF: bildet auf Einheitskugel in ∞ Dimensionen ab (‖φ(x)‖ = 1); **γ groß → schmale Glocke, enge Anpassung; γ klein → glatter**
- γ logarithmisch testen oder γ = 1/(dim·var(X))

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
- **SVDD** (Folie 35): findet **Kugel** (Radius R, Zentrum c), die Normaldaten umschließt: min R² + 1/(νn)·Σξᵢ mit ‖xᵢ−c‖² ≤ R² + ξᵢ. **Mit Gauß-Kernel: SVDD ≡ OCSVM**

## Deep SVDD (Folien 40–52) — Verbotsliste! (Typ 10)

**Ziel:** Netz φ(·; W) bildet Normaldaten in Kugel (c, R) mit minimalem Volumen ab.
Vereinfachte Zielfunktion: min_W 1/n·Σ ‖φ(xᵢ;W) − c‖² + λ/2·Σ‖Wˡ‖²

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
- **Triplet Center Loss**: max(0, ‖f(Tⱼx)−cⱼ‖² + s − min_{k≠j} ‖f(Tⱼx)−cₖ‖²) → Intra-Abstand klein, Inter-Abstand groß (s ≈ 1)
- Gesamt: L = L_ce (Kreuzentropie „welche Transformation?" als Stabilisierung) + λ₁·L_tc + λ₂/N·Σ‖zᵢ‖² — Standardwerte **λ₁ = 0,1; λ₂ = 10**
- **Score(x) = −Σⱼ log P(Tⱼ | Tⱼ(x))** — Wahrscheinlichkeit, dass jede transformierte Version im richtigen Cluster landet; ε als Regularisierung. Niedrige P → hoher Score → Anomalie

## CutPaste (Folien 62–65)

- Für **kleine, lokale Defekte** (Kratzer in Fertigung) — bisherige Verfahren sehen eher globale Anomalien
- Selbstüberwacht mit Pseudo-Anomalien: Rechteck aus dem Bild kopieren + woanders einfügen
- 3 Klassen: **unverändert / normales CutPaste / CutPaste Scar** (sehr klein + dünn)
- Nach Training: Klassifikationsschicht abschneiden → CNN = Merkmalsextraktor f
- Score = Gauß-Dichte im Merkmalsraum: log p ∝ −½(f(x)−μ)ᵀΣ⁻¹(f(x)−μ), μ/Σ aus Normaldaten (vgl. Mahalanobis/Elliptic Envelope!)

## Contrastive Learning / SimCLR (Foliensatz 08a)

- Contrastive: Encoder lernt, ähnliche von unähnlichen Samples zu trennen; **Cosinus-Ähnlichkeit** sim(v,v′) = vᵀv′/(‖v‖‖v′‖); Contrastive Loss mit **Temperaturfaktor τ**
- SimCLR: positive Paare = 2 Augmentierungen desselben Bilds (t, t′ aus 𝒯), negative = alle anderen; Architektur: f(·) (z. B. ResNet ohne finale Schicht) → h, dann Projektionskopf g(·) (FC+ReLU, dann lineare FC) → z; optimiere f und g
