# Probeklausur 2 — SoSe 24, Korrektur (25.07.2026)

Gegengeprüft gegen `Lösung/Lösungsvorschlag EDy SoSe24.pdf`. Alle Zahlen unten sind die
offiziellen Werte.

> **Kontext:** Diese Probeklausur war die letzte vor dem Prüfungstermin 27.07.2026. Lena
> ist nicht angetreten (Begründung und Übergabe: `ED/CLAUDE.md`, Abschnitt „Übergabe").
> Das Dokument ist deshalb **für den Wiedereinstieg** geschrieben: bei jeder leer
> gebliebenen Teilaufgabe steht der vollständige Rechenweg, nicht nur der Befund.

## Punktebild (Schätzung, ±3 P)

| Aufgabe | max | erreicht | Kurzbefund |
|---|---|---|---|
| A1 Koax | 18 | **~7** | 1.1 α richtig, Faktor 3,59 fehlt; 1.2 leer; 1.3 falsche Richtung |
| A2 Hohlleiter | 17 | **~8** | **2.3 komplett richtig**; 2.1 halb; 2.2 zwei Faktoren fehlen; 2.4 leer |
| A3 Grenzfläche | 22 | **~7** | **3.2 + 3.3 komplett richtig**; 3.1 und 3.4 leer |
| A4 Leitungstrafo | 23 | **~11** | **4.3 komplett richtig**; 4.1 Struktur richtig/Zahl falsch; 4.2 Vorzeichen; 4.4 leer |
| A5 Antennen | 20 | **~6** | 5.2 richtig; 5.1 Zehnerpotenz; 5.3 falsche Route; 5.4 + 5.5 leer |
| **Summe** | **100** | **~39** | |

## Diagnose

**37 von 100 Punkten sind komplett unbearbeitet geblieben** (A1.2 3P, A2.4 3P, A3.1 6P,
A3.4 8P, A4.4 8P, A5.4 4P, A5.5 5P). In Probeklausur 1 waren es 28 — der Wert ist also
gestiegen, nicht gefallen.

Davon sind rund **20 Punkte reines Nachschlagen** in einer Open-Book-Klausur: A3.1, A2.4
und A1.2 sind je **eine** Formelzeile, A4.4 sind zwei. Keine dieser vier Teilaufgaben
setzt eine frühere voraus.

Die inhaltlichen Fehler der bearbeiteten Teile sind durchweg **Einzelschritte**, keine
Verständnislücken: eine Zehnerpotenz (A5.1), ein vergessener Wurzelfaktor und ein
vergessener Faktor 2 (A2.2), ein Vorzeichen (A4.2), ein fehlender Konstantenfaktor (A1.1).
Die konzeptionell schwierigen Stellen — Gruppengeschwindigkeit beim Impuls, Brewster
**und** Totalreflexion samt Polarisationsaussage, „reell → reell geht nur mit λ/4",
„R₁ = Z_L1 ⇒ keine Transformation" — saßen alle.

**Das wiederkehrende Muster aus beiden Probeklausuren ist damit dasselbe und es ist kein
Wissensproblem: es wird von vorne nach hinten gerechnet, bis die Zeit alle ist, statt
zuerst die billigen Teilaufgaben einzusammeln.**

---

## A1 Koaxialkabel — ~7/18

**1.1 ~4/8** — α richtig, Endwert fehlt.
- ✓ 2,0 dB ≙ 10^(−2/20), α = ln(10^0,1)/l = **1,151·10⁻² 1/m**. Exakt die Musterlösung.
- ✗ In deiner Formel für D fehlt der Faktor **3,59**. Vollständig:

  D_min = (l/ln(10^0,1)) · √(f·μ·εr/(π·κ)) · (1/120 Ω) · **3,59** = **12,8 mm**

  Der 3,59 ist (D/d)_opt: die Dämpfungsformel enthält (1 + D/d)/ln(D/d), und dieser
  Ausdruck nimmt bei D/d = 3,59 seinen kleinsten Wert an — genau **3,59**. „Mindestens
  welchen Durchmesser" heißt: bei optimalem Verhältnis rechnen. Steht in K1.

**1.2 0/3 (leer)** — eine Zeile, K1:

  f_g = 0,174 GHz·m/(D·√εr)  ⇒  εr,max = (0,174 GHz·m/(D·f))²
  = (0,174/(13·10⁻³ m · 3,5 GHz))² = **14,6**

**1.3 ~3/7** — richtige Formel, falsche Richtung.
- ✗ Du hast δ aus **f₀** berechnet. f₀ ist hier aber gar nicht gefragt — gesucht ist ja
  gerade die Frequenz. δ kommt aus der **Dämpfungsforderung**:

  100 dB ≙ A = 10⁻⁵  ⇒  w/δ = ln(10⁵) = 11,51  ⇒  δ = 0,15 mm/11,51 = **13,0 µm**

  (Gleichwertig über die FS-Zeile: δ = w·8,686 dB/a = 0,15 mm·8,686/100 = 13,0 µm.)
- ✓ Dein zweiter Schritt war **richtig**: f = 2/(2π·δ²·μ·κ) = **25,7 MHz**.
- Antwortsatz: Schirmdämpfung > 100 dB für **alle Frequenzen über 25,7 MHz** (a ∝ √f,
  also ist die geforderte Dämpfung eine **untere** Grenzfrequenz).

## A2 Rechteckhohlleiter — ~8/17

**2.1 ~2/4** — λ₀ = 20 cm ✓, aber nur eine der drei Bedingungen sauber.
- H₁₀ **muss** laufen: a ≥ λ₀/2 = 10 cm ✓ (hattest du)
- H₂₀ darf **nicht** laufen: a < λ₀ = **20 cm**
- H₀₁ darf **nicht** laufen: b < λ₀/2 = **10 cm**
- Ergebnis: **10 cm < a < 20 cm, b < 10 cm**
- ✗ Du hattest **b < a/2 = 5 cm**. Das ist die Bedingung „H₀₁ liegt über H₂₀", also eine
  hinreichende, aber unnötig enge Zusatzforderung — gefragt war der **volle Bereich**.
  Merke: die Grenzen kommen alle aus λ₀, nicht aus a.

**2.2 ~2/5** — Formeln richtig, zwei Faktoren verloren.
- ✗ √(f/GHz) = √1,5 vergessen: du 4,26·10⁻⁵, richtig **5,214·10⁻⁵**
- ✗ und der Faktor **2** in α = **2**·R_F/Z_F0 · […]: du 1,8·10⁻³, richtig **4,384·10⁻³ 1/m**
- Damit a_dB = 8,686 dB·α·l = **3,8 dB** (deine 1,57 dB folgen korrekt aus deinem α — der
  letzte Schritt war also richtig gerechnet).

**2.3 ✓ 5/5** — makellos. λ_c = 2a = 22 cm, v_gr = c₀·√(1−(λ₀/λ_c)²) = 1,250·10⁸ m/s,
τ = l/v_gr = **800 ns**. Das ist genau die FS-Zeile, die nach Probeklausur 1 eingebaut
wurde — sie hat funktioniert.

**2.4 0/3 (leer)** — eine Zeile:

  λ_c,H01 = π·D/η'₀₁ mit η'₀₁ = **3,83**
  ⇒ D_min = λ₀·3,83/π = 20 cm·3,83/π = **24,4 cm**

  (η'₀₁ = 3,83 ist die erste Nullstelle von J₁ — Tabellenwert, muss nachgeschlagen werden.
  Rundhohlleiter kommt in A2 nur als Anhängsel vor, aber genau dann als geschenkte Punkte.)

## A3 Grenzfläche — ~7/22 (die teuerste Aufgabe)

**3.1 0/6 (leer)** — zwei Zeilen, und die einzige Aufgabe der ganzen Klausur ohne jede
Vorbedingung:

  Z_F = Z_F0/√εr1 = 377 Ω/√5,0 = 168,6 Ω
  E = √(S·Z_F) = √(8,0 W/m² · 168,6 Ω) = **36,73 V/m**
  H = E/Z_F = **0,2178 A/m**

  Herleitung, falls die Formel nicht dasteht: S = E·H und E/H = Z_F ⇒ E²/Z_F = S.
  Effektivwerte sind gefragt, also **keine** √2-Umrechnung — S ist bereits ein Mittelwert.

**3.2 ~3/4** — α_B = arctan√(εr2/εr1) = arctan 0,632 = **32,3°** ✓.
  Der fehlende Teil ist die **Zeichnung**: E als Pfeil quer zum Strahl **in der
  Zeichenebene** (E in der Einfallsebene) — das ist die Polarisation, die bei Brewster
  vollständig durchgeht. Die Aufgabe sagt „in die Skizze oben einzeichnen"; ohne Pfeil
  fehlt ein Punkt.

**3.3 ✓ 4/4** — α_g = arcsin√(εr2/εr1) = **39,2°**, α ≥ 39,2°, „Polarisation unerheblich".
  Wortgleich mit der Musterlösung.

**3.4 0/8 (leer)** — die teuerste einzelne Teilaufgabe der Klausur. Route:
- „E ausschließlich **parallel zur Grenzschicht**" = E **senkrecht zur Einfallsebene**.
  Das ist die *andere* Polarisation als bei Brewster — deshalb wird hier auch etwas
  reflektiert, und deshalb ist „Brewster" (dein Stichwort auf dem Blatt) die falsche Spur.
- α = 30° liegt **unter** α_g = 39,2° ⇒ keine Totalreflexion, es geht etwas durch.

  β = arcsin(√(εr1/εr2)·sin α) = arcsin(√2,5·sin 30°) = **52,2°**
  t_eH = 2/(1 + (cosβ/cosα)·√(εr2/εr1)) = 2/(1 + 0,613/0,866·0,632) = **1,382**
  t_mH = 2·√(εr2/εr1)/(1 + (cosβ/cosα)·√(εr2/εr1)) = 2·0,632/1,448 = **0,874**
  S_d = t_eH·t_mH·S_h = 1,382·0,874·8,0 W/m² = **9,66 W/m²**

- **Wichtig, weil es nach einem Fehler aussieht:** S_d = 9,66 W/m² ist **größer** als die
  einfallenden 8,0 W/m² — und trotzdem richtig. Die Leistungs*dichte* darf steigen, weil
  der Strahl beim Übergang ins dünnere Medium **aufgeweitet** wird. Erhalten bleibt die
  **Leistung**: S_d·cosβ/(S_h·cosα) = 9,66·0,613/(8,0·0,866) = 0,85, also 85 % durch,
  15 % reflektiert. Das ist die Plausibilitätsprobe — nicht S_d gegen S_h vergleichen.

## A4 Leitungstransformation — ~11/23

λ = c₀/f = **34,6 cm**, βl₁ = 2π·0,10/0,346 = 1,8133 ≙ **103,9°** ✓ (beides richtig)

**4.1 ~5–6/8** — Struktur komplett richtig, eine Zahl falsch.
- ✓ **R₁ = Z_L1 = 300 Ω ⇒ keine Transformation**, der obere Zweig bleibt 300 Ω. Das ist
  der Denkschritt, um den es der Aufgabe geht, und du hast ihn gesehen.
- ✓ Parallelschaltung erkannt, in **Y** gerechnet — richtig.
- ✗ Der C-Zweig: Z_C1 = 1/(jωC₁) = **−j367,6 Ω**, transformiert über l₁:

  Z_1C = Z_C1·(1 + j(Z_L1/Z_C1)·tan βl₁)/(1 + j(Z_C1/Z_L1)·tan βl₁) = **+j400 Ω**

  Du hattest ≈ j303 Ω (aus Y = −j3,3 mS statt −j2,5 mS). Vorzeichen und Charakter waren
  richtig, nur der Betrag nicht.
- ⇒ **Z₁ = 1/(1/300 Ω + 1/(j400 Ω)) = (192 + j144) Ω**
  (Aufgaben-Anker zum Weiterrechnen: (200 + j150) Ω.)
- Beachte: der Kondensator wird hier **transformiert** und kommt als **induktiv** (+j400)
  am Verzweigungspunkt an. Die λ-Strecke dreht den Charakter — nicht am Bauteil ablesen.

**4.2 ~1/3** — hier sind zwei getrennte Punkte verloren gegangen.
- ✗ **Vorzeichen:** X muss den Imaginärteil **aufheben**, also jX = **−j144 Ω**
  (mit Anker: −j150 Ω), nicht +j150 Ω. Du hast Im{Z₁} hingeschrieben statt −Im{Z₁}.
- ✗ **Bauteile-Wert:** die Aufgabe schreibt „(Bauteile-Wert!)" — verlangt ist nicht die
  Impedanz, sondern das Bauteil mit Zahl. Negative Reaktanz in **Serie** ⇒ **Kapazität**:

  C = −1/(2π·f·X) = −1/(2π·866 MHz·(−144 Ω)) = **1,28 pF**   (mit Anker: 1,22 pF)
- ✓ Z₂ = Re{Z₁} = **192 Ω** (mit Anker: 200 Ω) — richtig.
- Merkregel, die beides erschlägt: **Serie kompensiert mit dem Gegenvorzeichen.** Im{Z} > 0
  (induktiv) ⇒ Kondensator; Im{Z} < 0 ⇒ Spule. Und: gefragte Einheit prüfen — Ω oder F/H.

**4.3 ✓ 4/4** — „reell → reell geht nur mit λ/4" erkannt, l₂ = λ/4 = **8,65 cm**,
Z_L2 = √(Z₂·Z₃) = √(200·300) = **245 Ω**. Deine Angabe l = λ/4 + n·λ/2 ist sogar
vollständiger als die Musterlösung.

**4.4 0/8 (leer)** — zweitteuerste leere Teilaufgabe. Zwei Wege, der zweite ist kürzer:

  **Weg über L' (empfohlen):**
  L' = Z_L/c₀ = 300 Ω/(3·10⁸ m/s) = 1,0 µH/m
  Zweidraht: L' = (μ₀/π)·ln(a/r) ⇒ ln(a/r) = π·L'/μ₀ = π·1,0·10⁻⁶/(4π·10⁻⁷) = 2,5
  ⇒ **a = r·e^2,5 = 0,5 mm·12,18 = 6,1 mm**

  **Weg über C':**
  C' = 1/(Z_L·c₀) = 11,1 pF/m; C' = π·ε₀/ln(a/r) ⇒ ln(a/r) = π·ε₀/C' = 2,504
  ⇒ a = 0,5 mm·e^2,504 = **6,1 mm**

  Der Einstieg ist beide Male derselbe und lohnt sich zu merken: **Z_L = √(L'/C') und
  c₀ = 1/√(L'C')** — aus den beiden bekommt man jeden der zwei Beläge aus Z_L allein,
  ohne die Geometrie zu kennen. Erst danach kommt die Zweidraht-Geometrieformel.

## A5 Antennen — ~6/20

**5.1 ~4/6** — alle drei Formeln richtig, eine Zehnerpotenz falsch.
- A_W = (π/4)·D² = (π/4)·(0,17 m)² = **2,27·10⁻² m²** — du hattest 10⁻⁴ statt 10⁻²
- λ₀ = c₀/f₀ = **3,9 mm** ✓
- G = 4π·A_W/λ² = **18 753**, du 188 ⇒ g = 10 dB·log(18753) = **42,7 dB**, du 22,7 dB
- ✓ Dass **10**·log (Leistung) und nicht 20·log zu nehmen ist, hattest du richtig.
- **Selbstcheck, der das sofort gefangen hätte:** Teilaufgabe 2 gibt „rechnen Sie mit
  g = 43 dBi" vor. 22,7 kann dann nicht stimmen. *Die Anker der späteren Teilaufgaben sind
  die eingebaute Kontrolle der früheren* — das steht seit Probeklausur 1 als Technik im
  Logbuch und hat auch diesmal nicht stattgefunden.

**5.2 ✓ 2/2** — G = 10^(43/10) = 2·10⁴, S_R = G·P_S/(4π·r²) = **198 µW/m²**.
Deckt sich mit dem Anker der Musterlösung.

**5.3 ~0–1/3** — falsche Route.
- ✗ Du hast die **Wirkfläche der Radarantenne** als auffangende Fläche genommen und
  zusätzlich mit G_S multipliziert.
- Richtig: das Fahrzeug fängt über seinen **Querschnitt 1,8 m²** auf und strahlt **isotrop**
  wieder ab — also **kein Gewinn** in dieser Stufe:

  P_R = A·S_R = 1,8 m²·186,5 µW/m² = **335,8 µW**
  S_E = P_R/(4π·r²) = 335,8 µW/(4π·(200 m)²) = **668 pW/m²**   (Anker: 716 pW/m²)

- Die Kette dieser Aufgabe merken, sie ist das ganze Radarprinzip:
  **P_S →(Antennengewinn, 1/r²)→ S_R →(Querschnitt 1,8 m²)→ P_R →(isotrop, 1/r²)→ S_E
  →(Wirkfläche A_W)→ P_E.** Der Gewinn taucht genau **einmal** auf, beim Senden.

**5.4 0/4 (leer)** — zwei Zeilen, hängt nur am Anker S_E = 700 pW/m²:

  P_E = A_W·S_E = 2,27·10⁻² m²·668·10⁻¹² W/m² = **15,16 pW**
  p_E = 10 dB·log(15,16·10⁻¹² W/10⁻³ W) = **−78,2 dBm**

  Der Bezug ist **1 mW = 10⁻³ W**, nicht 1 W — das ist die einzige Falle an dieser Zeile.

**5.5 0/5 (leer)** — konzeptionell die schönste Aufgabe der Klausur, und sie steht in zwei
Zeilen:
- Die Welle läuft **zweimal** durch den Schnee (hin und zurück) ⇒ **36 dB**, nicht 18.
- Radar-Gesetz: S_R ∝ P/r² und P_E ∝ S_R/r² ⇒ **P_E ∝ 1/r⁴**

  (r_neu/r_alt)⁴ = 10^(−3,6)  ⇒  r_neu = 200 m/10^0,9 = **25,2 m**

- Kernaussage zum Mitnehmen: **beim Radar geht die Entfernung in der vierten Potenz ein.**
  36 dB Dämpfung (Faktor 4000 in der Leistung) kosten deshalb nur den Faktor 4000^(1/4) ≈ 8
  in der Reichweite — und umgekehrt: doppelte Reichweite braucht die 16-fache Leistung.

---

## Was daraus für den nächsten Anlauf folgt

1. **Die Reihenfolge ist das Problem, nicht der Stoff.** Zweimal ~40 Punkte, beide Male mit
   ~20 Punkten unangetasteter Ein-Zeilen-Aufgaben auf dem Tisch. Vor dem ersten Rechnen die
   Klausur einmal komplett durchblättern und jede Teilaufgabe markieren, die (a) ≤ 4 Punkte
   gibt und (b) nach genau einer Größe fragt. Die zuerst.
2. **Die Anker in den eckigen Klammern sind Kontrollen, keine Notlösungen.** Beide
   Probeklausuren hatten Fehler, die ein Blick auf die nächste Teilaufgabe entlarvt hätte
   (g = 43 dBi gegen berechnete 22,7 dB; ε_r = 2,0 gegen berechnete 2,25).
3. **Bei „Bauteile-Wert" die Einheit prüfen.** Ω ist keine Antwort, wenn nach einem Bauteil
   gefragt ist.
4. **Zwei Typen waren nie fertig trainiert** (A5 gar nicht, A2 halb) — und genau dort liegen
   die leeren Punkte. Beim Wiedereinstieg mit A5 und A2 anfangen, nicht mit A1/A4.
