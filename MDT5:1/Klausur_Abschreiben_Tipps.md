# Spickzettel: Klausuraufgabe an Claude übergeben (Abschreiben)

> **Situation:** 90 Min Klausur · Internet erlaubt · Aufgabe darf **nicht fotografiert/hochgeladen** werden → ich muss sie **abtippen**.
> **Ziel:** so schnell wie möglich, ohne dass Claude später umbauen muss.

---

## Die goldene Regel

> **Erst ALLES abtippen → dann Bild beschreiben → dann bauen lassen.**
> Nicht Stück für Stück! Sonst baut Claude die Architektur um, sobald eine späte Anforderung kommt = Zeitverlust.

---

## Schritt für Schritt

### 1. Alle funktionalen Anforderungen am Stück abtippen
- Komplett, nicht häppchenweise.
- Grund: Claude legt Architektur (Sim-Kern, Datenmodell, Rotation) von Anfang an auf die *ganze* Aufgabe aus.

### 2. Allgemeine Anforderungen + Punktzahlen mitnehmen
- Package-Name (`de.NAME.wise25`), „darf nicht abstürzen", „muss kompilierbar sein".
- **Punkte in Klammern dranhängen** → z.B. `(5P)`. Claude erkennt die Gewichtung und priorisiert.

### 3. Abbildung in Worten beschreiben (nicht hochladen)
- Nur, was das Bild **zusätzlich** zum Text zeigt: Layout-Reihenfolge, Position von Elementen, exakte Beschriftungen.
- Kurze Stichpunkte reichen (Vorlage unten).

### 4. Erst dann bauen lassen
- Claude bitten: **„Spiegel mir die Anforderungen erst als Checkliste zurück."**
- So fange ich Abtipp- und Verständnisfehler ab, **bevor** Code entsteht.

---

## Zeitspar-Tricks beim Tippen

| Mach das | Statt |
|----------|-------|
| Stichpunkte: `2 SurfaceViews = 2 Welten, Teilchen bewegen sich, prallen am Rand ab` | ganze Sätze abschreiben |
| Punkte dranhängen: `Teleport Portal → andere Welt, gleiche rel. Position (5P)` | Punkte weglassen |
| Deckblatt/USB-Hinweise/Prüferdaten **weglassen** | alles abtippen |

### ⚠️ NICHT kürzen — wörtlich übernehmen:
- **Zahlenwerte** (z.B. „3 Teilchen pro Welt").
- **Farben** (hellrot/dunkelrot, hellblau/dunkelblau, cyan).
- **Textformate exakt** — die werden wörtlich bewertet:
  - `Welt X: Y Teilchen`
  - `Gesamt-Schritte: N`

---

## Vorlage Bildbeschreibung (anpassen)

```
Screenshot, Portrait-Layout, von oben nach unten:
- TextView "Welt 1: 3 Teilchen"
- großes hellrotes Rechteck (Welt 1) mit dunkelroten Punkten;
  links mittig senkrechtes cyan Portal, beschriftet "Portal 1"
- TextView "Welt 2: 3 Teilchen"
- großes hellblaues Rechteck (Welt 2) mit dunkelblauen Punkten;
  rechts mittig senkrechtes cyan Portal "Portal 2"
- TextView "Gesamt-Schritte: 0" (mittig)
Querformat: beide Welten nebeneinander, Textfelder jeweils darüber.
```

---

## Mini-Checkliste vor dem Loslegen

- [ ] Alle funktionalen Anforderungen abgetippt (am Stück)
- [ ] Allgemeine Anforderungen + Package-Name dabei
- [ ] Punktzahlen in Klammern notiert
- [ ] Bild in Stichpunkten beschrieben
- [ ] Zahlen / Farben / Textformate **wörtlich**
- [ ] Claude um Checkliste-Rückspiegelung gebeten → *dann erst Code*

> Vollständiger Leitfaden: siehe `Klausur_Leitfaden_Claude.md`
