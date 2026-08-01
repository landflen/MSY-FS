# SOS — was Kommiliton:innen berichten (Klausur SoSe 2026)

> **Quelle:** WhatsApp-Gruppe „efi Master", Export vom 10.–30.07.2026
> (`~/Downloads/efi Master/chat.md`). Alles hier ist **Hörensagen und
> Gedächtnisprotokoll**, keine offizielle Quelle. Zuverlässigkeit pro Punkt markiert:
> ✅ mehrfach bestätigt · ⚠️ einmalig genannt · ❓ Vermutung.
> **Die Prüfung fand am 22.07.2026 statt** — du bist nicht angetreten, das ist also der
> Termin, den du im WiSe 26/27 oder SoSe 27 nachholst.
>
> Ergänzt die eigenen Unterlagen in `Teil_A/`, `Teil_B/` und `Klausuren/`.
> Namen von Studierenden sind bewusst weggelassen.

## Prüfungsmodus — die harten Fakten

| Punkt | Info | Zuverl. |
|---|---|---|
| Zwei Teile | **Teil A = Prof. Wagner** (nichtlineare Systeme) · **Teil B = Prof. Siegl** (stochastische Systeme) | ✅ |
| Bestehen | **Punkte beider Teile werden addiert, dann erst die Note gebildet.** Es gibt **keine Mindestpunktzahl je Teil** — man kann rechnerisch allein über Teil A bestehen. | ✅ (dreimal bestätigt) |
| Überhang | **Teil Siegl: ca. 20 % Überhang.** Bei Wagner variiert es. | ⚠️ |
| Hilfsmittel | Papula erlaubt | ✅ |
| Korrekturdauer | Klausur 22.07. → Noten 27.07., Einsicht 29.07. | ✅ |
| Notenlage | siehe Tabelle unten — SoSe 2026 wurde das Niveau spürbar angehoben | ✅ Notenspiegel |

### Notenspiegel im Vergleich (`Notenspiegel/`)

| | SoSe 2025 | SoSe 2026 |
|---|---|---|
| Teilnehmende | 87 | 60 |
| **Schnitt** | **2,31** | **2,85** |
| Note 1,0 | **21 (24 %)** | 5 (8 %) |
| Note 5,0 | 3 (3,4 %) | 5 (8,3 %) |

Die 21 Einser im SoSe 2025 waren in der Gruppe Gesprächsthema („Überhang working overtime");
im SoSe 2026 wurden sie sichtbar „rausgebremst". **Trotzdem:** selbst im schlechteren Jahr
fallen nur 8 % durch und der Schnitt liegt bei 2,85 — SOS ist ein völlig anderes Kaliber als
VM (dort 33,9 % Fünfen bei Schnitt 3,79).

**Wichtigste Konsequenz aus dem Modus:** Der Überhang bei Siegl bedeutet, dass du dort mehr
Punkte holen kannst, als für 100 % nötig wären — es lohnt sich also, den Siegl-Teil
*vollständig* zu bearbeiten, statt Zeit in die letzten Prozente bei Wagner zu stecken.

## ⏱ Der zentrale Befund: Zeitnot, nicht Verständnis

Das dominierende Thema direkt nach der Klausur war die Zeit — nicht die Schwierigkeit:

- *„SIEGL TEIL ICH HATTE KEINE ZEIT MEHR"* ✅
- *„der Wagner seine Aufgaben haben sich wie 30 Stück angefühlt"* ✅
- Nur eine Handvoll Leute hat **alle drei Siegl-Aufgaben** geschafft; viele haben leere
  Aufgaben und leere Seiten abgegeben ✅
- Später in der Gruppe: *„der hat doch nur leere Seiten bis auf 20 Leute, die alle drei
  Aufgaben geschafft haben"* ✅

**Das ist exakt dein eigenes Muster aus INF4/1 und ED** (Lehre Nr. 2 im Root-`CLAUDE.md`:
der Engpass ist die Zeit pro Aufgabe, nicht das Verständnis) — hier unabhängig bestätigt und
sogar der Regelfall im ganzen Kurs. Für SOS heißt das:

1. **Reihenfolge vorher festlegen und aufs erste Blatt schreiben.** Bei Wagner gibt es
   3 Aufgaben mit je 5–6 Teilaufgaben; die kurzen Teilaufgaben zuerst einsammeln.
2. **Teil Siegl nicht hinten anstellen.** Wer ihn zuletzt gerechnet hat, ist reihenweise
   nicht fertig geworden — und dort liegt der Überhang.
3. Vollständigkeit schlägt Perfektion: die Leute mit leeren Aufgaben haben nicht an der
   Schwierigkeit verloren.

## Themen — Klausur SoSe 2026

### Teil B (Siegl, stochastisch)

Drei Aufgaben: ✅
1. **Korrelationsfunktion**
2. **Wahrscheinlichkeitsdichte** — eine Teilaufgabe allein **10 Punkte** ⚠️
3. **Kalman-Filter mit Innovationsfunktion**

Themenüberblick, den mehrere unabhängig voneinander bestätigt haben — *mehr gibt es
thematisch nicht*: ✅
- Kalman-Filter
- Wahrscheinlichkeitsdichtefunktion
- Erwartungswert und Varianz
- Faltung
- Korrelationsfunktionen

> Deine Formelsammlung `Teil_B/SOS_B_FS/` deckt genau diese Achse schon ab
> (Zufallsprozesse, diskrete Zufallsprozesse, Signal Estimation/Kalman inkl.
> Innovation und a-priori/a-posteriori-Abgriff). **Die Innovationsfunktion war in der
> Klausur explizit dran** — der Abschnitt ist also richtig gewichtet.

**Korrelation ist das gefürchtetste Thema** — mehrfach als „macht mich komplett kaputt",
„ich denke, ich hab's verstanden, dann muss ich wieder raten". ✅ Wenn du irgendwo mehr
Übungsaufgaben brauchst, dann dort.

### Teil A (Wagner, nichtlinear)

Drei Aufgaben mit je 5–6 Teilaufgaben: ✅
1. **Ortskurve** — mit Zweipunktschalter („Totschalter") **und** in weiteren Teilaufgaben
   mit **Hysterese**-Kennlinie ✅
2. **Linearisierung einer DGL**
3. **Stabilitätsuntersuchungen**

Themenüberblick für Teil A aus der Vorbereitung: ✅
- Stabilitätsanalyse nach **Lyapunov**
- **Ruhelagen und Betriebspunkte** bestimmen, **Linearisierung**
- **Zustandsraumdarstellung** und Stabilitätsuntersuchung darin
- **Harmonische Balance** mit Grenzzyklen

> Deckt sich mit deiner FS `Teil_A/SOS_A_FS/`
> (`01_signale_routh`, `02_zustandsraum_lyapunov`, `04_harmonische_balance`).
> **Die Zwei-Ortskurven-Methode mit den verschiedenen Kennlinien-Typen — Zweipunktschalter,
> Hysterese, Totzone — war der Schwerpunkt der Ortskurven-Aufgabe.** Genau dafür hast du am
> 01.07. die fünf TikZ-Grafiken in `04_harmonische_balance.tex` gebaut, inklusive
> „Lage der neg.-inv. Beschreibungsfunktion je NL-Typ" und dem Sonderfall mehrerer
> Schnittpunkte. Das ist die richtige Investition gewesen.

## Was NICHT drankam (Achtung: galt für SoSe 2026)

- **Wavelet-Transformation** — ausdrücklich ausgeschlossen ✅
- **Kreiskriterium** — ausdrücklich ausgeschlossen ✅

⚠️ **Vor dem eigenen Antritt neu erfragen.** Beide Ausschlüsse waren eine Ansage für *dieses*
Semester, keine Dauerregel. Dein FS-Teil `03_kreiskriterium.tex` bleibt also drin, bis das
Gegenteil bestätigt ist.

**Gegenbeispiel, warum man Ausschlüsse nicht raten sollte:** Das **Routh-Schema** galt in der
Gruppe als „kommt nie in Altklausuren dran" — es kam aber in SoSe 2024 in Aufgabe 3.3 vor und
ist mehreren Leuten in den *neueren* Altklausuren begegnet. ✅

## Altklausuren — welche taugen

- **Die ganz alten sind nur bedingt repräsentativ.** Empfehlung aus der Gruppe: *„das, was in
  den letzten paar Klausuren drin ist"*. Bei Wagner sind Altklausuren teils bis 1997
  hochgeladen, ausdrücklich nur zur Anschauung. ✅
- **SoSe 2023 und SoSe 2024 gelten als deutlich machbarer** als die Jahrgänge davor —
  mehrfach bestätigt. Das sind die realistischsten Proben. ✅
- **Siegls eigener Tipp:** die alten **Stochastik-Aufgaben von Wagner** sind sehr gut, um die
  Sachen zu *verstehen* (nicht unbedingt als Klausurabbild). ✅
- ⚠️ **Die aktuellen Probeklausuren enthalten Fehler.** Siegl hat sich dafür entschuldigt und
  von „Copy-Paste-Fehlern" gesprochen; er hat einmal nachgebessert, **es sind noch welche
  drin**. Typisch: Zahlendreher oder falsche Variablen **im Lösungsweg**, während das
  Endergebnis stimmt. ✅
  → Beim Nachrechnen einer Probeklausur nicht an sich selbst zweifeln, wenn der Weg nicht
  aufgeht: erst gegen das Endergebnis prüfen.
- Wenn keine gute Formelsammlung zur Hand ist, war der meistgenannte Rat: *Klausuren mit
  Lösungen ausdrucken, die Vorgehensschritte pro Aufgabentyp herausschreiben, dazu Papula
  oder Binomi.* — Das hast du mit `SOS_A_FS`/`SOS_B_FS` bereits in besserer Form. ✅
- Geteilte Materialsammlung der Studierenden (Altklausuren, Formelsammlungen), Nachfolger des
  eingestellten Teamcollab — **nicht an Dozierende weitergeben**:
  `https://osf.io/nwkhr/overview?view_only=0c9e327aea91468384ab3563cb63b5bb` ✅

## Organisatorisches

- **Fragestunden** laufen über **Teams** (einem Team per Code beitreten, dann startet der Prof
  die Besprechung). Mit einem **privaten Microsoft-Konto kommt man nicht rein** — mehrere
  Leute haben 15 Minuten gebraucht oder es gar nicht geschafft. Vorher testen. ✅
- Inhaltlich haben die Fragestunden SoSe 2026 **nichts Neues gebracht** (auf Nachfrage: „Nein",
  „nichts Wichtiges"). Der Termin verschob sich außerdem kurzfristig. ✅
- **Nicht antreten verbraucht keinen Versuch.** Anmelden + nicht hingehen + nicht
  unterschreiben = „nicht angetreten". Erst die Unterschrift macht den ersten Versuch. ✅
  (Gilt für dich rückwirkend für SoSe 2026.)

## Ableitungen für deinen nächsten Anlauf

1. **Beide Formelsammlungen sind inhaltlich richtig gewichtet** — die Klausurthemen SoSe 2026
   liegen vollständig in dem, was `SOS_A_FS` und `SOS_B_FS` abdecken. Kein Umbau nötig,
   nur Auffrischen.
2. **Der Engpass wird die Zeit sein, nicht der Stoff.** Plane mindestens eine vollständige
   Generalprobe unter Zeit — 90 Minuten, beide Teile, mit vorher festgelegter Reihenfolge.
   Das ist derselbe Hebel, der MDT5/2 gerettet hat.
3. **Priorisiere den Siegl-Teil zeitlich**, wegen des 20-%-Überhangs und weil dort reihenweise
   Aufgaben unbearbeitet blieben.
4. **Korrelationsfunktionen sind der wunde Punkt des ganzen Kurses** — dort mehr Aufgaben
   rechnen als der Umfang im Skript nahelegt.
5. **Ausschlüsse (Wavelet, Kreiskriterium) im neuen Semester neu erfragen**, nicht aus diesem
   Dokument übernehmen.

## Material aus dem Chat, das jetzt hier liegt

- `Notenspiegel/` — SoSe 2025 und SoSe 2026 (Zahlen oben eingearbeitet) ✅
- `SOS_Formelsammlung_aus_Chat.pdf` — 24 Seiten, in der Gruppe als „sieht gut aus" gehandelt.
  **Gegenprobe zu deinen eigenen FS**, nicht als Ersatz: 24 Seiten sind zum Nachschlagen unter
  Zeitdruck zu viel (dasselbe Argument, das in der Gruppe gegen die 24-seitige ED-FS kam).
  Nutzen: einmal durchsehen, ob dir etwas fehlt.
- `Faltung_Kreuz_Autokorrelation_Visualisierung.jpeg` — Schaubild, das Faltung,
  Kreuzkorrelation und Autokorrelation nebeneinanderstellt (x∗y, y∗x, y⋆x, x⋆y, x⋆x, y⋆y je mit
  Verschiebungsskizze). In der Gruppe als „beste Visualisierung" geteilt. **Korrelation ist der
  wunde Punkt des Kurses** — das Bild klärt genau die Verwechslung Faltung ↔ Korrelation
  (Spiegeln oder nicht) und die Asymmetrie der Kreuzkorrelation. Kandidat für die Formelsammlung.

## Noch zu beschaffen

- [ ] Inhalte der SOS-Einsichtnahme vom 29.07. — jemand hatte darum gebeten, Aufgaben
      mitzuschreiben; ob das jemand getan hat, steht nicht im Export.
- [ ] Die Klausur SoSe 2026 selbst (Aufgabentexte) — bisher nur die Themenliste aus dem Chat.
