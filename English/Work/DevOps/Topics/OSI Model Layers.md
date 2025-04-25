# OSI Model Layers

The OSI (Open Systems Interconnection) model defines seven layers of network functionality.

## 7. Application Layer

- **Function**: Provides network services directly to end-user applications.
- **Examples**: HTTP, FTP, SMTP, DNS.
- **Key Role**: User interface, data exchange (e.g., web browsing, email).

## 6. Presentation Layer

- **Function**: Translates data between application and network formats.
- **Examples**: Encryption (SSL/TLS), compression, data formatting (JPEG, ASCII).
- **Key Role**: Ensures data is readable, handles encryption/decryption.

## 5. Session Layer

- **Function**: Manages sessions between applications.
- **Examples**: NetBIOS, RPC, session establishment in TCP.
- **Key Role**: Establishes, maintains, and terminates communication sessions.

## 4. Transport Layer

- **Function**: Provides reliable data transfer and flow control.
- **Examples**: TCP, UDP.
- **Key Role**: Ensures complete data delivery, error checking, segmentation.

## 3. Network Layer

- **Function**: Handles logical addressing and routing.
- **Examples**: IP (IPv4, IPv6), ICMP, routers.
- **Key Role**: Determines best path for data across networks.

## 2. Data Link Layer

- **Function**: Ensures error-free data transfer between adjacent nodes.
- **Examples**: Ethernet, Wi-Fi (802.11), MAC addresses, switches.
- **Key Role**: Frames data, handles physical addressing, error detection.

## 1. Physical Layer

- **Function**: Transmits raw bits over physical medium.
- **Examples**: Cables (Ethernet, fiber), hubs, repeaters, bit encoding.
- **Key Role**: Defines hardware specifications (voltages, frequencies).

---

**Note**: Each layer interacts with the layers directly above and below it, abstracting complexity for higher layers.

