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
  - **Blatt ① handschriftlich übertragen ✅ (26.7.).** Damit ist S2 abgeschlossen.
    - Die vier S2-Befunde standen bis 26.7. **nicht** in der Vorlage, nur im Logbuch; am 26.7. in
      `Blatt_1_Verfahrensuebersicht.md` eingebaut (Kontrastpaar Min-Max vs. z-Transformation unter
      „Merkzettel Normalisierung"; neuer Abschnitt „Kleingedrucktes zu Scores & sklearn" mit
      iForest-s-Grenzfällen, contamination = Anteil/Schwellwert, sklearn-Dreizeiler
      fit/predict/score_samples) — **handschriftlich nachgetragen ✅ (26.7.)**.
- **Praktikum 04 (23.7.)** ✅ Probabilistische Verfahren (KDE, GMM, Elliptic Envelope) am
  Breast-Cancer-Datensatz komplett durchgearbeitet, alle Notebook-Fragen beantwortet und
  korrigiert. Metaparameterwahl über Mittelwert-/Streuungs-Plots geübt (KDE unüberw. bw≈0.5,
  überw. bw=2 am AUC-Plateau; GMM n=1 überw. wie unüberw.). Elliptic-Envelope-Kern verstanden:
  contamination = Schwellwert, nicht Formparameter → Grid-Search-Kurven **und** AUC flach,
  unüberwacht nicht schätzbar. Novelty→Outlier-Detection-Übergang (Fit auf kontaminierten
  Daten, TPR fällt auf 0.72). Stolperfallen 15–18 + Merksätze zu EE/contamination und
  Novelty-vs-Outlier ergänzt.
  - **Blatt `Probabilistisch` handschriftlich übertragen und geprüft ✅ (23.7.)** — treue
    Übertragung der Vorlage, inhaltlich vollständig. Restschliff notiert: „Modalverteilung"
    → „Normalverteilung" (unimodal) in der Tabelle, Transpose ᵀ gehört auf die ganze Klammer
    (x−μ)ᵀ, KDE-Summe = k(·) als Funktion (nicht Multiplikation). KDE(x) vs. k als zwei Funktionen
    geklärt (k = einzelner Gauß-Hügel je Punkt, KDE(x) = 1/(N·h)·Summe aller Hügel).
  - **Blatt `Session04_Probabilistisch` gelöst und korrigiert ✅ (24.7.):** 12 richtig, 4 teilweise,
    1 falsch. Aufg. 1 alle vier MC-Kreuze richtig (1.3 Begründung „Anzahl" statt „Anteil"),
    Aufg. 2 komplett richtig (2c ohne eingezeichneten Eckpunkt), Aufg. 3 a/c/d richtig,
    **3b falsch** (→ Stolperfalle 19), Aufg. 4 b/c richtig, 4a Zweck der Normalisierung verfehlt,
    Aufg. 5 schwächste Aufgabe (→ Stolperfalle 20), Aufg. 6 Reihenfolge richtig, E/M-Beschreibung
    ausgelassen (→ Stolperfalle 21). Durchgehendes Muster: **Begründung passt nicht zur gestellten
    Frage**, und nicht alle Teilfragen beantwortet.
- **S5 (24.7.)** 🟡 **teilweise — Rest auf Di 28.7. 14–16** (So-26.7.-Puffer am 24.7. gestrichen).
  Praktikum 05 (Deep Learning, MNIST)
  bis einschließlich CNN-Teil bearbeitet: Dense-Netz und CNN aufgebaut, Fragenblöcke 1 und 2
  beantwortet und korrigiert.
  - **Erledigt:** FC-Netz (Shape-/Aktivierungs-Syntaxfehler behoben), Dropout-Vergleich,
    CNN nach Vorgabe (6/12/24 Filter, strides=2, BatchNorm) — Architektur korrekt bis auf
    ReLU statt Softmax in der Ausgabeschicht (→ Stolperfalle 22). Learning-Rate-Frage mit
    frisch erzeugtem Netz wiederholt ✅.
  - **Blätter ② + ③ komplett handschriftlich übertragen ✅ (24.7.)** — inkl. Training
    (Folien 22–23: Learning Rate, SGD auf Batch, Schritt vs. Epoche, Metaparameter-vs-gelernte-
    Parameter-Liste) und Fehlerfinder-Checkliste (Aufgabentyp 4/5). **Noch offen: Korrektur-
    lesen** der Blätter.
  - **Offen — verlegt auf Di 28.7. 14–16** (So-26.7.-Puffer gestrichen): (1) Notebook Teil 3 —
    binäres CNN, unbalanciertes Anomalie-Setup (`number_of_anomaly_samples = 50`) + `class_weight`,
    3 Fragen. (2) Blätter ②/③ Korrektur lesen (nach S6 ggf. um Conv2DTranspose erweitern).
    ~~(3) Blatt `Session05_NeuronaleNetze`~~ → am 26.7. gelöst.
  - **Blatt `Session05_NeuronaleNetze` gelöst und korrigiert ✅ (26.7.):** Aufg. 1 drei von vier
    MC richtig (**1.3 BatchNorm falsch angekreuzt** → Stolperfalle 32), Aufg. 2 vier von neun
    Shapes falsch aus **einem** Rechenfehler (64/2 = 34 statt 32; Endwert 4096 trotzdem richtig,
    weil sich valid-Conv und ceil kompensieren → Stolperfalle 33), Aufg. 3b richtig, 3a unklar
    notiert (Kernelfläche 3·3 fehlt), **3c Schlussfolgerung invertiert** (→ Stolperfalle 34),
    Aufg. 4 b/c/d komplett richtig inkl. Formeln, **4a N_out = 1 statt 2** (Höhe *und* Breite
    überlesen, Muster von Stolperfalle 2), Aufg. 5 alle drei Netze richtig erkannt und begründet,
    Aufg. 6 c/d/e richtig, **6a falsch** (σ'(z) ≤ 1 statt 0,25, „Überanpassung hinten") und
    **6b halb** (Oberbegriff Unstable Gradients ✅, Richtung des Explodierens falsch)
    → Stolperfalle 35.
  - 🔁 **Offen, von Lena selbst markiert (26.7.): Aufg. 6a/6b nochmal durchgehen** —
    Kettenregel-Argument mit σ'(z) ≤ 0,25 und die Laufrichtung beider Gradientenprobleme
    (Backprop von hinten nach vorn ⇒ beides eskaliert Richtung **Eingangsschicht**).
    Wortlaut steht in Stolperfalle 35.
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
- **S6 (25.7.)** 🟡 **Praktikum 06 (Simple + Convolutional Autoencoder, MNIST, normal_label=7)**
  komplett durchgearbeitet — beide Netze selbst aufgebaut, alle Notebook-Fragen beantwortet und
  korrigiert. Konzepte durchgesprochen: Latent Space = Bottleneck in der Mitte (niedrigere
  Dimension verhindert Identität), RandNet-Maske ≠ Dropout (einmalig fest auf Verbindungen vs.
  pro Schritt neu auf Neuronen), End-to-End vs. AE-als-Initialisierungsschritt (Folien 154–165),
  255-Sentinel-Umkodierungstrick beim Label-Remapping. Kernbotschaft mehrfach: **AE klassifiziert
  nichts — nur Rekonstruktionsfehler**, Schwellwert macht die Klasse.
  - **Simple AE:** Struktur 784→200→100→**10**(z)→100→200→**784** aufgebaut; Fehler behoben:
    fehlende Ausgabeschicht `Dense(784, sigmoid)` vor dem `Reshape` (200≠784-Crash), `get_shape()`
    → `.shape` (Keras-3-Versionsfehler), `.shape()` → `.shape` (Property, keine Methode).
  - **Convolutional AE:** nach Vorlage aufgebaut (Conv strides=2 → Flatten → Dense z → Dense →
    Reshape → Conv2DTranspose strides=2). Mehrere Struktur-/Reihenfolgefehler korrigiert
    (→ Stolperfalle 27). Endstand: AUC 0.96 (Simple AE 0.95), normals acc 0.983, anomalies 0.71 —
    praktisch gleichauf, Conv-Vorteil bei kleinen 28×28-Ziffern noch gering.
  - Notebook-Frageblöcke beider AEs korrigiert: überwiegend richtig, wiederkehrender Denkfehler
    „AE klassifiziert / sigmoid wegen binärer Klassifikation" (→ Stolperfalle 25).
  - **Praktikum 07 (Extended Autoencoder, RandNet-Ensemble, KDD-Cup 1999, `outlier_ratio=0.01`)**
    im Anschluss bearbeitet — reine **Outlier** Detection, unüberwacht, 30 Netze × 100 Epochen.
    Versionsfehler behoben: `np.float` → `float` in `return_kdd99_outlier_set` (seit NumPy 1.24
    entfernt; in den restlichen Praktika 08–11 mit demselben Fehler zu rechnen, ebenso
    `plt.boxplot(labels=)` → `tick_labels=`).
    - **Schwellwertwahl blind geübt** (sortierter Score-Plot + Histogramm): erste Schätzung 0.8
      aus dem Histogramm = **35 % geflaggt** → viel zu niedrig (→ Stolperfalle 30). Aus dem
      bekannten Anteil berechnet: Schwellwert **4.26**, damit **TPR nur 0.25** bei TNR 0.99.
      Kernbefund → Merksatz: Quantil-Schwellwert trifft die **Anzahl**, nicht die **Punkte**.
    - Notebook-Fragen beantwortet und korrigiert: 1 falsch, 3 teilweise, keine ganz richtig.
      → Stolperfallen 29–31.
    - **Auswertung (Endstand): AUC 0.947** — die Score-Rangfolge ist also **gut**, „Modell
      unbrauchbar" war die falsche Diagnose. ROC-Sprung bei FPR ≈ 0.06 von TPR 0.25 auf **0.94**;
      **Knie ≈ (0.06, 0.94)**, Schwelle grob 2–2.5 (exakter Wert per `argmin` noch nachzutragen).
      Vergleich der Betriebspunkte: Schwelle 0.85 → TPR 1.00 / FPR 0.25 / ~2500 Fehlalarme;
      Knie → TPR 0.94 / FPR 0.06 / ~600; Schwelle 4.26 → TPR 0.25 / FPR 0.01 / ~100.
    - **Boxplot als Schlüssel zum Befund:** Normal-Box Median ~0.4, Whisker bis 1.65, darüber
      aber eine **dichte Wolke normaler Punkte bis 5.1** (schwerer oberer Schwanz). Outlier-Box
      Median 2.85 (Box ~2.45–3.4), Gruppe bei 4.9–5.4, zwei Nachzügler bei ~1.0/1.25. Die
      Ausreißer liegen damit in einem **mittleren Band**, durch das der Normal-Schwanz
      hindurchreicht → die obersten 1 % der Scores sind **überwiegend Normaldaten**. Genau
      deshalb versagt 4.26 (→ Merksatz).
    - **Vorlagen nachgezogen (25.7.):** Blatt ⑤ RandNet-Block geschärft (3 Diversitätsquellen
      statt „Verbindungen der Neuronen"; ≈ 37 % gekappt / 63 % überleben; eigene Zeile
      Maske ≠ Dropout). Blatt ⑥ um neuen Abschnitt **„Schwellwert wählen"** ergänzt (Schwellwert
      vs. Anteil, drei Wege je nach Vorwissen, Gegenprobe über die Alarmzahl, Schulter vs.
      Senkrechte, Knie = oberes Ende, Quantil-Fallstrick, Diagnoseregel AUC vs. TPR).
  - **Blatt `Session06_Autoencoder_VAE` gelöst und korrigiert ✅ (26.7.)** — bearbeitet wurde ein
    **alter Ausdruck mit VAE-Teil**; MC 1.2 und Aufg. 5 (VAE) bewusst leer gelassen, das ist nach
    der Klammer-Regel richtig. Ergebnis: MC 1.1/1.3 richtig, **1.4 Kreuz richtig, Begründung
    falsch** („Ensemble-Score = Mittelwert" statt **Median** → Stolperfalle 36; in Aufg. 4c
    dagegen richtig hingeschrieben, also Selbstwiderspruch auf demselben Blatt). Aufg. 2 Encoder
    komplett richtig, Decoder mit drei Fehlern (aufweitende `Dense(H·W·C)` fehlt, `Reshape()`
    ohne Ziel-Shape, `padding='same'` bei beiden `Conv2DTranspose` fehlt; Ausgabe als
    nachgestellte `Dense(3)` statt als letzte Transponierte mit 3 Filtern) → Wiederholung von
    Stolperfalle 27. **Aufg. 2a unbeantwortet** (x = y = train_data, weil das Ziel die Eingabe
    selbst ist ⇒ unüberwacht), 2b richtig ohne Schwellwert-Schluss. Aufg. 3a Kern richtig
    (Bottleneck), 3b nur **ein** Grund von zweien (Weight Sharing fehlt), 3c richtig.
    Aufg. 4a alle drei Diversitätsquellen richtig (Rückfall aus Praktikum 07 behoben),
    4b zu knapp, **4c vollständig richtig** — beste Antwort des Blattes.
    - Für die Blätter mitzunehmen (Vorlagen noch nicht angefasst): BatchNorm-Zeile,
      σ'(z)_max = 0,25, Richtung der Unstable Gradients, Shape-Dreizeiler (same / valid −(k−1) /
      Pool abrunden vs. strides=2 aufrunden), Dense = Produkt ⇒ höchste Overfitting-Gefahr,
      Decoder-Block `Dense(H·W·C)` → `Reshape` → `Conv2DTranspose(..., padding='same')` mit
      Kanalzahl + Sigmoid am Ende, Ensemble-Score = Median.
  - **Blatt ⑤ handschriftlich übertragen bis einschließlich GAN-Teil ✅ (27.7.)** — offen bleiben
    nur noch die beiden letzten Abschnitte **AnoGAN (Folien 37–42)** und **f-AnoGAN (Folien 43–49)**,
    also genau der Aufgabentyp-9-Kern. Vorgezogen aus dem Slot Di 28.7. (S7 Teil 2); dort jetzt nur
    noch der Rest zu schreiben. Der neue
    ⑥-Abschnitt „Schwellwert wählen" ist ein kurzer Nachtrag auf ein bereits übertragenes Blatt
    → passt in den Slot **Mi 29.7. nachm. („Blätter ①–⑦ finalisieren")**.
- **S8 (28.7.)** 🟡 **Praktikum 09 (SVM/OCSVM) komplett durchgearbeitet und abgeschlossen** —
  synthetisches Zwei-Klassen-Beispiel (C-Reihe, RBF, ν-SVM), OCSVM linear/RBF, Brustkrebs-
  Datensatz mit unüberwachter (δ_min/δ_max-Heuristik) vs. überwachter (Grid Search, balanced
  accuracy) Metaparameterschätzung. Alle vier Frageblöcke beantwortet und korrigiert.
  - Vorab geklärt: **Margin** (Streifen zwischen h₁/h₂, ±1 ist nur Normierung ⇒ Breite 2/‖w‖)
    und **Nebenbedingung** (kein Punkt zwischen h₁/h₂; sie fesselt die Ebene an die Daten, sonst
    wäre w = 0 die Lösung — gleiches Muster wie die triviale Lösung bei Deep SVDD). Ebenso
    geklärt, warum w aus der Rechnung fällt (∂L/∂w = 0 einsetzen) und dass w im transformierten
    Raum unendlich viele Komponenten hätte. Herleitung selbst bleibt **nicht klausurrelevant**.
  - **Ergebnis Brustkrebs:** unüberwacht acc_norm 0.72 / acc_anom 0.99 (bal. acc 0.855),
    überwacht 0.99 / 0.92 (bal. acc 0.955). Kernbotschaft: der Unterschied ist **mehr Information
    (gelabelte Anomalien)**, nicht der bessere Algorithmus.
  - **Grid-Search-Plot gelesen:** γ dominiert vollständig, ν fast wirkungslos; **ab γ ≥ 0,6 exakt
    0,5 = Raten** (Glocke so schmal, dass jeder Punkt nur sich selbst erkennt ⇒ alles wird Anomalie);
    Optimum am **linken Rand** des Rasters (γ = 0,01) ⇒ `np.logspace(-2, 2, 10)` müsste nach unten
    verlängert werden. `gamma='scale'` ≈ 0,867.
  - Stolperfallen 37–41 ergänzt. **Wiederkehrendes Muster erneut, dreimal in einem Block:
    Teilfragen unbeantwortet gelassen** (γ-Frage leer, „warum ist der Kernel-Trick für die OCSVM
    essentiell?" fehlt, „welche Seite normal/anomal" fehlt).
  - **Blatt-④-Vorlage nachgezogen (SVM-/OCSVM-Teil):** Margin + Nebenbedingung als Klartextsätze,
    Antwortmuster Typ 6b inkl. **„C zu klein ⇒ Lage beliebig, viele Fehlklassifikationen"**
    (fehlte, wird in Original-Aufg. 6b ausdrücklich gefragt), Zeichenregeln Typ 7 (linearer Fall:
    Gerade vom Ursprung weg bis an die ursprungsnächsten Punkte; Normaldaten ursprungsfern),
    Antwortmuster Typ 7b (ν zu klein → Overfitting, ν zu groß → Underfitting), γ zu groß/zu klein,
    **Inselstrukturen als Stärke** (Argument der Musterlösung zu Original-Aufg. 8) und
    `gamma='scale'` = 1/(dim · var) nach Folie 22.
    ⚠️ `Alle_Blaetter.md` enthält noch den **alten** Blatt-④-Stand → beim Finalisieren Mi 29.7. nachziehen.
  - **Blatt-④-Vorlage (SVM-/OCSVM-Teil) ist vollständig und abschreibbereit** — alle Nachträge
    vom 28.7. sind eingearbeitet. **Handschriftlich übertragen steht noch aus**, wird in einem
    Zug vom fertigen Stand geschrieben.
  - **Blatt `Session08_SVM_OCSVM` gelöst und korrigiert ✅ (28.7.)** — damit ist **Typ 6/7 einmal
    komplett gerechnet**. Überwiegend richtig; stark waren Aufg. 3d (warum linearer Kernel bei der
    OCSVM unbrauchbar ist) und Aufg. 5a (Kernel-Trick beidseitig nachgerechnet, 25 = 5²).
    Zwei inhaltliche Korrekturen (→ Stolperfalle 42) und drei offen gebliebene Teilfragen:
    die **zwei Schranken** von ν (Aufg. 3b), die **Entscheidungsgrenze** statt nur der Glocke
    (4b), `sklearn.svm.OneClassSVM` als dritte Klasse (6c).
  - **Bewertungsmaßstab geklärt (Ansage Lena, 28.7.):** Der Prof wertet die **Begründung** mit —
    **richtig gedacht zählt**, auch wenn der Wortlaut von Folie/Musterlösung abweicht. Auch das
    Widerlegen der falschen MC-Alternativen ist eine gültige Begründung. Gilt ab sofort für alle
    Korrekturen.
  - **Offen aus S8:** Blatt ④ SVM-/OCSVM-Teil **handschriftlich übertragen**.

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

15. **überwacht ↔ unüberwacht mehrfach vertauscht (23.7., Praktikum 04).** Wiederkehrendes
    Fehlerbild in den Antworten: „Anomalien in den Validierungsdaten" = **überwacht** (nicht
    unüberwacht); Metaparameterwerte in Q1 getauscht (überw. bw=2 / unüberw. bw=0.5 hingeschrieben
    als 0.5/2). Merkanker: **Labels/Anomalien vorhanden ⇒ überwacht.** Vor dem Hinschreiben den
    zugehörigen Grid-Search-Aufruf gegenchecken (welches Intervall gab welchen Wert).
16. **Precision ↔ Recall im medizinischen Kontext vertauscht (23.7.).** „Anomalien erkennen ist
    wichtiger" = **Recall/Sensitivität (TPR)**, nicht Precision. Precision = von den geflaggten,
    wie viele echt; Recall = von den echten Anomalien, wie viele gefangen. Im Krebs-Kontext wird
    **Recall** priorisiert. Nicht „Precision" schreiben, wenn Recall gemeint ist.
17. **Achsenbeschriftung im Notebook kann lügen (23.7.).** Bei der überwachten GMM/EE-Suche steht
    „Mean negative log-likelihoods", geplottet wird aber die **AUC** (Werte 0.9–0.97, `scoring`-
    Lambda mit `roc_auc_score`). Immer den Wertebereich + das `scoring`-Argument prüfen, nicht der
    Achsenbeschriftung glauben — sonst dreht man höher/niedriger=besser um.
18. **Metaparameter bei monoton fallendem Mittelwert (23.7., GMM unüberw.).** Wenn der Mittelwert
    monoton fällt **und** die Streuung monoton steigt (kein Plateau, kein innerer Peak), sprechen
    **beide** Kriterien für die **kleinste** Metaparameterzahl (hier n=1) — nicht in die Mitte
    (n=3) gehen. Nur bei einem echten **Plateau** nimmt man „kleinster Wert am Plateau" (das war
    der KDE-überwacht-Fall). Erst prüfen: Plateau oder monoton?

19. **„Warum entsteht X beim Logarithmieren?" ⇒ rechnen, nicht qualitativ beschreiben (24.7.,
    Blatt S4 Aufg. 3b).** Geantwortet wurde „kleine Werte bleiben klein, große werden umso größer" —
    das beschreibt Monotonie (und stimmt für log nicht einmal, log **staucht**). Verlangt war die
    Umformung von Folie 15: log der multivariaten PDF = −½·(x−μ)ᵀΣ⁻¹(x−μ) − c. Der Logarithmus hebt
    die e-Funktion auf, der Vorfaktor wird zur additiven, x-unabhängigen Konstanten c; übrig bleibt
    exakt der quadrierte Mahalanobis-Abstand. Folge: **log-Dichte und D_M sind bis auf Vorzeichen
    und Konstante dasselbe** → auf die Dichte schwellen = auf D_M schwellen.
20. **Ausschlussgrund muss zur gestellten Frage passen (24.7., Blatt S4 Aufg. 5).** GMM für die
    Bananen-Verteilung mit „ist sehr langsam" abgelehnt — gefragt war nach der **Dichtebeschreibung**,
    nicht der Laufzeit. GMM mit mehreren Komponenten passt sich dem Bogen durchaus an (bedingt
    geeignet; Komponentenzahl muss gesucht werden). Ebenso: EE scheitert am Bogen wegen der
    **Krümmung** (eine Ellipse deckt den leeren Bereich unter dem Bogen mit ab), nicht wegen
    „1-Klassen-Problem mit Kovarianzen". Zusatz: bei Verfahrenswahl-Aufgaben **jedes** abgefragte
    Verfahren pro Szenario beurteilen — KDE in Szenario 2 blieb unbeantwortet = verschenkter Punkt.
21. **Nicht auf mitgelieferten Aufgabentext verweisen (24.7., Blatt S4 Aufg. 6).** „E-/M-Schritt:
    s. o., steht doch gut beschrieben" — in der Klausur steht der Text nicht daneben. E-Schritt:
    Parameter festhalten, je Punkt die Wahrscheinlichkeit für jede der K Verteilungen berechnen
    (weiche Zuordnung). M-Schritt: Zuordnungen festhalten, μ/Σ/Gewicht per Maximum-Likelihood neu
    schätzen. Wechseln sich ab, Likelihood steigt monoton → Konvergenz, ggf. **lokales** Optimum.

22. **Ausgabeschicht mit ReLU statt Softmax (24.7., Praktikum 05).** Im CNN stand
    `Dense(10, activation='relu')`. ReLU liefert beliebige nichtnegative Werte, die sich nicht
    zu 1 summieren — keine Wahrscheinlichkeitsverteilung, passt nicht zu
    `categorical_crossentropy`; zusätzlich Gradient 0 für alle abgeschnittenen Neuronen.
    **Letzte Zeile jedes Netzes gegen die Aufgabenstellung gegenlesen** (Klassenzahl + Softmax
    bzw. Sigmoid bzw. keine bei Regression) — genau das ist Aufgabentyp 5.
23. **`fit` erneut ausführen = WEITERtrainieren (24.7.).** Bei der Learning-Rate-Frage wurde nur
    die `fit`-Zelle neu gestartet; das Netz behielt seine Gewichte, das Ergebnis sah aus, als
    lernte lr=1e-4 *schneller* als 1e-3. Plausibilitätsanker: **kleinere Learning Rate kann nie
    schneller lernen.** Vor jedem Vergleichslauf die Zelle mit `tf.keras.Sequential()` erneut
    ausführen (Hinweis steht im Notebook erst weiter unten, gilt überall).
24. **„Warum braucht jede Schicht eine Aktivierung?" ≠ Vanishing Gradient (24.7.).** Geantwortet
    wurde mit Unstable Gradients (Folien 31–34) — das beantwortet, **welche** Nichtlinearität man
    nimmt. Gefragt ist: ohne Aktivierung sind verkettete lineare Abbildungen wieder **eine**
    lineare Abbildung → Tiefe wertlos, nur linear trennbare Probleme lösbar. Siehe Blatt ②/③.

25. **AE klassifiziert nichts — „sigmoid = binäres Klassifikationsproblem" ist falsch (25.7.,
    Praktikum 06, in beiden Frageblöcken).** Der Autoencoder gibt immer nur einen
    **Rekonstruktionsfehler** aus; die Ja/Nein-Entscheidung macht erst ein **Schwellwert** darauf,
    nicht das Netz. Sigmoid am Ausgang steht dort, weil die Pixel auf **[0,1] normiert** sind und
    sigmoid den Ausgabebereich genau darauf begrenzt — **nichts mit Klassifikation**. Wörter wie
    „einstufen/klassifizieren" für den AE selbst sind ein Warnsignal.
26. **Ähnliche Anomalien sind SCHWER erkennbar, nicht leicht (25.7.).** Intuition oft umgekehrt:
    Anomalie-Fehler ist groß, **weil** die Ziffer der Normalklasse *unähnlich* ist. Je ähnlicher
    eine Anomalie den Normaldaten (7↔1 „1 mit Strich"), desto **kleiner** ihr Rekonstruktionsfehler
    → desto eher rutscht sie durch (erklärt FNR≈0.29). Gute Normalklasse = möglichst distinktiv.
27. **Convolutional-AE-Struktur: drei typische Fehler (25.7.).** (a) `Conv2DTranspose` braucht ein
    **4D-Bild** (H,W,C) — nie direkt nach `Flatten` auf einen platten Vektor (Crash); der Weg vom
    Code zurück ist **Dense → Reshape((H,W,C))**, erst dann transponierte Faltungen. (b) Der
    Bottleneck entsteht **erst flach machen, DANN `Dense(z)`** — `Dense` *vor* `Flatten` wirkt nur
    pro Pixel auf die Kanäle, ist kein Code. (c) Die **letzte `Conv2DTranspose` hat so viele Filter
    wie das Bild Kanäle** (MNIST: **1**, Farbe: 3), sonst passt das abschließende `Reshape` nicht
    (28×28×8 ≠ 784). Zusätzlich: `padding='same'` überall, sonst halbiert/verdoppelt sich die
    Kantenlänge nicht sauber zurück auf 28.
28. **Was verhindert die Identitätsabbildung? Der Bottleneck, nicht Encoder/Flatten (25.7.).**
    Die **niedrigere Dimension der Code-Schicht z** zwingt zur Kompression; wäre die Mitte ≥
    Eingabegröße, lernte der AE die Identität. Flatten/„der Encoder" sind falsche Antworten.

29. **RandNet als Dropout beschrieben — Rückfall am selben Tag (25.7., Praktikum 07 Frage 1).**
    Geantwortet wurde „zufällige **Neuronen**, die aus dem Netz rausgenommen werden" — das ist
    Dropout. RandNet kappt **Verbindungen** (Einträge der Gewichtsmatrix), **einmalig fest** in
    `build()`, für das ganze Training gleich. Dropout würfelt **pro Schritt neu**, trifft
    **Neuronen**, ist in der Inferenz aus. Warnsignal beim Schreiben: das Wort „Neuronen" bei
    RandNet. Zusatzfehler derselben Antwort: **nur eine von zwei Diversitätsquellen** genannt —
    es fehlte, dass jedes Netz auf einem **anderen zufälligen Zehntel** der Daten trainiert
    (`np.random.shuffle(rand_idx)` in der Trainingsschleife). Gleiches Muster wie Stolperfalle 20:
    nicht alles beantwortet, was die Frage hergibt.
30. **Schwellwert (Score) ↔ Anteil (Rate) verwechselt (25.7., mehrfach).** Ein Schwellwert ist
    ein **Score-Wert** (y-Achse des sortierten Plots), ein Ausreißeranteil ist ein **Anteil der
    Punkte** (x-Achse). Beide bezeichnen denselben Schnitt, sind aber **nicht derselbe Zahlenwert**
    („Schwelle 1 ⇒ Anteil 0.2, also Schwellwert 0.2?" — nein). Der **sortierte Score-Plot ist die
    Übersetzungstabelle** zwischen beiden. Prüfregel vor dem Festlegen: Schwelle → Indexposition
    ablesen → `n − Index` = Anzahl Alarme → ist der Anteil als Ausreißeranteil plausibel? 35 %
    geflaggt ist keine Outlier Detection. Verschärfung von Stolperfalle 5: `outlier_ratio` ist
    ein **Erzeugungs**parameter des Datensatzes — daran drehen tauscht die Aufgabe aus, nicht den
    Betriebspunkt.
31. **Untere statt obere Ecke des ROC-Sprungs als Knie gelesen (25.7., Praktikum 07 Frage 4).**
    Die Kurve hat bei FPR ≈ 0.06 ein fast **senkrechtes Stück** von (0.06, **0.25**) hinauf auf
    (0.06, **0.94**). Abgelesen wurde das **untere** Ende („Knie bei TPR = 0.27") — ein reales
    Merkmal der Kurve, aber der falsche Punkt. **Das Knie ist immer das obere Ende des Sprungs**,
    der Punkt mit kleinstem Abstand zu (0,1). Der Sprung selbst ist die Botschaft: gleiche FPR,
    aber 0.94 statt 0.25 TPR — gratis. Rechnen statt ablesen: `best = np.argmin(fpr**2 + (1-tpr)**2)`,
    dann `fpr[best]`, `tpr[best]`, `thr[best]`.
    Zwei Folgefehler in derselben Antwort: (a) „**demnach** Schwellwert 0.75" — der Wert 0.75/0.85
    war korrekt abgelesen (dort TPR = 1.0, **TNR = 0.75**), folgt aber **nicht** aus dem Knie; zwei
    verschiedene Punkte der Kurve als Ursache und Wirkung verkettet. (b) Notation: „0.75 % der
    Normaldaten" — 0.75 als Rate heißt **75 %**. (c) Der **Boxplot** wurde gar nicht erwähnt,
    obwohl die Frage ihn ausdrücklich verlangt.

32. **Batch Normalization fasst nie Gewichte an (26.7., Blatt S5 Aufg. 1.3).** Angekreuzt wurde
    „normalisiert die **Gewichte** der Schicht auf Mittelwert 0", und die Begründung verneinte
    ausgerechnet die richtige Aussage. Richtig: BN standardisiert die **Eingaben/Aktivierungen**
    einer Schicht über die **Batch-Dimension** und lernt zusätzlich **γ (Skalierung) und β (Shift)**
    mit. Warnsignal: das Wort „Gewichte" in einer BatchNorm-Antwort.
33. **Shapes Zeile für Zeile, nicht im Kopf durchziehen (26.7., Blatt S5 Aufg. 2).** 64/2 wurde als
    34 notiert, danach lief die ganze Kette verschoben (34/34/32/16 statt 32/32/30/15) — der
    Endwert 4096 stimmte trotzdem, weil sich der valid-Conv-Abzug und die ceil-Rundung zufällig
    kompensierten. **Ein richtiges Endergebnis beweist keine richtige Zwischenrechnung.**
    Die drei Regeln: `same`+strides=1 ⇒ Größe **bleibt**; `valid`, Kernel k ⇒ **minus (k−1)**;
    Halbieren ⇒ Pooling **abrunden**, Conv mit strides=2 **aufrunden** (ceil).
34. **Dense-Schichten sind die Overfitting-Gefahr, nicht ihr Gegenmittel (26.7., Blatt S5 Aufg. 3c).**
    Geantwortet wurde, die Gefahr werde dort „durchaus geringer". Richtig: Dense ist vollverknüpft,
    die Gewichtszahl ist das **Produkt** aus Eingangslänge und Neuronenzahl (4096·256 ≈ 1 Mio),
    Faltungen brauchen dank **Weight Sharing** nur k·k·C_in·C_out unabhängig von der Bildgröße.
    Viele Parameter ⇒ **hohe** Overfitting-Gefahr ⇒ Dropout/L2 sitzen genau dort.
35. 🔁 **NOCHMAL ANSCHAUEN (von Lena selbst markiert, 26.7.) — Vanishing Gradient ist eine
    Rechnung mit 0,25 (Blatt S5 Aufg. 6a/6b).** „σ'(z) kann
    höchstens 1 annehmen" ist falsch — das **Maximum von σ'(z) ist 0,25** (bei z = 0; die 1 gehört
    zu tanh). Backprop multipliziert **pro Schicht einen Faktor ≤ 0,25**, über L Schichten 0,25^L
    ⇒ die vorderen Schichten bekommen praktisch keinen Gradienten. „Überanpassung hinten" ist keine
    Begründung. Zu 6b: Beide Phänomene laufen Richtung **Eingangsschicht** (Backprop läuft von
    hinten nach vorn) — „explodiert zur Ausgangsschicht hin" ist die falsche Richtung.
36. **Ensemble-Score ist der MEDIAN, nicht der Mittelwert (26.7., Blatt S6 Aufg. 1.4).** Auf
    demselben Blatt in Aufg. 4c richtig hingeschrieben, in der MC-Begründung falsch. Der Median
    ist zugleich die **Begründung** für „Ensembles stabilisieren den Score" (robust gegen einzelne
    Ausreißer-Netze) — mit „Mittelwert" verschenkt man das eigene Argument. Ablauf komplett:
    quadratischer Fehler je Netz → auf **Standardabweichung 1** normieren → **Median** über alle Netze.

37. **Vokabular aus dem falschen Setting (28.7., Praktikum 09).** Bei der **überwachten
    Zwei-Klassen-SVM** (`SVC` mit Labels) wurde „RBF bildet einen Kreis um die **Normaldaten**"
    geschrieben — es gibt dort keine Normaldaten und keine Anomalien, nur Klasse 0 und Klasse 1.
    Richtig: die Grenze wird von der Geraden zu einer geschlossenen krummen Kurve **um die eine
    Klasse**. Gleiches Muster wie Stolperfalle 25 („AE klassifiziert"). Teuer, weil die Klausur
    genau zwischen SVM (zwei Klassen) und OCSVM (eine Klasse) unterscheidet.
38. **„Die Support Vektoren ändern sich bei RBF gar nicht" ist falsch (28.7.).** Je kleiner C,
    desto mehr Punkte dürfen die Bedingung verletzen — und **jeder Verletzer ist per Definition
    ein Support Vektor**, ebenso jeder Punkt **in** der Margin. Im Grenzfall C → 0 werden fast
    alle Punkte SV. Im Notebook-Plot nicht sichtbar, weil die Markierungskreise (`radius=0.008`)
    in der dichten Wolke verschwinden → **`len(est.support_)` bzw. `est.n_support_` ausgeben
    statt zählen.**
39. **„Erst Skalarprodukt, dann quadrieren" ist der POLYNOMIALE Kernel, nicht der RBF (28.7.).**
    Beim RBF setzt man den **Abstand** der beiden Punkte in die Gauß-Funktion ein.
    Allgemein gilt nur: k(a,b) liefert das Skalarprodukt der **transformierten** Punkte, ohne je
    zu transformieren. Beim RBF ist das nicht bloß billiger, sondern die **einzige** Möglichkeit
    (unendlich viele Komponenten).
40. **Achsenbeschriftung (ν, γ) — erste Zahl ist ν (28.7.).** Aus dem Grid-Search-Plot wurde
    „mit γ = 0,2 noch hohe Accuracy" abgelesen; 0,010–0,200 sind aber die **ν**-Werte, γ = 0,2154
    liefert nur ~0,565. Verschärfung von Stolperfalle 17: **vor dem Ablesen prüfen, welche Größe
    auf welcher Position des Tupels steht.**
41. **Keine Metrik behaupten, die gar nicht berechnet wurde (28.7.).** „…mit einer höheren AUC" —
    Zelle 21 gibt ausschließlich zwei Accuracies aus, AUC kommt im ganzen Vergleich nicht vor.
    Zusatzfehler in derselben Antwort: die δ_min/δ_max-Heuristik ist das **unüberwachte**
    Verfahren, also das **schlechtere** — „hat sich ausgezahlt" war der überwachten Grid Search
    zuzuschreiben (Rückfall in Stolperfalle 15).

42. **Zwei Korrekturen aus Blatt S8 (28.7.).** (a) **Die SVM hat eine eindeutige, globale Lösung** —
    das Optimierungsproblem ist konvex (Folien 20/30). „Je nach Initialisierung unterschiedliche
    Trennebenen" ist deshalb falsch; das ist der Unterschied zum neuronalen Netz. Merkhilfe: die
    Eigenschaft steht als **Stärke** auf Folie 30. (b) Die Seite eines neuen Punkts nicht schätzen,
    sondern über den **Abstand zum nächsten Punkt jeder Klasse** bestimmen — (2,5|2,5) liegt näher
    an ×(3|3) als an •(1,5|1,8), also Klasse +1, dabei **innerhalb** der Margin.
    Zusatz zu Stolperfalle 37: „die Ebene verschiebt sich vom **Ursprung** weg" gehört zur OCSVM;
    im Zwei-Klassen-Fall wandert sie zur **Masse der Punkte** hin.

## Gesicherte Merksätze (für die Blätter)

- **Parameterzahl einer Dense-Schicht = Ausgaben der Vorschicht × eigene Neuronen + Bias.**
  Eingang ist die **Aktivierung** der Vorschicht, nicht deren Gewichtszahl: 200er-Schicht nach
  200er-Schicht ⇒ 200·200 + 200 = 40 200, unabhängig davon, dass die Vorschicht selbst 157 000
  Gewichte hat. Deshalb wächst ein Netz durch weitere gleich große Schichten nur linear.
- **CNN schlägt FC mit WENIGER Gewichten (Folie 36).** Praktikum 05: erste Faltung 222 Parameter
  gegen 157 000 der ersten Dense-Schicht, trotzdem bessere Val-Accuracy. Gründe: lokale
  Verknüpfung, **Weight Sharing** (Filter gilt an jeder Bildposition), Erhalt der
  Nachbarschafts-/2D-Information, gelernte statt vorgegebener Filter (Sobel).
- **ReLU löst Vanishing, nicht Exploding Gradient.** Die Ableitung von max(0, z) ist exakt 1
  oder 0 — nie größer 1, egal wie groß z wird (unbegrenzt ist der **Ausgang**, nicht die
  Steigung). Steigung 1 heißt: das Produkt über viele Schichten schrumpft nicht gegen 0 (anders
  als Sigmoid mit max. 0,25). Explodieren kann der Gradient trotzdem, weil beim Backprop die
  **Gewichte** mitmultipliziert werden. He-Initialisierung = doppelte Varianz gegenüber Xavier,
  weil ReLU die Hälfte der Aktivierungen auf 0 setzt.
- **Dropout ist nur im Training aktiv** (wie Data Augmentation): Trainings-Loss kann dadurch
  **über** dem Validierungs-Loss liegen und die Trainings-Accuracy darunter — sieht falsch aus,
  ist korrekt, weil validiert wird ohne deaktivierte Neuronen. Lernfortschritt wird langsamer.

- **C und ν laufen gegenläufig: großes C ≈ kleines ν.** C ist ein Strafgewicht, ν eine
  **Mengenvorgabe** (untere Schranke für den SV-Anteil, obere Schranke für die Margin-Verletzer).
  Deshalb bei ν kein logarithmisches Raster — ν ∈ (0; 1], also linear suchen (`np.linspace`).
  Zu großes ν wirft `ValueError: specified nu is infeasible` (durch die Klassenverteilung begrenzt).
- **γ zu groß ⇒ balanced accuracy exakt 0,5 (Praktikum 09).** Die Glocke wird so schmal, dass jeder
  Trainingspunkt nur noch **sich selbst** erkennt — jeder Testpunkt fällt aus der Grenze, alles wird
  als Anomalie geflaggt, Raten. Das ist die **Overfitting-Signatur** von γ und tritt schon ab
  γ ≈ 0,6 auf; γ = 100 im Raster ist tote Zone.
- **Liegt das Optimum am RAND des Suchrasters, ist das Raster falsch — verlängern, nicht
  auswählen.** Gegenstück zum „Suchintervall anpassen"-Merksatz: dort wird der kaputte Rand
  **abgeschnitten**, hier muss das Intervall **erweitert** werden (γ-Optimum saß auf dem kleinsten
  Wert von `np.logspace(-2, 2, 10)`).
- **OCSVM mit RBF beschreibt auch mehrere getrennte Cluster als Inseln.** Genau das ist ihr
  Vorteil bei mehrmodalen Normaldaten und das Argument der Musterlösung zu Original-Aufg. 8 —
  Mahalanobis/Elliptic Envelope (eine Ellipse) deckt den leeren Bereich dazwischen mit ab.
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
- **Elliptic Envelope: `contamination` ist ein Schwellwert, kein Formparameter.** `score_samples`
  (neg. Mahalanobis-Abstand) hängt **nur vom Kovarianz-Fit** ab, `contamination` verschiebt nur
  `offset_` (die ±1-Grenze in `predict`). Folgen: (1) unüberwachte Grid-Search-Kurven **flach**
  → contamination unüberwacht **nicht** schätzbar; (2) **AUC invariant** gegen contamination
  (doppelt: AUC ist schwellwertfrei **und** die Scores ändern sich nicht). AUC = feste Modellgüte,
  contamination = Betriebspunkt auf der festen ROC-Kurve. Schätzbar nur **überwacht** (Accuracies/
  TPR/FPR mit Validierungs-Anomalien) oder per **bekanntem Ausreißeranteil**.
- **Novelty vs. Outlier Detection.** Novelty: Fit auf **sauberen Normaldaten**, Anomalien nie im
  Training. Outlier: `fit_predict` auf **gemischten, unlabelten** Daten (Anomalien **kontaminieren**
  den Fit), kein Split/Grid-Search, contamination = bekannter Anteil vorgegeben. Fit auf
  kontaminierten Daten ist schwerer → Anomalien ziehen die Kovarianz zu sich, TPR fällt (Praktikum
  04: 0.72 statt ~0.93–0.97 bei Novelty). Wählt man bei unlabeltem Batch ohne sauberen Normalsatz,
  v. a. zum **Datenbereinigen**; setzt einen grob bekannten Ausreißeranteil voraus (real meist nicht
  exakt bekannt → empfindlich).
- **In Novelty-Setups meint `contamination` Normaldaten am Rand**, die als Anomalien abgeschnitten
  werden (Fit ist rein normal) — entspricht der Trainings-FPR / Grenztightness. Nur bei echter
  Outlier Detection (gemischte Daten) meint es reale Ausreißer.
- **Unüberwachte Metaparameteroptimierung braucht keine Labels — warum sie ohne `scoring`
  läuft.** Gibt man bei `GridSearchCV` kein `scoring` an und übergibt kein `y`, wird die
  eingebaute `.score()`-Methode des Estimators benutzt. Bei **KDE und GMM** ist das die
  **mittlere Log-Likelihood** (wie gut passt die Dichte zu den Normaldaten) → label-frei,
  genau deshalb „unüberwacht". **Ausnahme EllipticEnvelope:** dessen `.score()` erwartet
  Labels → man muss ein eigenes, label-freies `scoring=lambda est, X: np.sum(est.score_samples(X))`
  liefern, sonst crasht die unüberwachte Suche.
- **Mittelwert-/Streuungs-Plot lesen (Bandbreite/Komponenten wählen).** Ziel: **hoher
  Mittelwert bei kleiner Streuung**. Der Abschnitt mit **großer Streuung ist die Overfitting-
  Ecke, kein Ziel** — ein hoher Mittelwert dort ist unzuverlässig (spitze Dichte, in jedem
  Fold anders). Bei KDE fällt der Mittelwert oft **monoton** (kein innerer Peak, links am
  höchsten aber dort auch maximale Streuung). Dann gilt: **kleinste Bandbreite nehmen, bei der
  die Streuungskurve schon abgeknickt/flach ist** (Elbow, z. B. ~0.4–0.5) — kleiner = mehr
  Mittelwert, weiter rechts kauft nur noch Mittelwert-Verlust ohne Stabilitätsgewinn.
  Klausur-Begründung zählt mehr als die Zahl: „Mittelwert monoton, links unbrauchbar wegen
  Streuung → Elbow der Streuungskurve bei möglichst hohem Mittelwert."
- **KDE-Normalisierung 1/(Nh) sichert die Dichteeigenschaft (Fläche = 1).** Der Gauß-Kernel hat
  Fläche 1; gestreckt auf k((x−tᵢ)/h) hat er Fläche h; N Stück aufsummiert ergeben Fläche N·h;
  Teilen durch N·h bringt sie zurück auf 1. Nicht „damit die Kernel zusammengefasst werden".
  Bandbreite h = **kontrolliert den Einfluss der Nachbarschaft**.
- **contamination ist ein ANTEIL, keine Anzahl** (Folie 17) — und ein **Schwellwert, kein
  Formparameter**: der Kovarianz-Fit bleibt gleich, nur `offset_` verschiebt sich. Ersetzt die
  starre 3σ-Grenze durch eine aus den Daten angepasste.
- **„Suchintervall anpassen" ist Darstellungs-, kein Auswahlgrund.** Die Extremwerte am Rand
  (sehr negativer Score, riesige Streuung) **stauchen die Skala**, sodass man im interessanten
  Bereich nichts unterscheidet. Also den kaputten Rand **abschneiden** und um den Elbow zoomen
  (`np.linspace(0.2, 0.8, 100)`), **nicht** in die Streuungs-Ecke hineinzoomen.
- **Autoencoder-Grundgerüst (Blatt ⑤).** Encoder verjüngt → **Code z = Latent Space = Bottleneck**
  in der Mitte (muss **niedrigere Dimension** als Eingabe haben, sonst wird die Identität gelernt).
  Decoder = gespiegelter Encoder. **Anomalie-Score = Rekonstruktionsfehler** (auf Normaldaten
  trainiert, Anomalien werden schlecht rekonstruiert). Aktivierungen: **ReLU in versteckten
  Schichten** (Nichtlinearität, sonst = lineare Abbildung ≈ PCA), **sigmoid am Ausgang** (Bilder
  auf [0,1] normiert). Conv-AE: Encoder `Conv2D strides=2` → `Flatten` → `Dense z`; Decoder
  `Dense` → `Reshape((H,W,C))` → `Conv2DTranspose strides=2, padding='same'`, letzte Transponierte
  mit **1 Filter** (= Bildkanäle).
- **End-to-End vs. AE-als-Initialisierungsschritt (Folien 154–165).** *End-to-End* (heute Standard,
  dank Xavier/He-Init): ganzes Netz auf einmal auf das Ziel trainieren. *AE-als-Init* (historisch,
  „heute selten"): jede Schicht **schichtweise als Autoencoder vortrainieren** → gute Startgewichte
  → *danach* end-to-end feinabstimmen. Nicht verwechseln mit **Feature-Descriptor** (Encoder liefert
  Merkmale für einen separaten klassischen Klassifikator, z. B. OCSVM — hilft bei **zu wenig Daten**).
- **Label-Remapping mit Sentinel (255-Trick, Praktikum 06).** Um Klassenlabels 0–9 auf binär
  (normal→0, Anomalie→1) umzuschreiben, ohne **Wert-Kollisionen** (0/1 sind selbst gültige Labels):
  erst Anomalien auf einen **Zwischenwert außerhalb des Bereichs** (255) setzen, dann Normale→0,
  dann 255→1. Direkt auf 1 zu setzen bricht, sobald `normal_label` selbst 1 wäre.
- **Ein Schwellwert aus dem bekannten Ausreißeranteil garantiert die richtige ANZAHL an Alarmen,
  aber nicht die richtigen PUNKTE.** Er ist ein Quantil der Score-Verteilung und unterstellt
  stillschweigend, die Ausreißer seien die **höchsten** Scores. Praktikum 07 zeigt den Gegenfall:
  Schwelle 4.26 flaggt exakt 1 % der Daten, fängt davon aber nur ein Viertel der Ausreißer
  (TPR 0.25) — **bei AUC 0.947**. Die Rangfolge war also gut, die Annahme war falsch.
- **Warum ein Quantil-Schwellwert bei guter AUC trotzdem scheitert: schwerer Oberschwanz der
  Normaldaten.** Liegen die Ausreißer in einem **mittleren Band** (klar über der Masse der
  Normaldaten), reicht ein langer Normal-Schwanz **durch dieses Band hindurch und darüber
  hinaus** — dann bestehen die obersten Prozent der Scores überwiegend aus **Normaldaten**, und
  das Quantil schneidet **oberhalb** des Anomalie-Hauptfelds ab. Erkennbar im **Boxplot**: dichte
  Ausreißerpunkte der Normal-Box, die bis über den Median der Outlier-Box hinausgehen.
  Konsequenz: **Diagnose immer über AUC + Boxplot, nicht über die TPR eines einzelnen
  Betriebspunkts.** Hohe AUC + schlechte TPR = falsche **Schwelle**; niedrige AUC = schlechtes
  **Modell**.
- **Das Knie ist das OBERE Ende eines senkrechten ROC-Stücks.** Ein senkrechter Sprung heißt:
  bei **gleicher FPR** springt die TPR (Praktikum 07: bei FPR 0.06 von 0.25 auf 0.94). Der Gewinn
  ist gratis, also nimmt man immer den oberen Punkt — formal den mit kleinstem Abstand zu (0,1).
  Danach prüfen, was der letzte Rest TPR kostet: von (0.06, 0.94) auf (0.25, 1.00) kauft man die
  letzten 6 % Ausreißer mit **~1900 zusätzlichen Fehlalarmen**.
- **Sortierten Score-Plot lesen: Schulter ≠ Knie.** Eine **Schulter** (Kurve flacht ab und steigt
  danach weiter) ist meist eine **zweite Normalgruppe** — bei KDD-Cup z. B. seltener, aber
  harmloser Verkehr, den der AE schlecht rekonstruiert. Erst wo die Kurve in die **Senkrechte**
  geht, beginnen die Ausreißer. Das **Histogramm** taugt dafür nicht: die interessante Region ist
  genau die, in der die Balken schon fast auf 0 liegen (100 Ausreißer bei y-Achse bis 5600 =
  unsichtbar). Es zeigt nur „die Masse ist normal", nicht wo die Masse **aufhört**.
- **Diversität im Autoencoder-Ensemble (RandNet, Folien/Praktikum 07): zwei Quellen.** (1) Jede
  Schicht jedes Netzes bekommt eine **eigene zufällige Verbindungsmaske** ⇒ jedes Netz hat eine
  andere Architektur. (2) Jedes Netz trainiert auf einer **anderen zufälligen Teilmenge** (je 10 %
  der Daten, Bagging). Dazu schwächer die zufällige Gewichtsinitialisierung. Score = **Median** der
  auf Standardabweichung 1 normierten Rekonstruktionsfehler über alle Netze (Median, weil robust
  gegen einzelne Ausreißer-Netze — das ist die „Stabilisierung des Scores").
- **RandNet-Schicht, wie sie realisiert ist.** Kindklasse von `Dense`. In `build()` werden **mit
  Zurücklegen** so viele Verbindungsindizes gezogen, wie es Verbindungen gibt; die **Duplikate**
  sorgen dafür, dass ein Teil **nie gezogen** wird (≈ 37 % gekappt, ≈ 63 % überleben — das ist
  1/e). Ergebnis ist eine **binäre Maske** in Form der Gewichtsmatrix. In `call()` wird
  `kernel = kernel * kernel_mask` gesetzt, die gekappten Gewichte also bei jedem Aufruf auf **0**
  gezwungen — sie werden nicht gelöscht, sondern am Wiederbeleben gehindert.
- **Warum Outlier Detection schlechter läuft als Novelty Detection — am Score sichtbar.** Im
  Outlier-Setup **kontaminieren** die Ausreißer den Fit: das Ensemble lernt sie mit und
  rekonstruiert sie zu gut ⇒ kleiner Fehler ⇒ niedriger Score ⇒ TPR bricht ein (Praktikum 07:
  0.25). Novelty-Variante desselben Verfahrens: Teilmengen nur aus **sauberen Normaldaten** ziehen,
  Scoring identisch. Zusatzgewinn: der Schwellwert lässt sich dann **bestimmen** statt raten —
  über ein Quantil der Normaldaten-Scores auf einem Validierungssatz (95. Perzentil = 5 %
  Trainings-FPR) oder überwacht per ROC.

## Änderungslog

- **2026-07-27 (Nachtrag 4): Blatt ⑤ abgeschrieben bis auf AnoGAN und f-AnoGAN.** Übertragen sind
  AE/CAE-Teil, Curse of Dimensionality, RandNet, GAN-Grundlagen und das G-/D-Gerüst; offen bleiben
  die Abschnitte „AnoGAN (Folien 37–42)" und „f-AnoGAN (Folien 43–49)" — beides Aufgabentyp 9.
  Damit ist Blatt ⑤ das einzige noch unvollständige Blatt. Rest → Di 28.7. (S7 Teil 2), davor
  nichts an diesen beiden Abschnitten der Vorlage ändern.
  ⚠️ Beim Weiterschreiben gilt die Formel-Diät (Nachtrag): f-AnoGAN-Score **ohne** MSE-Terme,
  L_res/L_disc als Abstände benannt statt als Formeln. Für den schon geschriebenen Teil prüfen,
  ob Curse-of-Dim.-Quotient und AE-Loss-Summe noch draufstehen → ggf. auf die Streichliste
  (Slot Mi 29.7. nachm.).

- **2026-07-27 (Nachtrag 3): Musterlösung zu Aufg. 9 ist an zwei Stellen fehlerhaft — Blatt ⑤
  bleibt wie es ist.** Der Lösungsteil (uebungen.pdf S. 44/45) zeigt `Dense(units=8*8*64)` **ohne**
  BN/ReLU und eine D-Ausgabe `Dense(1)` **ohne** Aktivierung, obwohl die Aufgabenstellung „vor jeder
  Aktivierung BN", „immer ReLU" und „Aktivierung ergibt sich aus der Klassifikationsaufgabe"
  verlangt. Zwischendurch war das Blatt darauf umgestellt worden; **auf Lenas Ansage (Fehler in der
  ML, ML neu geladen) wieder zurückgedreht** — es gilt weiter: Dense in G mit `use_bias=False` +
  BN + ReLU, D-Ausgabe mit sigmoid **plus** dem `from_logits`-Halbsatz. Praktikum 08 stützt das
  beim Dense (BN + LeakyReLU); nur bei der D-Ausgabe schreibt auch das Praktikum `Dense(1)` roh —
  deshalb bleibt der Halbsatz auf dem Blatt stehen, er deckt beide Varianten ab.
  ⚠️ Die neu geladene `uebungen.pdf` (27.7., 19:40) enthält an diesen beiden Stellen **denselben
  Text** wie vorher — falls die Korrektur woanders eingespielt wurde, nochmal gegenlesen.

- **2026-07-27 (Nachtrag): Formel-Diät auf den Blättern.** Leitregel neu: Was zu **keinem der 12
  Aufgabentypen** gehört, steht in der Open-Book-Klausur im Skript und kostet auf dem Blatt nur
  Suchzeit. Gestrichen in den **Vorlagen** von Blatt ④ (SVM-Optimierungsproblem + Nebenbedingung,
  duale Klassifikationsformel, Soft-Margin-Loss, Kernel-Definitionen, SVDD-Minimierung,
  Deep-SVDD-Zielfunktion, Triplet-Center-Loss, GOAD-Gesamtloss, CutPaste-Gaußdichte,
  Cosinus-Ähnlichkeit) und Blatt ⑤ (Curse-of-Dim.-Quotient, AE-Loss-Summe, L_res/L_disc als
  Formeln → als Abstände benannt, f-AnoGAN-MSE-Terme). Inhalt bleibt jeweils als Klartextsatz
  stehen. **Blätter, die schon abgeschrieben sind (①, ②/③, ⑥, Probabilistisch, Kap. 4), werden
  NICHT neu geschrieben** — dafür steht eine **Streichliste** im Lernplan (Slot Mi 29.7. nachm.):
  nur durchstreichen, Vorlagen bleiben unverändert, damit sie dem Blatt weiter entsprechen.
  `Alle_Blaetter.md` neu erzeugt (war noch auf dem Stand vor der ⑤-Prüfrunde vom 27.7.).

- **2026-07-27:** **Blatt ⑤ zweite Prüfrunde** — diesmal nicht nur gegen Foliensatz 07, sondern
  zusätzlich gegen **Original-Aufgabe 9** (Übungssammlung S. 16–20) und **Praktikum 08**. Zahlen
  und Folienangaben erneut alle bestätigt; fünf Stellen im G-/D-Teil geändert:
  1. **BN-Zählregel war falsch verallgemeinert.** „n Faltungen ⇒ (n−1)× BN" gilt nur für G (Ausgabe
     = letzte `Conv2DTranspose`). In D ist die Ausgabeschicht die `Dense(1)`, dort bekommen **alle**
     Faltungen BN — so stand es im D-Gerüst der Vorlage, die Regel daneben widersprach dem eigenen
     Code. Neue Formulierung: **kein BN nur in der Ausgabeschicht des Netzes**, und die ist in G und
     D eine andere Schichtart.
  2. **D-Ausgabe jetzt `Dense(units=1, activation='sigmoid')`** statt „KEINE Aktivierung". Aufg. 9b
     sagt „die Aktivierung ergibt sich aus der Klassifikationsaufgabe" ⇒ sigmoid; ohne Aktivierung
     ist nur richtig, wenn der Loss `from_logits=True` benutzt (Folie 30). Auf dem Blatt steht jetzt
     beides — sigmoid **plus** Halbsatz —, damit die Antwort in jeder Aufgabenvariante trägt.
  3. **`Dense` in G bekommt BN + ReLU** (`use_bias=False` → BN → ReLU → `Reshape`). Die alte Zeile
     „nach dem Dense kein BN, keine Aktivierung" stand gegen Aufg. 9a („**immer** ReLU", Ausnahme
     nur die Ausgabeschicht) **und** gegen Paulus' eigenen Code in Praktikum 08.
  4. **Trainingsende (Folie 28) ergänzt** — für Aufg. 9c: D-Kosten dauerhaft hoch + G-Kosten
     niedrig, aber **mehrdeutig**, weil dasselbe Bild entsteht, wenn G schneller gelernt hat
     ⇒ generierte Daten ansehen.
  5. **AnoGAN-Motivation (Folie 37) ergänzt** — für Aufg. 9d: ein GAN kennt nur z → Sample, **kein
     inverses Mapping**, deshalb muss z gesucht werden; die Restkosten sind der Score.
  Zusätzlich geprüft und ausdrücklich als **kein Fehler** auf dem Blatt vermerkt: die **fallenden**
  Filterzahlen im f-AnoGAN-Encoder (64, 32) — Gs Filterzahlen ohne Ausgabeschicht werden in **Gs
  Reihenfolge** übernommen, genau wie in Praktikum 08 (G: 32, 16 ⇒ E: 32, 16). Ebenso richtig:
  0,2·x bei Leaky ReLU (Folie 36 druckt nur „0,2").

- **2026-07-26 (Nachtrag 3):** **Blatt ⑤ vollständig gegen Foliensatz 07 (S. 2–49) geprüft** —
  jede Zahl nachgeschlagen, kein inhaltlicher Fehler gefunden (RandNet-Kennzahlen, DCGAN-Liste,
  λ = 0,1, `layers[-2]`, 500 Iterationen, MSE-Losses, RMSprop stimmen alle). Zwei echte **Lücken**
  geschlossen: (1) **G-/D-Keras-Gerüst nach Folie 29** — fehlte komplett, obwohl Aufgabentyp 9
  „Generator-/Discriminator-Code" verlangt (inkl. der Klarstellung, dass „keine FC-Layers" nur
  *dazwischen* gilt: Dense am Eingang von G und die Dense(1) ohne Aktivierung am Ausgang von D
  bleiben); (2) **Vorteile der GANs (Folie 34)** — auf dem Blatt standen nur die Nachteile.
  Kleinkram: Überschrift „Drei Fallen" bei vier Punkten, `feature_model.trainable = False`
  ergänzt, f-AnoGAN-Snippet benutzte ein undefiniertes `encoder_model_output` (jetzt wie Folie 47
  mit `autoencoder_input` → `z = encoder_model(...)`), Κ-Gewichtung als Folien-vs-Code-Differenz
  vermerkt. Blatt ist damit **abschreibbereit**, Umfang ~3 statt 2,5 Seiten.

- **2026-07-26 (Nachtrag 2):** Blätter `Session05_NeuronaleNetze` und `Session06_Autoencoder_VAE`
  gelöst und korrigiert. S5: 4 harte Fehler (BatchNorm-Kreuz, Shape-Kette, Dense/Overfitting
  invertiert, N_out = 1 statt 2) bei sonst solidem Bild — Aufgabentyp 5 (Architekturfehler) sitzt
  komplett. S6: stärkeres Blatt, Fehler nur im CAE-Code (Decoder) und in der 1.4-Begründung;
  RandNet-Fragen fast vollständig richtig, damit ist der Rückfall aus Praktikum 07 behoben.
  Stolperfallen 32–36 ergänzt. **Blatt ⑤ direkt nachgezogen** (CAE-Keras-Gerüst mit
  Shape-Kommentaren, die drei Decoder-Fallen, `fit(x=y=train_data)`-Begründung, Score-Ablauf mit
  Schwellwert, zweiter Grund CAE-vs-Dense = Weight Sharing) — muss beim Übertragen am Mo 27.7.
  mitgeschrieben werden. **Für Blatt ②/③ noch offen** (Slot Mi 29.7.): BatchNorm-Zeile,
  σ'(z)_max = 0,25 + Laufrichtung der Unstable Gradients, Shape-Dreizeiler, Dense = höchste
  Overfitting-Gefahr. Aufg. 6a/6b von Lena als **nochmal-anschauen** markiert. nachm.

- **2026-07-26:** Blatt ① handschriftlich übertragen ✅ — letzter offener Punkt aus S2 erledigt.
  Vorlage `Blatt_1_Verfahrensuebersicht.md` um die vier S2-Befunde ergänzt (Min-Max-vs-z-Kontrast,
  iForest-Grenzfälle, contamination-Definition, sklearn-Dreizeiler); diese ~10 Zeilen fehlen noch
  auf dem handgeschriebenen Blatt.

- **2026-07-26 (Planänderung):** **ED wird doch geschrieben** (Mo 27.7., 8:30–10:00) — der
  MDT-Vormittag heute bleibt, aber **Mo 27.7. vormittags entfällt** (3 h weg). Umbau im
  Lernplan: Mo 27.7. 14–16 = Kap. 07 S. 25–51 + Praktikum 08 **nur mitlesend**; Blatt ⑤ und
  Blatt `Session07_GANs` auf Di 28.7. 14–16; S5-Reste auf Mi 29.7. 14–16; **Notebook 05
  Teil 3 (binäres CNN + `class_weight`) ersatzlos gestrichen**. Leitlinie beim Kürzen: erst
  fällt, was keinem der 12 Aufgabentypen entspricht.

- **2026-07-25 (Nachtrag):** Praktikum 07 (Extended Autoencoder / RandNet-Ensemble, KDD-Cup)
  bearbeitet — `np.float`-Versionsfehler behoben, Schwellwertwahl aus sortiertem Score-Plot und
  bekanntem Ausreißeranteil geübt (4.26 ⇒ TPR 0.25). Notebook-Fragen korrigiert: schwächster
  Frageblock bisher (1 falsch, 3 teilweise). Stolperfallen 29–31 (RandNet als Dropout beschrieben
  + nur eine Diversitätsquelle; Schwellwert ↔ Anteil verwechselt; untere statt obere Ecke des
  ROC-Sprungs als Knie) und Merksätze ergänzt (Quantil trifft Anzahl nicht Punkte; Schulter ≠
  Knie im sortierten Plot; zwei Diversitätsquellen; RandNet-Realisierung mit Zurücklegen;
  Kontamination erklärt schwache TPR).
  Nach Vorlage von ROC und Boxplot **korrigiert**: der ursprünglich notierte Vorwurf „Knie
  geraten" war **falsch** — die TPR 0.27 ist ein reales Merkmal der Kurve (unteres Ende des
  Sprungs bei FPR 0.06), ebenso die 0.75 (= TNR bei Schwelle ~0.85). Fehler ist die Wahl der
  falschen Ecke und das „demnach" zwischen zwei unverbundenen Ablesungen. Ebenso korrigiert:
  **AUC 0.947**, das Modell ist gut — nur die Quantil-Annahme ist falsch, weil der schwere
  Oberschwanz der Normaldaten die obersten Prozent besetzt (neuer Merksatz).

- **2026-07-25:** S6 — Praktikum 06 (Simple + Convolutional Autoencoder, MNIST) komplett
  durchgearbeitet, beide Netze aufgebaut und alle Notebook-Fragen korrigiert. Stolperfallen 25–28
  (AE klassifiziert nichts / sigmoid = [0,1] nicht Klassifikation; ähnliche Anomalien schwer
  erkennbar; Conv-AE-Struktur Conv2DTranspose/Bottleneck/Filterzahl; Bottleneck verhindert
  Identität) und Merksätze zum AE-Bottleneck, End-to-End-vs-Init und 255-Sentinel-Trick ergänzt.
  Blatt ⑤ (AE-Teil), Praktikum 07 und Blatt `Session06` noch offen aus S6.

- **2026-07-24:** Blatt `Session04_Probabilistisch` korrigiert (12 richtig / 4 teilweise / 1 falsch).
  Stolperfallen 19–21 (Logarithmier-Frage rechnen, Ausschlussgrund passend zur Frage + alle
  Teilverfahren beurteilen, E/M selbst formulieren) und Merksätze zu KDE-Normalisierung und
  contamination-Anteil ergänzt. Blatt `Session05_NeuronaleNetze` bewusst auf den Puffer 26.7.
  geschoben.

- **2026-07-24 (Nachtrag):** S5 begonnen (Praktikum 05 bis CNN-Teil), Rest bewusst auf den
  Puffer 26.7. geschoben. Stolperfallen 22–24 (ReLU statt Softmax am Ausgang, `fit` ohne
  Netz-Neuerzeugung, Aktivierungsfrage ≠ Vanishing Gradient) und Merksätze zu Dense-Parameterzahl,
  Weight Sharing und Dropout-nur-im-Training ergänzt. Vorlage `Blatt_2_3_Shapes_Keras.md` um
  MaxPool-vs-strides-Vergleich und die Nichtlinearitäts-Begründung erweitert.

- **2026-07-24 (Nachtrag 2):** Blätter ②/③ vollständig handschriftlich übertragen (inkl.
  Training Folien 22–23 und Fehlerfinder-Checkliste); nur noch **Korrekturlesen** offen (Puffer
  26.7.). Merksatz zur ReLU-Ableitung ergänzt (Ableitung nie > 1; ReLU löst Vanishing, nicht
  Exploding; He-Init als doppelte Xavier-Varianz).

- **2026-07-18:** Datei angelegt (S2). S1/S2-Stand eingetragen, Stolperfallen 1–6 aus
  Praktikum 02 + Blatt Session02.
- **2026-07-20:** S3 eingetragen (Kap. 5 + Praktikum 03 Teil 1), Stolperfallen 7–8.
- **2026-07-20 (Nachtrag):** Praktikum 03 Teil 2 (CIFAR) ergänzt, Stolperfallen 9–11,
  offene Blatt-⑥-Korrektur (K/`pos_label`) vermerkt.
- **2026-07-20 (Nachtrag 3):** Blatt `Session03_Evaluierung` korrigiert; Stolperfallen 11–13
  (Standard-CV vs. Novelty-CV, „kein Fehler" als Antwort, Leakage-Ursache benennen) und
  Merksätze zu Metrik-Ehrlichkeit und ROC-Schwellwert ergänzt. Die beiden offenen S3-Punkte
  (Blatt ⑥ K/`pos_label`, CIFAR-Codefehler) verworfen.
- **2026-07-23 (Nachtrag):** Praktikum 04 (probabilistische Verfahren) — unüberwachte
  Metaparameteroptimierung durchgesprochen: warum `GridSearchCV` bei KDE/GMM ohne `scoring`/`y`
  läuft (Default `.score` = mittlere Log-Likelihood), EllipticEnvelope-Sonderfall, Mittelwert-/
  Streuungs-Plot lesen (Elbow-Regel), „Suchintervall anpassen" = Darstellungsgrund. Vier
  Merksätze ergänzt.
- **2026-07-23 (Nachtrag 2):** Praktikum 04 abgeschlossen (KDE/GMM/Elliptic Envelope). Alle
  Notebook-Fragen korrigiert. Stolperfallen 15–18 (überw.↔unüberw. vertauscht, Precision↔Recall,
  Achsenbeschriftung lügt = AUC, monoton vs. Plateau bei Metaparameterwahl) und Merksätze zu
  EE-contamination-Invarianz, Novelty-vs-Outlier-Detection und contamination-Bedeutung im
  Novelty-Setup ergänzt.
- **2026-07-23:** Klammer-Regel geklärt (alles Eingeklammerte raus). Material bereinigt:
  VAE aus Blatt ⑤ + Übungsblatt 6, k-Means/PCA aus Blatt ①; `Blatt_Clustering_PCA.md` und
  Übungsblatt `Session09_Clustering_PCA` gelöscht; READMEs + `Alle_Blaetter.md` nachgezogen;
  Session01/06-PDFs neu kompiliert. S9 (Clustering/PCA) entfällt, S6 nur noch AE — siehe Lernplan.
- **2026-07-20 (Nachtrag 2):** Blatt ⑥ als übertragen markiert; Antwortkorrektur Praktikum 03
  Teil 2 und Merksätze zu Overfitting-Kriterium, Loss-Skala, Loss vs. Accuracy, L2 im
  angezeigten Loss und Data Augmentation ergänzt.
