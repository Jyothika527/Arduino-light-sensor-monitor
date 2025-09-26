Project: Automatic Night Light Indicator 

 Overview

This repository documents an embedded systems mini-project: a Arduino light Sensor Monitoring System designed to demonstrate core skills in circuit design and microcontroller programming. The system functions as an automatic night light that detects when ambient light levels drop below a defined threshold and activates an LED indicator.

The required project deliverables—the schematic, the code (`light_sensor_code.ino`), and this tutorial-style documentation—are all contained within this repository.


 1. System Requirements and Components

The system is built around the Arduino Uno R3 microcontroller. The primary input component is a Photoresistor (LDR), which acts as the light sensor. The system's output is a standard **LED**, serving as the night light indicator. Two resistors are necessary: a **$10 \text{k}\Omega$ resistor** to create the sensor voltage divider and a **$220 \Omega$ resistor** to limit current to the LED.



 2. Circuit Implementation and Wiring Guide

The circuit is implemented on a breadboard in Tinkercad Circuits and involves two main sections: the sensor input (LDR) and the digital output (LED). 

 A. The Sensor Circuit (Input)

The Photoresistor (LDR) needs a voltage divider configuration to convert its changing resistance into a readable voltage signal for the Arduino's Analog-to-Digital Converter (ADC).

1.  Connect one leg of the LDR directly to the +5V pin on the Arduino.
2.  Connect the other leg of the LDR to one end of the 10kΩ resistor.
3.  Connect the free end of the 10kΩ resistor to GND.
4.  Crucially, the signal line must be taken from the junction where the LDR and the 10kΩ resistor meet, and connected to the Arduino's Analog Pin A0.
   
 B. The LED Circuit (Output)

The LED is connected to a digital pin for simple ON/OFF control.

1.  Connect the LED Anode  to Arduino Digital Pin 13.
2.  Connect the LED Cathode  through the 220Ω current-limiting resistor to the common GND rail.


 3. Programming Logic (`light_sensor_code.ino`)

The firmware implements continuous monitoring and threshold-based decision-making.

The `setup()` function configures Pin 13 as an output and initializes the Serial Monitor for debugging. The core logic resides in the `loop()`:

  1.  Analog-to-Digital Conversion (ADC): The `analogRead(A0)` function samples the voltage from the LDR circuit, yielding a digital value between 0 (very dark)and 1023 (very bright)**. This reading is stored in the `lightValue` variable.
  2.  Threshold Check: A constant, DARK_THRESHOLD, is set to 400. This value defines the state we are monitoring.
  3.  Conditional Control: An `if/else` statement compares the `lightValue` against the threshold. If the `lightValue` is less than 400 (indicating darkness), the program executes `digitalWrite(LED_PIN, HIGH)`, turning the light ON. Otherwise, the LED remains LOW (OFF).
  4.  The current `lightValue` and the system's decision are printed to the Serial Monitor in each cycle for real-time monitoring and calibration.

   

4. Testing and Verification

The system's operation was verified through real-time simulation:

1.  The simulation is started, and the Serial Monitor is opened to track the sensor readings.
2.  When the simulated ambient light is bright (sensor value is high, e.g., 900), the LED remains OFF.
3.  As the simulated light intensity is reduced (by clicking the LDR and adjusting the slider), the sensor value drops. Once the reading falls below the 400 threshold (e.g., to 350), the LED immediately switches ON, confirming the successful implementation of the control logic.
This functionality confirms the system correctly interprets analog sensor input and drives a digital output based on the programmed condition.
