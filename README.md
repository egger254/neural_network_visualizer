# Neuronales Netz – Trainingsvisualisierung

Interaktive, **rein simulierte** Visualisierung, wie ein kleines neuronales Netz (3 Input-, 3 Hidden-, 2 Output-Knoten) während des Trainings seine Gewichte anpasst. Gewichte werden als „Steine“ auf den Verbindungen dargestellt.

## Starten

`index.html` im Browser öffnen – kein Build, keine Abhängigkeiten, läuft offline.

## Funktionen

- **Steine = Gewichte:** grün = positiv, rot = negativ, Anzahl (0–3) = Stärke. Steine liegen mittig auf der Linie nahe am Startknoten (Form aus `stone_green.svg`, 16 px). Nach jeder Epoche werden Steine animiert weggenommen / hinzugefügt.
- **Labels:** zwei frei wählbare Klassennamen (o1 / o2).
- **Trainingsbilder:** Upload per Dateiauswahl oder Drag & Drop, eingebaute Beispielbilder; jedem Bild wird eines der beiden Labels zugeordnet.
- **Ablauf pro Bild:** Bild anlegen → Vorwärtsdurchlauf → Vorhersage → Bewertung (richtig/falsch). Die simulierte Trefferquote steigt über die Epochen von ca. 40 % auf ca. 95 %.
- **Wahrscheinlichkeitsbalken** unter dem Trainingsbild zeigen die Ausgabe des Netzes je Label; Vorhersage hervorgehoben, nach der Bewertung grün (richtig) bzw. rot (falsch).
- **Statusliste & Fortschritt:** Ergebnis je Bild (wird pro Epoche zurückgesetzt), Fortschrittsbalken der abgeschlossenen Epochen, Genauigkeit.
- **Steuerung:** Start/Pause/Reset, Geschwindigkeit 0,25×–4×, 1–50 Epochen, Schritt-Modus mit wählbarer Schrittgröße (Phase / Bild / Epoche). Tastatur: Leertaste, →.
- Während des Trainings sind Labels und Bilder gesperrt; Reset entsperrt.

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
10. **Events & Start**
