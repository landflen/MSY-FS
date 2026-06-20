---
name: project-edy-fs
description: Status und Dateipfade der EDy-Formelsammlung (Elektrodynamik, TH Nürnberg MSY)
metadata:
  type: project
---

Formelsammlung Elektrodynamik (EDy) wird aufgebaut.

**Why:** Prüfungsvorbereitung MSY, analog zu SOS:A-FS.

**How to apply:** Kapitel für Kapitel, warten auf Bestätigung vor dem nächsten.

## Zielverzeichnis
`/Users/Lena1/Documents/TH Nürnberg/MSY/ED/ED_FS/`

## Quelldokumente
`/Users/Lena1/Documents/TH Nürnberg/MSY/ED/EDy0.pdf` bis `EDy8.pdf` + `ED/Ergänzung/EDy.pdf`

## Stilreferenz
- Prompt-Template: `/Users/Lena1/Documents/TH Nürnberg/MSY/Formelsammlung_Prompt_Template.md`
- CLAUDE_PROMPT: `/Users/Lena1/Documents/TH Nürnberg/MSY/FS_Template/CLAUDE_PROMPT.md`
- Preamble-Referenz: SOS:A FS (`SOS_A_FS.tex`)

## Kapitelfarben
| cKap | Farbe | Skript | Inhalt |
|------|-------|--------|--------|
| cKap0 | gray!80!black | EDy0 | Übersicht/Einteilung |
| cKap1 | blue | EDy1 | Einteilung EM-Felder |
| cKap2 | teal | EDy2 | Elektrostatisches Feld |
| cKap3 | violet | EDy3 | Magnetisches Feld |
| cKap4 | orange!90!red | EDy4 | Stationäres Strömungsfeld |
| cKap5 | olive | EDy5 | Zeitveränderliches Strömungsfeld |
| cKap6 | purple | EDy6 | Elektromagnetische Wellen |
| cKap7 | cyan!70!black | EDy7 | Wellenleiter |
| cKap8 | red!70!black | EDy8 | Antennen |

## Dateistruktur
```
ED_FS/
├── ED_FS.tex                    ← Hauptdatei
└── parts/
    ├── 00_einteilung.tex        ← EDy0+EDy1: Klassifikation
    ├── 01_elektrostatik.tex     ← EDy2: Elektrostatik (2.1–2.7)
    ├── 02_magnetfeld.tex        ← EDy3: Magnetisches Feld (3.1–3.7) ✓
    ├── 03_stroemungsfeld.tex    ← EDy4: Stationäres Strömungsfeld (4.1–4.7) ✓
    ├── 04_zeitveraenderlich.tex ← EDy5: TODO
    ├── 05_em_wellen.tex         ← EDy6: TODO
    ├── 06_wellenleiter.tex      ← EDy7: TODO
    └── 07_antennen.tex          ← EDy8: TODO
```

## Bekannte LaTeX-Fallstricke
- `"` ist in ngerman babel aktiv — niemals ASCII-Anführungszeichen in LaTeX-Code
  verwenden; stattdessen `\glqq...\grqq` oder ganz weglassen
- Deutsche Umlaute in `\text{}` innerhalb von Formelblöcken: ö → oe etc. als Fallback,
  aber UTF-8 mit inputenc funktioniert normalerweise; Probleme entstehen nur durch `"`

## Status (Stand 2026-06-10)
| Datei | Status |
|-------|--------|
| ED_FS.tex | fertig, kompiliert ✓ |
| 00_einteilung.tex | fertig, kompiliert ✓ |
| 01_elektrostatik.tex | fertig, kompiliert ✓ (2.1–2.7) |
| 02_magnetfeld.tex | fertig, kompiliert ✓ (3.1–3.7) |
| 03_stroemungsfeld.tex | fertig, kompiliert ✓ (4.1–4.7) |
| 04_zeitveraenderlich.tex | ausstehend |
| 05_em_wellen.tex | ausstehend |
| 06_wellenleiter.tex | ausstehend |
| 07_antennen.tex | ausstehend |
