# Prompt: Formelsammlung aus Vorlesungsskript erstellen

## Kontext

Du hilfst beim Aufbau einer kompakten LaTeX-Formelsammlung für eine Ingenieur-/Mathe-Klausur.
Das Ziel ist maximale Informationsdichte auf wenig Platz bei guter Lesbarkeit.

Die Formelsammlung basiert auf einem bestehenden Template (TEMPLATE.tex) mit einem
dreispaltigen Layout: **Spalte 1–2 = Formeln**, **Spalte 3 = Beispiele**.

---

## Deine Aufgabe

Du bekommst ein Vorlesungsskript (PDF-Text oder Beschreibung) für ein neues Kapitel.
Erstelle daraus eine kompakte `parts/XX_kapitelname.tex`-Datei.

---

## Verfügbare Makros

### `\bereich[Farbe]{Titel}`
Farbiger Abschnittsbalken. Jedes thematische Unterkapitel bekommt einen eigenen Abschnitt.
```latex
\bereich[cKap1]{Wahrscheinlichkeiten}
```
Verfügbare Farben (in TEMPLATE.tex definiert): `cKap1`, `cKap2`, `cKap3`, `cKap4`

---

### `\bereichende`
Dünne Trennlinie nach einer `formelreihe`. Immer nach `\end{formelreihe}` setzen.

---

### `formelreihe` (Umgebung)
Drei-Spalten-Block. Zeilen mit `&` trennen, mit `\\` oder `\\[0.3em]` abschließen.
```latex
\begin{formelreihe}
  Spalte1 & Spalte2 & Spalte3 \\
  Spalte1 & Spalte2 & Spalte3 \\[0.3em]   % größerer Zeilenabstand
\end{formelreihe}
```
Leere Zelle: einfach leer lassen: `& &` oder `&` am Ende.

---

### `\formelblock{Bezeichnung}{Formel}`
Standardblock für Formeln. Bezeichnung erscheint klein/grau darüber.
```latex
\formelblock{Erwartungswert}{E\{X\} = \int_{-\infty}^{\infty} x\,f_X(x)\,\mathrm{d}x}
```
Für **mehrzeilige Formeln**: `aligned`-Umgebung in Argument 2 verwenden:
```latex
\formelblock{Mehrzeilig}{\begin{aligned}
  \mu &= E\{X\} \\
  \sigma^2 &= E\{X^2\} - \mu^2
\end{aligned}}
```
Für **Interpretationszeilen** unter der Formel (Text nach Formel):
```latex
\formelblock{Kovarianz}{\mathrm{Cov}(X,Y) = E\{(X-\mu_X)(Y-\mu_Y)\}\\[0.1em]
  {>}0\text{: steigen zusammen}\\
  {<}0\text{: gegenläufig}}
```

---

### `\beispielblock{Kontext}{Inhalt}`
Orangefarben hervorgehobener Block — **immer in Spalte 3** (rechte Spalte).
```latex
\beispielblock{Würfelwurf}{P(X=3) = \tfrac{1}{6}}
```
Für **Zeilenumbruch** in Inhalt: `aligned` verwenden:
```latex
\beispielblock{Glücksrad}{%
  \begin{aligned}
    \mu_X &= \pi \\
    \sigma_X^2 &= \tfrac{\pi^2}{3}
  \end{aligned}}
```

---

### `\infoblock{Text}`
Kursiver Erklärungstext — **in Spalte 1**, wenn eine Formel Kontext braucht.
Unterstützt `\\` für Zeilenumbrüche.
```latex
\infoblock{$X:\Omega\to\mathbb{R}$ ordnet jedem Ergebnis\\eine reelle Zahl zu.}
```

---

## Layout-Regeln

| Spalte | Inhalt |
|--------|--------|
| 1 | Hauptformel, Definition, oder `\infoblock` für Kontext |
| 2 | Verwandte Formel, Variante, oder Folgerung |
| 3 | `\beispielblock` mit konkretem Zahlenbeispiel |

**Wenn Spalte 3 leer ist:** `& \\` am Ende der Zeile.  
**Wenn nur Spalte 1 belegt:** `& & \\`

---

## Inhaltliche Entscheidungen

**Was aufnehmen:**
- Alle Formeln, die direkt in Aufgaben verwendet werden
- Definitionen mit Formel
- Wichtige Sonderformeln (z.B. diskrete vs. stetige Variante einer Formel)
- Zahlreiche Beispiele in Spalte 3 — sie sparen Zeit in der Klausur

**Was weglassen:**
- Herleitungen und Beweise (nur Endergebnis)
- Texterklärungen, die sich aus der Formel selbst ergeben
- Blockdiagramme und Abbildungen
- Triviale Umformungen

**Kompakte Schreibweise:**
- `\tfrac{}{}` statt `\dfrac{}{}` für kleine Brüche in Texten
- `\dfrac{}{}` für wichtige Brüche, die lesbar bleiben müssen
- `\cdot` für Multiplikation bei Unabhängigkeit/Verbund
- `\mathrm{d}x` für Integrationsvariablen
- `E\{X\}` statt `E[X]` (konsistent mit Skript halten)

---

## Dateistruktur

```
TEMPLATE.tex              ← Preamble, Makros, \input-Liste
parts/
  01_kapitel.tex          ← Kapitel 1 (diese Datei)
  02_kapitel.tex          ← Kapitel 2
  ...
```

Neue Kapitel: In `TEMPLATE.tex` mit `\input{parts/XX_name}` einbinden,
Farbe mit `\colorlet{cKapX}{Farbe}` definieren.

---

## Qualitätskontrolle

Nach dem Schreiben prüfen:
1. Kein `\multicolumn` mit `l`-Ausrichtung — führt zu 175pt Overfull
2. Zeilenumbrüche `\\` nur **außerhalb** von `$...$` oder innerhalb von `aligned`
3. Jede `formelreihe` mit `\bereichende` abschließen
4. Kompilieren: `pdflatex -interaction=nonstopmode TEMPLATE.tex`
5. Nur Overfull > 5pt beheben; kleinere sind visuell irrelevant

---

## Beispiel-Output

```latex
\bereich[cKap1]{Wahrscheinlichkeiten}
\begin{formelreihe}
  \infoblock{$\Omega$: Ergebnismenge,\; $E\subseteq\Omega$: Ereignis.} &
  \formelblock{Wahrscheinlichkeit}{P(E)=\dfrac{|E|}{|\Omega|}} &
  \beispielblock{Würfel}{P(\text{gerade})=\tfrac{3}{6}=\tfrac{1}{2}} \\[0.3em]
  \formelblock{Komplement}{P(\bar{E})=1-P(E)} &
  \formelblock{Additivität (disjunkt)}{P(E\cup F)=P(E)+P(F)} &
  \beispielblock{Komplement}{P(X{\le}4)=1-\tfrac{1}{3}=\tfrac{2}{3}} \\
\end{formelreihe}
\bereichende
```
