# Wochenplan WiSe 26/27 — Auswertung des Stundenplans

**Quellen:** `Organisation/MSY2.pdf` (offizieller MSY-Stundenplan, Kopf „Winter26/27", Stand 15.06.2026),
`Organisation/efi_1464_VO_MSY_Modulhandbuch_public.pdf` (Ausgabe Q), `Organisation/efi_1474_VO_MSY_Merkblatt_Modulwahl_public.pdf`.
Erstellt 03.09.2026.

---

## 1. Notation im Stundenplan (einmal lernen, gilt für alle Semester)

| Kürzel | Bedeutung |
|---|---|
| `SU` | **Vorlesung** (seminaristischer Unterricht) |
| `Ü` | Übung |
| `Pr` | **Praktikum** |
| `S` | Seminar |
| `NZ` | **Nachzügler-Kurs** — Modul wird außerhalb seines regulären Semesters nochmal angeboten |
| `/A`, `/B`, `/C`, `/D` | **Stoffteile** eines Moduls — alle nötig, keine Auswahl |
| `:2.1`, `:2.2`, `:3.1` … | **Parallelgruppen.** Erste Zahl = SWS, zweite = Gruppennummer |
| `G` / `U` | gerade / ungerade KW (14-tägig), KW gezählt ab der KW des 1.10. |
| `G1/G2`, `U1/U2` | alle 4 Wochen |
| `SH1` / `SH2` | erste / zweite Semesterhälfte |

> ⚠️ **Gruppenregel:** Wer sich für Gruppe `2.1` entscheidet, muss **alle** Veranstaltungen dieser
> Gruppe besuchen. Die Gruppennummer zieht sich durch alle Teile eines Moduls — man kann nicht
> Teil A in Gruppe 1 und Teil B in Gruppe 2 belegen.

---

## 2. Angebot WiSe 26/27 — was für Lena relevant ist

| Modul | Status | Im Winter? |
|---|---|---|
| **VM** — Vertiefungsgebiete der Mathematik | offen, Pflicht | ✅ als `VM-NZ`, Bolik |
| **SOS** — Stochastische u. nichtlineare Systeme | offen, Pflicht | ❌ **keine LV** (Sommermodul) — **Klausur trotzdem möglich → reine Selbstlernzeit** |
| **INF6/1 + INF6/2** — Human Centered SW Engineering | offen, letztes Vertiefungsmodul Gruppe 1 | ✅ regulär (Wintermodule) |
| **PU** — Personal- und Unternehmensführung | offen, Pflicht | ✅ als `PU-NZ` |
| **PRS** — projektbegleitendes Seminar (Modul 5b) | offen | ✅ — **und nur im Winter!** (Modulhandbuch: Projektarbeit+Seminar im WiSe, im SoSe nur Projektarbeit) |
| **ED** | ✅ bestanden 3,0 | (läuft als `ED-NZ`, irrelevant) |

**Vertiefungsblock Gruppe 1:** 3 Module à 10 ECTS. Erledigt: `mINF4` (INF4/1+4/2) und `mMDT5`
(MDT5/1+5/2). Offen ist **genau ein** Modul → gewählt: **`mINF6`** (Prototyping im Software
Engineering + Usability Engineering). Begründung siehe Abschnitt 6.

---

## 3. Alle relevanten Termine

### Fix, keine Wahl

| Veranstaltung | Tag | Zeit | Dozent | Raum |
|---|---|---|---|---|
| `VM-NZ/A:SU` | Di | **11:30–13:00** | Bolik | WE.209 |
| `VM-NZ/B:SU` | Mi | **14:00–15:30** | Bolik | WE.209 |
| `mINF6/1:SU` | Di | **15:45–17:15** | Jakobi | WE.102 |
| `mINF6/2:SU` | Fr | **09:45–11:15** | Harms | KH.108 |

VM-NZ/A und /B sind die zwei Stoffhälften (Analysis/LinAlg bzw. Stochastik), **beide nötig**.

### Wahlgruppen

| Wahl | Gruppe 1 | Gruppe 2 | Gruppe 3 |
|---|---|---|---|
| **INF6/1 Praktikum** | `Pr:2.1` Di 17:30–19:00, WE.102 | `Pr:2.2` **Di 14:00–15:30**, WE.102 | — |
| **INF6/2 Praktikum** | `Pr:2.1` Do 14:00–15:30, WG.212 | `Pr:2.2` **Fr 11:30–13:00**, WG.212 | — |
| **PU-NZ** (beide Termine der Gruppe!) | `2.1` **Mi 08:00–09:30** WE.209 + **Sa/Block**, Knicker | `2.2` Do 15:45–17:15 KA.204 + **Sa/Block**, Lehner | — |
| **PRS Seminar** | `3.1` **Mo 08:00–09:30**, Wieczorek, WE.209 | `3.2` Mo 09:45–11:15, Scheuerpflug, WE.209 | `3.3` Sa/Block, Scheuerpflug |

### Sonstiges

- **`1005:WF` — Bolik, Mi 15:45–17:15, WE.209.** Einziges Wahlfach im MSY-Plan, liegt direkt hinter
  VM-NZ/B im selben Raum beim selben Dozenten → **heißer Kandidat für WPM Gruppe 2** (2 × 2 SWS nötig,
  Angebot sonst über virtuohm: `oes_web.show_fachuebersicht?in_lv_art=FWPF&in_org_id=269&in_abg_id=1`).
- **`mINF5` (Digitale Signalverarbeitung)** als Alternativ-Vertiefung: SU/A Mo 14:00–15:30 (Kornagel),
  SU/B Di 17:30–19:00 (Popp-Nowak), Pr/A Fr 09:45–13:00, Pr/B Fr 14:00–17:15 (beide 14-tägig; Gruppe
  2.1 = gerade KW, 2.2 = ungerade KW → durch die Gruppenbindung landen beide Praktika **am selben
  Freitag**). Zerlegt Montag *und* Freitag → für einen 12-Stunden-Job schlechter als INF6.

---

## 4. Gewählte Kombination

**INF6 Gruppe 2.2 · PU Gruppe 2.1 · PRS 3.1**

| | Mo | Di | Mi | Do | Fr |
|---|---|---|---|---|---|
| **08:00–09:30** | PRS 3.1 (S) | | PU 2.1 (SU) | | |
| **09:45–11:15** | | | | | INF6/2 SU |
| **11:30–13:00** | | VM/A SU | | | INF6/2 Pr |
| **14:00–15:30** | | INF6/1 Pr | VM/B SU | | |
| **15:45–17:15** | | INF6/1 SU | *(1005:WF)* | | |
| **17:30–19:00** | | | | | |

+ PU-Block an einzelnen Samstagen. **≈ 12 h Präsenz/Woche**, nichts nach 17:15, vier Anwesenheitstage.

**Warum so:**
- `INF6/1 Pr:2.2` (Di 14:00) statt 17:30 → Dienstag wird ein Block 11:30–17:15 statt bis 19:00.
- `INF6/2 Pr:2.2` (Fr 11:30) statt Do 14:00 → **hält den Donnerstag komplett frei**; Freitag wird ein
  Block 09:45–13:00. Nebeneffekt: durchgängig Gruppe 2.2 — falls Jakobi und Harms dieselbe
  Gruppeneinteilung benutzen, ist die Kombination auch dann zulässig.
- `PU 2.1` (Mi + Sa) statt 2.2 → Gruppe 2.2 legt einen einzelnen 90-Minuten-Termin auf Do 15:45 und
  zerstört damit den freien Donnerstag. Der Mittwochmorgen kostet nichts, weil wegen VM/B ohnehin
  Anwesenheitstag.
- `PRS 3.1` (Mo 08:00) statt 3.2 → Montag ab 09:30 frei statt erst ab 11:15. `3.3` würde mit dem
  PU-Samstagsblock kollidieren.

### Der Wochenrhythmus mit allem drin (Stand 03.09.2026)

**Grundentscheidungen:** VM läuft im **Selbststudium** (die Vorlesung taugt laut Berichten im
Kommiliton:innen-Chat wenig, `VM/VM_Klausurinfos_Kommilitonen.md`), die beiden VM-Termine
Di 11:30 und Mi 14:00 entfallen. **Mittwoch und Donnerstag sind Arbeitstage**, **Montag ist
Projekttag**, **Freitag ist Mathe-Tag**.

| Zeit | Mo | Di | Mi | Do | Fr |
|---|---|---|---|---|---|
| **08:00–09:30** | PRS 3.1 (S) | | PU 2.1 (SU) | | |
| **09:45–11:15** | Projekt | **VM** 1,5 h | INF6/1-Nacharb. 45 min | | INF6/2 SU |
| **11:30–13:00** | Projekt | **SOS** 1 h | Arbeit | | INF6/2 Pr |
| **14:00–15:30** | **SOS** 1 h | INF6/1 Pr | Arbeit | | INF6/2-Nacharb. 1 h |
| **15:45–17:15** | frei | INF6/1 SU | *(1005:WF)* | | **VM** 1,5 h |
| **ganztägig** | | | **Arbeit 4 h** | **Arbeit 8 h** | |

**Wochenbudget**

| Posten | Stunden | Wo |
|---|---|---|
| Anwesenheit LV | 9 (10,5 mit WF) | Mo/Di/Mi/Fr |
| Arbeit | **12** | Mi 4 h + Do 8 h |
| Projektarbeit | 3 | Mo 09:45–12:45 |
| VM (Selbststudium) | **3** | Di 09:45–11:15 + Fr 15:45–17:15 |
| SOS (Selbststudium) | **2** | Mo 14:00–15:00 + Di 11:30–12:30 |
| Vor-/Nachbereitung INF6/1 + INF6/2 | ~1,75 | Mi 09:45 (frisch vom Vortag) + Fr direkt im Anschluss |
| PU | 0 | bewusst keine Nacharbeit |
| **Summe** | **≈ 31 h** (33 mit WF) | |

Frei: Mo ab 15:00 · Di ab 17:15 · Mi ab 15:00 · Do ab 17:00 · Fr ab 17:15 · **das ganze Wochenende**
(außer den PU-Blockterminen).

**Warum diese Verteilung**
- **Mittwoch statt Freitag als zweiter Arbeitstag:** Mi hat nach PU (08:00–09:30) nichts mehr —
  ein ganzer Tag mit nur 90 min Uni ist als Arbeitstag effizienter denn als Lerntag. Freitag ist
  durch INF6/2 (09:45–13:00) ohnehin ein Uni-Tag; dort noch arbeiten zu gehen hieße dritter
  Ortswechsel-Tag. Achtung: mit `1005:WF` (Mi 15:45–17:15) ist der Mittwoch-Arbeitsblock auf
  09:45–15:00 begrenzt.
- **VM auf Di-Vormittag und Fr-Nachmittag:** zwei feste Termine statt „irgendwann", an den Rändern
  von Uni-Tagen (kein zusätzlicher Weg), und mit maximalem Abstand zueinander — VM verträgt
  Wiederholungsabstand besser als einen Block.
- **SOS auf Mo und Di à 1 h:** SOS ist reine Wiederholung auf fertigem Material (Formelsammlungen,
  Typ-Ranking, Altklausuren liegen in `SOS/`) — kurze, häufige Einheiten reichen dafür.
- **Nachbereitung direkt an die Veranstaltung gekoppelt:** INF6/1 am Mittwochmorgen (Stoff einen Tag
  alt), INF6/2 am Freitag unmittelbar danach. PU bekommt bewusst nichts.

> ⚠️ **Rechnerischer Vorbehalt:** 3 h VM × ~15 Semesterwochen = **45 h**. Der Aufwandsanker aus dem
> Chat liegt bei **≈ 120 h**. Die fehlenden ~75 h müssen in der **Prüfungsphase** entstehen — also
> beim Bau des Klausur-Lernplans einen eigenen VM-Block von 2–3 Wochen einplanen. Dasselbe gilt
> abgeschwächt für SOS (2 h × 15 = 30 h, aber auf fertigem Material). Während des Semesters ist
> das Ziel dieser Blöcke **nicht Klausurreife, sondern Stoff-Mitlaufen** — damit die Prüfungsphase
> mit Üben starten kann statt mit Erstkontakt.

---

## 5. Modulfakten für den Lernplan

| Modul | ECTS | SWS | Prüfung | Verantwortung | Voraussetzungen laut MHB |
|---|---|---|---|---|---|
| VM | 5 | 4 (3 SU + 1 Ü) | schriftlich **90 min** | Steinbach / Bolik | Diff.-/Integralrechnung, LinAlg + EW-Problem, gew. DGL |
| SOS | 5 | 4 (3 SU + 1 Ü) | schriftlich **90 min** | — | Fourier/Laplace, Übertragungsfunktion, Stabilität, Zustandsraum |
| INF6/1 Prototyping | 5 | 4 (2 SU + 2 Pr) | schriftlich **90 min** | Jakobi | UML, Design Pattern; hilfreich: SW-Projekterfahrung |
| INF6/2 Usability | 5 | 4 (2 SU + 2 Pr) | schriftlich **90 min** | Harms | UML, Design Pattern; hilfreich: Web-App-Entwicklung |
| PU | 5 | 4 (2 SU + 2 S) | schriftlich **90 min** | Wagner | keine |
| Projekt 5a+5b | 8+2 | 8 (6 PA + 2 S) | **Leistungsnachweis** (Seminar) | Niebler | Kenntnisse aus den themenbezogenen Modulen |
| WPM Gruppe 2 | ~5 | 4 (2 WPM à 2 SWS) | **Leistungsnachweis** | — | — |

Workload je 5-ECTS-Modul = 150 h; INF6/1 und INF6/2 jeweils mit nur **20 h Prüfungsvorbereitung**
angesetzt (der Rest ist Praktikum und Nachbereitung während des Semesters).

**Klausurlast WiSe 26/27:** VM, SOS, INF6/1, INF6/2, PU = **5 Klausuren**. Im SS 2026 waren
ebenfalls 5 angesetzt (geschrieben: 4). Also bekanntes Terrain — der Engpass ist laut Lehre 1/2 im
Root-`CLAUDE.md` nicht das Verständnis, sondern die Zeit pro Modul.

---

## 6. Warum mINF6 und nicht ein anderes Vertiefungsmodul

- **Profil-Match:** beste Noten in Software/Informatik (MDT5/1 1,0 · MDT5/2 1,3 · INF4/2 1,7 ·
  INF4/1 2,3), schwächste in Feldtheorie (ED 3,0). INF6 ist reines Software Engineering — keine
  Feldtheorie, keine schwere Mathematik.
- **Konkurriert nicht mit VM** um dieselbe Denkkapazität im selben Semester (anders als INF5 oder MDT4).
- **Zwei getrennte 5-ECTS-Klausuren** statt eines 10-ECTS-Blocks — im Notfall auf zwei Semester
  trennbar.
- **Praktikumslastig** → ein Teil der Leistung entsteht während des Semesters, nicht in der
  Prüfungswoche.

Nicht gewählt: **INF5** (Mathe-Konkurrenz zu VM, zerlegt Mo+Fr), **MDT4** (Physik + riesiger Stoff,
120-min-Klausur), **KOM5** (HF = ED-Schwachpunkt), MEC/ENT/AUT/ESY/PHO/OQT (hardware-/physiknah,
kein Vormaterial).

---

## 7. Offene Punkte

- [ ] Sind die Praktikumsgruppen von INF6/1 (Jakobi) und INF6/2 (Harms) **gekoppelt**? Der Plan sagt
      es nicht. Die Wahl 2.2/2.2 ist in beiden Fällen zulässig.
- [ ] PU-Samstagstermine (`n.V.`) erfragen — sie sind das einzige Wochenendrisiko.
- [ ] `1005:WF` (Bolik): Inhalt und Prüfungsform klären → taugt es als WPM Gruppe 2? Zweites WPM
      Gruppe 2 über virtuohm suchen, **Wahlfrist prüfen**.
- [ ] SOS-Klausurtermin im WiSe 26/27 bestätigen lassen (keine LV, aber Prüfung).
- [ ] Prüfungstermine WiSe 26/27 abwarten → Lernplan rückwärts bauen, mit mindestens einer freien
      Woche zwischen zwei Prüfungen.
- [ ] Projektarbeit: Start im WiSe 26/27 zusammen mit PRS? Das Seminar (5b) gibt es **nur im Winter**
      — wer es verpasst, wartet ein Jahr.
