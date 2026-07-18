# MDT5/2 — Lern-Logbuch (Maschinelles Lernen zur Anomalieerkennung)

> **Zweck:** Sparsames Logbuch nach dem Muster von INF4:1/CLAUDE.md — Fortschritt,
> Stolperfallen, Planänderungen in wenigen Zeilen. Plan, Aufgabentypen und Arbeitsweise
> stehen in `Lernplan_MDT52.md` und werden hier **nicht** dupliziert.
> Prüfung: **Fr 31.07.2026, 11:00** — Open Book (Skript + handschriftliche Blätter, KEINE Praktika).

## Sessionfortschritt

- **S1 (8.7.)** ✅ Kap. 1+2, Blatt 1 korrigiert. Nacharbeit (Praktika 01a/01b + NumPy-Blatt) → 22.7.
- **S2 (18.7., geplant 17.7.)** ✅ Kap. 3a/4 (kNN, iForest — LOF/Matrix Profiles laut
  Klammer-Regel nicht klausurrelevant, aus Blatt/Vorlagen entfernt) + Praktikum 02
  (Outlier/Novelty am Breast-Cancer-Datensatz) + Blatt `Session02_Abstand` gelöst und
  korrigiert (~⅔ richtig; Fehlerbild → Stolperfallen 1–4).
  - Notebook-Fragen beantwortet, mit fremder Mitschrift abgeglichen, korrigiert.
  - Blatt_Kap4_Abstand handschriftlich übertragen ✅ (18.7.).
  - **Noch offen aus S2:** Blatt ① handschriftlich übertragen und um die S2-Befunde
    ergänzen (Kontrastpaar Min-Max vs. z-Transformation, s-Grenzfälle des iForest,
    contamination-Definition, sklearn-Dreizeiler).

## Stolperfallen (vor der Klausur gezielt wiederholen)

1. **StandardScaler ≠ [−1, 1] — zweimal aufgetreten (17.7.).** StandardScaler = z-Transformation:
   Mittelwert 0, Standardabweichung 1, **kein fester Wertebereich**. Min-Max-Normalisierung:
   Default [0, 1]; [−1, 1] nur mit `feature_range=(-1, 1)`. Namen nicht mischen
   („Min-Max-Standardisierung" gibt es nicht).
2. **Aufgabenparameter k überlesen (Blatt S2, Aufg. 2).** k = 2 gefordert, mit 3 Nachbarn
   gerechnet — in a) zufällig gleiches Ergebnis, in b) falsch (√17 statt ≈ 4,8).
   Rezept: Abstände sortieren → **genau k Stück abzählen** → durch k teilen.
3. **Begründungen zu allgemein für den MC-Begründungsstil.** Beispiele 17.7.: „fit trainiert,
   predict klassifiziert" (gilt für jedes Verfahren — Kern bei Novelty: fit **nur auf
   Normaldaten** + **getrennter** predict); Schwellwert s > √2 gewählt, obwohl die
   Trainingspunkte selbst Score 2 haben (Schwelle immer gegen typischen Normal-Score prüfen).
4. **contamination falsch definiert.** Richtig: **erwarteter Anteil an Ausreißern in den
   Daten** → legt den Schwellwert für die ±1-Entscheidung fest; `'auto'` = feste Schwelle aus
   der Score-Definition. Ändert am AUC nichts
   (AUC ist schwellwertunabhängig, bewertet nur die Scores).
5. **ROC-Betriebspunkt wird über den Schwellwert gewählt, nicht über die Datenzusammensetzung**
   (17.7., Praktikum: `outlier_ratio` verstellt statt Schwelle). Knie der Kurve suchen,
   (FPR, TPR) ablesen; AUC: 1.0 perfekt, 0.5 Raten.
6. **iForest-Baumtiefe log₂(n_sub):** Begrenzung, weil Anomalien **kurze** Pfade haben — wer
   tiefer sitzt, ist ohnehin normal; tiefer bauen kostet nur Rechenzeit. (Subsampling
   n_sub = 256: dünnt Cluster aus, macht Isolation wieder möglich.)

## Gesicherte Merksätze (für die Blätter)

- **Normalisierung nötig?** kNN und andere abstandsbasierte Verfahren: ja (größter
  Wertebereich dominiert sonst den Abstand). **iForest: nein** (keine Abstände; Splits je
  ein Merkmal einzeln).
- **iForest-Grenzfälle:** E(h)→0 ⇒ s→1 (Anomalie); E(h)=c(n) ⇒ s=0,5 (unauffällig);
  E(h)→n−1 ⇒ s→0 (sicher normal).
- **sklearn-Konvention:** predict liefert **+1 = normal, −1 = Anomalie**; `score_samples` beim
  iForest negiert in [−1, 0], niedriger = anomaler.
- **Hohe Dimension/viele Punkte ⇒ iForest statt kNN** (kNN langsam in der Anwendung +
  Curse of Dimensionality: Abstände werden ähnlich).

## Änderungslog

- **2026-07-18:** Datei angelegt (S2). S1/S2-Stand eingetragen, Stolperfallen 1–6 aus
  Praktikum 02 + Blatt Session02.
