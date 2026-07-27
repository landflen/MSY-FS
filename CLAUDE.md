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

## Studienstand (Stand 26.07.2026)

| Modul | ECTS | Status | Note |
|---|---|---|---|
| MDT5/1 | 5 | ✅ abgeschlossen (WiSe 25/26) | **1,0** |
| INF4/1 — Algorithmen & Datenstrukturen | 5 | ✅ abgeschlossen (13.07.2026) | **2,3** |
| INF4/2 — Low Level & Seminumerische Alg. | 5 | ✅ abgeschlossen (20.07.2026) | **1,7** |
| ED — Elektrodynamik | 5 | ✅ geschrieben (27.07.2026), Note ausstehend → `ED.zip` | – |
| **MDT5/2 — ML zur Anomalieerkennung** | 5 | 🔴 **Prüfung Fr 31.07.2026, 11:00** | – |
| SOS — Stochastische u. nichtlineare Systeme | 5 | ⏸ verschoben, nicht im SS 2026 geschrieben | – |
| VM — Vertiefungsgebiete der Mathematik | 5 | ⏸ offen, **kein Material im Repo** | – |
| INF6/1 | 5 | ⏸ offen, noch nicht terminiert | – |
| INF6/2 | 5 | ⏸ offen, noch nicht terminiert | – |
| PU — Personal- und Unternehmensführung | 5 | ⏸ offen (nur Skript vorhanden) | – |
| Wahlpflicht Gruppe 2 | ~5 | ⏸ offen, **WPM noch nicht gewählt** | – |
| Projektarbeit + Masterseminar | 10 | ⏸ offen | – |
| Masterarbeit + Masterseminar | 25 | ⏸ offen | – |

**Nach dem 31.07.2026 sind rund 60 ECTS offen**, davon 30 ECTS Prüfungsleistungen
(VM, SOS, ED, INF6/1, INF6/2, PU) plus Wahlpflicht, Projektarbeit und Masterarbeit.

## Wo liegt was

| Ordner | Inhalt | Zustand |
|---|---|---|
| `MDT5:2/` | Skripte, 11 Praktika, Übungsblätter, 7 Zusammenfassungsblätter, Logbuch + Lernplan | aktiv |
| `ED.zip` | Skript (`Ergänzung/EDy.pdf`, 296 S.), 11 Altklausuren + Lösungen, kompakte Sammlung nach Aufgabentyp (`Klausur/Kompakt/`), Formelsammlung `ED_FS/` (11 S.), drei Probeklausur-Korrekturen, Logbuch mit **Übergabe an den nächsten Anlauf**. Die 24 Vorlesungsvideos wurden gelöscht — Link + Passwort stehen in `Link_Videos.txt` im Zip. | archiviert 27.07.2026 |
| `SOS/` | `Teil_A/` (Skript + FS), `Teil_B/` (Folien + FS), `Klausuren/` (drei Sätze Altklausuren) | pausiert |
| `PU/` | nur `Skript.pdf` | unbearbeitet |
| `Projektarbeit/` | eine fremde Bachelorarbeit als Referenz | unbearbeitet |
| `FS_Template/` | LaTeX-Vorlage für neue Formelsammlungen | Werkzeug |
| `Organisation/` | Stundenpläne, Modulhandbuch, Merkblatt Modulwahl | Referenz |

## Lehren aus dem SS 2026 (Grundlage für den nächsten Lernplan)

1. **Drei Prüfungen in zwei Wochen gehen nicht auf.** INF4/1 (13.07.), INF4/2 (20.07.),
   ED (27.07.) und MDT5/2 (31.07.) lagen in 19 Tagen. ED hat die Reste bekommen, wurde am
   25.07. abgesagt und am 26.07. doch wieder angesetzt; SOS fiel schon vorher raus. Ergebnis:
   von vier geplanten Prüfungen werden drei geschrieben — ED mit einem Vorbereitungsstand,
   der in drei Probeklausuren bei ~40–48 von 100 lag.
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
   Logbücher sind beim zweiten Anlauf sofort wieder einsatzbereit — der Wiedereinstieg in ED
   kostet einen Tag, nicht einen Monat.

## Offene Planungsfragen für WiSe 26/27

Der Lernplan fürs nächste Semester kann erst gebaut werden, wenn Folgendes geklärt ist —
**VM, ED und SOS zusammen in einem Semester ist nach Lenas eigener Einschätzung nicht machbar,
mindestens eines muss weiter geschoben werden:**

- [ ] Welche Module werden im WiSe 26/27 überhaupt **angeboten** (VM, SOS, ED, INF6/1, INF6/2, PU)?
      Entscheidend ist, welche davon nur **einmal im Jahr** laufen — die haben Vorrang.
- [ ] Wann soll die **Masterarbeit** starten? Sie bestimmt, wie viele Semester für die restlichen
      Prüfungen bleiben.
- [ ] **Wahlpflicht Gruppe 2** ist noch nicht gewählt — Frist prüfen.
- [ ] Für **VM existiert kein Material im Repo**; Umfang und Prüfungsform sind unbekannt.
- [ ] **ED-Note abwarten.** Fällt sie durch, `ED.zip` entpacken — der Statuskasten in
      `ED/CLAUDE.md` enthält die Übergabe an den nächsten Anlauf; Videos ggf. über den
      faubox-Link in `Link_Videos.txt` neu laden.
- [ ] Prüfungstermine WiSe 26/27, sobald veröffentlicht → daraus rückwärts planen, mit
      **mindestens einer freien Woche zwischen zwei Prüfungen**.
