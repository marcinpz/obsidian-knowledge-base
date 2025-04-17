# Python Basics for DevOps

## Introduction
Python is a versatile and widely-used programming language in DevOps. It is known for its simplicity, readability, and extensive libraries that make automation, scripting, and infrastructure management easier.

## Why Python for DevOps?
- **Automation**: Automate repetitive tasks like deployments, backups, and monitoring.
- **Scripting**: Write scripts to manage servers, containers, and cloud resources.
- **Integration**: Integrate with APIs, databases, and DevOps tools like Ansible, Jenkins, and Kubernetes.
- **Cross-Platform**: Python works seamlessly across different operating systems.

## 1. Variables and Data Types

```python
# Basic variable types
server_name = "web01"              # String
port = 8080                        # Integer
is_active = True                   # Boolean
cpu_usage = 75.5                   # Float

# Collections
servers = ["web01", "web02"]       # List
ports = (80, 443)                  # Tuple (immutable)
config = {"port": 80, "active": True}  # Dictionary
```

## 2. Control Flow

```python
# If-else for service status
status_code = 200
if status_code == 200:
    print("Service is UP")
elif status_code == 503:
    print("Service Unavailable")
else:
    print("Unknown status")

# Loops for server checks
servers = ["web01", "web02", "web03"]
for server in servers:
    print(f"Checking {server}")
```

## 3. Functions

```python
def check_disk_space(threshold=80):
    usage = 75  # Simulated disk usage
    if usage > threshold:
        return f"Warning: Disk usage at {usage}%"
    return f"Disk usage OK: {usage}%"

# Function with multiple parameters
def deploy_app(app_name, version, env="prod"):
    return f"Deploying {app_name} v{version} to {env}"
```

## 4. File Operations

```python
# Reading config file
with open("config.txt", "r") as file:
    config_data = file.read()

# Writing log file
with open("deploy.log", "a") as file:
    file.write("Deployment started\n")
```

## 5. Error Handling

```python
try:
    # Attempt to connect to server
    connection = open_connection("web01")
except ConnectionError as e:
    print(f"Connection failed: {e}")
except Exception as e:
    print(f"Unexpected error: {e}")
finally:
    print("Cleanup complete")
```

## 6. Working with Modules

```python
# Import built-in modules
import os
import sys
import time

# Import specific functions
from datetime import datetime

# Check if file exists
if os.path.exists("/etc/config"):
    print("Config found")

# Get current timestamp
current_time = datetime.now()
```

## 7. Simple DevOps Example

```python
import os
import time

def monitor_service(service_name):
    # Simulate service check
    pid_file = f"/var/run/{service_name}.pid"
    
    if os.path.exists(pid_file):
        uptime = time.time() - os.path.getctime(pid_file)
        return f"{service_name} is running (Uptime: {uptime/3600:.2f} hours)"
    else:
        return f"{service_name} is not running"

# Usage
print(monitor_service("nginx"))
```

## DevOps-Relevant Tips

- Use `os` module for system operations
- Use `sys` for command-line arguments
- Use `time`/`datetime` for scheduling
- Keep functions small and focused
- Add comments for maintenance
- Use meaningful variable names

## Next Steps

- Learn about:
   - Python package management (pip)
   - Virtual environments
   - Working with APIs
   - Automation libraries (e.g., paramiko, fabric)

---
Tags
#Python #DevOps #Programming #Automation #Scripting #Infrastructure #Cloud