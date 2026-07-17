# S6 — Lösungen

### M1 — a·b ≥ 0 auf ℤ
- **R:** a·a = a² ≥ 0 gilt für alle a, **auch für a = 0** (0 ≥ 0). ✓
- **S:** a·b = b·a, also überträgt sich a·b ≥ 0 direkt. ✓
- **T:** ✗. Gegenbeispiel **mit der 0 in der Mitte**: a = 1, b = 0, c = −1:
  - 1·0 = 0 ≥ 0 ⇒ 1 ~ 0 ✓
  - 0·(−1) = 0 ≥ 0 ⇒ 0 ~ −1 ✓
  - 1·(−1) = −1 < 0 ⇒ 1 ≁ −1 ✗
- **Keine ÄR.** Die 0 ist mit *jeder* Zahl verwandt und verbindet so die positiven mit den negativen Zahlen — dadurch bricht die Transitivität. (Ohne die 0, also auf ℤ\{0}, wäre es eine ÄR mit den zwei Klassen „positiv"/„negativ".)

### M2 — a·b ungerade auf ℤ
- **R:** a·a ungerade müsste für **alle** a gelten. Gegenbeispiel a = 2: 2·2 = 4 gerade ⇒ 2 ≁ 2. **Nicht reflexiv** → keine ÄR, fertig.
- (S gilt übrigens: a·b = b·a. Spielt aber keine Rolle mehr — eine verletzte Eigenschaft reicht.)

### M3 — Differenz durch 3 teilbar (allgemeiner Beweis, keine Zahlenbeispiele)
Definition: a ~ b :⇔ a − b = q·3 mit q ∈ ℤ.
- **R:** a − a = 0 = 0·3. Also a ~ a für alle a. ✓ (q = 0 ist erlaubt!)
- **S:** Sei a ~ b, also a − b = q·3. Dann b − a = −(a − b) = (−q)·3, und −q ist ganz. Also b ~ a. ✓
- **T:** Sei a ~ b und b ~ c, also a − b = q·3 und b − c = p·3. Addieren: a − c = (a − b) + (b − c) = (q + p)·3, und q + p ist ganz. Also a ~ c. ✓
Alle drei erfüllt ⇒ **ÄR**. Äquivalenzklassen: die drei Rest-Töpfe **{…,−3,0,3,6,…}, {…,−2,1,4,7,…}, {…,−1,2,5,8,…}** — Repräsentanten {0, 1, 2}.

### M4 — Teilbarkeit und die 0
a) **Ja.** 0 = 0·7, q = 0 ist ganz. (Jede Zahl teilt die 0.)
b) **Nein.** 7 = q·0 = 0 ist für kein q erfüllbar.
c) **Ja.** 0 = q·0 gilt für jedes q (z. B. q = 0).
Merke: **m teilt 0 — immer.** Deshalb ist bei „mod m" die Reflexivität nie in Gefahr: a − a = 0.

### M5 — Klausurantwort in voller Form
a ~ b :⇔ |a − b| ≤ 0,5. Eine ÄR muss reflexiv, symmetrisch und transitiv sein.
- **Reflexiv:** |a − a| = 0 ≤ 0,5 für alle a. ✓
- **Symmetrisch:** |a − b| = |b − a|, also folgt aus a ~ b sofort b ~ a. ✓
- **Transitiv:** Gegenbeispiel: x = 0, y = 0,5, z = 1:
  - |0 − 0,5| = 0,5 ≤ 0,5 ⇒ 0 ~ 0,5 ✓
  - |0,5 − 1| = 0,5 ≤ 0,5 ⇒ 0,5 ~ 1 ✓
  - |0 − 1| = 1 > 0,5 ⇒ 0 ≁ 1 ✗ — nicht transitiv.
Da die Transitivität verletzt ist, ist ~ **keine Äquivalenzrelation**. ∎
(Form-Checkliste: alle drei Eigenschaften genannt ✓, konkrete Zahlen beim Gegenbeispiel ✓, Schlusssatz ✓.)

### M6 — Wiederholtes Quadrieren
Zählweise wie in S5/Ü2: von Hand zählt man nur echte Produkte (kein 1·s).
a) **x¹⁶ = 4 Mult:** x² = x·x, x⁴ = x²·x², x⁸ = x⁴·x⁴, x¹⁶ = x⁸·x⁸. (Naiv: 15.)
b) **x¹² = 4 Mult:** 12 = `1100` ⇒ x¹² = x⁸·x⁴. Quadrieren bis x⁸ (3 Mult), dann x⁸·x⁴ (1 Mult). (Naiv: 11.)
c) **x¹⁰ = 4 Mult:** 10 = `1010` ⇒ x¹⁰ = x⁸·x². x², x⁴, x⁸ (3 Mult), dann x⁸·x² (1 Mult). (Naiv: 9.)
Muster: Exponent binär lesen — Quadrieren liefert die x^(2^i), die gesetzten Bits sagen, welche davon multipliziert werden.

### M7 — power_r2l(a, 25)
25 = `11001`. Start: t = 1, s = a.

| Durchlauf | e (vorher) | e&1 | t danach | s danach |
|---|---|---|---|---|
| 1 | 25 (11001) | 1 | a | a² |
| 2 | 12 (1100) | 0 | a | a⁴ |
| 3 | 6 (110) | 0 | a | a⁸ |
| 4 | 3 (11) | 1 | a·a⁸ = a⁹ | a¹⁶ |
| 5 | 1 (1) | 1 | a⁹·a¹⁶ = a²⁵ | — (break, e = 0) |

Ergebnis a²⁵ ✓ (Bits 11001: a¹·a⁸·a¹⁶ = a²⁵).
**Code-Multiplikationen:** 4 Quadrierungen (s: a²,a⁴,a⁸,a¹⁶) + 3 t-Produkte (drei gesetzte Bits) = **7**.
Zählregel: Stelle(MSB) = 5 ⇒ 5 − 1 = 4 Quadrierungen; 3 gesetzte Bits ⇒ 3 t-Produkte ⇒ 4 + 3 = **7** ✓.
Naiv: a·a·…·a = **24** Multiplikationen.
(Feinheit: der Code zählt auch das erste `t *= s` mit t = 1 als Multiplikation — von Hand könnte man das sparen. Bei „wie viele Multiplikationen führt der Code aus" gilt die Code-Zählung.)

### M8 — Latency vs. Throughput
a) Die MUL-Einheit ist eine **Pipeline** mit 3 Stufen: ein einzelnes MUL braucht 3 Cycles bis zum Ergebnis (**Latency**), aber pro Cycle kann ein neues MUL nachgeschoben werden — es sind bis zu 3 gleichzeitig unterwegs, und ab dem dritten Cycle wird jeden Cycle eines **fertig** (**Throughput** 1/Cycle).
b) Falsch ist der Schluss „Throughput ⇒ Dauer des Einzelbefehls". Throughput ist eine **Rate** (wie viele werden pro Cycle fertig, wenn viele unabhängige Befehle anstehen), Latency die **Dauer eines einzelnen** Befehls. Das einzelne MUL ist erst nach 3 Cycles fertig — wer sofort das Ergebnis braucht (Datenabhängigkeit!), wartet 3 Cycles, egal wie gut der Throughput ist.

### M9 — popcount auf 256 Bit
a) Blockgröße verdoppelt sich pro Schritt: 1 → 2 → 4 → … → 256 ⇒ **log₂(256) = 8 Schritte**. (64 Bit: 6, 128 Bit: 7, 256 Bit: 8.) Genau dieser Schluss „Verdopplung pro Schritt ⇒ log₂(n) Schritte" ist die O(log n)-Begründung.
b) **Jede** Maske ist so breit wie das ganze Wort: 256 Bit = **64 Hex-Ziffern**. Auch die 5er-Maske! (Das war der Ü15-Fehler: Maske zu kurz.)
c) Erste Maske: 64× `5` (also `0x5555…5` mit 64 Fünfen).
Letzte Maske (Schritt „128 → 256"): **32× `0`, dann 32× `f`** — die untere Worthälfte voll Einsen.

### M10 — O-Definition
T(n) ∈ O(f(n)) :⇔ es gibt c > 0 und n₀, sodass **T(n) ≤ c·f(n) für alle n ≥ n₀**.
Für T(n) = 7n + 50: wähle z. B. **c = 8, n₀ = 50**: für n ≥ 50 ist 7n + 50 ≤ 7n + n = 8n. ✓
(Auch okay: c = 57, n₀ = 1, denn 7n + 50 ≤ 7n + 50n = 57n für n ≥ 1. c und n₀ sind nicht eindeutig — es muss nur *ein* Paar existieren.)

### M11 — Präzedenz
`+` bindet stärker als `&`. C rechnet also `(x >> 2) & (0x33 + (x & 0x33))` — die Addition frisst die rechte Maske, das AND links maskiert mit einem Zufallswert. Korrekt:
```c
x = ((x >> 2) & 0x33) + (x & 0x33);
```
