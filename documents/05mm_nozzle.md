# 0.5mm Nozzle
When it comes to 3D printing we want strength and quality. After did intensive testing with 0.6mm
nozzle size knowing Slicer software like (PrusaSlicer we use) gave layer widths to the slicer
with its Arachne engine. This gives us a wider range of nozzle use from a single nozzle size.

We later decided that a 0.5mm is a sweet spot, since it gives us a range from 0.4mm - 0.65mm widths
from a single nozzle. The 0.6mm did not like to go as low as 0.4mm.

This gives the advantage of both printing quality, strength and speed.

Let me help break this down step by step.

1. First, let's convert 600 mm³/min to mm³/s:
   600 ÷ 60 = 10 mm³/s volumetric flow rate (max flow rate of the Bigtreetech H2 V2S extruder)

2. Now, let's calculate maximum speeds for different layer heights:
The formula is: Max Speed = Volumetric Flow Rate ÷ (Layer Height × Extrusion Width)

For 0.5mm nozzle:
- Typical extrusion width = nozzle diameter × 1.1 = 0.55mm
- For outer perimeter at 0.4mm width

Calculations:
A. With 0.4mm extrusion width (outer perimeter):
- 0.1mm layer: 10 ÷ (0.1 × 0.4) = 250 mm/s
- 0.2mm layer: 10 ÷ (0.2 × 0.4) = 125 mm/s
- 0.3mm layer: 10 ÷ (0.3 × 0.4) = 83.3 mm/s
- 0.4mm layer: 10 ÷ (0.4 × 0.4) = 62.5 mm/s

B. With 0.55mm extrusion width (internal/infill):
- 0.1mm layer: 10 ÷ (0.1 × 0.55) = 181.8 mm/s
- 0.2mm layer: 10 ÷ (0.2 × 0.55) = 90.9 mm/s
- 0.3mm layer: 10 ÷ (0.3 × 0.55) = 60.6 mm/s
- 0.4mm layer: 10 ÷ (0.4 × 0.55) = 45.5 mm/s

Important considerations:
1. These are theoretical maximums - practical speeds will be lower due to:
   - Printer mechanical limitations
   - Cooling requirements for PLA
   - Acceleration/jerk limits
   - Print quality requirements

2. For PLA specifically:
   - Outer perimeters typically print best at 30-60 mm/s
   - Inner perimeters can go faster at 60-80 mm/s
   - Infill can go fastest at 80-150 mm/s

Using the same formula: Max Speed = 10 mm³/s ÷ (Layer Height × Extrusion Width)

Layer Height ranges: 0.1mm to 0.4mm
Extrusion Width ranges: 0.3mm to 0.65mm

Here's the matrix of maximum speeds (in mm/s):

| Layer Height | 0.3mm width | 0.4mm width | 0.5mm width | 0.6mm width | 0.65mm width |
|--------------|-------------|-------------|-------------|-------------|--------------|
| 0.1mm        | 333.3      | 250.0       | 200.0       | 166.7       | 153.8        |
| 0.2mm        | 166.7      | 125.0       | 100.0       | 83.3        | 76.9         |
| 0.3mm        | 111.1      | 83.3        | 66.7        | 55.6        | 51.3         |
| 0.4mm        | 83.3       | 62.5        | 50.0        | 41.7        | 38.5         |

Practical considerations:
1. Thinner extrusion widths (0.3-0.4mm):
   - Better for fine details and outer perimeters
   - Can achieve higher speeds
   - Less strength

2. Wider extrusion widths (0.5-0.65mm):
   - Better for infill and internal structures
   - Stronger parts
   - Must print slower
   - Better layer adhesion

3. Optimal combinations for different purposes:
   - Fine detail: 0.3mm width × 0.1mm height
   - Standard quality: 0.4-0.5mm width × 0.2mm height
   - Speed/strength: 0.6-0.65mm width × 0.3mm height

Remember, these are theoretical maximums at 10mm³/s. Real-world speeds will need to be lower to account for:
- Cooling requirements
- Corner acceleration limits
- Layer adhesion quality
- Mechanical printer limitations