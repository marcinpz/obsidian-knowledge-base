# Bash Basics for DevOps

Essential Bash scripting concepts for DevOps tasks

## 1. Variables and Input
```bash
# Variables
SERVER_NAME="web01"
PORT=8080

# Array
SERVERS=("web01" "web02" "web03")

# User input
read -p "Enter server name: " INPUT_SERVER
```

## 2. Control Flow
```bash
# If-else for service status
STATUS_CODE=200
if [ $STATUS_CODE -eq 200 ]; then
    echo "Service is UP"
elif [ $STATUS_CODE -eq 503 ]; then
    echo "Service Unavailable"
else
    echo "Unknown status"
fi

# For loop for server checks
for SERVER in "${SERVERS[@]}"; do
    echo "Checking $SERVER"
done
```

## 3. Functions
```bash
# Function to check disk space
check_disk_space() {
    THRESHOLD=$1
    USAGE=$(df -h / | awk 'NR==2 {print $5}' | cut -d'%' -f1)
    if [ $USAGE -gt $THRESHOLD ]; then
        echo "Warning: Disk usage at ${USAGE}%"
    else
        echo "Disk usage OK: ${USAGE}%"
    fi
}

# Usage
check_disk_space 80
```

## 4. File Operations
```bash
# Reading config file
CONFIG_DATA=$(cat config.txt)

# Writing to log file
echo "Deployment started" >> deploy.log

# Check if file exists
if [ -f "config.txt" ]; then
    echo "Config found"
fi
```

## 5. Error Handling
```bash
# Check command success
if ! ping -c 1 "web01" > /dev/null 2>&1; then
    echo "Ping failed"
    exit 1
fi

# Trap errors
trap 'echo "Error occurred"; exit 1' ERR
```

## 6. System Commands
```bash
# Process info
ps aux | grep nginx

# Disk usage
df -h /

# Network status
netstat -tuln

# System uptime
UPTIME=$(uptime -p)
echo "System $UPTIME"
```

## 7. Simple DevOps Example
```bash
#!/bin/bash

# Service monitoring script
monitor_service() {
    SERVICE=$1
    PID_FILE="/var/run/${SERVICE}.pid"
    
    if [ -f "$PID_FILE" ]; then
        PID=$(cat "$PID_FILE")
        if ps -p "$PID" > /dev/null; then
            echo "$SERVICE is running (PID: $PID)"
        else
            echo "$SERVICE PID exists but not running"
        fi
    else
        echo "$SERVICE is not running"
    fi
}

# Usage
monitor_service "nginx"
```

## DevOps-Relevant Tips
- Use `#!/bin/bash` shebang
- Quote variables `"$VAR"` to handle spaces
- Redirect errors with `2>/dev/null`
- Use `&&` and `||` for command chaining
- Add comments with `#`
- Make scripts executable: `chmod +x script.sh`

## Next Steps
- Learn about:
  - Cron scheduling
  - SSH commands
  - Systemd integration
  - Log parsing with grep/awk/sed