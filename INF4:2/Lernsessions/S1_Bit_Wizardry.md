# Session 1 — Di 14.07., 3 h · Bit Wizardry I + Asymptotik

**Quellen:** `V5.pdf`, `V6.pdf` · **Prüfungsthemen:** Bit Wizardry, Asymptotik

---

# Teil A — Kompaktskript

## 1. Asymptotik: die O-Definition

> Ein Algorithmus ist **O(f(n))**, wenn für die Laufzeit T(n) gilt:
> **T(n) ≤ c · f(n)** für alle **n ≥ n₀**, mit einem **c > 0**, c ∈ ℝ.

Das ist wörtlich die Definition aus V5 — so hinschreiben, mit c *und* n₀. Beide Quantoren gehören dazu.

### Der Satz, den der Prof extra notiert hat

> **„O(1) heißt nicht nur 1 Befehl."**

O(1) bedeutet: die Laufzeit ist **durch eine Konstante beschränkt**, unabhängig von n. Diese Konstante darf 1 sein, 5 sein oder 200 sein. `x & -x` sind drei Befehle und trotzdem O(1). Eine Folge von 12 Shifts und Masken ist O(1), solange die **Anzahl der Befehle nicht von n abhängt**.

Umgekehrt: Wenn du die Wortbreite verdoppelst (32 → 64 Bit) und der Code braucht *deshalb* mehr Schritte, ist er nicht O(1).

### Was ist n bei Bit Wizardry?

> **n = Anzahl der Bits im Wort** (BPL, „bits per long" = 64).

**Das ist die Falle.** Nicht die Anzahl Array-Elemente, nicht der Zahlenwert. Bei einem 64-Bit-Wort ist n = 64. Deshalb:

| Komplexität | bedeutet bei 64 Bit | Beispiel |
|---|---|---|
| O(n) | ~64 Schritte | Bit für Bit durchlaufen (Schleife mit Shift 1) |
| O(log n) | ~6 Schritte | Divide & Conquer (64 → 32 → 16 → 8 → 4 → 2 → 1) |
| O(1) | feste Anzahl, egal ob 32 oder 64 Bit | `x & -x` |

log₂(64) = 6 — merke dir die Zahl, dann siehst du dem Code die Klasse an: **eine Schleife über alle Bits = O(n), eine Kaskade halbierender Masken = O(log n).**

---

## 2. Der Befehlsvorrat (1 CPU-Cycle)

Aus V5 — diese Befehle kosten je einen Cycle:

**XOR, AND, NOT, ADD, SUB, NEG, INC, DEC, SHIFT, ROTATE**

Alles, was du aus diesen zusammensetzt und dessen Anzahl nicht von n abhängt, ist O(1).

**Tipp aus V4:** immer mit `unsigned long` arbeiten, wenn möglich. Bei signed shifts wird das Vorzeichenbit nachgezogen (arithmetischer Shift) — Quelle böser Fehler.

---

## 3. Zweierkomplement — die zwei Formeln

```
~w            alle Bits gekippt (NOT)
-w = ~w + 1   Negation im Zweierkomplement
```

Beispiel aus V5:
```
 w = 011011000
~w = 100100111
-w = 100101000     (= ~w + 1)
```

**Warum das der wichtigste Trick ist:** `-w` kippt alles **oberhalb** des niedrigsten gesetzten Bits, lässt das niedrigste gesetzte Bit selbst und die Nullen darunter aber **unverändert**. Deshalb:

```
w & -w   →  isoliert das niedrigste gesetzte Bit      (O(1))
w & (w-1) →  löscht das niedrigste gesetzte Bit        (O(1))
```

Prüfe an obigem w: `011011000 & 100101000 = 000001000` ✓ — genau das niedrigste gesetzte Bit.

---

## 4. Rotation (V5)

```c
typedef unsigned long ulong;

ulong bit_rotate_right(ulong w, ulong s) {
    constexpr ulong BPL = 64;
    return (w >> s) | (w << (BPL - s));
}
```

Der Prof rechnet es mit **BPL = 6** vor (Spielzeug-Wortbreite, damit man es hinschreiben kann), w = `abcdef`, s = 2:

```
w >> 2        = 00abcd
w << (6-2)=4  = ef0000
OR            = efabcd     ✓ um 2 nach rechts rotiert
```

**Vorsicht (nicht in der Mitschrift, aber klausurrelevant, falls er fragt):** für s = 0 ist `w << 64` in C++ *undefined behavior*. Sauber wäre `(w >> s) | (w << ((BPL - s) & (BPL - 1)))`. Wenn er das nicht behandelt hat, schreib die Vorlesungsversion — aber wisse, warum sie wackelt.

---

## 5. Die drei Komplexitätsklassen an *einer* Aufgabe

V5 stellt genau diese Aufgabe (das ist der didaktische Kern und ein sehr wahrscheinlicher Klausur-Kandidat):

> Gegeben w = `0110100`. Gesucht: `0000100` — **isoliere das niedrigste gesetzte Bit.**

**Variante 1 — O(n): AND + SHIFT 1**
```c
ulong lowest_naiv(ulong w) {
    for (ulong m = 1; m; m <<= 1)   // Maske wandert durch alle n Bits
        if (w & m) return m;
    return 0;
}
```
Schleife läuft im Worst Case über alle n = 64 Bits → **O(n)**.

**Variante 2 — O(log n): Divide & Conquer**
Halbiere den Suchbereich: liegt ein gesetztes Bit in der unteren Hälfte? Wenn ja, dort weitersuchen, sonst in der oberen. log₂(64) = 6 Schritte → **O(log n)**. (So funktioniert auch die Bit-Position-Bestimmung.)

**Variante 3 — O(1): der Zweierkomplement-Trick**
```c
ulong lowest(ulong w) { return w & -w; }
```
Drei Befehle, unabhängig von n → **O(1)**. Und hier siehst du live: O(1), aber eben nicht *ein* Befehl.

> **Merksatz für die Klausur:** Dieselbe Aufgabe in O(n), O(log n) und O(1) — der Unterschied liegt nicht in der Aufgabe, sondern in der Technik: *Schleife über Bits* → O(n), *halbierende Masken* → O(log n), *arithmetischer Trick* → O(1).

---

## 6. popcount (ones_count) — Divide & Conquer (V6)

Die Aufgabe: Zähle die gesetzten Bits. V6 baut das **rekursiv nach Wortbreite** auf. Genau so herleiten, nicht auswendig lernen.

**1 Bit:** Das Wort *ist* schon seine eigene Anzahl (0 → 0, 1 → 1).
```c
uint01_t ones_count(uint01_t x) { return x; }
```

**2 Bit:** Addiere das obere Bit zum unteren.
```c
uint02_t ones_count(uint02_t x) {
    return (x >> 1) & 0b01  +  (x & 0b01);
}
```
Ergebnis steht als 2-Bit-Zahl da (max. 2 = `10`).

**4 Bit:** Erst alle 2er-Blöcke parallel zählen, dann die beiden 2er-Ergebnisse addieren.
```c
uint04_t ones_count(uint04_t x) {
    x = (x >> 1) & 0b0101  +  (x & 0b0101);   // je 2er-Block: Anzahl
    return (x >> 2) + (x & 0b0011);           // die zwei Blöcke addieren
}
```

**Das Muster** (und damit die ganze Klausuraufgabe):

| Schritt | Blockgröße | Maske (4 Bit) | Maske (8 Bit) | Maske (32 Bit) |
|---|---|---|---|---|
| 1 | 1 → 2 | `0101` | `01010101` | `0x55555555` |
| 2 | 2 → 4 | `0011` | `00110011` | `0x33333333` |
| 3 | 4 → 8 | — | `00001111` | `0x0f0f0f0f` |
| 4 | 8 → 16 | — | — | `0x00ff00ff` |
| 5 | 16 → 32 | — | — | `0x0000ffff` |

**Wie du jede Maske selbst herleitest** (nie auswendig!):
Im Schritt „Blöcke der Größe k addieren" brauchst du eine Maske, die **abwechselnd k Einsen und k Nullen** hat:
- k=1: `…010101` → 0x5 pro Nibble → `0x5555…`
- k=2: `…00110011` → 0x3 pro Nibble → `0x3333…`
- k=4: `…00001111` → 0x0f pro Byte → `0x0f0f…`
- k=8: `0x00ff00ff`, k=16: `0x0000ffff`

Merke die Hex-Ziffern **5, 3, f** — der Rest ist nur Wiederholung des Musters über die Wortbreite.

**Anzahl Schritte:** log₂(n). Bei 32 Bit: 5 Schritte. Bei 64 Bit: 6 Schritte → **O(log n)**.

**Referenz aus dem fxtbook (§1.8, S. 18):** Die offizielle 64-Bit-Version, mit der du deine Herleitung kontrollieren kannst — beachte, dass jede Maske *vor und nach* dem Shift angewendet wird:

```c
static inline ulong bit_count(ulong x) {
    x = (0x5555555555555555UL & x) + (0x5555555555555555UL & (x>> 1));  // 0-2 in 2 bits
    x = (0x3333333333333333UL & x) + (0x3333333333333333UL & (x>> 2));  // 0-4 in 4 bits
    x = (0x0f0f0f0f0f0f0f0fUL & x) + (0x0f0f0f0f0f0f0f0fUL & (x>> 4));  // 0-8 in 8 bits
    x = (0x00ff00ff00ff00ffUL & x) + (0x00ff00ff00ff00ffUL & (x>> 8));  // 0-16 in 16 bits
    x = (0x0000ffff0000ffffUL & x) + (0x0000ffff0000ffffUL & (x>>16));  // 0-32 in 32 bits
    x = (0x00000000ffffffffUL & x) + (0x00000000ffffffffUL & (x>>32));  // 0-64 in 64 bits
    return x;
}
```

Das fxtbook zeigt danach (§1.8, S. 19) eine optimierte Variante, bei der ab Schritt 3 die Maskierung wegfallen darf (die Blocksummen können nicht mehr überlaufen) — nice to know, aber für die Klausur reicht die saubere Grundform.

### 32 → 64 Bit verdoppeln (steht wörtlich in den Prüfungsthemen!)

Zwei Dinge ändern sich, sonst nichts:
1. **Masken verlängern:** `0x55555555` → `0x5555555555555555` (8 → 16 Hex-Ziffern). Das Muster bleibt identisch, es wiederholt sich nur doppelt so oft.
2. **Ein Schritt mehr:** zusätzlich der Schritt „32 → 64" mit Maske `0x00000000ffffffff`.

Das ist die ganze Antwort. Wenn er fragt „wie machen Sie das für 64 Bit?" — genau diese zwei Sätze.

---

## 7. Shift-and-Add-Multiplikation (V5, Aufgabe)

Multiplikation nur mit SHIFT und ADD — die Schulmethode zur Basis 2:

```c
ulong mul(ulong a, ulong b) {
    ulong r = 0;
    while (b) {
        if (b & 1) r += a;   // Bit gesetzt → a addieren
        a <<= 1;             // a verdoppeln
        b >>= 1;             // nächstes Bit
    }
    return r;
}
```
Läuft über alle Bits von b → **O(n)**.

---

# Teil B — Übungen

Erst selbst rechnen, Lösungen in `S1_Bit_Wizardry_Loesungen.md`.

### Ü1 — O-Definition
Schreibe die Definition von O(f(n)) exakt hin (mit allen Quantoren). Erkläre in einem Satz, warum `x & -x` O(1) ist, obwohl es drei Befehle sind.

### Ü2 — Was ist n?
Ein Kommilitone sagt: „popcount ist O(log n), also bei einem Array mit 1000 Zahlen etwa 10 Schritte." Was ist an dem Satz falsch?

### Ü3 — Zweierkomplement von Hand
w = `0101 1000` (8 Bit). Berechne `~w`, `-w`, `w & -w`, `w & (w-1)`. Was bewirken die letzten beiden?

### Ü4 — Rotation
Sei BPL = 8, w = `1101 0011`, s = 3. Berechne `bit_rotate_right(w, s)` schrittweise (w>>s, w<<(BPL−s), OR).

### Ü5 — Klassifizieren
Gib für jeden Code die O-Klasse an (n = Bits im Wort) und begründe in einem Satz:
```c
a)  ulong f(ulong w){ ulong c=0; while(w){ c += w&1; w >>= 1; } return c; }
b)  ulong g(ulong w){ ulong c=0; while(w){ w &= w-1; ++c; } return c; }
c)  ulong h(ulong w){ return w & -w; }
d)  bool  p(ulong w){ return (w & (w-1)) == 0; }
```
(Bei b): Was zählt die Schleife? Wovon hängt die Schrittzahl ab — von n oder von etwas anderem?)

### Ü6 — Masken herleiten
Leite die popcount-Masken für **16 Bit** her (alle 4 Schritte, binär *und* hex). Schreibe dann die vollständige 16-Bit-popcount-Funktion.

### Ü7 — Die Prüfungsfrage
Gegeben ist eine fertige 32-Bit-popcount-Funktion mit den Masken 0x55555555, 0x33333333, 0x0f0f0f0f, 0x00ff00ff, 0x0000ffff. **Was müssen Sie ändern, damit sie für 64-Bit-Worte funktioniert?** Antworte präzise in zwei Punkten und gib die neuen Masken an.

### Ü8 — Niedrigstes gesetztes Bit, drei Wege
Schreibe für „isoliere das niedrigste gesetzte Bit" je eine Lösung in O(n) und in O(1). Begründe für jede die Klasse.

### Ü9 — Shift-and-Add
Rechne `mul(a=5, b=6)` mit der Shift-and-Add-Funktion von Hand durch (Tabelle: a, b, r nach jedem Durchlauf).

---

# Teil C — Warm-up Mittwoch (Ü10–Ü17)

Neue Aufgaben für die Wiederholung am Mi 15.07. — gezielt auf die Schwachstellen aus Session 1. Lösungen wieder in `S1_Bit_Wizardry_Loesungen.md`.

### Ü10 — Die Rolle von n₀
Ein Algorithmus braucht T(n) = 2ⁿ Schritte für n < 8, aber T(n) = 5n Schritte für alle n ≥ 8. Ist er O(n)? Begründe mit der Definition und gib konkrete Werte für c und n₀ an.

### Ü11 — Ohne Schleife heißt nicht O(1)
Zwei Code-Stücke, beide **ohne Schleife**:
a) 40 fest hingeschriebene XOR/ADD/SHIFT-Befehle nacheinander — egal, wie breit das Wort ist, es bleiben 40 Befehle.
b) Ein „ausgerollter" popcount für 64 Bit: die 6 Maskenschritte stehen einzeln untereinander im Code (keine Schleife). Für ein 128-Bit-Wort bräuchte man einen 7. Schritt.
Gib für beide die O-Klasse an (n = Bits im Wort) und begründe je in ein bis zwei Sätzen.

### Ü12 — Rotation, neues w
BPL = 8, w = `1001 0110`, s = 5. Berechne `bit_rotate_right(w, s)` schrittweise (w>>s, w<<(BPL−s), OR). **Selbsttest:** Einsen zählen vor und nach der Rotation.

### Ü13 — Finde den Bug
Diese Zeile soll der erste popcount-Schritt für 8 Bit sein (2er-Blöcke zählen):
```c
x = (x >> 1) & 0x55 + (x & 0x55);
```
Sie liefert falsche Ergebnisse. Warum? Schreibe die korrigierte Zeile hin.

### Ü14 — Zweierkomplement, neues w
w = `0110 1100` (8 Bit). Berechne `~w`, `-w`, `w & -w`, `w & (w-1)`.
**Zusatz:** Der Test `(w & (w-1)) == 0` aus Ü5d meldet auch für w = 0 „Zweierpotenz". Repariere ihn zu einem O(1)-Test „genau ein Bit gesetzt".

### Ü15 — Verdopplung in die andere Richtung
Jemand baut den 64-Bit-popcount auf **128-Bit-Worte** um. Wie viele Schritte hat die neue Funktion, was ändert sich an den Masken, und wie sieht die Maske des neuen letzten Schritts aus (Muster genügt)? Begründe die O-Klasse — der Schluss „Blockgröße verdoppelt sich pro Schritt ⇒ log₂(n) Schritte" muss vorkommen.

### Ü16 — Klassifizieren II
Gib für jeden Code die O-Klasse an (n = Bits im Wort) und begründe in einem Satz. Sage bei a) und b) auch, *was* die Funktion berechnet:
```c
a)  ulong f(ulong w){ ulong c=0; for(ulong i=0; i<64; ++i) c += (w>>i)&1; return c; }
b)  ulong g(ulong w){ ulong c=0; while(w>1){ w>>=1; ++c; } return c; }
c)  ulong h(ulong w){ return (w>>7) | (w<<57); }        // BPL = 64
d)  bool  q(ulong w){ return (w & 1) == 0; }
```

### Ü17 — Shift-and-Add II
Rechne `mul(a=9, b=5)` von Hand durch (Tabelle wie in Ü9). Wie viele Schleifendurchläufe sind es genau, und wovon hängt diese Zahl ab?
