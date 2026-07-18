# Blatt ④ — SVM, OCSVM, Deep SVDD, GOAD, CutPaste, Contrastive (Kap. 8 + 8a)

> Vorlage zum handschriftlichen Übertragen. Quellen: Foliensatz 08 + 08a.
> Deckt Aufgabentypen 6/7 (SVM/OCSVM zeichnen) + 10 (Deep-SVDD-Code beurteilen) ab. Zielumfang: ~2,5 A4-Seiten.

---

## SVM überwacht (Folien 5–30) — fürs Zeichnen (Typ 6)

- Hyperebene h₀: wᵀx + b = 0; Parallelebenen h₁/h₂: wᵀx + b = ±1
- **Optimale Ebene = maximaler Abstand (Margin) zu den nächsten Punkten beider Klassen = Support Vektoren**; Ebene hängt NUR von den SV ab
- Margin zwischen h₁ und h₂ = 2/‖w‖ → min ½‖w‖² unter yᵢ(wᵀxᵢ + b) ≥ 1
- Klassifikation: y = sgn(wᵀx − d) bzw. f(x) = sgn(Σ yᵢαᵢ·k(x, xᵢ) + b), Summe nur über SV

**Zeichenregeln (Typ 6):**
1. SV = die Punkte beider Klassen, die der Trennlinie am nächsten liegen (meist 2–3 Stück)
2. Trennlinie mittig zwischen den SV, Margin symmetrisch
3. Punkte, die keine SV sind, dürfen sich bewegen/entfallen ohne Änderung der Ebene
4. Entfernt man einen SV → Ebene ändert sich!

**Soft Margin / Straffaktor C (Folie 10):**
- Schlupfvariablen ξᵢ erlauben Verletzungen: yᵢ(wᵀxᵢ+b) ≥ 1 − ξᵢ; L = ½‖w‖² + C·Σξᵢ
- **C groß → wenig Verletzungen erlaubt, schmaler Margin** (Tendenz Overfitting); **C klein → mehr Verletzungen, breiter Margin** (robuster)
- C in logarithmischen Intervallen testen
- Alternative ν-SVM: ν ∈ (0;1] = untere Schranke für Anteil der SV, obere Schranke für Margin-Verletzer (intuitiver als C)

**Kernel-Trick (Folien 15–27):**
- Duales Problem enthält Daten NUR als Skalarprodukte xᵢᵀxⱼ → ersetze durch Kernel k(a,b) = φ(a)ᵀφ(b)
- → implizite Transformation in höherdimensionalen Raum, ohne ihn je zu berechnen; linear dort = nichtlinear im Original
- Kernels: **linear** aᵀb; **polynomial** (c + aᵀb)^p; **RBF/Gauß** e^(−γ‖a−b‖²)
- RBF: bildet auf Einheitskugel in ∞ Dimensionen ab (‖φ(x)‖ = 1); **γ groß → schmale Glocke, enge Anpassung; γ klein → glatter**
- γ logarithmisch testen oder γ = 1/(dim·var(X))

**SVM-Eigenschaften (Folie 30, für Verfahrenswahl):**
+ stark bei wenig Trainingsdaten, eindeutige globale Lösung, robust ggü. Rauschen, gut bei hohen Dimensionen (sogar dim > n), schnelle Klassifikation, wenig Speicher
− Training langsam, Metaparameter unintuitiv, Probleme bei starker Klassenüberlappung, **Skalierung essenziell (v. a. RBF → Standardisierung!)**
- sklearn: `sklearn.svm.SVC`, `NuSVC`

## OCSVM (Folie 31) — Typ 7

- Problem: nur EINE Klasse (Normaldaten) → keine zweite Klasse für Margin
- **Idee: Trenne Normaldaten vom URSPRUNG, maximiere Abstand der Ebene zum Ursprung**
- **Warum Kernel (RBF) nötig?** Linear: Anomalien dürften nur auf der Ursprungsseite liegen — meist unbrauchbar. Mit RBF liegen alle Daten auf der Einheitskugel → Ebene „schneidet" den dichten Normaldaten-Bereich heraus (Klausur-Klassiker!)
- Metaparameter: **ν = Anteil erlaubter Ausreißer in den Normaldaten** (steuert, wie eng die Grenze anliegt); **γ = Einfluss der Nachbarschaft** (Form der Grenze)
- sklearn: `sklearn.svm.OneClassSVM`
- **SVDD** (Folie 35): findet **Kugel** (Radius R, Zentrum c), die Normaldaten umschließt: min R² + 1/(νn)·Σξᵢ mit ‖xᵢ−c‖² ≤ R² + ξᵢ. **Mit Gauß-Kernel: SVDD ≡ OCSVM**

## Deep SVDD (Folien 40–52) — Verbotsliste! (Typ 10)

**Ziel:** Netz φ(·; W) bildet Normaldaten in Kugel (c, R) mit minimalem Volumen ab.
Vereinfachte Zielfunktion: min_W 1/n·Σ ‖φ(xᵢ;W) − c‖² + λ/2·Σ‖Wˡ‖²

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
- **Triplet Center Loss**: max(0, ‖f(Tⱼx)−cⱼ‖² + s − min_{k≠j} ‖f(Tⱼx)−cₖ‖²) → Intra-Abstand klein, Inter-Abstand groß (s ≈ 1)
- Gesamt: L = L_ce (Kreuzentropie „welche Transformation?" als Stabilisierung) + λ₁·L_tc + λ₂/N·Σ‖zᵢ‖² — Standardwerte **λ₁ = 0,1; λ₂ = 10**
- **Score(x) = −Σⱼ log P(Tⱼ | Tⱼ(x))** — Wahrscheinlichkeit, dass jede transformierte Version im richtigen Cluster landet; ε als Regularisierung. Niedrige P → hoher Score → Anomalie

## CutPaste (Folien 62–65)

- Für **kleine, lokale Defekte** (Kratzer in Fertigung) — bisherige Verfahren sehen eher globale Anomalien
- Selbstüberwacht mit Pseudo-Anomalien: Rechteck aus dem Bild kopieren + woanders einfügen
- 3 Klassen: **unverändert / normales CutPaste / CutPaste Scar** (sehr klein + dünn)
- Nach Training: Klassifikationsschicht abschneiden → CNN = Merkmalsextraktor f
- Score = Gauß-Dichte im Merkmalsraum: log p ∝ −½(f(x)−μ)ᵀΣ⁻¹(f(x)−μ), μ/Σ aus Normaldaten (vgl. Mahalanobis/Elliptic Envelope!)

## Contrastive Learning / SimCLR (Foliensatz 08a)

- Contrastive: Encoder lernt, ähnliche von unähnlichen Samples zu trennen; **Cosinus-Ähnlichkeit** sim(v,v′) = vᵀv′/(‖v‖‖v′‖); Contrastive Loss mit **Temperaturfaktor τ**
- SimCLR: positive Paare = 2 Augmentierungen desselben Bilds (t, t′ aus 𝒯), negative = alle anderen; Architektur: f(·) (z. B. ResNet ohne finale Schicht) → h, dann Projektionskopf g(·) (FC+ReLU, dann lineare FC) → z; optimiere f und g
