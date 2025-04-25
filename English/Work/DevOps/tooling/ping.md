# Ping Tool Basics

## Overview
- **Purpose**: Tests network reachability between two devices
- **Protocol**: Uses ICMP (Internet Control Message Protocol) Echo Request/Reply
- **Common Use**: Diagnose connectivity issues, measure latency

## Syntax
```bash
ping [options] <destination>
```
- `<destination>`: IP address (e.g., 8.8.8.8) or hostname (e.g., google.com)

## Key Options
- `-c <count>`: Limit number of pings (e.g., `ping -c 10 google.com`)
- `-i <interval>`: Set time between pings in seconds (e.g., `-i 0.5`)
- `-t <ttl>`: Set Time To Live (e.g., `-t 64`)
- `-s <size>`: Specify packet size in bytes (e.g., `-s 100`)

## Output Explained
Example:
```
PING google.com (142.250.190.78): 56 data bytes
64 bytes from 142.250.190.78: icmp_seq=0 ttl=117 time=15.234 ms
```
- **64 bytes**: Size of reply packet
- **icmp_seq**: Sequence number of the ping
- **ttl**: Time To Live remaining (hops left)
- **time**: Round-trip latency in milliseconds

## Practical Examples
1. **Basic Ping**:
   ```bash
   ping google.com
   ```
   - Continuous ping until stopped (Ctrl+C)
2. **Limited Ping**:
   ```bash
   ping -c 5 8.8.8.8
   ```
   - Sends 5 pings to Google's DNS server
3. **Fast Ping**:
   ```bash
   ping -i 0.2 -c 10 localhost
   ```
   - Pings localhost 10 times, 0.2s apart

## Troubleshooting with Ping
- **No response**: Host unreachable, firewall blocking, or network down
- **High latency**: Network congestion or routing issues
- **Packet loss**: Unstable connection (check % loss in summary)

## DevOps Notes
- Automate `ping` in scripts to monitor uptime
- Use with tools like Nagios or Prometheus for alerting
- Be aware: Some servers block ICMP (ping might fail despite being up)

> **Tip**: On Windows, `ping` runs 4 times by default, no `-c` needed!