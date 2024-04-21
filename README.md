# Horizontal Thrust Measuring Stage

A stage to measure horizontral thrust generated by rocket engine.

This is a project created by students in The Aviation Club of the [Second High School Atteched to Beijing Normal University](https://www.shsbnu.net/index.html).

![SolidWorks Model](https://github.com/langonginc/ForceTestStand/assets/59787082/991fc9b3-a0c8-4702-90a3-2a5feca6abd2)

# Highlights

We use Arduino Mega 2560 and HX711 to record and store the magnitude of the thrust into the program, and graph the associated function (force @ time).

- **0-20kg** measuring range _(maximum value not to exceed 30kg)_
- 30-50mm engine diameter fit
- 10Hz sample rate (langonginc/ForceTestStand#1 We really need your help to increase it)
- Real-time display
- SD card data writing

# Theory

Presure -> Sensors -> HX711 -> Arduino.

Pressure sensors generate a voltage by sensing pressure. Sensitive voltage value is 1mv, which means if I apply a force of `1kg`, it produces a voltage of `1mV` (for 0-10kg sensor).

HX711 will firstly amplify the voltage generated by the pressure sensor, since the voltage is too small. Then it will convert the analog signals (amplified voltage values) to digital signals (ad values).

After that, Arduino will get the digital signals (ad values). We then scale the digital signal to fit the pressure.

## Why We Use HX711

Based on Avia Semiconductor’s patented technology, HX711 is a precision 24-bit analog- to-digital converter (ADC) designed for weigh scales and industrial control applications to interface directly with a bridge sensor.

The input multiplexer selects either Channel A or B differential input to the low-noise programmable gain amplifier (PGA). Channel A can be programmed with a gain of 128 or 64, corresponding to a full-scale differential input voltage of ±20mV or ±40mV respectively, when a 5V supply is connected to AVDD analog power supply pin. Channel B has a fixed gain of 32. On- chip power supply regulator eliminates the need for an external supply regulator to provide analog power for the ADC and the sensor. Clock input is flexible. It can be from an external clock source, a crystal, or the on-chip oscillator that does not require any external component. On-chip power- on-reset circuitry simplifies digital interface initialization.

There is no programming needed for the internal registers. All controls to the HX711 are through the pins.

## How HX711 works

The HX711 communicates with the microcontroller in serial communication mode consisting of pins SCK and DOUT. When DOUT goes from high to low, SCK inputs 25 pulses at a time to read the 24-bit A/D conversion data into the microcontroller and selects the input channel and gain for the next conversion on the 25th clock pulse.
