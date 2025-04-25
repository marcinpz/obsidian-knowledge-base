# iproute in Linux for DevOps

## Overview

`iproute2` is a collection of utilities for managing networking in Linux. The `ip` command is a powerful tool replacing older utilities like `ifconfig`, `route`, and `netstat`.

Useful for DevOps tasks such as:

- Debugging network issues
    
- Configuring network interfaces
    
- Managing routing tables
    
- Setting up policy-based routing
    
- Isolating network environments
    
- Automating infrastructure with scripts
    

---

## Common `ip` Command Syntax

```bash
ip [ OPTIONS ] OBJECT { COMMAND | help }
```

- **OBJECT**: e.g., `addr`, `link`, `route`, `rule`
    
- **COMMAND**: e.g., `add`, `del`, `show`, `flush`
    

---

## Basic Usage Examples

### Show Network Interfaces

```bash
ip link show
```

### Show IP Addresses

```bash
ip addr show
```

### Assign IP Address

```bash
ip addr add 192.168.1.100/24 dev eth0
```

### Delete IP Address

```bash
ip addr del 192.168.1.100/24 dev eth0
```

### Bring Interface Up/Down

```bash
ip link set dev eth0 up
ip link set dev eth0 down
```

---

## Routing
### What is a Routing Table?

A **routing table** is a set of rules, stored in the kernel, that determines where network traffic should be directed. Each rule specifies a destination subnet, the next hop (gateway), and the network interface to use.

The system consults the routing table every time it sends a packet to decide the correct path.

Example:

```
Destination     Gateway         Interface
0.0.0.0/0       192.168.1.1     eth0
192.168.1.0/24  0.0.0.0         eth0
```

- `0.0.0.0/0` is the default route (for all destinations not matched by more specific routes).
    
- Traffic to 192.168.1.0/24 is sent directly via eth0.

### Show Routing Table

```bash
ip route show
```

### Add Route

```bash
ip route add 192.168.2.0/24 via 192.168.1.1 dev eth0
```

### Delete Route

```bash
ip route del 192.168.2.0/24
```

---

## Policy-Based Routing

### Show Rules

```bash
ip rule show
```

### Add Rule

```bash
ip rule add from 192.168.3.0/24 table 100
```

### Add Route to Table

```bash
ip route add default via 192.168.3.1 table 100
```

---

## Namespaces (Advanced)

### Create Network Namespace

```bash
ip netns add devops-ns
```

### Run Command in Namespace

```bash
ip netns exec devops-ns bash
```

---

## Use Cases & Examples

### 1. Debugging Connectivity in CI/CD Pipelines

Use `ip route` and `ip addr` to verify network configurations inside build containers.

```bash
ip netns exec ci-container ip route show
```

### 2. Multi-Homed Servers

Use `ip rule` and multiple routing tables to route traffic based on source IP.

```bash
ip rule add from 10.0.0.1 table 200
ip route add default via 10.0.0.254 dev eth1 table 200
```

### 3. Container Networking with Custom Namespaces

Use `ip netns` to simulate container networking without Docker/Podman.

```bash
ip netns add test-ns
ip link add veth0 type veth peer name veth1
ip link set veth1 netns test-ns
```

### 4. Interface Flapping Detection

Automate scripts using `ip link show` output to detect frequent interface up/down changes.

### 5. Custom Network Bootstrapping in Cloud Init

Use `ip` in cloud-init scripts to bring up interfaces, configure static IPs, or set routing rules.

```bash
ip link set eth0 up
ip addr add 172.31.0.10/20 dev eth0
ip route add default via 172.31.0.1
```

---

## Persistence of Network Configuration

The `ip` command modifies the **live system state** and does **not persist** changes after a reboot. To make configurations persistent, use the network management tool appropriate to your distro:

### Debian/Ubuntu (using `netplan` or `/etc/network/interfaces`)

**Netplan (modern):**

```yaml
network:
  version: 2
  ethernets:
    eth0:
      addresses:
        - 192.168.1.100/24
      gateway4: 192.168.1.1
      nameservers:
        addresses: [8.8.8.8, 1.1.1.1]
```

Then apply:

```bash
sudo netplan apply
```

**Legacy ifupdown:**

```bash
# /etc/network/interfaces
iface eth0 inet static
  address 192.168.1.100
  netmask 255.255.255.0
  gateway 192.168.1.1
```

### RHEL/CentOS/AlmaLinux (using `network-scripts` or `nmcli`)

**With ifcfg files:**

```bash
# /etc/sysconfig/network-scripts/ifcfg-eth0
BOOTPROTO=static
DEVICE=eth0
ONBOOT=yes
IPADDR=192.168.1.100
NETMASK=255.255.255.0
GATEWAY=192.168.1.1
```

**With NetworkManager:**

```bash
nmcli con mod eth0 ipv4.addresses 192.168.1.100/24
nmcli con mod eth0 ipv4.gateway 192.168.1.1
nmcli con mod eth0 ipv4.method manual
nmcli con up eth0
```

### systemd-networkd (common in minimal servers)

```ini
# /etc/systemd/network/10-eth0.network
[Match]
Name=eth0

[Network]
Address=192.168.1.100/24
Gateway=192.168.1.1
DNS=8.8.8.8
```

Then reload:

```bash
sudo systemctl restart systemd-networkd
```

---

## Tips

- Use `ip -c` for colored output.
    
- Combine with `watch` for real-time updates:
    

```bash
watch -n 1 ip addr
```

- Pair with `jq` and `awk` in scripts for parsing and automation.
    
- Replace legacy `ifconfig`, `route`, and `netstat` for more consistent scripting.
    

---

## References

- `man ip`
    
- [https://wiki.linuxfoundation.org/networking/iproute2](https://wiki.linuxfoundation.org/networking/iproute2)