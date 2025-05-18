---
title: "0.5mm Nozzle Guide"
type: docs
---

# 0.5mm Nozzle Specifications 🎯

## Why 0.5mm? Our Testing Journey

After extensive testing with various nozzle sizes, we discovered that the 0.5mm nozzle provides an optimal balance between quality, strength, and speed. Here's why:

{{< callout type="info" >}}
While testing the 0.6mm nozzle with PrusaSlicer's Arachne engine, we found that the 0.5mm nozzle offers better versatility, allowing for line widths from 0.4mm to 0.65mm from a single nozzle size. The 0.6mm nozzle was less effective at producing thinner 0.4mm lines.
{{< /callout >}}

## 🔄 Volumetric Flow Calculations

### Base Flow Rate
The Bigtreetech H2 V2S extruder has a maximum volumetric flow rate of:
- 600 mm³/min = 10 mm³/s

### Speed Formula
```
Max Speed = Volumetric Flow Rate ÷ (Layer Height × Extrusion Width)
```

## 📊 Maximum Speed Charts

### A. Outer Perimeter (0.4mm width)
| Layer Height | Max Speed |
|--------------|-----------|
| 0.1mm        | 250 mm/s  |
| 0.2mm        | 125 mm/s  |
| 0.3mm        | 83.3 mm/s |
| 0.4mm        | 62.5 mm/s |

### B. Internal/Infill (0.55mm width)
| Layer Height | Max Speed |
|--------------|-----------|
| 0.1mm        | 181.8 mm/s |
| 0.2mm        | 90.9 mm/s  |
| 0.3mm        | 60.6 mm/s  |
| 0.4mm        | 45.5 mm/s  |

## 🎯 Comprehensive Speed Matrix

Layer heights: 0.1mm to 0.4mm
Extrusion widths: 0.3mm to 0.65mm

| Layer Height | 0.3mm width | 0.4mm width | 0.5mm width | 0.6mm width | 0.65mm width |
|--------------|-------------|-------------|-------------|-------------|--------------|
| 0.1mm        | 333.3      | 250.0       | 200.0       | 166.7       | 153.8        |
| 0.2mm        | 166.7      | 125.0       | 100.0       | 83.3        | 76.9         |
| 0.3mm        | 111.1      | 83.3        | 66.7        | 55.6        | 51.3         |
| 0.4mm        | 83.3       | 62.5        | 50.0        | 41.7        | 38.5         |

## 🛠️ Practical Considerations

### Extrusion Width Guidelines

{{< tabs items="Thin Lines,Standard Lines,Wide Lines" >}}
  {{< tab "Thin Lines" >}}
  **0.3-0.4mm Width**
  - ✅ Ideal for fine details
  - ✅ Better for outer perimeters
  - ✅ Enables higher speeds
  - ⚠️ Less structural strength
  {{< /tab >}}
  {{< tab "Standard Lines" >}}
  **0.4-0.5mm Width**
  - ✅ Balanced quality and strength
  - ✅ Perfect for standard prints
  - ✅ Good layer adhesion
  - ✅ Versatile for most applications
  {{< /tab >}}
  {{< tab "Wide Lines" >}}
  **0.5-0.65mm Width**
  - ✅ Excellent for infill
  - ✅ Maximum strength
  - ✅ Best layer adhesion
  - ⚠️ Slower print speeds required
  {{< /tab >}}
{{< /tabs >}}

### 🎯 Optimal Combinations

{{< callout type="warning" >}}
Remember that these are theoretical maximums at 10mm³/s. Real-world speeds will be lower due to various factors.
{{< /callout >}}

1. **Fine Detail Printing**
   - Width: 0.3mm
   - Height: 0.1mm
   - Use Case: Miniatures, artistic prints

2. **Standard Quality**
   - Width: 0.4-0.5mm
   - Height: 0.2mm
   - Use Case: General purpose prints

3. **Speed/Strength Focus**
   - Width: 0.6-0.65mm
   - Height: 0.3mm
   - Use Case: Functional parts

### ⚠️ Real-World Limitations

Consider these factors when setting actual print speeds:
- Cooling requirements for different materials
- Corner acceleration limits
- Layer adhesion quality
- Mechanical printer limitations

## Navigation

{{< cards >}}
  {{< card link="../getting_started" title="Getting Started" subtitle="New to Lister? Start here with our comprehensive setup guide." >}}
  {{< card link="../specifications" title="Specifications" subtitle="Detailed technical specifications of the Lister 3D printer." >}}
  {{< card link="../trouble_shooting" title="Troubleshooting" subtitle="Common issues and their solutions." >}}
{{< /cards >}}