# Networking Basics for DevOps/Programmers

## Core Concepts

- **IP Addresses**: Unique identifiers for devices on a network
   - IPv4: 32-bit (e.g., 192.168.1.1)
   - IPv6: 128-bit (e.g., 2001:0db8::1)

- **Subnetting**: Dividing networks into smaller segments
   - CIDR notation (e.g., /24 = 255.255.255.0)

- **Ports**: Endpoints for communication (0-65535)
   - Well-known: 0-1023 (e.g., 80 for HTTP)
   - Ephemeral: Dynamic, high-range ports

## Protocols

- **TCP**: Reliable, connection-oriented (e.g., HTTP, SSH)
- **UDP**: Fast, connectionless (e.g., DNS, streaming)
- **HTTP/HTTPS**: Web communication (ports 80, 443)
- **DNS**: Resolves names to IPs (port 53)
- **SSH**: Secure remote access (port 22)

## Tools for DevOps

- **[[ping]]**: Test reachability
- **traceroute** (or `tracert` on Windows): Trace packet path
- **netstat**: Network statistics
- **nslookup/dig**: DNS queries
- **curl**: Test HTTP requests
- **tcpdump/wireshark**: Packet analysis

## Networking in Practice

- **Load Balancers**: Distribute traffic (e.g., NGINX, HAProxy)
- **Firewalls**: Control traffic (e.g., [[iptables]], AWS Security Groups)
- **VPNs**: Secure remote access
- **Containers & Networking**: Docker bridges, [[Kubernetes overlays]]

## Key Terms

- **Latency**: Delay in data transfer
- **Bandwidth**: Data rate capacity
- **NAT**: Network Address Translation
- **Proxy**: Intermediary for requests

## Troubleshooting Tips

1. Check connectivity (`ping`)
2. Verify DNS (`nslookup`)
3. Inspect ports (`netstat -tuln`)
4. Trace routes (`traceroute`)
5. Analyze packets (`tcpdump`)

> **Note**: In DevOps, automate network configs with tools like Ansible or Terraform!