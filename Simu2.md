<!--

author:   <your name>
email:    <your name>
version:  0.1.0
language: EN
narrator: US English Female Female

import: https://raw.githubusercontent.com/liaTemplates/AVR8js/main/README.md

-->

# Simulation

## Working simulation

<div id="matrix-experiment">
<wokwi-neopixel-matrix pin="6" cols="12" rows="1"></wokwi-neopixel-matrix>
<span id="simulation-time"></span>
</div>

```cpp             Automata
#include <Adafruit_NeoPixel.h>

#define PIN 6 // Pin, an dem der Datenpin des LED-Streifens angeschlossen ist
#define NUMPIXELS 12 // Anzahl der LEDs im Streifen

Adafruit_NeoPixel strip = Adafruit_NeoPixel(NUMPIXELS, PIN, NEO_GRB + NEO_KHZ800);

// Herzmuster Simulation
float heartPattern[NUMPIXELS];

void setup() {
  strip.begin();
  strip.show(); // Initialisieren Sie alle Pixel auf 'aus'
  generateHeartPattern(); // Herzmuster generieren
}

void loop() {
  static int offset = 0; // Position des Herzmusters
  displayHeartPattern(offset); // Zeige das Herzmuster an
  offset = (offset - 1 + NUMPIXELS) % NUMPIXELS; // Verschiebe das Muster nach links und setze es zurück, wenn es das Ende erreicht
  delay(200); // Warte kurz, um das Muster sichtbar zu machen
}

// Funktion zur Generierung eines Herzmusters (Sinuskurve)
void generateHeartPattern() {
  for (int i = 0; i < NUMPIXELS; i++) {
    heartPattern[i] = (sin(i * (PI / 6.0)) + 1) * 127.5; // Werte zwischen 0 und 255
  }
}

// Funktion zur Anzeige des Herzmusters mit Verschiebung
void displayHeartPattern(int offset) {
  for (int i = 0; i < NUMPIXELS; i++) {
    int index = (i + offset) % NUMPIXELS; // Berechne den Index mit Verschiebung
    int brightness = (int)heartPattern[index];
    strip.setPixelColor(i, strip.Color(brightness, 0, 0)); // Setzt die Farbe der LEDs auf rot mit variabler Helligkeit
  }
  strip.show();
}
```
@AVR8js.sketch(matrix-experiment)
