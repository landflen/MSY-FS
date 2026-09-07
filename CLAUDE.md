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

## Studienstand (Stand 03.08.2026)

**Das SS 2026 ist durch — alle vier angetretenen Prüfungen bestanden, alle Noten liegen vor
(2,3 / 1,7 / 3,0 / 1,3).**

| Modul | ECTS | Status | Note |
|---|---|---|---|
| MDT5/1 | 5 | ✅ abgeschlossen (WiSe 25/26) | **1,0** |
| INF4/1 — Algorithmen & Datenstrukturen | 5 | ✅ abgeschlossen (13.07.2026) | **2,3** |
| INF4/2 — Low Level & Seminumerische Alg. | 5 | ✅ abgeschlossen (20.07.2026) | **1,7** |
| ED — Elektrodynamik | 5 | ✅ abgeschlossen (27.07.2026) → `ED.zip` | **3,0** |
| MDT5/2 — ML zur Anomalieerkennung | 5 | ✅ abgeschlossen (31.07.2026) | **1,3** |
| SOS — Stochastische u. nichtlineare Systeme | 5 | ⏸ Klausur im WiSe 26/27 geplant, **keine LV** → Selbstlernzeit | – |
| VM — Vertiefungsgebiete der Mathematik | 5 | ⏸ WiSe 26/27 als `VM-NZ` (Bolik), Skript+Übungen fehlen | – |
| INF6/1 — Prototyping im SW Engineering | 5 | ⏸ WiSe 26/27 (Jakobi), Gruppe 2.2 | – |
| INF6/2 — Usability Engineering | 5 | ⏸ WiSe 26/27 (Harms), Gruppe 2.2 | – |
| PU — Personal- und Unternehmensführung | 5 | ⏸ WiSe 26/27 als `PU-NZ`, Gruppe 2.1 (nur Skript vorhanden) | – |
| Wahlpflicht Gruppe 2 | ~5 | ⏸ offen, **WPM noch nicht gewählt** | – |
| Projektarbeit + Masterseminar | 10 | ⏸ offen | – |
| Masterarbeit + Masterseminar | 25 | ⏸ offen | – |

**Es sind rund 60 ECTS offen**, davon 25 ECTS Prüfungsleistungen (VM, SOS, INF6/1, INF6/2, PU)
plus Wahlpflicht Gruppe 2, Projektarbeit und Masterarbeit. **ED ist erledigt und fällt aus der
WiSe-26/27-Planung heraus** — das entlastet das nächste Semester spürbar.

## Wo liegt was

| Ordner | Inhalt | Zustand |
|---|---|---|
| `MDT5:2/` | Skripte, 11 Praktika, Übungsblätter, 7 Zusammenfassungsblätter, Logbuch + Lernplan | **abgeschlossen (1,3)** — bereit zum Zippen |
| `ED.zip` | Skript (`Ergänzung/EDy.pdf`, 296 S.), 11 Altklausuren + Lösungen, kompakte Sammlung nach Aufgabentyp (`Klausur/Kompakt/`), Formelsammlung `ED_FS/` (11 S.), drei Probeklausur-Korrekturen, Logbuch. Die 24 Vorlesungsvideos wurden gelöscht — Link + Passwort stehen in `Link_Videos.txt` im Zip. | **abgeschlossen (3,0)**, Archiv |
| `SOS/` | `Teil_A/` (Skript + FS), `Teil_B/` (Folien + FS), `Klausuren/` (drei Sätze Altklausuren), `SOS_Klausurinfos_Kommilitonen.md` | pausiert |
| `VM/` | **Beide Skripte von Bolik** (`M_SY_Dgl_Skript.pdf` 81 S., `M_SY_Stoch_Skript.pdf` 87 S., je mit Übungsaufgaben → 71 Stück, ohne Lösungen), **Probeklausur + Musterlösung**, Klausur-Tabellenblätter (`Tabellen_VM.pdf`), `Partialbruchzerlegung.pdf`, **Original-Klausur SoSe 2026 mit Musterlösung** (`Klausur_SoSe2026/`, 6 Fotos) + Auswertung `VM_Klausur_SoSe2026.md`, Notizen aus Boliks Klausurvorbereitung (`Fragestunde_Notizen/`), Notenspiegel, drei fremde Formelsammlungen samt Stoffinventar. Inventar: **`VM_Lernmaterial.md`** | **vollständig** seit 07.09.2026, unbearbeitet |
| `PU/` | `Skript.pdf`, zwei Zusammenfassungen (u. a. die vielgelobte von WiSe 22/23) und `PU_Altklausuren.pdf` | unbearbeitet |
| `Projektarbeit/` | eine fremde Bachelorarbeit als Referenz | unbearbeitet |
| `FS_Template/` | LaTeX-Vorlage für neue Formelsammlungen | Werkzeug |
| `Organisation/` | Stundenpläne, Modulhandbuch, Merkblatt Modulwahl + **`Wochenplan_WiSe26_27.md`** (ausgewerteter Stundenplan, Gruppenwahl, Modulfakten) | Referenz |

## Lehren aus dem SS 2026 (Grundlage für den nächsten Lernplan)

1. **Vier Prüfungen in 19 Tagen sind gegangen — aber nur knapp.** INF4/1 (13.07.), INF4/2 (20.07.),
   ED (27.07.) und MDT5/2 (31.07.). SOS fiel schon vorher raus, ED hat die Reste bekommen, wurde am
   25.07. abgesagt und am 26.07. doch wieder angesetzt. Ergebnis: **alle vier bestanden**
   (2,3 / 1,7 / 3,0 / 1,3). Die 3,0 in ED kam mit einem Vorbereitungsstand zustande,
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
   erst am 29.07.). Ergebnis: **keine unbearbeitete Aufgabe, Zeit sehr entspannt** — genau das
   Gegenteil des ED- und INF4/1-Musters aus Punkt 2 — und mit **1,3 die beste Note des Semesters**.
   Diese Regel gehört ungekürzt in jeden künftigen Lernplan.
7. **Das Gefühl nach der Klausur ist kein guter Schätzer — außer es stützt sich auf nachgerechnete
   Einzelfehler.** INF4/1 fühlte sich „mist" an → 2,3. ED fühlte sich aussichtslos an → 3,0,
   bestanden. MDT5/2 dagegen wurde nicht nach Gesamteindruck geschätzt, sondern über eine Liste
   konkret vermuteter Fehler (inkl. Nachprüfung der OCSVM-Aufgabe) — und diese Prognose („eher 1,3")
   traf **exakt**. Also: Fehlerliste statt Bauchgefühl, aber im Notentracker trotzdem erst nach der
   offiziellen Note als abgeschlossen werten.

## Offene Planungsfragen für WiSe 26/27

**Das WiSe-26/27-Angebot ist ausgewertet** (03.09.2026, `Organisation/MSY2.pdf`, Stand 15.06.2026)
— Ergebnis, Zeiten, Gruppenwahl und Begründung stehen in **`Organisation/Wochenplan_WiSe26_27.md`**.
Kurzfassung: **VM-NZ, PU-NZ, INF6/1, INF6/2 und PRS laufen im Winter; SOS hat keine Lehrveranstaltung**
(reines Sommermodul), die **Klausur ist aber schreibbar** → SOS ist reine Selbstlernzeit.
Gewählt sind das letzte Vertiefungsmodul **mINF6** und die Gruppenkombination
**INF6 2.2 · PU 2.1 · PRS 3.1**, die den Donnerstag komplett frei hält (12 Arbeitsstunden:
Do 8 h + Mo 4 h).

- [x] ~~Welche Module werden im WiSe 26/27 **angeboten**?~~ → geklärt, siehe
      `Organisation/Wochenplan_WiSe26_27.md`. **Nur einmal im Jahr und damit mit Vorrang:**
      INF6/1 + INF6/2 (Wintermodule) und das **projektbegleitende Seminar PRS — das gibt es
      ausschließlich im Wintersemester** (im Sommer läuft nur die Projektarbeit ohne Seminar).
      VM, ED und PU laufen im Winter als **Nachzügler-Kurse** (`-NZ`), regulär im Sommer.
- [ ] **SOS-Klausurtermin im WiSe 26/27 bestätigen lassen** — keine Lehrveranstaltung, aber Prüfung.
      Vorbereitung läuft komplett über das vorhandene Material in `SOS/`.
- [ ] Wann soll die **Masterarbeit** starten? Sie bestimmt, wie viele Semester für die restlichen
      Prüfungen bleiben.
- [ ] **Wahlpflicht Gruppe 2** ist noch nicht gewählt — Frist prüfen. Gebraucht werden **2 WPM
      à 2 SWS**; das Angebot läuft nicht übers Modulhandbuch, sondern über virtuohm
      (`oes_web.show_fachuebersicht?in_lv_art=FWPF&in_org_id=269&in_abg_id=1`). **Kandidat:**
      `1005:WF` bei Bolik, Mi 15:45–17:15 in WE.209 — direkt hinter VM-NZ/B, selber Raum, selber
      Dozent, kein zusätzlicher Anfahrtstag.
- [ ] **VM ist die härteste Klausur des Studiengangs** — SoSe 2026: Schnitt 3,79, **21 von 62
      durchgefallen (33,9 %), keine einzige 1,0**; kein Überhang, keine 4,0-Bremse, **keine
      Folgefehler-Punkte**; Aufwandsanker ≈ 120 h. Als **eigenständiger Prüfungsblock**
      einplanen, nicht als Beifang. Seit 01.08.2026 liegt die **Original-Klausur SoSe 2026 mit
      Musterlösung** im Repo (`VM/Klausur_SoSe2026/`, ausgewertet in `VM/VM_Klausur_SoSe2026.md`):
      6 Aufgaben, 90 Punkte, Bestehensgrenze 32, exakt hälftig Analysis/LinAlg und Stochastik,
      Hilfsmittel = 10 Seiten eigene Unterlagen + Formelsammlung.
      **Seit 07.09.2026 sind auch Skript und Übungsaufgaben da** (Moodle
      `e-learn.inventiones.de/course/view.php?id=29`): beide Skripte, 71 Übungsaufgaben
      (ohne Lösungen), Probeklausur **mit** Musterlösung und die Klausur-Tabellenblätter
      → Inventar und Aufgabentypen in `VM/VM_Lernmaterial.md`. Damit ist VM vollständig lernbar.
- [x] ~~ED-Note abwarten~~ → **3,0, bestanden im ersten Anlauf.** `ED.zip` bleibt als Archiv liegen,
      wird nicht mehr entpackt.
- [x] ~~MDT5/2-Note abwarten~~ → **1,3** (03.08.2026). Vertiefungsblock damit bei **1,58** über
      4 von 6 Modulen; offen sind nur noch INF6/1 und INF6/2. Ordner `MDT5:2/` zippen.
- [ ] **Projektarbeit (5a) im WiSe 26/27 starten?** Das projektbegleitende Seminar (5b, im Plan
      `PRS`) läuft **nur im Winter** — wer es auslässt, wartet ein Jahr. Thema/Betreuung klären.
- [ ] Prüfungstermine WiSe 26/27, sobald veröffentlicht → daraus rückwärts planen, mit
      **mindestens einer freien Woche zwischen zwei Prüfungen**.
