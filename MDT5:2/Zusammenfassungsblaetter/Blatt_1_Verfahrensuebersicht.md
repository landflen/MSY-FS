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
