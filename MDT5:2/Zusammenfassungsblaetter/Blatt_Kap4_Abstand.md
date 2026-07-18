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
