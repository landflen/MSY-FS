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
