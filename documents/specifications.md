# CWE3D Lister 3D Printer Specifications

## General Specifications

| Specification | Value |
|---------------|-------|
| Weight | 23kg |
| Default Max Acceleration | 3000 mm/s² |
| Default Max Velocity | 300 mm/s |
| Printable Area | 250mm x 250mm x 240mm |
| Dimensions | Height: 577mm<br>Width: 460mm<br>Length: 520mm |

## Frame and Construction

- **Frame Type**: CoreXY system
- **Frame Material**: Aluminum profile PG2020/40
- **Assembly**: Simple assembly and disassembly
- **Fasteners**: Over 400 quality stainless steel screws (M3, M4, M5, M6)
- **Additional Features**:
  - Anti-vibration feet
  - Chromed steel T-nuts
  - Open frame design for easy access and maintenance

## Gantry System

- **Belt System**: GT2 6mm belt drive
- **Pulleys**: GT2 idler pulley 20 teeth
  - 14x pulley alignment system
  - Simple belt tensioners
- **Linear Motion**:
  - Linear Rod Bearing (8mm) LM8LUU
  - 8mm hardened chromium steel rods
- **Homing**: Sensorless homing on all axes (X, Y, Z)

## Z-Axis System

- **Z-Axis Motion**: Dual ballscrew system
  - 2x Ballscrew bearing SFU 1204 (12mm w/ 4mm pitch)
  - 350mm long stainless steel
- **Z-Axis Support**:
  - 4x 12mm hardened chromium linear rod system
  - 5-6mm thickness base bed plate connecting 12mm rod brackets to bed
- **Coupler**: 5mm to 8mm aluminum flexible clamp coupler with single roller bearing pivot
- **Additional Features**:
  - Stepper supported Z thrust bearings decreasing stress from stepper bearings

## Print Bed

- **Bed Size**: 250mm x 250mm x 240mm (h)
- **Bed Material**: 300mm x 300mm Super flat Garolite F4 base
- **Bed Construction**:
  - 300mm x 300mm bed insulation
  - PG2020 construction
  - 1.5mm aluminum heat spreader
  - 260 x 260mm insulation
- **Bed Flatness**: Can be as flat as 0.14mm on lowest and highest point
- **Heating**:
  - 250W 250mm x 250mm isolated silicone heat pad
  - 80°C max heated bed surface (magnet starts degrading over 85°C)
- **Print Surface**: PEI flexible bed printing surface with rough texture
- **Bed Leveling**:
  - 8mm bed level induction probe
  - 4x aluminum level adjustment wheels with Silicone Heater Bed Standoff
  - Center level adjustment wheel
  - Auto bed leveling with bed mesh measuring and dynamic bed probing

## Extruder and Hot End

- **Extruder**: Bigtreetech H2 V2S Direct Drive Extruder
  - Extrusion Method: Dual Gear Extrusion
  - Maximum Printing Temperature: 270°C (Upgradable)
  - Weight: 198g (excluding wiring)
  - Maximum Extrusion Force: 770 N (approximately 7.5 kg)
  - Filament Diameter and Tolerance: 1.75 ± 0.05 mm
  - Extrusion Speed: Up to 600 mm³/min (depending on filament type)
- **Nozzle**: 0.6mm Hardened Steel Nozzle
- **Cooling**: 5015 24V part cooling blower

## Electrical System

- **Controller Board**: Bigtreetech SKR Pro V1.2
  - 32-bit ARM Cortex-M4 processor with 256KB of RAM
  - TMC 2209 silent stepper drivers
  - Multiple safeguard measures
  - 16 GB SD card
- **Power Supply**: 24V Mean Well power supply (350W) LRS-350-24
- **Stepper Motors**: 4x Wantai Nema 17 (42BYGHM810) 0.9 degree 2.4A
- **Raspberry Pi**: 3B+/4/5 1GB/2GB version with 32GB SD Card
- **Additional Components**:
  - 24V to 5V 5A stepdown for Raspberry Pi
  - Fotek SSR-25 DA Solid State Relay AC/DC for 250W bed heating pad
  - 3mm Aluminum electrical panel backplate 450mm x 410mm
  - 48 point terminal block 600V 15A patch panel
  - IEC Socket + Switch (With replaceable fuse cartridge)
  - LED print surface spotlight
- **Wiring**: Full wiring solder connections, hidden for aesthetics
- **Electrical Trunking**: Fully enclosed system for wire organization

## Software and Control

- **Operating System**: RatOS (Raspberry Pi based)
- **Firmware**: Klipper with Mainsail interface
- **Lister Plugins**:
  - Lister printables (all updated printer parts)
  - Lister config (all firmware and macros)
  - Lister control (numpad shortcut control)
- **User Interface**: Web interface and Mobile/Tablet interface

## Filament Compatibility

- Optimized for filaments that:
  - Don't require a heated chamber
  - Are less prone to warping
  - Don't need bed temperatures exceeding 90°C

### Compatible Filaments:
1. PLA variants (Standard, PLA+, filled PLAs, specialty PLAs)
2. PETG and its variants (including CF and GF reinforced)
3. TPU/TPE (up to 95A hardness)
4. PVA (for soluble supports)
5. PCTG
6. Some low-warp nylon blends
7. Various specialty and bio-based filaments

## Additional Features

- **Filament Runout Sensor**: Included
- **Sensorless Homing**: Full axis XYZ homing without physical end-stops
- **Upgradability**: Frame designed to accommodate future enhancements
- **Open Source**: Full access to CAD files, firmware, and documentation
- **Noise Level**: Quiet operation with noticeable but elegant stepper coil humming

## Printer Components Materials

- eSun ePLA-ST for most parts
- eSun PETG for black back panels
- Bamboo Labs PETG-CF for brackets
- eSun TPU 95A for anti-vibration feet

This comprehensive specification list covers all the key aspects of the CWE3D Lister 3D Printer, highlighting its unique features and capabilities.