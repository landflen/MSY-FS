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
| ~~08a Zusätzl. klassif.~~ | 6 F. | Selbstüberwacht, Contrastive Learning, SimCLR, CSI — **nicht klausurrelevant**, wie 03a und 07a ein „Zusätzliche Verfahren"-Satz (kein Übungsblatt, kein Praktikum, kein Aufgabentyp); am 29.7. aus Blatt ④ entfernt | — |

**Übungssammlung (mit Lösungen)** = explizit „Beispiele für mögliche Prüfungsaufgaben“.
`uebungen_paulus.pdf` = identische Aufgaben **ohne** Lösungen.
→ Am **29.7.** wurden die Originale **auf Teilaufgabenebene** zweigeteilt; die reservierte Hälfte
(klausurtypischer Querschnitt, ≈ 80 min über alle Typen) ist am **30.7. als Generalprobe
geschrieben**, die freie Hälfte ist Übungsreserve — Kasten „Originale — Aufteilung".

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

## Sessionplan (Stand 30.7. mittags — **1 Tag bis zur Klausur**)

### Erledigt (Details im Lern-Logbuch `CLAUDE.md`)

| Session | Termin | Stand |
|---|---|---|
| S1 | 8.7. | ✅ Kap. 1+2, Blatt 1 korrigiert |
| S2 | 18.7. | ✅ Kap. 3a/4 + Praktikum 02 + Blatt `Session02`; Blatt ① übertragen (26.7.) |
| S3 | 20.7. | ✅ Kap. 5 + Praktikum 03 (beide Teile) + Blatt `Session03`; Blatt ⑥ übertragen |
| S4 | 23./24.7. | ✅ Kap. 6 + Praktikum 04 + Blatt `Session04`; Blatt `Probabilistisch` übertragen |
| S5 | 24./26.7. | ✅ Kap. 3 + Praktikum 05 (Teile 1+2) + Blatt `Session05`; Blätter ②/③ übertragen — **offen: Korrekturlesen + 4 Nachträge** |
| S6 | 25./26.7. | ✅ Kap. 07 S. 1–24 + Praktika 06/07 + Blatt `Session06`; **Blatt ⑤ vollständig übertragen (28.7.)** — inkl. AnoGAN + f-AnoGAN |
| S7 | 27./28.7. | ✅ **komplett**: Kap. 07 S. 25–51 (GAN, AnoGAN, f-AnoGAN) + Praktikum 08 (mitlesend) + Blatt `Session07_GANs` **gelöst und korrigiert**; Blatt ⑤ vollständig übertragen (28.7.). Damit ist **Typ 9 einmal ganz geübt** — die Original-Aufg. 9 ist jetzt Vertiefung, nicht Ersatz |
| S8 | 28.7. | ✅ Kap. 08 S. 1–37 + Praktikum 09 + Blatt `Session08_SVM_OCSVM` (**Typ 6/7 einmal ganz**); Blatt ④ bis Folie 30. Nachm.: von 8 Originalen nur Aufg. 3, dafür **Blätter markiert** |
| S10 | 29.7. | ✅ **komplett**: Kap. 08 ganz gelesen, **Praktika 10 + 11 ⇒ Praktikumsteil komplett (01–11)**, Blatt `Session10` gelöst und korrigiert ⇒ **Typ 10 einmal ganz** |
| Blätter | 29./30.7. | ✅ **alle sieben Blätter fertig geschrieben** — Blatt ④ ab OCSVM (OCSVM ✅ 29.7., Deep SVDD/GOAD/CutPaste ✅ 30.7.), Blatt ⑤ ✅ 28.7. Handgeschriebene Blätter sind farbmarkiert (28.7.) |
| **Generalprobe** | **30.7. vorm.** | ✅ **komplett geschrieben** — reservierter Originalsatz (1.1/1.3/1.5/1.8/1.10 · 2 · 4.1/4.3 · 5.2 · 6a+b · 7b · 8 · 9a+c+d · 10.2 · 12), 90 min, nur Skript + Blätter |
| S9 | — | ⛔ entfällt (Klammer-Regel: Clustering/PCA nicht klausurrelevant) |
| S1-Nacharbeit | 22.7. geplant | ⚠️ **nicht im Logbuch dokumentiert** — Praktika 01a/01b + Blatt `Session01_Nacharbeit`. Kein eigener Aufgabentyp ⇒ **wird nicht nachgeholt** |

**Alle 12 Aufgabentypen sind mindestens einmal ganz geübt** (Typ 9 in S7, Typ 6/7 in S8,
Typ 10 in S10; Typ 11 ist per Klammer-Regel gestrichen). Der Stoffteil des Plans ist damit
**abgeschlossen** — was bleibt, ist Korrektur, Lückenschluss und Navigation.

### Restplan

Alles bis einschließlich **Do 30.7. vormittags** ist abgearbeitet (Details in der Tabelle oben und
im Logbuch). Übrig sind zwei Slots:

| Termin | Inhalt |
|---|---|
| **Do 30.7., 14–16** (2 h) | **Generalprobe auswerten + Lücken schließen.** Reihenfolge, Abbruch von unten: (1) **Korrektur der Generalprobe** gegen den Lösungsteil in `uebungen.pdf` ab S. 29 — dabei die **zwei Musterlösungs-Fallen** beachten (Aufg. 8 OCSVM+KDE ist nutzbar; Aufg. 12 LOF ist raus). (2) Aus dem Fehlerbild **1–2 schwächste Typen** nachziehen — dafür stehen die **freien Teilaufgaben** bereit (Kasten unten), vor allem **10.3** (`use_bias`-Falle, Stolperfalle 50), **7a/6c** (Kernel-Trick) und **5.1/5.3**. (3) Was in der Klausur **auf den Blättern nicht gefunden** wurde, nachtragen oder markieren — das ist die eigentliche Lehre einer Open-Book-Probeklausur. (4) Nachträge ②/③ + ⑥ + Streichliste — **darf fallen** |
| **Fr 31.7., 8:30–10:30** | Nur **Blätter + markierte MC-Begründungen** durchgehen, dazu die Klausur-Reihenfolge auf Blatt ①. **Kein neuer Stoff, keine neuen Aufgaben.** **11:00 Klausur** 🎯 |

**Unantastbar:** der Ruhetag Fr vormittags. Am Do nachm. gilt: **Korrektur vor Nachtrainieren,
Nachtrainieren vor Blätterkosmetik.** Neue Aufgaben nur zu Typen, die in der Generalprobe
tatsächlich schwach waren — nicht flächendeckend.

### Streichliste für die abgeschriebenen Blätter (Do 30.7. nachm., Punkt 4 — darf fallen)

Entscheidung 27.7.: Formeln, die zu **keinem** der 12 Aufgabentypen gehören, stehen in der
Open-Book-Klausur ohnehin im Skript — auf dem Blatt kosten sie nur Suchzeit. In den **Vorlagen**
von Blatt ④ und ⑤ sind sie schon raus — ⑤ ist seit dem 28.7. **komplett abgeschrieben**, also beim
Durchstreichen mitprüfen (Curse-of-Dim.-Quotient, AE-Loss-Summe, f-AnoGAN-MSE-Terme). Auf den **fertigen** Blättern
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

### Originale — Aufteilung (Stand 30.7.: reservierter Satz ✅ geschrieben)

Gearbeitet wird in **`uebungen_paulus.pdf`** (dieselben Aufgaben **ohne** Lösungen), korrigiert
gegen den Lösungsteil in **`uebungen.pdf`** ab S. 29. Seitenzahlen = `uebungen_paulus.pdf`.

**Aufteilungskriterium (29.7., Ansage Lena):** Reserviert wird **eine willkürliche Auswahl, die so
auch in der Klausur stehen könnte** — nicht die schwächsten Typen. Eine Probeklausur aus lauter
Baustellen wäre am Vortag demotivierend und misst nichts Realistisches. Geschnitten wird deshalb
**auf Teilaufgabenebene**: aus fast jeder Aufgabe wandert ein Teil in die Generalprobe, der Rest
ist frei. So deckt die Probeklausur **alle Typen** ab (wie eine echte Klausur, die quer durch die
Vorlesung greift) und trotzdem bleibt von jeder Aufgabe etwas zum Vorabüben übrig.

Teilaufgabenstruktur laut `uebungen_paulus.pdf`: **1.1–1.10** · **2** ein Block (13 Shape-Zeilen) ·
**3** einteilig · **4.1–4.4** · **5.1–5.3** · **6 a–d** · **7 a–c** · **8** einteilig ·
**9 a–e** · **10.1–10.4** · **11 a–c** (gestrichen) · **12** einteilig.

#### ✅ Generalprobe Do 30.7. — geschrieben, jetzt Korrekturmaterial

| Aufg. | S. | Inhalt | Typ | Kap. | ≈ min |
|---|---|---|---|---|---|
| **1.1, 1.3, 1.5, 1.8, 1.10** | 1–4 | MC mit Begründung: Autoencoder · KDE · GANs · Motivation Novelty Detection · Outlier Detection | 1 | alle | 11 |
| **2** (ganz) | 5 | CNN-Ausgabe-Shapes, 32×32×3, 13 Zeilen bis `Dense(15, softmax)` | 2 | 03 | 8 |
| **4.1, 4.3** | 7–8 | Data Leakage in zwei sklearn-Ausschnitten (`SVC` nur als Blackbox) | 4 | 05 | 8 |
| **5.2** | 9–10 | Architekturfehler im zweiten Netz (32×32×3 → 5 Klassen) | 5 | 03 | 5 |
| **6 a) + b)** | 11–12 | SVM von Hand: Trenngerade + Support-Vektoren bei sehr großem C zeichnen; dann C schrittweise reduzieren | 6 | 08 | 9 |
| **7 b)** | 13 | OCSVM: Trennebene bei optimal angepasstem ν zeichnen/beschreiben | 7 | 08 | 5 |
| **8** (ganz) | 14 | Zwei geeignete + ein ungeeignetes **Novelty**-Verfahren zum Plot | 8 | 04/06 | 6 |
| **9 a) + c) + d)** | 15–18 | a) Generator-Architektur (z = 100 → 64×64×3, nur Faltungsvarianten, BatchNorm, Sigmoid) · c) GAN-Training in eigenen Worten · d) AnoGAN-Score für neue Daten | 9 | 07 | 17 |
| **10.2** | 20–21 | Deep-SVDD-Code-Ausschnitt beurteilen | 10 | 08 | 5 |
| **12** (ganz) | 27 | Zwei geeignete + ein ungeeignetes **Ausreißer**-Verfahren zum Plot | 12 | 04 | 6 |

**Summe ≈ 80 min** (+ ~10 min Lese-/Suchzeit = 90). **Alle 10 relevanten Aufgabentypen vertreten**,
Kapitel 03–08 durchgehend, gemischte Schwierigkeit: drei kurze sichere Teile (2, 8, 12), fünf
mittlere, ein großer Codeblock (9a). Vorgesehene Reihenfolge war: erst die Ein-Zeilen-Teile
(8, 12, 5.2, 10.2), dann 2, 4, 6, 7, dann 9, MC zuletzt.

→ **Korrektur am Do-Nachmittag.** Beim Auswerten nicht nur zählen, sondern drei Dinge notieren:
(a) welche Teilfragen **unbeantwortet** blieben (das wiederkehrende Muster, Stolperfallen
11/13/19/20/21/29/45/49), (b) wo die **Begründung nicht zur Frage** passte, (c) was auf den
Blättern **nicht gefunden** wurde. Nur (a)–(c) steuern den Rest des Tages.

#### 🔓 Frei — Übungsreserve für den Do-Nachmittag

| Aufg. | S. | Inhalt | Typ | ≈ min |
|---|---|---|---|---|
| **1.2, 1.4, 1.6, 1.9** | 1–4 | MC: FC-Schichten vs. SVM · Normalisierung · Outlier Detection · GANs | 1 | 9 |
| **4.2, 4.4** | 7–8 | Data Leakage, die beiden übrigen Ausschnitte | 4 | 8 |
| **5.1, 5.3** | 9–10 | Architekturfehler im ersten und dritten Netz | 5 | 10 |
| **6 c) + d)** | 12 | Kernel-Trick erklären + warum hier nicht nötig · OCSVM-Trennebene mit RBF vs. Zweiklassenfall | 6 | 7 |
| **7 a) + c)** | 13 | OCSVM mit **linearem** Kernel und ν = 0.001 · warum der Kernel-Trick für OCSVMs praktisch notwendig ist | 7 | 7 |
| **9 b) + e)** | 16, 19 | b) Discriminator-Architektur (3 Faltungen, LeakyReLU) · e) f-AnoGAN-Encoder + Verbindung mit dem eingefrorenen Generator | 9 | 13 |
| **10.1, 10.3, 10.4** | 20–23 | Die drei übrigen Deep-SVDD-Ausschnitte — **10.3 ist die `use_bias`-Falle**, die auf dem generierten Blatt heute durchgerutscht ist (Stolperfalle 50) | 10 | 15 |
| **3** (ganz) | 6 | Conv-Autoencoder in Keras schreiben — ✅ **28.7. gerechnet** (→ Stolperfallen 43/44), als Wiederholung frei | 3 | 12 |
| **11 a–c** | 24–26 | Clustering — gestrichen (Klammer-Regel), nur als Gegencheck | 11 | – |

**Ausgelassen:** **1.7** (VAE / KL-Divergenz) → per Klammer-Regel gestrichen.
**≈ 80 min freier Übungsstoff**, ebenfalls über alle Typen verteilt — **mehr als der
Do-Nachmittag trägt.** Nach der Korrektur gezielt 2–3 Teilaufgaben daraus ziehen, nicht der Reihe
nach abarbeiten.

**Zwei Fallen in den Musterlösungen** (Stoffumfang hat sich geändert):
- Aufg. **8** (reserviert): Musterlösung nennt **OCSVM + KDE** — OCSVM ist seit dem 28.7. durch,
  die Musterlösung ist also **voll nutzbar**. **KDE + GMM** wäre ebenfalls vollständig. Ungeeignet
  bleibt der Mahalanobis-Abstand (unimodal, deckt den leeren Bereich mit ab).
- Aufg. **12** (frei): Musterlösung nennt **iForest + LOF**. **LOF ist per Klammer-Regel raus** —
  zweites Verfahren aus dem eigenen Repertoire wählen (kNN-Abstand oder KDE).

### Änderungslog des Plans

- **30.7. mittags — Plan auf die Schlussgerade gekürzt:** Generalprobe **komplett geschrieben**,
  Blatt ④ **ab Deep SVDD fertig übertragen** ⇒ alle sieben Blätter stehen, alle 12 Aufgabentypen
  sind einmal ganz geübt, der Praktikumsteil ist komplett. **Der Stoffteil des Plans ist damit
  durch.** Übrig sind zwei Slots (Do nachm., Fr vorm.), der Restplan wurde entsprechend
  zusammengestrichen. Neue Priorität am Do nachm.: **Korrektur der Generalprobe vor allem
  anderen**, danach gezielt 2–3 freie Teilaufgaben zu den schwächsten Typen, zuletzt Blätterpflege
  (darf fallen). Der reservierte Originalsatz ist nicht mehr gesperrt, sondern Korrekturmaterial;
  die freie Hälfte ist bewusst **größer als der Nachmittag** — daraus wird gezogen, nicht
  abgearbeitet.
- **29.7. abends — Originale aufgeteilt statt komplett gesperrt (Ansage Lena):** Für die
  Generalprobe wird nur so viel reserviert, wie in **90 min** passt. **Erste Ziehung nach
  „neuestes + schwächstes" verworfen** — eine Probeklausur aus lauter Baustellen ist am Vortag
  demotivierend und misst nichts Realistisches. Geschnitten wird jetzt **auf Teilaufgabenebene**
  statt ganze Aufgaben zu sperren: Generalprobe = **1.1/1.3/1.5/1.8/1.10 · 2 · 4.1/4.3 · 5.2 ·
  6a+b · 7b · 8 · 9a+c+d · 10.2 · 12** (≈ 80 min, **alle 10 Typen**, Kapitel 03–08 durchgehend).
  Frei bleibt aus fast jeder Aufgabe ein Teil, zusammen ≈ 80 min — darunter **10.3** (die
  `use_bias`-Falle von Stolperfalle 50) und **7a/6c**, also genau der Kap.-08-Stoff, der sich
  jetzt noch üben lässt.
- **29.7. — Originale zurück auf die Generalprobe, Rücknahme der Vorziehung vom 27.7.:** Vom
  Di-Nachmittag ist nur Original-Aufg. 3 erledigt (dafür sind die handgeschriebenen Blätter
  markiert). Der Überhang wird **nicht** am Mi nachm. nachgeholt, sondern bildet am **Do** die
  Generalprobe — die dadurch wieder eine **volle 90-min-Klausur aus Originalaufgaben** ist und
  ohne generierte Füllaufgaben auskommt. Kap. 08 ist vollständig gelesen ⇒ Mi vormittags nur noch
  Praktika 10/11; Mi nachm. trägt **Blatt ④ ab OCSVM + Blatt `Session10` (Typ 10)**, die
  Blätter-Nachträge rutschen dahinter und dürfen fallen. Damit bleibt die Leitlinie gewahrt:
  *jeder Aufgabentyp mindestens einmal ganz* — Typ 10 ist der letzte offene.

- **28.7. — S8 durch, Blatt ⑤ fertig, Blatt ④ halb:** Praktikum 09 + Blatt `Session08` erledigt
  (**Typ 6/7 einmal ganz gerechnet**), Blatt ⑤ **vollständig** übertragen (AnoGAN + f-AnoGAN
  nachgezogen ⇒ **Typ 9 steht**), Blatt ④ bis Folie 30 (SVM überwacht) geschrieben. Der Slot
  **Di nachm.** verliert dadurch seinen ⑤-Punkt und bekommt stattdessen **Blatt ④ ab OCSVM** —
  das nimmt dem Mi-Vormittag den Deep-SVDD-/GOAD-Blattteil ab, der dort neben Kap. 08 S. 38–64
  ohnehin eng lag. Ungeübt bleiben damit nur noch **Typ 10** (Deep-SVDD-Code, Mi) und die
  Original-Aufgaben.
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
  - ⚠️ Rest-Widerspruch (bewusst nachrangig, Prof.-Ansage zählt): Die Übungssammlung führt Clustering als Aufgabentyp 11 (Original-Aufg. 11 a–c). Falls in der Klausur doch eine reine Clustering-Aufgabe steht, **nicht blind überspringen** — k-Means-Eignung und Ellbogen/Silhouette lassen sich aus Blatt ① und dem Skript beantworten.
- **Praktikumsteil komplett (01–11, Stand 29.7.)** — keine Notebooks mehr offen. Zusatzmaterial
  (VAE, Matrix Profiles) und das Review-Paper bleiben liegen, beides ist nicht klausurrelevant.
- **Mitzunehmen am Freitag:** ausgedrucktes Skript (bzw. das 4-up-Gesamtskript mit
  Inhaltsverzeichnis auf Blatt 1) + die sieben handgeschriebenen, farbmarkierten Blätter.
  **Keine Praktika** — die sind nicht zugelassen.

## Offene To-dos

- [ ] **Generalprobe korrigieren** (Do 30.7. nachm., **erster Punkt**) — Lösungsteil
  `uebungen.pdf` ab S. 29, die zwei Musterlösungs-Fallen beachten. Ergebnis steuert alles Weitere.
- [ ] **Klausur-Reihenfolge auf Blatt ① notieren** (Lehre aus dem SS 2026, Punkt 4): Open Book
  ist eine Navigationsprüfung — erst alle Ein-Zeilen-Teilaufgaben einsammeln, Code-/Zeichenaufgaben
  danach. **Vor Fr vormittags erledigen** (Zwei-Minuten-Punkt, in der Generalprobe erprobt).
- [ ] **Nachträge auf Blätter ②/③** (Slot Mi 29.7. nachm., zusammen mit dem Korrekturlesen):
  BatchNorm normalisiert **Aktivierungen**, nicht Gewichte (+ γ/β gelernt) · **σ'(z)_max = 0,25**
  (die 1 gehört zu tanh) und beide Unstable-Gradient-Phänomene laufen Richtung **Eingangsschicht** ·
  Shape-Dreizeiler (`same` ⇒ bleibt / `valid` ⇒ −(k−1) / Pooling abrunden vs. strides=2 aufrunden) ·
  **Dense = höchste Overfitting-Gefahr** (Parameterzahl = Produkt; Faltung spart per Weight Sharing).
- [ ] **Aufg. 6a/6b von Blatt `Session05` nochmal durchgehen** (von Lena selbst markiert, 26.7.):
  Kettenregel-Argument mit 0,25^L und die Laufrichtung. Wortlaut steht in Stolperfalle 35 im Logbuch.
- [x] ~~**Blatt ⑤ zu Ende übertragen**~~ ✅ **28.7. komplett** (AE/CAE, Curse of Dimensionality,
  RandNet, GAN-Grundlagen, G-/D-Gerüst, AnoGAN, f-AnoGAN). Damit steht der **Typ-9-Kern** auf Papier.
- [x] ~~**Blatt ④ ab OCSVM (Folie 31) übertragen**~~ ✅ **komplett** — OCSVM am 29.7., Deep SVDD /
  GOAD / CutPaste am 30.7. (Contrastive/08a gestrichen). Damit stehen **alle sieben Blätter**.
- [ ] **Frage-Disziplin beim Korrigieren mitprüfen** (statt des ursprünglich geplanten Drills —
  die Generalprobe hat die Rolle übernommen): In der Korrektur jede Aufgabe daraufhin durchgehen,
  ob **alle Teilfragen beantwortet** wurden und ob die **Begründung zur gestellten Frage** passt
  (Stolperfallen 11/13/19/20/21/29/45/49 — dreimal wiederholt: Was-Fragen sitzen, Warum-Fragen
  enden zu früh). Regel für morgen: **erst die Frage markieren, dann jede Teilfrage abhaken.**
