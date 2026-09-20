# tig

An Arduino Nano module controller for a 3-digit common-cathode 7-segment display, 4 user buttons, and isolated torch/arc-feedback I/O using optocouplers. 

STRICT ROUTING RULES FOR EASY SINGLE-SIDED HOME ETCHING (LUT):
1. Target a 1-layer style layout with routing restricted to the Bottom layer only.
2. If routing on a single layer is impossible without crossings, allow the Top layer to be used strictly for straight jumper wires (minimize top layer traces). 
3. Set global clearance to 0.4 mm and minimum signal trace width to 0.5 mm to allow traces to pass between component pads without violating DRC.
4. Set power and welding-terminal traces to 1.2 mm width.
5. Through-hole pad diameters must be 2.5 mm with a 0.7 mm drill guide.
6. Maintain a strict 6 mm isolation gap between the main microcontroller digital zone and the welding terminal area.
