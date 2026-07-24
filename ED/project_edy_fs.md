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
    ├── 04_zeitveraenderlich.tex ← EDy5: Maxwell, Fortpfl.konst., Skineffekt, R~ ✓
    ├── 05_em_wellen.tex         ← EDy6: EM-Wellen (Wellengl., ebene Welle, Grenzflächen) ✓
    ├── 06_wellenleiter.tex      ← EDy7 komplett: Koax, Hohlleiter (Rechteck/Rund), Resonatoren, Leitungstheorie ✓
    ├── 07_antennen.tex          ← EDy8 komplett: Ersatzschaltbild, Elementardipol, Kenngrößen, Gewinn, Dipol, Gruppenantennen, EMV ✓
    └── 08_rezepte.tex           ← K0/K0b/K1–K5 Klausur-Rezepte als Wenn→Dann-Tabellen, self-contained + Konstanten/Einheiten-Kasten ✓ Stand 2026-07-18 nachm.
```

## Grafiken (TikZ, seit 2026-07-05)
- `ED_FS.tex` lädt jetzt `tikz` (+ arrows.meta, decorations.pathmorphing, calc).
- Helper: `\grafik[opts]{tikz-code}` = kompakte, zentrierte Mini-Grafik (minimaler Platz).
- Stile: `vec`, `fld`, `plus`, `minus`. Merk-/Hervorhebungsbox: `\merkblock[farbe]{Titel}{Formel}`.
- Eingebaute Skizzen: Dipol-Feldlinien (2.1), Platten-+Zylinderkond. (2.4),
  Leiter mit Ring-H-Feld (3.1), bewegter Leiter im B-Feld (3.4.1), H10-Feldbild (7.1).

## Bekannte LaTeX-Fallstricke
- `"` ist in ngerman babel aktiv — niemals ASCII-Anführungszeichen in LaTeX-Code
  verwenden; stattdessen `\glqq...\grqq` oder ganz weglassen
- Deutsche Umlaute in `\text{}` innerhalb von Formelblöcken: ö → oe etc. als Fallback,
  aber UTF-8 mit inputenc funktioniert normalerweise; Probleme entstehen nur durch `"`

## Status (Stand 2026-07-18 nachmittags) — ALLE KAPITEL FERTIG ✓ + Rezeptseiten im Wenn→Dann-Layout
| Datei | Status |
|-------|--------|
| ED_FS.tex | fertig, kompiliert ✓ (**11 Seiten** Stand 2026-07-24, 0 Overfull, TikZ aktiv, EDy0–EDy8 komplett + Rezeptseiten K0–K5 mit 4 Skizzen; Seitenaufteilung der Rezepte: S. 8 K0/K0b, S. 9 K1, S. 10 K2+K3, S. 11 K4+K5) |
| 08_rezepte.tex | fertig ✓, **komplett neu strukturiert (2026-07-18 nachmittags)**: zweispaltige Wenn→Dann-Tabellen (`rezepttab`-Umgebung, `\wenn`/`\dann`/`\rzhl` lokal in der Datei definiert) statt 3-Spalten-Blöcke — linke Spalte = Klausur-Fragestellung kursiv, rechte Spalte = ALLE nötigen Formeln (self-contained, keine Verweise auf 7.x/8.x mehr nötig). Neu: K0b Konstanten & Einheiten (c0, Z_F0, ε0, μ0, κ_Ag/Cu/Messing, Ergebnis-Einheiten Np/m·rad/m·W/m² etc., 1 Np = 8,686 dB, dBm-Formel). In K1–K5 zusätzlich eingebaut: Z_L-Formel + α_L/α_D (7.1), Wanddämpfungs-3-Schritt + Z_FH (7.4), senkrechter Einfall q=1 (6.7), allg. Trafo-Formel (7.8), C_HW (8.6) + Gruppenfaktor √G_Gr/u (8.7) |
| 00_einteilung.tex | fertig, kompiliert ✓ |
| 01_elektrostatik.tex | fertig ✓ (2.1–2.7) + Grafiken |
| 02_magnetfeld.tex | fertig ✓ (3.1–3.7) + Grafiken |
| 03_stroemungsfeld.tex | fertig ✓ (4.1–4.7) |
| 04_zeitveraenderlich.tex | fertig ✓ (5.1 Maxwell [Klausur!], 5.2 Fortpfl.konst. γ, 5.3 Skineffekt/δ, 5.4 R~ + innere Induktivität) |
| 05_em_wellen.tex | fertig ✓ (6.1 Wellengl./Helmholtz, 6.2 γ/α/β, 6.3 v/λ/Dispersion, 6.4 Z_F/Poynting, 6.5 Polarisation, 6.6 Metall-Stehwelle, 6.7 Dielektr. r/t, 6.8 Brechung/Totalrefl./Brewster) |
| 06_wellenleiter.tex | fertig ✓ komplett EDy7 (7.1 Koax, 7.2 Hohlleiter-Grundl., 7.3 Rechteck Hmn/Emn, 7.4 H10+Leistung, 7.5 Rundhohlleiter/Bessel, 7.6 Resonatoren+EMV, 7.7 Telegrafengl., 7.8 λ/4-Trafo+Reflexionsfaktor) |
| 07_antennen.tex | fertig ✓ komplett EDy8 (8.1 Ersatzschaltbild/η, 8.2 Elementardipol/Nah-Fernfeld, 8.3 Richtcharakteristik C/D, 8.4 Gewinn dBi/dBd, 8.5 Wirkfläche/leff/RS, 8.6 Dipol λ/2·Ganzwelle·λ/4, 8.7 Gruppenantennen/Phased Array/Yagi, 8.8 EMV-Abstrahlung) |

## Klausur-Kernformel Hohlleiter H10 (übertragene Leistung)
`P = a·b·E0² / (4·Z_FH) = a·b·E0²/(4·Z_F0)·√(1−(λ/2a)²)` mit `λc=2a`,
`Z_FH = Z_F0/√(1−(λ/λc)²)`, `Z_F0≈377 Ω`. War **nicht** in der Referenz-FS
`ED/Formelsammlung Elektrodynamik.pdf` → in 06_wellenleiter.tex ergänzt.
