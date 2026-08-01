# Blatt ④ — SVM, OCSVM, Deep SVDD, GOAD, CutPaste (Kap. 8)

> Vorlage zum handschriftlichen Übertragen. Quelle: Foliensatz 08.
> Foliensatz **08a (Contrastive Learning / SimCLR / CSI) ist nicht klausurrelevant** — wie 03a
> und 07a ein „Zusätzliche Verfahren"-Satz ohne Übung und ohne Praktikum; am 29.7. entfernt.
> Deckt Aufgabentypen 6/7 (SVM/OCSVM zeichnen) + 10 (Deep-SVDD-Code beurteilen) ab. Zielumfang: ~2,5 A4-Seiten.

---

## SVM überwacht (Folien 5–30) — fürs Zeichnen (Typ 6)

- Trennebene h₀ in der Mitte, Parallelebenen h₁/h₂ durch die nächsten Punkte
- **Optimale Ebene = maximaler Abstand (Margin) zu den nächsten Punkten beider Klassen = Support Vektoren**; Ebene hängt NUR von den SV ab
- **Margin = Streifen zwischen h₁ und h₂**; ±1 ist nur **Normierung** (w, b frei skalierbar) ⇒ Breite 2/‖w‖ ⇒ **Margin max = ‖w‖ min**
- **Nebenbedingung:** kein Punkt zwischen h₁/h₂, jeder auf seiner Seite. Fesselt die Ebene an die Daten — ohne sie wäre w = 0 die Lösung (vgl. triviale Lösung Deep SVDD)

**Zeichenregeln (Typ 6):**
1. SV = die Punkte beider Klassen, die der Trennlinie am nächsten liegen (meist 2–3 Stück)
2. Trennlinie mittig zwischen den SV, Margin symmetrisch
3. Nicht-SV dürfen sich bewegen/entfallen — Ebene bleibt; entfernt man einen **SV**, ändert sie sich

**Soft Margin / Straffaktor C (Folie 10):**
- Schlupfvariablen ξᵢ erlauben Punkte im Margin / auf der falschen Seite; C = Strafgewicht dafür
- **C groß → wenig Verletzungen erlaubt, schmaler Margin** (Tendenz Overfitting); **C klein → mehr Verletzungen, breiter Margin** (robuster)
- **Typ 6b („C wird reduziert"):** 1. Ausreißer-SV darf **in die Margin / auf die falsche Seite** rutschen. 2. Ebene richtet sich nach der **Masse** → breiterer Margin, **robuster**. 3. **C zu klein ⇒ Lage beliebig, viele Fehlklassifikationen** (Underfitting)
- C in logarithmischen Intervallen testen
- Alternative ν-SVM: ν ∈ (0;1] = untere Schranke für Anteil der SV, obere Schranke für Margin-Verletzer (intuitiver als C)

**Kernel-Trick (Folien 15–27):**
- **Welche Rechnung?** Beide: **duales Problem** (Training, Skalarprodukt xᵢ·xⱼ zweier Trainingspunkte) und **Entscheidungsfunktion** (Anwendung, x·xᵢ = neuer Punkt mit jedem SV)
- Beide brauchen die Daten **nur als Skalarprodukte**, nie die Koordinaten selbst → jedes Skalarprodukt wird k(·,·). Dass w herausfällt, ist die Folge, nicht der Ort
- → implizite Transformation in höherdim. Raum, ohne ihn zu berechnen; dort linear = nichtlinear im Original
- Kernels: **linear**, **polynomial** (erst Skalarprodukt, dann potenzieren), **RBF/Gauß** (über den **Abstand** — nicht verwechseln!)
- **RBF:** Ähnlichkeit zweier Punkte über ihren **Abstand** (Gauß-Glocke: 1 bei a = b, fällt gegen 0). Legt **jeden** Punkt auf die **Einheitskugel in ∞ Dim** ⇒ Abstand 1 vom Ursprung — Basis der OCSVM
- **γ groß** → schmale Glocke ⇒ Grenze zerfällt in **Inseln** (Overfitting); **γ klein** → glatte, fast kreisförmige Grenze, schließt Leerraum ein (Underfitting). Log. testen, alt. `gamma='scale'`

**SVM-Eigenschaften (Folie 30, für Verfahrenswahl):**
+ stark bei wenig Trainingsdaten, eindeutige globale Lösung, robust ggü. Rauschen, gut bei hohen Dimensionen (sogar dim > n), schnelle Klassifikation, wenig Speicher
− Training langsam, Metaparameter unintuitiv, Probleme bei starker Klassenüberlappung, **Skalierung essenziell (v. a. RBF → Standardisierung!)**
- sklearn: `sklearn.svm.SVC`, `NuSVC`

## OCSVM (Folie 31) — Typ 7

- Problem: nur EINE Klasse (Normaldaten) → keine zweite Klasse für Margin
- **Idee: Trenne Normaldaten vom URSPRUNG, maximiere Abstand der Ebene zum Ursprung**

**Warum Kernel-Trick nötig? (Aufg. 6d + 7c — in 4 Schritten:)**
1. Keine zweite Klasse ⇒ Trennung **vom Ursprung**.
2. **Linear wertlos:** eine Ebene halbiert nur den Raum — jenseits der Wolke gilt alles weiter als **normal**, die Daten werden nicht umschlossen.
3. **RBF legt alles auf die Einheitskugel.** Erst dort ist „max. Ursprungsabstand" sinnvoll: Ebene schneidet die **Kappe** mit den dichten Normaldaten heraus.
4. Im Originalraum ⇒ **geschlossene, krumme Grenze**, bei passendem γ auch **Inseln**.
- Ohne Trick **unmöglich** (nicht nur teurer): φ_RBF hat unendlich viele Komponenten

**Zeichenregeln (Typ 7):**
1. **Linear:** Gerade **vom Ursprung weg** schieben, bis sie an den **ursprungsnächsten** Punkten anliegt = SV. **Normaldaten ursprungsfern, Anomalien ursprungsseitig**
2. ν sehr klein (0,001) ⇒ auch der ursprungsnächste **Ausreißer** muss mit hinein → Gerade weit rausgedrückt
3. **RBF:** geschlossene, krumme Grenze **um die Wolke**; liegt umso enger an, je passender ν

- Metaparameter: **ν = Anteil erlaubter Ausreißer in den Normaldaten** (steuert, wie eng die Grenze anliegt); **γ = Einfluss der Nachbarschaft** (Form der Grenze)
- **Typ 7b (ν):** **zu klein** → Ausreißer mit eingeschlossen, Normalbereich zu groß = **Overfitting**. **passend** → Ausreißer draußen, Grenze eng an der Wolke. **zu groß** (0,5) → halbe Wolke fälschlich als Anomalie = **Underfitting**
- ν = **untere** Schranke SV-Anteil, **obere** Schranke Verletzer
- **Typ 8/12:** OCSVM+RBF beschreibt auch **mehrere Cluster als Inseln** ⇒ gut bei mehrmodalen Normaldaten; Mahalanobis/EE (eine Ellipse) deckt den Leerraum dazwischen mit ab
- γ-Wirkung auf die Grenze und `gamma='scale'` → siehe **Kernel-Trick-Block oben**
- sklearn: `sklearn.svm.OneClassSVM`
- **SVDD** (Folie 35): findet die **kleinste Kugel** (Radius R, Zentrum c), die die Normaldaten umschließt; ν erlaubt wieder Ausreißer. **Mit Gauß-Kernel: SVDD ≡ OCSVM**

## Deep SVDD (Folien 40–52) — Verbotsliste! (Typ 10)

**Ziel:** Netz φ(x) bildet Normaldaten in eine Kugel (c, R) mit minimalem Volumen ab.
**Loss = mittlerer quadratischer Abstand zu c** (+ Weight Decay λ).

**⚠ Verbotsliste — jede Verletzung ermöglicht die TRIVIALE LÖSUNG (Netz kollabiert alles auf einen Punkt, R=0, Kosten 0, nutzlos):**
| Verbot | Warum |
|---|---|
| **c darf NICHT mitoptimiert werden / c ≠ 0** | sonst c=0 + Nullgewichte → φ(x)=0 ∀x. Lösung: c = Mittel der Abbildungen mit initialen Gewichten VOR dem Training, danach fix; Komponenten nahe 0 auf ±ε (0,1) setzen |
| **Keine Biases** (`use_bias=False` überall) | Nullgewichte + Biases → φ(x)=c ∀x konstant |
| **Keine beschränkten („gedeckelten") Aktivierungen** (kein Sigmoid/tanh) → ReLU/LeakyReLU | gesättigte Aktivierung ≈ konstante 1 → wirkt wie Bias |
| **BatchNorm ist KEIN Fehler** | steht in Aufg. 10.2 drin und gilt dort als „Netz in Ordnung"; Paulus nutzt sie auch im Praktikum. Nicht anstreichen! |

**Alle drei durchgehen:** (1) `use_bias` in **jeder** Schicht (fehlt es, ist Default `True` = Fehler!), (2) Aktivierungen auf Sigmoid/tanh, (3) `transform_center` — außerhalb des Trainings und ≠ 0? **Ein Ausschnitt kann mehrere Fehler haben**; „alles korrekt" ist eine zulässige Antwort.

**Ablauf:**
1. **Vortraining als Autoencoder** (Encoder = Deep-SVDD-Netz + Wegwerf-Decoder, MSE-Loss)
   – **Ohne Vor-Training?** Zwei Wege, den Loss klein zu machen: (a) gute Merkmale lernen, (b) alles auf einen Punkt legen. (b) ist leichter, denn der Loss misst nur den **Abstand zu c** — nicht, ob die Abbildung noch etwas über das Bild aussagt. Also klumpen Normaldaten **und** Anomalien zusammen: alle Scores gleich, **AUC ≈ 0,5**. Der AE-Loss verlangt, das Bild **zurückzubauen** — konstant geht das nicht.
     (Bias/Sigmoid/c ≠ 0 verbieten nur „**exakt** auf c", fast konstant bleibt erlaubt.)
   – **Decoder, `Dense`→`Reshape`:** muss nur die **Auflösung** treffen (7×7, damit 2× Upsampling wieder 28 gibt); die **Kanalzahl ist frei** (Praktikum: 7·7·2 statt 7·7·4), weil die nächste `Conv2DTranspose` sie neu setzt. Exakt die letzte Encoder-Shape nur, wenn die Aufgabe „spiegeln" verlangt (Orig.-Aufg. 3).
2. Decoder verwerfen; c = Mittel der Encodierungen (get_center)
3. Encoder als Deep SVDD trainieren: Loss = mittlerer quadrat. Abstand zu c
4. **Radius NACH dem Training**: R = **(1 − ν)-Quantil** der Abstände zu c → `np.quantile(np.sqrt(dists), 1-nu)` (ν = erlaubter Ausreißeranteil)
   – **Warum kommt R im Loss nicht vor?** Der Loss zieht alle Normaldaten so nah wie möglich an c; R ist danach nur das Quantil genau dieser Abstände ⇒ kleine Abstände = kleines R = **minimales Kugelvolumen**. (Der Weight Decay ist nur Regularisierung, kein Volumen-Argument.)

**Score & Klassifikation:** score(x) = ‖φ(x) − c‖² − R² → **negativ = in Kugel = normal; positiv = Anomalie** (sgn)

## GOAD (Folien 55–60)

- **Selbstüberwacht:** Hilfsaufgabe „Welche Transformation wurde angewendet?" liefert Pseudo-Labels
- Bilder: Rotation (4) × Translation (9) × Spiegelung (2) = **M = 72 Transformationen** (inkl. Identität); allgemeine Daten: **zufällige affine Transformationen** Ax+b (Anzahl = Metaparameter, mehr = stabiler)
- Netz f bildet jede transformierte Version in Latent Space; Ziel: **pro Transformation ein dichtes Cluster** (Zentren cⱼ = Mittel)
- **Triplet Center Loss**: Abstand zum **eigenen** Zentrum klein, zum nächsten **fremden** groß (Marge s ≈ 1). Gesamtloss = Kreuzentropie „welche Transformation?" (Stabilisierung) + λ₁·L_tc + λ₂·L2-Norm der **Latent-Vektoren z** (kein Weight Decay!) — **λ₁ = 0,1; λ₂ = 10**
- **Score(x) = −Σⱼ log P(Tⱼ | Tⱼ(x))** — landet jede transformierte Version im richtigen Cluster? Niedrige P → hoher Score → Anomalie

**Die drei Warum-Fragen:**
- **Warum Transformationen?** Sie **erzeugen die Labels** (man hat nur Normaldaten, sonst kein Lernsignal) und machen aus **einer** Kugel **M Cluster**.
- **Warum die Transformations-Vorhersage?** Der Triplet Center Loss ist **pro Batch instabil** (Zentren aus dem Batch geschätzt, schwanken) ⇒ Kreuzentropie **stabilisiert**. Nebeneffekt: eine konstante Abbildung kann die Transformationen nicht unterscheiden ⇒ **triviale Lösung ausgeschlossen**.
- **Warum dichte, getrennte Cluster?** Der Score misst **Abstände zu den Zentren** — überlappende Cluster ⇒ nichtssagende P ⇒ unbrauchbarer Score.

**GOAD vs. Deep SVDD (Typ-10-Vergleichsfrage):**
| | Deep SVDD | GOAD |
|---|---|---|
| Normaldaten | **eine** Kugel (c, R) | **M Cluster**, eines je Transformation |
| Lernsignal | nur Abstand zu c ⇒ braucht **AE-Vortraining** | selbstüberwachte **Hilfsaufgabe** |
| Triviale Lösung | nur per **Verbotsliste** verhindert | durch die Klassifikation ausgeschlossen |
| Score | ‖φ(x)−c‖² − R² | Summe der neg. Log-Wahrscheinlichkeiten |

## CutPaste (Folien 62–65)

- Für **kleine, lokale Defekte** (Kratzer in Fertigung) — bisherige Verfahren sehen eher globale Anomalien
- Selbstüberwacht mit Pseudo-Anomalien: Rechteck aus dem Bild kopieren + woanders einfügen
- 3 Klassen: **unverändert / normales CutPaste / CutPaste Scar** (sehr klein + dünn)
- Nach Training: Klassifikationsschicht abschneiden → CNN = Merkmalsextraktor f
- Score = Gauß-Dichte im Merkmalsraum, μ/Σ aus Normaldaten — also **Mahalanobis auf f(x)** (vgl. Elliptic Envelope)
