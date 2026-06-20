# Prompt-Template: LaTeX Formelsammlung

Kopiere diesen Prompt in ein neues Gespräch. Ersetze die Platzhalter in `[...]`.

---

```
Erstelle eine kompakte LaTeX-Formelsammlung für [FACHNAME].
Quelldokumente: [z.B. "01_signale.pdf, 02_systeme.pdf, 03_filter.pdf"]

## Vorlage – Präambel (exakt so übernehmen)

\documentclass[a4paper,10pt]{article}
\usepackage[utf8]{inputenc}
\usepackage[T1]{fontenc}
\usepackage[ngerman]{babel}
\usepackage{amsmath,amssymb,mathtools}
\usepackage{xcolor}
\usepackage{geometry}
\usepackage{array,multirow,microtype,needspace}
\geometry{top=10mm,bottom=14mm,left=10mm,right=10mm,includefoot}
\setlength{\parskip}{0pt}
\setlength{\parindent}{0pt}
\renewcommand{\baselinestretch}{0.9}
\setlength{\emergencystretch}{2em}
\hfuzz=3pt
\setlength{\fboxsep}{0.18em}
\setlength{\fboxrule}{0.3pt}

% Eine Farbe pro Kapitel – nach Bedarf erweitern:
\colorlet{c01}{blue}
\colorlet{c02}{teal}
\colorlet{c03}{violet}
\colorlet{c04}{orange!90!red}

\newcommand{\bereich}[2][c01]{%
  \needspace{4\baselineskip}%
  \vspace{0.5em}%
  \noindent\colorbox{#1!10}{%
    \makebox[\dimexpr\linewidth-2\fboxsep\relax][l]{%
      \small\bfseries\color{#1!80!black}\strut\enspace #2}}%
  \nopagebreak\vspace{0.1em}\par\noindent}

\newcommand{\bereichende}{%
  \vspace{0.2em}{\color{gray!50}\hrule height 0.3pt}\vspace{0.2em}}

\newenvironment{formelreihe}{%
  \noindent\footnotesize\setlength{\tabcolsep}{0pt}%
  \renewcommand{\arraystretch}{0.85}%
  \begin{tabular}{@{}p{0.32\linewidth}@{\hspace{0.02\linewidth}}%
                     p{0.32\linewidth}@{\hspace{0.02\linewidth}}%
                     p{0.32\linewidth}@{}}}%
{\end{tabular}\par}

\newcommand{\formelblock}[2]{%
  \parbox[t]{\linewidth}{%
    {\scriptsize\scshape\color{gray!65!black} #1}\\[0.03em]%
    $\displaystyle #2$}}

\newcommand{\beispielblock}[2]{%
  \fcolorbox{orange!50}{yellow!15}{%
    \parbox[t]{\dimexpr\linewidth-2\fboxsep-2\fboxrule\relax}{%
      {\scriptsize\scshape\color{orange!80!black} Bsp: #1}\\[0.03em]%
      $\displaystyle #2$}}}

\newcommand{\infoblock}[1]{%
  \parbox[t]{\linewidth}{\scriptsize\itshape #1}}


## Layout-Regeln (STRIKT einhalten)

**3-Spalten-Layout (formelreihe-Umgebung):**
- Spalte 1 & 2: \formelblock, \infoblock, oder \parbox[t] mit gestapelten Formeln
- Spalte 3: AUSSCHLIESSLICH \beispielblock — niemals Formeln oder infoblocks

**Keine Lücken zwischen zusammengehörigen Inhalten:**
- Zusammengehörige Formeln IMMER in EINE gemeinsame \parbox[t]{\linewidth}{...} packen
- Trennabstand innerhalb einer parbox:  \\[0.25em]%   (% am Ende nicht vergessen!)
- Label zu Formel direkt darunter:      \\[0.03em]%
- Zwischen thematisch verschiedenen Zeilen: \\[0.3em]
- Wenn eine Spalte kürzer ist als die Nachbarspalten → Inhalt in dieselbe parbox packen,
  NICHT als separate Tabellenzeile

**Abschnittsköpfe:**
- \bereich[cXX]{Titel} zu Beginn, \bereichende nach jedem Abschnitt
- \needspace im \bereich-Befehl verhindert, dass ein Titel allein am Seitenende steht

**\formelblock / \beispielblock wrappen #2 automatisch in $\displaystyle...$:**
- Kein extra $...$ um den Formel-Inhalt — sonst doppeltes $$ und Compilefehler

**Mehrzeilige Formeln innerhalb eines \formelblock:**
- \begin{aligned}...\end{aligned} verwenden (NICHT equation oder align)
- Beispiel: \formelblock{Label}{\begin{aligned} a &= b \\ c &= d \end{aligned}}

**Kompakte Mathematik (Breite im Blick behalten):**
- \tfrac statt \dfrac — spart vertikalen Platz ohne Lesbarkeit zu opfern
- \textstyle\sum_{...}^{...} statt \sum für kompakte Summen
- \begin{bsmallmatrix}...\end{bsmallmatrix} für kleine Matrizen (aus mathtools)

**Mathematische Grundregeln (optional, am Anfang):**
- Für sehr kompakte Grundregeln darf ein einfaches tabular mit | verwendet werden
  (mehr als 3 Spalten erlaubt, kein formelreihe nötig)


## Vollständigkeit

Gehe jedes Quelldokument Kapitel für Kapitel durch.
Stelle sicher, dass ALLE Formeln, Definitionen, Eigenschaften und Sonderfälle enthalten sind.
Melde explizit, wenn ein Kapitel abgeschlossen ist, und frage ob mit dem nächsten fortgefahren werden soll.


## Dateistruktur

Lege pro Kapitel eine eigene Datei an:
  parts/01_[thema].tex
  parts/02_[thema].tex
  ...

Binde sie in der Hauptdatei ein:
  \input{parts/01_[thema]}
  \input{parts/02_[thema]}


## Abschluss nach jedem Kapitel

Kompiliere mit:
  pdflatex -interaction=nonstopmode [HAUPTDATEI].tex

Prüfe anschließend die Log-Datei:
  grep "^!" [HAUPTDATEI].log          # → muss leer sein (keine Fehler)
  grep -c "Overfull" [HAUPTDATEI].log # → sollte 0 sein

Prüfe visuell im PDF:
- Keine Lücken zwischen zusammengehörigen Formeln
- Keine Overfull hboxes (außer < 3pt, die werden durch hfuzz=3pt unterdrückt)
- Seitenzahlen vollständig sichtbar (geometry mit includefoot)
- Kein Abschnittstitel allein am Seitenende
```
