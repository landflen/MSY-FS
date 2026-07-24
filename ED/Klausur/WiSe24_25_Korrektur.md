# Probeklausur 1 — WiSe 24/25, Korrektur (24.07.2026)

Gegengeprüft gegen `Lösung/Lösungsvorschlag EDy WiSe24_25.pdf` — alle Zahlen unten sind
die offiziellen Werte, meine eigene Nachrechnung stimmt damit überein.

## Punktebild (Schätzung, ±3 P)

| Aufgabe | max | erreicht | Kurzbefund |
|---|---|---|---|
| A1 Koax | 20 | **17** | 1.–3. komplett richtig, nur 1.4 dB-Umrechnung falsch |
| A2 Hohlleiter | 21 | **4–5** | 2.2 und 2.4 leer, 2.1 nur halb, 2.3 falsches f_c |
| A3 Grenzfläche | 20 | **8–9** | Rechenwege richtig, aber keine Endwerte; E-Richtung falsch |
| A4 Leitungstrafo | 19 | **9–11** | Vorzeichenfehler in 4.1, λ/4 in 4.3 nicht erkannt |
| A5 Antennen | 20 | **1** | fast komplett leer, 5.2 mit falscher Größe |
| **Summe** | **100** | **~40** | |

**Die Diagnose ist nicht „zu wenig gekonnt", sondern: 28 von 100 Punkten sind komplett
unbearbeitet geblieben** (A2.2 6P, A2.4 5P, A5.1 5P, A5.3 5P, A5.4 7P). Dazu kommen
~15 Punkte, bei denen der Weg stand und nur ein Schritt kippte. Das ist genau die im
Lernplan bekannte Lücke: **A5 ist nie gerechnet worden**, A2 nur zur Hälfte.

---

## A1 Koaxialkabel — 17/20

- **1.1 ✓ 5/5** d = 50 mm/3,59 = 13,9 mm; ε_r = (77 Ω/40 Ω)² = 3,7.
- **1.2 ✓ 2/2** f_g = 0,174 GHz·m/(D·√ε_r) = 1,81 GHz.
- **1.3 ✓ 8/8** α_L = 3,70·10⁻³ 1/m, α_D = 9,06·10⁻³ 1/m, α = 12,77·10⁻³ 1/m,
  a = 2,76 dB (Lösung: 2,8 dB). Vollständig korrekt, auch das Runden auf d = 14 mm ist ok.
- **1.4 ✗ ~2/5** δ = 190,8 µm ✓ (und richtig bei **120 kHz** angesetzt — das ist der
  eigentliche Denkschritt, den viele verlieren: δ ∝ 1/√f, also ist die *unterste*
  Frequenz der schlechteste Fall).
  Der Fehler steckt in der dB-Umrechnung:
  - du: A = e^(−40 dB/20 dB) = 0,135 → w = 381,5 µm
  - richtig: 40 dB ≙ A = 1/100 = **10**^(−40/20), nicht e^(…) → w = δ·ln 100 = **0,88 mm**
  - **Direktweg ohne Umweg** (steht so schon in K1): a = 8,686 dB·w/δ
    ⇒ **w = δ·a/(8,686 dB)** = 190,8 µm · 40/8,686 = 879 µm. Eine Zeile, kein A.

## A2 Rechteckhohlleiter — 4–5/21 (die teuerste Aufgabe)

- **2.1 ~3–4/7** Du hast beide Randwerte gerechnet, aber nur *einen* der drei Modi geprüft
  und keine Bereiche angegeben. Gefragt ist ein **Intervall**, und dafür braucht es drei
  Bedingungen (K2, Zeile 1):
  - H₁₀ **muss** bei 6 GHz laufen: a ≥ c₀/(2·6 GHz) = 25 mm
  - H₂₀ darf bei 10 GHz **nicht** laufen: a < c₀/10 GHz = **30 mm** ← fehlte
  - H₀₁ darf bei 10 GHz **nicht** laufen: b < c₀/(2·10 GHz) = 15 mm
  - Ergebnis: **25 mm ≤ a < 30 mm, b < 15 mm**
- **2.2 0/6 (leer)** — reine Gruppengeschwindigkeit, FS 7.2:
  λ₀ = c₀/f₁ = 50 mm, λ_c = 2a = 54 mm
  v_gr = c₀·√(1 − (λ₀/λ_c)²) = 3·10⁸·√(1 − (50/54)²) = 1,133·10⁸ m/s
  τ = l/v_gr = 100 m/1,133·10⁸ = **883 ns**
  (Merksatz: „wie lange braucht ein **Impuls**" ⇒ immer v_gr, nie v_ph, nie c₀.)
- **2.3 ~1/3** Formel richtig, aber falsches f_c eingesetzt: nicht die 6 GHz aus der
  Bandangabe, sondern die **tatsächliche Grenzfrequenz des gewählten Hohlleiters**
  f_cH10 = c₀/2a = 3·10⁸/54 mm = 5,56 GHz.
  ε_r = (c₀/(f_g·2a))² = (3·10⁸/(4·10⁹·54·10⁻³))² = **1,93** (nicht 2,25).
  **Selbstcheck, der das sofort gefangen hätte:** Teilaufgabe 4 rechnet mit ε_r = 2,0 —
  das muss die Bedingung „mindestens" erfüllen. 2,0 > 1,93 ✓, aber 2,0 < 2,25 ✗.
- **2.4 0/5 (leer)** — dielektrische Dämpfung **im Hohlleiter**, das ist nicht die
  Koax-Formel, sondern die Koax-Formel geteilt durch den Hohlleiter-Wurzelterm:
  λ_ε = λ₀/√ε_r = c₀/(f₁√ε_r) = 35,36 mm
  α_ε = (π/λ_ε)·tan δ · 1/√(1 − (λ_ε/2a)²)
  3,0 dB ≙ Amplitudenverhältnis √2 = e^(α_ε·l) ⇒ α_ε = ln√2/l
  ⇒ tan δ = (ln√2 · λ_ε)/(l·π) · √(1 − (λ_ε/2a)²) = **2,95·10⁻⁵**
  **Diese Formel steht bisher nicht in der FS** (nur die Koax-Variante α_D = πf√ε_r tanδ/c₀).

## A3 Grenzfläche — 8–9/20

- **3.1 ~3/5** ε_r2 = 1·tan²55° = **2,04** ✓.
  Die E-Richtung ist falsch: du hast „senkrecht zum Blatt ⊙" geschrieben. Bei Brewster
  geht **E∥ Einfallsebene** durch (Pfeil in der Papierebene, quer zum Strahl) — E⊥ wird
  immer teilweise reflektiert. Genau der Punkt, den wir gestern in K3 geschärft haben:
  **„Brewster nimmt E∥ raus"** — was durchgeht ist E∥, was reflektiert wird ist E⊥.
  Die Musterlösung zeichnet einen Einfachpfeil quer zum Strahl in der Zeichenebene.
- **3.2 ~2–3/5** Weg richtig (S_d1 = cos α/cos β · S_h), β = 90° − α = 35° ist bei Brewster
  sogar zulässig (offiziell β = arcsin(sin55°/√2) = 35,4°), **aber es steht kein Ergebnis da**.
  S_d1 = 100 mW/m² · cos 55°/cos 35,4° = **70,4 mW/m²**.
- **3.3 ~3/8** Die Geometrie hast du **richtig**: δ = φ + β = 15° + 35,4° = **50,4°**
  (dein 40°/50°-Weg über die Winkelsumme führt aufs selbe).
  Und du warst einen Schritt vor der Pointe: arcsin(sin δ/n) mit n = 0,707 gibt
  arcsin(1,09) — **nicht lösbar ⇒ Totalreflexion**. Grenzwinkel δ_g = arcsin√(1/2) = 45° < 50,4°.
  ⇒ **S_r2 = S_d1 = 70,4 mW/m², S_d2 = 0.** Kein Fresnel, kein q.
- **3.4 0/2 (leer)** Antwort ist ein Satz: **„Nichts ändert sich, weil Totalreflexion
  polarisationsunabhängig ist."**

## A4 Leitungstransformation — 9–11/19

- **4.1 ~1–2/4** λ = 71,43 cm ✓, β = 8,8 1/m ✓, βl₁ = 201,6° ✓ — dann Vorzeichenfehler:
  du hast Z₁ = Z_L·(Z₀ − jZ_L tan βl)/(Z_L + jZ₀ tan βl) gerechnet.
  Das **Minus im Zähler gehört zur Rückwärtsformel 3b** (und dort steht es *auch im Nenner*).
  Vorwärts von der Last nach vorn (K4, Zeile 3) ist es **+j in beiden**:
  Z(l) = Z_L·(Z(0) + jZ_L tan βl)/(Z_L + jZ(0) tan βl) ⇒ **Z₁ = (57,44 + j90,24) Ω**.
  **Selbstcheck:** Teilaufgabe 2 sagt „für Z₁ = (60 + j90) Ω" — dein (41,81 − j98,9) hätte
  dort auffallen müssen, allein schon am Vorzeichen des Imaginärteils.
- **4.2 ~4–5/6** Y₁ = (5,13 − j7,69) mS ✓, C_P = 2,9 pF ✓ (Wert und Weg richtig; in der
  Zeile steht Y₂ = Y₁ − jωC, gemeint und gerechnet ist Y₂ = Y₁ **+** jωC — der Zahlenwert
  stimmt, aber schreib das Vorzeichen sauber hin). Der zweite gefragte Wert fehlt bzw.
  ist nicht erkennbar: **Z₂ = 1/5,13 mS = 195 Ω**.
- **4.3 ~0–1/5** Hier liegt der zweite echte Verlust: du hast Z₃ = Z₂ = 200 Ω gesetzt,
  das ist die **λ/2**-Regel. Es ist aber βl₂ = 2π·0,1786/0,7143 = 1,571 = **90° ⇒ λ/4**.
  ⇒ **Z₃ = Z_L2²/Z₂ = 240²/200 = 288 Ω**.
  Vor jeder Transformation einmal l/λ ausrechnen: 0,1786/0,7143 = **0,25**. Das kostet
  10 Sekunden und entscheidet zwischen „bleibt gleich" und „invertiert".
  **Selbstcheck:** 4.4 gibt Z₃ = 290 Ω vor — das ist 288, nicht 200.
- **4.4 ~3,5/4** Z_L3 = √(290·50) = **120,4 Ω** ✓. l₃: die Begründung „reell → reell geht
  nur mit λ/4" ist richtig, aber **l₃ = λ/4 = 17,86 cm**; wenn du Vielfache angibst, dann
  nur **ungerade**: (2n+1)·λ/4. „n·λ/4" ist zu weit, weil n = 2 wieder λ/2 wäre.

## A5 Antennen — ~1/20

Fast alles leer. Alle vier Teile hängen an zwei FS-Formeln (K5/8.5):
**A_w = λ²G/4π** und **S = P·G/(4πr²)**, für Flächenstrahler **A_w ≈ A_geom**.

- **5.1 0/5** λ₀ = c₀/f₀ = 27,3 mm; A = π/4·d_S² = 7,069·10⁻² m²;
  G = 4πA/λ² = 1194 ⇒ **g_S = 10 dB·lg 1194 = 30,8 dBi**.
- **5.2 ~1/3** G = 10^(30/10) = 1000 ✓ — dann aber **d = 30 cm statt r = 36 000 km**
  eingesetzt. Das „d" in S = G·P/(4πd²) ist immer die **Entfernung**:
  S_E = 1000·100 W/(4π·(3,6·10⁷ m)²) = **6,14 pW/m²**.
  Ein Blick auf die Größenordnung entlarvt das sofort: 88,4 kW/m² wären mehr als
  Sonneneinstrahlung, aus 100 W in 36 000 km Entfernung.
- **5.3 0/5** A_w = P_E/S_E = 1,5 pW/6,0 pW/m² = 0,25 m²;
  d_E = √(4A/π) = **56,4 cm**.
- **5.4 0/7** G = 4πA_w/λ² = 4224; ein λ/2-Dipol hat G = 1,64
  ⇒ **N = 4224/1,64 = 2576 Dipole**; Länge l = (N−1)·λ/4 = **17,6 m**.
  (Mit dem Ersatzwert d_E = 60 cm: N = 2913, l = 19,9 m.)

---

## Was daraus für Fr/Sa folgt

1. **A5 zuerst und komplett** — der einzige Typ, der in dieser Klausur bei 0 stand, und
   der einzige, der nie gerechnet wurde. SoSe25 A5 mit Lösung, dann SoSe22 A5 allein.
   A5 ist rechnerisch der einfachste Typ (vier Formeln), das sind ~20 sichere Punkte.
2. **A2 nachziehen** (SoSe25 A2 ist der Altrückstand): speziell Laufzeit über v_gr und
   die Dämpfungs-Varianten.
3. **FS-Lücken sind geschlossen** (eingebaut am 24.07., FS jetzt 11 Seiten, 0 Overfull):
   - K2 neu: „wie lange braucht ein Impuls" → v_gr = c₀√(1 − (λ₀/λ_c)²), τ = l/v_gr
   - K2 neu: „Dämpfung durch das Dielektrikum / max. tanδ" → λ_ε = λ₀/√ε_r,
     α_ε = π tanδ/(λ_ε·√(1 − (λ_ε/2a)²)), nach tanδ umgestellt
   - K1: Schirmdämpfung jetzt mit beiden Richtungen, w = δ·a/(8,686 dB);
     das alte A = e^(−w/δ) ist raus (genau die Falle aus 1.4)
   - K0b neu: **dB → Verhältnis immer 10^…, nie e^…** (40 dB ≙ 1/100, 3 dB ≙ 1/2)
   - K2-Fallstricke: f_c ist immer die des *gewählten* Hohlleiters (c/2a), nicht die
     Bandgrenze aus der Angabe
   - **Achtung: K4 und K5 stehen jetzt auf Seite 11**, K2+K3 auf Seite 10 — beim
     Ausdrucken/Blättern in der Klausur daran denken.
4. **Selbstcheck-Regel, die in dieser Klausur allein ~11 Punkte gerettet hätte:** Die
   Angaben späterer Teilaufgaben sind die Kontrolle der früheren.
   A2.4 „ε_r = 2,0" widerlegt 2,25 · A4.2 „Z₁ = (60 + j90) Ω" widerlegt (41,8 − j98,9) ·
   A4.4 „Z₃ = 290 Ω" widerlegt 200 Ω. Nach jeder Teilaufgabe 5 Sekunden nach unten schauen.
5. **Zeitdisziplin:** Es sind 28 Punkte unbearbeitet liegengeblieben, während in A3/A4
   an einzelnen Schritten gerechnet wurde. Bei 0,9 min/Punkt heißt das: A5 (20 P) hätte
   18 Minuten gebraucht. Nächste Probeklausur: erst alle Teilaufgaben *anlesen* und die
   billigen zuerst holen.
