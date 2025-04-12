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

# Creation of CMOS Inverter schematic
Creating a library

  


