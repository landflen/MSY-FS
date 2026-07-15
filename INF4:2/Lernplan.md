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
| `Fixpunkte_Newton.pdf`, `Übungen_Fixpunkt.pdf` | Skript + Übungen Newton | Übungsmaterial |
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
- `V7.pdf` + `Fixpunkte_Newton.pdf` (7-seitiges Skript — Hauptquelle, zuerst ganz lesen)
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
- Probeklausur mit **45-Min-Wecker** durchrechnen (das ist das Tempo, das der Prof erwartet — in der echten Klausur hast du 90 Min., also fast doppelt so viel Luft)
- Danach gezielt Lücken schließen
- Praktikumszettel sortieren und in die Tasche legen

---

## Merkkasten (wächst mit)

- **O-Notation:** T(n) ≤ c·f(n) für alle n ≥ n₀, c > 0
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
