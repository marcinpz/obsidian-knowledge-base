## 📡 Protocols for DevOps

### 🌐 DNS (Domain Name System)

- **Purpose**: Resolves domain names (e.g., `example.com`) to IP addresses.
    
- **Port**: UDP 53 (primary), TCP 53 (for zone transfers)
    
- **Tools**: `dig`, `nslookup`, `bind`, `dnsmasq`
    
- **Examples**:
    
    - `dig google.com`
        
    - `nslookup github.com`
        
- **DevOps Relevance**:
    
    - Debugging service discovery
        
    - Managing DNS zones (esp. in cloud, e.g., Route 53)
        
    - Diagnosing network failures
        
- #networking #dns #debugging
    

---

### 🌍 HTTP / HTTPS (HyperText Transfer Protocol)

- **Purpose**: Communication protocol for web traffic
    
- **Port**: HTTP - TCP 80, HTTPS - TCP 443
    
- **Tools**: `curl`, `wget`, `httpie`, `nginx`, `Apache`
    
- **Examples**:
    
    - `curl -I https://example.com`
        
    - `http GET https://api.example.com`
        
- **DevOps Relevance**:
    
    - API communication and monitoring
        
    - Health checks (e.g., in Kubernetes)
        
    - Web server configuration and security (SSL/TLS)
        
- #http #api #web
    

---

### 📦 TCP (Transmission Control Protocol)

- **Purpose**: Reliable, connection-oriented communication
    
- **Examples**: SSH, HTTP/S, FTP, SMTP
    
- **Tools**: `telnet`, `nc`, `ss`, `tcpdump`
    
- **Examples**:
    
    - `telnet example.com 80`
        
    - `nc -vz host 443`
        
- **DevOps Relevance**:
    
    - Network performance tuning (e.g., latency, throughput)
        
    - Load balancers, firewalls
        
    - Port monitoring & connectivity testing
        
- #tcp #connectivity #networking
    

---

### 📡 UDP (User Datagram Protocol)

- **Purpose**: Unreliable, connectionless protocol for speed
    
- **Examples**: DNS, syslog, SNMP, VoIP
    
- **Tools**: `iperf`, `tcpdump`, `nc -u`
    
- **Examples**:
    
    - `nc -u example.com 514`
        
    - `iperf -u -c server`
        
- **DevOps Relevance**:
    
    - Lightweight telemetry or logging
        
    - Real-time streaming or metrics (e.g., Prometheus remote_write)
        
    - Troubleshooting DNS or network discovery issues
        
- #udp #metrics #telemetry
    

---

### 🔐 SSH (Secure Shell)

- **Purpose**: Secure remote shell access and tunneling
    
- **Port**: TCP 22
    
- **Tools**: `ssh`, `scp`, `rsync`, `ssh-agent`
    
- **Examples**:
    
    - `ssh user@server`
        
    - `scp file.txt user@host:/path/`
        
- **DevOps Relevance**:
    
    - Core remote management tool
        
    - Automation with SSH keys / `ssh-agent`
        
    - Port forwarding, bastion hosts
        
- #ssh #remote-access #security
    

---

### ✉️ SMTP, POP3, IMAP

- **Purpose**: Email transmission and retrieval
    
- **Ports**: SMTP - TCP 25/587/465, IMAP - TCP 143/993, POP3 - TCP 110/995
    
- **Tools**: `postfix`, `dovecot`, `swaks`, `msmtp`
    
- **Examples**:
    
    - `swaks --to user@example.com --server smtp.example.com`
        
- **DevOps Relevance**:
    
    - Email alerts and notifications
        
    - Email server monitoring
        
    - SPF, DKIM, DMARC setup
        
- #email #smtp #notifications
    

---

### 📊 SNMP (Simple Network Management Protocol)

- **Purpose**: Monitor and manage network devices
    
- **Port**: UDP 161 (data), 162 (traps)
    
- **Tools**: `snmpwalk`, `snmpget`, `net-snmp`
    
- **Examples**:
    
    - `snmpwalk -v2c -c public localhost`
        
- **DevOps Relevance**:
    
    - Infrastructure monitoring
        
    - Device health checks
        
    - Alerting
        
- #monitoring #snmp #network-devices
    

---

### 🔄 ICMP (Internet Control Message Protocol)

- **Purpose**: Network diagnostics (e.g., ping)
    
- **Tools**: `ping`, `traceroute`, `mtr`
    
- **Examples**:
    
    - `ping 8.8.8.8`
        
    - `traceroute google.com`
        
- **DevOps Relevance**:
    
    - Basic connectivity checks
        
    - Used in tools like `ping`, `traceroute`
        
    - Often filtered by firewalls – consider alternatives
        
- #icmp #diagnostics #connectivity
    

---