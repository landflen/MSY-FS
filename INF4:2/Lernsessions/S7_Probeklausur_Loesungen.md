# S7 — Probeklausur, Lösungen

Bewertung: pro Aufgabe die genannten Punkte; bei Rechenaufgaben ~die Hälfte für den Ansatz, Rest für saubere Durchführung + Schlusssatz.

---

## Teil: ASYMPTOTIK & BIT WIZARDRY

**A1** T(n) ∈ O(f(n)) :⇔ es gibt ein **c > 0** und ein **n₀**, sodass **T(n) ≤ c·f(n) für alle n ≥ n₀**. (Alle drei Bestandteile nennen: c, n₀, „für alle n ≥ n₀" — 1 P Abzug pro fehlendem Stück.)

**A2**
a) **O(n)** — die Maske m wandert durch alle n Bits, die Schleife läuft n-mal.
b) **O(log n)** — Blockgröße verdoppelt sich pro Schritt (1→2→4→…→64) ⇒ log₂(n) Schritte, bei 64 Bit 6. *(Der Schluss „Verdopplung ⇒ log₂(n)" muss dastehen.)*
c) **O(1)** — zwei Befehle (SUB, AND), Anzahl unabhängig von n. (Löscht das niedrigste gesetzte Bit.)

**A3** Zwei Änderungen, sonst nichts:
1. **Masken auf 16 Hex-Ziffern verlängern** — das Muster wiederholt sich doppelt so oft: 0x5555555555555555, 0x3333333333333333, 0x0f0f0f0f0f0f0f0f, 0x00ff00ff00ff00ff, 0x0000ffff0000ffff.
2. **Ein Schritt mehr** (32 → 64) mit der neuen Maske 0x00000000ffffffff.

**A4** w = `0110 1000`:
- `~w` = `1001 0111` (alle Bits gekippt)
- `-w` = `~w + 1` = `1001 1000`
- `w & -w` = `0110 1000 & 1001 1000` = **`0000 1000`** — isoliert das **niedrigste gesetzte Bit**.
- **O(1):** feste Befehlszahl (NEG, AND), unabhängig von der Wortbreite.

---

## Teil: CODE-OPTIMIERUNG

**B1** `SHIFT`, `ADD` (1 Cycle) < `MUL` (wenige Cycles) < `DIV`, `pow` (**50–300 Cycles**). *(Größenordnung muss als Zahl dastehen, „sehr teuer" allein gibt Abzug.)*

**B2**
```c
double inv = 1.0 / d;                  // 1 Division vorab statt N
for (int i = 0; i < N; ++i) {
    double t = x[i];
    y[i] = t*t*t * inv;                // pow(·,3) → zwei MUL
}
```
Maßnahme 1: **pow durch Multiplikation ersetzen** — pow ist ein transzendenter Aufruf (50–300 Cycles), t·t·t sind zwei billige MUL.
Maßnahme 2: **Division durch Multiplikation mit dem Kehrwert** — statt N teuren DIV nur eine Division vorab, in der Schleife nur noch MUL.

**B3** **Latency** = Zeit, die *ein* Befehl bis zum Ergebnis braucht (Cycles im Prozessor). **Throughput** = Rate, mit der Befehle *fertig werden* (Befehle pro Cycle). Ja — die Ausführungseinheit ist eine Pipeline: ein einzelnes MUL braucht 3 Cycles, aber jeden Cycle kann ein neues starten, also wird ab dem 3. Cycle jeden Cycle eines fertig. *(Wichtig: das eine folgt nicht aus dem anderen.)*

**B4** Bei einer einzigen Summe hängt jede Addition vom Ergebnis der vorigen ab (**Datenabhängigkeit**) — die CPU muss warten. Die vier Teilsummen sind **unabhängig**, also rechnet die superskalare CPU sie **parallel in mehreren Addierern**; am Ende werden die Teilsummen einmal zusammengeführt.

---

## Teil: RELATIONEN

**C1** Rundungsfehler: zwei Rechenwege, die exakt dasselbe ergeben müssten, liefern doubles, die sich in späten Nachkommastellen unterscheiden — `==` ist dann false. Richtig: Toleranzvergleich `abs(a − b) <= eps` (z. B. eps = 1e-9).

**C2** Eine ÄR muss reflexiv, symmetrisch, transitiv sein.
- **Reflexiv:** |a − a| = 0 ≤ eps für alle a ✓
- **Symmetrisch:** |a − b| = |b − a|, also folgt aus a ~ b sofort b ~ a ✓
- **Transitiv:** ✗. Gegenbeispiel: x = 0, y = eps, z = 2·eps:
  - |x − y| = eps ≤ eps ⇒ x ~ y ✓
  - |y − z| = eps ≤ eps ⇒ y ~ z ✓
  - |x − z| = 2·eps > eps ⇒ x ≁ z ✗
Die Transitivität ist verletzt ⇒ **keine Äquivalenzrelation**. ∎
*(Konkrete Zahlen sind Pflicht — mit eps = 1 also 0, 1, 2. Punktschema: je 1 P für R und S, 3 P für das Gegenbeispiel mit Schlusssatz.)*

---

## Teil: NICHT-LINEARE ITERATIONEN

**D1** f(x) = 1/x − d, f'(x) = −1/x².
```
N(x) = x − (1/x − d)/(−1/x²) = x + x²·(1/x − d) = x + x − dx² = 2x − dx² = x(2 − dx)
```
Im Ergebnis kommt **keine Division** mehr vor — nur MUL und SUB. Das ist der Witz: die Iteration berechnet 1/d, *ohne* zu dividieren (genau so machen es FPUs; DIV kostet 50–300 Cycles, MUL wenige).

**D2** Fixpunkt: N(1/d) = (1/d)·(2 − d·(1/d)) = (1/d)·(2 − 1) = **1/d** ✓ (FP)
Ableitung: N'(x) = 2 − 2dx, also N'(1/d) = 2 − 2 = **0** ✓ (SA) ∎

**D3** N(0) = 0·(2 − 0) = **0** ✓ — ja, Fixpunkt. N'(0) = 2 − 0 = **2** ⇒ **nicht superattraktiv**, sondern repulsiv (|N'(0)| = 2 > 1). Das ist gut: der unerwünschte Fixpunkt stößt ab, die Iteration läuft von selbst zu 1/d.

---

## Selbst-Auswertung

| Punkte | Einschätzung |
|---|---|
| ≥ 40 | klausurfertig — Rest der Zeit in ED/andere Fächer |
| 32–39 | gut; die verlorenen Aufgaben gezielt in S6/Sessions nacharbeiten |
| < 32 | Lücken-Themen identifizieren, zugehörige Session wiederholen, zweiter Durchlauf mit dem So-Puffer |
