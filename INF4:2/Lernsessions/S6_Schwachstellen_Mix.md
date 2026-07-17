# S6 — Schwachstellen-Mix (themenübergreifendes Übungsblatt)

Gezielt auf die Fälle, die beim Üben (S1-Warm-up + S5) danebengingen. Lösungen in `S6_Schwachstellen_Mix_Loesungen.md`.

| Aufgabe | trainiert |
|---|---|
| M1, M2 | Randfälle testen (die 0!) bei „für alle"-Aussagen |
| M3 | Beweis ≠ Zahlenbeispiele; positiver R/S/T-Nachweis |
| M4 | „m teilt 0" — Definition von Teilbarkeit |
| M5 | Klausurform: Gegenbeispiel **konkret** hinschreiben |
| M6, M7 | wiederholtes Quadrieren + Multiplikationen zählen |
| M8 | Latency vs. Throughput sauber trennen |
| M9 | Maskenbreite = Wortbreite (Ü15-Wiedervorlage) + O(log n)-Schluss |
| M10 | O-Definition mit konkreten c, n₀ |
| M11 | C-Präzedenz (Kurz-Check) |

---

### M1 — Randfall-Training
Prüfe für die Relation auf ℤ: **a ~ b :⇔ a·b ≥ 0** alle drei Eigenschaften (R, S, T) und entscheide, ob ÄR. Vorsicht: diesmal killt die 0 nicht die Reflexivität — aber schau genau hin, wo sie zuschlägt.

### M2 — Noch ein Randfall
Auf ℤ: **a ~ b :⇔ a·b ungerade**. Reflexiv? (Ein konkretes Gegen-a genügt, falls nicht.) Symmetrisch? Ist die Relation eine ÄR?

### M3 — Beweisen heißt allgemein argumentieren
Zeige, dass **a ~ b :⇔ a − b ist durch 3 teilbar** eine Äquivalenzrelation auf ℤ ist.
Regel für diese Aufgabe: **keine einzige konkrete Zahl verwenden** — nur die Definition „durch 3 teilbar heißt: Differenz = q·3 mit q ganz". Gib am Ende die Äquivalenzklassen an.

### M4 — Teilbarkeit und die 0
a) Teilt 7 die 0? b) Teilt 0 die 7? c) Teilt 0 die 0?
Begründe jede Antwort mit der Definition „m teilt x :⇔ x = q·m für ein ganzes q".

### M5 — Die Klausurantwort in voller Form
Zeige, dass **a ~ b :⇔ |a − b| ≤ 0,5** auf ℝ keine Äquivalenzrelation ist. Schreibe die Antwort so auf, wie sie am Montag auf dem Blatt stehen muss: alle drei Eigenschaften benennen, R und S kurz begründen, die verletzte Eigenschaft mit **konkreten Zahlen** widerlegen (nicht nur „gilt nicht").

### M6 — Wiederholtes Quadrieren
Optimiere ohne pow, mit möglichst wenigen Multiplikationen (Zwischenvariablen erlaubt):
a) `pow(x, 16)`  b) `pow(x, 12)`  c) `pow(x, 10)`
Gib jeweils die Anzahl der Multiplikationen an. (Hinweis zu b/c: erst Zweierpotenzen sammeln, dann die passenden multiplizieren — der Exponent binär gelesen sagt dir, welche.)

### M7 — power_r2l zählen
Rechne `power_r2l(a, 25)` von Hand durch (25 = `11001`): Tabelle mit e, e&1, s, t nach jedem Durchlauf.
Dann: Wie viele Multiplikationen führt der **Code** aus? Kontrolliere mit der Zählregel **(Stelle des MSB − 1) Quadrierungen + (Anzahl gesetzter Bits) t-Produkte** — beide Wege müssen dieselbe Zahl liefern. Wie viele wären es naiv?

### M8 — Latency ist keine Folge von Throughput
Eine CPU hat für MUL: Latency 3 Cycles, Throughput 1 pro Cycle.
a) Erkläre, wie beides gleichzeitig wahr sein kann (Stichwort Pipeline).
b) Ein Kommilitone sagt: „Throughput 1 pro Cycle, also ist ein einzelnes MUL nach einem Cycle fertig." Was ist daran falsch?

### M9 — Verdopplung, Wiedervorlage
popcount wird von 64 auf **256-Bit-Worte** erweitert (ja, 256).
a) Wie viele Maskenschritte hat die Funktion? (Begründung muss den Schluss „Blockgröße verdoppelt sich pro Schritt ⇒ log₂(n) Schritte" enthalten.)
b) Wie breit ist **jede** Maske der neuen Funktion, in Hex-Ziffern?
c) Schreibe die erste Maske (5er-Muster) und die letzte Maske als Muster hin (Anzahl der Wiederholungen genügt, z. B. „k× `f`, dann m× `0`" — aber mit den richtigen Zahlen).

### M10 — O-Definition anwenden
Gib die Definition von O(f(n)) an. Zeige dann mit konkreten Werten für c und n₀, dass T(n) = 7n + 50 in O(n) liegt.

### M11 — Kurz-Check Präzedenz
Was ist an dieser Zeile falsch, was rechnet C tatsächlich, und wie lautet die korrigierte Zeile?
```c
x = (x >> 2) & 0x33 + (x & 0x33);
```
