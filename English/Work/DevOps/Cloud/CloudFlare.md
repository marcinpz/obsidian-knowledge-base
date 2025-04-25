# 🌐 Cloudflare Basics

## 🧠 What is Cloudflare?
Cloudflare is a global network and platform that provides security, performance, and reliability services for websites and applications.

---

## 🚀 Core Features

### 1. DNS Management
- Acts as an authoritative DNS provider.
- Super fast global DNS propagation.
- Lets you proxy traffic through Cloudflare.

### 2. CDN (Content Delivery Network)
- Caches static assets at edge locations.
- Reduces latency and load on origin servers.

### 3. DDoS Protection
- Automatic detection and mitigation.
- Always-on protection at no extra cost (even on free plan).

### 4. SSL/TLS
- Free SSL certificates (Flexible, Full, Full Strict).
- TLS termination and HTTPS redirection.

### 5. Firewall Rules
- Custom security rules by IP, country, path, headers, etc.
- Rate limiting and challenge pages (CAPTCHA / JS).

### 6. Page Rules
- Define behaviors for specific URLs (e.g., cache level, redirects, HTTPS enforce).

---

## 🧰 Useful Tools

- **Analytics** – traffic stats, cache hits, threats blocked.
- **Workers** – serverless code at the edge (e.g., redirect, rewrite, transform).
- **Zero Trust** – identity-aware access to internal apps.
- **Access** – secure apps with identity provider (SSO, MFA).
- **Tunnel (Cloudflared)** – expose local apps securely.

---

## 🔒 Security Notes

- Hide origin IP if proxy is enabled (orange cloud ☁️ in DNS).
- Use Firewall Rules to block countries, IP ranges, bots.
- Enable “Under Attack Mode” during heavy abuse.

---

## 📦 Plans Overview

| Plan       | Price     | Key Features                          |
|------------|-----------|----------------------------------------|
| Free       | $0        | CDN, SSL, DDoS, DNS                    |
| Pro        | $20/mo    | Extra firewall rules, image optimization |
| Business   | $200/mo   | Custom WAF rules, prioritized support |
| Enterprise | Custom    | Advanced features, SLAs, BYO IP        |

---

## 📁 Common CLI Commands (Cloudflared)

```bash
# Install
brew install cloudflare/cloudflare/cloudflared

# Create a tunnel (local -> cloud)
cloudflared tunnel create my-tunnel

# Connect to local app (e.g., HA on port 8123)
cloudflared tunnel route dns ha.example.com

# Start tunnel
cloudflared tunnel run my-tunnel