# Session 3 — Lösungen

### Ü1 — Fixpunkt-Typen für Φ(x) = x²/4
Fixpunkte: x²/4 = x ⇒ x² = 4x ⇒ x(x−4) = 0 ⇒ **x\* = 0** und **x\* = 4**.
Φ'(x) = x/2.
- x\* = 0: Φ'(0) = 0 → **superattraktiv**.
- x\* = 4: Φ'(4) = 2 > 1 → **repulsiv**.

### Ü2 — Newton allgemein
Φ(x) = x − f/f'. Ableiten, mit Quotientenregel (f/f')' = (f'·f' − f·f'')/(f')² = 1 − f·f''/(f')²:
```
Φ'(x) = 1 − [1 − f·f''/(f')²] = f(x)·f''(x)/f'(x)²
```
An einfacher Nullstelle r ist f(r) = 0, also **Φ'(r) = 0·f''(r)/f'(r)² = 0** (da f'(r) ≠ 0). Der Zählerfaktor f(r) macht die ganze Ableitung null ⇒ superattraktiv ⇒ quadratische Konvergenz.

### Ü3 — Konvergenzordnung
ε¹-Koeffizient ist 0, kleinster nicht-verschwindender Term ist ε² (Koeffizient −½ ≠ 0) ⇒ **quadratische Konvergenz** (Ordnung 2). Der ε³-Term ist nur eine Korrektur höherer Ordnung.

### Ü4 — Newton für 1/d
**a)** f(x) = 1/x − d, f'(x) = −1/x².
```
Φ(x) = x − (1/x − d)/(−1/x²) = x + x²(1/x − d) = x + x − dx² = 2x − dx² = x(2 − dx)
```
**b)** Φ(1/d) = (1/d)(2 − d·(1/d)) = (1/d)(2 − 1) = 1/d ✓
**c)** Φ'(x) = 2 − 2dx; Φ'(1/d) = 2 − 2d·(1/d) = 2 − 2 = 0 ✓ → superattraktiv.
**d)** x = (1/d)(1+ε):
```
Φ = (1/d)(1+ε)[2 − d·(1/d)(1+ε)] = (1/d)(1+ε)(2 − 1 − ε)
  = (1/d)(1+ε)(1 − ε) = (1/d)(1 − ε²)
```
α₁ = 0, α₂ = −1 ⇒ **quadratisch** ✓

### Ü5 — Warum nicht naiv
f(x) = x − 1/d, f'(x) = 1. Φ(x) = x − (x − 1/d)/1 = **1/d**.
Sinnlos, weil Φ das Ergebnis 1/d bereits **explizit enthält** — man müsste 1/d schon kennen, um es auszurechnen. Kein Algorithmus, nur eine Tautologie.

### Ü6 — √d
**a)** f(x) = x² − d, f'(x) = 2x.
```
Φ(x) = x − (x² − d)/(2x) = (2x² − x² + d)/(2x) = (x² + d)/(2x) = ½(x + d/x)
```
**b)** Φ(√d) = ½(√d + d/√d) = ½(√d + √d) = √d ✓
**c)** Φ'(x) = ½(1 − d/x²); Φ'(√d) = ½(1 − d/d) = ½·0 = 0 ✓ → superattraktiv.
**d)** Φ enthält den Term **d/x**, also eine **Division** — genau die Operation, die man vermeiden wollte. Umgehung: **√d = d·(1/√d)** und 1/√d divisionsfrei über f(x) = 1/x² − d berechnen, Φ(x) = (x/2)(3 − dx²). Dann nur Multiplikationen, Subtraktion und Halbieren (Bit-Shift).

### Ü7 — Geometrie
Tangente an f in x_k: y = f(x_k) + f'(x_k)(x − x_k). Der nächste Iterationswert ist der Nulldurchgang, also y = 0 setzen und nach x auflösen:
```
0 = f(x_k) + f'(x_k)(x − x_k)  ⇒  x = x_k − f(x_k)/f'(x_k) = Φ(x_k)
```
Also ist Φ(x_k) genau der x-Achsenschnittpunkt der Tangente — man ersetzt f lokal durch seine Tangente und nimmt deren Nullstelle als bessere Näherung.
