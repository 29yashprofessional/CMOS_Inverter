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

![Test_bench](https://github.com/user-attachments/assets/65db124c-57c0-4b07-b817-628a85235597)


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
### Calculation of Noise Margins
NML = VIL - VOL = 388.255mV

NMH = VOH - VIH = 925.72mV

## Pre layout transient analysis
Pre-layout transient analysis simulates the time-dependent behavior of the CMOS inverter using the schematic before layout. It applies a time-varying input and observes how the output voltage responds to it. It captures the dynamic performance of the circuit, unlike DC analysis which only focuses on steady-state behavior.
This analysis is essential for evaluating key performance metrics such as propagation delay, rise time, and fall time, which impact the overall speed and efficiency of digital circuits. The Vin is the pulse voltage with the following parameters:

![vpulse_transient](https://github.com/user-attachments/assets/4aade500-28de-420e-9a0d-0c059dd691c9)

To perform transient analysis we have to go to **Launch -> ADE L ->tran** ,here we are performing transient analysis for 160ns, the output of the transient response comes out to be:

![Prelayout_transient](https://github.com/user-attachments/assets/9e9d0234-7a1d-4f44-9340-a7bb8aa45126)

### Calculation of Propagation delay
Propagation delay is the time it takes for the output of a CMOS inverter to respond to a change in the input signal. It is of 2 types, first being when the input changes changes from high to low and output changes from low to high(Tplh) and the other when input changes from low to high and output changes from high to low(Tphl). The average of the two is termed as the propagation delay. 50% voltage is generally taken as the threshold to calculate propagation delay. 

Calculation of Tplh:

![Prelayout_Tplh](https://github.com/user-attachments/assets/b7f66b72-7c16-4e6b-9b3a-910233d8b0a1)

From the above figure, Tplh(given by dx in the image)= 306.36ps.

Calculation of Tphl:

![Prelayout_Tphl](https://github.com/user-attachments/assets/93440cbc-d3b7-4edc-a9ca-2bed0999575a)

From the above figure, Tphl= 27.80ps.
Propagation delay,Tp= (Tplh+Tphl)/2 = 167.08ps.

### Calculation of Static and Dynamic power dissipation
Static power disisipation refers to the power dissipated when the state of the CMOS inverter is not changing. It occurs primarily due to leakage currents.
Dynamic power dissipation refers to the power dissipated when the state of the CMOS inverter is changing. It occurs to the charging and dischanrging of capacitive loads. 

![Pre_power_dissipation](https://github.com/user-attachments/assets/8d7398d6-3c24-4d91-9a2d-0a92015e4507)

There are 2 values of static power dissipation because one of them is for the HIGH state while the other is for LOW state, higher one being for the HIGH state. Similarly, there are 2 different values for dynamic power dissipation because they represent different transitions, one representing shift of state from HIGH to LOW while the other representing change of state from LOW to HIGH, higher one being for the HIGH to LOW transition. The values for dissipation are calculated by taking the average of the two values.

Average Static power dissipation = (4.03705 + 481.9898) nW / 2 = 243.01 nW
Average Dynamic power dissipation = (79.38654 + 94.22233) μW / 2 = 86.80 μW

## Pre layout netlist
```
Cadence (R) Virtuoso (R) Spectre (R) Circuit Simulator
Version 12.1.0.347.isr3 32bit -- 10 Jan 2013
Copyright (C) 1989-2012 Cadence Design Systems, Inc. All rights reserved worldwide. Cadence, Virtuoso and Spectre are registered trademarks of Cadence Design Systems, Inc. All others are the property of their respective holders.

Protected by U.S. Patents: 
        5,610,847; 5,790,436; 5,812,431; 5,859,785; 5,949,992; 5,987,238; 
        6,088,523; 6,101,323; 6,151,698; 6,181,754; 6,260,176; 6,278,964; 
        6,349,272; 6,374,390; 6,493,849; 6,504,885; 6,618,837; 6,636,839; 
        6,778,025; 6,832,358; 6,851,097; 6,928,626; 7,024,652; 7,035,782; 
        7,085,700; 7,143,021; 7,493,240; 7,571,401.

Includes RSA BSAFE(R) Cryptographic or Security Protocol Software from RSA Security, Inc.

User: buet   Host: cadence   HostID: 7F0100   PID: 4035
Memory  available: 3.1112 GB  physical: 4.1155 GB
CPU Type: Intel(R) Core(TM) i5-10210U CPU @ 1.60GHz
          Processor PhysicalID CoreID Frequency
              0         0        0     2112.0
              1         0        1     2112.0
              2         1        0     2112.0
              3         1        1     2112.0
              4         2        0     2112.0
              5         2        1     2112.0
              6         3        0     2112.0
              7         3        1     2112.0


Simulating `input.scs' on cadence at 5:23:05 PM, Wed Apr 16, 2025 (process id: 4035).
Current working directory: /home/buet/simulation/inverter_tb/spectre/schematic/netlist.
Command line:
    /home/buet/cadence/MMSIM121/tools.lnx86/spectre/bin/32bit/spectre  \
        input.scs +escchars +log ../psf/spectre.out +inter=mpsc  \
        +mpssession=spectre0_3475_1 -format psfxl -raw ../psf  \
        +lqtimeout 900 -maxw 5 -maxn 5
spectre pid = 4035

Loading /home/buet/cadence/MMSIM121/tools.lnx86/cmi/lib/5.0/libinfineon_sh.so ...
Loading /home/buet/cadence/MMSIM121/tools.lnx86/cmi/lib/5.0/libphilips_o_sh.so ...
Loading /home/buet/cadence/MMSIM121/tools.lnx86/cmi/lib/5.0/libphilips_sh.so ...
Loading /home/buet/cadence/MMSIM121/tools.lnx86/cmi/lib/5.0/libsparam_sh.so ...
Loading /home/buet/cadence/MMSIM121/tools.lnx86/cmi/lib/5.0/libstmodels_sh.so ...
Reading file:  /home/buet/simulation/inverter_tb/spectre/schematic/netlist/input.scs
Reading file:  /home/buet/cadence/gpdk090_v4.6/models/spectre/gpdk090.scs
Reading file:  /home/buet/cadence/gpdk090_v4.6/models/spectre/gpdk090_mos.scs
Reading file:  /home/buet/cadence/gpdk090_v4.6/models/spectre/gpdk090_mos_iso.scs
Reading file:  /home/buet/cadence/gpdk090_v4.6/models/spectre/gpdk090_resistor.scs
Reading file:  /home/buet/cadence/gpdk090_v4.6/models/spectre/resd_va.va
Reading link:  /home/buet/cadence/MMSIM121/tools.lnx86/spectre/etc/ahdl/discipline.h
Reading file:  /home/buet/cadence/MMSIM121/tools.lnx86/spectre/etc/ahdl/disciplines.vams
Reading link:  /home/buet/cadence/MMSIM121/tools.lnx86/spectre/etc/ahdl/constants.h
Reading file:  /home/buet/cadence/MMSIM121/tools.lnx86/spectre/etc/ahdl/constants.vams
Reading file:  /home/buet/cadence/gpdk090_v4.6/models/spectre/rnoise_va.va
Reading file:  /home/buet/cadence/gpdk090_v4.6/models/spectre/gpdk090_capacitor.scs
Reading file:  /home/buet/cadence/gpdk090_v4.6/models/spectre/gpdk090_diode.scs
Reading file:  /home/buet/cadence/gpdk090_v4.6/models/spectre/gpdk090_bipolar.scs

Time for NDB Parsing: CPU = 3.41448 s, elapsed = 3.8968 s.
Time accumulated: CPU = 3.41448 s, elapsed = 3.8968 s.
Peak resident memory used = 32.2 Mbytes.


Time for Elaboration: CPU = 174.974 ms, elapsed = 208.823 ms.
Time accumulated: CPU = 3.59145 s, elapsed = 4.10699 s.
Peak resident memory used = 34.7 Mbytes.


Time for EDB Visiting: CPU = 17.998 ms, elapsed = 53.777 ms.
Time accumulated: CPU = 3.60945 s, elapsed = 4.1616 s.
Peak resident memory used = 35.1 Mbytes.


Warning from spectre during initial setup.
    WARNING (CMI-2477): I0.PM0: `Rds' = 70.9091 uOhm is less than 0.001. Set to 0.


Circuit inventory:
              nodes 3
            bsim3v3 2     
          capacitor 1     
            vsource 2     


Warning from spectre during initial setup.
    WARNING (CMI-2477): I0.PM0: `Rds' = 70.9091 uOhm is less than 0.001. Set to 0.


Time for parsing: CPU = 36.995 ms, elapsed = 88.9468 ms.
Time accumulated: CPU = 3.64744 s, elapsed = 4.25146 s.
Peak resident memory used = 35.8 Mbytes.

Entering remote command mode using MPSC service (spectre, ipi, v0.0, spectre0_3475_1, ).

Warning from spectre.
    WARNING (SPECTRE-16707): Only tran supports psfxl format, result of other analyses will be in psfbin format.


*************************************************
Transient Analysis `tran': time = (0 s -> 160 ns)
*************************************************
DC simulation time: CPU = 4 ms, elapsed = 60.57 ms.
Important parameter values:
    start = 0 s
    outputstart = 0 s
    stop = 160 ns
    step = 160 ps
    maxstep = 3.2 ns
    ic = all
    useprevic = no
    skipdc = no
    reltol = 1e-03
    abstol(V) = 1 uV
    abstol(I) = 1 pA
    temp = 27 C
    tnom = 27 C
    tempeffects = all
    errpreset = moderate
    method = traponly
    lteratio = 3.5
    relref = sigglobal
    cmin = 0 F
    gmin = 1 pS

    tran: time = 5.407 ns    (3.38 %), step = 2.19 ns      (1.37 %)
    tran: time = 15.01 ns    (9.38 %), step = 3.2 ns          (2 %)
    tran: time = 21 ns       (13.1 %), step = 2.793 ns     (1.75 %)
    tran: time = 30.97 ns    (19.4 %), step = 3.2 ns          (2 %)
    tran: time = 37.37 ns    (23.4 %), step = 3.2 ns          (2 %)
    tran: time = 45.61 ns    (28.5 %), step = 2.292 ns     (1.43 %)
    tran: time = 52.01 ns    (32.5 %), step = 3.2 ns          (2 %)
    tran: time = 61 ns       (38.1 %), step = 2.59 ns      (1.62 %)
    tran: time = 70 ns       (43.8 %), step = 3.2 ns          (2 %)
    tran: time = 76.4 ns     (47.8 %), step = 3.2 ns          (2 %)
    tran: time = 86.55 ns    (54.1 %), step = 2.762 ns     (1.73 %)
    tran: time = 92.95 ns    (58.1 %), step = 3.2 ns          (2 %)
    tran: time = 101 ns      (63.1 %), step = 2.424 ns     (1.52 %)
    tran: time = 108.2 ns    (67.6 %), step = 3.081 ns     (1.93 %)
    tran: time = 117.8 ns    (73.6 %), step = 3.2 ns          (2 %)
    tran: time = 126.5 ns    (79.1 %), step = 2.754 ns     (1.72 %)
    tran: time = 132.9 ns    (83.1 %), step = 3.2 ns          (2 %)
    tran: time = 141 ns      (88.1 %), step = 2.432 ns     (1.52 %)
    tran: time = 148.2 ns    (92.6 %), step = 3.054 ns     (1.91 %)
    tran: time = 157.8 ns    (98.6 %), step = 3.2 ns          (2 %)
Number of accepted tran steps =             257

Notice from spectre during transient analysis `tran'.
    Trapezoidal ringing is detected during tran analysis.
        Please use method=trap for better results and performance.

Initial condition solution time: CPU = 4 ms, elapsed = 60.7028 ms.
Intrinsic tran analysis time:    CPU = 63.991 ms, elapsed = 122.649 ms.
Total time required for tran analysis `tran': CPU = 80.988 ms, elapsed = 210.493 ms.
Time accumulated: CPU = 3.74943 s, elapsed = 4.60977 s.
Peak resident memory used = 37.3 Mbytes.

finalTimeOP: writing operating point information to rawfile.

******************
DC Analysis `dcOp'
******************
Important parameter values:
    reltol = 1e-03
    abstol(V) = 1 uV
    abstol(I) = 1 pA
    temp = 27 C
    tnom = 27 C
    tempeffects = all
    gmindc = 1 pS
Convergence achieved in 6 iterations.
Total time required for dc analysis `dcOp': CPU = 11.997 ms, elapsed = 12.958 ms.
Time accumulated: CPU = 3.80042 s, elapsed = 4.67413 s.
Peak resident memory used = 37.5 Mbytes.

dcOpInfo: writing operating point information to rawfile.

****************************************
DC Analysis `dc': V0:dc = (0 V -> 1.8 V)
****************************************
Important parameter values:
    reltol = 1e-03
    abstol(V) = 1 uV
    abstol(I) = 1 pA
    temp = 27 C
    tnom = 27 C
    tempeffects = all
    gmindc = 1 pS
    dc: dc = 72 mV          (4 %), step = 36 mV           (2 %)
    dc: dc = 108 mV         (6 %), step = 36 mV           (2 %)
    dc: dc = 144 mV         (8 %), step = 36 mV           (2 %)
    dc: dc = 180 mV        (10 %), step = 36 mV           (2 %)
    dc: dc = 216 mV        (12 %), step = 36 mV           (2 %)
    dc: dc = 252 mV        (14 %), step = 36 mV           (2 %)
    dc: dc = 288 mV        (16 %), step = 36 mV           (2 %)
    dc: dc = 324 mV        (18 %), step = 36 mV           (2 %)
    dc: dc = 360 mV        (20 %), step = 36 mV           (2 %)
    dc: dc = 396 mV        (22 %), step = 36 mV           (2 %)
    dc: dc = 432 mV        (24 %), step = 36 mV           (2 %)
    dc: dc = 468 mV        (26 %), step = 36 mV           (2 %)
    dc: dc = 504 mV        (28 %), step = 36 mV           (2 %)
    dc: dc = 540 mV        (30 %), step = 36 mV           (2 %)
    dc: dc = 576 mV        (32 %), step = 36 mV           (2 %)
    dc: dc = 612 mV        (34 %), step = 36 mV           (2 %)
    dc: dc = 648 mV        (36 %), step = 36 mV           (2 %)
    dc: dc = 684 mV        (38 %), step = 36 mV           (2 %)
    dc: dc = 720 mV        (40 %), step = 36 mV           (2 %)
    dc: dc = 756 mV        (42 %), step = 36 mV           (2 %)
    dc: dc = 792 mV        (44 %), step = 36 mV           (2 %)
    dc: dc = 828 mV        (46 %), step = 36 mV           (2 %)
    dc: dc = 864 mV        (48 %), step = 36 mV           (2 %)
    dc: dc = 900 mV        (50 %), step = 36 mV           (2 %)
    dc: dc = 936 mV        (52 %), step = 36 mV           (2 %)
    dc: dc = 972 mV        (54 %), step = 36 mV           (2 %)
    dc: dc = 1.008 V       (56 %), step = 36 mV           (2 %)
    dc: dc = 1.044 V       (58 %), step = 36 mV           (2 %)
    dc: dc = 1.08 V        (60 %), step = 36 mV           (2 %)
    dc: dc = 1.116 V       (62 %), step = 36 mV           (2 %)
    dc: dc = 1.152 V       (64 %), step = 36 mV           (2 %)
    dc: dc = 1.188 V       (66 %), step = 36 mV           (2 %)
    dc: dc = 1.224 V       (68 %), step = 36 mV           (2 %)
    dc: dc = 1.26 V        (70 %), step = 36 mV           (2 %)
    dc: dc = 1.296 V       (72 %), step = 36 mV           (2 %)
    dc: dc = 1.332 V       (74 %), step = 36 mV           (2 %)
    dc: dc = 1.368 V       (76 %), step = 36 mV           (2 %)
    dc: dc = 1.404 V       (78 %), step = 36 mV           (2 %)
    dc: dc = 1.44 V        (80 %), step = 36 mV           (2 %)
    dc: dc = 1.476 V       (82 %), step = 36 mV           (2 %)
    dc: dc = 1.512 V       (84 %), step = 36 mV           (2 %)
    dc: dc = 1.548 V       (86 %), step = 36 mV           (2 %)
    dc: dc = 1.584 V       (88 %), step = 36 mV           (2 %)
    dc: dc = 1.62 V        (90 %), step = 36 mV           (2 %)
    dc: dc = 1.656 V       (92 %), step = 36 mV           (2 %)
    dc: dc = 1.692 V       (94 %), step = 36 mV           (2 %)
    dc: dc = 1.728 V       (96 %), step = 36 mV           (2 %)
    dc: dc = 1.764 V       (98 %), step = 36 mV           (2 %)
    dc: dc = 1.8 V        (100 %), step = 36 mV           (2 %)
Total time required for dc analysis `dc': CPU = 37.994 ms, elapsed = 38.655 ms.
Time accumulated: CPU = 3.86041 s, elapsed = 4.73907 s.
Peak resident memory used = 37.5 Mbytes.

modelParameter: writing model parameter values to rawfile.
element: writing instance parameter values to rawfile.
outputParameter: writing output parameter values to rawfile.
designParamVals: writing netlist parameters to rawfile.
primitives: writing primitives to rawfile.
subckts: writing subcircuits to rawfile.
```

# Post layout analysis
To create layout, make a new cell with name inverter of type layout then go to **Connectivity-> Generate -> All from source**, moving the components into the design area , the layout is generated as shown in the figure.

![Layout](https://github.com/user-attachments/assets/d89d14b0-ea8b-40b5-92ba-694fefe4feaa)

Now, LVS check is performed to ensure that the layout is identical to the schematic. To perform this, go to **Assura->Run LVS**.

![Assura_lvs](https://github.com/user-attachments/assets/2e825e1c-f305-4820-8cac-280e11e1113f)

The result of LVS check is as shown below:

![Assura_match](https://github.com/user-attachments/assets/f34f1626-d7b3-4f28-b6b0-fc3c3828b9d7)

To perform the Post layout analysis, the extracted view of the layout is generated that includes circuit connectivity alongwith parasitic components such as parasitic resistances and capacitances extracted from the physical layout. It is used for post layout simulations to ensure that the real-world implementation behaves as expected. To generate extracted view go to **Assura->Run RCX**. The extracted view is as follows:

![Layout_extracted](https://github.com/user-attachments/assets/bff04482-d858-46ff-9515-f811f5c75c08)

## Post layout DC analysis

Post layout DC analysis helps plot the VTC curve while considering parasitic components i.e in a non-ideal environment.

![Postlayout_dc](https://github.com/user-attachments/assets/ce829565-3975-42c3-80ae-bb7e2541d05d)

Calculation of VOH:

![Post_VOH_calculation](https://github.com/user-attachments/assets/5db78222-16a5-4d91-b004-6db6fd2047fe)

From the figure above, VOH = 1.7982V.

Calculation of VOL:

![Post_VOL_calculation](https://github.com/user-attachments/assets/b42ef26a-c4e9-45b4-b4e9-d52d75cb9dfd)

From the figure above, VOL = 14.892uV.

Calculation of VIL and VIH:

![Post_VIL_and_VIH_calculation](https://github.com/user-attachments/assets/3077d2b9-48bf-4556-85c6-fb90897be30a)

It can be inferred that VIL = 398.944mV and VIH = 885.437mV from the figure above.

Calculation of VTH:

![Post_VTH_calculation](https://github.com/user-attachments/assets/4cfdd3e2-a44d-43bb-9a9a-a526cbcf2292)

VTH = 700mV as inferred from the figure above.

### Calculation of Noise Margins

NML = VIL - VOL = 398.929mV

NMH = VOH - VIH = 912.763mV

## Post layout transient analysis

Post layout transient analysis simulates the time-dependent behavior of the CMOS inverter using the extracted layout. It applies a time-varying input and observes how the output voltage responds to it. It captures the dynamic performance of the circuit. The output of transient analysis is as shown below:

![Postlayout_transient](https://github.com/user-attachments/assets/892746de-02ed-42b0-85c9-4319f44c09aa)

### Calculation of Propagation delay

Calculation of Tplh:

![Postlayout_Tplh](https://github.com/user-attachments/assets/240f3c79-930e-4990-9ba6-0fe04a30ef66)

From the figure above, Tplh = 311.228ps.

Calculation of Tphl:

![Postlayout_Tphl](https://github.com/user-attachments/assets/94e41c90-d049-4a45-8f24-42703038ca89)

Tphl = 32.306ps, as inferred from the above figure.

Propagation delay, Tp = Tp = (Tplh + Tphl) / 2 = 171.767 ps.

### Calculation of Static and Dynamic power dissipation

Just like pre-layout calculation, we would have 2 values of static power dissipation due to existence of 2 states, HIGH and LOW. Similarly, 2 values of dynamic power dissipation are present due to 2 different types of possible state transitions, HIGH to LOW and LOW to HIGH.

![Post_power_dissipation](https://github.com/user-attachments/assets/24f6c607-ddfb-454b-8d4f-2590eb5d980f)

Average Static power disspation = (4.04 + 481.99) nW/ 2 = 243.015 nW

Average Dynamic power dissipation = (79.39 + 94.22) / 2 = 86.805 μW






























  


