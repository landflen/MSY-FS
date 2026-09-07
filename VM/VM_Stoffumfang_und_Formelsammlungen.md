# VM — Stoffumfang und die drei fremden Formelsammlungen

> Bestandsaufnahme vom 01.08.2026. Grundlage: die drei aus dem Kommiliton:innen-Chat
> stammenden Formelsammlungen in `Formelsammlungen_fremd/`.
>
> ⚠️ **Überholt seit 07.09.2026:** Skript und Übungsaufgaben liegen inzwischen vor
> (→ [`VM_Lernmaterial.md`](VM_Lernmaterial.md)). Die Frage „was gehört zum Stoff?" beantwortet
> jetzt das Skript selbst. Diese Datei bleibt als **Bewertung der drei fremden Formelsammlungen**
> nützlich — für die Frage, welche davon sich als Vorlage für die eigenen 10 Seiten eignet.

## Warum das wichtig ist

Die Klausur SoSe 2026 (→ [`VM_Klausur_SoSe2026.md`](VM_Klausur_SoSe2026.md)) zeigt, was *in einem
Jahr* abgefragt wurde. Die Formelsammlungen zeigen, was **insgesamt zum Stoff gehört** — und das
ist deutlich mehr. Alles, was hier steht und 2026 nicht drankam, ist ein Kandidat für dein Jahr.

**Der Modulaufbau ist über die Jahre stabil und zweigeteilt:**

| Teil | Inhalt | Anteil in der Klausur SoSe 2026 |
|---|---|---|
| **A** | Lineare Algebra, DGL-Systeme, Systemtheorie | 45 von 90 Punkten |
| **B** | Wahrscheinlichkeitsrechnung, Statistik, Markov-Ketten | 45 von 90 Punkten |

Die Toni-Sammlung von 2023 ist genau so geteilt (zwei getrennte Dateien) — die 50/50-Aufteilung
der Klausur ist also kein Zufall des Jahrgangs 2026, sondern die Struktur des Moduls.

## Die drei Sammlungen im Vergleich

| Datei | Umfang | Stand | Deckt ab |
|---|---|---|---|
| `VM_Formelsammlung_MayPa_2025.pdf` | **10 Seiten** | 2025 | **Teil B komplett**, folgt der Skriptgliederung (1.4.1 usw.) |
| `VM_TeilA_LinAlg_DGL_Toni_2023.pdf` | 6 Seiten | 03.07.2023 | Teil A komplett |
| `VM_TeilB_Stochastik_Toni_2023.pdf` | 6 Seiten | 06.07.2023 | Teil B Grundlagen bis Normalverteilung |

**Bewertung:**

- **MayPa 2025 ist der beste Startpunkt.** Genau **10 Seiten** — exakt das erlaubte Limit
  („Selbstgefertigte Arbeitsunterlagen, 10 Seiten DIN A4") — sie ist also schon auf die
  Klausurregel zugeschnitten. Sie folgt der **Nummerierung des aktuellen Skripts** (1.4.1
  Zufallsvariablen …), was mit den Abschnittsnummern aus Boliks Klausurvorbereitung
  zusammenpasst, und enthält genau die Punkte, die er zum Anstreichen genannt hat: **Satz von
  Steiner, Ungleichung von Tschebyscheff, Quantile**. Sie reicht bis Markov-Ketten,
  Konfidenzintervalle, Hypothesentests und χ²-Anpassungstest.
  ⚠️ Sie deckt **nur Teil B** ab („VM Stoch" in der Kopfzeile) — für die 45 Punkte aus Teil A
  brauchst du zusätzlich Toni A.
- **Toni 2023 A** ist die einzige Quelle für den Analysis-/LinAlg-Teil und **inhaltlich breiter
  als die Klausur 2026** (siehe Stoffliste unten).
- **Toni 2023 B** ist gegenüber MayPa redundant und hört früher auf (endet bei der
  Normalverteilung, keine induktive Statistik, keine Markov-Ketten). Nur als Zweitmeinung nutzen.

> **Rechenaufgabe fürs Limit:** MayPa (10) + Toni A (6) = 16 Seiten, erlaubt sind **10**.
> Du wirst also kürzen müssen — genau die Übung, die du bei ED und MDT5/2 schon gemacht hast.
> Der Kürzungsmaßstab von dort gilt: **was zu keinem Aufgabentyp gehört, fliegt raus.**

## Stoffliste Teil A (aus Toni 2023)

- Linear/nichtlinear, zeitvariant/zeitinvariant — Definitionen und Erkennungsmerkmale
  (Nichtlinearität versteckt in f, Addition einer Konstanten, Kennlinien; Zeitvarianz durch
  Multiplikation mit f(t))
- **DGL n-ter Ordnung → DGL-System 1. Ordnung → Zustandsraumdarstellung** (Begleitmatrix)
- Eigenwerte und Eigenvektoren, charakteristisches Polynom, algebraische Vielfachheit
- **Gerschgorin-Kreise** — Lage der Eigenwerte ohne Berechnung *(kam 2026 nicht dran)*
- **Routh-Hurwitz-Kriterium** *(kam 2026 nicht dran — Überschneidung mit SOS Teil A!)*
- **Diagonalisierbarkeit und Jordan-Normalform**, Hauptvektoren, Darstellungsformen
  *(2026 kam nur der diagonalisierbare Fall — der Jordan-Fall ist offen)*
- Berechnung von e^(At)
- Lösung von DGL-Systemen:
  - **zeitvariabel**: Transitionsmatrix Φ(t;t₀), Fundamentalmatrix, Variation der Konstanten
    *(kam 2026 nicht dran)*
  - **zeitinvariant**: über Matrixexponentialfunktion (geht immer) oder über EW/EV (nur bei
    Diagonalisierbarkeit) — genau die Wahl aus Klausuraufgabe 1b
  - homogene + spezielle Lösung, Anfangsbedingungen einsetzen
- **Ruhelagen, Linearisierung um die Ruhelage, Stabilität**: alle EW mit negativem Realteil →
  asymptotisch stabil; Re(λ)=0 → stabil, falls algebraische = geometrische Vielfachheit;
  Analyse der Jacobi-Matrix mit Routh-Hurwitz

> ⚠️ **Auffällig:** Die Laplace-Transformation — mit 19 Punkten die größte Aufgabe 2026 —
> steht in Toni A **nicht** drin. Entweder war sie 2023 nicht im Stoff, oder die Sammlung ist
> dort unvollständig.
> **Erledigt seit 07.09.2026:** Laplace steht in Abschnitt 1.6 des DGL-Skripts (inkl.
> Verschiebungs- und Faltungssatz), und das Tabellenblatt aus dem Klausursatz liegt als
> `Tabellen_VM.pdf` bzw. am Ende von `VM_Probeklausur.pdf` vor — **nur 9 Korrespondenzen**.

## Stoffliste Teil B (aus MayPa 2025 + Toni 2023)

- Axiome von Kolmogoroff, Rechenregeln, Additionssatz
- **Bedingte Wahrscheinlichkeit**, Baumdiagramm, Vierfeldertafel, stochastische Unabhängigkeit,
  **totale Wahrscheinlichkeit und Satz von Bayes** → Klausuraufgabe 4
- Zufallsvariablen, Verteilungsfunktion, Dichtefunktion, Momente
- **Erwartungswert, Varianz, Standardabweichung, Satz von Steiner**
- **Ungleichung von Tschebyscheff** (bei unbekannter Verteilung)
- Diskrete Verteilungen: Gleichverteilung, Bernoulli/**Binomial**, **Poisson**, geometrisch
  → Klausuraufgabe 5
- Stetige Zufallsvariablen: Dichte, Verteilungsfunktion, **Transformation einer ZV**, Quantile,
  Median
- **Normalverteilung**, kσ-Intervalle, Rechnen mit Φ, Quantile der Standardnormalverteilung
- **Zentraler Grenzwertsatz**
- **Konfidenzintervalle** *(2026 nicht dran, von Bolik aber als „interessant" markiert)*
- **Hypothesentests** *(2026 nicht dran)*
- **χ²-Anpassungstest** *(2026 nicht dran, obwohl als „sehr wahrscheinlich" angekündigt)*
- **Markov-Ketten**: Übergangsmatrix, stationäre Verteilung, Ergodensatz → Klausuraufgabe 6

## Was du daraus baust

1. **Eigene Formelsammlung, 10 Seiten**, aus MayPa (Teil B) + Toni A (Teil A), gekürzt auf das,
   was zu einem Aufgabentyp gehört. Vorlage für die Gliederung: die sechs Rezepte aus
   `VM_Klausur_SoSe2026.md`.
2. ~~**Die Lücke Laplace** selbst füllen — aus Papula und der Klausuraufgabe 2.~~ → erledigt:
   Skript-Abschnitt 1.6 plus `Partialbruchzerlegung.pdf`. Auf die eigenen 10 Seiten gehören die
   **Sätze** (Ableitung, Verschiebung, Faltung) — die 9 Korrespondenzen liegen in der Klausur bei.
3. **Teil A doppelt verwerten:** Ruhelagen, Linearisierung, Jacobi, Stabilität, Routh und
   Lyapunov stehen fast identisch in `SOS/Teil_A/SOS_A_FS/`. Wenn du VM und SOS im selben
   Semester schreibst, ist das derselbe Lernblock — und deine SOS-Formelsammlung ist dafür
   bereits fertig.
