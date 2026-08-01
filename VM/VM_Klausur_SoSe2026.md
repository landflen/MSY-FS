# VM — Klausur SoSe 2026 im Original, mit Musterlösung

> **Quelle:** Fotos der Original-Klausur **samt gedruckter Musterlösung**, aufgenommen bei der
> Einsichtnahme am 20.07.2026, geteilt in der Gruppe „efi Master".
> Bilder: `Klausur_SoSe2026/` (6 Fotos, je eine Doppelseite).
> Das ist **harte Evidenz**, kein Gedächtnisprotokoll — im Gegensatz zu
> `VM_Klausurinfos_Kommilitonen.md`, wo das Drumherum aus dem Chat steht.

## Deckblatt — Rahmen und Hilfsmittel

| | |
|---|---|
| Prüfungsfach | Vertiefungsgebiete der Mathematik |
| Studiengang | M-SY |
| Prüfer | J. Bolik |
| Termin | 10.07.2026, 11:00 Uhr, KA.034 + BB.103 |
| Dauer | **90 Minuten** |
| Aufgabensatz | Deckblatt + **Tabellenblatt** + 10 Aufgabenblätter |
| Gesamtpunktzahl | **90** |
| Bestehensgrenze | **32 von 90 = 35,6 %** (Angabe aus der Gruppe) |

**Hilfsmittel (wörtlich vom Deckblatt):**
- Taschenrechner
- Wörterbuch Muttersprache / Deutsch
- **Selbstgefertigte Arbeitsunterlagen (10 Seiten DIN A4)**
- **Mathematische Formelsammlung**

→ Das ist **keine Open-Book-Klausur**, aber du darfst 10 selbstgeschriebene Seiten plus eine
gedruckte Formelsammlung (Papula/Binomi) mitnehmen. Die 10 Seiten sind der eigentliche Hebel.
Ansage aus Boliks Klausurvorbereitung dazu: *„In Papula nicht zu viel reinschreiben, lieber
gelbe Zettel."*

⚠️ **Das Tabellenblatt ist Teil des Aufgabensatzes.** In Aufgabe 2 stand ausdrücklich:
*„Verwenden Sie für Ihre Laplace-Transformation lediglich solche Transformationsfunktionen,
die das beigefügte Tabellenblatt enthält."* Eine Korrespondenz aus Papula, die dort nicht steht,
ist also nicht zulässig.

## Punkteverteilung — exakt 50/50

| Aufgabe | Thema | Punkte |
|---|---|---|
| 1 | Eigenwerte, Diagonalisierung, DGL-System über Matrixexponential | 11 |
| 2 | **Laplace-Transformation** eines DGL-Systems, PBZ + Faltungssatz | **19** |
| 3 | Nichtlineare DGL: System 1. Ordnung, Gleichgewichtspunkt, Jacobi, **Lyapunov** | 15 |
| 4 | Bedingte Wahrscheinlichkeit, totale Wahrscheinlichkeit, **Bayes** | 12 |
| 5 | **Poisson + Binomialverteilung** | 18 |
| 6 | **Markov-Kette**: Übergangsmatrix, stationäre Verteilung, Grenzwert | 15 |
| | **Summe** | **90** |

**Struktureller Kernbefund:** Aufgaben 1–3 = **45 Punkte Analysis/LinAlg/DGL**,
Aufgaben 4–6 = **45 Punkte Stochastik**. Die Klausur ist exakt hälftig geteilt.
Wer nur einen der beiden Blöcke kann, kommt rechnerisch auf maximal 45 von 90 — das reicht zwar
für die 32er-Grenze, aber ohne jeden Puffer. **Beide Hälften müssen sitzen.**

---

## Aufgabe 1 — Diagonalisierung + DGL-System (11 P)

Homogenes System y′ = A·y mit **A = [[−1, 6], [−1, 4]]**

- **a) (6 P)** Matrix C bestimmen, sodass C⁻¹AC eine Diagonalmatrix ergibt.
- **b) (5 P)** Das DGL-System mit dieser Matrix C lösen (Matrixexponentialfunktion **oder ein
  anderes Verfahren** — hier war der Weg ausnahmsweise freigestellt).

**Lösungsweg:**
det(A − λE) = (−1−λ)(4−λ) + 6 = λ² − 3λ + 2 = (λ−1)(λ−2) ⇒ λ₁ = 1, λ₂ = 2 ⇒ diagonalisierbar.
Eigenvektoren: zu λ₁ = 1 → μ·(3, 1)ᵀ, zu λ₂ = 2 → μ·(2, 1)ᵀ ⇒ **C = [[3, 2], [1, 1]]**, C⁻¹ = [[1, −2], [−1, 3]].

exp(Ax) = C · diag(eˣ, e²ˣ) · C⁻¹ = [[3eˣ − 2e²ˣ, −6eˣ + 6e²ˣ], [eˣ − e²ˣ, −2eˣ + 3e²ˣ]],
allgemeine Lösung y(x) = exp(Ax)·y₀.
Die Musterlösung nennt als gleichwertige Schreibweise
y(x) = C · (c₁eˣ, c₂e²ˣ)ᵀ mit c₁ = y₀,₁ − 2y₀,₂ und c₂ = −y₀,₁ + 3y₀,₂.

> 🔴 **Genau hier ist jemandem der Fehler passiert, der im Chat berichtet wurde:
> die Diagonalisierungsmatrix C statt der Diagonalmatrix angegeben.** Die Frage lautet
> „bestimmen Sie **C**, sodass C⁻¹AC diagonal ist" — gefragt ist also **C**, nicht das Ergebnis
> C⁻¹AC. Beim Lesen genau trennen, was gesucht ist.

## Aufgabe 2 — Laplace-Transformation (19 P) ⭐ größte Aufgabe

Für t ≥ 0 die Lösung des Systems bestimmen:
- x′(t) − 3x(t) − 3y(t) = t
- y′(t) + x(t) + y(t) = 1
- mit x(0) = 0 und y(0) = 0

**Vorgeschriebener Weg (steht in der Aufgabenstellung):** einzelne Rechenschritte angeben ·
nur Korrespondenzen vom beigefügten Tabellenblatt · *Hinweis: Partialbruchzerlegung für
sX(s) und sY(s) durchführen und dann den Faltungssatz verwenden.*

**Lösungsweg:**
Transformiert: (s−3)X − 3Y = 1/s² und X + (s+1)Y = 1/s.
Auflösen ⇒ X = (1/s)·(4s+1)/(s²(s−2)) und Y = (1/s)·(s²−3s−1)/(s²(s−2)).

Partialbruchzerlegung:
(4s+1)/(s²(s−2)) = −9/4·(1/s) − 1/2·(1/s²) + 9/4·(1/(s−2))
(s²−3s−1)/(s²(s−2)) = 7/4·(1/s) + 1/2·(1/s²) − 3/4·(1/(s−2))

Rücktransformation ⇒ −9/4 − (1/2)t + (9/4)e²ᵗ bzw. 7/4 + (1/2)t − (3/4)e²ᵗ.
Der Faktor 1/s davor wird über den **Faltungssatz** zur Integration von 0 bis t:

- x(t) = ∫₀ᵗ (−9/4 − τ/2 + (9/4)e²ᵗ) dτ = **(1/8)·(−9 − 18t − 2t² + 9e²ᵗ)**
- y(t) = ∫₀ᵗ (7/4 + τ/2 − (3/4)e²ᵗ) dτ = **(1/8)·(3 + 14t + 2t² − 3e²ᵗ)**

> **Das ist die Aufgabe, die im Chat als „Falle" bezeichnet wurde** — 19 Punkte, viel Rechnung,
> und laut Bericht nur eine halbe Seite Platz. Der Trick ist, den Faktor 1/s **nicht** in die
> Partialbruchzerlegung hineinzuziehen, sondern ihn als Faltung mit 1 (= Integration) stehen zu
> lassen. Genau das schreibt der Hinweis vor.

## Aufgabe 3 — Nichtlineare DGL mit Lyapunov (15 P)

Gegeben: **m·x″(t) = −a·x′(t)·|x′(t)| − (b·x + c·x³)** mit a, b, c positiven reellen Konstanten
(gedämpfter nichtlinearer Schwinger mit quadratischer Dämpfung und kubischer Federkennlinie).

- **a) (3 P)** In ein DGL-System erster Ordnung umformen:
  x₁′ = x₂ · x₂′ = −(a/m)·x₂|x₂| − (b/m)·x₁ − (c/m)·x₁³
- **b) (2 P)** Gleichgewichtspunkt(e): aus x₂ = 0 und 0 = x₁·(b/m + (c/m)x₁²) folgt x₁ = 0
  ⇒ **einziger Gleichgewichtspunkt (0, 0)**
- **c) (5 P)** Jacobi-Matrix und Eigenwerte:
  Df(x) = [[0, 1], [−b/m − (3c/m)x₁², −(2a/m)·x₂·sgn(x₂)]] (getrennt für x₂ ≥ 0 und x₂ < 0)
  ⇒ Df(0,0) = [[0, 1], [−b/m, 0]] ⇒ **λ₁,₂ = ±i·√(b/m)** (rein imaginär — die Linearisierung
  entscheidet also **nicht**, deshalb Teil d)
- **d) (5 P)** Stabilität der Null-Lösung über die **vorgegebene Lyapunov-Funktion**
  V(x₁, x₂) = ½·m·x₂² + ½·b·x₁² + ¼·c·x₁⁴:
  grad V = (b·x₁ + c·x₁³, m·x₂), und
  dV/dt = ⟨grad V, f⟩ = (b x₁ + c x₁³)·x₂ + m·x₂·(−(a/m)x₂|x₂| − (b/m)x₁ − (c/m)x₁³)
  = **−a·x₂²·|x₂| ≤ 0** ⇒ Musterlösung: *„Demnach ist die Null-Lösung asymptotisch stabil."*

> **Zwei Dinge dazu:**
> 1. 🎯 **Diese Aufgabe war angekündigt.** In den Notizen aus Boliks Klausurvorbereitung vom
>    05.07. steht: *„DGL-Teil Lyapunov kam letztes Jahr nicht dran — interessant."* Fünf Tage
>    später kam sie. **Solche Nebenbemerkungen mitschreiben.**
> 2. ⚠️ Formal folgt aus V̇ ≤ 0 nur **Stabilität**; für *asymptotische* Stabilität bräuchte man
>    V̇ < 0 oder das Invarianzprinzip von LaSalle (V̇ = 0 nur auf x₂ = 0, und dort bleibt keine
>    Trajektorie außer der Ruhelage). Die Musterlösung springt direkt auf „asymptotisch stabil".
>    Im Zweifel den Schluss der Musterlösung schreiben und den LaSalle-Halbsatz ergänzen — das
>    kostet nichts und ist sachlich richtig.
> 3. **Überschneidung mit SOS Teil A!** Lyapunov-Stabilität, Ruhelagen, Linearisierung und
>    Jacobi-Matrix stehen genauso in `SOS/Teil_A/SOS_A_FS/parts/02_zustandsraum_lyapunov.tex`.
>    Wer VM und SOS im selben Semester schreibt, lernt diesen Block **einmal für beide**.

## Aufgabe 4 — Bayes (12 P)

Zwei Betriebe: **A = 70 %** der Gesamtproduktion, **B = 30 %**.
Normgerecht: **83 % von A**, **63 % von B**.
*(Im Chat-Gedächtnisprotokoll stand fälschlich 73 % für B — der echte Wert ist **63 %**.)*

Gegeben: P(A) = 0,7 · P(B) = 0,3 · P(N|A) = 0,83 · P(N|B) = 0,63

- **a-i) (2 P)** P(N|B) = **0,63** — steht direkt in der Angabe, zwei geschenkte Punkte.
- **a-ii) (6 P)** Totale Wahrscheinlichkeit:
  P(N) = P(N|A)·P(A) + P(N|B)·P(B) = 0,83·0,7 + 0,63·0,3 = **0,77**
- **b) (4 P)** Bayes: P(B|N) = P(B∩N)/P(N) = (0,63·0,3)/0,77 = **0,245**

> Die Musterlösung definiert zuerst sauber die Ereignisse A, B, N und den Ereignisraum Ω und
> schreibt „Gegeben ist …" hin. **Das ist der Rechenweg, den er sehen will** — bei 6 Punkten für
> eine Zeile Rechnung geht es offensichtlich um die Herleitung, nicht um die Zahl.

## Aufgabe 5 — Poisson und Binomial (18 P)

Großbäckerei mischt Rosinen in den Teig und teilt ihn in Portionen.

- **a) (6 P)** P(mindestens eine Rosine) ≥ 0,98, poissonverteilt. Wie viele Rosinen durchschnittlich?
  P(X ≥ 1) ≥ 0,98 ⇒ P(X = 0) ≤ 0,02 ⇒ e^(−μ) ≤ 0,02 ⇒ **μ ≥ 4**, wenn man μ ∈ ℕ₀ voraussetzt.
  *(exakt wäre μ ≥ ln 50 ≈ 3,912 — die Musterlösung rundet auf die nächste ganze Zahl und sagt
  das ausdrücklich dazu. Die Annahme hinschreiben!)*
- **b) (5 P)** μ = 5: P(X ≥ 2) = 1 − (e^(−5) + 5·e^(−5)) = **1 − 6·e^(−5) = 0,9596**
- **c) (7 P)** 500 Rosinen auf 100 Gebäckstücke, **ausdrücklich mit Binomialverteilung**:
  n = 500, **p = 1/100** ⇒ P(X ≥ 2) = 1 − B(0) − B(1)
  = 1 − (99/100)⁵⁰⁰ − 500·(1/100)·(99/100)⁴⁹⁹ = **0,9602**
  *Anmerkung der Musterlösung:* die Wahrscheinlichkeit, dass Rosine i in Gebäck j landet, ist
  1/100 — was sich auch aus E(X) = 5 = n·p ergibt.

> **Der Twist:** dieselbe Sachlage, dreimal, mit wechselndem Modell — und **p = 1/100 ergibt sich
> aus der Zahl der Gebäckstücke, nicht aus den 500 Rosinen.** Die Ergebnisse von b) und c) liegen
> mit 0,9596 und 0,9602 dicht beieinander (Poisson ist der Grenzfall der Binomialverteilung) —
> das ist die eingebaute Gegenprobe.

## Aufgabe 6 — Markov-Kette (15 P)

KFZ-Versicherung, drei Kategorien: **unzureichend (3), ausreichend (2), bevorzugt (1)**.
Keine direkten Wechsel (3)→(1) und (1)→(3). Es ändern sich **40 % von (3) zu (2), 30 % von (2)
zu (1), 10 % von (2) zu (3), 20 % von (1) zu (2)**.

- **a) (5 P)** Übergangsmatrix. Die Musterlösung baut zuerst eine „von/nach"-Tabelle in der
  Reihenfolge **3, 2, 1**:

  | von \ nach | 3 | 2 | 1 |
  |---|---|---|---|
  | **3** | 0,6 | 0,4 | 0 |
  | **2** | 0,1 | 0,6 | 0,3 |
  | **1** | 0 | 0,2 | 0,8 |

  *Anmerkung der Musterlösung:* konventionsgemäßer wäre die Anordnung 1, 2, 3:
  P = [[0,8, 0,2, 0], [0,3, 0,6, 0,1], [0, 0,4, 0,6]]
- **b) (7 P)** Stationäre Verteilung **mittels eines geeigneten linearen Gleichungssystems und
  elementarer Zeilenumformungen** (Weg vorgeschrieben!): (Pᵀ − E)·x = 0 lösen
  ⇒ x₂ = (2/3)·x₃, x₁ = (1/4)·x₂ = (1/6)·x₃
  ⇒ x = μ·(1/6, 4/6, 1) mit μ = 6/11, in der Anordnung 1-2-3: **x = (1/11)·(6, 4, 1)**
- **c) (3 P)** Nach dem **Ergodensatz**:
  lim(n→∞) Pⁿ = (1/11)·[[1, 4, 6], [1, 4, 6], [1, 4, 6]]
  (in der Anordnung 123 sind die Spalten entsprechend vertauscht)
  → **alle Zeilen identisch = die stationäre Verteilung**, unabhängig vom Startzustand.

> 🔴 **Das ist die Aufgabe mit dem Kein-Folgefehler-Problem** aus dem Chat: wer die
> Übergangsmatrix falsch aufstellt, bekommt **1 von 5 Punkten** in a) — und b) und c) bauen
> darauf auf und geben ebenfalls nichts, obwohl richtig weitergerechnet.
> **Gegenproben, die zehn Sekunden kosten:** jede Zeile von P summiert sich zu 1; die
> Diagonaleinträge sind „bleibt in derselben Klasse" = 1 − (Summe der Abflüsse); in c) muss
> jede Zeile des Grenzwerts dieselbe sein und sich zu 1 summieren ((1+4+6)/11 = 1 ✓).
> **Und: die Reihenfolge der Zustände selbst wählen und dazuschreiben** — die Musterlösung
> macht es in 321 und liefert die 123-Variante nach, beides gilt.

---

## Was Bolik vorher angesagt hat — und was davon stimmte

Quelle: `Fragestunde_Notizen/2026-07-05_*.jpeg` (Mitschrift aus der Klausurvorbereitung,
fünf Tage vor der Prüfung).

### Traf zu ✅
- **Bedingte Wahrscheinlichkeit** — *„spielt eine Rolle, P(B|A) gegeben, Umrechnung auf P(A|B)
  genauer anschauen"*, dazu totale Wahrscheinlichkeit und Bayes → **Aufgabe 4, 12 P**
- **Lyapunov** — *„kam letztes Jahr nicht dran — interessant"* → **Aufgabe 3d, 5 P**
- **Markov-Ketten** — *„wenn was drankäme, dann was Einfaches"*, letzte Klasse über die
  stationäre Verteilung → **Aufgabe 6**; „einfach" war es inhaltlich, aber es gab **15 Punkte**
- **Binomial- und Gaußverteilung** als die wichtigen Verteilungen → Aufgabe 5

### Traf NICHT zu ❌
- **χ²-Anpassungstest** — als *„sehr wahrscheinlich"* bezeichnet, dazu die Hausaufgabe mit den
  60 Briefen zum Niveau α = 0,05 → **kam nicht dran**
- **Konfidenzintervalle** (*„interessant, S. 52/53 einrahmen"*) → kam nicht dran
- **Hypothesentest über den Mittelwert bei bekannter Varianz** (*„könnte vorkommen, S. 58
  größter Teil des Inhalts"*) → kam nicht dran
- Das **gesamte Kapitel 2 (Induktive Statistik)** tauchte in der Klausur nicht auf.

> **Lehre:** Seine Ausschlüsse („ausgeschlossen", „gänzlich weglassen") kannst du nutzen, seine
> *Wahrscheinlichkeitsaussagen* („sehr wahrscheinlich") nicht. Der Stochastik-Teil bestand aus
> dem klassischen Wahrscheinlichkeitsrechnungs-Block, nicht aus der induktiven Statistik.

### Ausschlüsse aus derselben Mitschrift (fürs nächste Mal gegenprüfen!)
- Kapitel 1.1 „gibt nichts her"; Kombinatorik nur am Rande (allenfalls Binomialkoeffizient)
- **T-Verteilung und F-Verteilung gänzlich weglassen**
- **Multivariate Gaußverteilung ausgeschlossen** (Korrelation bivariat, nichts höherer Ordnung)
- Skript S. 25/26 überspringen
- Keine **Maximum-Likelihood**-Schätzung
- Hypothesentest bei **unbekannter** Varianz, Hypothesen über die Varianz und die zwei folgenden
  Tests **ausgeschlossen bis S. 60 inkl.**; S. 61 wieder möglich, aber sehr unwahrscheinlich
- Grenzwertsatz von Poisson weniger interessant; zentraler Grenzwertsatz v. a. der „mittlere Teil"
- Markov: Tschebyschew/Kolmogorow nicht interessant
- **Übungsaufgaben zur Klausurvorbereitung, vom Prof markiert:** A1 ✓ · A2 ✓ · A3 ✗ · A4 (✓) ·
  A5 ✓ · A6 ✗

⚠️ Diese Liste galt für **SoSe 2026**. Vor dem eigenen Antritt neu erfragen — aber sie zeigt,
dass er in der Klausurvorbereitung sehr konkret wird. **Diesen Termin auf keinen Fall verpassen.**

## Notenverteilung — die Zahlen dahinter

`Notenspiegel/VM_SoSe2026_Schnitt_3-79.jpeg` bzw. `..._WiSe2024-25_Schnitt_3-09_Steinbach.jpeg`

| | SoSe 2026 (Bolik) | WiSe 2024/25 (Steinbach) |
|---|---|---|
| Teilnehmende | 62 | 48 |
| **Schnitt** | **3,79** | **3,09** |
| Note 5,0 | **21 = 33,9 %** | 5 = 10,4 % |
| Note 1,0 | **0** | 2 |
| besser als 2,0 | 3 (4,8 %) | 5 (10,4 %) |

Im SoSe 2026 wurde **keine einzige 1,0** vergeben, der größte Balken ist mit Abstand die 5,0.
Der Vergleich mit dem Steinbach-Semester zeigt, dass das kein Fachproblem ist, sondern am
Prüfungsstil hängt.

## Konsequenzen für deinen Antritt

1. **Die Klausur SoSe 2026 mit Musterlösung ist ab jetzt deine wichtigste Übungsressource.**
   Vollständig, mit Punkteverteilung und offiziellem Lösungsweg — das gibt es sonst nirgends.
   Rechne sie mindestens zweimal, das zweite Mal unter 90 Minuten.
2. **Beide Hälften lernen.** 45 P Analysis/LinAlg + 45 P Stochastik, kein Ausweichen möglich.
3. **10 Seiten eigene Unterlagen sind erlaubt** — das ist genug für eine richtige Formelsammlung
   nach dem Muster deiner anderen. `VM_Formelsammlung_MayPa_2025.pdf` (10 Seiten, aus dem Chat)
   liegt als Startpunkt daneben; die Aufgabentypen oben geben die Gliederung vor.
4. **Rezepte statt Formeln.** Jede der sechs Aufgaben ist ein fester Ablauf
   (charakteristisches Polynom → Eigenvektoren → C; transformieren → auflösen → PBZ → Faltung;
   System 1. Ordnung → Ruhelage → Jacobi → Lyapunov; Ereignisse definieren → totale W. → Bayes;
   Verteilung wählen → Gegenwahrscheinlichkeit; Tabelle → P → (Pᵀ−E)x = 0 → Ergodensatz).
   Genau diese sechs Rezepte gehören auf die ersten Seiten der eigenen Unterlagen.
5. **Anfangsschritte doppelt prüfen** — wegen der fehlenden Folgefehler-Punkte, siehe Aufgabe 6.
6. **Zur Klausurvorbereitungs-Stunde gehen und mitschreiben.** Der Lyapunov-Hinweis war fünf
   Punkte wert und stand in keinem Skript.
