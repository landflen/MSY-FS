# Lösungen — Übung 1: Sequenztypen und ihre Fallen

Erst selbst vorhersagen, dann hier nachlesen. Die Zahl ist nicht der Punkt —
die Begründung ist es.

| Nr | Ergebnis | Worum es geht |
|---|---|---|
| 1.1 | `'chatnik'` | Slicing |
| 1.2 | `(4, 4, 5)` | Zuweisung kopiert nicht |
| 1.3 | `99` | flache Kopie |
| 1.4 | `[[1, 0, 0], [1, 0, 0]]` | `*` vervielfacht Referenzen |
| 1.5 | `[1, 2]` | Default-Argument lebt weiter |
| 1.6 | `('int', 1)` | Klammern machen kein Tupel |
| 1.7 | `(None, [1, 2, 3])` | `.sort()` gibt nichts zurück |
| 1.8 | `['a', 'b', 'e', 'n']` | Menge wirft Duplikate weg |
| 1.9 | `(['a', 'b', 'c'], 0)` | `get` mit Default |
| 1.10 | `[1, 9, 25]` | List Comprehension mit Filter |
| 1.11 | `[10, 7, 4, 1]` | `range` mit negativer Schrittweite |
| 1.12 | `TypeError` | Strings sind unveränderlich |
| 1.13 | `(True, False)` | `==` vergleicht Inhalt, `is` Identität |
| 1.14 | `'a-b-c'` | `split()` ohne Argument |

## Die Fallen im Einzelnen

**1.1 Slicing.** `s[2:6]` heißt „ab Index 2 **bis vor** 6" → Indizes 2,3,4,5 → `'chat'`.
Die obere Grenze ist immer ausgeschlossen; deshalb ist `len(s[a:b]) == b - a`.
`s[-3:]` zählt von hinten: die letzten drei Zeichen, `'nik'`.

**1.2 Zuweisung kopiert nicht.** `b = a` gibt der *selben* Liste einen zweiten Namen.
Was du über `b` änderst, siehst du über `a` — beide sind 4 lang. Erst `a[:]`
(oder `list(a)`, `a.copy()`) legt eine neue Liste an, die unabhängig auf 5 wächst.
Das ist der häufigste Python-Anfängerfehler überhaupt und ein sicherer Klausurkandidat.

**1.3 Flache Kopie.** `m[:]` kopiert die *äußere* Liste, aber die inneren Listen sind
in beiden dieselben Objekte. `n[0][0] = 99` ändert die innere Liste, die `m` auch benutzt.
Wenn du wirklich alles unabhängig brauchst: `import copy; copy.deepcopy(m)`.

**1.4 `*` vervielfacht Referenzen.** `[[0]*3]*2` ist nicht „zwei Zeilen", sondern
zweimal *dieselbe* Zeile. Eine Änderung erscheint in beiden. Richtig ist
`[[0]*3 for _ in range(2)]` — die Comprehension erzeugt jedes Mal eine neue Liste.
Genau diese Falle trifft dich beim Aufbau einer Matrix.

**1.5 Default-Argument lebt weiter.** Der Default-Wert wird **einmal** bei der
Definition der Funktion erzeugt, nicht bei jedem Aufruf. Die Liste bleibt also
zwischen den Aufrufen bestehen und füllt sich auf. Die Standardlösung:
`def sammle(x, ziel=None): if ziel is None: ziel = []`.

**1.6 Klammern machen kein Tupel.** Das Komma macht das Tupel, nicht die Klammer:
`(5)` ist die Zahl 5 in Klammern, `(5,)` ist ein Tupel mit einem Element.
Deshalb schreibt man Ein-Element-Tupel immer mit Komma.

**1.7 `.sort()` gibt nichts zurück.** Methoden, die ein Objekt *an Ort und Stelle*
ändern, geben in Python `None` zurück — `list.sort()`, `list.append()`, `list.reverse()`.
Wer `y = x.sort()` schreibt, hat `None` in der Hand. Willst du eine sortierte Kopie,
nimm die Funktion `sorted(x)`.

**1.8 Menge.** `set("banane")` zerlegt den String in Zeichen und wirft Duplikate weg:
`{'b','a','n','e'}`. Eine Menge hat keine Reihenfolge — deshalb steht `sorted(...)`
drumherum, sonst wäre die Ausgabe nicht vorhersagbar.

**1.9 `dict`.** `list(d)` gibt die *Schlüssel* (nicht die Werte), und zwar in
Einfügereihenfolge — die ist seit Python 3.7 garantiert. `d.get("z", 0)` liefert den
Default `0` statt eines `KeyError`, den `d["z"]` auslösen würde.

**1.10 List Comprehension.** `if x % 2` filtert die ungeraden Zahlen: jede Zahl außer 0
ist „wahr", 0 ist „falsch". Aus 1, 3, 5 werden die Quadrate 1, 9, 25.

**1.11 `range` rückwärts.** `range(10, 0, -3)` startet bei 10 und geht in Dreierschritten
abwärts, solange der Wert **größer als 0** ist: 10, 7, 4, 1. Die 0 selbst kommt nie vor,
weil die Grenze auch hier ausgeschlossen ist.

**1.12 Strings sind unveränderlich.** Es gibt keine Zuweisung an eine Position im String —
`TypeError: 'str' object does not support item assignment`. Ein neuer String muss gebaut
werden: `"X" + s[1:]`.

**1.13 `==` gegen `is`.** `==` fragt „gleicher Inhalt?", `is` fragt „dasselbe Objekt im
Speicher?". Zwei gleich aussehende Listen sind gleich, aber nicht identisch.
`is` benutzt man praktisch nur für `is None`.

**1.14 `split()` ohne Argument.** Ohne Trennzeichen zerlegt `split()` an beliebig vielen
Leerzeichen und wirft leere Teile am Rand weg → `['a','b','c']`. Mit Argument,
`" ".split(" ")`, bekämst du leere Strings dazwischen.
