# Blatt ⑥ — Evaluierung, Metriken, Data-Leakage-Checkliste (Kap. 5)

> Vorlage zum handschriftlichen Übertragen. Quelle: Foliensatz 05.
> Zielumfang: ~2 handgeschriebene A4-Seiten. Deckt Aufgabentyp 4 (Leakage finden) + MC ab.

---

## Metriken-Formelblock (Folien 16–21) — mit Confusion Matrix

Confusion Matrix (Zeile = tatsächlich, Spalte = erkannt):

|  | erkannt K | erkannt K̄ |
|---|---|---|
| **wirklich K** | TP | FN |
| **wirklich K̄** | FP | TN |

| Metrik | Formel | Frage, die sie beantwortet |
|---|---|---|
| Sensitivität / TPR / **Recall** | TP / (TP+FN) | Welcher Anteil der Klasse K wurde gefunden? |
| Spezifizität / TNR | TN / (TN+FP) | Welcher Anteil der anderen Klasse richtig? |
| Accuracy | (TP+TN) / alle | Anteil richtig insgesamt — **nur bei balancierten Daten!** |
| Balanced Accuracy | ½·(TPR + TNR) | Mittel über beide Klassen |
| **Precision** | TP / (TP+FP) | Welcher Anteil der als K Erkannten ist wirklich K? |
| F1 | 2·(prec·rec)/(prec+rec) | harmonisches Mittel |
| F_β | (1+β²)·(prec·rec)/(β²·prec+rec) | β=0,5 → Precision wichtiger; β=2 → Recall wichtiger |

**Merkbeispiel (Folie 19/20, unbalanciert, K selten):**
- K wird nie erkannt → acc 0,90 aber bal. acc 0,50 → Accuracy lügt!
- K wird doppelt so oft erkannt wie vorhanden → bal. acc 0,95, aber Precision 0,50 → auch bal. acc kann lügen, erst Precision deckt auf

**ROC & AUC (Folie 25):**
- ROC = Plot **TPR gegen FPR** für alle möglichen Schwellwerte
- AUC = Fläche darunter, Interpretation (MC-Klassiker!): **Wahrscheinlichkeit, dass eine zufällige Anomalie einen höheren Score bekommt als ein zufälliger Normalpunkt**
- AUC = 0,5 → Raten; AUC = 1,0 → perfekte Trennung
- sklearn: `roc_curve(true_y, scores, pos_label=1)` → fpr, tpr, thresholds; `roc_auc_score(true_y, scores)`

## Schwellwert wählen (Praktikum 07)

**Schwellwert = Score-Wert (y-Achse). Ausreißeranteil = Anteil der Punkte (x-Achse). Nicht dasselbe!**
Der **sortierte Score-Plot** ist die Übersetzung zwischen beiden.

Drei Wege, je nach Vorwissen:

| Vorwissen | Methode |
|---|---|
| nichts (blind) | sortierten Score-Plot: dort schneiden, wo die Kurve **senkrecht** wird |
| Ausreißeranteil bekannt | **Quantil**: `sorted_scores[int((1−ratio)·n)]` |
| Labels vorhanden | **ROC-Knie**: `best = np.argmin(fpr**2 + (1−tpr)**2)` → `thr[best]` |

- **Pflicht-Gegenprobe:** Schwelle → Indexposition ablesen → `n − Index` = Anzahl Alarme → ist dieser **Anteil** als Ausreißeranteil plausibel? (35 % geflaggt ist keine Outlier Detection.)
- Im sortierten Plot: **Schulter** (flacht ab, steigt weiter) = zweite **Normal**gruppe; erst die **Senkrechte** sind die Ausreißer. Das Histogramm taugt dafür **nicht** — die interessante Region ist genau die, wo die Balken schon fast 0 sind.
- **Knie = OBERES Ende eines senkrechten ROC-Stücks** (senkrecht heißt: gleiche FPR, mehr TPR ⇒ gratis). Danach prüfen, was der letzte TPR-Rest kostet.
- **Fallstrick Quantil:** unterstellt, die Ausreißer seien die **höchsten** Scores. Bei schwerem **Oberschwanz der Normaldaten** (im Boxplot: Ausreißerpunkte der Normal-Box reichen über den Median der Outlier-Box) liegen die Anomalien in einem **mittleren Band** → Quantil schneidet darüber ab, TPR bricht ein **trotz guter AUC**.
- **Diagnoseregel:** hohe AUC + schlechte TPR ⇒ falsche **Schwelle**. Niedrige AUC ⇒ schlechtes **Modell**. Immer AUC **und** Boxplot ansehen, nie nur die TPR eines Betriebspunkts.

## Bias-Variance (Folie 3)

- **Bias** = falsche Modellannahmen → Underfitting (auf Trainingsdaten sichtbar)
- **Varianz** = Anfälligkeit für Rauschen → Overfitting (erst auf Validierungs-/Testdaten sichtbar)
- Beide nicht gleichzeitig minimierbar; Overfitting-Maß = Differenz Trainings- vs. Validierungsergebnis

## Datenaufteilung (Folien 4–9)

- Train / Validierung / Test: **disjunkt!** Trennung beginnt schon bei der Vorverarbeitung
- Abhängigkeiten beachten: z. B. alle Samples eines Probanden in NUR eine Teilmenge (sklearn: Parameter `groups`)
- Validierung → Metaparameter einstellen; **Test → nur einmal ganz am Ende** (bei Fehlschlag „verbraucht")
- Wenig Daten → **k-Fold Cross Validation**: Testdaten zuerst abspalten, Rest in k Teilmengen, jede 1× Validierung; Ergebnis = Mittelwert ± Std
- sklearn nutzt standardmäßig **stratified** CV (Klassenverhältnisse bleiben in jedem Fold erhalten)
- Metaparameter-Suche: `GridSearchCV(pipe, param_grid, cv=5, refit=False)` → pro Kombination eine komplette CV

**Sonderfall Novelty Detection (Folien 12–14, klausurtypisch!):**
Standard-CV verteilt Anomalien auch in die Trainingsfolds — bei Novelty Detection dürfen dort aber NUR Normaldaten sein. Lösung: eigene cv-Liste an GridSearchCV übergeben:
1. Indizes in Normal / Anomalie trennen
2. Normal-Indizes mischen (`np.random.shuffle`)
3. `KFold().split()` NUR auf Normal-Indizes
4. Anomalie-Indizes per `np.concatenate` **jeder Validierungsmenge** hinzufügen
→ Form: Liste von Tupeln `[(train_idx, valid_idx), …]`

## Korrekte Evaluierungs-Pipeline (Folie 11 — auswendig können!)

```python
pipe = Pipeline([('scaler', MinMaxScaler()), ('clf', KNeighborsClassifier())])

train_data, test_data, train_labels, test_labels = train_test_split(
    data, labels, test_size=0.2, random_state=123)   # 1. Split ZUERST

grid_search = GridSearchCV(estimator=pipe,
    param_grid={'clf__n_neighbors': [5, 10, 15, 20]},
    cv=5, refit=False, n_jobs=-2)
grid_search.fit(train_data, train_labels)             # 2. Suche NUR auf Train

pipe.set_params(**grid_search.best_params_)
pipe.fit(train_data, train_labels)                    # 3. Finale Pipeline auf Train
np.mean(pipe.predict(test_data) == test_labels)       # 4. Test EINMAL am Ende
```

Warum Pipeline? Scaler + Klassifikator werden als **eine Einheit** behandelt → bei jeder CV-Teilung wird der Scaler nur auf dem jeweiligen Trainings-Fold gefittet. Testdaten werden mit Trainings-Statistik skaliert.

## Data-Leakage-Checkliste (Aufgabentyp 4 — Code-Fehler finden)

1. `scaler.fit()` oder `fit_transform()` auf **Gesamtdaten oder Testdaten**? → Leakage! (fit nur Train)
2. `train_test_split` **nach** der Normalisierung? → Leakage! (Split muss zuerst kommen)
3. GridSearchCV/CV **ohne Pipeline**, aber mit vorab global skalierten Daten? → Leakage in jeden Fold
4. Testdaten mehrfach benutzt (nach Metaparameter-Anpassung nochmal getestet)? → Testdaten verbraucht
   - auch: Metaparametersuche und finale Bewertung auf **derselben** Datenmenge? → die „beste" Parameterwahl ist an genau diese Daten angepasst, Testergebnis zu optimistisch
5. Abhängige Samples (gleicher Proband/gleiche Serie) in Train UND Test? → verstecktes Overfitting
6. Novelty Detection: Anomalien in Trainingsfolds der CV? → falsche Aufteilung (s. o.)
7. Accuracy bei stark unbalancierten Daten als einzige Metrik? → falsche Metrik (bal. acc / Precision+Recall / AUC)
8. Benutzt die **Vorverarbeitung die Labels**? (z. B. Imputation mit `median` getrennt nach Klasse) → schwerste Form von Leakage: Das Label steckt danach im Merkmal selbst. Bei neuen Daten ist das Label unbekannt → Modell wirkt im Test gut, bricht im Feld ein. Korrekt: **ein** Median pro Merkmal, nur auf den Trainingsdaten berechnet.

**Achtung, kein Fehler:** Beim Novelty-CV-Rezept (s. o.) stehen in jedem Fold **dieselben** Anomalien — das ist methodenbedingt so gewollt, nicht falsch. Als Einschränkung formulieren: Streuung über die Folds wird dadurch unterschätzt.

## Keras-Metriken (Folie 24)

```python
net.compile(optimizer=tf.keras.optimizers.Adam(),
            loss='categorical_crossentropy',
            metrics=[tf.keras.metrics.CategoricalAccuracy(),
                     tf.keras.metrics.Precision(),
                     tf.keras.metrics.Recall()])
```
