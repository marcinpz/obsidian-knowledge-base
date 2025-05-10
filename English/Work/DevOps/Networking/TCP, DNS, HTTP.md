### **TCP, DNS, and HTTP Explained**

**1. TCP (Transmission Control Protocol)**  
TCP is a transport-layer protocol (4) that ensures reliable, ordered, and error-checked delivery of data between devices. It establishes a connection using a three-way handshake before transmitting data. It’s like setting up a phone call before speaking.

**2. DNS (Domain Name System)**  
DNS is an application-layer (7) protocol used to resolve human-readable domain names (like `example.com`) into IP addresses (like `93.184.216.34`). Before your device can connect to a server, it uses DNS to find out where that server is on the internet.

**3. HTTP (HyperText Transfer Protocol)**  
HTTP is also an application-layer protocol (7). It is used by web browsers to communicate with web servers. Once TCP has established a connection, HTTP sends a request (e.g., `GET /index.html`) and receives a response (e.g., a webpage).

---

### **How They Work Together**

1. You type a URL into your browser.
    
2. The browser uses **DNS** to resolve the domain to an IP address.
    
3. It then establishes a **TCP** connection to that IP address.
    
4. Over this connection, it sends an **HTTP** request.
    
5. The server responds with the **HTTP** response (e.g., webpage content).
    

---

Would you like the same explanation in a printable one-pager format (PDF or DOC)?