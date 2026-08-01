# MSY — Studienübersicht und Repo-Konventionen

Masterstudiengang **Elektronische und Mechatronische Systeme (MSY)**, TH Nürnberg, Fakultät efi.
Dieses Repo enthält Lernmaterial, Formelsammlungen und Lern-Logbücher aller Module.

> **Diese Datei ist der Einstiegspunkt.** Sie sagt, *was* wo liegt und wie der Studienstand ist.
> Fachliche Details und Lernfortschritt stehen in den Logbüchern der einzelnen Module,
> Noten und Selbsteinschätzungen in `Notentracker.md`. Hier wird nichts davon dupliziert.

## Konventionen

- **Ein Ordner pro Modul.** Darin ein `CLAUDE.md` als **Lern-Logbuch** (Sessionfortschritt,
  Stolperfallen, Planänderungen) und — sofern vorhanden — ein `Lernplan_*.md` mit Sessionplan
  und Aufgabentypen. Logbuch und Plan werden getrennt gehalten.
- **Abgeschlossene Module werden gezippt** und liegen als `<Modul>.zip` im Root
  (aktuell: `INF4:1.zip`, `INF4:2.zip`, `MDT5:1.zip`, `ED.zip`). Der entpackte Ordner wird dann
  gelöscht. ⚠️ **Diese Löschungen nicht committen** — nur einzeln bearbeitete Dateien stagen.
  Vor dem Zippen alle `.tex`/`.md` des Moduls committen, damit sie in der Historie bleiben.
- **Git trackt nur `.tex` und `.md`** (siehe `.gitignore`). PDFs, Skripte, Videos, Notebooks
  bleiben lokal. Build-Artefakte (`.aux`, `.log`, `.fls`, `.fdb_latexmk`, `.synctex.gz`) sind
  ignoriert und dürfen jederzeit weggeräumt werden.
- **Formelsammlungen** werden aus `FS_Template/` heraus gebaut; der zugehörige Prompt steht in
  `Formelsammlung_Prompt_Template.md`. Konventionen für den Satz (`\tfrac`, Spaltenregeln,
  Kompilier-Check) sind in den Modul-Logbüchern festgehalten.
- **Organisatorische Dokumente** (Stundenpläne, Modulhandbuch, Merkblätter) liegen in
  `Organisation/`.

## Studienstand (Stand 01.08.2026)

**Das SS 2026 ist durch — alle vier angetretenen Prüfungen bestanden.**

| Modul | ECTS | Status | Note |
|---|---|---|---|
| MDT5/1 | 5 | ✅ abgeschlossen (WiSe 25/26) | **1,0** |
| INF4/1 — Algorithmen & Datenstrukturen | 5 | ✅ abgeschlossen (13.07.2026) | **2,3** |
| INF4/2 — Low Level & Seminumerische Alg. | 5 | ✅ abgeschlossen (20.07.2026) | **1,7** |
| ED — Elektrodynamik | 5 | ✅ abgeschlossen (27.07.2026) → `ED.zip` | **3,0** |
| MDT5/2 — ML zur Anomalieerkennung | 5 | ✅ geschrieben (31.07.2026), Note ausstehend | – |
| SOS — Stochastische u. nichtlineare Systeme | 5 | ⏸ verschoben, nicht im SS 2026 geschrieben | – |
| VM — Vertiefungsgebiete der Mathematik | 5 | ⏸ offen, **kein Material im Repo** | – |
| INF6/1 | 5 | ⏸ offen, noch nicht terminiert | – |
| INF6/2 | 5 | ⏸ offen, noch nicht terminiert | – |
| PU — Personal- und Unternehmensführung | 5 | ⏸ offen (nur Skript vorhanden) | – |
| Wahlpflicht Gruppe 2 | ~5 | ⏸ offen, **WPM noch nicht gewählt** | – |
| Projektarbeit + Masterseminar | 10 | ⏸ offen | – |
| Masterarbeit + Masterseminar | 25 | ⏸ offen | – |

**Es sind rund 60 ECTS offen**, davon 25 ECTS Prüfungsleistungen (VM, SOS, INF6/1, INF6/2, PU)
plus Wahlpflicht Gruppe 2, Projektarbeit und Masterarbeit. **ED ist erledigt und fällt aus der
WiSe-26/27-Planung heraus** — das entlastet das nächste Semester spürbar.

## Wo liegt was

| Ordner | Inhalt | Zustand |
|---|---|---|
| `MDT5:2/` | Skripte, 11 Praktika, Übungsblätter, 7 Zusammenfassungsblätter, Logbuch + Lernplan | geschrieben 31.07.2026, **zippen sobald die Note da ist** |
| `ED.zip` | Skript (`Ergänzung/EDy.pdf`, 296 S.), 11 Altklausuren + Lösungen, kompakte Sammlung nach Aufgabentyp (`Klausur/Kompakt/`), Formelsammlung `ED_FS/` (11 S.), drei Probeklausur-Korrekturen, Logbuch. Die 24 Vorlesungsvideos wurden gelöscht — Link + Passwort stehen in `Link_Videos.txt` im Zip. | **abgeschlossen (3,0)**, Archiv |
| `SOS/` | `Teil_A/` (Skript + FS), `Teil_B/` (Folien + FS), `Klausuren/` (drei Sätze Altklausuren) | pausiert |
| `PU/` | nur `Skript.pdf` | unbearbeitet |
| `Projektarbeit/` | eine fremde Bachelorarbeit als Referenz | unbearbeitet |
| `FS_Template/` | LaTeX-Vorlage für neue Formelsammlungen | Werkzeug |
| `Organisation/` | Stundenpläne, Modulhandbuch, Merkblatt Modulwahl | Referenz |

## Lehren aus dem SS 2026 (Grundlage für den nächsten Lernplan)

1. **Vier Prüfungen in 19 Tagen sind gegangen — aber nur knapp.** INF4/1 (13.07.), INF4/2 (20.07.),
   ED (27.07.) und MDT5/2 (31.07.). SOS fiel schon vorher raus, ED hat die Reste bekommen, wurde am
   25.07. abgesagt und am 26.07. doch wieder angesetzt. Ergebnis: **alle vier bestanden**
   (2,3 / 1,7 / 3,0 / MDT5/2 ausstehend). Die 3,0 in ED kam mit einem Vorbereitungsstand zustande,
   der in drei Probeklausuren bei ~40–48 von 100 lag — das ist kein Modell zum Nachmachen,
   sondern der Beleg, wie viel Luft in der Notenskala nach unten war.
2. **Der Engpass war nie das Verständnis, sondern die Zeit pro Modul.** In beiden ED-Probeklausuren
   waren 28 bzw. 37 von 100 Punkten *unbearbeitet* — die Fehler in den bearbeiteten Teilen waren
   Einzelschritte. Dasselbe Muster steht im INF4/1-Eintrag im Notentracker („teilweise Aufgaben
   nicht bearbeitet").
3. **Was in einem Modul nie komplett geübt wurde, steht in der Klausur bei null.** In ED war das
   Aufgabentyp A5 (nie einmal allein gerechnet → ~1/20 bzw. 6/20). Ein Lernplan muss deshalb
   *jeden* Aufgabentyp mindestens einmal vollständig abdecken, bevor irgendein Typ vertieft wird.
4. **Open-Book-Klausuren sind Navigationsprüfungen.** Punkte gehen nicht verloren, weil eine
   Formel fehlt, sondern weil sie unter Zeitdruck nicht gefunden wird. Reihenfolge in der Klausur
   (erst alle Ein-Zeilen-Teilaufgaben einsammeln) gehört mit auf das erste Blatt der Formelsammlung.
5. **Was gebaut wurde, verfällt nicht.** Formelsammlungen, sortierte Altklausur-Sammlungen und
   Logbücher sind beim zweiten Anlauf sofort wieder einsatzbereit — der Wiedereinstieg in ein
   pausiertes Modul (SOS) kostet einen Tag, nicht einen Monat.
6. **Punkt 3 wurde in MDT5/2 zum ersten Mal konsequent umgesetzt — und es hat gewirkt.** Jeder der
   12 Aufgabentypen war vor der Klausur mindestens einmal komplett gerechnet (der letzte, Typ 10,
   erst am 29.07.). Ergebnis laut Selbsteinschätzung: **keine unbearbeitete Aufgabe, Zeit sehr
   entspannt** — genau das Gegenteil des ED- und INF4/1-Musters aus Punkt 2. Diese Regel gehört
   ungekürzt in jeden künftigen Lernplan.
7. **Das Gefühl nach der Klausur ist kein guter Schätzer.** INF4/1 fühlte sich „mist" an → 2,3.
   ED fühlte sich aussichtslos an → 3,0, bestanden. Eintrag im Notentracker erst nach der
   offiziellen Note als abgeschlossen werten.

## Offene Planungsfragen für WiSe 26/27

Der Lernplan fürs nächste Semester kann erst gebaut werden, wenn Folgendes geklärt ist.
**Entlastung gegenüber dem letzten Stand: ED ist bestanden (3,0)** — die befürchtete Dreierlast
VM + ED + SOS reduziert sich auf **VM + SOS**, was nach Lenas Einschätzung machbar ist.

- [ ] Welche Module werden im WiSe 26/27 überhaupt **angeboten** (VM, SOS, INF6/1, INF6/2, PU)?
      Entscheidend ist, welche davon nur **einmal im Jahr** laufen — die haben Vorrang.
- [ ] Wann soll die **Masterarbeit** starten? Sie bestimmt, wie viele Semester für die restlichen
      Prüfungen bleiben.
- [ ] **Wahlpflicht Gruppe 2** ist noch nicht gewählt — Frist prüfen.
- [ ] Für **VM existiert kein Material im Repo**; Umfang und Prüfungsform sind unbekannt.
- [x] ~~ED-Note abwarten~~ → **3,0, bestanden im ersten Anlauf.** `ED.zip` bleibt als Archiv liegen,
      wird nicht mehr entpackt.
- [ ] **MDT5/2-Note abwarten** (Prüfung 31.07.2026). Gefühl danach gut, zeitlich entspannt —
      Selbsteinschätzung der vermuteten Fehler steht in `Notentracker.md`.
- [ ] Prüfungstermine WiSe 26/27, sobald veröffentlicht → daraus rückwärts planen, mit
      **mindestens einer freien Woche zwischen zwei Prüfungen**.
