# Session 5 — Sa 18.07., 3 h · Code-Optimierung + Relationen (Erstkontakt)

**Quellen:** `V9.pdf` (Code-Opt.), `V3.pdf` S.1 + `V4.pdf` S.1 (Relationen) · **Prüfungsthemen:** Code-Optimierung mit Floating Point, Relationen (keine ÄR zeigen)

---

# Teil A1 — Code-Optimierung (V9)

## 1. Wie eine moderne superskalare CPU arbeitet

**Pipeline (skalar):** ein Befehl durchläuft Stufen: read instr → decode → read/write memory → ALU op → read/write memory. Bei 5 Stufen, Annahme 1 Cycle/Stufe:
- **Latency** = Zeit, die *ein* Befehl in der CPU verweilt ≥ Anzahl Stufen (z. B. 5 Cycles).
- **Throughput** = Rate, mit der Befehle *fertig* werden (Befehle/Cycle). Ideal skalar: 1.

**Superskalar** heißt: mehrere Befehle gleichzeitig in Bearbeitung. Tricks (die „hidden logic"):
- mehr als eine Execution Unit für schnelle Befehle (z. B. 4 Addierer)
- mehr physische als logische Register (**register renaming**)
- **out-of-order execution**
- **speculative execution** + **branch prediction**

Realer Throughput: **5–7 Befehle/Cycle**.

## 2. Die Befehlskosten-Tabelle — DAS Klausurwissen

| Klasse | Latency | Throughput | Befehle |
|---|---|---|---|
| **schnell** | 1 Cycle | ~4/Cycle | XOR, ADD, SUB, AND, INC, DEC, SHIFT |
| **mittel** | wenige Cycles | ~1/Cycle | **MUL** |
| **teuer** | **50–300 Cycles** | ~1/20 pro Cycle | **DIV, MOD, sin, cos, exp, log, pow** |

> **Kernaussage:** Multiplikation ist ~1 Cycle-Klasse (billig), aber **Division, Modulo und alle transzendenten Funktionen (pow, exp, log, sin, cos) sind 50–300× teurer.** Optimierung heißt: teure durch billige ersetzen.

## 3. Das Optimier-Repertoire

**a) pow durch Multiplikation ersetzen** (der Prof schreibt „POW kommt drin vor"):
```c
pow(x, 2)  →  x*x
pow(x, 3)  →  x*x*x
pow(x, 4)  →  { double x2 = x*x; return x2*x2; }   // 2 statt 1 teure Op
```
`pow` ist ein transzendenter Aufruf (intern exp(y·log(x))) → teuer. Bei kleinen ganzzahligen Exponenten ist die explizite Multiplikation um Größenordnungen schneller.

**Vertiefung aus dem fxtbook (§28.5, „Binary exponentiation"):** Für beliebige ganzzahlige Exponenten e berechnet man aᵉ mit nur **~log₂(e) Multiplikationen** statt e−1. Idee: schreibe e binär, dann ist aᵉ das Produkt der a^(2^i) für die gesetzten Bits — und die a^(2^i) entstehen durch **fortgesetztes Quadrieren**:

```c
double power_r2l(double a, ulong e) {   // right-to-left powering, fxtbook §28.5.1
    double t = 1;
    if (e) {
        double s = a;
        while (1) {
            if (e & 1)  t *= s;   // Bit gesetzt → Faktor mitnehmen
            e /= 2;
            if (0 == e)  break;
            s *= s;               // s = a^(2^i) durch Quadrieren
        }
    }
    return t;
}
```

Beispiel a¹¹ (e = 11 = `1011`): t sammelt a¹·a²·a⁸ = a¹¹ — 5 Multiplikationen statt 10. Schau, wie hier zwei Prüfungsthemen zusammenlaufen: der Exponent wird **Bit für Bit** abgearbeitet (Bit Wizardry!) und macht die teure pow-Operation billig (Code-Optimierung).

**b) Division durch Multiplikation mit dem Kehrwert:**
```c
// schlecht: N Divisionen
for (i) a[i] = a[i] / d;
// gut: 1 Division, N Multiplikationen
double inv = 1.0 / d;
for (i) a[i] = a[i] * inv;
```
Ein Kehrwert vorab, dann nur noch billige Multiplikationen. (Das ist genau der Grund für Newton-Raphson-Division in den FPUs — S3/S4.)

**c) Loop Unrolling + mehrere Akkumulatoren** (V9-Beispiel):
```c
int s0=0,s1=0,s2=0,s3=0;
for (unsigned j=0; j+3 < N; j+=4) {   // 4 Teilsummen parallel
    s0 += A[j];   s1 += A[j+1];
    s2 += A[j+2]; s3 += A[j+3];
}
int summe = s0+s1+s2+s3;
```
Warum schneller: die 4 Teilsummen sind **voneinander unabhängig** → die superskalare CPU rechnet sie parallel in verschiedenen Addierern (bei einer einzigen Summe blockiert die Datenabhängigkeit s += A[j] die Pipeline). Nutzt außerdem **Level-1-Cache** gut, weil A linear durchlaufen wird.

**d) Branches vermeiden:** `if` zwingt die CPU zur Vorhersage; bei Fehlvorhersage wird die spekulativ geladene Pipeline verworfen (Performance-Verlust). Branch-freier Code (Masken, arithmetische Tricks aus Session 1) hält die Pipeline voll.

Zwei Beispiele aus dem fxtbook (§1.11, „Avoiding branches"):
```c
// Bereichstest ohne zwei Vergleiche: statt  if (x<0 || x>m)
if ( (unsigned)x > m )  { ... }   // negativer x wird als riesige unsigned-Zahl > m

// max(0, x) ohne if:
long max0(long x) { return x & ~(x >> (BITS_PER_LONG-1)); }
```
Der max0-Trick: bei negativem x liefert der arithmetische Shift ein Wort aus lauter Einsen; negiert und ge-AND-et löscht das alle Bits → 0. Bei positivem x ist die Maske lauter Einsen → x bleibt. (Das fxtbook merkt trocken an: moderne Compiler erzeugen so etwas oft selbst — „your compiler may be smarter than you thought".)

## 4. Float-Gleichheit (V4) — Brücke zu Teil A2

```c
double a = rechne1(), b = rechne2();
if (a == b) { ... }   // gefährlich: Rundung macht exakt Gleiches ungleich
bool equal(double a, double b) {
    constexpr double eps = 1.0e-9;
    return abs(a - b) <= eps;   // Toleranzvergleich
}
```
Merke: `==` auf Floats ist fast immer falsch. Man vergleicht mit einem eps. **Aber** genau dieser eps-Vergleich hat eine tückische Eigenschaft → Teil A2.

---

# Teil A2 — Relationen (V3 S.1, V4 S.1)

## 1. Relation und die drei Eigenschaften

Eine **Relation** R auf einer Menge M ist eine Abbildung M × M → {0,1}. Man schreibt a ~ b, wenn (a,b) auf 1 abgebildet wird. (Auf einer n-elementigen Menge gibt es 2^(n²) Relationen.)

Eine **Äquivalenzrelation (ÄR)** erfüllt alle drei:

| Eigenschaft | Bedingung |
|---|---|
| **Reflexivität** (R) | a ~ a für alle a |
| **Symmetrie** (S) | a ~ b ⇒ b ~ a |
| **Transitivität** (T) | a ~ b und b ~ c ⇒ a ~ c |

Eine ÄR zerlegt M in **Äquivalenzklassen**. Beispiel: „mod m" auf ℤ (a ≡ b ⇔ m teilt a−b) → Klassen {0,1,…,m−1}.

## 2. „Zeige, dass etwas KEINE ÄR ist" — die Klausuraufgabe

**Strategie:** Es genügt, **eine** der drei Eigenschaften durch ein **Gegenbeispiel** zu widerlegen. Nicht alle drei prüfen — eine reicht, dann ist es fertig.

### Das wahrscheinlichste Beispiel: Float-Gleichheit mit eps

Definiere a ~ b :⇔ |a − b| ≤ eps. Ist das eine ÄR?
- **Reflexiv?** |a − a| = 0 ≤ eps ✓
- **Symmetrisch?** |a − b| = |b − a| ✓
- **Transitiv?** a ~ b und b ~ c ⇒ a ~ c? **NEIN.**

**Gegenbeispiel** (eps = 1): x = 0, y = 1, z = 2.
```
|x − y| = 1 ≤ 1  ⇒ x ~ y  ✓
|y − z| = 1 ≤ 1  ⇒ y ~ z  ✓
|x − z| = 2 > 1  ⇒ x ≁ z  ✗   → nicht transitiv!
```
Die kleinen Abstände „addieren sich auf". Das ist die Skizze aus V4: ein Zahlenstrahl, auf dem Nachbarn je ~ sind, die Enden aber nicht. **→ keine Äquivalenzrelation.**

## 3. Weitere typische Nicht-ÄR (zum Trainieren)

| Relation auf | ~ definiert als | scheitert an |
|---|---|---|
| ℤ | a ~ b :⇔ a ≤ b | Symmetrie (2≤3, aber 3≰2) |
| ℤ | a ~ b :⇔ a < b | Reflexivität (a<a falsch) *und* Symmetrie |
| Menschen | a ~ b :⇔ a kennt b | Symmetrie/Transitivität |
| ℝ | a ~ b :⇔ \|a−b\| ≤ 1 | Transitivität |

---

# Teil B — Übungen

Lösungen in `S5_Code_Optimierung_Relationen_Loesungen.md`.

### Ü1 — Befehlskosten
Ordne nach Kosten (billig → teuer): `MOD`, `ADD`, `pow`, `MUL`, `SHIFT`, `sin`. Nenne für die teure Gruppe die Größenordnung in Cycles.

### Ü2 — pow optimieren
Optimiere ohne pow: (a) `pow(x,2)`, (b) `pow(x,3)`, (c) `pow(x,8)` (Ziel: möglichst wenige Multiplikationen — Hinweis: wiederholtes Quadrieren). Wie viele Multiplikationen jeweils?

### Ü3 — Division raus
Diese Schleife dividiert N-mal. Schreib sie so um, dass nur **eine** Division vorkommt:
```c
for (int i = 0; i < N; ++i) result[i] = data[i] / faktor;
```

### Ü4 — Loop Unrolling
Warum ist die Version mit vier Teilsummen s0..s3 schneller als eine einzige Summe `s += A[j]`, obwohl beide gleich viele Additionen ausführen? (Stichworte: Datenabhängigkeit, superskalar.)

### Ü5 — Latency vs. Throughput
Erkläre den Unterschied in je einem Satz. Eine CPU hat für ADD Latency 1 und Throughput 4/Cycle — wie passt das zusammen?

### Ü6 — Float-Vergleich
Warum ist `if (a == b)` bei zwei berechneten doubles gefährlich? Wie macht man es richtig?

### Ü7 — Keine ÄR (Kernaufgabe)
Zeige, dass a ~ b :⇔ |a − b| ≤ eps **keine** Äquivalenzrelation auf ℝ ist. Nenne die drei Eigenschaften, prüfe jede, gib ein konkretes Gegenbeispiel für die verletzte an.

### Ü8 — Eigenschaften prüfen
Prüfe für jede Relation R, S, T und entscheide, ob ÄR:
a) auf ℤ: a ~ b :⇔ a·b > 0
b) auf ℤ: a ~ b :⇔ a − b ist gerade
c) auf ℤ: a ~ b :⇔ a ≤ b

### Ü9 — Transfer
In V3 heißt es, „mod m" sei eine ÄR. Zeige kurz R, S, T für a ≡ b :⇔ m teilt (a−b).

### Ü10 — Binary exponentiation (fxtbook §28.5)
Rechne `power_r2l(a, 13)` von Hand durch (13 = `1101` binär): Tabelle mit e, e&1, s, t nach jedem Schleifendurchlauf. Wie viele Multiplikationen insgesamt, und wie viele wären es naiv?
