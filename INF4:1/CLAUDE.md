# INF4:1 — Klausurvorbereitung (Algorithmen & Datenstrukturen)

> **Zweck dieser Datei:** Lebendiges Lern-Logbuch. Nach **jeder** Erkenntnis, die für
> die Klausurvorbereitung wichtig ist, wird diese Datei aktualisiert — sei es
> *was* zu lernen ist, *wie* ich (Claude) antworten soll, oder *wie* ich beim
> Lernen helfe. Immer mit Datum im Änderungslog unten.

---

## 0. Zeitplan & Deadline

**🎯 PRÜFUNG: 13. Juli 2026, 11:00–12:30 Uhr.** (Heute: 29.06.2026 → noch 2 Wochen)

Geplante Lern-Sessions (Themen an Foliennummern gekoppelt):

| Datum | Inhalt | Dauer |
|-------|--------|-------|
| 29.06. (heute) | Kap. 1–3: Grundlagen, **Effizienz**, elem. Sortieren | 15:30–17:30 |
| 30.06. | INF4/1 (Vorlesung/Praktikum, wiederkehrend) | 14:00–17:15 |
| 01.07. | Kap. 4 + 6: fortg. Sortieren, binäre Suchbäume | 12:45–14:45 |
| 03.07. | Kap. 7–8: AVL-, B-Bäume | 13:15–15:15 |
| 06.07. | Kap. 9–10: Hashtabellen, Graphen | 08:15–10:15 |
| 08.07. | Kap. 11–12 + 15: kurze Wege, aufsp. Bäume, Komplexität | 08:15–10:15 |
| 09.07. | Praktika 01–11 durchsehen | 08:15–10:15 |
| 10.07. | **Probeklausur** rechnen + Schwachstellen nacharbeiten | 08:15–12:00 |
| 12.07. | Last-Minute-Recap | 16:00–17:30 |
| 13.07. | finaler Blick → **Prüfung** | 08:30 → 11:00 |

> **Konsequenz für die Arbeitsweise:** Heute Schwerpunkt Kap. 1–3. Tempo ist eng — pro
> Session das jeweilige Kapitel sichern (Spickzettel + Abfrage), Stolperfallen sofort in §4
> notieren, damit am 10./12.07. gezielt nachgearbeitet werden kann.

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

### Bewährter Lern-Workflow pro Kapitel (von Lena vorgeschlagen, lernpsychologisch validiert)
1. Lena liest den Foliensatz und schreibt **aus dem Gedächtnis**, was hängenblieb.
2. Claude **ergänzt/korrigiert** und liefert kompakten Spickzettel.
3. Lena sieht das zugehörige **Praktikum** an → gemeinsam Klausurrelevanz bestimmen
   (Programmier-Details niedrig gewichten).
4. Lena bearbeitet das Wichtigste grob.
5. Claude stellt **klausurähnliche Aufgaben** (analog, nicht identisch).
6. Bei Schwächen: Recap + mehr Aufgaben; sonst nächstes Kapitel.

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

## 3b. Lieferbares Artefakt

`INF4_1_Learnings.tex` → `INF4_1_Learnings.pdf`: lesbare Lern-Zusammenfassung, **eine Seite
pro Foliensatz** (Def-/Tipp-/Stolperfallen-Boxen). **Bewusst KEIN Formelsammlungs-Layout**
(nicht die 3-spaltige FS der rechtlichen Module). Nach jedem Kapitel um eine Seite erweitern
(`\clearpage` + `\kapitel{}{}`) und neu kompilieren (`pdflatex`, 2×).

## 2b. Themenliste (aus dem Ordner)

Reihenfolge = Foliennummerierung. Status: ⬜ offen · 🟡 angefangen · ✅ sitzt

| Nr | Thema | Status | Notiz |
|----|-------|--------|-------|
| 01 | Allgemeines | 🟡 | von Lena gelernt + abgefragt (29.06.); 2 Schwachstellen offen → §4 |
| 02 | Effizienz / Big-O | 🟡 | von Lena gelesen + Recap (29.06.); O/Ω-Verwechslung korrigiert → §4. Praktikum 02 noch offen |
| 03 | Elementares Sortieren | ⬜ | |
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

## 5. Offene Fragen / noch klären

- Erlaubte Hilfsmittel (Formelsammlung/Spickzettel erlaubt)?
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
