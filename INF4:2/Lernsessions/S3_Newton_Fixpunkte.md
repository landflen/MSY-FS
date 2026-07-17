# Session 3 — Do 16.07., 3 h · Newton & Fixpunkte (Erstkontakt)

**Quellen:** `V7.pdf` + `V8.pdf` · **Prüfungsthema:** Newton-Iteration

---

# Teil A — Kompaktskript

## 1. Fixpunkt

Iteration: wähle x₀, dann **x_{k+1} = Φ(x_k)**. Man hofft, dass die Folge konvergiert.

> **x\* heißt Fixpunkt von Φ, wenn Φ(x\*) = x\*.**

Geometrisch: Schnittpunkt der Kurve y = Φ(x) mit der Diagonalen y = x (Cobweb-Diagramm).

## 2. Die drei Typen — die Kerntabelle

Setze x = x\* + ε (kleiner Fehler). Taylor: Φ(x\* + ε) ≈ x\* + Φ'(x\*)·ε.
→ Der Fehler wird pro Schritt mit **Φ'(x\*)** multipliziert.

| Typ | Bedingung | Fehler pro Schritt |
|---|---|---|
| **attraktiv** (anziehend) | \|Φ'(x\*)\| < 1 | schrumpft → Konvergenz |
| **repulsiv** (abstoßend) | \|Φ'(x\*)\| > 1 | wächst → Divergenz |
| **superattraktiv** | Φ'(x\*) = 0 | schrumpft *sehr* schnell |

Merkhilfe Skizze: attraktiv = flache Kurve schneidet Diagonale, repulsiv = steile Kurve, superattraktiv = waagrechte Tangente am Schnittpunkt.

## 3. Konvergenzordnung — das Klausurwerkzeug

In V8-Schreibweise: N((1/d)(1+ε)) = (1/d)(1+αε+βε²+…) mit **α = 0 ⟺ superattraktiv**.

Bei Fixpunkt x\* ≠ 0 nimmt man den **relativen** Fehler: setze **x = x\*(1 + ε)**.

> Die Iteration hat **Konvergenzordnung n**, wenn
> **Φ(x\*(1+ε)) = x\*(1 + α·εⁿ + O(εⁿ⁺¹))** mit α ≠ 0.

Äquivalent: Φ'(x\*) = Φ''(x\*) = … = Φ⁽ⁿ⁻¹⁾(x\*) = 0, aber Φ⁽ⁿ⁾(x\*) ≠ 0.

| Ordnung n | Name | Fehler |
|---|---|---|
| 1 (\|α\|<1) | linear | ε_{k+1} ≈ α·ε_k (konstant viele Stellen/Schritt) |
| 2 | quadratisch | ε_{k+1} ≈ α·ε_k² (**Stellen verdoppeln sich**) |
| 3 | kubisch | ε_{k+1} ≈ α·ε_k³ (verdreifachen) |

> **Das Klausurrezept:** setze x = x\*(1+ε) in Φ ein, entwickle nach ε, lies den **kleinsten nicht-verschwindenden Koeffizienten** ab → das ist die Ordnung. Verschwindet der ε¹-Term (α₁=0), ist es mindestens quadratisch.

**Warnung zur Notation:** die Schreibweise x\*(1+ε) funktioniert **nur für x\* ≠ 0**. Bei x\* = 0 (z. B. Φ(x)=x²) nimmt man den absoluten Fehler ε_{k+1} = ε_k².

## 4. Beispiel Φ(x) = x²  (zum Verständnis)
Fixpunkte: x\* = 0 und x\* = 1.
- x\* = 0: Φ'(0) = 0 → **superattraktiv**. Startwert 0,1 → 10⁻², 10⁻⁴, 10⁻⁸, 10⁻¹⁶: Nullen verdoppeln sich → quadratisch.
- x\* = 1: Φ'(1) = 2 → **repulsiv**.

**Basin der Attraktion** = Menge aller Startwerte x₀, die gegen x\* konvergieren. Bei z² in ℂ: |z₀|<1 → 0, |z₀|>1 → ∞, |z₀|=1 → bleibt auf dem Kreis. Für kompliziertere Iterationen ist der Rand **fraktal** (Newton-Fraktale) — die zackige Skizze aus V7 ist realistisch.

---

## 5. Newton-Verfahren — die Konstruktion

**Idee:** Gegeben f mit Nullstelle r (f(r) = 0). Baue ein Φ, das dort einen **superattraktiven** Fixpunkt hat.

> **Newton-Iteration:  Φ(x) = x − f(x)/f'(x)**

**Fixpunkt?** Φ(r) = r − f(r)/f'(r) = r − 0 = r ✓ (die Nullstelle von f ist Fixpunkt von Φ).

**Superattraktiv?** Mit Quotientenregel (f/f')' = 1 − f·f''/(f')²:
```
Φ'(x) = 1 − (1 − f·f''/(f')²) = f(x)·f''(x) / f'(x)²
```
An der Nullstelle: Φ'(r) = **0·f''(r)/f'(r)² = 0** (falls f'(r) ≠ 0). ✓

> **Bei einfacher Nullstelle ist Newton quadratisch konvergent** — die Anzahl korrekter Stellen verdoppelt sich pro Schritt. Das ist die zentrale Aussage.

**Geometrisch:** Φ(x_k) = Schnittpunkt der **Tangente** an f in x_k mit der x-Achse.

---

## 6. Der Standardablauf für jede Newton-Aufgabe

Immer diese vier (bzw. fünf) Schritte — das ist die Struktur, die der Prof sehen will:

1. **Nullstelle formulieren:** finde f, dessen Nullstelle die gesuchte Größe t ist.
2. **Newton aufstellen:** f'(x) bilden, Φ(x) = x − f(x)/f'(x), **vereinfachen**.
3. **Fixpunkt prüfen:** Φ(t) = t nachrechnen.
4. **Superattraktivität zeigen:** entweder Φ'(t) = 0, **oder** x = t(1+ε) einsetzen und zeigen, dass der ε¹-Term verschwindet.
5. (evtl.) **Konvergenzordnung** aus der ε-Entwicklung ablesen.

---

## 7. Die drei Klausur-Klassiker (hier rechnen, Fr in Session 4 vertiefen)

Alle drei berechnen etwas **ohne** die teure Operation (Division/Wurzel) — das ist der Sinn: FPUs machen Division und Wurzel intern genau so.

| gesucht | f(x) | Newton Φ(x) | nur mit |
|---|---|---|---|
| **1/d** | 1/x − d | **x(2 − dx)** | Mult, Sub |
| **√d** | x² − d | ½(x + d/x) | (enthält noch /x!) |
| **1/√d** | 1/x² − d | **(x/2)(3 − dx²)** | Mult, Sub, Shift |

Alle drei Zeilen stehen so in `V8.pdf` (dort N = x + x(1−dx) bzw. N = x + x(1−dx²)/2 — algebraisch identisch); die 1/√d-Zeile hat der Prof orange mit **„Klausur"** markiert. Außerdem in V8: x = 0 ist ebenfalls Fixpunkt von x(2−dx), aber N'(0) = 2 → **repulsiv** — „gut, weil der unerwünschte Fixpunkt abstößt". Das ist eine beliebte Zusatzfrage.

**Feinheit √d (wichtig, Prof fragt das):** Der direkte Weg f = x²−d liefert Φ = ½(x + d/x) — enthält noch eine **Division d/x**. Deshalb rechnet man √d *nicht* direkt, sondern über **√d = d · (1/√d)** und berechnet 1/√d mit der divisionsfreien dritten Zeile. Das ist die Pointe der Aufgabe „warum taugt die direkte Iteration nicht als Antwort?".

**Verifikation 1/d** (steht wörtlich in V7 S. 2 und V8 S. 1 — vom Prof rot als „Klausuraufgabe" markiert):
Setze x = (1/d)(1+ε) in Φ(x) = x(2−dx):
```
Φ = (1/d)(1+ε)·[2 − d·(1/d)(1+ε)] = (1/d)(1+ε)(2 − 1 − ε)
  = (1/d)(1+ε)(1−ε) = (1/d)(1 − ε²)
```
→ α₁ = 0, α₂ = −1 ⇒ **quadratisch**. ✓

---

# Teil B — Übungen

Lösungen in `S3_Newton_Fixpunkte_Loesungen.md`. Formeln von Hand, nichts überspringen.

Ü1–Ü3 sind **wörtlich die Aufgaben aus der Altklausur SS16** (Teil „Nicht-lineare Iterationen"), Ü4 ist dieselbe Aufgabe mit neuen Zahlen. Beachte das Klausurformat: N(x) bzw. f(x) ist immer **gegeben** — verlangt wird einsetzen, ableiten, prüfen. Keine ε-Entwicklung nötig (die ist nur „Möglichkeit 2" aus V8).

> **Gegebene Formeln** (stehen auch in der Klausur — mehr braucht es nicht, alles Weitere wird daraus hergeleitet):
>
> | | |
> |---|---|
> | Newton-Iteration | **Φ(x) = x − f(x)/f'(x)** |
> | Fixpunkt | Φ(x\*) = x\* |
> | Typen | attraktiv \|Φ'(x\*)\| < 1 · repulsiv \|Φ'(x\*)\| > 1 · superattraktiv Φ'(x\*) = 0 |
> | ε-Ansatz | x = x\*(1+ε) einsetzen: Φ(x\*(1+ε)) = x\*(1 + αε + βε² + …), **α = 0 ⟺ superattraktiv** |
> | Hilfsableitung | (f/g)' = (f'g − g'f)/g² |

### Ü1 — Newton allgemein *(Klausur SS16, Aufgabe 1 — wörtlich)*
Zeigen Sie, dass für f(x) mit f(r) = 0 die Funktion **N(x) = x − f(x)/f'(x)** einen superattraktiven Fixpunkt bei r hat. (Nehmen Sie an, dass f'(r) ≠ 0 ist.)

### Ü2 — Gegebenes N untersuchen *(Klausur SS16, Aufgabe 2 — wörtlich)*
Sei **N(x) = x + x·(1 − d·x)**.
a) Zeigen Sie, dass N(x) den superattraktiven Fixpunkt 1/d hat.
b) Hat N einen Fixpunkt bei −1/d? (Falls ja: ist dieser superattraktiv?)
c) Hat N einen Fixpunkt bei 0? (Falls ja: ist dieser superattraktiv?)

### Ü3 — N aus f berechnen *(Klausur SS16, Aufgabe 3 — wörtlich)*
Sei **f(x) = 1/x² − d** (also f(r) = 0 für r = √(1/d)).
a) Berechnen Sie N(x) = x − f(x)/f'(x).
b) Zeigen Sie, dass r ein superattraktiver Fixpunkt von N ist.
c) Zeigen Sie, dass −r ein superattraktiver Fixpunkt von N ist.

### Ü4 — Transfer mit neuen Zahlen *(gleicher Stil, selbst rechnen ohne Lösungsvorlage)*
Sei **f(x) = 1/x³ − d** (also f(r) = 0 für r = d^(−1/3)).
a) Berechnen Sie N(x) = x − f(x)/f'(x).
b) Zeigen Sie, dass r ein superattraktiver Fixpunkt von N ist.
c) Hat N einen Fixpunkt bei 0? (Falls ja: ist dieser superattraktiv?)

---

# Teil C — Vertiefung (über das SS16-Format hinaus)

Alles hier stammt ebenfalls direkt aus V7/V8 — Stoff, den der Prof behandelt oder als Hausaufgabe gestellt hat, der aber in der SS16-Klausur nicht abgefragt wurde. Falls die Klausur 2026 anders aussieht, bist du damit abgedeckt.

### Ü5 — Fixpunkt-Typen klassifizieren
Bestimme für Φ(x) = x²/4 alle Fixpunkte und klassifiziere jeden über Φ' (attraktiv/repulsiv/superattraktiv).

### Ü6 — ε-Entwicklung für 1/d *(„Möglichkeit 2" aus V8)*
Sei N(x) = x(2 − dx). Setze x = (1/d)(1+ε) ein und vereinfache, bis die Form (1/d)(1 + αε + βε² + …) dasteht. Lies α und β ab. Was folgt aus α = 0, und was bedeutet der ε²-Term für die Anzahl korrekter Stellen pro Schritt?

### Ü7 — ε-Entwicklung für 1/√d *(die Hausaufgabe aus V7, mit Zielform)*
Sei N(x) = x + x(1 − dx²)/2 und r = 1/√d. Setze x = r(1+ε) ein und entwickle bis ε³. V7 gibt die Zielform vor: r(1 + αε + βε² + γε³ + …). Bestimme α, β, γ. Superattraktiv?

### Ü8 — Warum nicht der naive Ansatz? *(steht so in V7)*
Für 1/d könnte man auch f(x) = x − 1/d nehmen. Berechnen Sie N(x). Warum ist dieses N als Divisions-Algorithmus sinnlos? (Ein Satz.)

### Ü9 — √d, die Feinheit *(„Verbessert"-Stelle in V8)*
a) Sei f(x) = x² − d. Berechnen Sie N(x) und vereinfachen Sie zu ½(x + d/x).
b) Zeigen Sie, dass √d superattraktiver Fixpunkt ist.
c) Warum taugt dieses N **nicht** als „Wurzel ohne Division"? Wie rechnet man √d stattdessen?

### Ü10 — Allgemeine inverse Wurzel *(steht als „Allg." in V8)*
Für 1/ᵃ√d sei f(x) = 1/xᵃ − d.
a) Berechnen Sie N(x) und vereinfachen Sie zu N(x) = x + x(1 − dxᵃ)/a.
b) Prüfen Sie, dass d^(−1/a) Fixpunkt ist.
c) Kontrolle: a = 1, 2, 3 müssen Ü2, Ü3, Ü4 reproduzieren.
