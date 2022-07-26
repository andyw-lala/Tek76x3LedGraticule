![After Photo](images/After.jpg)
# Tek76x3LedGraticule
A project to retro-fit LED graticule lighting to Tektronix 76x3 scopes.

After retrofitting [LED graticule lighting in my 7904A](https://github.com/andyw-lala/Tek7904ALedGraticule) (which was in turn inspired by the white LED upgrade to a [Tek 7854 by Zenwizard Studios](https://youtu.be/GYkjuE7Pez8)), I decided to upgrade the graticule lights on my 7603 and 7633 scopes.

Attempts to take the simple route of just replacing the lamps with LEDs, as per [another excellent Zenwizard video](https://youtu.be/xNx9IgudV4Y) resulted in burnt out LEDs - eventually I added a dropping resistor, but was unhappy with the result - specifically the adjustment range, so I kept digging.
The control circuitry in the 76x3 scopes will current limit, so I initially investigated adjusting the current limit sense circuitry to limit the max current to a safe level for the LEDs, but that resulted in even less useful adjustment range from the front panel control.

Like the 7904A retrofit, this design completely replaces the existing incandescent graticule lamp driver circuit with a variable current source, while honoring the existing control mechanism.

## Theory of Operation
The 76x3 mainframes control the graticule illumination by means of a front panel variable resistor (R1095) and circuitry on the rectifier PCB (A11) at the rear of the unit. R1095 provides a voltage between -15V (graticule off) and +5V (graticule max). This voltage is applied to Q829, Q835, & Q827 and associated passives to provide a current limited variable voltage to three incandescent lamps that are wired in parallel. A single 4-way ribbon cable carries +15V, -15V, the control signal from R1095 and the output to the graticule light assembly. This cable mates with P891 on the rectifier board where the control circuit resides.

In a similar manner to the 7904A retrofit, the replacement circuit uses the same control signal (-15 to +5 volts) to control an approximately 0 - 20 mA current to ground that is used to drive the LEDs, which are re-wired to be in series.

The -15 to +5V control voltage from R1095 drives the base of T1, resulting in a 0 - 4 mA T1 collector current. In order drive a current to ground and preserve the wiring of the graticule assembly, this 0 - 4 mA control current is mirrored by T2, T3, & T4 acting as a [Wilson current mirror](https://en.wikipedia.org/wiki/Wilson_current_mirror), however due to the differing values of R3 & R4, the resultant current between the collector of T4 and ground varies between 0 and approximately 20 mA. As in the 7904A retrofit design, the exact fidelity of the current mirror is not important, so discrete, unmatched transistors are used.

Since all the required signals a present on the ribbon cable that normally connects to P891 on the rectifier board, a small PCB was designed to accept the ribbon cable instead. Installation comprises of removing the ribbon connection to P891 (which can be done without removing the power supply assembly from the case.)

The graticule light board (A13) is modified to replace the lamps with wide angle white LEDs,and to wire them in series.

## [Schematic](V1.pdf) (pdf)

## [BOM](BOM.md)

## Eagle Files
* [Schematic](V1.sch)
* [Board](V1.brd)

## Gerber Files
Here are generated gerbers, so you can use your PCB house of choice.
Note that I have only checked these with a viewer, I ordered my boards direct from OSHPark using the eagle board file. Send feedback if you use these files and they work or don't work.
* [Gerber zipfile](V1_gerbers.zip)

## Order Boards
You can order multiples of three known good boards directly from OSHpark (TODO)

## Installation
TODO

# Licence
All work here is covered by the MIT Licence, which is simple and permissive.

# Disclaimer
This mod worked well for me, and is presented here in the hope it can be as useful to others. However, do not undertake this unless you have the skills to perform the work safely and without damaging anything. You perform all work at your own risk, and I have no responsibility for any damage or injury whatsoever.
