# INF4:1 — Klausurvorbereitung (Algorithmen & Datenstrukturen)

> **Zweck dieser Datei:** Lebendiges Lern-Logbuch. Nach **jeder** Erkenntnis, die für
> die Klausurvorbereitung wichtig ist, wird diese Datei aktualisiert — sei es
> *was* zu lernen ist, *wie* ich (Claude) antworten soll, oder *wie* ich beim
> Lernen helfe. Immer mit Datum im Änderungslog unten.

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

## 2b. Themenliste (aus dem Ordner)

Reihenfolge = Foliennummerierung. Status: ⬜ offen · 🟡 angefangen · ✅ sitzt

| Nr | Thema | Status | Notiz |
|----|-------|--------|-------|
| 01 | Allgemeines | 🟡 | von Lena gelernt + abgefragt (29.06.); 2 Schwachstellen offen → §4 |
| 02 | Effizienz / Big-O | 🟡 | von Lena gelesen + Recap (29.06.); O/Ω-Verwechslung korrigiert → §4. **Praktikum 01** (= Kap. 02) erledigt |
| 03 | Elementares Sortieren | 🟡 | gelesen + Recap + Praktikum 02 + Übungsblatt (30.06.) → §3.2. Ergebnisse alle richtig; 2 Begründungs-Stolperfallen §4.7–4.8 (Selection-Mechanik, Induktion). Vor Klausur kurz nachhaken |
| 04 | Fortgeschrittenes Sortieren | ⬜ | |
| 06 | Binäre Suchbäume | ⬜ | |
| 07 | AVL-Bäume | ⬜ | |
| 08 | B-Bäume | ⬜ | |
| 09 | Hashtabellen | ⬜ | |
| 10 | Suche in Graphen (BFS/DFS) | ⬜ | |
| 11 | Kürzeste Wege | ⬜ | |
| 12 | Aufspannende Bäume (MST) | ⬜ | |
| 15 | Komplexität (P/NP) | ⬜ | |

Praktika 01–11 als Übungsmaterial / klausurnahe Aufgaben vorhanden.

> **⚠️ Praktikum-Nummerierung ≠ Kapitelnummer!** Die Praktika sind um eins versetzt:
> Praktikum 01 → Kap. 02, Praktikum 02 → Kap. 03 („Debriefing") usw. Nicht verwechseln.

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
