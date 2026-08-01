# Korrekturliste der handgeschriebenen Blätter (Stand 29.07.2026)

Grundlage: Fotos aller 19 Seiten, gegengelesen gegen die Vorlagen in diesem Ordner.
Reihenfolge: erst umsortieren, dann nummerieren, dann die Nachträge eintragen.

---

## A — Umsortieren (4 Bewegungen)

1. **① Übersichtsseite vor die ① Verfahrenstabelle.** Die Übersicht ist der Einstieg, die Tabelle
   das Nachschlagewerk.
2. **⑤ „Discriminator + Generator bauen" eine Seite nach hinten**, hinter die RandNet/GAN-Seite.
   Beleg auf den Blättern selbst: die CAE-Seite endet mit „# x = y (nächste Seite)", die
   RandNet/GAN-Seite beginnt mit „Warum fit(x=train_data, y=train_data)?" — die beiden gehören
   direkt aneinander.
3. **„Overfitting + Regularisierung" und „Data Augmentation + BatchNorm" hinter die
   Keras-Grundgerüst-Seite**, vor die Fehlerfinder-Checkliste. Dann läuft Kap. 3 durch:
   Shapes → Keras → Regularisierung → Fehlerfinder.
4. **Probabilistisch direkt hinter Kap. 4.** Beides sind die Shallow-Verfahren für Typ 8/12;
   ⑥ steht danach für sich.

## B — Seitenzahlen (oben rechts)

| S. | Blatt / Inhalt |
|---:|---|
|  1 | ① Verfahrensübersicht + Grundbegriffe |
|  2 | ① Verfahrenstabelle (quer) |
|  3 | ②/③ Shapes & Keras |
|  4 | ②/③ Keras-Grundgerüst + Schnellfakten |
|  5 | Overfitting + Regularisierung |
|  6 | Data Augmentation + Batch Normalization |
|  7 | Fehlerfinder-Checkliste |
|  8 | Kap. 4 — kNN, iForest |
|  9 | Probabilistisch — Mahalanobis, KDE, GMM |
| 10 | ⑥ Metriken, ROC/AUC, Bias-Variance, Datenaufteilung |
| 11 | ⑥ Novelty-CV, Pipeline, Leakage-Checkliste |
| 12 | ⑤ Rekonstruktion, AE, CAE |
| 13 | ⑤ fit(x=y), RandNet, GAN |
| 14 | ⑤ Discriminator + Generator bauen |
| 15 | ⑤ AnoGAN + f-AnoGAN |
| 16 | ④ SVM überwacht |
| 17 | ④ OCSVM |
| 18 | ④ Deep SVDD |
| 19 | ④ GOAD + CutPaste |

**Register auf Seite 1 oben rechts:**
Verfahrenswahl 1–2 · Shapes/Keras 3–7 · Shallow 8–9 · Evaluierung 10–11 · AE/GAN 12–15 ·
SVM/Deep SVDD 16–19

---

## C — Was nachgetragen werden muss

### S. 10 (⑥) — fehlt komplett: Abschnitt „Schwellwert wählen"

Gehört zwischen ROC/AUC und Bias-Variance; wenn dort kein Platz ist, oben auf S. 11.
**Wichtigster Nachtrag der ganzen Liste** — der Stoff kam in Praktikum 07 vor und ist nirgends
auf Papier.

> **Schwellwert wählen**
> Schwellwert = **Score-Wert** (y-Achse). Ausreißeranteil = **Anteil der Punkte** (x-Achse).
> Nicht dasselbe — der sortierte Score-Plot ist die Übersetzung zwischen beiden.
> - nichts bekannt → sortierter Score-Plot, dort schneiden, wo die Kurve **senkrecht** wird
> - Anteil bekannt → **Quantil** `sorted_scores[int((1-ratio)*n)]`
> - Labels vorhanden → **ROC-Knie** `best = np.argmin(fpr**2 + (1-tpr)**2)` → `thr[best]`
>
> **Gegenprobe (Pflicht):** Schwelle → Indexposition → `n − Index` = Anzahl Alarme → ist der
> Anteil plausibel? 35 % geflaggt ist keine Outlier Detection.
> **Schulter ≠ Knie:** eine Schulter im sortierten Plot ist eine **zweite Normalgruppe**; erst die
> Senkrechte sind die Ausreißer. Das Histogramm taugt dafür nicht (die interessante Region ist
> genau da, wo die Balken schon fast 0 sind).
> **Knie = OBERES Ende** eines senkrechten ROC-Stücks (gleiche FPR, mehr TPR ⇒ gratis).
> **Quantil-Fallstrick:** unterstellt, die Ausreißer seien die höchsten Scores. Bei schwerem
> Oberschwanz der Normaldaten liegen die Anomalien in einem **mittleren Band** → das Quantil
> schneidet darüber ab, TPR bricht ein **trotz guter AUC**.
> **Diagnoseregel:** hohe AUC + schlechte TPR ⇒ falsche **Schwelle**. Niedrige AUC ⇒ schlechtes
> **Modell**. Immer AUC **und** Boxplot ansehen.

### S. 16 (④ SVM) — ein Halbsatz beim Kernel-Trick

Bei „Kernels: linear, polynomial, RBF/Gauß" steht der RBF-Teil richtig (über den **Abstand**),
der Kontrast fehlt. Dazuschreiben:

> polynomial = **erst Skalarprodukt, dann potenzieren**; RBF = über den **Abstand**.

Kommt in Original-Aufgabe 5a genau so vor.

### S. 18 (④ Deep SVDD) — eine Zeile ist widersprüchlich

Aktuell steht: „Kanalzahl ist frei … **letzte Encoder-Shape muss aber stimmen**". Der zweite
Halbsatz hebt den ersten auf. Durchstreichen und ersetzen durch:

> `Dense → Reshape` muss nur die **Auflösung** treffen (7×7, damit 2× Upsampling wieder 28 gibt);
> die **Kanalzahl ist frei**, weil die nächste `Conv2DTranspose` sie neu setzt.
> Exakt die letzte Encoder-Shape nur, wenn die Aufgabe **„spiegeln"** verlangt (Orig.-Aufg. 3).

### S. 3 (②/③ Shapes) — zwei Nachträge

Bei der Shape-Tabelle, neben „Auflösung halbieren":

> Bei **ungerader** Kantenlänge: Pooling **abrunden**, Conv mit strides=2 **aufrunden** (ceil).
> `same`+strides=1 ⇒ bleibt · `valid`, Kernel k ⇒ **minus (k−1)**.

Bei „Gewichte zählen":

> **Dense = höchste Overfitting-Gefahr** — Parameterzahl ist das **Produkt** (4096·256 ≈ 1 Mio);
> Faltung braucht dank **Weight Sharing** nur k·k·C_in·C_out, unabhängig von der Bildgröße.
> Deshalb sitzen Dropout/L2 genau an den Dense-Schichten.

### S. 1 (①) — Klausur-Reihenfolge oben drauf

Offener Punkt aus dem Lernplan, Lehre aus dem SS 2026 (Open Book = Navigationsprüfung):

> **Reihenfolge in der Klausur:** erst alle **Ein-Zeilen-Teilaufgaben** einsammeln (MC,
> Definitionen, Metaparameter), danach Code- und Zeichenaufgaben. Typ 10 und Typ 9 vor dem
> MC-Block, wenn die Zeit knapp wird. Jede Teilfrage vor dem Antworten **markieren** und
> einzeln abhaken.

### S. 17 (④ OCSVM) — optional, ein Wort

Bei SVDD („findet die kleinste Kugel, die die Normaldaten umschließt") ergänzen:
**ν erlaubt auch hier Ausreißer.**

---

## D — Streichliste (nur wenn Zeit bleibt)

Reine Suchzeit-Optimierung, kein Fehler. Nur **durchstreichen**, nichts neu schreiben.

| Seite | durchstreichen | daneben (falls Platz) |
|---|---|---|
| 3 | die drei ausgeschriebenen Loss-Formeln (MSE, binary_/categorical_crossentropy) | nur die **Keras-Namen** — gefragt ist nie die Formel, sondern welcher Loss zu welcher Ausgabe passt |
| 3 | Softmax-Formel | „normiert auf **Summe 1** ⇒ Wahrscheinlichkeitsverteilung; Sigmoid pro Neuron nicht" |
| 5 | L2-Strafterm C + λ/(2n_w)·Σw² | „Strafterm **λ·Σw²** auf den Loss" |
| 12 | Curse-of-Dim-Quotient, AE-Loss-Summe | Klartextsatz steht schon daneben |

**Nicht streichen, auch wenn es nach Formel aussieht:** Shape-Regeln, Gewichte-Zählen,
σ'(z)_max = 0,25, Deep-SVDD-Score, alle Metrik-Formeln auf S. 10, D_M und die KDE-Normierung
1/(N·h), iForest-s. Die stehen alle in Aufgabentypen 2/5/10 bzw. sind schon abgefragt worden.

---

## E — Geprüft und in Ordnung (nichts zu tun)

- **① beide Seiten:** Grundbegriffe, Taxonomie inkl. Klammern, Entscheidungsbaum (alle 7 Punkte),
  Normalisierungs-Kontrastpaar, iForest-Grenzfälle, contamination, sklearn-Dreizeiler.
  Die 13-zeilige Verfahrenstabelle stimmt Zeile für Zeile.
- **Kap. 4** und **Probabilistisch:** vollständig, inkl. der Restschliffe vom 23.7.
  (Normalverteilung statt „Modalverteilung", Transpose auf der ganzen Klammer, KDE-Summe als
  Funktion).
- **⑥ Metriken:** Confusion Matrix, alle sieben Metriken, F_β-Richtung, das Merkbeispiel,
  ROC/AUC-Definition, Bias-Variance, Datenaufteilung, Novelty-CV, Pipeline, Leakage-Checkliste 1–8
  plus „Achtung, kein Fehler".
- **②/③:** BatchNorm-Zeile richtig (Aktivierungen, nicht Gewichte, mit γ/β), σ'(z)_max = 0,25 mit
  Laufrichtung, Aktivierungs-/Loss-Tabelle, Keras-Grundgerüst, Fehlerfinder-Checkliste.
- **⑤ komplett:** alle drei Code-Gerüste korrekt (CAE mit `filters=3` am Ausgang, G/D mit
  `use_bias=False` + BN + ReLU und dem `from_logits`-Halbsatz, f-AnoGAN-Encoder mit den
  **fallenden** Filterzahlen), GAN-Training in sechs Schritten, AnoGAN-Ablauf, L_disc-Warnung.
- **④:** SVM-Kernel-Block mit der präzisierten „welche Rechnung"-Antwort, OCSVM vollständig
  (vier Kernel-Trick-Schritte, Zeichenregeln, ν-Dreisatz, Inselstrukturen), Deep-SVDD-Verbotsliste
  inkl. „BatchNorm ist KEIN Fehler", R als (1−ν)-Quantil mit dem Volumen-Argument, GOAD mit dem
  korrigierten Loss („kein Weight Decay!") und der Vergleichstabelle, CutPaste.
