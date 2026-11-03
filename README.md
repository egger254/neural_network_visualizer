# Neuronales Netz – Trainingsvisualisierung

Interaktive, **rein simulierte** Visualisierung, wie ein kleines neuronales Netz (3 Input-, 3 Hidden-, 2 Output-Knoten) während des Trainings seine Gewichte anpasst. Gewichte werden als „Steine“ auf den Verbindungen dargestellt.

## Starten

`index.html` im Browser öffnen – kein Build, keine Abhängigkeiten, läuft offline.

## Funktionen

- **Steine = Gewichte:** grün = positiv, rot = negativ, Anzahl (0–3) = Stärke. Steine liegen mittig auf der Linie nahe am Startknoten (Form aus `stone_green.svg`, 16 px). Nach jeder Epoche werden Steine animiert weggenommen / hinzugefügt; Plaketten (z. B. „+2 🟢“, „−2 🔴 +1 🟢“) zeigen die Änderung, weggenommene Steine bleiben als gestrichelte Geistersteine bis zur nächsten Epoche sichtbar.
- **Start-Gewichte:** pro Verbindung festlegen, wie die Steine zu Beginn liegen; Reset stellt genau diese wieder her.
- **Ziel-Gewichte:** pro Verbindung vorgeben, wie die Steine am Ende liegen sollen (−3 rot … +3 grün). Das Training nähert sich dem Ziel und endet exakt darauf.
- **Labels:** zwei frei wählbare Klassennamen (o1 / o2).
- **Trainingsbilder:** Upload per Dateiauswahl oder Drag & Drop, eingebaute Beispielbilder; jedem Bild wird eines der beiden Labels zugeordnet.
- **Ablauf pro Bild:** Bild anlegen → Vorwärtsdurchlauf → Vorhersage → Bewertung (richtig/falsch). Die simulierte Trefferquote steigt über die Epochen von ca. 40 % auf ca. 95 %.
- **Wahrscheinlichkeitsbalken** unter dem Trainingsbild zeigen die Ausgabe des Netzes je Label; Vorhersage hervorgehoben, nach der Bewertung grün (richtig) bzw. rot (falsch).
- **Kacheln & Fortschritt** (unter dem Netz): je Bild Nummer, ✓/✗, Vorhersage-Balken (Klassenfarbe, Länge = Sicherheit) und Plakette mit echtem Label; Zurücksetzen pro Epoche. Klassenfarben: Lavender / #EFE9AE. Bilder werden immer vollständig (nicht beschnitten) angezeigt.
- **Steuerung:** Start/Pause/Reset, Geschwindigkeit 0,25×–4×, 1–50 Epochen, Schritt-Modus mit wählbarer Schrittgröße (Phase / Bild / Epoche). Tastatur: Leertaste, →.
- **Screenshot** (Steuerung): Netz ohne Trainingsbild / Netz / Netz mit Trainingsbildern / Netz mit Trainingsbildern und Fortschrittsbalken – als PNG speichern oder in die Zwischenablage kopieren.
- **Video** (Schritt-Modus, „ein Bild“): nächsten Schritt als MP4 (H.264, 30 fps, bis Full HD) speichern – Bild für Bild berechnet, daher ruckelfrei. Kopieren von Videos erlauben Browser nicht.
- Während des Trainings sind Labels, Bilder und Ziel-Gewichte gesperrt; Reset entsperrt.

## Code-Aufbau (`index.html`)

Das Script ist in nummerierte Abschnitte gegliedert:

1. **Konfiguration** – Knoten, Verbindungen, Steinformen, Phasen, Dauern
2. **Zustand** – zentrales `state`-Objekt
3. **Hilfsfunktionen** – u. a. `tween()` (berücksichtigt Geschwindigkeit, Pause, Abbruch)
4. **Simulation** – Gewichte, Trefferquote, Vorhersagen (keine echte Berechnung)
5. **Rendering – Netz** – SVG-Aufbau, Steine, Signale
6. **Rendering – Panels** – Phasenleiste, Statusliste, Fortschritt, Steuerung, Bildliste
7. **Trainingsablauf** – Phasen-Funktionen und `runTraining()`
8. **Steuerung** – Start, Pause, Schritt, Reset
9. **Inputs** – Upload und Beispielbilder
10. **Screenshot** – Netz-SVG als Bild, Kacheln/Fortschritt per Canvas
11. **Video** – WebCodecs-H.264-Encoder und kleiner MP4-Muxer
12. **Events & Start**
