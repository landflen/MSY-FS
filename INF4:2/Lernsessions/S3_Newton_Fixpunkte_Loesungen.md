# Session 3 — Lösungen

(Ü1–Ü3 entsprechen der Musterlösung in `INF4_KlausurSS16.pdf`, S. 3–4.)

### Ü1 — Newton allgemein
Fixpunkt: N(r) = r − f(r)/f'(r) = r − 0/f'(r) = **r** ✓
Superattraktiv? Ableiten mit Quotientenregel, (f/f')' = (f'·f' − f·f'')/(f')²:
```
N'(x) = 1 − [ (f')² − f·f'' ] / (f')²  =  1 − 1 + f·f''/(f')²  =  f(x)·f''(x)/f'(x)²
```
An der Stelle r: **N'(r) = f(r)·f''(r)/f'(r)² = 0**, da f(r) = 0 und f'(r) ≠ 0 ⇒ superattraktiv. ∎

### Ü2 — N(x) = x + x(1 − dx)
**a)** Fixpunkt: N(1/d) = 1/d + (1/d)·(1 − d·(1/d)) = 1/d + (1/d)·0 = **1/d** ✓ (FP)
Ableitung (Produktregel):
```
N'(x) = 1 + 1·(1 − dx) + x·(−d) = 2 − 2dx
```
N'(1/d) = 2 − 2 = **0** ✓ (SA)
**b)** N(−1/d) = −1/d + (−1/d)·(1 − d·(−1/d)) = −1/d + (−1/d)·2 = **−3/d ≠ −1/d** ⇒ **kein Fixpunkt** (Frage nach SA entfällt).
**c)** N(0) = 0 + 0·(1 − 0) = **0** ✓ (FP). N'(0) = 2 − 0 = **2** ⇒ **nicht superattraktiv** — sogar repulsiv, denn |N'(0)| = 2 > 1.

### Ü3 — f(x) = 1/x² − d
**a)** f'(x) = −2/x³.
```
N(x) = x − (1/x² − d)/(−2/x³) = x + (x³/2)·(1/x² − d) = x + (x − dx³)/2
     = x + x·(1 − dx²)/2
```
**b)** Mit dr² = d·(1/d) = 1:
N(r) = r + r·(1 − dr²)/2 = r + r·0/2 = **r** ✓ (FP)
Nebenrechnung wie in der Musterlösung:
```
N'(x) = 1 + (1 − dx²)/2 + x·(−2dx)/2 = 1 + ½ − ½dx² − dx² = 3/2 − (3/2)dx²
      = (3/2)(1 − dx²)
```
N'(r) = (3/2)(1 − 1) = **0** ✓ (SA)
**c)** N(−r) = −r + (−r)·(1 − d·r²)/2 = −r + 0 = **−r** ✓ (FP, da (−r)² = r²).
N'(−r) = (3/2)(1 − dr²) = **0** ✓ (SA)

### Ü4 — f(x) = 1/x³ − d
**a)** f'(x) = −3/x⁴.
```
N(x) = x − (1/x³ − d)/(−3/x⁴) = x + (x⁴/3)·(1/x³ − d) = x + (x − dx⁴)/3
     = x + x·(1 − dx³)/3
```
**b)** Mit dr³ = d·(1/d) = 1:
N(r) = r + r·(1 − dr³)/3 = r + 0 = **r** ✓ (FP)
```
N'(x) = 1 + (1 − dx³)/3 + x·(−3dx²)/3 = 1 + ⅓ − ⅓dx³ − dx³ = 4/3 − (4/3)dx³
      = (4/3)(1 − dx³)
```
N'(r) = (4/3)(1 − 1) = **0** ✓ (SA)
**c)** N(0) = 0 + 0 = **0** ✓ (FP). N'(0) = **4/3 > 1** ⇒ nicht superattraktiv, sondern repulsiv — gut, denn der unerwünschte Fixpunkt stößt ab.

---

# Teil C

### Ü5 — Fixpunkt-Typen für Φ(x) = x²/4
Fixpunkte: x²/4 = x ⇒ x(x − 4) = 0 ⇒ **x\* = 0** und **x\* = 4**.
Φ'(x) = x/2.
- x\* = 0: Φ'(0) = 0 → **superattraktiv**.
- x\* = 4: Φ'(4) = 2 > 1 → **repulsiv**.

### Ü6 — ε-Entwicklung für 1/d
x = (1/d)(1+ε):
```
N = (1/d)(1+ε)·[2 − d·(1/d)(1+ε)] = (1/d)(1+ε)(2 − 1 − ε)
  = (1/d)(1+ε)(1 − ε) = (1/d)(1 − ε²)
```
⇒ **α = 0, β = −1**. α = 0 heißt: der Fehler erster Ordnung verschwindet ⇒ **superattraktiv** (V8: α = 0 ⟺ SA). Der ε²-Term bedeutet quadratische Konvergenz — die **Anzahl korrekter Stellen verdoppelt sich** pro Schritt (aus ε = 10⁻⁴ wird ε² = 10⁻⁸).

### Ü7 — ε-Entwicklung für 1/√d
x = r(1+ε), dabei dr² = 1 nutzen, also d·r²(1+ε)² = (1+ε)²:
```
N = r(1+ε) + r(1+ε)·[1 − (1+ε)²]/2
  = r(1+ε)·[1 + (1 − 1 − 2ε − ε²)/2]
  = r(1+ε)(1 − ε − ε²/2)
  = r(1 − ε − ε²/2 + ε − ε² − ε³/2)
  = r(1 − 3/2·ε² − 1/2·ε³)
```
⇒ **α = 0, β = −3/2, γ = −1/2** (genau die Zielform aus V7). α = 0 ⇒ **superattraktiv**, quadratische Konvergenz.

### Ü8 — Naiver Ansatz
f(x) = x − 1/d, f'(x) = 1 ⇒ N(x) = x − (x − 1/d)/1 = **1/d**.
Sinnlos, weil N das Ergebnis 1/d bereits **explizit enthält** — man müsste die Division schon ausgeführt haben, um die Iteration hinschreiben zu können.

### Ü9 — √d
**a)** f'(x) = 2x.
```
N(x) = x − (x² − d)/(2x) = (2x² − x² + d)/(2x) = ½(x + d/x)
```
**b)** N(√d) = ½(√d + d/√d) = ½(√d + √d) = **√d** ✓ (FP).
N'(x) = ½(1 − d/x²), N'(√d) = ½(1 − 1) = **0** ✓ (SA).
**c)** N enthält **d/x — eine Division pro Schritt**, genau die Operation, die vermieden werden soll. Stattdessen (V8 „Verbessert"): **√d = d·(1/√d)**, und 1/√d divisionsfrei mit N = x + x(1 − dx²)/2 aus Ü3 — nur Multiplikation, Subtraktion, Halbieren (Shift).

### Ü10 — Allgemeine inverse Wurzel
**a)** f'(x) = −a/x^(a+1).
```
N(x) = x − (1/xᵃ − d)/(−a/x^(a+1)) = x + (x^(a+1)/a)·(1/xᵃ − d)
     = x + x·(1 − dxᵃ)/a
```
**b)** Für x = d^(−1/a) ist dxᵃ = 1 ⇒ N(x) = x + x·0/a = **x** ✓ (FP).
**c)** a = 1: N = x + x(1 − dx) — Ü2 ✓ · a = 2: N = x + x(1 − dx²)/2 — Ü3 ✓ · a = 3: N = x + x(1 − dx³)/3 — Ü4 ✓
