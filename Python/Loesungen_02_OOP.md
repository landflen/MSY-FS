# Lösungen — Übung 2: Klassen, Vererbung, Exceptions

Erst selbst schreiben, bis `python3 Uebung_02_OOP.py` alle fünf auf ✓ hat.
Hier steht eine Musterlösung — nicht *die* einzige richtige.

## 2.1 Grundklasse

```python
class Messreihe:
    def __init__(self, name):
        self.name = name
        self.werte = []

    def hinzufuegen(self, wert):
        self.werte.append(wert)

    def mittelwert(self):
        if not self.werte:
            return 0.0
        return sum(self.werte) / len(self.werte)

    def __len__(self):
        return len(self.werte)

    def __str__(self):
        return f"Messreihe {self.name}: {len(self.werte)} Werte"
```

`self` ist nicht magisch: es ist einfach das erste Argument jeder Methode und zeigt auf
die Instanz, auf der die Methode aufgerufen wurde. `r.hinzufuegen(5)` ist genau
`Messreihe.hinzufuegen(r, 5)`.

Die Methoden mit zwei Unterstrichen (`__len__`, `__str__`) heißen *Dunder*-Methoden.
Sie werden nie direkt aufgerufen — sie klinken deine Klasse in die Sprache ein:
`len(r)` ruft `r.__len__()`, `print(r)` und `str(r)` rufen `r.__str__()`.
Genau darauf baut die ganze Qt-/PySide-Welt auf.

## 2.2 Vererbung

```python
class GefilterteMessreihe(Messreihe):
    def __init__(self, name, min_wert, max_wert):
        super().__init__(name)
        self.min_wert = min_wert
        self.max_wert = max_wert
        self.verworfen = 0

    def hinzufuegen(self, wert):
        if self.min_wert <= wert <= self.max_wert:
            super().hinzufuegen(wert)
        else:
            self.verworfen += 1
```

Zwei Dinge, die man in der Klausur sehen will:

- `super().__init__(name)` — die Elternklasse muss ihre eigene Initialisierung
  machen dürfen, sonst gibt es die Liste `werte` gar nicht. Vergisst man das,
  kommt später ein `AttributeError`.
- **Überschreiben heißt nicht ersetzen.** `hinzufuegen` prüft nur und delegiert das
  eigentliche Anhängen mit `super().hinzufuegen(wert)` nach oben. `mittelwert()` und
  `__len__` musst du gar nicht anfassen — die werden geerbt und funktionieren mit.

Nebenbei: `min_wert <= wert <= max_wert` ist in Python eine erlaubte Kette und
bedeutet genau das, was dasteht.

## 2.3 Eigene Exception

```python
class MessfehlerError(Exception):
    pass


def pruefe_wert(wert):
    if not isinstance(wert, (int, float)) or isinstance(wert, bool):
        raise MessfehlerError(f"kein Zahlenwert: {wert!r}")
    if wert < 0:
        raise MessfehlerError(f"negativer Wert: {wert}")
    return float(wert)


def robuste_summe(liste):
    summe = 0.0
    fehler = 0
    for w in liste:
        try:
            summe += pruefe_wert(w)
        except MessfehlerError:
            fehler += 1
    return (summe, fehler)
```

Eine eigene Exception ist meist nur eine leere Klasse, die von `Exception` erbt —
mehr braucht es nicht. Der Sinn: der Aufrufer kann **gezielt** genau diesen Fehler
abfangen, statt mit `except Exception` alles einzusammeln (auch Tippfehler im
eigenen Code, die man sehen will).

Reihenfolge im try-Block: `try` → `except` → optional `else` (läuft, wenn *kein*
Fehler kam) → optional `finally` (läuft immer, auch bei `return`).

Die `isinstance(wert, bool)`-Zeile ist Feinheit, nicht Pflicht: `bool` ist in Python
eine Unterklasse von `int`, `True` würde sonst als gültiger Messwert 1.0 durchgehen.

## 2.4 Klassen- vs. Instanzattribut

```python
class Sensor:
    def __init__(self, kennung):
        self.kennung = kennung
        self.messwerte = []      # gehört jetzt der Instanz
```

Alles, was **direkt im Klassenkörper** steht, gehört der Klasse und wird von allen
Instanzen geteilt. Bei unveränderlichen Werten (`einheit = "°C"`) ist das erwünscht;
bei einer Liste ist es fast immer ein Fehler, weil alle Sensoren in denselben Eimer
schreiben. Instanz-Zustand gehört nach `__init__` mit `self.`.

Warum es so lange unentdeckt bleibt: `self.messwerte.append(1)` *funktioniert* — die
Liste wird über die Klasse gefunden und verändert. Erst `self.messwerte = [...]`
(Zuweisung statt Änderung) legt ein Instanzattribut an. Dieselbe Falle wie 1.5.

## 2.5 property und Vergleich

```python
class Temperatur:
    def __init__(self, celsius):
        self.celsius = celsius

    @property
    def kelvin(self):
        return self.celsius + 273.15

    def __eq__(self, other):
        return isinstance(other, Temperatur) and self.celsius == other.celsius

    def __repr__(self):
        return f"Temperatur({self.celsius})"
```

`@property` macht aus einer Methode ein **Attribut zum Lesen**: `t.kelvin` ohne
Klammern. Weil kein passender Setter definiert ist, wirft `t.kelvin = 300` einen
`AttributeError` — der Wert ist abgeleitet und soll nicht direkt gesetzt werden.

`__eq__` schaltet `==` frei. Der `isinstance`-Test verhindert einen Absturz beim
Vergleich mit etwas völlig anderem. `__repr__` ist die Darstellung für Entwickler
(Debugger, Listenausgabe), `__str__` die für Benutzer; ist nur `__repr__` da,
wird sie auch für `print` benutzt.
