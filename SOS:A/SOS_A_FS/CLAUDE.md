# Formelsammlung SOS:A — CLAUDE.md

Modul: **Nichtlineare und Stochastische Systeme, Teil A**
Dozent: Prof. Dr. B. Wagner, TH Nürnberg, MSY

## Kompilieren

```bash
cd "/Users/Lena1/Documents/TH Nürnberg/MSY/SOS:A/SOS_A_FS"
pdflatex -interaction=nonstopmode SOS_A_FS.tex
```

Erfolg prüfen: keine Zeilen mit `^!`, `grep -c "Overfull" SOS_A_FS.log` soll 0 sein.

## Dateistruktur

```
SOS_A_FS/
├── SOS_A_FS.tex              ← Hauptdatei (Preamble, \input-Liste)
└── parts/
    ├── 00_grundlagen.tex     ← Teil 0 (Determinanten & Eigenwerte)
    ├── 01_signale_routh.tex  ← Teil 1 (Signale/Systeme) + Teil 2 (Routh)
    ├── 02_zustandsraum_lyapunov.tex  ← Teil 3 (ZR/ÜF) + Teil 4 (NL) + Teil 5 (Lin./Lyapunov)
    ├── 03_kreiskriterium.tex ← Teil 6 (Kreiskriterium)
    └── 04_harmonische_balance.tex    ← Teil 7 (Harmonische Balance) — TODO
```

Skript: `/Users/Lena1/Documents/TH Nürnberg/MSY/SOS:A/SOS_A_Skript.pdf` (154 Seiten)
Referenz-FS: `/Users/Lena1/Documents/TH Nürnberg/MSY/SOS:B/SOS_B_FS/`
Template/Stilregeln: `/Users/Lena1/Documents/TH Nürnberg/MSY/Formelsammlung_Prompt_Template.md`

## Kapitelfarben

| Farbe      | Teil | Inhalt                        |
|------------|------|-------------------------------|
| `cKap0` black!70   | 0 | Mathematische Grundlagen      |
| `cKap1` blue       | 1 | Signale & Systeme             |
| `cKap2` teal       | 2 | Routh-Schema                  |
| `cKap3` violet     | 3 | Zustandsraum & ÜF             |
| `cKap4` orange!90!red | 4 | Nichtlineare Systeme        |
| `cKap5` olive      | 5 | Linearisierung & Lyapunov     |
| `cKap6` purple     | 6 | Kreiskriterium                |
| `cKap7` cyan!70!black | 7 | Harmonische Balance        |

## Custom-Befehle

```latex
\bereich[cKapX]{Titel}          % farbiger Abschnittsheader
\bereichende                    % dünne Trennlinie nach Abschnitt

% Drei-Spalten-Layout (je 0.32\linewidth ≈ 60.8 mm)
\begin{formelreihe} ... \end{formelreihe}

\formelblock{Label}{Formel}     % Formel in $\displaystyle...$
\infoblock{Text}                % kursiver Hinweistext
\beispielblock{Titel}{Inhalt}   % orange Box — NUR Spalte 3!
```

## Kritische Layoutregeln

1. **Spalte 3** ausschließlich `\beispielblock` — niemals `\formelblock` oder `\infoblock`.
2. Zusammengehörige Formeln in einer Zelle → `\parbox[t]{\linewidth}{...}` mit `\\[0.25em]` zwischen den Blöcken.
3. `\formelblock` / `\beispielblock` wrappen `#2` automatisch in `$\displaystyle...` — kein extra `$...$` nötig.
4. Mehrzeilige Formeln in Formelblöcken: `\begin{aligned}...\end{aligned}` verwenden.
5. Breite im Blick behalten: `\tfrac` statt `\dfrac`, `\textstyle\sum` für kompakte Summen, `\begin{bsmallmatrix}` für kleine Matrizen.

## Status

| Datei                         | Status     |
|-------------------------------|------------|
| 00_grundlagen.tex             | fertig, kompiliert ✓ |
| 01_signale_routh.tex          | fertig, kompiliert ✓ |
| 02_zustandsraum_lyapunov.tex  | fertig, kompiliert ✓ |
| 03_kreiskriterium.tex         | fertig, kompiliert ✓ |
| 04_harmonische_balance.tex    | fertig, kompiliert ✓ |
