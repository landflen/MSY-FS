# Notentracker

Tracking von Noten, Aufwand und Selbsteinschätzung pro Prüfung.
Skala Gefühl: frei formuliert. Aufwand/Zeit: grob in Stunden bzw. Lernzeitraum.

## Übersicht

| Modul  | Prüfung    | Aufwand | Gefühl vorher | Gefühl danach | Note |
|--------|------------|---------|---------------|---------------|------|
| MDT5/1 | WiSe 25/26 | ≈ 4 h  | wird leicht   | gut           | 1,0  |
| INF4/1 | 13.07.2026 | ≈ 20 h (7 Sessions über 2 Wochen) | gut vorbereitet | war mist | 2,3  |
| INF4/2 | 20.07.2026 |         |               |               | 1,7  |
| ED     | 27.07.2026 | Reste der drei anderen Prüfungen; Probeklausuren ~40–48/100 | schlecht vorbereitet | – | 3,0  |
| MDT5/2 | 31.07.2026 | 10 Sessions 8.–30.07. (Praktika 01–11, 7 Blätter, alle 12 Aufgabentypen) | gut vorbereitet | gut, zeitlich sehr entspannt | **1,3** |

## Details

### MDT5/1 (WiSe 25/26)
- **Gefühl vor der Klausur:** wird leicht, aber hängt alles von KI ab
- **Gefühl direkt danach:** gut
- **Note:** 1,0
- **Aufwand/Zeit:** _noch nachtragen_

### INF4/1 — Algorithmen & Datenstrukturen (13.07.2026)
- **Gefühl vor der Klausur:** gut vorbereitet, wird einfach
- **Gefühl direkt danach:** war Mist — Blackout, Flüchtigkeitsfehler, teilweise Aufgaben nicht bearbeitet
- **Note:** 2,3 (bestätigt)
- **Aufwand/Zeit:** ≈ 20 h, rekonstruiert aus dem Lern-Logbuch (INF4:1/CLAUDE.md) — 7 Sessions in 2 Wochen:
  - 29.06. — Kap. 01–02 + Praktikum 1 + Übungsblatt
  - 30.06. — Kap. 03 + Praktikum 02 + Übungsblatt + Open-Book-Umplanung (Plan: 14:00–17:15)
  - 01.07. — Kap. 04 + Gesamtskript 4-up gebaut
  - 08.07. — Kap. 06 + 07 inkl. Traces (großer Tag, viele Logeinträge)
  - 09.07. — Kap. 08 + 09 + 10 inkl. Traces
  - 10.07. — Learnings-PDF komplettiert + radikale Kürzung 27→11 Seiten (Plan: 08:15–12:00)
  - 12.07. — Kap. 11 + 12 (Dijkstra/A*/MST-Traces)
  - _Hinweis: geplante Slots 03.07. und 06.07. tauchen im Log nicht auf — vermutlich ausgefallen/verschoben. Stundenzahl ist Schätzung (2–4 h pro Session), bitte korrigieren._

### INF4/2 — Low Level und Seminumerische Algorithmen (20.07.2026)
- **Note:** 1,7 (bestätigt)
- **Gefühl/Aufwand:** _noch nachtragen_

### ED — Elektrodynamik (27.07.2026)
- **Note:** 3,0 (bestätigt) — **bestanden im ersten Anlauf**
- **Gefühl vor der Klausur:** schlecht vorbereitet; die Klausur wurde am 25.07. schon abgesagt
  und am 26.07. doch wieder angesetzt
- **Aufwand:** ED bekam die Restzeit neben INF4/1, INF4/2 und MDT5/2. Drei Probeklausuren lagen
  bei ~40–48 von 100 Punkten, mit 28 bzw. 37 Punkten **unbearbeitet**.
- **Befund:** Die 3,0 liegt deutlich über dem Probeklausurstand. Der Vorbereitungsstand war also
  besser als das Gefühl — die Formelsammlung + die nach Aufgabentyp sortierte Altklausursammlung
  haben unter Zeitdruck getragen. Material bleibt in `ED.zip` archiviert (wird nicht mehr gebraucht).

### MDT5/2 — Maschinelles Lernen zur Anomalieerkennung (31.07.2026)
- **Note:** **1,3** (bestätigt, 03.08.2026) — zweitbeste Note des Studiums nach MDT5/1
- **Gefühl vor der Klausur:** gut vorbereitet — jeder der 12 Aufgabentypen mindestens einmal
  komplett gerechnet, alle 11 Praktika durch, 7 handschriftliche Blätter mit Farbmarkierung
- **Gefühl direkt danach:** gut. **Zeit war sehr entspannt** — erstmals kein Modul mit
  unbearbeiteten Aufgaben (Gegenteil von INF4/1 und ED).
- **Vermutete Mindestfehler (Selbsteinschätzung):**
  - 1 Multiple-Choice-Frage
  - AUC-Kurve: falscher Schwellwert, aber richtig eingegrenzt
  - OCSVM: Zahl der SV richtig hergeleitet (ν = 0,001 → 1 SV, ν = 0,01 → 2 SV bei 20 Punkten),
    Trennlinie jeweils genau auf diese Punkte gelegt. **Nachgeprüft am 01.08.: das ist richtig** —
    SV liegen per Definition *auf* der Grenze, außerhalb liegen nur Verletzer, und ν·n = 0,02
    bzw. 0,2 < 1 ⇒ null erlaubte Ausreißer, Grenze umschließt alle 20 Punkte.
  - Fehlerfinde-Aufgabe (Typ 4) sollte richtig sein
- **Erwartung war:** deutlich besser als 2,0, wenn die Selbsteinschätzung trägt.
- **Befund:** Die Selbsteinschätzung hat getragen — 1,3 ist exakt die „optimistischere Variante"
  aus der Prognose vom 01.08. Damit ist das Gefühl danach hier zum ersten Mal ein guter Schätzer
  gewesen (anders als bei INF4/1 und ED, s. Lehre 7 im Root-`CLAUDE.md`). Der Unterschied:
  das Gefühl stützte sich auf **nachgerechnete Einzelfehler**, nicht auf einen Gesamteindruck.

## Anstehende Prüfungen (zum Nachtragen)

| Modul  | Prüfung    | Gefühl vorher | Gefühl danach | Note |
|--------|------------|---------------|---------------|------|
| SOS    | ~~22.07.2026~~ → offen | — | — | **nicht geschrieben** (nicht im SS 2026 angetreten) |
| INF6/1 | noch offen |               |               |      |
| INF6/2 | noch offen |               |               |      |
| VM     | noch offen |               |               |      |
| PU     | noch offen |               |               |      |

## Vertiefungs-Notentabelle (INF4, MDT5, INF6)

Quelle: Modulhandbuch M-SY (efi_1464_VO_MSY_Modulhandbuch_public.pdf). Das Handbuch nennt keine
eigene "Gewichtungsformel" — die Gewichtung läuft über die Leistungspunkte (ECTS) je Modul.
Alle sechs Wahlpflichtmodule der drei Vertiefungen sind **gleich groß: je 5 ECTS / 150 h**,
mit je eigener schriftlicher Prüfung. Macht 30 ECTS insgesamt → innerhalb dieses Blocks ist der
Schnitt ein einfacher arithmetischer Mittelwert der sechs Noten, kein Modul zieht stärker.

| Modul  | ECTS | Prüfungstermin | Status                        | Note |
|--------|------|-----------------|--------------------------------|------|
| MDT5/1 | 5    | WiSe 25/26      | abgeschlossen                  | 1,0  |
| INF4/1 | 5    | 13.07.2026      | abgeschlossen                  | 2,3  |
| INF4/2 | 5    | 20.07.2026      | abgeschlossen                  | 1,7  |
| MDT5/2 | 5    | 31.07.2026      | abgeschlossen                  | 1,3  |
| INF6/1 | 5    | noch nicht terminiert | offen                    | –    |
| INF6/2 | 5    | noch nicht terminiert | offen                    | –    |

### Schnitt-Berechnung

- **Jetziger Schnitt (alle vier bestätigt):** (1,0 + 2,3 + 1,7 + 1,3) / 4 = 6,3 / 4
  = **1,58** — basiert auf 4 von 6 Modulen (20 von 30 ECTS), alle Noten offiziell.
  Offen sind nur noch INF6/1 und INF6/2.
- **Best Case:** INF6/1, INF6/2 beide 1,0 →
  (1,0 + 2,3 + 1,7 + 1,3 + 1,0 + 1,0) / 6 = 8,3 / 6 = **1,38**
- **Worst Case (realistisch, d. h. beide noch bestanden):** INF6/1, INF6/2 beide 4,0 →
  (1,0 + 2,3 + 1,7 + 1,3 + 4,0 + 4,0) / 6 = 14,3 / 6 = **2,38**
  (durchgefallene Module zählen nicht in den Schnitt, bis sie wiederholt und bestanden sind —
  2,38 ist daher der schlechteste Fall, der überhaupt in die Durchschnittsberechnung eingeht)
- **Realistischer Schnitt (Prognose, 03.08.2026):** INF6/1, INF6/2 mit je ca. 2,0 angesetzt →
  (1,0 + 2,3 + 1,7 + 1,3 + 2,0 + 2,0) / 6 = 10,3 / 6 = **1,72**
  (ED gehört **nicht** in diesen Block — die 3,0 in ED lässt den Vertiefungsschnitt unberührt)
- **Wirkung der MDT5/2-Note:** Die 1,3 hat die alte „optimistischere Variante" exakt bestätigt.
  Gegenüber der Prognose mit 2,0 sinkt der erwartete Vertiefungsschnitt von 1,83 auf **1,72**,
  die Gesamtspanne von 1,33–2,83 auf 1,38–2,38. Der Block ist damit weitgehend festgezurrt —
  selbst zwei 4,0en in INF6 lassen ihn nicht schlechter als 2,38 werden.

## Gesamtnote (ganzer Studiengang, ca. 90 ECTS)

Gleiche Quelle wie oben. Der ganze Master M-SY setzt sich laut Modulhandbuch so zusammen:

| Bereich              | Modul(e)                              | ECTS | Prüfungsform          | Status |
|-----------------------|----------------------------------------|------|------------------------|--------|
| Grundfächer            | VM – Vertiefungsgebiete der Mathematik | 5    | schriftl. Prüfung      | unklar — bisher in keiner Unterlage erwähnt |
| Grundfächer            | SOS – Stochastische u. nichtlineare Systeme | 5 | schriftl. Prüfung      | verschoben, nicht im SS2026 |
| Grundfächer            | ED – Elektrodynamik                    | 5    | schriftl. Prüfung 90'  | ✅ **abgeschlossen 27.07.2026 — Note 3,0** |
| Vertiefung Gruppe 1     | INF4/1+2, INF6/1+2, MDT5/1+2           | 30   | je schriftl. Prüfung   | s. Vertiefungs-Tabelle oben |
| Projekt                | 5a Projektarbeit + 5b Seminar          | 10   | Leistungsnachweis      | offen |
| PU                     | Personal- und Unternehmensführung      | 5    | schriftl. Prüfung 90'  | offen |
| Wahlpflicht Gruppe 2    | 2 WPM à 2 SWS                          | ~5 (rechnerisch ergänzt, im Handbuch nicht beziffert) | Leistungsnachweis | offen, WPM noch nicht gewählt? |
| Abschlussarbeit         | Masterarbeit (23) + Masterseminar (2)  | 25   | Leistungsnachweis      | noch weit weg |
| **Summe**               |                                        | **≈ 90** |                    |        |

**Annahmen für die Rechnung** (Modulhandbuch selbst nennt keine Gewichtungsformel, nur ECTS):
ECTS-gewichteter Durchschnitt über alle 90 ECTS, keine Sonder-/Doppelgewichtung der Masterarbeit,
und Projekt/Gruppe 2/Masterseminar fließen als normale benotete Posten mit ein (ob das in der
SPO wirklich so steht, ist ungeprüft — v. a. bei der Masterarbeit realistisch, bei Projekt/Gruppe 2
evtl. nur Bestehenspflicht ohne Note).

### Schnitt-Berechnung (ganzer Studiengang)

- **Bekannt (alle bestätigt):** MDT5/1 = 1,0 + INF4/1 = 2,3 + INF4/2 = 1,7 + ED = 3,0 + MDT5/2 = 1,3
  → zusammen 25 von 90 ECTS. Summe dieser fünf Noten: 9,3 (ECTS × Note = 46,5). Die übrigen
  65 ECTS sind offen — allein die Masterarbeit (23 ECTS) ist größer als alles bisher Bekannte.
- **Best Case:** alle übrigen 65 ECTS mit 1,0 →
  (46,5 + 65×1,0) / 90 = 111,5 / 90 = **≈ 1,24**
- **Worst Case (realistisch, d. h. alles nur gerade so bestanden):** alle übrigen 65 ECTS mit 4,0
  → (46,5 + 65 × 4,0) / 90 = 306,5 / 90 = **≈ 3,41**

Die Spanne 1,24–3,41 ist erneut enger als vorher (1,22–3,56): Die 1,3 in MDT5/2 hebt den Boden
kaum, drückt aber die Decke um 0,15. Getrieben wird die Spanne weiterhin von den 65 offenen ECTS
(allen voran die Masterarbeit mit 23) — ab hier verengt sie nur noch das Projekt bzw. die
Masterarbeit spürbar, nicht mehr einzelne 5-ECTS-Prüfungen.

### Realistischer Schnitt (Prognose, Stand 03.08.2026)

Auf Basis von Lenas eigenen Einschätzungen für die übrigen Bereiche:

| Bereich                          | ECTS | angesetzte Note | ECTS × Note |
|-----------------------------------|------|------------------|--------------|
| VM (Mathe)                        | 5    | 3,7              | 18,5         |
| SOS                                | 5    | 3,3              | 16,5         |
| **ED** (bestätigt)                 | 5    | **3,0**          | 15,0         |
| MDT5/1 (bestätigt)                 | 5    | 1,0              | 5,0          |
| INF4/1 (bestätigt)                 | 5    | 2,3              | 11,5         |
| INF4/2 (bestätigt)                 | 5    | 1,7              | 8,5          |
| **MDT5/2** (bestätigt)             | 5    | **1,3**          | 6,5          |
| INF6/1, INF6/2 (je ~2,0)           | 10   | 2,0              | 20,0         |
| Projekt + Masterarbeit             | 35   | 1,3              | 45,5         |
| PU                                  | 5    | 1,3              | 6,5          |
| **Zwischensumme**                  | **85** |                | **153,5**    |

→ Realistischer Schnitt über diese 85 ECTS: 153,5 / 85 = **≈ 1,81**
(vorher 1,85 mit MDT5/2 als geschätzter 2,0 — die echte 1,3 bringt also **0,04**)

Mit Wahlpflicht Gruppe 2 (5 ECTS) über volle 90 ECTS gerechnet:

| Gruppe 2 | Rechnung | Schnitt |
|---|---|---|
| 1,0 | 158,5 / 90 | ≈ 1,76 |
| 2,0 | 163,5 / 90 | ≈ 1,82 |
| 4,0 | 173,5 / 90 | ≈ 1,93 |

Der realistische Gesamtschnitt liegt also grob **zwischen 1,76 und 1,93**, mit ≈ 1,81 als Anker.

**Was den Schnitt jetzt noch bewegt:** Projekt + Masterarbeit sind 35 ECTS = 39 % — ein Zehntel
dort wiegt mehr als eine ganze Notenstufe in einem 5-ECTS-Modul (ein 5-ECTS-Modul ist 5/90 ≈ 5,6 %,
eine ganze Note dort ≈ 0,06 im Schnitt). Die vier verbleibenden Prüfungen (VM, SOS, INF6/1, INF6/2)
und PU sind zusammen 25 ECTS.

**Lücke:** nur noch Wahlpflicht Gruppe 2 (~5 ECTS, noch nicht gewählt). Alle fünf geschriebenen
Prüfungen sind benotet und eingetragen.
