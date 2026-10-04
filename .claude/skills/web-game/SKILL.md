---
name: web-game
description: Konventionen für kleine Browser-Spiele in reinem HTML/CSS/JavaScript mit <canvas> und ohne externe Abhängigkeiten. Immer verwenden, wenn der Nutzer ein Web-Spiel, Browser-Spiel oder Canvas-Spiel bauen oder erweitern will (z. B. Snake, Pong, Breakout, Flappy-Klon) — auch wenn er "Skill" oder "Canvas" nicht erwähnt. Nicht für Spiele mit Server, Frameworks oder Build-Tools.
---

# Web-Spiel mit Canvas (Vanilla JS)

Ziel: ein kleines Spiel, das Einsteiger:innen per Doppelklick auf `index.html` öffnen und verstehen können. Deshalb gilt: so wenig bewegliche Teile wie möglich.

## Dateistruktur

Genau drei Dateien im Projektordner, keine Unterordner:

```
index.html   – Gerüst: <canvas>, Score-Anzeige, Verweis auf CSS und JS
style.css    – Layout und Farben
game.js      – gesamte Spiellogik
```

Keine Bibliotheken, Frameworks, CDN-Links, npm oder Build-Schritte. Das Spiel muss offline und ohne Server laufen. Grund: Jede Abhängigkeit ist etwas, das bei Einsteiger:innen kaputtgehen kann und das sie nicht überblicken.

## Aufbau von `game.js`

Halte die Datei in dieser Reihenfolge, mit kurzen deutschen Abschnitts-Kommentaren:

1. **Konstanten** – Canvas-Größe, Rastergröße, Geschwindigkeit (keine "magischen Zahlen" im Code)
2. **Zustand** – ein Objekt `state` mit Position, Score, `gameOver`
3. **Eingabe** – `keydown`-Listener, der nur den Zustand ändert
4. **`update()`** – Logik pro Schritt, zeichnet nichts
5. **`draw()`** – zeichnet den aktuellen Zustand, ändert nichts
6. **`loop()`** – ruft `update()` und `draw()` auf und plant sich mit `requestAnimationFrame` neu
7. **`reset()`** – setzt den Zustand für einen Neustart zurück

Update und Draw zu trennen macht Fehler leichter auffindbar: Stimmt die Anzeige nicht, liegt es an `draw()`; verhält sich das Spiel falsch, an `update()`.

## Canvas-Konventionen

- `const ctx = canvas.getContext("2d");` einmal oben holen.
- Pro Frame zuerst `ctx.clearRect(...)` oder den Hintergrund füllen, dann zeichnen.
- Für Rasterspiele (Snake usw.) in Zellen denken (`x * CELL`), nicht in Pixeln.
- Steuerung per Pfeiltasten und zusätzlich WASD; bei Pfeiltasten `event.preventDefault()`, damit die Seite nicht scrollt.
- Geschwindigkeit bei Rasterspielen über ein Zeitintervall steuern (nicht über jeden Frame), damit das Tempo auf allen Bildschirmen gleich ist.

## Spielfluss

Jedes Spiel hat Startzustand, laufendes Spiel und "Game Over" mit sichtbarem Hinweis und Neustart per Leertaste oder Enter. Den Score immer anzeigen (im Canvas oder im HTML-Element darüber).

## Arbeitsweise

- Zuerst eine minimal spielbare Version (Bewegung + Kollision + Score), erst dann Extras wie Highscore oder Schwierigkeitsstufen.
- Nach jeder Änderung kurz sagen, wie man testet (Datei im Browser öffnen, Seite neu laden).
- Kommentare auf Deutsch, kurz, nur wo das *Warum* nicht offensichtlich ist.
