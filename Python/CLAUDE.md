# Python-Blockkurs — Lern-Logbuch

Einführungskurs Python, **Blockkurs 21.–24.09.2026**, Tag 1 9:00–15:30, Start in **WB.210**.
**Schriftliche Präsenzklausur Fr 25.09.2026, 10:00.** Kursinfo Stand 23.07.2026.
Aufgaben und Termine liegen in Ambly im Projekt **Python** (unter MSY).

## Kursinhalt (laut Ankündigung)

Überblick Sprache und Programmierumgebung · Variablen und Datentypen (Grunddatentypen,
Sequenztypen) · Funktionen · Module/Pakete · Exception-Handling · OOP und Python-Klassen ·
kurze Einführung GUI/Grafik (voraussichtlich PySide/PyQt) · kurze Einführung NumPy und
Matplotlib.

## Werkzeugstand (07.09.2026)

| | Stand |
|---|---|
| Python | 3.14.7 (Homebrew, `/opt/homebrew/bin/python3`) — Kurs verlangt ≥ 3.11 ✅ |
| NumPy | 2.4.4 ✅ |
| Matplotlib | 3.10.8 ✅ |
| Editor | VS Code ✅ (eigener Editor ausdrücklich erlaubt) |
| IDLE | ⚠️ startet nicht: `_tkinter` fehlt → `brew install python-tk@3.14` |
| PySide6 | ❌ nicht installiert — bewusst auf später verschoben. 6.11.2 hat ein `cp310-abi3`-Wheel, läuft also mit 3.14. Homebrew-Python ist „externally managed" → venv oder `--break-system-packages` |

## Sessions

### 07.09.2026 — Vorbereitung, zwei Übungsblätter
Die Kursgrundlagen (Variablen, Funktionen, Module, Exceptions) sind durch MDT5/2 abgedeckt —
dort lief Python mit NumPy/sklearn im venv `~/.venvs/mdt52`. Vorbereitung deshalb gezielt auf
die zwei Stellen, die das nicht abdeckt und die für den GUI-Teil gebraucht werden:

- `Uebung_01_Sequenztypen.py` — 14 Vorhersage-Aufgaben („Was gibt der Code aus?"), Prüfung
  im Skript selbst, Lösungswerte über `-l`. Themen: Slicing, Kopie vs. Referenz, flache Kopie,
  `[[0]*3]*2`, veränderbares Default-Argument, Ein-Element-Tupel, `.sort()` → `None`, Mengen,
  `dict.get`, Comprehension, `range` rückwärts, unveränderliche Strings, `is` vs. `==`,
  `split`/`join`.
- `Uebung_02_OOP.py` — 5 Schreibaufgaben mit Selbsttest: Grundklasse mit Dunder-Methoden,
  Vererbung mit `super()`, eigene Exception-Klasse, Klassen- vs. Instanzattribut, `@property`
  und `__eq__`.

Beide Musterlösungen sind gegengeprüft (14/14 bzw. 5/5 ✓). Erklärungen in den
`Loesungen_*.md` — bewusst mit Begründung, nicht nur mit Ergebnis.

**Offen:** Aufgabenstand nach dem Bearbeiten hier nachtragen. Nach Kurstag 1 prüfen, ob der
Dozent eine andere Python-Version oder eine bestimmte Umgebung voraussetzt.
