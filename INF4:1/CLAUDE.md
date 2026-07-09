# INF4:1 — Klausurvorbereitung (Algorithmen & Datenstrukturen)

> **Zweck dieser Datei:** Lern-Logbuch — **sparsam** geführt (Feedback 08.07.):
> Das Mitnahme-PDF `INF4_1_Learnings.tex` steht im Vordergrund und wird primär
> gepflegt. Diese Datei nur bei wirklich Wichtigem kurz aktualisieren (wenige
> Zeilen: Fortschritt, Stolperfallen, Planänderungen). Keine unnötigen Tokens.

---

## 0. Zeitplan & Deadline

**🎯 PRÜFUNG: 13. Juli 2026, 11:00–12:30 Uhr.** (Heute: 30.06.2026 → noch knapp 2 Wochen)

> **📖 OPEN BOOK (geklärt 30.06.):** Alle Hilfsmittel erlaubt. Strategiewechsel — Details
> müssen **nicht auswendig** sitzen, nur **verstanden** sein. Memorieren wird gestrichen,
> der Stoff wandert ins Mitnahme-PDF. **ABER:** Diese Klausur ist überwiegend eine
> *„Mach"-Klausur* (Bäume tracen, Algorithmus entwerfen, MC mit Minuspunkten — §2). Das
> lässt sich **nicht nachschlagen** → Hand-Fertigkeiten (Tracing, Design) bleiben voll im
> Übungsfokus. Gewählter Kürzungsgrad: **moderat** (s. §1).

Verschlankte Lern-Sessions (moderat gekürzt — Verständnis-Lesen + Referenzseite + je 1 Trace
+ 1 kurze Aufgabe pro „Mach"-Thema; keine Recall-Schleifen, kein Übungsblatt je Kapitel):

| Datum | Inhalt | Dauer |
|-------|--------|-------|
| 29.06. ✅ | Kap. 1–3: Grundlagen, **Effizienz**, elem. Sortieren | erledigt |
| 30.06. | INF4/1 (Vorlesung/Praktikum, wiederkehrend) | 14:00–17:15 |
| 01.07. | Kap. 04 + 06: fortg. Sortieren, bin. Suchbäume — Referenzseiten + je 1 Trace (Merge/Quick-Partition, BST-Insert) | verkürzt |
| 03.07. | Kap. 07–08: AVL-, B-Bäume — **Tracing-Schwerpunkt** (AVL-Rotationen, B-Baum-Split) | 13:15–15:15 |
| 06.07. | Kap. 09–10: Hashtabellen, Graphen — Hash-Insert + BFS/DFS tracen | 08:15–10:15 |
| 08.07. | Kap. 11–12 + 15: Dijkstra, MST je 1 Trace; P/NP **nur Verständnis** (open book) | 08:15–10:15 |
| 10.07. | **Probeklausur unter Realbedingungen MIT Mitnahme-PDF** → Fertigkeit *und* Blatt-Tauglichkeit testen; Rezept-Boxen nachschärfen | 08:15–12:00 |
| 12.07. | Leichter Skim + PDF final (**kein** Memorieren) | kurz |
| 13.07. | finaler Blick → **Prüfung** | 08:30 → 11:00 |

> **Entfallen ggü. altem Plan:** eigener „Praktika 01–11 durchsehen"-Slot (09.07.) — die
> Praktikum-Learnings wandern beim jeweiligen Kapitel direkt ins PDF. 12.07. stark verkürzt
> (open book ⇒ kein Last-Minute-Auswendiglernen). Freigewordene Slots → andere Module.
>
> **Konsequenz für die Arbeitsweise:** Pro Session zählt das **Mitnahme-PDF vollständig &
> auffindbar** zu machen + die Hand-Tracings flüssig zu bekommen. Stolperfallen weiter in §4
> notieren, aber Begriffs-Stolperfallen (§4.1–4.6) nicht mehr drillen — nur ins PDF heben.

## 1. Wie Claude beim Lernen helfen soll (Arbeitsweise)

- **Sprache:** Deutsch. Fachbegriffe deutsch *und* englisch nennen (Klausur kann beides verlangen).
- **Lernmodus statt Lösungsmodus:** Nicht sofort die Komplettlösung liefern. Erst
  Verständnis prüfen, Schritte gemeinsam entwickeln, dann zusammenfassen.
- **Aktives Abfragen:** Wenn die Studentin "frag mich ab" o. Ä. sagt → Fragen stellen,
  Antwort abwarten, dann korrigieren/ergänzen.
- **Quellen sind die PDFs in diesem Ordner** (Vorlesung + Praktika). Bei inhaltlichen
  Aussagen aus dem konkreten Foliensatz schöpfen, nicht aus Allgemeinwissen, wenn ein
  PDF das Thema abdeckt.
  - **⚠️ Erst Folien lesen, dann bewerten (08.07. vereinbart):** Bevor ich Lenas Kapitel-
    Zusammenfassung korrigiere oder Aufgaben stelle, **zuerst den zugehörigen Foliensatz per
    Read (PDF) öffnen**. Am 08.07. habe ich Kap. 06 aus dem Kopf „korrigiert" und lag zweimal
    daneben (≤ beidseitig; Löschen 2 Kinder = Nachfolger rechts) — die Folien hatten recht.
- **Komplexität immer mitnennen:** Bei jedem Algorithmus Best/Average/Worst-Case +
  Speicher, stabil ja/nein, in-place ja/nein.
- **Konkret rechnen:** Bei Verständnisfragen kleine Beispiele durchspielen (Array
  sortieren, Baum aufbauen, Hash einfügen) statt nur abstrakt erklären.
- **KEINE 1:1-Aufgaben aus der Probeklausur** stellen — nur *analoge* (andere Zahlen,
  andere Verfahren gleicher Tiefe). Die Probeklausur (`Klausurvorbereitung.pdf`) zeigt nur
  das Niveau; sie soll nicht „verbraucht" werden.
- **Lernpsychologie:** Active Recall vor dem Ergänzen, Testing Effect (Aufgaben), Spacing
  (Sessionstart: 2 Min Vorkapitel abrufen), Stolperfallen in §4 sammeln und gezielt wiederholen.

### Verschlankter Lern-Workflow pro Kapitel (OPEN BOOK, moderat gekürzt — ab 30.06.)
1. Lena liest den Foliensatz **einmal auf Verständnis** (kein Memorieren, kein Recall-Schreiben).
2. Claude verdichtet das Kapitel zu **Referenzseite + Rezept-Box** im Mitnahme-PDF
   (Praktikum-Learnings gleich mit rein, s. §3b).
3. Nur bei **„Mach"-Themen** (Bäume/Graphen/Tracing): **1 Trace gemeinsam**, bis der Ablauf
   flüssig ist + **1 kurze analoge Aufgabe**. Bei reinen Verständnis-Themen (z.B. P/NP) entfällt das.
4. Sitzt der Ablauf → nächstes Kapitel. **Keine** Recall-Schleife, **kein** volles Übungsblatt je Kapitel.

> **Was gestrichen ist (open book):** Auswendiglernen von Definitionen/Formeln/Tabellen, die
>2-Min-Spacing-Abfragen am Sessionstart, das Drillen der Begriffs-Stolperfallen §4.1–4.6.
> Diese Inhalte **nur noch ins PDF heben**, nicht mehr abprüfen.
> **Was bewusst bleibt:** Hand-Tracing (AVL/B-Baum/Hash/BFS/DFS/Dijkstra/MST), Algorithmus-Design
> (Sliding Window & Co.), die Probeklausur. Das lässt sich nicht nachschlagen.

### Archiv: alter Workflow (galt bis 29.06., closed-book-Annahme)
Read-Recall-schreiben → ergänzen → Praktikum → Aufgaben → Recap-Schleife bei Schwächen.
Durch den Open-Book-Wechsel ersetzt; hier nur als Historie.

## 2. Prüfungsstil (aus Probeklausur abgeleitet)

Prüfer: **Prof. Dr. O. Hofmann.** Aufgabentypen & Niveau:
- **Algorithmus selbst entwerfen** (Pseudocode/Struktogramm) mit geforderter Komplexität,
  z.B. „max. Summe 3 aufeinanderfolgender Zahlen in $O(n)$" → Sliding Window. (8 P)
- **Multiple Choice** zu O/Ω/Θ-Mengenbeziehungen — **Minuspunkte für Falsches**, kein
  negatives Gesamtergebnis. → im Zweifel nicht ankreuzen. (3 P)
- **Algorithmus von Hand tracen**, Zwischenzustände angeben, z.B. SELECT-Sort: Feld nach
  *jedem Tausch*. (5 P)
- **Bäume von Hand**: AVL-Balancefaktor erklären, Element einfügen + rebalancieren zeichnen. (8 P)
- **Fokus:** Anwenden/Durchspielen + exakte Definitionen + Pseudocode. **Kein Programmieren.**

## 3b. Lieferbares Artefakt — **jetzt das wichtigste Klausur-Werkzeug (open book)**

`INF4_1_Learnings.tex` → `INF4_1_Learnings.pdf`: lesbare Lern-Zusammenfassung, **eine Seite
pro Foliensatz** (Def-/Tipp-/Stolperfallen-Boxen). **Bewusst KEIN Formelsammlungs-Layout**
(nicht die 3-spaltige FS der rechtlichen Module). Nach jedem Kapitel um eine Seite erweitern
(`\clearpage` + `\kapitel{}{}`) und neu kompilieren (`pdflatex`, 2×).

> **⭐ Aufgewertet (30.06., open book):** Dieses PDF nimmt Lena **mit in die Klausur** → vom
> Spickzettel zum zentralen Werkzeug. Anforderungen daher höher:
> - **Vollständig** — auch der nicht-memorierte Stoff (alle Definitionen, Komplexitätstabellen,
>   Landau-Regeln) muss drinstehen, weil nichts mehr im Kopf „gepuffert" ist.
> - **Schnell auffindbar** — Inhaltsverzeichnis / Kopfzeile mit Kapitelname; in 90 Min zählt Sekunden.
> - **Rezept-Boxen pro Verfahren** — knappe Schritt-für-Schritt-Abläufe (z.B. „AVL-Insert:
>   einfügen → Balancefaktoren hoch → erste Verletzung → Rotationstyp → rotieren"), damit das
>   Blatt beim *Machen* hilft, nicht nur beim Nachschlagen.
> - **Am 10.07. an der Probeklausur getestet** — taugt das Blatt unter Realbedingungen?

> **Regel:** Die Learnings aus dem **zugehörigen Praktikum** gehören grundsätzlich mit auf die
> Kapitelseite (Nummerierung versetzt, s. §2b: Praktikum $k$ → Kap. $k{+}1$). Also pro Kapitel
> *Vorlesung + Praktikum* zusammenführen, nicht nur die Folien.
> **Inhalt strikt auf den jeweiligen Foliensatz begrenzen** — kein Stoff aus späteren Kapiteln
> vorwegnehmen (z.B. Merge Sort gehört zu Kap. 04, nicht auf die Kap.-03-Seite).

### 3c. Mitnahme-**Gesamtskript** (alle Vorlesungsfolien, 4-up) — `INF4_1_Gesamtskript_4up.pdf`

Gedrucktes Komplett-Skript für die Klausur: **alle 12 inhaltlichen Vorlesungs-Decks** (Kap. 02–15,
ohne 01_Allgemeines/Praktika), **4 Folien pro A4-Blatt** (quer, 2×2, Rahmen). Label unten rechts je
Folie: **„Kapitel – Thema  «Foliennr.»``** (z.B. „Fortg. Sortieren – Counting-Sort 45"); je Blatt
**„Blatt «Nr.»``** in der Ecke. Titel-, „Ziele der heutigen Lerneinheit"- und „Vielen Dank"-Folien
raus; Animations-Zwischenschritte moderat gefiltert (letzte vollständige Folie bleibt).
> **Konvention (01.07.):** **Effizienzüberlegung/-betrachtung-Folien werden aus dem Gesamtskript
> entfernt** — die Komplexität gehört **kompakt pro Algorithmus ins Learning-PDF** (Best/Avg/Worst
> + Speicher/in-place). Betrifft **nicht** Vergleichstabellen und **nicht** die Trace-/Beispiel-Folien.
> Für Kap. 06+ (BST/B-Bäume …) sind die Effizienz-Folien schon rausgenommen → die Werte müssen beim
> Durcharbeiten des jeweiligen Kapitels **noch ins Learning-PDF** (Kap. 02–04 stehen dort bereits).
> Regeneriert wird über das Python-Skript im Scratchpad (Symlinks s01–s12 → Decks, pdfpages-Pass A
> nummeriert+labelt, Pass B macht 4-up + Blattnr.).

## 2b. Themenliste (aus dem Ordner)

Reihenfolge = Foliennummerierung. Status: ⬜ offen · 🟡 angefangen · ✅ sitzt

| Nr | Thema | Status | Notiz |
|----|-------|--------|-------|
| 01 | Allgemeines | 🟡 | von Lena gelernt + abgefragt (29.06.); 2 Schwachstellen offen → §4 |
| 02 | Effizienz / Big-O | 🟡 | von Lena gelesen + Recap (29.06.); O/Ω-Verwechslung korrigiert → §4. **Praktikum 01** (= Kap. 02) erledigt |
| 03 | Elementares Sortieren | 🟡 | gelesen + Recap + Praktikum 02 + Übungsblatt (30.06.) → §3.2. Ergebnisse alle richtig; 2 Begründungs-Stolperfallen §4.7–4.8 (Selection-Mechanik, Induktion). Vor Klausur kurz nachhaken |
| 04 | Fortgeschrittenes Sortieren | 🟡 | von Lena gelesen (01.07.): Quick/Heap/Counting Sort + untere Schranke → §3.3. 3 Stolperfallen §4.9–4.11. Quicksort-Trace (grafisch) ergänzt |
| 06 | Binäre Suchbäume | ✅ | gelesen + 3 Lösch-Traces (08.07.): 1. Versuch Wiederanhäng-Fehler → §4.14, Blitz-Trace danach fehlerfrei. PDF-Seite + Übersichtszeilen gebaut. Praktikum 4 (= BST!) gesichtet: Entartungs-Drill + Rekurrenzen ins PDF; AVL-Löschen-Teil → Kap. 07 |
| 07 | AVL-Bäume | ✅ | gelesen + Traces (08.07.): BF-Bestimmung, Einfügen (einfache + Doppelrotation), Löschen alle 3 Fälle inkl. lösch-ausgelöster Doppelrotation — fehlerfrei. PDF-Seite + Übersichtszeilen gebaut. Kein eigenes Praktikum (AVL-Teil = Praktikum 4, erledigt) |
| 08 | B-Bäume | 🟡 | gelesen + Abfrage + Lösch-Traces (09.07.): 1. Versuch Unterlauf-Knoten weggelassen → §4.16, Blitz-Trace danach fehlerfrei, **aber laut Lena mit sehr langer Überlegungszeit → Lösch-Drill vor der Klausur wiederholen** (z.B. 10.07. nach der Probeklausur oder 12.07.). PDF-Seite + 2 Übersichtszeilen gebaut. Praktikum 05 gesichtet (m-vs-I/O + 4-KB-Block-Rechnung ins PDF; Graphviz/Code übersprungen) |
| 09 | Hashtabellen | ⬜ | |
| 10 | Suche in Graphen (BFS/DFS) | ⬜ | |
| 11 | Kürzeste Wege | ⬜ | |
| 12 | Aufspannende Bäume (MST) | ⬜ | |
| 15 | Komplexität (P/NP) | ⬜ | |

Praktika 01–11 als Übungsmaterial / klausurnahe Aufgaben vorhanden.

> **⚠️ Praktikum-Nummerierung ≠ Kapitelnummer!** Die Praktika sind versetzt:
> Praktikum 01 → Kap. 02, Praktikum 02 → Kap. 03 („Debriefing") usw. **Aber der Versatz ist
> nicht durchgehend $k{+}1$** (es gibt kein Kapitel-05-Deck): **Praktikum 04 → Kap. 06 (BST)**,
> **Praktikum 05 → Kap. 08 (B-Baum)** — AVL (Kap. 07) hat **kein eigenes Praktikum** (der
> AVL-Lösch-Teil steckt in Praktikum 04); beides verifiziert 08.07. Im Zweifel den Titel auf
> Seite 1 des Praktikums prüfen.

## 3. Fachliche Erkenntnisse (gesicherter Lernstoff)

> Pro Eintrag: Kernidee + typische Klausurfrage + Stolperfalle.

### 3.0 Grundbegriffe (Kap. 01)

**4 Merkmale eines Algorithmus** (Eselsbrücke F-T-D-A): **Finitheit** (endlich beschreibbar),
**Terminiertheit** (endet in endl. Zeit), **Determiniertheit** (eindeutig, kein Spielraum),
**Allgemeingültigkeit** (für versch. Eingaben). Definition: endliche Folge von Regeln →
nach endl. vielen, eindeutig festgelegten Schritten → Lösung einer Klasse von Problemen.

**Datenstruktur:** Organisation der vom Algorithmus bearbeiteten Daten; Algo & DS bedingen
sich gegenseitig. **Darstellungsformen:** informell → UML-Aktivitätsdiagramm → Struktogramm
(Nassi-Shneiderman, DIN 66261) → Pseudocode → Implementierung. **Eigenschaften:** Korrektheit
+ Effizienz, **beide unabhängig von der Implementierung**. **Korrektheitsnachweis** = Terminierung
+ Schleifeninvariante (Bsp. Euklid-ggT). **RAM-Modell** (Random Access Machine): zählt Befehle
(Laufzeit) bzw. Zellen (Speicher) statt real zu messen.

**Typische Klausurfrage:** 4 Merkmale nennen / „welche Eigenschaft ist verletzt?``
**Stolperfalle:** Finitheit (endl. Beschreibung) ≠ Terminiertheit (endl. Laufzeit).

### 3.1 Effizienz & Landau-Symbole (Kap. 02)

**Kernidee:** Komplexität = Befehlszahl (Laufzeit) bzw. Speicherzellen (Speicher) als
Funktion der Problemgröße $n$. Für große $n$ zählt nur der **führende Term**, konstante
Koeffizienten fallen weg: $1{,}5n^2 + 0{,}5n - 1 \to \Theta(n^2)$.

**Leitbeispiel Maximale Abschnittssumme** (4 Ansätze = 4 Klassen):

| Ansatz | Komplexität | Name |
|--------|-------------|------|
| MAXFOLGE1 (3 Schleifen) | $O(n^3)$ | kubisch |
| MAXFOLGE2 (2 Schleifen) | $O(n^2)$ | quadratisch |
| MAXFOLGE3 (Teile-und-Herrsche) | $O(n\log n)$ | — |
| MAXFOLGE4 (einmal durchlaufen) | $O(n)$ | linear |

**Landau-Symbole** (für $n \ge n_0$, positive Konstanten):

- $O(g)$: obere Schranke, „höchstens so schnell" — $0 \le f(n) \le c\,g(n)$
- $\Omega(g)$: untere Schranke, „mindestens so schnell" — $0 \le c\,g(n) \le f(n)$
- $\Theta(g)$: scharfe Schranke, „genauso schnell" — $0 \le c_1 g(n) \le f(n) \le c_2 g(n)$
- **Beziehungen:** $\Theta(f)=O(f)\cap\Omega(f)$; $\;\Theta(f)\subseteq O(f)$; $\;\Theta(f)\subseteq\Omega(f)$

**Typische Klausurfragen:** (a) Komplexität eines Pseudocodes anhand verschachtelter
Schleifen bestimmen; (b) $c$ und $n_0$ für $f\in O(g)$ finden; (c) Notationen O/Ω/Θ
abgrenzen.

**Stolperfallen:** O ist nur obere Schranke (auch $n \in O(n^2)$ ist korrekt!) — für die
*exakte* Klasse Θ verwenden. Historie: **Bachmann** führte O ein, **Landau** machte es bekannt.

### 3.2 Elementares Sortieren (Kap. 03)

**Eigenschaften eines Sortierverfahrens** (Klausur-Vokabular):
- **korrekt** = terminiert (finit) + liefert sortierte Permutation der Eingabe
- **in-place** = nur $O(1)$ Zusatzspeicher (lokale Variablen erlaubt, kein zweites Feld)
- **stabil** = gleichwertige Elemente behalten ihre relative Reihenfolge über die gesamte Laufzeit

**Die drei elementaren Verfahren** (alle $\Theta(n^2)$ avg/worst, in-place):

| Verfahren | Best | Avg | Worst | stabil | Mechanik |
|-----------|------|-----|-------|--------|----------|
| **Selection** | $n^2$ | $n^2$ | $n^2$ | ✗ | sucht Min des unsort. Rests, hängt an sort. Teil an |
| **Insertion** | $n$ | $n^2$ | $n^2$ | ✓ | nimmt 1. unsort. Element, schiebt es von hinten in sort. Teil |
| **Bubble** | $n$ | $n^2$ | $n^2$ | ✓ | vertauscht benachbarte Paare, „blubbert" durch; mehrere Durchläufe |

**Best/Worst/Average-Case allgemein:** Best = Array bereits sortiert, Worst = umgekehrt
sortiert (allg.: jedes Element muss mit jedem verglichen werden), Average = zufällig.

**Typische Klausurfragen:** SELECT-Sort von Hand tracen, Feld **nach jedem Tausch** angeben
(§2, 5 P); stabil/in-place einordnen; Best-Case-Komplexität begründen.

**Stolperfallen (Kap. 03, 30.06.):**
- **Selection Sort hat KEINEN guten Best-Case** → auch bei sortiertem Feld $n^2$, weil der
  innere Pointer *immer* den ganzen Rest durchläuft, um das Min zu finden (datenunabhängig,
  ~$n^2/2$ Vergleiche). Die Regel „Best = sortiert ⇒ $n$" gilt nur für Insertion/Bubble!
  Dafür hat Selection nur $O(n)$ **Swaps** (relevant, wenn Tauschen teuer ist).
- **Selection Sort ist meist NICHT stabil:** der Min-Swap kann gleichwertige Elemente
  überspringen. Bsp. $[5_a, 5_b, 1] \to [1, 5_b, 5_a]$ (5er vertauscht).
- **Bubble Best-Case $n$ nur mit „swapped"-Flag:** ohne die Abbruch-Optimierung (kein Tausch
  im Durchlauf ⇒ fertig) läuft naives Bubble Sort immer $n^2$.

### 3.3 Fortgeschrittenes Sortieren (Kap. 04)

**Überblick** ($k$ = Größe des Wertebereichs bei Counting Sort):

| Verfahren | Best | Avg | Worst | stabil | in-place | Idee |
|-----------|------|-----|-------|--------|----------|------|
| **Quicksort** | $n\log n$ | $n\log n$ | $n^2$ | ✗ | ✓ ($O(\log n)$ Stack) | Pivot → partitionieren → rekursiv |
| **Heapsort** | $n\log n$ | $n\log n$ | $n\log n$ | ✗ | ✓ | Max-Heap bauen, Wurzel abtragen |
| **Counting Sort** | $n+k$ | $n+k$ | $n+k$ | ✓ | ✗ | zählen statt vergleichen (Wertebereich bekannt) |

**Quicksort** — Pivot wählen (oft **Median-of-Three**), Pivot an die **letzte Stelle**, dann
Zwei-Zeiger-Partition: linker Zeiger läuft nach rechts bis Wert **≥ Pivot**, rechter nach links
bis Wert **≤ Pivot** — beide vergleichen mit dem **Pivot**, *nicht miteinander*. Stehen beide →
**Tausch**. Kreuzen sich die Zeiger → Pivot an die Position des linken Zeigers tauschen (jetzt
**endgültig platziert**). Rekursion auf linkem/rechtem Teil **ohne** den Pivot. Worst Case $n^2$
bei ungünstigem Pivot (immer kleinstes/größtes Element ⇒ z. B. bereits sortiertes Feld) —
Median-of-Three entschärft genau das.

**Heapsort** — 1) Feld als **Max-Heap** aufbauen (Kind ≤ Elternknoten; als Array: Kinder von
$i$ liegen bei $2i{+}1,\,2i{+}2$). 2) Wurzel (= Maximum) mit letztem Heap-Element tauschen,
Heap-Größe um 1 **verkleinern** (das Max liegt jetzt endgültig hinten, „gelöscht" = nur Größe−1).
3) `heapify`/`sift-down` von der Wurzel ⇒ Max-Heap wiederhergestellt. 4) wiederholen, bis der
Heap leer ist. Kein Zusatzspeicher, aber **nicht stabil**.

**Untere Schranke** — Jedes **vergleichsbasierte** Sortierverfahren braucht im Worst Case
$\Omega(n\log n)$ Vergleiche (Entscheidungsbaum hat $n!$ Blätter ⇒ Höhe $\ge \log_2(n!) =
\Theta(n\log n)$). Merksatz: **schneller als $n\log n$ geht mit reinen Vergleichen nicht.**

**Counting Sort** — umgeht die Schranke, weil es **nicht vergleicht, sondern zählt** (Wertebereich
$0..k$ muss bekannt & klein sein). 1) Zählarray $C$: wie oft kommt jeder Wert vor. 2) **Präfixsumme**
über $C$: danach ist $C[v]$ = Anzahl Elemente $\le v$ (= Endposition von $v$). 3) Eingabe **von
hinten** durchlaufen (⇒ **Stabilität**): Element $v$ → Ausgabe an Position $C[v]-1$, dann $C[v]{-}{-}$.
$O(n+k)$, **stabil**, **nicht in-place**.

#### Quicksort-Trace (grafisch)

Konvention: `L` = linker Zeiger, `R` = rechter Zeiger, `P` = Pivot (steht an letzter Stelle).
Gezeigt ist jeweils der **Moment vor einem Tausch**.

**Pass 1 — Feld `4 2 7 1 6 3 8 5`, Pivot = 6** (an letzte Stelle geschoben ⇒ `…8 6`, die 5 rutscht auf Index 4):

```
       4  2  7  1  5  3  8  6      Zeiger stoppen: L bei 7 (≥6), R bei 3 (≤6)
             L        R     P      → L < R ⇒ Tausch 7 ↔ 3
```
```
       4  2  3  1  5  7  8  6      weiter: L stoppt bei 7 (Idx5), R bei 5 (Idx4)
                   R  L     P      → Zeiger gekreuzt (L rechts von R) ⇒ Pivot setzen: 7 ↔ 6
```
Ergebnis: `[4 2 3 1 5]  6  [8 7]` — die 6 ist endgültig platziert.

**Pass 2 — linkes Teilfeld** (du hattest `4 2 5 1 3` genannt — genau das), **Pivot = 3** (schon letzte Stelle):

```
       4  2  5  1  3      Zeiger stoppen: L bei 4 (≥3), R bei 1 (≤3)
       L        R  P      → L < R ⇒ Tausch 4 ↔ 1
```
```
       1  2  5  4  3      weiter: L stoppt bei 5 (Idx2), R bei 2 (Idx1)
          R  L     P      → gekreuzt ⇒ Pivot setzen: 5 ↔ 3
```
Ergebnis: `[1 2]  3  [4 5]` → nach den (trivialen) Rekursionen auf `[1 2]` und `[4 5]` ist alles sortiert.

### 3.4 Binäre Suchbäume (Kap. 06)

**Kernidee:** Menge schon *beim Einfügen* in eine Baumstruktur einsortieren → effizientes
Suchen, dynamisch wachsend. **Binärbaum:** Knoten mit max. 2 Kindern; Blätter = äußere Knoten
(kein Kind); kann unbalanciert sein ⇒ *kein* Array-Mapping (anders als Heap), verkettet.

**BST-Eigenschaft (Folie 8):** für jeden Knotenwert $x$: $\forall v$ im **linken** Teilbaum
$v\le x$, $\forall w$ im **rechten** Teilbaum $x\le w$ — gilt für den **ganzen Teilbaum**, nicht
nur die Kinder; **$\le$ auf beiden Seiten** (Duplikate beidseitig erlaubt). BST zu einer Menge
**nicht eindeutig** (Einfügereihenfolge bestimmt die Form).

**Operationen:** *Sortieren* = **Inorder-Tree-Walk** (links → Knoten → rechts) ⇒ aufsteigend,
$O(n)$. *Suchen* TREE-SEARCH $O(h)$. *Einfügen* absteigen bis NIL, als **Blatt** einhängen $O(h)$.

**Löschen — 3 Fälle (Folien 13–15):** (1) **Blatt** → entfernen. (2) **ein Kind** → Zeiger aufs
einzige Kind umlenken. (3) **zwei Kinder** → durch **symmetrischen Nachfolger** = **kleinster
Wert im rechten Teilbaum** ersetzen; ist der ein innerer Knoten, hat er kein linkes Kind → sein
**rechtes** Kind nachrücken lassen.

**Komplexität (Folie 16):** Traversieren $O(n)$; Suchen/Einfügen/Löschen $O(h)$. $h\approx\log n$
balanciert, $h=n$ entartet (sortierte Eingabe → Kette) ⇒ Motivation für AVL (Kap. 07).
**Höhen-Konvention (AVL-Folie 3, verifiziert 08.07.):** Höhe wird in **Knoten-Ebenen** gezählt,
**Wurzel zählt mit** — Kette aus $n$ Knoten hat Höhe $n$ (nicht $n{-}1$ wie in CLRS/Lehrbüchern
mit Kanten-Zählung). Wichtig für AVL-Balancefaktoren!

**Typische Klausurfrage:** Baum von Hand (8 P) — einfügen bzw. löschen zeichnen; beim Löschen
erst Fall bestimmen. **Stolperfallen §4.12–4.13.**

## 4. Stolperfallen & häufige Fehler

**🔁 OFFEN — nach Abschluss Kap. 02 mit Lena wiederholen (Re-Recall):**

1. **Finitheit = endliche *Beschreibung*** (endlich viele Regeln / endlich aufschreibbar) —
   *nicht* „endliche Ressourcen / Bibliotheken". Lena verwechselte Finitheit zweimal:
   erst mit „endliche Anzahl Schritte", dann mit „Ressourcen wie Bibliotheken".
   Abgrenzung: Finitheit (endl. Beschreibung) ≠ Terminiertheit (endl. Laufzeit).
2. **Die zwei zentralen Eigenschaften = Korrektheit + Effizienz.** Lena nannte statt
   *Korrektheit* fälschlich *Komplexität* (Komplexität ist Teil der Effizienz, Kap. 02).
3. **O und Ω im „gut"-Wortlaut vertauscht (Kap. 02, 29.06.).** Lena: „O = höchstens so gut,
   Ω = mindestens so gut" — genau andersrum. Ursache: „schneller wachsen = mehr Laufzeit =
   *schlechter*". Richtig: **O** = obere Schranke = wächst *höchstens* so schnell = a ist
   *mindestens* so gut; **Ω** = untere Schranke = wächst *mindestens* so schnell = a ist
   *höchstens* so gut. **Merkhilfe:** in „wächst so schnell" denken, nicht in „so gut".
   Gegencheck: $n\in O(n^2)$, aber Laufzeit $n$ ist *besser* als $n^2$ → O heißt „mind. so gut".
   (Klausurrelevant: MC zu O/Ω/Θ mit Minuspunkten, §2!)
4. **Exponentiell schlägt Polynom (Kap. 02, 29.06.).** Lena kreuzte $2^n \in O(n^2)$ als *wahr*
   an — falsch. $2^n$ wächst schneller als **jedes** Polynom → $2^n \notin O(n^2)$.
   Wachstumshierarchie merken: $1 < \log n < n < n\log n < n^2 < n^3 < 2^n < n!$.
5. **„nur O" richtig begründen (Kap. 02, 29.06.).** Lena begründete „nur O" mit „kein
   (ganzzahliger) Wert für $c$". $c$ muss **nicht** ganzzahlig sein. Korrekt: $\Theta$ scheitert
   an der **unteren** Schranke $\Omega$, weil $f$ *strikt langsamer* wächst, d.h.
   $f(n)/g(n)\to 0$. (Lenas Schlussfolgerungen waren aber alle richtig — nur die Begründung.)
6. **Innere Schleife `for j=i to n` (Kap. 02, 29.06.).** Lena: „läuft häufiger als n-mal" —
   umgekehrt: sie macht $n-i+1$ Durchläufe, also *abnehmend* von $n$ auf $1$ (≈ $n/2$ im Schnitt).
   Gesamt $\tfrac{n(n+1)}{2}=\Theta(n^2)$. Ergebnis war richtig, Begründung verdreht.

**Kap. 03 (30.06., aus Übungsblatt Kap. 03):**

7. **Selection- vs. Insertion-Mechanik (Aufg. 3).** Lena beschrieb Selection Sort mit „vergleicht
   mit dem *letzten sortierten* Element`` — das ist **Insertion Sort**. Selection sucht das
   *Minimum des unsortierten Rests* (muss immer den ganzen Rest absuchen). Merke: $n^2$ bei
   Selection kommt aus den **Vergleichen** (Minimumsuche, datenunabhängig), nicht aus Tauschen.
8. **Induktion ≠ nur Basisfall (Aufg. 4).** Lena: Induktionsbeweis zeige, „dass auch bei 1 Element
   der Alg funktioniert``. Das ist nur der **Basisfall**. Der Beweis zeigt die ganze Rekursion:
   Basis + **Annahme** (kleinere Aufrufe korrekt) + **Schritt** (zwei sortierte Hälften + Merge
   → ganz sortiert). Der *Schritt* ist der Kern. (Korrektheits-Ergebnisse waren überall richtig,
   nur die Begründungen unscharf — gleiches Muster wie Kap. 02.)

**Kap. 04 (01.07., aus Lenas Kapitel-Zusammenfassung):**

9. **Quicksort-Zeiger vergleichen mit dem *Pivot*, nicht miteinander.** Lena: „die Werte der beiden
   Pointer werden immer miteinander verglichen". Richtig: linker Zeiger stoppt bei **≥ Pivot**,
   rechter bei **≤ Pivot** — jeder gegen den **Pivotwert**; erst *dann* wird getauscht.
10. **Untere Schranke ist eine *untere* Grenze.** Lena: vergleichsbasierte Sortierer „können nur
    $n\log n$ erreichen". Schärfer: $\Omega(n\log n)$ heißt, sie kommen **nicht darunter** (nicht
    besser als $n\log n$). „Undefinierte Elemente" = man kann Elemente nur paarweise vergleichen.
11. **Counting-Sort-Zählarray wird am Ende *nicht* komplett null.** Lena-Annahme: fertig, „wenn das
    Hilfsarray nur Nullen enthält". Tatsächlich endet jedes $C[v]$ bei „Anzahl Elemente **echt
    kleiner** als $v$" (nur der kleinste Wert endet bei 0). Abbruchkriterium ist: **alle $n$
    Eingabe-Elemente einsortiert**.

**Kap. 06 (08.07., beim Foliencheck aufgefallen — Fehler waren diesmal bei *mir*, nicht bei Lena):**

12. **BST-Eigenschaft gilt für den ganzen Teilbaum, nicht nur die Kinder.** Lenas Formulierung
    „die *Kinder* ≤ Elternknoten" ist zu eng — es sind *alle Nachfahren* im linken Teilbaum.
    (Lenas „links ≤, rechts ≥" war dagegen korrekt und deckt sich mit Folie 8: ≤ beidseitig.)
13. **Löschen mit 2 Kindern: Foliensatz nimmt den Nachfolger aus dem RECHTEN Teilbaum**
    (kleinster Wert dort), nicht den Vorgänger von links. Beide ergeben gültige BSTs, aber die
    Klausur folgt den Folien. Feinheit: ist der Nachfolger ein innerer Knoten, hat er kein linkes
    Kind → rechtes Kind nachrücken.
14. **Beim 2-Kinder-Löschen zieht NUR der Nachfolger um (Trace 08.07.).** Lena hängte beim
    Löschen der 20 den restlichen rechten Teilbaum (30…) *unter* das rechte Kind des Nachfolgers
    (23) → Baum umgebaut statt lokal repariert. Richtig: (1) rechtes Kind des Nachfolgers rückt
    an dessen *alte* Stelle, (2) Nachfolger übernimmt Position **und beide Kinder** des
    Gelöschten — sonst ändert sich nichts. Tückisch: ihr Ergebnis war trotzdem ein gültiger BST
    (Inorder sortiert!) — die Klausur will aber das Ergebnis des *Verfahrens*. Merksatz: „Der
    Nachfolger zieht allein um."
15. **Median ≠ Mittelwert (Praktikum-4-Drill, 08.07.).** Lena: ausgewogener Baum entsteht, wenn
    „der *Mittelwert* des (Teil-)Arrays" die Wurzel bildet. Richtig ist der **Median = das
    mittlere *Element* des sortierten Arrays** (dann rekursiv auf beide Hälften). Gegenbeispiel
    $[1,2,3,100]$: Mittelwert $26{,}5$ ist gar kein Element; der Median-Ansatz nimmt die $2$
    oder $3$. Bei $[1..8]$ fallen beide zufällig zusammen — deshalb fiel der Fehler nicht auf.
    (Gleiches Muster wie §4.5/4.7–4.8: Ergebnis richtig, Begründung unscharf.)

**Kap. 08 (09.07., aus den Lösch-Traces):**

16. **B-Baum: Unterlauf-Knoten nie einfach weglassen.** Lena ließ beim Löschen (Unterlauf) den
    leeren Knoten komplett wegfallen und prüfte „Wurzel hat noch ≥ 2 Kinder" — falsches Kriterium.
    Richtig: **Kinder = Schlüssel + 1 in jedem Knoten**; ein Unterlauf wird immer repariert
    (erst Verschieben übers Elternteil, sonst Verschmelzen). Merksatz: „Unterlauf? Knoten bleibt!"
    Blitz-Trace danach fehlerfrei. Zweite Feinheit: innerer Knoten → B-Baum-Folien nehmen den
    **Vorgänger von links** (BST Kap. 06: Nachfolger von rechts). Außerdem korrigiert: Baum wächst
    nur beim **Wurzel-Split** in die Höhe, nicht „wenn alle Knoten voll sind".

## 5. Offene Fragen / noch klären

- ~~Erlaubte Hilfsmittel?~~ → geklärt **30.06.: OPEN BOOK**, alle Hilfsmittel erlaubt.
  Strategiewechsel s. §0/§1; Mitnahme-PDF = zentrales Werkzeug (§3b).
- Schwerpunkt der Klausur (Rechnen vs. Verständnis vs. Pseudocode schreiben)?
- ~~Klausurdatum~~ → geklärt: **13.07.2026** (s. §0).

---

## Änderungslog

- **2026-06-29:** Datei angelegt. Themenliste aus Ordnerinhalt abgeleitet, Arbeitsweise definiert.
- **2026-06-29:** Kap. 02 (Effizienz/Big-O) durchgearbeitet → §3.1. Zeitplan + Prüfungstermin (13.07.) in §0 ergänzt.
- **2026-06-29:** Probeklausur analysiert → Prüfungsstil §2. Lern-Workflow §1 festgehalten.
  Learnings-PDF (`INF4_1_Learnings.tex/.pdf`) angelegt (kein FS-Layout!), §3b.
- **2026-06-29:** Kap. 01 (Grundbegriffe) durchgearbeitet → §3.0 + PDF-Seite 2 ergänzt.
- **2026-06-29:** Kap. 01 mit Lena per Active Recall abgefragt → Status 🟡. 2 Schwachstellen
  in §4 vermerkt (Finitheit=Beschreibung; Korrektheit als 2. Eigenschaft), nach Kap. 02 wiederholen.
- **2026-06-29:** Kap. 02 von Lena gelesen + Recap. Komplexitätsberechnung sitzt; O/Ω im
  „gut"-Wortlaut vertauscht → Stolperfalle §4.3. Status Kap. 02 → 🟡 (Praktikum 02 als Nächstes).
- **2026-06-29:** Praktikum 1 (= Kap. 02) durch. Übungsblatt `Uebung_Kap02.tex/.pdf` erstellt
  (5 Aufgaben + Bonus, ohne Lösungen). Lena bearbeitet → Auswertung: O/Ω-Richtung sitzt jetzt
  (alle Schlüsse korrekt!). 3 neue Stolperfallen §4.4–4.6 ($2^n\notin O(n^2)$; „nur O" via
  $f/g\to0$; `for j=i to n` abnehmend). $c/n_0$-Aufgabe sauber gelöst.
- **2026-06-30:** Kap. 03 (Elementares Sortieren) von Lena gelesen + Recap → §3.2. Mechanik
  aller drei Verfahren korrekt erfasst; ergänzt: „?"=**stabil**; 2 Korrekturen: Selection
  hat keinen guten Best-Case ($n^2$ auch sortiert) und ist meist nicht stabil; Bubble-Best $n$
  nur mit Flag. Status Kap. 03 → 🟡.
- **2026-06-30:** Praktikum-Nummerierung geklärt (versetzt: Praktikum $k$ → Kap. $k{+}1$),
  Warnhinweis in §2b. In-place geschärft: $O(1)$ = unabhängig von $n$ (nicht Variable-vs-Array;
  Merge Sort $O(n)$ ⇒ nicht in-place) → als Stolperfalle in Learnings-PDF. Kap.-03-Seite ins
  `INF4_1_Learnings.tex/.pdf` ergänzt.
- **2026-06-30:** Learnings-PDF: Korrektheitsnachweis-über-Invariante-Box ergänzt (3 Schritte
  Init/Erhaltung/Terminierung, Insertion-Sort-Beispiel mit Walkthrough $[5,2,4,1]$). Merge Sort
  wieder entfernt (gehört zu Kap. 04, nicht vorwegnehmen). Neue Regel in §3b: Praktikum-Learnings
  gehören grundsätzlich mit auf die Kapitelseite; Inhalt strikt auf den Foliensatz begrenzen.
- **2026-06-30:** Aus Praktikum 02 (Aufg. 3/4): Kurzbox „Korrektheit der Rekursion: (strukturelle)
  Induktion" auf Kap.-03-Seite ergänzt — Dominoprinzip (Basis/Annahme/Schritt), Merge nur als
  knappes Beispiel, Kernaussage Schleifeninvariante + Induktion = volle Korrektheit.
- **2026-06-30:** Übungsblatt `Uebung_Kap03.tex/.pdf` (5 Aufgaben) mit Lena durchgearbeitet.
  Ergebnisse alle korrekt (SELECT-Trace, Eigenschaften-Tabelle, Best-Case, Induktion, Stabilität);
  Begründungen z.T. unscharf → 2 neue Stolperfallen §4.7–4.8 (Selection-vs-Insertion-Mechanik;
  Induktion ≠ nur Basisfall). Status Kap. 03 bleibt 🟡 (vor Klausur kurz nachhaken).
- **2026-06-30:** **🔄 UMPLANUNG — Klausur ist OPEN BOOK** (vorher closed-book angenommen).
  Strategiewechsel: Memorieren raus, Stoff wandert ins Mitnahme-PDF; Hand-Tracing & Design
  bleiben voller Übungsfokus (nicht nachschlagbar). Kürzungsgrad **moderat** (Lena gewählt).
  §0 Zeitplan verschlankt (09.07.-Praktika-Slot entfällt, 12.07. verkürzt, Probeklausur 10.07.
  jetzt MIT PDF), §1 neuer Workflow + alter archiviert, §3b PDF zum zentralen Klausur-Werkzeug
  aufgewertet (Vollständigkeit/Auffindbarkeit/Rezept-Boxen), §5 Hilfsmittel-Frage geklärt.
- **2026-07-01:** Kap. 04 (Fortgeschrittenes Sortieren) von Lena gelesen + Recap → §3.3
  (Quick-/Heap-/Counting Sort + untere Schranke, Komplexitätstabelle). 3 Korrekturen als
  Stolperfallen §4.9–4.11 (Quicksort-Zeiger vs. Pivot; $\Omega(n\log n)$ als untere Schranke;
  Counting-Sort-Zählarray endet nicht bei 0). **Grafischer Quicksort-Trace** ergänzt (Feld
  `4 2 7 1 6 3 8 5`, Pivot 6; linkes Teilfeld `4 2 5 1 3`, Pivot 3 — je „Moment vor dem Tausch").
  Status Kap. 04 → 🟡.
- **2026-07-01:** Kap.-04-Seite ins `INF4_1_Learnings.tex/.pdf` gebaut (Überblickstabelle, Quicksort-
  Rezept + grafischer Trace via `fancyvrb`, Heapsort, untere Schranke + Counting Sort, Klausurtipps,
  Stolperfallen). Paket `fancyvrb` ergänzt. 2× kompiliert → 7 Seiten, fehlerfrei; Trace-Ausrichtung
  (L/R/P unter den Werten) visuell geprüft.
- **2026-07-01:** **Gesamtskript `INF4_1_Gesamtskript_4up.pdf` gebaut** (§3c): alle 12 inhaltlichen
  Decks, 4-up quer, 47 Blätter, 187 Folien. Label „Kapitel – Thema «Nr.»`` je Folie + „Blatt «Nr.»``
  je Blatt. Entfernt: Titel-, Ziele-, „Vielen Dank"-Folien, Animations-Zwischenschritte (moderat) und
  **alle Effizienzüberlegung-Folien** (30 Löschungen inkl. Landau-Historie #11, Dijkstra-Bio, Topol.-
  Beispiel; Effizienz Kap. 02–08). **Konvention:** Effizienz gehört pro Alg. ins Learning-PDF, nicht
  ins Skript (Vergleichstabellen/Traces bleiben). **TODO:** Effizienz Kap. 06+ (BST/B-Bäume) noch ins
  Learning-PDF nachtragen, sobald das Kapitel drankommt.
- **2026-07-08:** Learnings-PDF: **Titelseite (alte Seite 1) entfernt**, dafür Übersichtsseite
  „Algorithmen auf einen Blick`` als neue Seite 1 (kapitelübergreifend). 3-spaltige Tabelle
  (`array`/`L`-Spalten, raggedright) — **Algorithmus · So funktioniert es (anschaulich) · Beispiel
  Schritt für Schritt**; alle 9 bisher behandelten Verfahren (Euklid, Sliding Window, Selection/
  Insertion/Bubble/Merge/Quick/Heap/Counting Sort). **Bewusst keine Komplexitätsspalte** (steht je
  Kapitelseite). Farblegende in die Fußzeile gewandert. Auf Lenas Feedback nachgebessert: Overflow
  („Max-Abschnittssumme``) behoben, Erklärungen anschaulicher, Selection-Sort-Beispiel korrigiert
  (jetzt echtes 2-Pass-Trace statt irreführendem Ein-Swap). 2× kompiliert, 7 Seiten, kein Overfull.
  **TODO:** Zeilen für Kap. 06+ (BST/AVL/B-Baum/Hash/BFS/DFS/Dijkstra/MST) ergänzen, sobald behandelt.
- **2026-07-08:** Zusätzlicher (vorbestehender) Overflow behoben: in der Landau-Symbole-Box (Kap. 02)
  wurde die *Mengenschreibweise*-Tabelle **inline** hinter den Fließtext gesetzt und lief rechts aus
  der Box → jetzt `\par`-Umbruch davor + Spaltenbreite auf Box-Innenmaß (`l L{13.8cm}`, raggedright).
  Alle 7 Seiten visuell auf Überlauf geprüft — sauber.
- **2026-07-08:** **⚠️ Prozessfehler + Regel:** Kap. 06 (Binäre Suchbäume) zuerst aus dem
  Allgemeinwissen „korrigiert", *bevor* ich `06_BinaereSuchbäume.pdf` gelesen hatte → zwei
  Korrekturen waren falsch (Folie 8: ≤ beidseitig, Lenas „links ≤ rechts ≥" war richtig; Löschen
  2 Kinder = Nachfolger aus RECHTEM Teilbaum, nicht Vorgänger links). Auf Lenas Ansage neue
  Arbeitsregel in §1: **immer zuerst den Foliensatz per Read öffnen**, dann bewerten. Auch als
  Memory `feedback_check_slides_first.md` gesichert.
- **2026-07-08:** Kap. 06 durchgearbeitet → §3.4 (BST-Eigenschaft, Inorder/Suchen/Einfügen,
  Löschen 3 Fälle, Komplexität $O(h)$). 2 Stolperfallen §4.12–4.13. **Kap.-06-Seite ins
  `INF4_1_Learnings.tex/.pdf` gebaut** (Def-Boxen, Löschen-Rezept, Lösch-Trace als ASCII-Bäume,
  Komplexitätstabelle inkl. $h=\log n$ vs. $n$ als AVL-Motivation). 2× kompiliert → 9 Seiten,
  Seiten 8–9 visuell geprüft (Bäume ausgerichtet, kein Überlauf). Status Kap. 06 → 🟡. Trace mit
  Lena noch offen.
- **2026-07-08:** Lösch-Traces mit Lena: Nachfolger-Suche saß sofort; 1. Versuch mit
  Wiederanhäng-Fehler (Teilbaum unter das nachrückende Kind gehängt) → Stolperfalle §4.14 +
  Merksatz „Der Nachfolger zieht allein um" in PDF-pitbox; Blitz-Trace danach **fehlerfrei** →
  Kap. 06 ✅. Übersichtsseite: Rubrik „Bäume" mit 2 Zeilen (BST; BST-Löschen 2 Kinder) ergänzt;
  Tabelle dabei auf `longtable` umgestellt (lief nicht mehr auf eine Seite → brach vorher als
  Ganzes um und kollidierte mit der Fußzeile), `\pagebreak` vor der Bäume-Rubrik. → 10 Seiten.
- **2026-07-08:** **Praktikum 4 gesichtet — Achtung: Praktikum 04 = BST (Kap. 06)**, der
  $k{+}1$-Versatz gilt nicht durchgehend (kein Kap.-05-Deck) → Warnhinweis §2b korrigiert.
  Klausurrelevant daraus ins PDF (Kap.-06-Seite): (a) Inorder verrät die Baumform nicht,
  Level-Order schon (tipbox); (b) Entartungs-Beispiel $n{=}8$: search(8) entartet 8 vs.
  balanciert 4 Vergleiche + Rekurrenz-Herleitung $T(n){=}T(n{-}1){+}c \Rightarrow O(n)$ bzw.
  $T(n){=}T(n/2){+}c \Rightarrow O(\log n)$ (Laufzeit-defbox). Übersprungen (kein Programmieren
  in der Klausur): Graphviz, Code-Fragen. **AVL-Löschen-Teil des Praktikums → bei Kap. 07 üben.**
- **2026-07-08:** Entartungs-Drill (4 Fragen aus Praktikum 4) mit Lena: Kette/8 Vergleiche ✓,
  balanciert 4 ✓, Einfügereihenfolge fast (Mittelwert statt **Median** → §4.15); Level-Order +
  Begriff „entartet" konnte sie noch nicht deuten → erklärt (Kette vs. balanciert, Ebenen zählen).
- **2026-07-08:** **Kap. 07 (AVL) durchgearbeitet → ✅.** Lena hat alle Traces fehlerfrei gelöst:
  BFs bestimmen, Einfügen mit einfacher Rotation (LL) und Doppelrotation (50/30/70/60/65),
  Praktikum-4-AVL-Löschen alle 3 Fälle inkl. lösch-ausgelöster Doppelrotation zwei Ebenen über
  der Löschstelle (Teilbaum-Umhänge-Details 6 und 8 korrekt!). Einziger Wackler: „20 als linkes
  Kind der 10`` nach Rechtsrotation (laut Lena Tippfehler) → Merksatz „nach Rotation Inorder-Check``
  in PDF-Tipbox. Fürs Punktbild nachgeschärft: verletzten Knoten + BF + Kriterium (BF des Kindes)
  + End-BFs immer explizit hinschreiben. **Kap.-07-Seite ins Learnings-PDF** (BF-Box mit
  rechts-minus-links-Konvention, Rotations-Mechanik, Entscheidungstabelle, Rezepte Einfügen/Löschen,
  2 Session-Traces, Komplexität) + 2 AVL-Zeilen auf der Übersichtsseite → 12 Seiten, sauber
  kompiliert, Seiten 2/11/12 visuell geprüft.
- **2026-07-09:** **Kap. 08 (B-Bäume) durchgearbeitet → 🟡** (Trace korrekt, aber noch langsam —
  Wiederholungs-Drill vor der Klausur nötig, s. §2b). Abfrage 4/6 (Lücken: Unterlauf-Begriff,
  „Baum wächst wenn alle voll" → nur Wurzel-Split). Lösch-Trace 1. Versuch mit Unterlauf-Fehler
  (→ §4.16), Blitz-Trace fehlerfrei — gleiches Muster wie BST. Praktikum 05 gesichtet
  (klausurrelevant: m-vs-I/O, optimales m für 4-KB-Block = 128). **Kap.-08-Seite ins Learnings-PDF**
  (Struktur-Regeln, Suche, Einfüge-/Lösch-Rezept, Session-Lösch-Trace alle 4 Fälle, Praktikum-Box,
  Tipps/Stolperfallen) + 2 B-Baum-Zeilen auf der Übersichtsseite → 14 Seiten, 2× kompiliert,
  Seiten 2/13/14 visuell geprüft.
- **2026-07-08:** **Höhen-Konvention geklärt** (Lena fragte nach, Check in AVL-Folie 3): Höhe in
  **Knoten-Ebenen, Wurzel zählt mit** — sortierte Folge mit $n$ Elementen ⇒ Höhe $n$. Mein
  ursprüngliches $h=n{-}1$ (CLRS-Kanten-Zählung) war für diesen Kurs **falsch** → in Learnings-PDF
  (Begriffe-Box, Laufzeit-Box, Stolperfalle) und §3.4 auf $h=n$ korrigiert, Konvention explizit in
  die Begriffe-Box aufgenommen. Erneut bestätigt: Folien-Konvention schlägt Lehrbuch-Konvention.
