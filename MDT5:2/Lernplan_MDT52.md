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
→ **Beide bleiben bis zum 29.7. unangetastet** (Generalproben-Material). Vorher wird mit von Claude generierten, ähnlichen Aufgaben geübt.

## Die 12 Aufgabentypen der Übungssammlung (Zielbild fürs Üben)

1. **MC mit Begründung** (alle Themen — Punkte nur mit richtiger Begründung!)
2. **CNN Ausgabe-Shapes** pro Schicht berechnen
3. **Keras-Code schreiben**: Autoencoder nach Textbeschreibung
4. **Data-Leakage finden**: sklearn-Code (Scaler/GridSearch vor/nach Split, Pipeline)
5. **Architekturfehler finden** (Reshape-Unsinn, zu viel Pooling …)
6. **SVM von Hand**: Support-Vektoren + Trenngerade zeichnen, Einfluss von C, Kernel-Trick
7. **OCSVM von Hand**: Einfluss von ν, warum Kernel-Trick nötig
8. **Verfahrenswahl** zu gegebenem Daten-Plot (geeignet/ungeeignet + Begründung)
9. **AnoGAN komplett**: Generator-/Discriminator-Code, Training beschreiben, Anomalie-Score, f-AnoGAN-Encoder
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

## Sessionplan (Stand 17.7. — SOS-Klausur entfällt dieses Semester, Termine aus dem Kalender)

Erledigt: **S1 (8.7.)** Kap. 1+2, Blatt 1 korrigiert. **S2 (18.7.)** Kap. 3a/4 + Praktikum 02 + Blatt korrigiert — Details im Lern-Logbuch `CLAUDE.md`; Blatt ① -Erweiterung noch offen. Offen aus Phase 1: S1-Nacharbeit (Praktika 01a/01b + NumPy-Blatt) am 22.7.

| Termin | Praktikum | Stoff + Übung |
|---|---|---|
| **Fr 17.7., 15:15–17:15** | 02 (Abstand) | **S2 nachholen.** Kap. 4: kNN, Isolation Forest (3a optional → weglassen). Blatt ① erweitern. Blatt `Session02_Abstand` (Typ 8/12) |
| **Mo 20.7., 14–16** | 03 (Evaluierung) | **S3.** Kap. 5: ROC/AUC, Splits. Blatt ⑥. Blatt `Session03_Evaluierung` (Leakage, Typ 4) |
| **➕ Di 21.7., 14–16 (NEU — in Kalender eintragen!)** | 04 (Probabilistisch) | **S4.** Kap. 6: Mahalanobis, GMM, KDE. Blatt ① fertig. Blatt `Session04_Probabilistisch` |
| **Mi 22.7., 14–15:30** | 01a + 01b (zügig) | **S1-Nacharbeit.** Python/NumPy: shapes, mean/axis, Broadcasting. Blatt `Session01_Nacharbeit` lösen |
| **Fr 24.7., 14–16** | 05 (Deep Learning) | **S5.** Kap. 3: Shapes, Aktivierungen, Loss. Blätter ② + ③. Blatt `Session05_NeuronaleNetze` (Typ 2/5) |
| **Sa 25.7., 14–16** | 06 + 07 (Autoencoder) | **S6.** Kap. 7 Teil 1: **nur AE (VAE entfällt, Klammer-Regel)**. Blatt `Session06_Autoencoder_VAE` — VAE-Teil überspringen (Typ 3) |
| **🟡 So 26.7. nachm. (PUFFER)** | — | Reserve: Überlauf aus S5/S6 aufholen, hakende Notebooks fertig machen, oder schwächsten bisherigen Aufgabentyp nachtrainieren. Wenn alles im Plan liegt → frei |
| **Mo 27.7., 14–16** | 08 (GANs) | **S7.** Kap. 7 Teil 2: GAN, AnoGAN, f-AnoGAN. Blatt ⑤. Blatt `Session07_GANs` (Typ 9) |
| **Di 28.7., 8:30–11:30** | 09 (SVM) | **S8.** Kap. 8 Teil 1: SVM, Kernel-Trick, OCSVM. Zeichenübungen, Blatt `Session08_SVM_OCSVM` (Typ 6/7) |
| ~~**Di 28.7., 14–16**~~ | ~~Zusatz: pca_clustering~~ | ~~**S9.** Kap. 7a: k-Means, Silhouette, PCA~~ → **ENTFÄLLT (Klammer-Regel).** Slot frei: Reserve / Originale vorziehen |
| **Mi 29.7., 8:30–11:30** | 10 + 11 (Deep SVDD, GOAD) | **S10.** Kap. 8 Teil 2 + 8a. Blatt ④. Blatt `Session10_DeepSVDD_GOAD` (Typ 10) |
| **Mi 29.7., 14–16** | — | Blätter ①–⑦ finalisieren, Skript mit Registerreitern. **Ab jetzt Originale:** Übungssammlung Aufgaben 1–5 lösen, mit Lösungen abgleichen |
| **Do 30.7., 8:30–10:30** | — | **Generalprobe:** Übungssammlung Aufgaben 6–12 unter Klausurbedingungen (90 min, nur Skript + Blätter als Hilfsmittel!), korrigieren |
| **➕ Do 30.7., 14–16 (NEU — in Kalender eintragen!)** | — | Lücken aus Generalprobe schließen, schwächste Aufgabentypen mit neu generierten Varianten nachtrainieren |
| **Fr 31.7., 8:30–10:30** | — | Nur Blätter + markierte MC-Begründungen durchgehen. Kein neuer Stoff! **11:00 Klausur** 🎯 |

**Struktur-Logik:** S4 ist auf Di 21.7. vorgezogen, dadurch rückt alles hinter dem 22.7. einen Slot nach vorn und der Mi 29.7. nachmittags wird frei für Originale 1–5 — der bewährte Dreier-Abschluss (Originale → Generalprobe → Lückenschluss) bleibt erhalten. Die 3h-Vormittage gehören SVM (28.7.) und Deep SVDD/GOAD (29.7.).

## Hinweise

- **Klammer-Regel (Ansage Prof., 18.7.) — GEKLÄRT am 23.7.:** Was in der Verfahrensübersicht (Folie 01/33) eingeklammert ist, ist NICHT klausurrelevant — **ausnahmslos alles in Klammern**. Damit fallen raus: **LOF, Matrix Profiles** (03a, bereits entfernt), **VAE, PCA, k-Means**. Konsequenz: S6 nur noch **AE (ohne VAE)**, **S9 (Kap. 7a, Clustering/PCA) entfällt komplett** → der Slot Di 28.7. 14–16 wird frei (Reserve/Originale). Blatt `Blatt_Clustering_PCA.md` und der VAE-Teil von `Session06_Autoencoder_VAE` sind obsolet.
  - ⚠️ Rest-Widerspruch (bewusst nachrangig, Prof.-Ansage zählt): Die Übungssammlung führt Clustering als Aufgabentyp 11 — falls in der Generalprobe (30.7.) eine reine Clustering-Aufgabe auftaucht, kurz gegenchecken statt blind überspringen.
- `mlAno08_gans.zip` vor dem 27.7. entpacken und testen
- Zusatzmaterial-Notebooks (VAE, Matrix Profiles) nur bei Zeitüberschuss
- Review-Paper (40 S.) = Hintergrund, nicht priorisieren
- In jeder Session Claude nutzen: Aufgaben generieren, Notebook-Fragen klären, Zusammenfassungen gegenchecken
