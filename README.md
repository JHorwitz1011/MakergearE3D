# MakergearE3D

Components

Heater - https://e3d-online.com/high-temperature-heater-cartridges
65W @ 24V
RAMBo 1.3 MOSFETs can handle
Rated at 117W, 89A
Connector of heater is not compatible with the port on M3, potential mod?
Solution: Remove the old heater block wires from the screw terminal and replace with the 65W heater wires.
Zip tie through the back to the filament drive 

Heat Break - https://e3d-online.com/v6-titanium-heat-break-1-75mm
Lower heat conductivity
Maybe not necessary - requires further testing
Alternative: https://e3d-online.com/v6-heat-break
Plated Copper Heater Block - https://e3d-online.com/v6-plated-copper-heater-block
Aluminum heater blocks will soften at high temperatures

High Temp PTFE tubing - https://e3d-online.com/capricorn-bowden-tubing-100mm
For heat sink
Normal PTFE will melt with high temp. Materials such as PEEK

PT100 Temperature Sensor - https://e3d-online.com/pt100-temperature-sensor
Accurately reads temperatures up to 400 deg. C
Alternative: https://e3d-online.com/type-k-thermocouple-cartridge
Requires a different amplifier board

PT100 Amplifier Board - https://e3d-online.com/pt100-amplifier-board
Required for the PT100 Temperature Sensor to work
Requires Vcc and GND pins from RAMBo 1.3
Signal pin must be connected to analog input of RAMBo 1.3
Explained later


Threaded Heat Sink - https://e3d-online.com/v6-threaded-heatsink
Alternative groove mount: https://e3d-online.com/v6-heatsink-1-75mm-universal








Firmware Changes -  attached in Marlin firmware

Configuration.h

temperature sensor 1 changed to match signal from PT100 amplifier board.

pins_RAMBO.h

temp sensor 1 pin changed to match signal pin on analog pins input.






Hardware Changes

REFER TO Analog pins.png

        Blue circle - Analog Pins location on RAMBo 1.3 Board

        Yellow Wire - Signal wire of PT100 Amplifier Board to corresponding analog pin 5 in firmware (shown above)
        Black Wire - GND of Amplifier Board
        Orange Wire - Vcc of Amplifier Board

REFER TO Heater Pins.png 

        Heater 1 Screw Terminal - replaced with E3D Heater Cartridge wires (glossy black in the picture above)
        Third terminal from the bottom

GCode Changes
http://marlinfw.org/meta/gcode/
	These changes save to the EEPROM of the RAMBo board, and are not changed when updating the firmware of the board.  

Offset between nozzle - M218 command
T1 specifies extruder head, X/Y/Z specifies axis. 
For vertical adjustments, use Z.
-33.26 worked with an M3 with a normal T0, and a modded T1 with Ryan’s 3D printed mount
Negative values move the bed further from the hotend (down).

Printout from M503 

        M218 T1 X252.00 Y0.00 Z-33.26

http://marlinfw.org/docs/gcode/M218.html

Autotune PID - M303 

        M303 E1 S265 C10

This will run 10 cycles of PID autotuning based on 265 deg. C.
Copy the PID settings into M301, using P, I, and D before each number to change their respective values.



Printout from M503
M301 P15.33 I1.39 D42.38 C120.00 L20

http://marlinfw.org/docs/gcode/M303.html
http://marlinfw.org/docs/gcode/M301.html
