University of Pennsylvania, ESE 5190: Intro to Embedded Systems, Lab 2B

    Sizhe Ma
        masizhe@seas.upenn.edu
    Tested on: Thinkpad X1, Windows 10 Pro, Intel(R) Core(TM) i7-8650U CPU @ 1.90GHz   2.11 GHz
    
# Proposal

## Breadboard LED Buildup and RP2040 GPIO Test

In this part, we firstly try to build a single LED circuit (Blue LED and 1k protect resistor), then use GPIO pin on RP2040 as a power supply to drive the circuit.

We use GPIO pin at on the Stemma QT cable as the input, with the number "GPIO22"

The test code is shown below:

```
#include "pico/stdlib.h"

int main() {
    //const uint LED_PIN = PICO_DEFAULT_LED_PIN;
    const uint LED_PIN = 22;      # since we use GPIO22 pin on Stemma QT, we initialize LED pin value as 22
    gpio_init(LED_PIN);
    gpio_set_dir(LED_PIN, GPIO_OUT);
    while (true) {
        gpio_put(LED_PIN, 1);    
        sleep_ms(250);
        gpio_put(LED_PIN, 0);
        sleep_ms(250);
    }
}
```
## Result

The result is shown below:


# Outline

In lab 2B we plan to build the circuit in following steps:

1) Since there are several GPIO pins on QT-PY 2040 which can be used as I/O port. We plans to use several GPIO pins to drive several different color LEDs connect in parallel (Or let's say, we are going to build several individual LED circuits powered by different GPIO port.) To test if those GPIO port can drive different color LED individually, we can design different patterns similar to patterns in lab2A ws2812 example to light up LEDs (random, one-by-one, etc.)

2) Then to make our design has some practical usage, we can utilize the sensor APDS9960, such as brightness detecting or gesture modules to control the change in LEDs. For example, if the sensor detect that the environment brightness is in a specific range, QT-PY 2040 will turn on one of LEDs. Or if the sensor detect the continuing change in brightness, the circuit will light up one specific LED to show if the brightness is going up/down. For the gesture sensor, we can design a program which use different gestures to light up different color LEDs.

I think our design is cool because integrate different devises that we used in previous labs and make designs with practical usage. For example, it can be used as a visualized brightness detector, or it can be used as a motion detector.

The components we will use in this lab are QT-PY 2040 and sensor APDS9960, which we have already got from lab 1. Besides, we will use resistors (330ohm - 1k ohm) and different color LEDs. All these items are availiable in Detkin Lab.

## Questions
For our design, we do have some questions:

1) When the sensor detect the brightness, will it return a specific value back to RP2040? Or will it return values in different pattern?

2) Same question for gesture sensor and its return... Will it use I2C protocol?
