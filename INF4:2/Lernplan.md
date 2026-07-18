# INF4/2 — Lernplan

**Prüfung:** Mo, 20.07.2026, 08:30–10:00 — **90 Minuten Bearbeitungszeit**
Der Prof sagt, die Klausur sei „in 45 Minuten machbar" → doppelte Zeit als Reserve. Kein Zeitdruck-Fach, aber: der Umfang ist auf 45 Min. ausgelegt, d. h. **die Aufgaben sind eher kurz und dafür präzise zu beantworten**. Punkte gehen über Sauberkeit verloren, nicht über Tempo.
**Hilfsmittel:** Praktikumszettel mitbringen! (In V8 steht „Klausur: keine Hilfsmittel" — beim Prof gegenchecken, ob das nur für die dortige Aufgabe galt.)

---

## Prüfungsthemen (aus der Mitschrift des Profs)

1. **Newton-Iteration** — nichtlineare Iterationen, ausdrücklich *nur* Newton
2. **Bit Wizardry** — n = Anzahl Bits im Wort; O(1) / O(n) / O(log n); Masken für 32-Bit-Worte, Verdopplung auf 64 Bit; „O(1) heißt nicht nur 1 Befehl"
3. **Code-Optimierung** — Floating Point nach Geschwindigkeit; „POW kommt drin vor"
4. **Asymptotik** — O-Notation, saubere Definition
5. **Relationen** — zeigen, dass etwas *keine* Äquivalenzrelation ist (vom Prof in Klammern → wackelig, aber billig zu lernen)

**Kommt nicht dran:** Primzahlen (Fermat, Miller-Rabin) → **V10 komplett überspringen.**

---

## Materialzuordnung

| Datei | Inhalt | Relevanz |
|---|---|---|
| `V5.pdf` | Bit Wizardry Start, O-Definition, Rotate, O(n) vs. O(log n) | **Kern** |
| `V6.pdf` | Bit Wizardry: popcount per Divide & Conquer mit Masken | **Kern** |
| `V7.pdf` | Fixpunkte (attraktiv/repulsiv/superattraktiv), Newton hergeleitet — markiert „Klausuraufgabe" | **Kern** |
| `V8.pdf` | Newton für 1/d, √d, 1/√d; Superattraktivität nachweisen | **Kern** |
| `V9.pdf` | Superskalare CPU, Latency/Throughput, teure Befehle (DIV, pow, exp, log), Loop Unrolling, Cache | **Kern** (= „Code optimieren") |
| `V3.pdf` | Äquivalenzrelationen, mod m | nur S. 1 (R/S/T-Nachweis) |
| `V4.pdf` | S. 1: Float-Gleichheit ist **nicht transitiv** → genau das „keine ÄR"-Beispiel. S. 2: Gruppen (irrelevant) | nur S. 1 |
| `V10.pdf` | Zyklische Gruppen, Fermat, Miller-Rabin | **überspringen** |
| `Fixpunkte_Newton.pdf`, `Übungen_Fixpunkt.pdf` | **von Claude erstellt** (keine Vorlesungsunterlagen!) — Skript + Übungen Newton, gegen V7/V8 abgeglichen | Zusatzmaterial, V7/V8 sind die Autorität |
| `fxtbook.pdf` | Nachschlagewerk: Kap. 1 Bit Wizardry, Newton-Kapitel | punktuell |

---

## Zeitbudget

Eingeplant (ohne heute): 5 × 3 h + 1 × 2 h = **17 h**
Geschätzter Netto-Bedarf: **11–12 h**
→ **~5 h Puffer**, bewusst über die Woche verteilt statt gestrichen.

Puffer nutzen für: hängengebliebene Themen, zweiter Probeklausur-Durchlauf, oder — falls INF4/2 früh sitzt — ED.

---

## Wochenplan

> **Vorbereitete Sessions:** Die Erstkontakt-Themen liegen ausgearbeitet in `Lernsessions/` (Skript + Übungen + separate Lösungen): `S1_Bit_Wizardry`, `S3_Newton_Fixpunkte`, `S5_Code_Optimierung_Relationen`. Die Vertiefungstage (Do, Fr) bauen darauf auf.

### Di 14.07. — 08:30–11:30 (3 h) · Bit Wizardry I + Asymptotik
→ **`Lernsessions/S1_Bit_Wizardry.md`** (mit Übungen + Lösungen)
- `V5.pdf` komplett, `V6.pdf` komplett
- O-Notation sauber hinschreiben: T(n) ≤ c·f(n) für n ≥ n₀
- Warum „O(1) heißt nicht nur 1 Befehl"
- Ein-Cycle-Befehle: XOR, AND, NOT, ADD, SUB, NEG, INC, DEC, SHIFT, ROTATE
- Zweierkomplement-Trick: −w = ~w + 1; lowest set bit isolieren
- `bit_rotate_right` von Hand nachvollziehen
- *Puffer: 30 min*

### Mi 15.07. — 08:30–11:30 (3 h) · S1-Wiederholung + Newton I *(getauscht mit Do)*
- **Erst:** S1 überfliegen, unsichere Übungen aus `S1_Bit_Wizardry.md` nochmal rechnen
- **Dann:** → **`Lernsessions/S3_Newton_Fixpunkte.md`** (mit Übungen + Lösungen)
- `V7.pdf` + `V8.pdf` zuerst (echte Vorlesung = Autorität); `Fixpunkte_Newton.pdf` nur als Claude-Lesehilfe danach
- Fixpunkt Φ(x*) = x*; attraktiv |Φ'| < 1, repulsiv |Φ'| > 1, superattraktiv Φ' = 0
- Newton herleiten: Φ(x) = x − f(x)/f'(x), zeigen dass Φ'(Nullstelle) = 0
- Konvergenzordnung: Anzahl korrekter Ziffern verdoppelt sich

### Do 16.07. — 08:30–11:30 (3 h) · Bit Wizardry II (Masken)
- popcount per Divide & Conquer: 0x5555…, 0x3333…, 0x0f0f… **selbst herleiten**, nicht auswendig
- Masken von 32 auf 64 Bit verdoppeln
- O(n) (AND + SHIFT 1) vs. O(log n) (Divide & Concat) begründen können
- Shift-and-Add-Multiplikation
- *Puffer: 45 min*

### Fr 17.07. — 08:30–11:30 (3 h) · Newton II — die Klausuraufgaben
Die drei Klassiker aus `V8.pdf`, jeweils: N(x) aufstellen → Fixpunkt prüfen → Superattraktivität zeigen (über N'(x*) = 0 **oder** über N(x*(1+ε)) = x*(1 − ε²)):
- **1/d** über f(x) = 1/x − d → N = x(2 − dx) *(division-frei!)*
- **√d** über f(x) = x² − d → N = ½(x + d/x)
- **1/√d** über f(x) = 1/x² − d → N = x + x(1 − dx²)/2 — vom Prof mit „Klausur" markiert
- `Übungen_Fixpunkt.pdf` rechnen
- *Puffer: 30 min*

### Sa 18.07. — 08:30–11:30 (3 h) · Code-Optimierung + Relationen
→ **`Lernsessions/S5_Code_Optimierung_Relationen.md`** (mit Übungen + Lösungen)
- `V9.pdf`: Latency vs. Throughput; schnelle Befehle (1 Cycle) / MUL (few) / **teure Befehle DIV, MOD, sin, cos, exp, log, pow (50–300 Cycles)**
- Optimier-Repertoire: `pow(x,3)` → `x*x*x`; Division → Multiplikation mit vorberechnetem Kehrwert; Loop Unrolling (mehrere Teilsummen s0..s3); Cache-freundlich; Branches vermeiden
- Relationen: R/S/T prüfen; `V4.pdf` S. 1 — Float-Vergleich mit eps ist **nicht transitiv** (x~y, y~z, aber x≁z)
- *Puffer: 45 min*

### So 19.07. — 08:30–10:30 (2 h) · Probeklausur + Lücken
- **Vorher (Sa oder So früh):** → **`Lernsessions/S6_Schwachstellen_Mix.md`** — themenübergreifendes Übungsblatt, gezielt auf die Fehler aus S1-Warm-up und S5 (Randfall 0, Beweis vs. Beispiel, m teilt 0, wiederholtes Quadrieren, Latency/Throughput, Maskenbreite)
- → **`Lernsessions/S7_Probeklausur.md`** mit **45-Min-Wecker** durchrechnen (das ist das Tempo, das der Prof erwartet — in der echten Klausur hast du 90 Min., also fast doppelt so viel Luft)
- Danach gezielt Lücken schließen (Selbst-Auswertung am Ende der Lösungsdatei)
- Praktikumszettel sortieren und in die Tasche legen

---

## Offene Todos aus der S6-Auswertung (17.07.) — vor der Probeklausur abarbeiten

- [ ] **M3 komplett neu rechnen** (ohne aufs alte Blatt zu schauen): a ~ b :⇔ a − b durch 3 teilbar ist eine ÄR. Rezept: R über a − a = 0 = 0·3; S über Vorzeichen drehen (−q); T über **zwei Buchstaben** (q, p) und Addieren. Äquivalenzklassen (Rest-Töpfe 0, 1, 2) mit angeben. Danach gegen `Lernsessions/S6_Schwachstellen_Mix_Loesungen.md` prüfen.
- [ ] **M2 neu in Klausurform:** a·b ungerade → Reflexivität mit a = 2 widerlegen (2·2 = 4 gerade), Schlusssatz „keine ÄR" nicht vergessen.
- [ ] **M4 b) und c) schriftlich beantworten:** Teilt 0 die 7? Teilt 0 die 0? Jeweils mit der Definition x = q·m begründen.
- [ ] **M8 a) und b) neu formulieren** (je 2 Sätze, das Wort **Pipeline** muss vorkommen): Latency = Dauer des Einzelbefehls, Throughput = Rate bei voller Pipeline; bei Datenabhängigkeit zählt die Latency. Gegen Lösungsdatei checken.
- [ ] **M6-Zählweise festigen:** pow(x,12) und pow(x,10) nochmal von Hand mit Minimal-Zählung (je 4 Mult) — Regel: Hand = Code-Zählung − 1, das erste t·s mit t = 1 spart man sich.
- [ ] **O-Definition einmal blind hinschreiben:** „Es **gibt** c > 0 und n₀, sodass **für alle** n ≥ n₀: T(n) ≤ c·f(n)" — Quantoren in genau dieser Reihenfolge. Dazu die saubere Kette für 7n + 50: ≤ 7n + 50n = 57n für n ≥ 1.
- [ ] **Schlusssatz-Disziplin:** bei jeder Relationen-Aufgabe zum Schluss explizit „⇒ ÄR" / „⇒ keine ÄR, da X verletzt" hinschreiben (fehlte bei M1).
- [ ] Direkt vor S7 (Probeklausur): **Merkkasten einmal komplett durchlesen.**

---

## Merkkasten (wächst mit)

- **O-Notation:** **Es gibt** c > 0 und n₀ (Existenz — du darfst sie wählen!), sodass **für alle n ≥ n₀**: T(n) ≤ c·f(n). Das „für alle" gehört nur zum n, nie zum c (S6-M10-Befund)
- **Bit Wizardry:** n = **Bits im Wort**, nicht Anzahl Elemente
- **−w = ~w + 1**
- **Superattraktiv:** N'(x*) = 0 → quadratische Konvergenz
- **Newton 1/d:** N(x) = x(2 − dx) — braucht keine Division
- **Teuer:** DIV, MOD, pow, exp, log, sin, cos
- **O(1)-Test:** „Ändert sich die Schrittzahl, wenn n wächst?" Nein → O(1), egal ob 3 oder 40 Befehle
- **n₀:** erlaubt endlich viele Ausnahmen bei kleinen n — für n < n₀ darf T(n) > c·f(n) sein
- **O(log n)-Begründung:** Blockgröße verdoppelt sich pro Schritt ⇒ log₂(n) Schritte (64 Bit: 6)
- **Selbsttest Rotation:** erhält die Anzahl der Einsen — Einsen zählen vor/nach!
- **C-Klammern:** `+` und `==` binden stärker als `&` → immer `((x>>1) & m) + (x & m)` schreiben
- **Maskenbreite:** *jede* Maske ist so breit wie das ganze Wort — bei 128 Bit hat auch die neue Maske 32 Hex-Ziffern (16× `0`, 16× `f`)
- **Relationen widerlegen:** ein konkretes **Zahlen**-Gegenbeispiel hinschreiben (nicht nur „gilt nicht"); beweisen dagegen nur allgemein (Zahlenbeispiele sind kein Beweis!)
- **Randfälle bei „für alle":** auf ℤ immer die **0** und negative Zahlen einsetzen (0·0 > 0 ist falsch!)
- **m teilt 0 — immer** (0 = 0·m, q = 0 erlaubt) → Reflexivität von „mod m" ist nie in Gefahr
- **Reflexivität = Definition mit (a, a) füttern:** in der Bedingung landet **a − a = 0** (bzw. a·a), nie a allein — „a nicht durch 3 teilbar" ist kein R-Argument! (S6-M3-Befund)
- **ÄR beweisen (mod m):** R: a−a = 0 = 0·m ✓; S: Vorzeichen drehen, b−a = (−q)·m; T: **verschiedene Buchstaben** ansetzen (a−b = q·m, b−c = **p**·m) und **addieren** → a−c = (q+p)·m. Nie dasselbe q für beide Voraussetzungen! (S6-M3-Befund)
- **R/S auch mit einem Gegenbeispiel widerlegbar:** „für alle a" heißt ganz ℤ — bei „a·b ungerade" killt a = 2 die Reflexivität (2·2 = 4 gerade). Nicht nur T braucht Gegenbeispiele! (S6-M2-Befund)
- **power_r2l-Zählung:** (Stelle MSB − 1) Quadrierungen + (Anzahl gesetzter Bits) t-Produkte — bei e = 13: 3 + 3 = **6**
- **Hand-Zählung ≠ Code-Zählung:** „möglichst wenige Mul" von Hand = Code-Zählung **− 1** (das erste t·s mit t = 1 spart man sich): pow(x,16) = 4, pow(x,12) = 4, pow(x,10) = 4. Welche Zählung gefragt ist, sagt die Aufgabe („Code führt aus" vs. „möglichst wenige") — S6-M6-Befund
- **Latency folgt nicht aus Throughput:** Throughput = Rate (pro Cycle fertig), Latency = Dauer des Einzelbefehls. In der Antwort muss das Wort **Pipeline** fallen: 3 Stufen, pro Cycle kann ein **neues** MUL rein (bis zu 3 gleichzeitig unterwegs), ab Cycle 3 wird jeden Cycle eines fertig — so sind Latency 3 **und** Throughput 1/Cycle zugleich wahr (S6-M8-Befund)
