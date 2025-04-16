# CMOS_Inverter
This project aims at designing and analyzing a CMOS Inverter using GPDK90 90nm technology using Cadence Virtuoso and then comparing pre layout and post layout designs using Transient and DC analyses. It contains:
- [Introduction](#introduction)
- [Pre layout analysis](#pre-layout-analysis)
  - [Pre layout DC analysis](#pre-layout-dc-analysis)
  - [Pre layout Transient analysis](#pre-layout-transient-analysis)
  - [Pre layout netlist](#pre-layout-netlist)
- [Post layout analysis](#post-layout-analysis)
  - [Post layout DC analysis](#post-layout-dc-analysis)
  - [Post layout Transient analysis](#post-layout-transient-analysis)
  - [Post layout netlist](#post-layout-netlist)
- [Pre layout v/s Post layout analysis report](#pre-layout-vs-post-layout-analysis-report)

# Introduction
A CMOS inverter is the most basic logic gate built using CMOS technology. It consists of a PMOS transistor connected to VDD and an NMOS transistor connected to GND, both sharing a common gate input and a common output node. When the input is HIGH, the NMOS conducts and the PMOS is OFF, pulling the output LOW. When the input is LOW, the PMOS conducts and the NMOS is OFF, pulling the output HIGH. This inverts the input signal.
The CMOS inverter operates using two distinct voltage levels to represent binary logic—logic 0 and logic 1. It is ideal for digital applications such as processors, memory, and logic circuits. Additionally, it offers advantages like low static power consumption, high speed, and excellent noise margins.

![image](https://github.com/user-attachments/assets/7522a8cb-b4ce-4a7e-ac4f-a78ce2d9531f)

## Creation of CMOS Inverter schematic
Creating a library

![Create_library](https://github.com/user-attachments/assets/b00af3e5-35b9-4854-b103-286db2475524)

Creating a cellview for design, the schematic is as follows:

![schematic](https://github.com/user-attachments/assets/17fdfd5f-dd1a-4adc-ab49-7222327f2613)

After creation of schematic, the symbol for the same is as follows:

![symbol](https://github.com/user-attachments/assets/87beeb1d-d9e8-49c3-994a-50f314510eed)

# Pre layout analysis
Pre-layout analysis is performed on the schematic design of the CMOS inverter before the physical layout is created to verify the logical behavior and performance of the circuit without parasitic effects.
## Pre layout DC analysis
DC analysis for a CMOS inverter is a simulation used to determine the output voltage of the inverter for different constant input voltage levels, keeping all other sources steady. It helps plot the voltage transfer characteristic (VTC) of the CMOS inverter. This curve shows how the output voltage changes as the input voltage is swept from 0 to VDD. It helps in identifying the following parameters:
* VOH (Output High Voltage)
* VOL (Output Low Voltage)
* VIH (Input High Voltage)
* VIL (Input Low Voltage)
* VTH (Threshold Voltage)

To perform DC analysis we have to first create a testbench or simulation setup on which we will provide input waveforms and measure output waveform.

![Pre_test_bench](https://github.com/user-attachments/assets/afec9ac7-4b91-42d1-ae8d-458cfccc13ef)

Here, VIN is a pulse voltage with the following parameters:
V1=OV, V2=1.8V, Period=40ns, Delay time=0ns, Fall time=1ns, Rise time=1ns and Pulse width=20ns.
Vdc is 1.8V To perform DC analysis we have to go to **Launch->ADE L->dc**,in dc, check save operating point and select component parameter as vpulse to do the dc sweep. The DC output comes out to be as shown in figure below:

![Prelayout_dc](https://github.com/user-attachments/assets/f870e628-e938-4bf0-ac1a-ac23abc3c186)



VOH is measured at the minimum value of VIN(VOL) i.e 0, VOL is calculated at input voltage maximum value of VIN( VOH or VDD) i.e 1.8V, VIH are calculated by finding points at VTC where derivative of VOUT wrt VIN = -1, the smaller value being VIL and higher being VIH, for them, we use the calculator functionality
of ADE L to plot **deriv(VS("/vout"))**.
Calculation of VOH:

![VOH_calculation](https://github.com/user-attachments/assets/b4a4ab5f-2b7d-459d-b043-a25a208624aa)

It can be inferred that VOH = 1.795V from the above figure.

Calculation of VOL:

![VOL_calculation](https://github.com/user-attachments/assets/17fb4b24-7a01-4b3d-ad8d-4816536bf979)

It can be inferred that VOL = 14.725uV from the above figure.

Calculation of VIH and VIL:

![VIH_and_VIL_calculation](https://github.com/user-attachments/assets/2617035d-9127-4ec2-b59f-ed8530c81a90)

From the above figure, it can be noted that VIL = 388.27mV and VIH = 869.28mV.

Calculation of VTH:

![VTH_calculation](https://github.com/user-attachments/assets/51206d9c-84cb-4061-aa5c-a8700ecabaa9)

It can be noted that VTH = 0.7V from the above figure.
### Calculation of noise margin
NML = VIL - VOL = 388.255mV

NMH = VOH - VIH = 925.72mV

## Pre layout transient analysis
Pre-layout transient analysis simulates the time-dependent behavior of the CMOS inverter using the schematic before layout. It applies a time-varying input and observes how the output voltage responds to it. It captures the dynamic performance of the circuit, unlike DC analysis which only focuses on steady-state behavior.
This analysis is essential for evaluating key performance metrics such as propagation delay, rise time, and fall time, which impact the overall speed and efficiency of digital circuits. The Vin is the pulse voltage with the following parameters:

![vpulse_transient](https://github.com/user-attachments/assets/4aade500-28de-420e-9a0d-0c059dd691c9)

To perform transient analysis we have to go to **Launch -> ADE L ->tran** ,here we are performing transient analysis for 160ns, the output of the transient response comes out to be:

![Prelayout_transient](https://github.com/user-attachments/assets/9e9d0234-7a1d-4f44-9340-a7bb8aa45126)

### Calculation of Propagation delay
Propagation delay is the time it takes for the output of a CMOS inverter to respond to a change in the input signal. It is of 2 types, first being when the input changes changes from high to low and output changes from low to high(Tplh) and the other when the input changes from low to high and  
















  


