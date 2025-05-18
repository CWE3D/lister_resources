---
title: "Moonraker Configuration"
type: docs
---

# Moonraker Component System Guide

## Core Concepts

### Component Definition
A Moonraker component is a modular piece of functionality that can be loaded and initialized by the server. Components are Python modules located in the `moonraker/components` directory.

### Key Requirements
1. Each component module must define a `load_component(config: ConfigHelper)` function
2. The load_component function returns an instance of the component class
3. Components may have an optional async `component_init()` method for post-initialization tasks

### Component Types
1. **Server Components**
   - Use the [server] section for configuration
   - Examples: application, websockets, klippy_connection

2. **Core Components**
   - Required for basic functionality 
   - Loaded in specific order
   - Examples: database, file_manager, klippy_apis, machine

3. **Optional Components**
   - Loaded if configured in moonraker.conf
   - Can fail without affecting core functionality

## Component Lifecycle

### 1. Loading
```python
def load_component(config: ConfigHelper):
    return ComponentClass(config)
```

### 2. Initialization Flow
1. Basic constructor initialization
2. Server components loaded first
3. Core components loaded in order
4. Optional components loaded
5. async component_init() called if exists
6. Configuration validated

### 3. Error Handling
- Components can raise ConfigError during load
- Failed components tracked in server.failed_components
- Optional components can fail without crashing server

## Configuration Helper

The ConfigHelper class provides robust configuration management:

### Key Methods
1. `get(option, default)` - Get string value
2. `getint(option, default)` - Get integer value
3. `getboolean(option, default)` - Get boolean value
4. `getfloat(option, default)` - Get float value
5. `getlist(option, default)` - Get list value
6. `getdict(option, default)` - Get dictionary value
7. `getsection(section)` - Get new ConfigHelper for section

### Special Features
1. Type validation and conversion
2. Range checking (min/max values)
3. Required vs optional parameters
4. Fallback values
5. Deprecation tracking

## Component Registration

Components can register:

### 1. Endpoints
```python
self.server.register_endpoint(
    "/component/path",
    RequestType.GET | RequestType.POST,
    callback_method
)
```

### 2. Remote Methods
```python
self.server.register_remote_method(
    "method_name",
    callback_method
)
```

### 3. Event Handlers
```python
self.server.register_event_handler(
    "event_name",
    callback_method
)
```

### 4. Notifications
```python
self.server.register_notification(
    "notification_name"
)
```

## Component Communication

Components can interact through:

1. **Direct Lookup**
```python
component = self.server.lookup_component("component_name")
```

2. **Event System**
```python
await self.server.send_event("event_name", *args)
```

3. **Remote Methods**
- Called through klippy_connection
- Allows bidirectional communication

## Best Practices

1. **Error Handling**
```python
try:
    # Component operation
except Exception as e:
    self.server.add_warning(
        f"Error in component: {str(e)}",
        warn_id="unique_id"
    )
```

2. **Cleanup**
```python
async def close():
    # Cleanup resources
    pass
```

3. **Configuration Validation**
- Always validate required options
- Provide sensible defaults
- Document configuration in comments

4. **Type Safety**
- Use type hints
- Validate input types
- Handle type conversion errors

## Component Template

Basic component structure:
```python
from __future__ import annotations
from typing import TYPE_CHECKING, Dict, Any

if TYPE_CHECKING:
    from confighelper import ConfigHelper

class NewComponent:
    def __init__(self, config: ConfigHelper) -> None:
        self.server = config.get_server()
        # Initialize from config
        
    async def component_init(self) -> None:
        # Async initialization
        pass
        
    async def close(self) -> None:
        # Cleanup
        pass

def load_component(config: ConfigHelper) -> NewComponent:
    return NewComponent(config)
```

## Important Notes

1. Components should be independent and loosely coupled

2. Core components are initialized synchronously in order

3. Optional components can be initialized asynchronously

4. Always provide proper error handling and cleanup

5. Use type hints and documentation

6. Follow the established naming conventions

7. Register endpoints/methods before server starts

8. Clean up resources in close() method

9. Validate configuration thoroughly

10. Use server.error for error handling

This guide provides the core understanding needed to create and maintain Moonraker components. Reference the specific component implementations for more detailed examples.

# Example Component
# Moonraker Component System Guide

## Core Concepts

### Component Definition
A Moonraker component is a modular piece of functionality that can be loaded and initialized by the server. Components are Python modules located in the `moonraker/components` directory.

### Key Requirements
1. Each component module must define a `load_component(config: ConfigHelper)` function
2. The load_component function returns an instance of the component class
3. Components may have an optional async `component_init()` method for post-initialization tasks

### Component Types
1. **Server Components**
   - Use the [server] section for configuration
   - Examples: application, websockets, klippy_connection

2. **Core Components**
   - Required for basic functionality 
   - Loaded in specific order
   - Examples: database, file_manager, klippy_apis, machine

3. **Optional Components**
   - Loaded if configured in moonraker.conf
   - Can fail without affecting core functionality

## Component Lifecycle

### 1. Loading
```python
def load_component(config: ConfigHelper):
    return ComponentClass(config)
```

### 2. Initialization Flow
1. Basic constructor initialization
2. Server components loaded first
3. Core components loaded in order
4. Optional components loaded
5. async component_init() called if exists
6. Configuration validated

### 3. Error Handling
- Components can raise ConfigError during load
- Failed components tracked in server.failed_components
- Optional components can fail without crashing server

## Configuration Helper

The ConfigHelper class provides robust configuration management:

### Key Methods
1. `get(option, default)` - Get string value
2. `getint(option, default)` - Get integer value
3. `getboolean(option, default)` - Get boolean value
4. `getfloat(option, default)` - Get float value
5. `getlist(option, default)` - Get list value
6. `getdict(option, default)` - Get dictionary value
7. `getsection(section)` - Get new ConfigHelper for section

### Special Features
1. Type validation and conversion
2. Range checking (min/max values)
3. Required vs optional parameters
4. Fallback values
5. Deprecation tracking

## Component Registration

Components can register:

### 1. Endpoints
```python
self.server.register_endpoint(
    "/component/path",
    RequestType.GET | RequestType.POST,
    callback_method
)
```

### 2. Remote Methods
```python
self.server.register_remote_method(
    "method_name",
    callback_method
)
```

### 3. Event Handlers
```python
self.server.register_event_handler(
    "event_name",
    callback_method
)
```

### 4. Notifications
```python
self.server.register_notification(
    "notification_name"
)
```

## Component Communication

Components can interact through:

1. **Direct Lookup**
```python
component = self.server.lookup_component("component_name")
```

2. **Event System**
```python
await self.server.send_event("event_name", *args)
```

3. **Remote Methods**
- Called through klippy_connection
- Allows bidirectional communication

## Best Practices

1. **Error Handling**
```python
try:
    # Component operation
except Exception as e:
    self.server.add_warning(
        f"Error in component: {str(e)}",
        warn_id="unique_id"
    )
```

2. **Cleanup**
```python
async def close():
    # Cleanup resources
    pass
```

3. **Configuration Validation**
- Always validate required options
- Provide sensible defaults
- Document configuration in comments

4. **Type Safety**
- Use type hints
- Validate input types
- Handle type conversion errors

## Component Template

Basic component structure:
```python
from __future__ import annotations
from typing import TYPE_CHECKING, Dict, Any

if TYPE_CHECKING:
    from confighelper import ConfigHelper

class NewComponent:
    def __init__(self, config: ConfigHelper) -> None:
        self.server = config.get_server()
        # Initialize from config
        
    async def component_init(self) -> None:
        # Async initialization
        pass
        
    async def close(self) -> None:
        # Cleanup
        pass

def load_component(config: ConfigHelper) -> NewComponent:
    return NewComponent(config)
```

## Important Notes

1. Components should be independent and loosely coupled

2. Core components are initialized synchronously in order

3. Optional components can be initialized asynchronously

4. Always provide proper error handling and cleanup

5. Use type hints and documentation

6. Follow the established naming conventions

7. Register endpoints/methods before server starts

8. Clean up resources in close() method

9. Validate configuration thoroughly

10. Use server.error for error handling

This guide provides the core understanding needed to create and maintain Moonraker components. Reference the specific component implementations for more detailed examples.

```python
from __future__ import annotations
import logging
import asyncio
from typing import TYPE_CHECKING, Dict, Any, Optional, List, Union

if TYPE_CHECKING:
    from ..confighelper import ConfigHelper
    from ..common import WebRequest
    from .klippy_apis import KlippyAPI
    from .database import MoonrakerDatabase
    from .file_manager import FileManager
    from .machine import Machine
    from .job_state import JobState
    from .template import TemplateFactory
    from .http_client import HttpClient
    from .websockets import WebsocketManager
    from .announcements import Announcements


class ExampleComponent:
    def __init__(self, config: ConfigHelper) -> None:
        # Server instance - provides access to core server functionality
        self.server = config.get_server()

        # Event loop - for scheduling async tasks
        self.event_loop = self.server.get_event_loop()

        # Component name from config section
        self.name = config.get_name()

        # Get config options with type conversion and validation
        self.update_interval = config.getfloat('update_interval', 1.0, above=0.)
        self.enabled = config.getboolean('enabled', True)
        self.retries = config.getint('retries', 3, minval=1)
        self.directories = config.getlist('watched_dirs', separator=',')
        
        # Template support
        self.cmd_template = config.gettemplate('command_template', None)
        
        # Register endpoints (HTTP/Websocket)
        self.server.register_endpoint(
            "/example/status", ['GET'], self._handle_status_request
        )
        self.server.register_endpoint(
            "/example/command", ['POST'], self._handle_command_request
        )
        
        # Register remote methods (called from Klipper)
        self.server.register_remote_method(
            "example_notification", self._handle_klippy_notification
        )
        
        # Register notification
        self.server.register_notification("example:status_update")

        # Register event handlers
        self.server.register_event_handler(
            "server:klippy_ready", self._handle_ready
        )
        self.server.register_event_handler(
            "server:klippy_shutdown", self._handle_shutdown
        )

        # Initialize state
        self.is_ready: bool = False
        self.last_status: Dict[str, Any] = {}
        self._update_timer = self.event_loop.register_timer(
            self._handle_timer_update
        )

    def get_status(self) -> Dict[str, Any]:
        """Return component status"""
        return {
            'enabled': self.enabled,
            'is_ready': self.is_ready,
            'last_status': self.last_status
        }

    async def _handle_status_request(self, web_request: WebRequest) -> Dict[str, Any]:
        """Handle status request endpoint"""
        return {
            'status': self.get_status(),
            # Access to other component status
            'klippy_status': self._get_klippy_status(),
            'job_status': self._get_job_status()
        }

    async def _handle_command_request(self, web_request: WebRequest) -> Dict[str, Any]:
        """Handle command request endpoint"""
        command = web_request.get_str('command')
        value = web_request.get_float('value', 0.)
        
        # Example of sending gcode
        if command == "move":
            await self._send_gcode(f"G1 X{value} F3000")
        
        # Example of getting printer objects
        elif command == "info":
            return await self._query_printer_objects()
            
        return {'ok': True}

    def _handle_klippy_notification(self, **kwargs) -> None:
        """Handle notification from Klipper"""
        self.last_status.update(kwargs)
        # Emit notification to clients
        self.server.send_event("example:status_update", kwargs)

    async def _handle_ready(self) -> None:
        """Handle Klippy ready event"""
        self.is_ready = True
        # Start update timer
        self._update_timer.start()

    async def _handle_shutdown(self) -> None:
        """Handle Klippy shutdown event"""
        self.is_ready = False
        self._update_timer.stop()

    async def _handle_timer_update(self, eventtime: float) -> float:
        """Periodic timer callback"""
        # Example of database usage
        db: MoonrakerDatabase = self.server.lookup_component('database')
        stored_data = db.get_item("example", "stored_value", None)
        
        # Example of template rendering
        if self.cmd_template is not None:
            rendered = await self.cmd_template.render_async({
                'eventtime': eventtime,
                'stored_data': stored_data
            })
            logging.info(f"Rendered template: {rendered}")

        # Return next interval
        return eventtime + self.update_interval

    def _get_klippy_status(self) -> Dict[str, Any]:
        """Example of accessing Klippy APIs"""
        kapis: KlippyAPI = self.server.lookup_component('klippy_apis')
        return {
            'klippy_connected': kapis.is_connected(),
            'klippy_state': str(kapis.get_klippy_state()),
        }

    def _get_job_status(self) -> Dict[str, Any]:
        """Example of accessing Job State"""
        job_state: JobState = self.server.lookup_component('job_state')
        return job_state.get_last_stats()

    async def _send_gcode(self, gcode: str) -> str:
        """Example of sending gcode command"""
        kapis: KlippyAPI = self.server.lookup_component('klippy_apis')
        return await kapis.run_gcode(gcode)

    async def _query_printer_objects(self) -> Dict[str, Any]:
        """Example of querying printer objects"""
        kapis: KlippyAPI = self.server.lookup_component('klippy_apis')
        query = {'toolhead': None, 'extruder': ['temperature']}
        return await kapis.query_objects(query)

    async def component_init(self) -> None:
        """Async initialization"""
        # Example of HTTP client usage
        client: HttpClient = self.server.lookup_component('http_client')
        try:
            resp = await client.get(
                "https://api.example.com/status",
                attempts=self.retries
            )
            resp.raise_for_status()
            self.last_status = resp.json()
        except Exception:
            logging.exception("Error fetching remote status")

        # Example of websocket notification
        wsm: WebsocketManager = self.server.lookup_component('websockets')
        wsm.notify_clients({'example_init': True})

        # Example of file manager usage
        file_manager: FileManager = self.server.lookup_component('file_manager')
        for directory in self.directories:
            if not file_manager.check_directory_exists(directory):
                logging.info(f"Creating directory: {directory}")
                await file_manager.mkdir(directory)

    async def close(self) -> None:
        """Component shutdown"""
        self._update_timer.stop()
        # Example of database update
        db: MoonrakerDatabase = self.server.lookup_component('database')
        db.insert_item("example", "last_shutdown", self.last_status)

def load_component(config: ConfigHelper) -> ExampleComponent:
    """Load component"""
    return ExampleComponent(config)
```

{{< cards >}}
  {{< card link="../klipper" title="Klipper Setup" subtitle="Set up and configure Klipper firmware." >}}
  {{< card link="../getting_started" title="Getting Started" subtitle="New to Lister? Start here with our comprehensive setup guide." >}}
  {{< card link="../trouble_shooting" title="Troubleshooting" subtitle="Common issues and their solutions." >}}
{{< /cards >}}