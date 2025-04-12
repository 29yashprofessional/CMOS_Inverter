# CMOS_Inverter
This project aims at designing and analyzing a CMOS Inverter using GPDK90 90nm technology using Cadence Virtuoso and then comparing pre layout and post layout designs using Transient and DC analyses. It contains:
* Pre layout analysis using schematic
  * Pre layout DC analysis
  * Pre layout Transient analysis
  * Pre layout netlist
* Post layout analyis
  * Post layout DC analysis
  * Post layout Transient analysis
  * Post layout netlist
* Pre layout v/s Post layout analysis report
# Introduction
A CMOS inverter is the most basic logic gate built using Complementary Metal-Oxide-Semiconductor (CMOS) technology. It consists of a PMOS transistor connected to VDD and an NMOS transistor connected to GND, both sharing a common gate input and a common output node. When the input is high, the NMOS conducts and the PMOS is off, pulling the output low. When the input is low, the PMOS conducts and the NMOS is off, pulling the output high. This inverts the input signal.
The CMOS inverter is a fundamental digital circuit because it operates using two distinct voltage levels to represent binary logic—logic 0 and logic 1. It switches cleanly between these states, making it ideal for digital applications such as processors, memory, and logic circuits. Additionally, it offers advantages like low static power consumption, high speed, and excellent noise margins.

![image](https://github.com/user-attachments/assets/7522a8cb-b4ce-4a7e-ac4f-a78ce2d9531f)

# Creation of CMOS Inverter schematic
Creating a library

![Create_library](https://github.com/user-attachments/assets/b00af3e5-35b9-4854-b103-286db2475524)

Creating a cellview for design, the schematic is as follows:

![schematic](https://github.com/user-attachments/assets/17fdfd5f-dd1a-4adc-ab49-7222327f2613)

After creation of schematic, the symbol for the same is as follows:

![symbol](https://github.com/user-attachments/assets/87beeb1d-d9e8-49c3-994a-50f314510eed)

# Pre layout analysis
Pre layout dc analysis
DC analysis for a CMOS inverter is a simulation used to determine the output voltage of the inverter for different constant input voltage levels, while keeping all other sources steady. It helps plot the voltage transfer characteristic (VTC) of the CMOS inverter. This curve shows how the output voltage changes as the input voltage is swept from 0 to VDD. It helps in identifying the following parameters:
* VOH (Output High Voltage): Minimum voltage the output reaches when representing logic 1.
* VOL (Output Low Voltage): Maximum voltage the output reaches when representing logic 0.
* VIH (Input High Voltage): Minimum input voltage recognized as logic 1.
* VIL (Input Low Voltage): Maximum input voltage recognized as logic 0.

VOH is measured at the minimum value of VIN(VOL) i.e 0, VOL is calculated at input voltage maximum value of VIN( VOH or VDD) i.e 1.8V, VIH are calculated by finding points at VTC where derivative of VOUT wrt VIN = -1, the smaller value being VIL and higher being VIH, for them, we use the calculator functionality
of ADE L to plot deriv(VS("/vout")).




  


