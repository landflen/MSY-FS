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
