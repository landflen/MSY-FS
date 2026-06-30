# Klausur-Leitfaden für Claude — Android-Programmierung (Kotlin, Android Studio)

> **Fach:** WPF Android-Programmierung 202efi · Prof. Dr. Thomas Mahr
> **Format:** **90 Min**, eigener Laptop, **Internet erlaubt**, schriftliche Unterlagen erlaubt
> **Sprache/Stack:** Kotlin + Android Studio. Abgabe per USB-Stick.
> **Wichtig:** Die Klausur darf **nicht fotografiert/hochgeladen** werden → die Aufgabe muss **abgetippt** an Claude übergeben werden (siehe §1).
> Dieses Dokument sagt Claude, **worauf er achten muss**, **was wichtig ist** und **was er besser nicht macht**.

---

## 0. Das Wichtigste in einem Satz

> **Trenne den Simulationskern (reines Kotlin, ohne Android-Imports) strikt von der GUI.**
> Dann läuft die App *und* die Unit-Tests sind auf der JVM ausführbar — das ist die halbe Klausur.

---

## 1. Klausur-Aufbau (Erwartung)

| Teil | Inhalt | Worauf es ankommt |
|------|--------|-------------------|
| **A** | App nach Anforderungen bauen (wie Beispiel: 2 Welten, Teilchen, Portale) | **Kompiliert, läuft, stürzt nicht ab.** Jede Anforderung sichtbar erfüllt. |
| **B** | 3–5 eigene **Qualitätsanforderungen** als Markdown + **Unit-Tests** dazu | Anforderungen testbar formuliert, Tests verweisen auf IDs, **doppelt so viele** Tests wie Anforderungen, alle **grün**. |

### 1.1 Die Aufgabe an Claude übergeben (Abschreiben — kritischer Schritt!)

Die Klausur darf **nicht fotografiert/hochgeladen** werden → du musst die Aufgabe **abtippen**. Bei 90 Minuten ist das verlorene Zeit, also effizient machen:

**Empfohlenes Vorgehen — „erst Anforderungen, dann Bild, dann bauen":**

1. **Tippe ALLE funktionalen Anforderungen am Stück ab** (nicht Stück für Stück). Grund: Claude muss die Architektur (Sim-Kern, Datenmodell, Rotation) von Anfang an auf das *gesamte* Bild auslegen. Tippt man häppchenweise, baut Claude evtl. um, sobald Anforderung 12 (Rotation) kommt → Zeitverlust.
2. **Tippe die allgemeinen Anforderungen mit** (Package-Name `de.NAME.wise25`, „darf nicht abstürzen", Punktevergabe). Die Punkte verraten die **Gewichtung** → Claude priorisiert richtig.
3. **Beschreibe die Abbildung in Worten** statt sie hochzuladen. Eine knappe Bildbeschreibung reicht völlig (siehe Vorlage unten). Tippe **nicht** ab, was schon im Text steht — nur was das Bild *zusätzlich* zeigt (Layout-Anordnung, Position des Portals, Beschriftungs-Format).
4. **Lass dann erst bauen.** Bitte Claude, die Anforderungen vorher kurz **als Checkliste zurückzuspiegeln** — so siehst du Abtipp-/Verständnisfehler, bevor Code entsteht.

**Abkürzungen beim Tippen (spart Zeit, Claude versteht es trotzdem):**
- Stichpunkte statt ganzer Sätze: `2 SurfaceViews = 2 Welten, Teilchen bewegen sich, prallen am Rand ab`.
- Punktzahlen in Klammern dranhängen: `Teleport durch Portal in andere Welt, gleiche rel. Position (5P)`.
- Zahlenwerte exakt übernehmen (3 Teilchen, Farben, Textformate wörtlich) — hier **nicht** kürzen.

**Vorlage für die Bildbeschreibung (anpassen):**
```
Screenshot zeigt Portrait-Layout, von oben nach unten:
- TextView "Welt 1: 3 Teilchen"
- großes hellrotes Rechteck (Welt 1) mit dunkelroten Punkten;
  links mittig senkrechtes cyanfarbenes Portal, beschriftet "Portal 1"
- TextView "Welt 2: 3 Teilchen"
- großes hellblaues Rechteck (Welt 2) mit dunkelblauen Punkten;
  rechts mittig senkrechtes cyan Portal "Portal 2"
- TextView "Gesamt-Schritte: 0" (mittig)
Im Querformat: beide Welten nebeneinander, Textfelder jeweils darüber.
```

**Was du NICHT abtippen musst:** Deckblatt, Korrektur-Tabellen, USB-Hinweise, Prüferdaten — irrelevant für den Code.

---

## 2. Harte Rahmenbedingungen (NICHT verletzen)

### Verboten — niemals verwenden
- ❌ Kein **TensorFlow / ML**, kein **SQL / Room / SQLite**, keine **Kamera**, kein **Mikrofon**, keine **Sockets**, kein **Bluetooth**, **NFC**.
- ⚠️ Internet ist erlaubt, **neue Gradle-Dependencies kosten aber Zeit** (Download/Sync) und bergen Build-Risiko. Bei 90 Min: nur einbinden, wenn wirklich nötig — Standard-Android/Kotlin reicht für die Aufgabe.

### Pflicht
- ✅ Package-Verzeichnis exakt nach Vorgabe: **`de.NAME.wise25`** (NAME = eindeutige Kennung der Studentin).
- ✅ Programm **kompilierbar + ausführbar**, **darf nicht abstürzen**.
- ✅ **Mehrere Activities**, **Grafik**, **Animation** (Anforderung an die App).
- ✅ **Clean Architecture / Clean Code** + **Unit-Tests für die Logik**.

### Erlaubt / Standard
- ✅ `SurfaceView` **oder** die `GrafikView` aus der Vorlesung für das Rendering.
- ✅ `onSaveInstanceState` / `ViewModel` für Zustandserhalt.
- ✅ JUnit (lokale Unit-Tests unter `src/test/`, **nicht** instrumentiert unter `androidTest/`).

---

## 3. Architektur — so aufsetzen, dass Tests funktionieren

**Goldene Regel: Simulationslogik enthält KEINEN einzigen `android.*`-Import.**

```
de.NAME.wise25
├── sim/                  ← reines Kotlin, JVM-testbar, KEIN Android
│   ├── Particle.kt       data class (x, y, vx, vy, world)
│   ├── World.kt          Grenzen, Farbe, Portal, Teilchenliste
│   ├── Portal.kt         Position/Rechteck, enthält(p)
│   └── Simulation.kt     step(): bewegen, abprallen, teleportieren
├── ui/                   ← Android: Activities, Views
│   ├── MainActivity.kt
│   └── WorldView.kt      SurfaceView, zeichnet sim-Zustand
└── (Tests in src/test/java/de/NAME/wise25/sim/)
```

**Warum:** Die Klausur verlangt Tests auf dem **Simulationskern, unabhängig von der GUI**. Liegt die Physik im `SurfaceView` oder in der `Activity`, sind die Tests nur instrumentiert lauffähig → langsam, fragil, oft „rot". Reine Kotlin-Klassen testet JUnit in Millisekunden grün.

**Konkret heißt das:**
- `Simulation.step(dt)` verändert nur Datenobjekte — gibt z. B. neue Positionen zurück.
- Kollision/Abprallen, Portal-Teleport, Teilchen-Erzeugung: alles als **pure functions / deterministisch testbare Methoden**.
- Für Zufall (`random Position/Geschwindigkeit`): **injizierbarer `Random`-Seed**, damit Tests deterministisch sind. (`Simulation(random = Random(42))`)

---

## 4. Teil A — typische Anforderungen & Fallstricke (Beispiel: Teilchen-Welten)

Aus der Beispielklausur ergeben sich diese Punkte. Bei einer anderen Aufgabe sinngemäß übertragen.

| # | Anforderung | Achtung / Stolperstein |
|---|-------------|------------------------|
| Layout | TextView, View, TextView, View, TextView **gestapelt** (Portrait) | Reihenfolge exakt einhalten. |
| Physik | Teilchen bewegen sich, **prallen an Rändern ab** | vx/vy Vorzeichen umkehren bei Randkontakt. |
| Start | je Welt **3 Teilchen**, zufällige Position + Geschwindigkeit | Seed injizierbar (s. o.). |
| Farben | Welt 1 hellrot/dunkelrot, Welt 2 hellblau/dunkelblau | Konstanten zentral definieren. |
| Portal | cyan, senkrecht beschriftet „Portal 1/2" | Beschriftung gedreht zeichnen. |
| **Teleport** | Teilchen betritt Portal → andere Welt, **gleiche relative Position** | relative Koordinaten (0–1) umrechnen, **Welt-/Farbzugehörigkeit wechselt mit**. |
| Klick | Klick in Welt → neues Teilchen dort, Farbe der Welt | `onTouchEvent` → Koordinaten in Sim-Koordinaten mappen. |
| Anzeige | „Welt X: Y Teilchen" über jeder Welt | Format **exakt** wie gefordert. |
| Schritte | Simulationsschritt-Zähler mittig unter Welt 2 | Zähler im Sim-Kern hochzählen. |
| **Rotation** | Querformat → Welten **nebeneinander** | separates Layout `layout-land/`. |
| **Identität** | Beim Kippen: **Farbe + Geschwindigkeit bleiben**, relative Position darf sich ändern | **`onSaveInstanceState` oder `ViewModel`** — sonst gehen Teilchen verloren = Punktverlust. |

**Häufigste Fehler, die Claude vermeiden muss:**
1. **State geht beim Drehen verloren** → Zustand in `ViewModel` halten (überlebt Config-Change automatisch) **oder** Teilchen in `onSaveInstanceState` serialisieren (`Parcelable`/Bundle).
2. **App stürzt ab** (NPE, IndexOutOfBounds beim Iterieren+Mutieren der Teilchenliste) → über Kopie iterieren oder Iterator-sicher arbeiten.
3. **Animation-Loop blockiert UI-Thread** → eigener Render-/Game-Thread beim `SurfaceView`, sauber in `surfaceDestroyed` beenden.
4. **Textformat weicht ab** → Bewertung erfolgt wörtlich, exakt „Welt X: Y Teilchen" / „Gesamt-Schritte: N".
5. **Teleport vergisst Farbwechsel** → Teilchen muss in Zielwelt deren Farbe annehmen.

---

## 5. Teil B — Qualitätsanforderungen + Unit-Tests

### 5.1 Anforderungen formulieren (Regeln S.34–36)

Jede Anforderung braucht: **ID · Prozesswort · eindeutig · testbar · einzeln**.

**Gute Anforderung (Vorlage):**
```
QA-01: Beim Abprallen an einer Wand kehrt die Simulation
       die entsprechende Geschwindigkeitskomponente des
       Teilchens vorzeichenverkehrt um.
```
- **Identifizierbar:** ID `QA-01` → Test kann darauf verweisen.
- **Nachweisbar/testbar:** prüfbarer Ein-/Ausgang.
- **Eindeutig:** keine schwammigen Wörter.
- **Einzeln:** genau eine Aussage pro Satz.
- **Klar:** aktiver, kurzer Satz.

**Regeln aus der Vorlesung (S. 34–36):**
- ✅ **Prozesswort** verwenden (zeigt, erzeugt, teleportiert, zählt, kehrt um …).
- ❌ Keine schwammigen Begriffe: „benutzerfreundlich", „einfach", „fast immer korrekt", „schnell".
- ❌ **Keine Ausnahmen** („außer…", „es sei denn…").
- ❌ **Nicht mischen** — funktionale Anforderungen getrennt von Randbedingungen; **eine** Aussage pro Satz.
- ✅ **Realistisch** (technisch machbar) und **explizit** (nichts implizit voraussetzen).
- ⚠️ Teil B verlangt Anforderungen an die **Simulationslogik, NICHT an die GUI** → also über Teilchenverhalten, Teleport, Zähler, Abprallen — nicht über Buttons/Farben/Layout.

**Schlecht → Gut Beispiele:**
| Schlecht | Gut |
|----------|-----|
| „Die Simulation soll zuverlässig sein." | „QA-02: `Simulation.step()` erhöht den Schrittzähler bei jedem Aufruf um genau 1." |
| „Teilchen verhalten sich korrekt und schnell." | „QA-03: Ein Teilchen, das die Portalfläche betritt, wechselt in die andere Welt." |

### 5.2 Unit-Tests

- **Anzahl:** mindestens **doppelt so viele Tests wie Anforderungen** (3–5 Anforderungen → 6–10+ Tests).
- **Jeder Test verweist auf eine ID** — im Testnamen und/oder Kommentar:
  ```kotlin
  @Test
  fun `QA-01 abprallen kehrt vx um`() { ... }
  ```
- **Nur auf dem Simulationskern**, GUI-unabhängig → unter `src/test/`, läuft auf JVM.
- **Alle Tests müssen grün** sein, wenn sie ausgeführt werden — vor Abgabe einmal komplett laufen lassen.
- **Deterministisch** halten: festen `Random`-Seed injizieren, keine Zeit-/Thread-Abhängigkeit.

Beispiel:
```kotlin
// Testet QA-01
@Test fun `QA-01 teilchen prallt an rechter wand ab`() {
    val sim = Simulation(random = Random(1))
    val p = Particle(x = 99.0, y = 50.0, vx = 5.0, vy = 0.0, world = 1)
    sim.step(p, worldWidth = 100.0, worldHeight = 100.0)
    assertTrue(p.vx < 0)   // Geschwindigkeit umgekehrt
}
```

---

## 6. Workflow während der Klausur (Claudes Verhalten)

1. **Erst lesen, dann bauen:** alle Anforderungen durchnummerieren, abhaken.
2. **Package zuerst** korrekt anlegen: `de.NAME.wise25`.
3. **Sim-Kern vor GUI** bauen — und sofort Tests dazu.
4. **Inkrementell + nach jedem Schritt testen** (User-Vorgabe): kompilieren → laufen lassen → weiter. Nie 10 Features auf einmal ohne Build.
5. **Möglichst keine neuen Dependencies** — Internet ist zwar da, aber Sync/Download frisst von den 90 Min. Standard-Android/Kotlin nutzen.
6. **Robustheit vor Eleganz:** lieber simpel und absturzfrei als clever und fragil. Null-Checks, leere Listen, Division durch 0 abfangen.
7. **Vor Abgabe:** komplett kompilieren, App starten, drehen, klicken, **alle Unit-Tests grün**.

### Abgabe-Checkliste (USB)
- [ ] Stick **vor** Prüfung getestet, danach **geleert**.
- [ ] Komplettes Projekt nach Ende auf Stick **kopiert**.
- [ ] Stick raus, wieder rein, Projekt **lokal nochmal gespeichert und getestet** (Kopie wirklich vollständig + lauffähig).
- [ ] Package korrekt, kompiliert, läuft, Tests grün.

---

## 7. Was Claude NICHT tun soll — Kurzliste

- ❌ Physik/Logik in `Activity` oder `SurfaceView` schreiben (→ untestbar).
- ❌ Unnötige Bibliotheken einbinden — Sync/Download kostet Klausurzeit.
- ❌ Verbotene APIs (TensorFlow, SQL, Kamera, Mikro, Socket, Bluetooth, NFC).
- ❌ Schwammige Qualitätsanforderungen ohne ID/Prozesswort.
- ❌ Zu wenige Tests (< 2× Anforderungen) oder Tests, die GUI brauchen.
- ❌ Nicht-deterministische Tests (echter Zufall, Threads, Zeit).
- ❌ Großen Wurf ohne Zwischen-Builds — immer schrittweise testen.
- ❌ Textformate frei interpretieren — wörtlich übernehmen.
- ❌ Zustand beim Geräte-Drehen verlieren.
```
