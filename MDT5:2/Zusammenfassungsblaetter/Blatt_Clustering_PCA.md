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
