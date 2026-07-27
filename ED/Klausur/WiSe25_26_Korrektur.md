# Generalprobe — WiSe 25/26, Korrektur (25.07.2026)

Gegengeprüft gegen `Lösung/Lösungsvorschlag EDy WiSe25_26.pdf`. Alle Zahlen unten sind die
offiziellen Werte, wo nicht anders vermerkt.

> **Materialbuchhaltung:** WiSe25/26 war die letzte **unverbrauchte** Klausur und laut Plan
> als Generalprobe reserviert. Sie ist damit aufgebraucht. Unverbraucht bleiben für den
> Wiedereinstieg: SoSe21, SoSe23, WiSe20/21, WiSe21/22, WiSe22/23.

## Punktebild (Schätzung, ±4 P)

| Aufgabe | max | erreicht | Kurzbefund |
|---|---|---|---|
| A1 Koax | 25 | **~17** | 1.1, 1.3, 1.4 komplett richtig; **1.2 und 1.5 leer** (8 P) |
| A2 Hohlleiter | 17 | **~12** | 2.1 + 2.3 richtig; 2.2 ein Klammerfehler; 2.4 falsche Bezugslänge |
| A3 Grenzfläche | 19 | **~12** | Brewster, Geometrie, Totalreflexion sitzen; S_d1-Faktor falsch; 3.3 leer |
| A4 Leitungstrafo | 20 | **~4** | Route richtig, aber λ/4 nicht erkannt → alle Zahlen falsch; 4.2 + 4.3 leer |
| A5 Antennen | 19 | **~4** | 5.1 nur ein Dipol statt vier; 5.2/5.3 angefangen; 5.4 leer |
| **Summe** | **100** | **~48** | |

## Diagnose

**Das ist die beste der drei Probeklausuren** (~48 gegen ~40 und ~39) — und der Zugewinn kommt
fast vollständig aus A1 und A2, also aus den Typen, die zuletzt trainiert wurden.

Trotzdem ist das Muster unverändert: **31 von 100 Punkten sind komplett leer geblieben**
(A1.2 4 P, A1.5 4 P, A2.4 3 P, A3.3 3 P, A4.2 6 P, A4.3 4 P, A5.4 7 P), dazu zwei halb
gerechnete Teilaufgaben in A5. Davon sind wieder rund **14 Punkte reines Nachschlagen**:

- **A1.2 (4 P)** — Abstand Max→Min ist λ/4. Zwei Zeilen, keine Vorbedingung.
  (Achtung: die Musterlösung rechnet hier falsch — siehe Kasten unten.)
- **A4.3 (4 P)** — ein **Satz** ohne jede Rechnung: kein ohmscher Verbraucher mehr im System
  ⇒ Re{Z₂} = 0.
- **A2.4 (3 P)** und **A3.3 (3 P)** — je eine Formelzeile.

Die inhaltlichen Fehler sind wieder Einzelschritte, und drei davon sind **Eingabefehler am
Rechner**, keine Verständnisfehler: eine fehlende Klammer (A2.2), eine falsche Bezugsgröße
(A2.4), ein Transmissionsfaktor (A3.2).

**Der eine echte Einbruch ist A4** — der Typ, der im Juli als „durchgearbeitet und verstanden"
abgehakt war. Ursache ist genau die FS-Zeile, die nach Probeklausur 1 eingebaut wurde:
*vorher l/λ ausrechnen!* Hier war l₁/λ = 75/60 = 1,25 = λ + λ/4 ⇒ **λ/4-Transformation**.
Statt der Ein-Zeilen-Formel Z₀ = Z_L²/Z_V wurde die allgemeine Transformationsformel benutzt —
und die steht bei βl₁ = 450° **direkt auf dem Pol des Tangens**, wo jede Rundung explodiert.
Ein Rechenfehler war unvermeidlich, und er hat 10 Punkte gekostet (plus die 6 aus 4.2, die
darauf aufbauen).

---

## A1 Koaxialkabel — ~17/25

**1.1 ✓ 2/2** — f_g = 0,174 GHz·m/(D·√εr) = 0,174/(40·10⁻³·1) = **4,35 GHz**. Exakt die
Musterlösung, inklusive √εr = 1 für Luft.

**1.2 0/4 (leer)** — zwei Zeilen, und sie hängen an nichts:

  Abstand Spannungs**maximum** → **minimum** = **λ/4**
  λ/4 = 70 cm − 20 cm = 50 cm  ⇒  λ = 4·Δz = **2,0 m**
  f = c₀/λ = **150 MHz**

> ⚠️ **Hier weicht die Musterlösung ab — und sie hat unrecht.** Der Lösungsvorschlag setzt
> „Abstand Maximum zu Minimum: λ/2" an und kommt auf λ = 1,0 m und **300 MHz**. Das
> widerspricht dem Stehwellenmuster: |U(z)| enthält den Term 2βz, wiederholt sich also mit
> **λ/2**, und zwischen einem Maximum und dem benachbarten Minimum liegt die **halbe**
> Periode, also **λ/4**. Gegenprobe mit den Zahlen der Aufgabe: wäre λ = 1,0 m, dann läge
> bei einem Minimum in z = 20 cm 50 cm weiter (= λ/2) wieder ein **Minimum** — die Aufgabe
> sagt aber, dort ist das Maximum. Die eigene FS sagt dasselbe (K1, Zeile „Stehwellen-Sonde":
> Δz_max→min = λ/4 ⇒ λ = 4Δz).
>
> Konsequenz für die Klausur: **150 MHz hinschreiben und die Begründung dazu** („Muster
> wiederholt sich mit λ/2, Max→Min = λ/4"). Mit Begründung kann ein Korrektor das nicht
> stillschweigend streichen. Beruhigend: **keine spätere Teilaufgabe braucht f** — 1.3, 1.4
> und 1.5 laufen ohne, hier hängt also nichts dran.

**1.3 ✓ 8/8** — U_h = (U_max+U_min)/2 = 4,0 V, U_r = (U_max−U_min)/2 = 3,0 V,
|r| = U_r/U_h = **0,75**. Weg und Ergebnis wortgleich mit der Musterlösung.

**1.4 ✓ 7/7** — Z_L = R_V·(1−r)/(1+r) = 350 Ω·0,25/1,75 = **50 Ω**, dann
d = D·e^(−Z_L√εr/60 Ω) = 40 mm·e^(−50/60) = **17,4 mm**. Beide Schritte richtig, auch die
Richtung der Exponentialformel (großer Durchmesser gegeben ⇒ **teilen**, also negativer
Exponent).

**1.5 0/4 (leer)** — drei Zeilen, und Z_L = 50 Ω wird in der Aufgabe sogar geschenkt:

  P_h = U_h²/Z_L = (4,0 V)²/50 Ω = **320 mW**
  P_V = P_abs = P_h − P_r = P_h·(1 − |r|²) = 320 mW·(1 − 0,75²) = **140 mW**

  Kernaussage: **die Leistung geht mit |r|², die Spannung mit |r|.** Und der Hinweis „die
  reflektierte Leistung wird vollständig im Generator absorbiert" heißt nur: es kommt nichts
  ein zweites Mal zurück, du darfst mit der einfachen Bilanz rechnen.

## A2 Rechteckhohlleiter — ~12/17

**2.1 ✓ 4/4** — f_cH10 = c₀/2a = **5,0 GHz**, f_cH20 = 2·f_cH10 = **10 GHz**, also
**5,0 GHz < f < 10 GHz**. (Kontrolle H₀₁ = c₀/2b = 12,5 GHz liegt darüber, der zweite
Wellentyp ist also wirklich H₂₀ — b < a/2, die Reihenfolge stimmt.)

**2.2 ~4/6** — Formelgerüst komplett richtig, **eine Klammer** verloren.
- ✓ R_F/Z_F0 = 2,12·10⁻⁵·√(κ_Ag/κ_Ms)·√(f/GHz) = **1,043·10⁻⁴** — richtig aufgebaut,
  inklusive √6,0 für die Frequenz.
- ✗ Im Zähler steht **a/(2b)**, nicht a/b. Du hast 30/12 = **2,5** gerechnet, richtig ist
  30/24 = **1,25**:

  α = 2·(R_F/Z_F0)·[a/(2b) + (λ₀/2a)²] / [a·√(1−(λ₀/2a)²)]
    = 2·1,043·10⁻⁴·[1,25 + 0,694]/[0,030 m·0,5528] = **2,445·10⁻² 1/m**

- ✓ Der letzte Schritt war richtig gerechnet: a = 8,686 dB·α·l. Mit dem korrekten α sind das
  **5,3 dB** statt deiner 8,72 dB. (Dein Ergebnis folgt exakt aus deinem α — 8,686·0,0402·25 =
  8,72; der Fehler sitzt **nur** in der Klammer.)
- Plausibilitätsanker fürs nächste Mal: mit 2,5 statt 1,25 wird die Klammer 3,19 statt 1,94,
  also Faktor 1,64 — und genau um diesen Faktor liegt das Ergebnis daneben. **Wenn eine
  Dämpfung „zu rund" um einen einzelnen Faktor danebenliegt, ist es fast immer eine Klammer
  im Rechner.**

**2.3 ✓ 4/4** — λ_H = λ₀/√(1−(λ₀/2a)²) = 90,45 mm, Resonator = λ_H/2 ⇒ **d = 45,2 mm**.
Sauber, auch der Denkschritt „Resonator muss eine halbe **Hohlleiter**wellenlänge lang sein".

**2.4 0/3** — der erste Schritt war richtig, der zweite hat die falsche Bezugslänge.
- ✓ λ bei f₂: c₀/2,5 GHz = **120 mm**.
- ✗ Verglichen werden muss mit der **Grenzwellenlänge** λ_c = 2a = **60 mm**, nicht mit den
  50 mm aus Teilaufgabe 2 (die gehören zu 6,0 GHz) — und der Quotient wird **quadriert**:

  f₂ = f_c,H10 = c₀/(√εr·2a)  ⇒  √εr = c₀/(2a·f₂) = 2,0  ⇒  **εr = 4,0**

- Merksatz: **das Dielektrikum verkleinert alle Grenzfrequenzen um √εr.** Damit 2,5 GHz
  laufen kann, muss f_cH10 = 5,0 GHz auf ≤ 2,5 GHz gedrückt werden — Faktor 2 in der
  Frequenz ⇒ Faktor 4 in εr. Diese Überschlagsrechnung im Kopf hätte die 0,42 sofort
  entlarvt (εr < 1 gibt es nicht).

## A3 Grenzfläche — ~12/19

**3.1 ✓ 3/3** — α = α_B = arctan√(εr2/εr1) = arctan 1,5 = **56,31°**. Der Pfeil am
einfallenden Strahl zählt nur, wenn er **quer zum Strahl in der Zeichenebene** liegt (E in der
Einfallsebene) — so zeichnet es die Musterlösung. Das ist die Polarisation, die bei Brewster
vollständig durchgeht.

**3.2 ~9–10/13** — Geometrie und Totalreflexion komplett richtig, **ein Faktor** falsch.
- ✓ β = arcsin(√(εr1/εr2)·sin α) = **33,69°** (Kurzweg: bei Brewster ist β = 90° − α).
- ✓ Winkelsumme im Dreieck: (90°−γ) + φ + (90°+β) = 180° ⇒ **γ = φ + β = 63,69°**.
- ✓ α_g = arcsin√(εr1/εr2) = **41,8° < γ ⇒ Totalreflexion**, also **S_d2 = 0**.
- ✓ Und der richtige Schluss daraus: **S_r2 = S_d1** (bei Totalreflexion geht nichts verloren).
- ✗ **S_d1 stimmt nicht.** Dein Weg über die Feldstärken ist in sich konsistent
  (E_h = √(S_h·Z_F0) = 33,6 V/m, S_d = E_d²·√εr2/Z_F0), aber dein Transmissionsfaktor ist
  ≈ 0,51; richtig ist:

  t_mE = 1,0  und  t_eE = 0,667  ⇒  S_d1 = t_eE·t_mE·S_h = **2,0 W/m²**  ⇒  S_r2 = **2,0 W/m²**

- **Der Kurzweg, den du in der FS stehen hast (K3, Brewster-Zeile), spart die beiden
  t-Formeln komplett:** bei Brewster gilt

  S_d = S_h·cosα/cosβ = 3,0 W/m²·cos56,31°/cos33,69° = 3,0·0,6667 = **2,0 W/m²**

  Eine Zeile, kein Fresnel. Der Faktor cosα/cosβ = 0,667 ist genau das t_eE·t_mE von oben —
  wenn beide Wege 0,667 liefern und dein Rechner 0,51 zeigt, ist es der Rechner.

**3.3 0/3 (leer)** — zwei Zeilen, und die Anker in der Klammer hätten sie unabhängig von 3.2
gemacht:

  „reflexionsfrei austreten" ⇒ δ muss **Brewsterwinkel von innen** sein:
  δ_B = arctan√(εr1/εr2) = arctan(1/1,5) = **33,69°** (= β, weil Brewster hin und zurück
  denselben Winkelpartner hat)
  Winkelsumme: (90°−δ) + (90°−γ) + ϑ = 180°  ⇒  **ϑ = δ + γ = 33,69° + 63,69° = 97,38°**

  Mit den Ankerwerten [β = 30°, γ = 60°] wären es 90° gewesen — die Musterlösung führt genau
  das als Alternativergebnis mit auf.

## A4 Leitungstransformation — ~4/20

λ = c₀/f = **60 cm**, β = 2π/λ = 10,47 1/m ✓ — beides richtig.

**4.1 ~4/10** — die **Route ist komplett richtig**, nur die Transformation nicht.
- ✗ **l₁/λ = 75/60 = 1,25 = λ + λ/4 ⇒ λ/4-Transformation.** Damit ist die ganze erste Zeile
  eine Division:

  Z₀ = Z_L1²/Z_V = 240² Ω²/(1000 − j1000) Ω = **(28,8 + j28,8) Ω**

  (Der Lösungsvorschlag schreibt an dieser Stelle „75 cm = 3λ/4" — das ist ein Tippfehler,
  richtig ist 5λ/4. Am Ergebnis ändert es nichts, λ/4 bleibt λ/4.)

  Du hattest **(28,4 + j6,15) Ω** aus der allgemeinen Formel. Der Grund, warum das schiefgehen
  *musste*: βl₁ = 450°, und dort hat tan βl₁ seinen **Pol**. Zähler und Nenner werden beide
  riesig, und jede Rundung in β (10,5 statt 10,472) verschiebt das Ergebnis massiv. Die
  allgemeine Formel ist hier nicht nur unnötig, sie ist numerisch unbrauchbar.
- ✓ Danach war alles richtig gedacht — C liegt **parallel**, also in Y rechnen:

  Y₀ = 1/Z₀ = (17,36 − j17,36) mS
  ωC = −Im{Y₀} = +17,36 mS  ⇒  **C = 17,36·10⁻³/(2π·500 MHz) = 5,5 pF**
  **Z₁ = 1/Re{Y₀} = 1/17,36 mS = 57,6 Ω**

  Deine 2,32 pF folgen exakt aus deinem Z₀ — der Rechenweg von Z₀ bis C ist also fehlerfrei,
  nur mit falschem Startwert. Und Z₁ = 1/Re{Y₀} hattest du als Formel hingeschrieben, aber
  nicht mehr ausgerechnet: **hinschreiben und nicht auswerten kostet die vollen Punkte**, das
  sind hier ~2 P für eine Kehrwert-Taste.
- Der Selbstcheck lag auf demselben Blatt: Teilaufgabe 2 nennt **Z₁ = 57,6 Ω** als Anker.
  Dein Weg hätte 29,7 Ω ergeben — Faktor 2 daneben, sofort sichtbar.

**4.2 0/6 (leer)** — und diese Teilaufgabe war durch den Anker **unabhängig** von 4.1:

  X_L = ωL = 2π·500 MHz·10 nH = **31,42 Ω**
  Z'₁ = Z₁ + jX_L = (57,6 + j31,42) Ω          (L liegt in Serie ⇒ Z addieren)
  tan βl₂ = tan(2π/60 cm · 26 cm) = tan 156° = **−0,4452**
  Z₂ = Z'₁·(1 + j(Z_L2/Z'₁)·tan βl₂)/(1 + j(Z'₁/Z_L2)·tan βl₂) = (50,06 − j0,12) Ω ≈ **50 Ω**

  Drei Schrittarten, genau wie im Rezept: **Serie (L) → transformieren (l₂)**. l₂/λ = 0,433,
  also kein Sonderfall, hier ist die allgemeine Formel richtig.

**4.3 0/4 (leer)** — **ein Satz, keine Rechnung**, die billigste Teilaufgabe der ganzen Klausur:

  Klemmt man Z_V ab, enthält das Netzwerk nur noch verlustlose Leitungen, ein L und ein C.
  Es gibt keinen ohmschen Verbraucher mehr, in dem Wirkleistung umgesetzt werden könnte
  ⇒ **Re{Z₂} = 0**.

  Das ist derselbe Gedanke wie der Selbstcheck aus der A4-Session im Juli („verlustlose
  Stichleitung ist rein imaginär") — nur einmal aufs ganze Netzwerk angewandt.

## A5 Antennen — ~4/19

**5.1 ~1/2** — λ₀ = c₀/f₀ = **11,54 cm** ✓, aber gefragt war der Gewinn **der Antenne**, nicht
des einzelnen Dipols. Vier Halbwellendipole:

  G_ges = N·G_½ = 4·1,64 = 6,56  ⇒  g_ges = 10 dB·lg 6,56 = **8,17 dBi**
  (Faustweg: Verdopplung = +3 dB, vier Stück = +6 dB ⇒ 2,15 dBi + 6 dB = 8,15 dBi)

  Deine 2,15 dBi sind der Wert **eines** Dipols. Kontrolle direkt darunter: Teilaufgabe 2
  sagt „der Gewinn sei nun **8,0 dBi**" — das ist praktisch dein Ergebnis plus 6 dB, also der
  Anker, der die 2,15 widerlegt hätte.

**5.2 ~1/4** — richtig angefangen, nicht zu Ende gerechnet, und ein G verwechselt.
- ✓ G = 10^(8,0/10) = **6,31** aus den dBi — richtig umgerechnet.
- ✗ In A_w gehört der Gewinn der **Empfangs**antenne (Elementardipol, G = 1,5), nicht die 6,3
  des Senders. Dein A_w passt zum Sendegewinn.
- Vollständig:

  S_E = P_S·G_S/(4π·r²) = 10 W·6,31/(4π·(10·10³ m)²) = **50,2 nW/m²**
  A_w = λ₀²·G_MobTel/(4π) = (0,1154 m)²·1,5/(4π) = **1,59·10⁻³ m²**
  P_E = S_E·A_w = **79,8 pW**

- Die Kette, die hier zweimal auftaucht und die du im Juli schon einmal durchgesprochen hast:
  **P_S →(G_S, 1/4πr²)→ S_E →(A_w)→ P_E.** Der Sendegewinn steht **nur** in der ersten Stufe,
  der Empfangsgewinn **nur** in A_w. Nie beide in einer Formel.

**5.3 ~2/6** — Gruppenfaktor richtig angesetzt, zwei Dinge fehlen.
- ✓ u = δ + (2π/λ₀)·b·cos ϑ = 0 + 2π·cos150° = **−5,441** (Bogenmaß! b = λ₀, δ = 0 weil
  gleichphasig) — das ist korrekt.
- ✗ Der Vorfaktor ist **1/N**, nicht 1/√N, und der Betrag wird **quadriert**:

  G_Dl = (1/N)·|sin(N·u/2)/sin(u/2)|² = (1/4)·|sin(−10,88)/sin(−2,721)|² = **1,479**

- ✗ Es fehlt der **Elementfaktor** — die Dipole strahlen bei 150° selbst schon schwach:

  G_½,150° = 1,64·|cos(π/2·cos ϑ)/sin ϑ|² = 1,64·|cos(π/2·cos150°)/sin150°|² = **0,286**

- ⇒ G_ges = 1,479·0,286 = 0,423  ⇒  **g_ges = −3,7 dBi**
- Merksatz: **Gruppengewinn = Gruppenfaktor × Einzelstrahler**, immer beide Faktoren. Und ein
  Gewinn **unter** 0 dBi ist an dieser Stelle plausibel — 150° liegt weit weg von der
  Hauptstrahlrichtung.

**5.4 0/7 (leer)** — die teuerste leere Teilaufgabe. Der Hinweis in der Klammer („Richtcharakteristik
des Halbwellendipols vernachlässigbar") sagt schon, dass **nur** der Gruppenfaktor gebraucht wird:

  Hauptstrahlrichtung: der Zähler sin(N·u/2) und der Nenner sin(u/2) müssen beide null werden
  ⇒ **u = 0**, also δ/2 + (π/λ₀)·b·cos ϑ = 0.
  Geometrie: tan(180° − ϑ) = R/h ⇒ ϑ = 180° − arctan(600 m/10 m) = **90,955°**
  δ = −(2π/λ₀)·b·cos ϑ = −2π·cos(90,955°) = **6,0°**

  Der Lösungsvorschlag schreibt −6,0°; seine eigene Formel liefert mit cos ϑ < 0 ein **+**.
  Was zählt, ist der **Betrag 6,0°** und die Aussage, in welche Richtung die Phase fortschreitet.
  Plausibilitätsprobe: der Strahl muss nur 0,955° unter die Waagrechte gekippt werden — dass
  dafür wenige Grad Phasenunterschied genügen, passt.

---

## Was daraus für den nächsten Anlauf folgt

1. **A1 und A2 sind stabil.** 17/25 und 12/17 sind die besten Werte aller drei Probeklausuren,
   und die beiden Fehler in A2 sind Rechnereingaben, keine Lücken. Diese Typen brauchen beim
   Wiedereinstieg nur eine Auffrischung.
2. **A4 ist nicht so sicher, wie es im Juli aussah** — nicht wegen der Theorie (die Route war
   komplett richtig), sondern weil der **Sonderfall-Check am Anfang fehlte**. Die FS-Zeile
   *„vorher l/λ ausrechnen: 0,25 → λ/4, 0,5 → λ/2, sonst Formel 3"* muss zur Handbewegung
   werden: erst l/λ hinschreiben, dann erst zum Rechner greifen. Hier hätte diese eine Zahl
   (1,25) 16 Punkte gerettet.
3. **A5 bleibt der schwächste Typ** — zum dritten Mal einstellig. Es ist weiterhin der Typ, der
   nie einmal komplett allein gerechnet wurde. Der Stoff ist nicht schwer: 5.1 ist eine
   Multiplikation mit 4, 5.2 sind zwei Formeln. Beim Wiedereinstieg hier anfangen.
4. **Die Reihenfolge ist unverändert das größte Einzelthema.** Zum dritten Mal ~30 leere Punkte,
   darunter ein Satz für 4 Punkte (A4.3) und zwei Zeilen für 4 Punkte (A1.2). Der Ablauf, der
   das erschlägt, steht seit SoSe24 fest: **erst die ganze Klausur durchblättern und jede
   Teilaufgabe einsammeln, die ≤ 4 Punkte gibt und nach genau einer Größe fragt.** Hier wären
   das A1.2, A2.4, A3.3, A4.3 gewesen — 14 Punkte in vielleicht 12 Minuten.
5. **Die Anker in den eckigen Klammern wurden wieder nicht als Kontrolle gelesen.** Zweimal
   hätten sie sofort gewarnt: Z₁ = 57,6 Ω gegen deine 29,7 Ω (A4.1) und „Gewinn sei nun
   8,0 dBi" gegen deine 2,15 dBi (A5.1). Das ist derselbe Befund wie in beiden vorigen
   Korrekturen — und es ist kein Wissens-, sondern ein Ablaufpunkt.
