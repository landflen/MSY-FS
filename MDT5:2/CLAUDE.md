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
- **S3 (20.7.)** ✅ Kap. 5 + Praktikum 03 Teil 1 (PIMA-Diabetes, fehlerhafte iForest-
  Evaluierung analysieren). Notebook-Fragen 1–4 durchgearbeitet; Blatt ⑥ um die Befunde
  ergänzt (Leakage-Checkliste Punkt 4-Zusatz + Punkt 8, „Achtung, kein Fehler"-Kasten).
  - Fundliste am PIMA-Code als Muster für Aufgabentyp 4: Label-Imputation (Median je
    Klasse) → Punkt 8; Scaler auf Gesamtdaten; Suche und Bewertung auf denselben Daten;
    Accuracy als einzige Auswahlmetrik; `random_state` beim finalen Modell nicht gesetzt.
  - Praktikum 03 Teil 2 (CIFAR) bearbeitet, Fragen beantwortet (Overfitting am Abstand
    Trainings-/Validierungskurve erkannt; Testdaten als fehlender Schlussschritt genannt ✅).
    Endstand ~0,78 train / ~0,73 val.
  - Blatt ⑥ handschriftlich übertragen ✅ (20.7.).
  - Antworten zu Praktikum 03 Teil 2 korrigiert: Fragen 1 und 4 inhaltlich richtig (zu knapp
    begründet), Frage 3 (Data Augmentation) zu dünn — beschreibt nur Schwanken statt Wirkung
    aufs Overfitting. Frage 2 nach Rückfrage **bestätigt**: fallender Trainings-Loss bei
    stagnierendem Validierungs-Loss ist Overfitting (→ Merksatz).
  - Loss-Begriff aufgearbeitet (Kreuzentropie-Skala, Loss vs. Accuracy) → Merksätze.
  - Blatt `Session03_Evaluierung` gelöst und korrigiert (20.7.): Aufg. 1 alle vier MC richtig,
    Aufg. 2 rechnerisch komplett richtig (nur Schreibfehler Precision 40/40 statt 40/90),
    Aufg. 3 richtig bis auf die Skizze „brauchbar" (fällt unter die Diagonale), Aufg. 4 b–d
    richtig, 4a Frage verfehlt (→ Stolperfalle 11), Aufg. 5 zwei von drei (→ Stolperfallen
    12–13). Schwächste Begründung: 2c (F1/Precision, → Merksatz).
  - **Nichts mehr offen aus S3** — beide zuvor notierten Punkte am 20.7. bewusst **verworfen**
    (nicht erledigt): die K/`pos_label`-Nachbesserung auf Blatt ⑥ und das Korrigieren der zwei
    CIFAR-Codefehler samt Neubewertung von Antwort 3. Stolperfallen 9–10 bleiben als Merkposten
    bestehen; die Vorlage `Blatt_6_Evaluierung_Leakage.md` behält `pos_label=1` und definiert
    K weiterhin nicht.

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
7. **Nicht jede Auffälligkeit im Code ist ein Fehler (20.7.).** „Dieselben Anomalien in jedem
   Validierungs-Fold" ist beim Novelty-CV-Rezept **gewollt** — richtig ist nur die
   Einschränkung, dass die Streuung dadurch unterschätzt wird. Bei Aufgabentyp 4 erst gegen
   das Soll-Rezept (Blatt ⑥) prüfen, bevor etwas als Fehler markiert wird.
8. **Zwei Accuracy-Zahlen sind nur vergleichbar, wenn die bewertete Menge gleich
   zusammengesetzt ist (20.7., PIMA).** Suche bewertet 768 Punkte (~65 % normal, davon 500
   aus dem Fit), CV bewertet je Fold ~100 Normale + alle 268 Anomalien (~73 % anomal).
   Accuracy hängt direkt an der Klassenprior → Abweichung erklärt sich aus
   Trainingsdaten-Bewertung **und** Verteilungswechsel, nicht aus „CV vs. predict".

9. **`10e-3` ist nicht 10⁻³ (20.7., CIFAR).** `10e-3` = 0,01, gefordert war `1e-3` = 0,001 —
   Faktor 10 zu stark reguliert. Bei Zehnerpotenzen in Code immer `1e-x` schreiben.
10. **Schicht konstruieren ≠ Schicht hinzufügen (20.7., CIFAR).** `CifarDataAugmentation(net)`
    erzeugt nur ein Objekt (und übergibt `net` als `random_flip`!) und verwirft es —
    richtig ist `net.add(CifarDataAugmentation())`. Kontrolle: `net.summary()` bzw. die
    Parameterzahl vor/nach der Änderung vergleichen.
11. **Standard-k-Fold und Novelty-CV verwechselt (20.7., Blatt S3 Aufg. 4a).** Auf die Frage
    nach dem *allgemeinen* k-Fold-Ablauf das Novelty-Rezept (Indizes trennen, Normal-Indizes
    mischen, Anomalien in jede Validierungsmenge) hingeschrieben — das ist die Antwort auf 4d.
    Standard: Testdaten zuerst abspalten → Rest in k Teilmengen → k Durchläufe mit je einer
    Validierungsmenge → Mittelwert ± Std → finale Pipeline auf ganzem Trainingsteil, Test
    einmal. **Erst prüfen, ob die Frage den Sonderfall überhaupt meint.**
12. **„Kein Fehler" ist bei Aufgabentyp 4 eine zulässige Antwort (20.7.).**
    Blatt S3 Aufg. 5 Variante B war Zeile für Zeile das Rezept von Folie 11 (Split zuerst,
    Pipeline, `refit=False`, finales Fit auf Train, Test einmal); markiert wurde trotzdem ein
    Fehler („Anomalien in Testdaten"), obwohl es gar kein Novelty-Verfahren war. Verschärfung
    von Stolperfalle 7: **Code-Ausschnitt Zeile für Zeile gegen Folie 11 legen**, erst dann
    urteilen. Zulässige Restkritik dort: kein `random_state` gesetzt.
13. **Leakage-Ursache falsch benannt (20.7., Blatt S3 Aufg. 5 Variante A).** „In der
    Parametersuche wird mit Testdaten trainiert" — es gab keine Parametersuche. Ursache war
    `SelectKBest.fit_transform(features, labels)` **vor** dem Split: Die Merkmalsauswahl sieht
    Testdaten *und* Testlabels. In der Klausur nicht nur „Leakage" schreiben, sondern die
    **Codezeile** benennen, die zu früh auf den Gesamtdaten arbeitet.
14. **Lücken im Histogramm erst gegen die Binbreite prüfen (20.7., PIMA).** Bei ganzzahligen
    Merkmalen erzeugt `bins=20` auf Wertebereich 0–17 leere Bins (Breite 0,85) — sah nach
    fehlenden Werten bei „5 Schwangerschaften" aus, war reines Darstellungsartefakt. Echte
    fehlende Werte: isolierter Balken bei exakt 0, abgesetzt von der Verteilung
    (Glucose, BloodPressure, SkinThickness, **Insulin**, BMI).

## Gesicherte Merksätze (für die Blätter)

- **Welche Metrik ist „am ehrlichsten"?** Nicht die, die Unbalanciertheit *einbezieht*, sondern
  die, die die große Klasse **nicht** enthält: F1 und Precision kennen keine TN — und genau die
  vielen TN blähen die Accuracy auf. Reihenfolge des Aufdeckens: Accuracy lügt → bal. Accuracy
  beschönigt noch → **Precision deckt auf**. Recall allein ist kein Ehrlichkeitsmaß: Er kann
  hoch sein, während massenhaft Fehlalarme laufen (Beispiel S3: Recall 0,8 bei Precision 0,44).
- **ROC-Schwellwert ablesen:** Punkt am Knie bzw. mit kleinstem Abstand zu (0,1) wählen,
  zugehörigen Wert aus dem `thresholds`-Array nehmen; Verschiebung je nachdem, ob FP oder FN
  teurer sind. Die „brauchbare" ROC-Kurve liegt beim Skizzieren immer **über** der Diagonalen.
- **Normalisierung nötig?** kNN und andere abstandsbasierte Verfahren: ja (größter
  Wertebereich dominiert sonst den Abstand). **iForest: nein** (keine Abstände; Splits je
  ein Merkmal einzeln).
- **iForest-Grenzfälle:** E(h)→0 ⇒ s→1 (Anomalie); E(h)=c(n) ⇒ s=0,5 (unauffällig);
  E(h)→n−1 ⇒ s→0 (sicher normal).
- **sklearn-Konvention:** predict liefert **+1 = normal, −1 = Anomalie**; `score_samples` beim
  iForest negiert in [−1, 0], niedriger = anomaler.
- **Hohe Dimension/viele Punkte ⇒ iForest statt kNN** (kNN langsam in der Anwendung +
  Curse of Dimensionality: Abstände werden ähnlich).
- **Overfitting-Kriterium: Kurven laufen auseinander.** Trainings-Loss fällt weiter, während
  Validierungs-Loss **stagniert oder steigt** — Stagnation genügt, ein Anstieg ist nicht nötig.
  Ein bloßer Abstand zwischen beiden Kurven ist noch kein Overfitting; bloßes Schwanken des
  Validierungs-Loss ist Rauschen (Mini-Batches/Shuffling).
- **Loss-Skala (Kreuzentropie):** Loss = −log(Wahrscheinlichkeit der **richtigen** Klasse),
  nach unten 0 (perfekt), **nach oben unbegrenzt** — auch bei 2 Klassen. Ratewert = log(Anzahl
  Klassen): **2,30 bei 10 Klassen, 0,69 bei 2**. Das ist die Startlinie, keine Obergrenze —
  schlechter als Raten geht (selbstbewusst falsch: p = 0,01 ⇒ Loss 4,6).
- **Loss vs. Accuracy:** Loss nutzt die Wahrscheinlichkeiten und ist ableitbar → wird
  optimiert. Accuracy zählt nur richtig/falsch (Sprungfunktion, nicht ableitbar) → reine
  Anzeige, steht in `metrics`, nie in `loss`. Können auseinanderlaufen: Accuracy konstant,
  aber val_loss steigt = Netz wird bei seinen Fehlern selbstsicherer.
- **Angezeigter Loss enthält den L2-Strafterm.** Läufe mit unterschiedlichem λ sind über den
  Loss **nicht** vergleichbar (Startwert liegt dann über dem Ratewert) — für den Vergleich
  Accuracy oder die Größe der Kurvenlücke nehmen.
- **Data Augmentation ist nur im Training aktiv.** Trainings-Accuracy kann dadurch **unter**
  die Validierungs-Accuracy fallen (schwerere Aufgabe auf augmentierten Bildern) — sieht falsch
  aus, ist korrekt. Konvergenz wird langsamer ⇒ ggf. mehr Epochen.

## Änderungslog

- **2026-07-18:** Datei angelegt (S2). S1/S2-Stand eingetragen, Stolperfallen 1–6 aus
  Praktikum 02 + Blatt Session02.
- **2026-07-20:** S3 eingetragen (Kap. 5 + Praktikum 03 Teil 1), Stolperfallen 7–8.
- **2026-07-20 (Nachtrag):** Praktikum 03 Teil 2 (CIFAR) ergänzt, Stolperfallen 9–11,
  offene Blatt-⑥-Korrektur (K/`pos_label`) vermerkt.
- **2026-07-20 (Nachtrag 3):** Blatt `Session03_Evaluierung` korrigiert; Stolperfallen 11–13
  (Standard-CV vs. Novelty-CV, „kein Fehler" als Antwort, Leakage-Ursache benennen) und
  Merksätze zu Metrik-Ehrlichkeit und ROC-Schwellwert ergänzt. Die beiden offenen S3-Punkte
  (Blatt ⑥ K/`pos_label`, CIFAR-Codefehler) verworfen.
- **2026-07-20 (Nachtrag 2):** Blatt ⑥ als übertragen markiert; Antwortkorrektur Praktikum 03
  Teil 2 und Merksätze zu Overfitting-Kriterium, Loss-Skala, Loss vs. Accuracy, L2 im
  angezeigten Loss und Data Augmentation ergänzt.
