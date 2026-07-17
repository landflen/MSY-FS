# S7 — Probeklausur (von Claude erstellt, nicht original!)

Format und Ton nach `INF4_KlausurSS16.pdf`, Inhalte exakt entlang der Prüfungsthemen 2026 (Newton, Bit Wizardry, Code-Optimierung, Asymptotik, Relationen — kein Prim, keine Gruppen).
**Bearbeitung: 45-Minuten-Wecker stellen** (das ist das Tempo, das der Prof erwartet — real hast du 90 Min.). 45 Punkte ≈ 1 Punkt/Minute. Lösungen in `S7_Probeklausur_Loesungen.md` — erst nach dem Wecker aufmachen.

---

```
Probeklausur "Low level und seminumerische Algorithmen"

  Bearbeitungszeit: 90 Minuten (Ziel: 45)
  Hilfsmittel: Alles, was aus Papier besteht.
```

---

## Teil: ASYMPTOTIK & BIT WIZARDRY  (16 P)

**A1** (3 P) Geben Sie die Definition an: Wann ist ein Algorithmus mit Laufzeit T(n) in O(f(n))? (Alle Bestandteile der Definition!)

**A2** (6 P) Geben Sie für jede Funktion die Komplexitätsklasse an (n = Anzahl Bits im Wort) und begründen Sie in je einem Satz:
```c
a)  ulong f(ulong w){ ulong c=0; for(ulong m=1; m; m<<=1) if(w&m) ++c; return c; }
b)  ulong g(ulong w){                    // popcount, 64 Bit
        x = (0x55…55 & x) + (0x55…55 & (x>>1));
        x = (0x33…33 & x) + (0x33…33 & (x>>2));
        …                                // insgesamt 6 solche Zeilen
        return x; }
c)  ulong h(ulong w){ return w & (w-1); }
```

**A3** (4 P) Eine 32-Bit-popcount-Funktion arbeitet mit den Masken 0x55555555, 0x33333333, 0x0f0f0f0f, 0x00ff00ff, 0x0000ffff. Was müssen Sie ändern, damit sie für 64-Bit-Worte funktioniert? (Zwei Punkte nennen; neue Masken angeben — Muster genügt.)

**A4** (3 P) Sei w = `0110 1000` (8 Bit). Berechnen Sie `~w`, `-w` und `w & -w`. Was bewirkt der letzte Ausdruck, und in welcher O-Klasse liegt er?

---

## Teil: CODE-OPTIMIERUNG  (12 P)

**B1** (3 P) Ordnen Sie nach Kosten (billig → teuer): `DIV`, `ADD`, `pow`, `MUL`, `SHIFT`. Geben Sie für die teuerste Gruppe die Größenordnung in Cycles an.

**B2** (5 P) Optimieren Sie diese Schleife (N groß). Nennen Sie beide Maßnahmen und begründen Sie kurz, warum sie schneller sind:
```c
for (int i = 0; i < N; ++i)
    y[i] = pow(x[i], 3) / d;
```

**B3** (2 P) Definieren Sie Latency und Throughput (je ein Satz). Kann ein Befehl Latency 3 und Throughput 1 pro Cycle haben? (Ein Begründungssatz.)

**B4** (2 P) Warum ist die Summation mit vier Teilsummen s0…s3 (Loop Unrolling) auf einer superskalaren CPU schneller als eine einzige Summe, obwohl beide gleich viele Additionen ausführen?

---

## Teil: RELATIONEN  (7 P)

**C1** (2 P) Warum ist `if (a == b)` für zwei berechnete double-Werte gefährlich? Wie vergleicht man stattdessen?

**C2** (5 P) Zeigen Sie, dass die Relation aus C1, also **a ~ b :⇔ |a − b| ≤ eps** (eps > 0 fest), **keine** Äquivalenzrelation auf ℝ ist. Prüfen Sie alle drei Eigenschaften; geben Sie für die verletzte ein konkretes Gegenbeispiel an.

---

## Teil: NICHT-LINEARE ITERATIONEN  (10 P)

> Gegeben: Newton-Iteration **N(x) = x − f(x)/f'(x)** · Fixpunkt: N(x\*) = x\* · superattraktiv: N'(x\*) = 0 · Quotientenregel: (u/v)' = (u'v − v'u)/v²

**D1** (4 P) Sei **f(x) = 1/x − d** (also f(r) = 0 für r = 1/d). Berechnen Sie N(x) = x − f(x)/f'(x) und vereinfachen Sie so weit wie möglich. Welche teure Operation kommt im Ergebnis *nicht* mehr vor — und warum ist das der Witz dieser Iteration?

**D2** (4 P) Zeigen Sie, dass 1/d ein superattraktiver Fixpunkt von N ist.

**D3** (2 P) Hat N einen Fixpunkt bei 0? (Falls ja: ist dieser superattraktiv?)

---

```
(Ende der Klausur)
```
