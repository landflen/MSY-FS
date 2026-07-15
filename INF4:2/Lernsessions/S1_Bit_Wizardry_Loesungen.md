# Session 1 — Lösungen

### Ü1 — O-Definition
> T(n) ist O(f(n)), wenn es c > 0 und n₀ gibt, sodass **T(n) ≤ c·f(n) für alle n ≥ n₀**.

`x & -x` ist O(1), weil es aus einer **festen Anzahl** Befehle besteht (NEG + AND = 2, das Laden mitgezählt 3), die **nicht von n abhängt**. O(1) verlangt eine konstante obere Schranke, nicht einen einzigen Befehl.

### Ü2 — Was ist n?
Falsch ist die Bedeutung von n. Bei Bit Wizardry ist **n = Anzahl Bits im Wort**, nicht die Anzahl der Array-Elemente. popcount eines 64-Bit-Wortes ist O(log 64) = 6 Schritte pro Wort — die 1000 Zahlen haben damit nichts zu tun (die gäben einen Faktor 1000 als separate Schleife, aber n bleibt die Wortbreite).

### Ü3 — Zweierkomplement
```
 w        = 0101 1000
~w        = 1010 0111
-w = ~w+1 = 1010 1000
w & -w    = 0000 1000   → isoliert das niedrigste gesetzte Bit
w & (w-1):
 w-1      = 0101 0111
 w &(w-1) = 0101 0000   → löscht das niedrigste gesetzte Bit
```
`w & -w` isoliert das niedrigste gesetzte Bit, `w & (w-1)` löscht es.

### Ü4 — Rotation
BPL = 8, w = `1101 0011`, s = 3:
```
w >> 3            = 0001 1010
w << (8-3)=5      = 0110 0000     (untere 5 Bits 00011 nach oben, Rest fällt raus)
OR                = 0111 1010
```
Ergebnis: `0111 1010`. (Kontrolle: die 3 herausrotierten unteren Bits `011` erscheinen oben wieder.)

### Ü5 — Klassifizieren
- **a) O(n)** — Schleife schiebt w Bit für Bit, im Worst Case n Durchläufe (höchstes Bit gesetzt).
- **b) O(n)** im Worst Case (alle Bits gesetzt), aber genauer: **O(popcount(w))** — die Schleife läuft *einmal pro gesetztem Bit* (`w &= w-1` löscht je eins). Zählt die gesetzten Bits. Hängt nicht von n direkt, sondern von der Anzahl gesetzter Bits ab; obere Schranke n.
- **c) O(1)** — zwei Befehle, unabhängig von n. Isoliert das niedrigste gesetzte Bit.
- **d) O(1)** — testet, ob w eine Zweierpotenz ist (bzw. 0): genau ein Bit gesetzt ⇒ `w & (w-1) == 0`.

### Ü6 — Masken für 16 Bit
```
Schritt 1 (1→2):  0101010101010101 = 0x5555
Schritt 2 (2→4):  0011001100110011 = 0x3333
Schritt 3 (4→8):  0000111100001111 = 0x0f0f
Schritt 4 (8→16): 0000000011111111 = 0x00ff
```
```c
uint16_t ones_count16(uint16_t x) {
    x = (x & 0x5555) + ((x >> 1) & 0x5555);
    x = (x & 0x3333) + ((x >> 2) & 0x3333);
    x = (x & 0x0f0f) + ((x >> 4) & 0x0f0f);
    x = (x & 0x00ff) + ((x >> 8) & 0x00ff);
    return x;
}
```
4 Schritte = log₂(16). ✓

### Ü7 — Die Prüfungsfrage
Zwei Änderungen, sonst nichts:
1. **Masken auf 64 Bit verlängern** (Muster bleibt, wiederholt sich doppelt):
   `0x5555555555555555`, `0x3333333333333333`, `0x0f0f0f0f0f0f0f0f`, `0x00ff00ff00ff00ff`, `0x0000ffff0000ffff`.
2. **Einen Schritt ergänzen** (32→64) mit Maske `0x00000000ffffffff` und Shift 32.
Aufwand bleibt O(log n), jetzt 6 statt 5 Schritte.

### Ü8 — Niedrigstes gesetztes Bit
```c
// O(n): Maske durch alle Bits wandern lassen
ulong lowest_On(ulong w){ for(ulong m=1;m;m<<=1) if(w&m) return m; return 0; }
// O(1): Zweierkomplement-Trick
ulong lowest_O1(ulong w){ return w & -w; }
```
O(n): Schleife bis zu n Durchläufe. O(1): feste Befehlszahl, unabhängig von n.

### Ü9 — Shift-and-Add, mul(5, 6)
a=5 (`101`), b=6 (`110`), r=0:

| Durchlauf | b&1 | r danach | a danach | b danach |
|---|---|---|---|---|
| Start | — | 0 | 5 | 6 (110) |
| 1 | 0 | 0 | 10 | 3 (011) |
| 2 | 1 | 10 | 20 | 1 (001) |
| 3 | 1 | 30 | 40 | 0 |

Ergebnis **30** ✓ (= 5·6).

---

# Teil C — Warm-up Mittwoch

### Ü10 — Die Rolle von n₀
**Ja, O(n).** Wähle c = 5 und n₀ = 8: für alle n ≥ 8 gilt T(n) = 5n ≤ 5·n. ✓
Die Ausreißer bei n < 8 sind egal — **genau dafür ist n₀ da**: die Definition erlaubt endlich viele Ausnahmen bei kleinen n. Ohne n₀ in der Definition wäre der Algorithmus nicht O(n), denn bei n = 5 ist 2⁵ = 32 > 5·5.

### Ü11 — Ohne Schleife heißt nicht O(1)
- **a) O(1).** 40 Befehle, aber die Anzahl hängt **nicht von n ab** — konstante obere Schranke genügt. „O(1) heißt nicht nur 1 Befehl" — auch 40 sind erlaubt.
- **b) O(log n).** Obwohl keine Schleife dasteht: verdoppelt man die Wortbreite, braucht der Code *deshalb* einen Schritt mehr (64 Bit → 6 Schritte, 128 Bit → 7). Die Schrittzahl wächst mit log₂(n) — das Ausrollen der Schleife ändert die Klasse nicht.

**Der Test dahinter:** „Ändert sich die Schrittzahl, wenn n wächst?" — a) nein → O(1); b) ja, um +1 pro Verdopplung → O(log n).

### Ü12 — Rotation, neues w
BPL = 8, w = `1001 0110`, s = 5:
```
w >> 5            = 0000 0100
w << (8-5)=3      = 1011 0000     (obere 3 Bits 100 fallen raus, Rest rückt hoch)
OR                = 1011 0100
```
Ergebnis: `1011 0100`. **Selbsttest:** vorher 4 Einsen, nachher 4 Einsen ✓. (Kontrolle: die unteren 5 Bits `10110` stehen jetzt oben, die oberen 3 Bits `100` unten.)

### Ü13 — Finde den Bug
`+` bindet in C **stärker** als `&`. Die Zeile wird geparst als:
```c
x = (x >> 1) & (0x55 + (x & 0x55));
```
— erst wird 0x55 zur unteren Blocksumme **addiert**, dann erst maskiert. Richtig:
```c
x = ((x >> 1) & 0x55) + (x & 0x55);
```
Jeden AND-Term einzeln klammern, dann addieren.

### Ü14 — Zweierkomplement, neues w
```
 w        = 0110 1100
~w        = 1001 0011
-w = ~w+1 = 1001 0100
w & -w    = 0000 0100   → isoliert das niedrigste gesetzte Bit ✓
 w-1      = 0110 1011
w & (w-1) = 0110 1000   → löscht das niedrigste gesetzte Bit ✓
```
**Zusatz:**
```c
bool exactly_one(ulong w){ return w != 0 && (w & (w-1)) == 0; }
```
Feste Befehlszahl, unabhängig von n → O(1). Der Fall w = 0 wird jetzt korrekt ausgeschlossen.

### Ü15 — Verdopplung auf 128 Bit
- **7 Schritte** statt 6 (log₂ 128 = 7).
- **Masken verlängern:** dieselben Muster (5, 3, f, …), nur doppelt so lang — 32 statt 16 Hex-Ziffern.
- **Neuer letzter Schritt** (64 → 128): Maske = 64 Nullen gefolgt von 64 Einsen, also `0x0000000000000000ffffffffffffffff`, mit Shift 64.
- **O-Klasse: O(log n).** Blockgröße verdoppelt sich pro Schritt (1 → 2 → 4 → … → 128) ⇒ **log₂(n) Schritte**; bei n = 128 sind das 7.

### Ü16 — Klassifizieren II
- **a) O(n)** — die „feste" 64 ist in Wahrheit **n** (Bits im Wort): für ein 128-Bit-Wort müsste die Schleife bis 128 laufen. Hartcodierte Wortbreite ist keine Konstante. Die Funktion berechnet **popcount** (naiv, Bit für Bit).
- **b) O(n)** — im Worst Case (höchstes Bit gesetzt) läuft die Schleife n−1 mal. Die Funktion berechnet die **Position des höchsten gesetzten Bits** (= ⌊log₂ w⌋).
- **c) O(1)** — zwei Shifts + OR, feste Befehlszahl: **Rotation um 7 nach rechts** (7 + 57 = 64 = BPL).
- **d) O(1)** — ein AND + Vergleich: testet, ob w **gerade** ist (unterstes Bit 0).

### Ü17 — Shift-and-Add, mul(9, 5)
a=9 (`1001`), b=5 (`101`), r=0:

| Durchlauf | b&1 | r danach | a danach | b danach |
|---|---|---|---|---|
| Start | — | 0 | 9 | 5 (101) |
| 1 | 1 | 9 | 18 | 2 (010) |
| 2 | 0 | 9 | 36 | 1 (001) |
| 3 | 1 | 45 | 72 | 0 |

Ergebnis **45** ✓ (= 9·5). **3 Durchläufe** — die Schleife läuft, bis b = 0 ist, also so oft, wie b Bits bis zum höchsten gesetzten Bit hat (5 = `101` → 3). Worst Case: höchstes Bit von b gesetzt → n Durchläufe → **O(n)**.
