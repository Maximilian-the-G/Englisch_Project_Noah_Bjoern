# Presentation on LED Heartbeat Pattern
![Heart Pattern](https://i.pinimg.com/originals/37/86/07/37860723477ec18ee6a8fc71532e3438.jpg)
## Introduction

Welcome to the presentation on the LED Heart Pattern code.

This project utilizes an LED strip to create a moving heart pattern.
We will cover the origin of the idea, the functionality of the code, how it works, challenges faced, future ideas, present you the code and the execution of it. 

---

## Where Did the Idea Come From?

The idea for this project originated from the desire to create a visually appealing LED display that simulates the rhythmic pulsing of a heart. This concept is often used in decorative lighting, wearable technology, and art installations to convey emotions and enhance aesthetics.
![Smartwatch measures heartbeat](https://media.product.which.co.uk/prod/images/original/gm-c1d5d7ac-0b34-416d-989d-9ec41158db08-apple-watch-5-ecg-615x369.jpg)
---

## What Does the Code Do?

The code is designed to control a strip of NeoPixel LEDs to display a heart pattern. The pattern moves smoothly along the strip, creating a dynamic visual effect. The brightness of the LEDs varies in a sinusoidal manner to mimic the shape of a heart.


How does it work?
---


### 1. Setup and Initialization

- **Library Inclusion**: Includes the Adafruit NeoPixel library.
- **Define Pin and Pixels**: Sets the pin number and the number of LEDs in the strip.
- **Initialize Strip**: Begins the strip and initializes all pixels to 'off'.
- **Generate Pattern**: Calls `generateHeartPattern` to create the heart pattern.

### 2. Main Loop

- **Static Offset**: Uses a static variable `offset` to track the position of the heart pattern.
- **Display Pattern**: Calls `displayHeartPattern` to show the pattern with the current offset.
- **Shift Pattern**: Adjusts the `offset` to move the pattern left and resets it if necessary.
- **Delay**: Waits for 200 milliseconds to make the pattern movement visible.

### 3. Generating the Heart Pattern

- **Sine Wave Calculation**: Uses a sine function to calculate brightness values.
- **Brightness Values**: Converts sine values to a range between 0 and 255.
- **Store Pattern**: Saves the calculated values into the `heartPattern` array.

### 4. Displaying the Pattern

- **Offset Calculation**: Adjusts the index of the pattern using the current offset.
- **Set Brightness**: Retrieves brightness from `heartPattern` and sets the LED color.
- **Update Strip**: Shows the updated LED colors on the strip.
---

## Challenges During Development

- **Reducing Expectations**: We wanted to use a heartbeatsensor to show a life heartbeat which we couldn't acomplish, so we had to lower our expectations.
- **Pattern Accuracy**: Ensuring the sine wave accurately represented a heart shape required careful adjustment.
- **Pattern moving direction**: Making the Pattern move from the left to the right.
- **Brightness Control**: Achieving the right brightness levels to make the heart pattern clearly visible without being too dim or too bright.

---

## Future Ideas

- **Multi-color Patterns**: Introducing different colors to create more complex and visually interesting patterns.
- **Interactive Controls**: Adding sensors or remote controls to scan a live heartbeat and display it.
- **Pattern Library**: Expanding the code to include a library of different heartbeat patterns that can be switched dynamically or compared with different colors.

---

## Code

To simulate the LED heart pattern, you can use the following code on an Arduino board connected to a NeoPixel strip:

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
  offset = (offset - 1 + NUMPIXELS) % NUMPIXELS; // bewegung
  delay(200); // sichtbarkeit delay
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
