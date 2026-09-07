# VM — Lernmaterial-Inventar (Stand 07.09.2026)

> **Die zentrale Lücke ist geschlossen.** Bis 01.08.2026 fehlten *Skript und Übungsaufgaben* —
> beides liegt jetzt vor. Damit ist VM zum ersten Mal vollständig lernbar.
> Quelle: Moodle-Kurs **https://e-learn.inventiones.de/course/view.php?id=29** (Login nötig).

## Was neu dazugekommen ist

| Datei | Umfang | Inhalt |
|---|---|---|
| `M_SY_Dgl_Skript.pdf` | **81 S.** | „Dynamische Systeme für M-SY", Bolik, Stand 31.07.2026 — **Teil A** |
| `M_SY_Stoch_Skript.pdf` | **87 S.** | „Stochastik für M-SY", Bolik, Stand 31.07.2026 — **Teil B** |
| `VM_Probeklausur.pdf` | 14 S. | vollständige Probeklausur, 6 Aufgaben, **84 Punkte**, 90 min |
| `VM_Probeklausur_loesungen.pdf` | 14 S. | zugehörige **Musterlösung** |
| `Tabellen_VM.pdf` | 3 S. | die **Tabellenblätter aus dem Klausursatz** (s. u.) |
| `Partialbruchzerlegung.pdf` | 2 S. | Zusatzblatt zur PBZ (braucht man in Aufgabe 2) |

**Die Übungsaufgaben stecken in den Skripten**, nicht in separaten Blättern:

| Ort | Abschnitt | Anzahl |
|---|---|---|
| DGL-Skript S. 46–52 | 1.8 Übungsaufgaben: Gewöhnliche DGL | **21** |
| DGL-Skript S. 77–81 | 2.5 Übungsaufgaben: Stabilität der Lösungen | **7** |
| Stoch-Skript S. 39–45 | 1.6 Übungsblatt 1 (Wahrscheinlichkeitstheorie) | **22** |
| Stoch-Skript S. 67–72 | 2.3 Übungsblatt 2 (Induktive Statistik) | **15** |
| Stoch-Skript S. 82–87 | 3.3 Übungsblatt 3 (Markov-Ketten) | **6** |
| | **Summe** | **71 Aufgaben** |

⚠️ **Zu diesen 71 Aufgaben gibt es keine Lösungen.** Der einzige durchgerechnete Satz ist die
Probeklausur. Das ist der wichtigste Unterschied zu MDT5/2 und ED, wo Musterlösungen vorlagen —
Rechenwege müssen hier selbst verifiziert werden.

## Gliederung der beiden Skripte

**Teil A — `M_SY_Dgl_Skript.pdf` (81 S.)**

1. Gewöhnliche Differentialgleichungen — 1. Ordnung · n-ter Ordnung (homogen/inhomogen, konst.
   Koeffizienten) · **Eigenwerte, Diagonalisierbarkeit, Abschätzung der EW (Gerschgorin)** ·
   DGL-Systeme 1. Ordnung · Variation der Konstanten · **Fourier- und Laplace-Transformation** ·
   zeitinvariante lineare Systeme (**Zustandsraum, Übertragungsfunktion**)
2. Stabilität — lineare Systeme · Systeme 1. Ordnung · **Methode von Ljapunov** · periodische
   Lösungen autonomer Systeme

**Teil B — `M_SY_Stoch_Skript.pdf` (87 S.)**

1. Grundlagen — Wahrscheinlichkeitsbegriff · Kombinatorik · **bedingte W., Unabhängigkeit** ·
   Zufallsvariablen und Kenngrößen · **Binomial · Hypergeometrisch · Poisson · Normal ·
   Exponential · χ² · t · F** · Grenzwertsätze
2. Induktive Statistik — Parameterschätzung · **Maximum-Likelihood** · **Konfidenzintervalle** ·
   **Hypothesentests** (Normalverteilung, Anteilswert) · **χ²-Anpassungstest**
3. Stochastische Prozesse — **Markov-Ketten** zeitdiskret und zeitstetig

Damit sind die beiden bisherigen Lücken aus `VM_Stoffumfang_und_Formelsammlungen.md` gefüllt:
**Laplace steht im Skript (Abschnitt 1.6, inkl. Verschiebungssatz und Faltungssatz)** — dafür
war bisher keine Vorlage vorhanden. **Jordan-Normalform und Gerschgorin** stehen ebenfalls drin.

## Der wichtigste Einzelbefund: die Laplace-Tabelle hat nur 9 Zeilen

Die Klausur SoSe 2026 schrieb in der 19-Punkte-Aufgabe vor, *ausschließlich* die Korrespondenzen
des beigefügten Tabellenblatts zu verwenden. Dieses Blatt liegt jetzt vor
(`Tabellen_VM.pdf` bzw. die letzten Seiten der Probeklausur) — und es enthält **genau neun**
Korrespondenzen:

| Nr. | F(s) | f(t) |
|---|---|---|
| 1 | 1/s | H(t) |
| 2 | 1/(s+a) | e^(−at) |
| 3 | 1/s² | t |
| 4 | 1/(s+a)² | t·e^(−at) |
| 5 | 1/(s(s+a)) | (1/a)(1 − e^(−at)) |
| 6 | a/(s²+a²) | sin(at) |
| 7 | s/(s²+a²) | cos(at) |
| 8 | a/(s²−a²) | sinh(at) |
| 9 | s/(s²−a²) | cosh(at) |

**Konsequenz:** Jede Rücktransformation muss über PBZ auf diese neun Formen gebracht werden —
deshalb liegt `Partialbruchzerlegung.pdf` dabei, und deshalb steht in der Aufgabenstellung
„Verwenden Sie … eine Partialbruchzerlegung". Sätze wie Ableitungs-, Verschiebungs- und
Faltungssatz stehen **nicht** auf dem Blatt → die gehören auf die eigenen 10 Seiten.

Die drei Tabellenblätter sind: **Φ(x) der Standardnormalverteilung**, **Quantile u_γ**,
**Quantile χ²_(n;γ)**. Die Laplace-Tabelle kommt im Probeklausur-Satz als viertes Blatt dazu.
→ Normalverteilungs- und χ²-Tabellen musst du **nicht** auf deine 10 Seiten schreiben.

## Probeklausur vs. echte Klausur SoSe 2026

| # | Probeklausur (84 P) | echte Klausur SoSe 2026 (90 P) |
|---|---|---|
| 1 | homogenes DGL-System, AWP (13) | Eigenwerte, Diagonalisierung, DGL-System (11) |
| 2 | **Übertragungsfunktion + Sprungantwort** RLC, PBZ (15) | Laplace eines DGL-Systems, PBZ + Faltung (19) |
| 3 | math. Pendel: System 1. O., Gleichgewichtspunkte, **Linearisierung**, EW (14) | nichtlineare DGL, Jacobi, **Lyapunov** (15) |
| 4 | **Normalverteilung**, Summe/Mittelwert, ZGS (13) | Bayes / totale W. (12) |
| 5 | **χ²-Anpassungstest + Anteilswerttest** (15) | Poisson + Binomial (18) |
| 6 | Markov: Irreduzibilität, 2 Schritte, **stationäre Verteilung** (14) | Markov: Übergangsmatrix, stationäre Verteilung (15) |

**Die Struktur ist identisch** — sechs Aufgaben, exakt hälftig A/B, gleiche Reihenfolge der
Themenblöcke (DGL-System → Laplace → nichtlineare DGL/Stabilität → Verteilung → Test/Verteilung →
Markov). Nur die *Füllung* der Stochastik-Hälfte unterscheidet sich. Zusammen decken die beiden
Sätze die Stochastik-Hälfte damit doppelt so breit ab: Normalverteilung + χ²-Test + Anteilswert
(Probe) **und** Bayes + Poisson/Binomial (echt).

> Die Einschätzung aus dem Chat, die Probeklausur „bilde das Niveau nicht ab", bleibt als Warnung
> stehen — sie taugt aber unverändert als **Aufgabentyp-Landkarte**, und mehr wird von ihr auch
> nicht gebraucht. Zur Belastbarkeit dieser Kritik siehe den Abschnitt weiter unten.

## Prüfung der Chat-Behauptung „das Material bereitet nicht auf die Klausur vor"

Am 07.09.2026 gegen die Original-Klausur SoSe 2026 geprüft. **Die Behauptung ist so nicht
haltbar — die Klausur besteht in Teil A aus wörtlichen Übungsaufgaben.**

### Zwei wörtliche Treffer

| Klausur SoSe 2026 | Übungsaufgabe | Übereinstimmung |
|---|---|---|
| **Aufgabe 2, 19 P** — x′−3x−3y = t, y′+x+y = 1, x(0)=y(0)=0 | **DGL-Skript 1.8, Aufgabe 21** | **identisch**, bis hin zum Hinweis „Führen Sie die Partialbruchzerlegung für sX(s) und sY(s) durch und verwenden Sie dann den Faltungssatz" |
| **Aufgabe 3, 15 P** — m·x″ = −a·x′|x′| − (bx + cx³) | **DGL-Skript 2.5, Aufgabe 7** | **identisch**, alle vier Teilaufgaben a)–d) in derselben Reihenfolge, dieselbe vorgegebene Lyapunov-Funktion V = ½mx₂² + ½bx₁² + ¼cx₁⁴ |

Dazu: **Probeklausur Aufgabe 2** (RLC-Schaltung, R = 1, L = 0,5, C = 0,4) ist **Übungsaufgabe 19**
im Wortlaut. Und Klausuraufgabe 1 (Diagonalisierung + DGL-System) ist der Typ der Übungen 2, 5
und 8. **Teil A der Klausur — 45 von 90 Punkten — ist damit komplett durch Übungsaufgaben
abgedeckt, 34 Punkte davon wörtlich.**

⚠️ **Vorbehalt zur Datierung:** Das Skript-PDF ist vom **31.07.2026**, die Klausur war am
**10.07.2026**. Es lässt sich nicht ausschließen, dass Bolik die Aufgaben 21 und 2.5/7
*nachträglich* eingepflegt hat. Dagegen spricht aber die Probeklausur vom **02.07.2026**
(also vor der Prüfung): sie enthält Übungsaufgabe 19 unverändert. **Er verwendet Übungs- und
Prüfungsaufgaben nachweislich identisch.** Und für die Vorbereitung ist es ohnehin gleichgültig:
Die Aufgaben stehen jetzt im Skript.

### Teil B, Stochastik: gut abgedeckt, mit einer Lücke

| Klausuraufgabe | passende Übungen | Bewertung |
|---|---|---|
| 4 — Bayes (12 P) | Übungsblatt 1, Aufgabe 7 (Taxi-Zeugen-Problem) | gleiches Rezept, andere Einkleidung ✅ |
| 5 — Poisson + Binomial (18 P) | Übungsblatt 1, Aufgaben 15–18, 21 | **sehr gut**; Aufg. 17 ist genau der Typ „μ bzw. Vorrat so bestimmen, dass P ≥ Schranke" aus 5a ✅ |
| 6 — Markov (15 P) | Übungsblatt 3, Aufgaben 1, 2, 5, 6 | stationäre Verteilung, Irreduzibilität, Periodizität ✅ — **aber kein einziges Beispiel, in dem eine Übergangsmatrix aus Prozentangaben eines Fließtextes aufgestellt wird** ❌ |

**Die Lücke bei Markov ist die teuerste im ganzen Bestand**, weil genau dieser Schritt in der
Klausur 5 Punkte kostete und ohne Folgefehler-Gutschrift die Teile b) und c) mitreißt. Die
Übungen 1 und 3 (Betrunkener, Würfel) sind Textaufgaben, aber mit *gleichverteilten* Übergängen —
das „40 % von (3) nach (2)"-Ablesen wird nirgends geübt. **Diesen Typ selbst konstruieren.**

### Was an der Kritik trotzdem stimmt

1. **Zu den 71 Übungsaufgaben gibt es keine Lösungen.** Man kann üben, aber nicht feststellen,
   ob man es kann. Vermutlich ist das der eigentliche Kern der Chat-Aussage.
2. **Ein Teil der Übungen ist Klausur-untypisch theoretisch**: „Zeigen Sie, dass (Xₙ) eine
   Markov-Kette ist", die Übergangsmatrix mit allgemeinem n, Dichtetransformationen,
   Interpolationspolynom für exp(A). Solche Aufgaben kamen nie dran — wer die 71 Aufgaben stur
   von vorne durchrechnet, verbrennt Zeit. **Nach Typen sortieren, nicht nach Nummern.**
3. **Die Übungen bilden die Randbedingungen nicht ab**: 90 Minuten für 6 Aufgaben, laut Bericht
   eine halbe Seite Platz für die 19-Punkte-Aufgabe, kein Folgefehler. Eine Aufgabe „können"
   und sie in 15 Minuten fehlerfrei hinschreiben sind hier zwei verschiedene Dinge — und genau
   das ist die Erfahrung, die im Chat wahrscheinlich als „bereitet nicht vor" formuliert wurde.

**Konsequenz für den Lernplan:** Das Material *reicht* — der Engpass ist nicht die Abdeckung,
sondern (a) die fehlende Korrekturinstanz und (b) das Tempo. Beides adressiert man mit derselben
Maßnahme: **Aufgaben unter Zeitnahme rechnen und die Rechnung selbst gegenprüfen**
(Zeilensummen bei Markov, Einsetzprobe bei DGL, Poisson-gegen-Binomial-Vergleich).

## Aufgabentypen für den Lernplan

Nach Lehre Nr. 3 und 6 aus dem Root-`CLAUDE.md` muss **jeder Typ mindestens einmal vollständig
gerechnet** sein, bevor irgendetwas vertieft wird. Aus beiden Klausursätzen ergeben sich:

**Teil A**
- A1 Eigenwerte, Diagonalisierung, e^(At), homogenes System mit AWP
- A2 Laplace: transformieren → auflösen → **PBZ** → 9-Zeilen-Tabelle → Rücktransformation
- A3 Übertragungsfunktion und Sprungantwort einer Schaltung (RLC)
- A4 Nichtlineare DGL → System 1. Ordnung → Gleichgewichtspunkte → Linearisierung/Jacobi → EW
- A5 **Lyapunov-Funktion** (deckungsgleich mit SOS Teil A)
- *(offen, im Skript, in keiner der beiden Klausuren: Jordan-Normalform, Gerschgorin,
  Variation der Konstanten, Fourier-Transformation)*

**Teil B**
- B1 Bedingte W., totale W., **Bayes**
- B2 Diskrete Verteilungen: **Binomial, Poisson** (Hypergeometrisch im Skript)
- B3 **Normalverteilung**, Summen und Mittelwerte, ZGS
- B4 **χ²-Anpassungstest** und **Anteilswerttest**
- B5 **Markov-Ketten**: Irreduzibilität, Periodizität, n-Schritt-W., stationäre Verteilung
- *(offen: Maximum-Likelihood, Konfidenzintervalle, Exponential-/t-/F-Verteilung)*

## Der Lernplan liegt in Ambly

Projekt **VM**, aufgebaut wie der SOS-Plan: vier Abschnitte, in „Aufgabentypen (Phase 1)" je eine
Aufgabe pro Typ mit den konkreten Übungs- und Klausurquellen als **Unteraufgaben** (13 Typen,
76 Unteraufgaben). Ohne Datum — die Reihenfolge steuert die Priorität:

- **P1 (zuerst):** A2 Laplace · A5 Lyapunov · B2 diskrete Verteilungen · B5 Markov —
  die vier teuersten Aufgaben (19 + 15 + 18 + 15 P).
- **P2:** A3 Übertragungsfunktion · A4 nichtlineare DGL · B1 Bayes · B3 Normalverteilung ·
  B4 χ²-Test.
- **P3/P4:** A1, A6, B6 und die Reserve A7 (Jordan, Gerschgorin, Fourier).

Regel aus Lehre 3 und 6 des Root-`CLAUDE.md`: **erst jeder Typ einmal ganz, dann vertiefen.**
Phase 2 (die beiden Klausursätze unter Zeit) beginnt erst, wenn Phase 1 einmal durch ist.

## Nächste Schritte

1. Probeklausur **ohne** Lösung rechnen, dann gegen `VM_Probeklausur_loesungen.pdf` korrigieren —
   das ist die einzige selbstkorrigierbare Übung im Bestand und ergibt den ersten Punktestand.
2. Die 71 Skript-Aufgaben nach den obigen Typen sortieren; pro Typ zuerst *eine* rechnen.
3. **Den fehlenden Typ selbst bauen:** eine Markov-Aufgabe, bei der die Übergangsmatrix aus
   Prozentangaben im Fließtext abgelesen werden muss — die einzige echte Lücke der Übungen.
4. Eigene **10-Seiten-Unterlage** bauen (MayPa Teil B + Toni A + Laplace-Sätze aus Skript 1.6);
   Normalverteilungs- und χ²-Tabelle **weglassen**, die liegen bei.
5. **Boliks eigenes Lehrbuch** ist jetzt identifiziert (stand im Literaturverzeichnis des
   Stochastik-Skripts): *J. Bolik, „Angewandte Statistik — Eine Einführung für technische
   Studiengänge", Kohlhammer, 2019.* Laut Chat standen zwei Klausuraufgaben so darin.
   Über die Hochschulbibliothek besorgen.
