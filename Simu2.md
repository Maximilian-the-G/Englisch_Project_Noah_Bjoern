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
#define NUMPIXELS 30 // Anzahl der LEDs im Streifen

Adafruit_NeoPixel strip = Adafruit_NeoPixel(NUMPIXELS, PIN, NEO_GRB + NEO_KHZ800);

// Herzmuster Simulation
float heartPattern[NUMPIXELS];

void setup() {
  strip.begin();
  strip.show(); // Initialisieren Sie alle Pixel auf 'aus'

  // Herzmuster generieren
  generateHeartPattern();
}

void loop() {
  // Zeige das Herzmuster an
  displayHeartPattern();
  delay(100); // Warte kurz, um das Muster sichtbar zu machen
}

// Funktion zur Generierung eines Herzmusters (Sinuskurve)
void generateHeartPattern() {
  for (int i = 0; i < NUMPIXELS; i++) {
    heartPattern[i] = (sin(i * 0.2) + 1) * 127; // Werte zwischen 0 und 254
  }
}

// Funktion zur Anzeige des Herzmusters
void displayHeartPattern() {
  for (int i = 0; i < NUMPIXELS; i++) {
    int brightness = (int)heartPattern[i];
    strip.setPixelColor(i, strip.Color(brightness, 0, 0)); // Setzt die Farbe der LEDs auf rot mit variabler Helligkeit
  }
  strip.show();
}
```
@AVR8js.sketch(matrix-experiment)
