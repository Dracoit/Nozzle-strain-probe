# Nozzle-strain-probe
Use the nozzle as a probe with a load cell.
This works great as you don't need to determine the probe to nozzle offsets, no additional probes to deploy or calibrate.
no limited life in contrast to BL touch. better than an inductive probe as it does not interfere with bed material or temperature fluctuations etc.

The project uses a 50Kg generic load cell with HX711 analog-to-digital converter along  with a cheap MW82F6D17 uController to read the digital signal of the ADC**.

**HX711 ADC**
  It is an easily available cheap & reliable PGA with little to no code required to use it optimally.
  It can read 80Sps which is sufficient for our purpose.
  It can be configured with the pins, no register configurations are required.
  Cheap, yes it is cheap for what it does!

**MW82F6D17**
The uController is a cheap 8051 ucontroller that requires no external component for operation.
It is required to read the serial data from the HX711 and does the following:
  1. Generates CLK signal for HX711 & reads the DATA from HX711.
  2. Reads data for a few mili seconds and calibrates it the probe.
  3. Reduces the noise from the sensor readings.
  4. Monitor the reading constantly for changes in the load cell reading.
  5. If the Nozzle touches the build surface it changes its output pin to High to be read by the printer endstop pin.
  6. The code is still a work in progress to adjust the nozzle to bed force for triggering, however, the current default value works best.

 **Future Plans**
 In future, the probe can be integrated into Klipper ( as it is programming-friendly & has many feature expansion capabilities) for the following:
   1. Read the nozzle pressure and determine the optimal flow rate for better print quality.
   2. Calibrate print temperature for different materials by determining the pressure of the nozzle and extruder, this will help reduce extruder skipping steps.
 And many more.
