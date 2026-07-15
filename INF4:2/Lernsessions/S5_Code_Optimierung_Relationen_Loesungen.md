# Session 5 — Lösungen

### Ü1 — Befehlskosten
Billig → teuer: **ADD ≈ SHIFT** (1 Cycle) < **MUL** (wenige Cycles) < **pow ≈ sin ≈ MOD** (teuer).
Genauer: ADD, SHIFT = 1 Cycle; MUL = wenige Cycles; MOD, pow, sin = **50–300 Cycles** (transzendente Funktionen und Division/Modulo).

### Ü2 — pow optimieren
- **a)** `pow(x,2)` → `x*x` — **1** Mult.
- **b)** `pow(x,3)` → `x*x*x` — **2** Mult.
- **c)** `pow(x,8)` → wiederholtes Quadrieren: `x2=x*x; x4=x2*x2; x8=x4*x4;` — **3** Mult (statt 7 bei naivem x*x*…). Exponentiation by squaring.

### Ü3 — Division raus
```c
double inv = 1.0 / faktor;              // eine einzige Division
for (int i = 0; i < N; ++i) result[i] = data[i] * inv;
```
Kehrwert einmal berechnen, dann N billige Multiplikationen statt N teurer Divisionen.

### Ü4 — Loop Unrolling
Bei `s += A[j]` hängt jede Addition vom Ergebnis der vorigen ab (**Datenabhängigkeit**): die CPU muss warten, bis s fertig ist, bevor sie den nächsten Wert addiert — die superskalaren Addierer stehen leer. Die vier Teilsummen s0..s3 sind **unabhängig**, also rechnet die CPU sie **parallel** in verschiedenen Execution Units. Gleich viele Additionen, aber die Pipeline bleibt gefüllt statt zu blockieren. (Zusätzlich cache-freundlich durch lineares Durchlaufen.)

### Ü5 — Latency vs. Throughput
**Latency** = wie lange *ein* Befehl von Start bis Ergebnis braucht. **Throughput** = wie viele Befehle pro Cycle *fertig* werden. Kein Widerspruch: die CPU hat mehrere Addierer und Pipelining — ein einzelnes ADD braucht zwar 1 Cycle bis zum Ergebnis, aber es können 4 ADDs gleichzeitig „unterwegs" sein und pro Cycle 4 fertig werden.

### Ü6 — Float-Vergleich
Berechnete doubles haben Rundungsfehler; zwei mathematisch gleiche Ergebnisse können sich im letzten Bit unterscheiden, dann ist `a == b` false, obwohl „eigentlich gleich". Richtig: Toleranzvergleich `abs(a - b) <= eps` mit kleinem eps (z. B. 1e-9).

### Ü7 — Keine ÄR
a ~ b :⇔ |a − b| ≤ eps.
- **Reflexiv:** |a−a| = 0 ≤ eps ✓
- **Symmetrisch:** |a−b| = |b−a| ✓
- **Transitiv:** ✗. Gegenbeispiel (eps = 1): 0 ~ 1 (|0−1|=1≤1) und 1 ~ 2 (|1−2|=1≤1), aber 0 ≁ 2 (|0−2|=2>1).
Da Transitivität verletzt ist, ist es **keine Äquivalenzrelation**. (Reflexiv und symmetrisch reichen nicht.)

### Ü8 — Eigenschaften prüfen
**a) a·b > 0:**
- Reflexiv? a·a = a² > 0 gilt **nicht für a=0** (0·0 = 0 ≯ 0) → **nicht reflexiv** → keine ÄR.
- (Symmetrisch ja; transitiv im Wesentlichen ja auf ℤ\{0}, aber die 0 kippt schon die Reflexivität.)

**b) a − b gerade** (= a ≡ b mod 2):
- Reflexiv: a−a = 0 gerade ✓
- Symmetrisch: a−b gerade ⇒ b−a gerade ✓
- Transitiv: a−b und b−c gerade ⇒ a−c = (a−b)+(b−c) gerade ✓
→ **Äquivalenzrelation** (zwei Klassen: gerade / ungerade).

**c) a ≤ b:**
- Reflexiv: a ≤ a ✓
- Symmetrisch: 2 ≤ 3, aber 3 ≰ 2 → **nicht symmetrisch** → keine ÄR (es ist eine Ordnungsrelation).

### Ü9 — mod m ist ÄR
a ≡ b :⇔ m | (a−b).
- **R:** m | (a−a) = 0 ✓
- **S:** m | (a−b) ⇒ a−b = k·m ⇒ b−a = −k·m ⇒ m | (b−a) ✓
- **T:** m | (a−b) und m | (b−c) ⇒ a−b = k·m, b−c = l·m ⇒ a−c = (k+l)·m ⇒ m | (a−c) ✓
Alle drei erfüllt → **Äquivalenzrelation**, Klassen {0,1,…,m−1}.

### Ü10 — Binary exponentiation, power_r2l(a, 13)
e = 13 = `1101`. Start: t = 1, s = a.

| Durchlauf | e (vorher) | e&1 | t danach | s danach |
|---|---|---|---|---|
| 1 | 13 (1101) | 1 | a | a² |
| 2 | 6 (110) | 0 | a | a⁴ |
| 3 | 3 (11) | 1 | a·a⁴ = a⁵ | a⁸ |
| 4 | 1 (1) | 1 | a⁵·a⁸ = a¹³ | — (break, e=0) |

Ergebnis a¹³ ✓ (Bits 1101: a¹·a⁴·a⁸ = a¹³).
**Multiplikationen:** 3 Quadrierungen (s) + 3 Produkte (t) = **6** statt **12** naiv (a·a·…·a). Der Vorteil wächst mit e: allgemein ~2·log₂(e) statt e−1.
