# tig

# STRICT PCB ROUTING BRIEF FOR HOME DIY FABRICATION (LUT / TONER TRANSFER METHOD)
# Target: Generate a 1-layer style layout optimized for home etching.
# Dimensions: 100mm x 50mm.

## STRICT MANUFACTURING CONSTRAINTS FOR TONER TRANSFER (LUT):
- SINGLE-SIDED PREFERENCE: Route 100% of signal and power traces on the BOTTOM layer only. Do not use top layer copper.
- NO VIAS: Do not generate any hidden or under-component via holes. If a collision occurs, use standard wire jumpers (0-ohm links) on the top layer.
- EXTRA WIDE TRACKS: 
  - Set default signal trace width to 0.8mm (minimum 0.6mm) to prevent over-etching.
  - Set power rails (+5V and GND) and welding terminal traces to 1.5mm width.
- LARGE CLEARANCE: Set minimum global clearance (trace-to-trace, trace-to-pad) to 0.6mm to prevent toner bleeding and short circuits during ironing.
- OVERSIZED PADS: All through-hole components (Arduino Nano, display, buttons, terminals) must use enlarged copper pads (minimum 2.5mm to 3.0mm diameter) with small inner holes (0.7mm) to act as a drill guide.

## Component Layout & Footprints Strategy:
- Microcontroller: 1x Arduino Nano (Standard through-hole DIP-30 module package).
- Display: 1x 3-digit 7-segment common cathode LED display (part 3631AGG or generic DIP).
- Surface Mount Placement: Place all 3x SOT-23 NPN transistors, 0603 resistors, and 0603 capacitors on the BOTTOM layer directly inline with the tracks for manual soldering.
- Through-Hole Placement: 4x 2-pin 5mm tactile switches, 3x 3mm status LEDs, and 2x 2-pin screw terminals (5.08mm pitch) are mounted from the TOP side.

## Netlist Pin-to-Pin Mapping:
1. Display Control:
   - Route Arduino Nano pins D9, D10, D11, D12, D13, A2, A3 through 0603 220-Ohm resistors directly to display segments A, B, C, D, E, F, G.
   - Connect multiplexing common cathodes DIG1, DIG2, DIG3 to the Collectors of the 3x SOT-23 NPN transistors.
   - Route Arduino Nano pins A4, A5, A6 to the Bases of these transistors via 0603 1k-Ohm resistors. Emitters connect to Arduino GND.
2. User Interface:
   - Route 4x buttons between Arduino pins D2, D3, D4, D5 and GND.
   - Route 3x 3mm LEDs from Arduino pins D6, D7, D8 to GND via 0603 220-Ohm series resistors.
3. Isolated Trigger Output:
   - Route Arduino pin A0 (D14) through a 220-Ohm resistor to the input LED of the first PC817 optocoupler.
   - Connect the photocoupler output phototransistor directly to the Torch terminal block. Place a 100-Ohm 0603 resistor inline with the Collector trace.
4. Isolated Arc Feedback Input:
   - Route the Arc Feedback terminal block to the second PC817 input LED pins (inline with a 1k-Ohm 0603 resistor).
   - Route the output phototransistor Collector to Arduino pin A1 (D15) with an 0603 10k-Ohm pull-up resistor to the Nano 5V pin. Emitter to GND.

## Anti-Interference & Copper Pour:
- Physical Ground Isolation: Split the board layout. The welding machine terminal tracks must be clustered at the far right edge, separated by a 6mm clear gap from the main Arduino digital area. No ground planes must bridge this barrier.
- Solid Copper Pour: Fill the entire Arduino digital zone with a massive GND copper pour. Use a clearance of 0.6mm from all tracks.
- Decoupling Capacitors: 
  - Position one 0603 0.1uF capacitor directly against the Arduino pin D2 track.
  - Position 0.1uF capacitors directly across pins 1-2 and pins 3-4 of the feedback optocoupler.
  - Position one 0.1uF capacitor directly across the output pins of the trigger optocoupler.
