# Session 3 — Do 16.07., 3 h · Newton & Fixpunkte (Erstkontakt)

**Quellen:** `V7.pdf`, `Fixpunkte_Newton.pdf` (7-seitiges Skript — das ist deine Hauptquelle!) · **Prüfungsthema:** Newton-Iteration

> **Wichtig:** `Fixpunkte_Newton.pdf` ist bereits ein vollständiges, sauber gesetztes Skript mit Kapiteln 1–8. Lies es als Erstes ganz durch. Dieses Dokument ist die **Kurzfassung zum Aktivlernen** plus Übungen — nicht als Ersatz gedacht.

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

**Warnung zur Notation** (steht so im Skript): die Schreibweise x\*(1+ε) funktioniert **nur für x\* ≠ 0**. Bei x\* = 0 (z. B. Φ(x)=x²) nimmt man den absoluten Fehler ε_{k+1} = ε_k².

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

## 7. Die drei Klausur-Klassiker (kommen Fr in Session 4 dran, hier zum Kennenlernen)

Alle drei berechnen etwas **ohne** die teure Operation (Division/Wurzel) — das ist der Sinn: FPUs machen Division und Wurzel intern genau so.

| gesucht | f(x) | Newton Φ(x) | nur mit |
|---|---|---|---|
| **1/d** | 1/x − d | **x(2 − dx)** | Mult, Sub |
| **√d** | x² − d | ½(x + d/x) | (enthält noch /x!) |
| **1/√d** | 1/x² − d | **(x/2)(3 − dx²)** | Mult, Sub, Shift |

**Feinheit √d (wichtig, Prof fragt das):** Der direkte Weg f = x²−d liefert Φ = ½(x + d/x) — enthält noch eine **Division d/x**. Deshalb rechnet man √d *nicht* direkt, sondern über **√d = d · (1/√d)** und berechnet 1/√d mit der divisionsfreien dritten Zeile. Das ist die Pointe der Aufgabe „warum taugt die direkte Iteration nicht als Antwort?".

**Verifikation 1/d** (aus dem Skript, Kap. 6.4 — die eigentliche Klausuraufgabe):
Setze x = (1/d)(1+ε) in Φ(x) = x(2−dx):
```
Φ = (1/d)(1+ε)·[2 − d·(1/d)(1+ε)] = (1/d)(1+ε)(2 − 1 − ε)
  = (1/d)(1+ε)(1−ε) = (1/d)(1 − ε²)
```
→ α₁ = 0, α₂ = −1 ⇒ **quadratisch**. ✓

---

# Teil B — Übungen

Lösungen in `S3_Newton_Fixpunkte_Loesungen.md`. Formeln von Hand, nichts überspringen.

### Ü1 — Fixpunkt-Typen
Bestimme für Φ(x) = x²/4 alle Fixpunkte und klassifiziere jeden (attraktiv/repulsiv/superattraktiv) über Φ'.

### Ü2 — Newton allgemein herleiten
Leite Φ'(x) = f·f''/(f')² aus Φ(x) = x − f/f' her (Quotientenregel). Erkläre in einem Satz, warum daraus Φ'(r) = 0 an einer einfachen Nullstelle folgt.

### Ü3 — Konvergenzordnung ablesen
Für eine Iteration ergibt sich Φ(x\*(1+ε)) = x\*(1 − ½ε² − ⅓ε³ + …). Welche Ordnung? Begründung.

### Ü4 — Newton für 1/d (die Kern-Klausuraufgabe)
a) Wähle f(x) = 1/x − d. Bilde f'(x) und stelle Φ(x) auf; vereinfache zu Φ(x) = x(2 − dx).
b) Zeige, dass 1/d ein Fixpunkt ist.
c) Zeige Superattraktivität über Φ'(1/d) = 0.
d) Setze x = (1/d)(1+ε) ein und bestätige die quadratische Konvergenz (Ergebnis (1/d)(1−ε²)).

### Ü5 — Warum nicht der naive Ansatz?
Für 1/d könnte man auch f(x) = x − 1/d nehmen. Bilde Φ(x). Warum ist dieses Φ als Divisions-Algorithmus **sinnlos**? (Ein Satz.)

### Ü6 — √d, die Feinheit
a) Wähle f(x) = x² − d, stelle Φ(x) auf und vereinfache zu ½(x + d/x).
b) Zeige, dass √d Fixpunkt ist.
c) Zeige Superattraktivität: Φ'(√d) = 0.
d) Warum taugt dieses Φ trotzdem **nicht** als „Wurzel ohne Division"? Wie umgeht man das Problem?

### Ü7 — Geometrie
Erkläre in zwei, drei Sätzen, warum Φ(x_k) = x_k − f(x_k)/f'(x_k) genau der Schnittpunkt der Tangente an f in x_k mit der x-Achse ist. (Tipp: Tangentengleichung y = f(x_k) + f'(x_k)(x − x_k), setze y = 0.)
