# Blatt ④ — SVM, OCSVM, Deep SVDD, GOAD, CutPaste, Contrastive (Kap. 8 + 8a)

> Vorlage zum handschriftlichen Übertragen. Quellen: Foliensatz 08 + 08a.
> Deckt Aufgabentypen 6/7 (SVM/OCSVM zeichnen) + 10 (Deep-SVDD-Code beurteilen) ab. Zielumfang: ~2,5 A4-Seiten.

---

## SVM überwacht (Folien 5–30) — fürs Zeichnen (Typ 6)

- Trennebene h₀ in der Mitte, Parallelebenen h₁/h₂ durch die nächsten Punkte
- **Optimale Ebene = maximaler Abstand (Margin) zu den nächsten Punkten beider Klassen = Support Vektoren**; Ebene hängt NUR von den SV ab
- **Margin = der Streifen zwischen h₁ und h₂.** Die ±1 auf h₁/h₂ sind nur eine **Normierung** (w, b sind frei skalierbar) ⇒ Streifenbreite = 2/‖w‖
- Margin = 2/‖w‖ ⇒ **Margin maximieren = ‖w‖ minimieren**
- **Nebenbedingung = „kein Trainingspunkt zwischen h₁ und h₂", jeder auf seiner Seite.** Sie fesselt die Ebene an die Daten — ohne sie wäre w = 0 die Lösung (Ebene weg, Kosten 0). Gleiches Muster wie die triviale Lösung bei Deep SVDD

**Zeichenregeln (Typ 6):**
1. SV = die Punkte beider Klassen, die der Trennlinie am nächsten liegen (meist 2–3 Stück)
2. Trennlinie mittig zwischen den SV, Margin symmetrisch
3. Punkte, die keine SV sind, dürfen sich bewegen/entfallen ohne Änderung der Ebene
4. Entfernt man einen SV → Ebene ändert sich!

**Soft Margin / Straffaktor C (Folie 10):**
- Schlupfvariablen ξᵢ erlauben Punkte im Margin / auf der falschen Seite; C = Strafgewicht dafür
- **C groß → wenig Verletzungen erlaubt, schmaler Margin** (Tendenz Overfitting); **C klein → mehr Verletzungen, breiter Margin** (robuster)
- **Antwortmuster Typ 6b („C wird schrittweise reduziert"):** 1. Ist ein SV ein **Ausreißer**, darf er bei kleinerem C **in die Margin oder auf die falsche Seite** rutschen. 2. Die Ebene richtet sich dann nach der **Masse** der Punkte → größerer Abstand zu beiden Klassen, **robustere** Klassifikation. 3. **C zu klein ⇒ die Lage der Trenngeraden wird beliebig, es kommt zu vielen Fehlklassifikationen** (Underfitting)
- C in logarithmischen Intervallen testen
- Alternative ν-SVM: ν ∈ (0;1] = untere Schranke für Anteil der SV, obere Schranke für Margin-Verletzer (intuitiver als C)

**Kernel-Trick (Folien 15–27):**
- Die Rechnung braucht die Daten nur als **Skalarprodukte** → ersetzbar durch einen Kernel
- **Wo genau?** Im **dualen Optimierungsproblem** und in der **Entscheidungsfunktion** — dort stehen die Trainingspunkte nur noch in Skalarprodukten, jedes davon wird durch k(·,·) ersetzt. Dass w herausfällt, ist die Folge davon, nicht der Ort
- → implizite Transformation in höherdimensionalen Raum, ohne ihn je zu berechnen; linear dort = nichtlinear im Original
- Kernels: **linear**, **polynomial**, **RBF/Gauß** (Kurs-Standard)
- **RBF (Kurs-Standard):** misst die **Ähnlichkeit zweier Punkte über ihren Abstand** — Gauß-Glocke, 1 bei a = b, fällt gegen 0. Seine Transformation legt **jeden** Punkt auf eine **Einheitskugel in ∞ Dimensionen**, d. h. jeder Punkt hat dort **Abstand 1 vom Ursprung** — genau darauf baut die OCSVM auf (s. u.)
- **γ groß → schmale Glocke, enge Anpassung** ⇒ Grenze zerfällt in **Inseln** um einzelne Punkte (Overfitting); **γ klein → glatter** ⇒ glatte, fast kreisförmige Grenze, die leere Bereiche mit einschließt (Underfitting). Logarithmisch testen, Alternative `gamma='scale'`

**SVM-Eigenschaften (Folie 30, für Verfahrenswahl):**
+ stark bei wenig Trainingsdaten, eindeutige globale Lösung, robust ggü. Rauschen, gut bei hohen Dimensionen (sogar dim > n), schnelle Klassifikation, wenig Speicher
− Training langsam, Metaparameter unintuitiv, Probleme bei starker Klassenüberlappung, **Skalierung essenziell (v. a. RBF → Standardisierung!)**
- sklearn: `sklearn.svm.SVC`, `NuSVC`

## OCSVM (Folie 31) — Typ 7

- Problem: nur EINE Klasse (Normaldaten) → keine zweite Klasse für Margin
- **Idee: Trenne Normaldaten vom URSPRUNG, maximiere Abstand der Ebene zum Ursprung**
**Warum ist der Kernel-Trick für die OCSVM nötig? (Klausur-Klassiker — Aufg. 6d UND 7c, in vier Schritten schreiben:)**
1. Die OCSVM hat keine zweite Klasse, sie trennt die Normaldaten **vom Ursprung**.
2. **Linear ist das fast wertlos:** eine Ebene teilt den Raum nur in zwei Hälften — als Anomalie gilt dann alles auf der **Ursprungsseite**, aber alles jenseits der Wolke (noch weiter vom Ursprung weg) gilt als **normal**. Die Normaldaten werden nicht umschlossen.
3. **Der RBF-Kernel legt alle Punkte auf die Einheitskugel** (Abstand 1 vom Ursprung). **Erst dort** ist „maximaler Abstand zum Ursprung" sinnvoll: die Ebene schneidet die **Kappe** heraus, auf der die Normaldaten dicht liegen.
4. Zurück im Originalraum wird aus diesem linearen Schnitt eine **geschlossene, krumme Grenze um die Wolke** — bei passendem γ auch mehrere **Inseln**.
- Zusatz: Ohne Trick nicht nur teurer, sondern **unmöglich** — die RBF-Transformation hat unendlich viele Komponenten, man könnte sie gar nicht hinschreiben.

**Zeichenregeln (Typ 7):**
1. **Linearer Kernel:** Gerade so weit wie möglich **vom Ursprung weg** schieben, bis sie an den **ursprungsnächsten** Normalpunkten anliegt — das sind die SV. **Normaldaten auf der ursprungsfernen Seite, Anomalien auf der Ursprungsseite.**
2. Bei sehr kleinem ν (z. B. 0,001) muss auch der ursprungsnächste **Ausreißer** noch mit hinein → Gerade wird weit nach unten/links gedrückt
3. **RBF-Kernel:** geschlossene, krumme Grenze **um die Wolke herum**; sie liegt umso enger an, je passender ν ist

- Metaparameter: **ν = Anteil erlaubter Ausreißer in den Normaldaten** (steuert, wie eng die Grenze anliegt); **γ = Einfluss der Nachbarschaft** (Form der Grenze)
- **Antwortmuster Typ 7b („ν wird optimal angepasst / ist zu groß"):** ν **zu klein** → die Ausreißer werden mit eingeschlossen, der Normalbereich wird unnötig groß → **Overfitting**. ν **passend** → die paar Ausreißer bleiben draußen, die Grenze liegt eng an der Wolke. ν **zu groß** (z. B. 0,5) → es werden Punkte als Ausreißer abgeschnitten, die keine sind, die Punktwolke wird etwa **halbiert** → **Underfitting**
- **γ zu groß** → Grenze zerfällt in **Inseln** um einzelne Punkte (Overfitting); **γ zu klein** → sehr glatte, fast kreisförmige Grenze, die leere Bereiche mit einschließt
- **Stärke für die Verfahrenswahl (Typ 8/12):** Mit RBF und passendem γ beschreibt die OCSVM auch **mehrere getrennte Cluster als Inseln** — deshalb geeignet bei mehrmodalen Normaldaten, wo Mahalanobis/Elliptic Envelope (eine Ellipse) den leeren Bereich dazwischen mit abdecken würden. Steht so in der Musterlösung zu Original-Aufg. 8
- **γ-Default in sklearn:** `gamma='scale'` = 1/(Anzahl Merkmale · Varianz der Daten) — die Alternative zur logarithmischen Suche (Folie 22)
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
| BatchNorm kritisch prüfen | der lernbare Shift β wirkt wie ein Bias (in Übungsaufgaben als Fehler gewertet) |

**Ablauf:**
1. **Vortraining als Autoencoder** (Encoder = Deep-SVDD-Netz + Wegwerf-Decoder, MSE-Loss)
2. Decoder verwerfen; c = Mittel der Encodierungen (get_center)
3. Encoder als Deep SVDD trainieren: Loss = mittlerer quadrat. Abstand zu c
4. **Radius NACH dem Training**: R = (1−ν)-Quantil der Abstände: `np.quantile(np.sqrt(dists), 1-nu)` (ν = erlaubter Ausreißeranteil)

**Score & Klassifikation:** score(x) = ‖φ(x) − c‖² − R² → **negativ = in Kugel = normal; positiv = Anomalie** (sgn)

## GOAD (Folien 55–60)

- **Selbstüberwacht:** Hilfsaufgabe „Welche Transformation wurde angewendet?" liefert Pseudo-Labels
- Bilder: Rotation (4) × Translation (9) × Spiegelung (2) = **M = 72 Transformationen** (inkl. Identität); allgemeine Daten: **zufällige affine Transformationen** Ax+b (Anzahl = Metaparameter, mehr = stabiler)
- Netz f bildet jede transformierte Version in Latent Space; Ziel: **pro Transformation ein dichtes Cluster** (Zentren cⱼ = Mittel)
- **Triplet Center Loss**: Abstand zum **eigenen** Zentrum klein, zum nächsten **fremden** groß (Marge s ≈ 1). Dazu Kreuzentropie „welche Transformation?" als Stabilisierung + Weight Decay — **λ₁ = 0,1; λ₂ = 10**
- **Score(x) = −Σⱼ log P(Tⱼ | Tⱼ(x))** — landet jede transformierte Version im richtigen Cluster? Niedrige P → hoher Score → Anomalie

## CutPaste (Folien 62–65)

- Für **kleine, lokale Defekte** (Kratzer in Fertigung) — bisherige Verfahren sehen eher globale Anomalien
- Selbstüberwacht mit Pseudo-Anomalien: Rechteck aus dem Bild kopieren + woanders einfügen
- 3 Klassen: **unverändert / normales CutPaste / CutPaste Scar** (sehr klein + dünn)
- Nach Training: Klassifikationsschicht abschneiden → CNN = Merkmalsextraktor f
- Score = Gauß-Dichte im Merkmalsraum, μ/Σ aus Normaldaten — also **Mahalanobis auf f(x)** (vgl. Elliptic Envelope)

## Contrastive Learning / SimCLR (Foliensatz 08a)

- Contrastive: Encoder lernt, ähnliche von unähnlichen Samples zu trennen; Ähnlichkeitsmaß = **Cosinus-Ähnlichkeit**; Contrastive Loss mit **Temperaturfaktor τ**
- SimCLR: positive Paare = 2 Augmentierungen desselben Bilds (t, t′ aus 𝒯), negative = alle anderen; Architektur: f(·) (z. B. ResNet ohne finale Schicht) → h, dann Projektionskopf g(·) (FC+ReLU, dann lineare FC) → z; optimiere f und g
