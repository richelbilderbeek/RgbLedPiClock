# RgbLedPiClock

[![Build Status](https://travis-ci.org/richelbilderbeek/RgbLedPiClock.svg?branch=master)](https://travis-ci.org/richelbilderbeek/RgbLedPiClock)

The PiClock is [one of my machines](https://github.com/richelbilderbeek/Machines) that uses Arduino.
It's an Arduino project for a clock that displays the time in binary and beeps at pi o'clock PM.

This [PiClock](README.md) uses RGB LEDs to display the time.

![Prototype of the RGB LED Pi Clock](PiClocks.jpg)

Thanks to James Rosindell for the picture.

## Prototype

![Pi Clock Prototype side](RgbLeds/PiClockRgbLedsPrototypeSide.jpg)
![Pi Clock Prototype front](RgbLeds/PiClockRgbLedsPrototypeFront.jpg)
![Pi Clock Prototype close up](RgbLeds/PiClockRgbLedsPrototypeCloseUp.jpg)
![Pi Clock Prototype and ApproxyClock prototypes](RgbLeds/PiClockRgbLedsPrototypeAndApproxyClockPrototype.jpg)

## How to read the time

Determine which LED goes on an off every second. This is LED with index 0. Then the LEDs are ordered clockwise. LEDs 4 and 8 change state every 1 in 5 seconds, to indicate their position.

| LED index |  0 | 1 | 2 | 3 | 4  | 5  | 6 | 7 | 8  | 9  | A | B | Color |
|-----------|----|---|---|---|----|----|---|---|----|----|---|---|------:|
| seconds   |  1 | 2 | 4 | 8 | 16 | 32 |   |   |    |    |   |   | Red   |
| minutes   |    |   |   |   | 1  | 2  | 4 | 8 | 16 | 32 |   |   | Green |
| hours     | 16 |   |   |   |    |    |   |   | 1  | 2  | 4 | 8 | Blue  |

### Example 1

Image the LEDs having the following colors (R: Red, G: Green, B: blue, blank: no color):

| LED index |  0 | 1 | 2 | 3 | 4  | 5  | 6 | 7 | 8  | 9  | A | B |
|-----------|----|---|---|---|----|----|---|---|----|----|---|---|
| LED       |  R | R |   |   |    | G  |   |   | B  |    |   |   |

This equals: 1:02:03 (hh:mm:ss)

| LED index |  0 | 1 | 2 | 3 | 4  | 5  | 6 | 7 | 8  | 9  | A | B | Color |
|-----------|----|---|---|---|----|----|---|---|----|----|---|---|------:|
| LED       |  R | R |   |   |    | G  |   |   | B  |    |   |   |
| seconds   |  1 | 2 | 4 | 8 | 16 | 32 |   |   |    |    |   |   | Red   |
| minutes   |    |   |   |   | 1  | 2  | 4 | 8 | 16 | 32 |   |   | Green |
| hours     | 16 |   |   |   |    |    |   |   | 1  | 2  | 4 | 8 | Blue  |


### Example 2

Image the LEDs having the following colors (R: Red, G: Green, B: blue, blank: no color):

| LED index |  0 | 1 | 2 | 3 | 4  | 5  | 6 | 7 | 8  | 9  | A | B |
|-----------|----|---|---|---|----|----|---|---|----|----|---|---|
| LED       |  R | R | R | R |    | G  | G | G | B  | B  | B | B |

This equals: 3:14:15 (hh:mm:ss)

| LED index |  0 | 1 | 2 | 3 | 4  | 5  | 6 | 7 | 8  | 9  | A | B | Color |
|-----------|----|---|---|---|----|----|---|---|----|----|---|---|------:|
| LED       |  R | R | R | R |    | G  | G | G | B  | B  | B | B |       |
| seconds   |  1 | 2 | 4 | 8 | 16 | 32 |   |   |    |    |   |   | Red   |
| minutes   |    |   |   |   | 1  | 2  | 4 | 8 | 16 | 32 |   |   | Green |
| hours     | 16 |   |   |   |    |    |   |   | 1  | 2  | 4 | 8 | Blue  |

### Example 3

Image the LEDs having the following colors (R: Red, G: Green, B: blue, blank: no color, M: magenta (R + B), Y: yellow (R + G), C: cyan (G + B)):

| LED index |  0 | 1 | 2 | 3 | 4  | 5  | 6 | 7 | 8  | 9  | A | B |
|-----------|----|---|---|---|----|----|---|---|----|----|---|---|
| LED       |  M | R |   | R | Y  | Y  |   | G | C  | C  | B |   |

This equals: 23:59:59 (hh:mm:ss)

| LED index |  0 | 1 | 2 | 3 | 4  | 5  | 6 | 7 | 8  | 9  | A | B | Color |
|-----------|----|---|---|---|----|----|---|---|----|----|---|---|------:|
| LED       |  M | R |   | R | Y  | Y  |   | G | C  | C  | B |   |
| seconds   |  1 | 2 |   | 8 | 16 | 32 |   |   |    |    |   |   | Red   |
| minutes   |    |   |   |   | 1  | 2  |   | 8 | 16 | 32 |   |   | Green |
| hours     | 16 |   |   |   |    |    |   |   | 1  | 2  | 4 | 8 | Blue  |

