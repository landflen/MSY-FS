# Lernplan MDT5/2 — Maschinelles Lernen zur Anomalieerkennung

**Prüfung: Fr 31.07.2026, 11:00–12:30 (90 min)**
**Hilfsmittel: Skript (ausgedruckt) + handgeschriebene Zusammenfassungen. Praktika dürfen NICHT mit!**

---

## Materialüberblick

| Kapitel | Umfang | Inhalt | Praktikum |
|---|---|---|---|
| 01 Einführung | 36 F. | KI/ML-Begriffe, Anomalie, Outlier vs. Novelty Detection | 01a/01b (Python/NumPy) |
| 02 Normalisierung | 6 F. | Min-Max, z-Score; wann essentiell (k-Means ja, iForest nein) | — |
| 03 NN überwacht | 56 F. | Perzeptron, Aktivierungen, CNN, Shapes, Training, Dropout | 05 deeplearning |
| 04 Abstandsbasiert | 15 F. | kNN-Abstand, Isolation Forest (03a mit LOF/Matrix Profiles = optional, nicht klausurrelevant) | 02 abstand |
| 05 Evaluierung | 28 F. | ROC/AUC, Precision/Recall, Train/Val/Test, Data Leakage | 03 evaluierung |
| 06 Probabilistisch | 27 F. | Mahalanobis, GMM, KDE | 04 probabilistische |
| 07 Rekonstruktionsbasiert | 51 F. | Autoencoder, VAE, GAN, AnoGAN, f-AnoGAN | 06 + 07 autoencoder, 08 gans |
| 07a Zusätzl. rekonstr. | 37 F. | k-Means, Silhouette, PCA | Zusatz: pca_clustering |
| 08 Klassifikationsbasiert | 64 F. | SVM, Kernel-Trick, OCSVM, Deep SVDD, GOAD | 09 svm, 10 deep_svdd, 11 goad |
| 08a Zusätzl. klassif. | 6 F. | Selbstüberwacht, Contrastive Learning | — |

**Übungssammlung (mit Lösungen)** = explizit „Beispiele für mögliche Prüfungsaufgaben“.
`uebungen_paulus.pdf` = identische Aufgaben **ohne** Lösungen.
→ ~~Beide bleiben bis zum 29.7. unangetastet~~ — **am 27.7. aufgehoben:** ab Di 28.7. nachm. wird
mit den Originalen gearbeitet, soweit der Stoff durch ist (Liste im Kasten „Originale für Di 28.7.").
Für die Generalprobe bleiben nur die Kapitel-08-Aufgaben frisch, der Rest wird mit generierten
Aufgaben aufgefüllt.

## Die 12 Aufgabentypen der Übungssammlung (Zielbild fürs Üben)

1. **MC mit Begründung** (alle Themen — Punkte nur mit richtiger Begründung!)
2. **CNN Ausgabe-Shapes** pro Schicht berechnen
3. **Keras-Code schreiben**: Autoencoder nach Textbeschreibung
4. **Data-Leakage finden**: sklearn-Code (Scaler/GridSearch vor/nach Split, Pipeline)
5. **Architekturfehler finden** (Reshape-Unsinn, zu viel Pooling …)
6. **SVM von Hand**: Support-Vektoren + Trenngerade zeichnen, Einfluss von C, Kernel-Trick
7. **OCSVM von Hand**: Einfluss von ν, warum Kernel-Trick nötig
8. **Verfahrenswahl** zu gegebenem Daten-Plot (geeignet/ungeeignet + Begründung)
9. **AnoGAN komplett**: Generator-/Discriminator-Code, Training beschreiben, Anomalie-Sc1ore, f-AnoGAN-Encoder
10. **Deep-SVDD-Code beurteilen**: Bias verboten, BatchNorm verboten, Zentrum ≠ 0, beschränkte Aktivierungen → triviale Lösung
11. **Clustering**: k-Means-Eignung, Ellbogen + Silhouette lesen, Ausreißer via k-Means
12. **Ausreißererkennung** zu Plot: 2 geeignete + 1 ungeeignetes Verfahren

→ Die Klausur ist **anwendungsorientiert**: Code schreiben/beurteilen, zeichnen, Verfahren begründet auswählen. Da das Skript daneben liegt, zählt Verständnis + Suchgeschwindigkeit, nicht Auswendigwissen.

## Arbeitsweise pro Session (fester Dreischritt)

1. **Praktikum durcharbeiten** (Notebook selbst ausführen/lösen, nicht nur lesen) + zugehörige Folien daneben
2. **Handschriftliche Zusammenfassung** schreiben — da die Praktika nicht mit dürfen, müssen Code-Muster (Keras-Syntax, Shape-Regeln, typische Pipelines) auf die Blätter!
3. **Üben mit generierten Aufgaben**: Für jede Session liegt ein fertiges Übungsblatt in `Uebungsblaetter/` (Session01–Session10, siehe README dort) — ausdrucken, auf dem Block lösen, Antworten an Claude zur Korrektur. Die Originale bleiben frisch für die Generalprobe

**Empfohlene Zusammenfassungsblätter:**
① Verfahrens-Übersichtstabelle (Verfahren × geeignet/ungeeignet × Metaparameter × Normalisierung nötig?)
② Shape-Rechenregeln (Conv2D, Pooling, Conv2DTranspose, Flatten)
③ Keras-Spickzettel (Sequential, Conv2D, BatchNorm-Position, Loss-Funktionen, compile/fit)
④ Deep-SVDD-Verbotsliste (kein Bias, keine BatchNorm, Zentrum ≠ 0, unbeschränkte Aktivierung)
⑤ AnoGAN/f-AnoGAN-Ablauf (Training, Score-Berechnung)
⑥ Evaluierung: ROC/AUC lesen, Leakage-Checkliste (fit_transform nur auf Train!)
⑦ sklearn-Pipelines der Praktika (welches Verfahren, welche Parameter, welcher Aufruf)

## Sessionplan (Stand 27.7. abends — 4 Tage bis zur Klausur)

### Erledigt (Details im Lern-Logbuch `CLAUDE.md`)

| Session | Termin | Stand |
|---|---|---|
| S1 | 8.7. | ✅ Kap. 1+2, Blatt 1 korrigiert |
| S2 | 18.7. | ✅ Kap. 3a/4 + Praktikum 02 + Blatt `Session02`; Blatt ① übertragen (26.7.) |
| S3 | 20.7. | ✅ Kap. 5 + Praktikum 03 (beide Teile) + Blatt `Session03`; Blatt ⑥ übertragen |
| S4 | 23./24.7. | ✅ Kap. 6 + Praktikum 04 + Blatt `Session04`; Blatt `Probabilistisch` übertragen |
| S5 | 24./26.7. | ✅ Kap. 3 + Praktikum 05 (Teile 1+2) + Blatt `Session05`; Blätter ②/③ übertragen — **offen: Korrekturlesen + 4 Nachträge** |
| S6 | 25./26.7. | ✅ Kap. 07 S. 1–24 + Praktika 06/07 + Blatt `Session06`; Blatt-⑤-Vorlage fertig, **Übertragen offen** |
| S9 | — | ⛔ entfällt (Klammer-Regel: Clustering/PCA nicht klausurrelevant) |
| S1-Nacharbeit | 22.7. geplant | ⚠️ **nicht im Logbuch dokumentiert** — Praktika 01a/01b + Blatt `Session01_Nacharbeit`. Kein eigener Aufgabentyp ⇒ **wird nicht nachgeholt**, sofern nicht doch erledigt |

**Damit sind 8 der 12 Aufgabentypen mindestens einmal ganz geübt.** Offen stehen nur noch
**Typ 6/7** (SVM/OCSVM von Hand), **Typ 9** (AnoGAN komplett) und **Typ 10** (Deep-SVDD-Code) —
alle drei haben unten einen festen Slot. Typ 11 (Clustering) ist per Klammer-Regel gestrichen.

### Restplan

| Termin | Praktikum | Stoff + Übung |
|---|---|---|
| **Mo 27.7., 14–16** (2 h) | 08 (GANs) | **S7 Teil 1, komprimiert** (nach der ED-Klausur 8:30–10:00). Kap. **07 S. 25–51** lesen (GAN, AnoGAN, f-AnoGAN) + Praktikum 08 **nur mitlesend** (Code nicht selbst tippen — bewusster Zeitschnitt für den verlorenen Vormittag). Kein Blatt heute. Nebenbei: läuft `mlAno08_gans.ipynb`? (entpackt ✅, Lauf noch nicht bestätigt) |
| **Di 28.7., 8:30–11:30** (3 h) | 09 (SVM) | **S8.** Kap. **08 S. 1–37**: SVM, Kernel-Trick, OCSVM/SVDD. Zeichenübungen + Blatt `Session08_SVM_OCSVM` (**Typ 6/7**). Blatt ④ **SVM-/OCSVM-Teil** übertragen |
| **Di 28.7., 14–16** (2 h) | — | **S7 Teil 2 — Originale statt generiertem Blatt** (Entscheidung 27.7., s. u.). (1) Blatt ⑤ **fertig** übertragen — nur noch AnoGAN + f-AnoGAN, der Rest steht seit 27.7. (Slot dadurch entlastet), (2) **Übungssammlung: alles bis einschließlich f-AnoGAN** — Reihenfolge und Liste siehe Kasten unten. Blatt `Session07_GANs` wird **nicht mehr gelöst** (durch Original-Aufg. 9 ersetzt). ⚠️ Deutlich mehr als 2 h — Überhang planmäßig auf Mi 29.7. nachm. |
| **Mi 29.7., 8:30–11:30** (3 h) | 10 + 11 (Deep SVDD, GOAD) | **S10.** Kap. **08 S. 38–64 + 08a**: Deep SVDD, GOAD, Selbstüberwacht. Blatt ④ **Deep-SVDD-/GOAD-Teil** (Verbotsliste!) + Blatt `Session10_DeepSVDD_GOAD` (**Typ 10**) |
| **Mi 29.7., 14–16** (2 h) | — | **Blätter final** (der Slot ist entlastet, weil Blatt `Session05` schon am 26.7. gelöst wurde): (1) Blätter ②/③ Korrektur lesen **+ 4 Nachträge**: BatchNorm-Zeile, σ'(z)_max = 0,25 + Laufrichtung der Unstable Gradients, Shape-Dreizeiler, „Dense = höchste Overfitting-Gefahr". (2) Blatt ⑥ Nachtrag „Schwellwert wählen". ~~(3) Blatt ⑤ Decoder-Fallen prüfen~~ (Vorlage am 26.7. gegen die Folien geprüft, Slot frei). (4) **Streichliste abarbeiten** (Kasten unten, 5 min mit dem Stift). (5) **Überhang der Originale vom Di** abarbeiten und korrigieren |
| **Do 30.7., 8:30–10:30** | — | **Generalprobe** unter Klausurbedingungen (90 min, nur Skript + handschriftliche Blätter!), danach korrigieren. Frisch geblieben sind **Aufg. 6, 7, 10, 11** + MC **1.2** — das ist keine volle 90-min-Klausur mehr (Folge der Vorziehung, s. Änderungslog). Auffüllen mit **neu generierten** Aufgaben zu Typ 2/3/4/5, damit die 90 min und der Zeitdruck echt sind |
| **Do 30.7., 14–16** | — | Lücken aus der Generalprobe schließen; schwächste Aufgabentypen mit neu generierten Varianten nachtrainieren |
| **Fr 31.7., 8:30–10:30** | — | Nur Blätter + markierte MC-Begründungen durchgehen. Kein neuer Stoff! **11:00 Klausur** 🎯 |

**Unantastbar:** Generalprobe Do vormittags und der Ruhetag Fr vormittags. Wenn etwas klemmt,
fällt zuerst Stoff ohne eigenen Aufgabentyp — nicht ein Übungsblatt.

### Streichliste für die bereits abgeschriebenen Blätter (Slot Mi 29.7. nachm.)

Entscheidung 27.7.: Formeln, die zu **keinem** der 12 Aufgabentypen gehören, stehen in der
Open-Book-Klausur ohnehin im Skript — auf dem Blatt kosten sie nur Suchzeit. In den **Vorlagen**
von Blatt ④ (noch nicht abgeschrieben) und ⑤ sind sie schon raus — bei ⑤ ist der AE-Teil aber
schon geschrieben, also beim Durchstreichen mitprüfen (Curse-of-Dim.-Quotient, AE-Loss-Summe). Auf den **fertigen** Blättern
lohnt kein Neuschreiben, nur **Durchstreichen mit dem Stift** — Ziel ist Navigierbarkeit, nicht
Schönheit. Vorlagen bleiben unverändert, damit sie weiter dem Blatt entsprechen.

| Blatt | durchstreichen | stattdessen daneben (falls Platz) |
|---|---|---|
| ②/③ | die drei ausgeschriebenen Loss-Formeln in der Aktivierungs-/Loss-Tabelle (MSE, binary_crossentropy, categorical_crossentropy) | nur die **Keras-Namen** — gefragt ist nie die Formel, sondern welcher Loss zu welcher Ausgabe passt |
| ②/③ | Softmax-Formel a_j = e^(z_j)/Σe^(z_k) | „normiert auf **Summe 1** ⇒ Wahrscheinlichkeitsverteilung; Sigmoid pro Neuron nicht" |
| ②/③ | L2-Strafterm C + λ/(2n_w)·Σw² | „Strafterm **λ·Σw²** auf den Loss" |
| ⑥ | nichts | alle Metrik-Formeln bleiben — Typ „Confusion Matrix ausrechnen" verlangt sie (S3 Aufg. 2) |
| Probabilistisch | nichts | D_M und die KDE-Normierung 1/(N·h) sind beide schon abgefragt worden (S4 Aufg. 3b) |
| ① / Kap. 4 | nichts | iForest-s und die zwei Normalisierungsformeln sind Einzeiler und klausurrelevant |

**Nicht streichen, auch wenn es nach Formel aussieht:** Shape-Regeln, Gewichte-Zählen
(C_in·k·k·filters, n_in·n_out), σ'(z)_max = 0,25, Deep-SVDD-Score ‖φ(x)−c‖² − R².
Die stehen alle in Aufgabentypen 2/5/10.

### Originale für Di 28.7. nachm. — „alles bis f-AnoGAN"

Gearbeitet wird in **`uebungen_paulus.pdf`** (dieselben Aufgaben **ohne** Lösungen), korrigiert
gegen den Lösungsteil in **`uebungen.pdf`** ab S. 29. Seitenzahlen unten = `uebungen_paulus.pdf`.
Kriterium der Auswahl: alles, was **kein Kapitel 08** (SVM, OCSVM, Deep SVDD, GOAD) und **kein
Clustering** braucht.

| # | Aufg. | S. | Inhalt | Typ |
|---|---|---|---|---|
| 1 | **3** | 6 | Conv-Autoencoder in Keras schreiben (64×64×1, 3× halbieren, 16→32→64 Maps, z = 10, Kernel 5×5, Decoder gespiegelt) | 3 |
| 2 | **9** | 15–19 | **AnoGAN komplett:** a) Generator (z = 100 → 64×64×3, nur Faltungsvarianten, BatchNorm, Sigmoid am Ausgang) · b) Discriminator (3 Faltungen, LeakyReLU) · c) GAN-Training in Worten · d) AnoGAN-Score · e) f-AnoGAN-Encoder + Verbindung mit dem eingefrorenen Generator | 9 |
| 3 | **5** | 9–10 | Architekturfehler in drei CNNs (32×32×3 → 5 Klassen) | 5 |
| 4 | **2** | 5 | CNN-Ausgabe-Shapes, 32×32×3, 3× MaxPool | 2 |
| 5 | **4** | 7–8 | Data Leakage in vier sklearn-Ausschnitten (`SVC` nur als Blackbox, kein SVM-Wissen nötig) | 4 |
| 6 | **8** | 14 | Zwei geeignete + ein ungeeignetes **Novelty**-Verfahren zum Plot | 8 |
| 7 | **12** | 27 | Zwei geeignete + ein ungeeignetes **Ausreißer**-Verfahren zum Plot | 12 |
| 8 | **1** | 1–4 | MC mit Begründung, **nur** 1.1, 1.3, 1.4, 1.5, 1.6, 1.8, 1.9, 1.10 | 1 |

**Reihenfolge ist Absicht:** Blatt ⑤ zuerst übertragen, dann sofort Aufg. 3 und 9 — das sind
genau die Aufgaben, die das frisch geschriebene Blatt testen (Open Book = Navigationsprüfung).
Was nicht fertig wird, rutscht auf Mi 29.7. nachm.; zuletzt fallen dürfen 8, 12 und der
MC-Block, die sind kurz und decken keinen ungeübten Typ ab.

**Ausgelassen (Stoff noch nicht dran bzw. gestrichen):**
- **1.2** (FC-Schichten vs. SVM) → erst nach Di vormittags
- **1.7** (VAE / KL-Divergenz) → per Klammer-Regel gestrichen, überspringen
- **6 + 7** (SVM / OCSVM von Hand, S. 11–13) und **10** (Deep SVDD, S. 20–23) → Generalprobe Do
- **11** (Clustering, S. 24–26) → gestrichen; falls Do doch Zeit ist, als Gegencheck zum bekannten
  Rest-Widerspruch der Klammer-Regel

**Zwei Fallen in den Musterlösungen** (Stoffumfang hat sich geändert):
- Aufg. **8**: Musterlösung nennt **OCSVM + KDE**. OCSVM kommt erst Di vormittags — mit
  **KDE + GMM** ist die Aufgabe vollständig beantwortet. Ungeeignet bleibt der
  Mahalanobis-Abstand (unimodal, deckt den leeren Bereich mit ab).
- Aufg. **12**: Musterlösung nennt **iForest + LOF**. **LOF ist per Klammer-Regel raus** — zweites
  Verfahren aus dem eigenen Repertoire wählen (kNN-Abstand oder KDE).

### Änderungslog des Plans

- **27.7. abends (dieser Stand) — Originale vorgezogen, „alles bis f-AnoGAN":** Der Slot
  Di 28.7. 14–16 bekommt statt des generierten Blatts `Session07_GANs` die **Original-Aufgaben
  1 (Teilmenge), 2, 3, 4, 5, 8, 9, 12** (Kasten unten). Blatt ⑤ übertragen bleibt davor stehen.
  **Bewusst in Kauf genommen:** (a) der Termin ist mit ~2,5–3 h überbucht, Überhang geht auf
  Mi 29.7. nachm. (der Slot trug vorher die Originale 1–5, ist also nur getauscht);
  (b) die **Generalprobe am Do verliert ihren Charakter als volle 90-min-Klausur** — frisch
  bleiben nur Aufg. 6, 7, 10, 11 + MC 1.2, aufgefüllt wird mit generierten Aufgaben zu den
  Typen 2/3/4/5. Typ 9 (AnoGAN) wird dadurch **am Original** statt am generierten Blatt geübt,
  was der Klausur näher kommt.
- **26.7. abends:** Blatt `Session05_NeuronaleNetze` und Blatt `Session06`
  gelöst + korrigiert, Blatt ① übertragen — der Aufräumtag ist durch. Damit ist **Mi 29.7.
  nachm. entlastet** (das S5-Blatt sollte dort erst gelöst werden) und trägt jetzt die
  Blätter-Nachträge + Originale 1–5. Offen geblieben vom 26.7.: Blätter ②/③ Korrekturlesen
  (→ Mi 29.7.). Neu aufgenommen: Blatt ④ wird **gesplittet** (SVM-Teil Di, Deep-SVDD-Teil Mi),
  damit der Mi-Vormittag nicht zwei Blätter auf einmal tragen muss.
- **26.7. mittags — ED wird doch geschrieben:** Prüfung Mo 27.7., 8:30–10:00. Verloren geht
  der MDT-Slot Mo vormittags (3 h). Umbau: Mo 14–16 trägt den ganzen GAN-Lesestoff, Praktikum 08
  nur mitlesend; Blatt ⑤ + Blatt `Session07_GANs` auf Di 28.7. 14–16; S5-Reste auf Mi 29.7.
  14–16. **Ersatzlos gestrichen:** Notebook 05 Teil 3 (binäres CNN + `class_weight`) — reiner
  Praktikumsdurchlauf ohne eigenen Aufgabentyp. Leitlinie beim Kürzen: *jeder Aufgabentyp
  mindestens einmal ganz* vor jeder Vertiefung (Lehre aus dem SS 2026).
- **25.7.:** ED-Absage machte So + Mo vormittags frei → beide an MDT (am 26.7. teilweise
  revidiert, s. o.).
- **23.7.:** Klammer-Regel geklärt → VAE, PCA, k-Means, LOF, Matrix Profiles raus; S9 entfällt.
- **17./21.7.:** S4 auf Di 21.7. vorgezogen, alles hinter dem 22.7. rückt einen Slot vor.

## Hinweise

- **Klammer-Regel (Ansage Prof., 18.7.) — GEKLÄRT am 23.7.:** Was in der Verfahrensübersicht (Folie 01/33) eingeklammert ist, ist NICHT klausurrelevant — **ausnahmslos alles in Klammern**. Damit fallen raus: **LOF, Matrix Profiles** (03a, bereits entfernt), **VAE, PCA, k-Means**. Konsequenz: S6 nur noch **AE (ohne VAE)**, **S9 (Kap. 7a, Clustering/PCA) entfällt komplett** → der Slot Di 28.7. 14–16 wird frei (Reserve/Originale). Blatt `Blatt_Clustering_PCA.md` und der VAE-Teil von `Session06_Autoencoder_VAE` sind obsolet.
  - ⚠️ Rest-Widerspruch (bewusst nachrangig, Prof.-Ansage zählt): Die Übungssammlung führt Clustering als Aufgabentyp 11 — falls in der Generalprobe (30.7.) eine reine Clustering-Aufgabe auftaucht, kurz gegenchecken statt blind überspringen.
- `mlAno08_gans.zip` **entpackt ✅** (Notebook + `my_generator_1000.hdf5` /
  `my_discriminator_1000.hdf5` liegen in `Praktika/`). Lauffähigkeit noch nicht bestätigt —
  in den Praktika 08–11 mit denselben Versionsfehlern rechnen wie in 07: `np.float` → `float`,
  `plt.boxplot(labels=)` → `tick_labels=`, `.shape()` → `.shape`
- Zusatzmaterial-Notebooks (VAE, Matrix Profiles) nur bei Zeitüberschuss
- Review-Paper (40 S.) = Hintergrund, nicht priorisieren
- In jeder Session Claude nutzen: Aufgaben generieren, Notebook-Fragen klären, Zusammenfassungen gegenchecken

## Offene To-dos

- [ ] **Nachträge auf Blätter ②/③** (Slot Mi 29.7. nachm., zusammen mit dem Korrekturlesen):
  BatchNorm normalisiert **Aktivierungen**, nicht Gewichte (+ γ/β gelernt) · **σ'(z)_max = 0,25**
  (die 1 gehört zu tanh) und beide Unstable-Gradient-Phänomene laufen Richtung **Eingangsschicht** ·
  Shape-Dreizeiler (`same` ⇒ bleibt / `valid` ⇒ −(k−1) / Pooling abrunden vs. strides=2 aufrunden) ·
  **Dense = höchste Overfitting-Gefahr** (Parameterzahl = Produkt; Faltung spart per Weight Sharing).
- [ ] **Aufg. 6a/6b von Blatt `Session05` nochmal durchgehen** (von Lena selbst markiert, 26.7.):
  Kettenregel-Argument mit 0,25^L und die Laufrichtung. Wortlaut steht in Stolperfalle 35 im Logbuch.
- [ ] **Blatt ⑤ zu Ende übertragen** (Di 28.7.) — **am 27.7. bis einschließlich GAN-Teil
  geschrieben** (AE/CAE, Curse of Dimensionality, RandNet, GAN-Grundlagen, G-/D-Gerüst ✅).
  Offen nur noch **AnoGAN (Folien 37–42)** und **f-AnoGAN (Folien 43–49)** = der Typ-9-Kern,
  ~1 Seite. Vorlage ist gegen Foliensatz 07 geprüft (26./27.7.); f-AnoGAN-Score **ohne**
  MSE-Terme schreiben (Formel-Diät), L_res/L_disc als Abstände benennen.
- [ ] **Frage-Disziplin-Drill für die Generalprobe (30.7.):** Claude 2–3 mehrteilige Textaufgaben
  bauen lassen, die gezielt das wiederkehrende Fehlerbild testen — **Begründung passt nicht zur
  gestellten Frage** + **nicht alle Teilfragen beantwortet** (Stolperfallen 11/13/19/20/21/29).
  Mit versteckter Präzisierung in der Frage, unter Zeitdruck lösen. Ziel: erst Frage markieren,
  dann jede Teilfrage abhaken.
- [ ] **Klausur-Reihenfolge auf Blatt ① notieren** (Lehre aus dem SS 2026, Punkt 4): Open Book
  ist eine Navigationsprüfung — erst alle Ein-Zeilen-Teilaufgaben einsammeln, Code-/Zeichenaufgaben
  danach.
