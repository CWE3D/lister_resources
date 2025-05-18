---
title: "Klipper Setup"
type: docs
---

# Klipper System Documentation

## Table of Contents

1. [System Overview](#system-overview)
2. [Core Components](#core-components)
3. [Event System](#event-system)
4. [G-Code Processing](#g-code-processing)
5. [Plugin Development Guide](#plugin-development-guide)
6. [Common Use Cases](#common-use-cases)

## System Overview

Klipper is a 3D printer firmware that uses a host computer to do detailed motion planning and sends low-level commands to microcontroller boards. Here's how it works at a high level:

1. The host computer runs the main Klipper software (in Python)
2. It processes G-code commands and performs motion planning
3. Sends precise timing commands to microcontrollers
4. Microcontrollers execute these commands with exact timing

### Key Features

- Precise timing control
- Complex motion planning on host computer
- Event-driven architecture
- Plugin system for extensibility
- Multi-MCU support

## Core Components

### 1. Printer Object

The central object that manages the entire system. All major components are registered with and accessible through the printer object.

```python
class Printer:
    def __init__(self):
        self.objects = {}  # All registered components
        self.event_handlers = {}  # Event system
```

### 2. GCode Handler

Processes G-code commands and manages command queue:

```python
class GCodeDispatch:
    def __init__(self, printer):
        self.printer = printer
        self.gcode_handlers = {}  # Command handlers
        self.mux_commands = {}    # Multiplexed commands
```

### 3. Toolhead

Manages motion control and coordinates movement:

```python
class ToolHead:
    def __init__(self, config):
        self.printer = config.get_printer()
        self.max_velocity = config.getfloat('max_velocity', above=0.)
        self.max_accel = config.getfloat('max_accel', above=0.)
```

## Event System

Klipper uses an event system for component communication. Events are registered and handled through the printer object.

### Common Events

- `klippy:connect` - System startup
- `klippy:ready` - System is ready for operation
- `klippy:shutdown` - System shutdown
- `gcode:command_error` - G-code command error

### Example Usage

```python
def __init__(self, config):
    self.printer = config.get_printer()
    self.printer.register_event_handler("klippy:connect", self.handle_connect)

def handle_connect(self):
    # Called when system connects
    pass
```

## G-Code Processing

G-code commands go through several stages:

1. **Parsing** - Command is parsed into components
2. **Validation** - Parameters are validated
3. **Execution** - Command is executed
4. **Response** - Results are returned

### Command Registration

```python
def __init__(self, config):
    self.gcode = config.get_printer().lookup_object('gcode')
    self.gcode.register_command('MY_COMMAND', self.cmd_MY_COMMAND)

def cmd_MY_COMMAND(self, gcmd):
    # Handle command
    value = gcmd.get_float('PARAM', default=0.)
```

## Plugin Development Guide

### Basic Plugin Structure

```python
class MyPlugin:
    def __init__(self, config):
        self.printer = config.get_printer()
        # Register event handlers
        self.printer.register_event_handler("klippy:connect", self.handle_connect)
        # Register G-code commands
        gcode = self.printer.lookup_object('gcode')
        gcode.register_command("MY_COMMAND", self.cmd_MY_COMMAND)

    def handle_connect(self):
        # Initialization after connection
        pass

    def cmd_MY_COMMAND(self, gcmd):
        # Handle G-code command
        pass

def load_config(config):
    return MyPlugin(config)
```

### Accessing Printer Data

1. **Configuration Values**:
```python
class MyPlugin:
    def __init__(self, config):
        # Get config values
        self.speed = config.getfloat('speed', default=100.0)
        self.distance = config.getint('distance', default=10)
```

2. **Printer Components**:
```python
def get_printer_objects(self):
    # Access toolhead
    toolhead = self.printer.lookup_object('toolhead')
    current_pos = toolhead.get_position()
    
    # Access gcode interface
    gcode = self.printer.lookup_object('gcode')
    
    # Access kinematics
    kin = toolhead.get_kinematics()
```

3. **Status Information**:
```python
def get_status(self, eventtime):
    return {
        'speed': self.speed,
        'position': self.toolhead.get_position(),
        'status': self.current_status
    }
```

## Common Use Cases

### 1. Moving the Printer

```python
def move_example(self):
    toolhead = self.printer.lookup_object('toolhead')
    
    # Get current position
    current_pos = toolhead.get_position()
    
    # Move to new position [X, Y, Z, E]
    new_pos = [100, 100, 20, 0]
    toolhead.move(new_pos, speed=50)
```

### 2. Reading Sensors

```python
def read_sensor(self):
    # Access MCU ADC
    mcu = self.printer.lookup_object('mcu')
    pin = mcu.setup_pin('analog_in', 'PA0')
    value = pin.get_adc_value()
```

### 3. Creating Status Updates

```python
def get_status(self, eventtime):
    return {
        'temperature': self.current_temp,
        'target': self.target_temp,
        'power': self.heater_power
    }
```

### 4. Configuration File Example

```ini
[my_plugin]
# Required configuration
speed: 100.0
distance: 10

# Optional configuration
pin: PA0
max_temp: 100
```

## Best Practices

1. **Error Handling**:
```python
def validate_conditions(self):
    if not self.is_ready:
        raise self.printer.command_error("Printer not ready")
```

2. **Event Handling**:
```python
def register_events(self):
    self.printer.register_event_handler("klippy:connect", self.handle_connect)
    self.printer.register_event_handler("klippy:ready", self.handle_ready)
```

3. **Command Registration**:
```python
def register_commands(self):
    self.gcode = self.printer.lookup_object('gcode')
    self.gcode.register_command(
        'MY_COMMAND', 
        self.cmd_my_command,
        desc="Command description"
    )
```

4. **Status Updates**:
```python
def get_status(self, eventtime):
    return {
        'status': self.current_status,
        'value': self.sensor_value
    }
```

This documentation provides a foundation for understanding Klipper's architecture and developing plugins. For more specific use cases or detailed information about particular components, refer to the Klipper source code or existing plugins.

{{< cards >}}
  {{< card link="../moonraker" title="Moonraker Configuration" subtitle="Configure Moonraker for your Klipper setup." >}}
  {{< card link="../getting_started" title="Getting Started" subtitle="New to Lister? Start here with our comprehensive setup guide." >}}
  {{< card link="../trouble_shooting" title="Troubleshooting" subtitle="Common issues and their solutions." >}}
{{< /cards >}}