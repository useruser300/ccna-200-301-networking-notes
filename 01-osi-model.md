## 1) What is a Network

A Network, in simple terms, is:
- A group of devices
- Connected through a specific medium
- To provide a specific service

These devices can be such as:
- Laptop
- Mobile
- Server

The medium used to connect these devices can be:
- Bluetooth
- Wi-Fi
- Cables
- Router
- Switch

The purpose of this connection is to provide a service, such as:
- File Transfer
- Browsing

For example, if we have a Laptop and a Server, the laptop needs a communication medium to reach the server.  
This medium could be a cable, Wi-Fi, or through a Switch or Router, depending on the network design.

---

## 2) OSI Model

The OSI Model consists of seven layers, and each layer has a specific function that helps in transferring data from one device to another.

### OSI Layers Overview

1. Physical Layer  
Responsible for transmitting raw bits over a physical medium (cables, signals).

2. Data Link Layer  
Handles frame delivery within the same network using MAC addresses.

3. Network Layer  
Provides logical addressing (IP) and routing between networks.

4. Transport Layer  
Ensures reliable or fast data delivery using TCP or UDP.

5. Session Layer  
Manages sessions between applications.

6. Presentation Layer  
Handles data formatting, encryption, and compression.

7. Application Layer  
Provides network services directly to user applications (HTTP, FTP, etc.).

When sending data from a laptop to a server, the process starts from top to bottom:
- Application Layer  
- Presentation Layer  
- Session Layer  
- Transport Layer  
- Network Layer  
- Data Link Layer  
- Physical Layer  

When receiving, the reverse happens. The receiving device starts from the bottom to the top until it understands the final request.

The format of the data also changes while moving down the layers:
- At Layer 7 → Data  
- At Layer 4 → Segments  
- At Layer 3 → Packets  
- At Layer 2 → Frames  

The main idea is that each layer adds its own information, then passes the data to the layer below.

### Beginning of Communication

When you type in a browser, for example:
- www.facebook.com  
- or www.wikipedia.com  

The device starts preparing a request to retrieve the desired page.

This request does not go all at once, but passes through multiple layers, and each layer adds its own part until the request is ready to be sent over the network.

---

## 3) Application Layer

The first important layer here is the Application Layer.

At this layer, a suitable protocol is used depending on the required service.

Examples of protocols:
- HTTP → for browsing  
- FTP → for file transfer  

A protocol is the language or method used by both sides to communicate with each other.

For example, if the laptop wants to request a page from Wikipedia, it needs a protocol that both the laptop and the server understand.  
In browsing, this protocol is HTTP.

So the laptop sends a request such as:
- I want this specific page  

The server may respond with:
- 200 OK → Page exists  
- 500 Server Problem → There is a server issue  

This layer is responsible for defining the type of request based on the service.

---

## Encapsulation

When each layer finishes its role, it adds its own header to the data, then passes it to the next layer.

This process is called:
**Encapsulation**

Meaning:
- Application → provides Data  
- Transport → adds Header  
- Network → adds Header  
- Data Link → adds Header  

When the data reaches the other side, these headers are removed in reverse order until the original request is obtained.

---

## 4) Transport Layer

This is Layer 4.

There are two important protocols here:
- TCP  
- UDP  

### TCP

TCP is a more reliable protocol.  
It is used when we need data to be delivered correctly and in order.

Examples:
- HTTP  
- FTP  

### UDP

UDP is faster, but it does not provide the same level of reliability and ordering as TCP.

Examples:
- Voice  
- Video  

### Functions of the Transport Layer

1. Session Establishment  
   Establishing a session between sender and receiver  

2. Session Management  
   Managing data transfer during the session  

3. Session Termination  
   Closing the session after communication ends  

4. Segmentation  
   Dividing large data into smaller pieces called Segments  

5. Sequencing  
   Assigning numbers to each segment so the receiver can reassemble them in order  

6. Error Detection / Correction  
   Detecting lost segments and requesting retransmission  

7. Flow Control  
   Controlling the amount of data sent based on the receiver’s capacity (e.g., Window Size)  

8. Port Addressing  
   Using:
   - Source Port  
   - Destination Port  

These are added to **every segment** inside the Transport Header, not just once for the whole request.

Each segment has:
- Source Port  
- Destination Port  

---

### Source Port / Destination Port

#### Source Port
Usually a temporary or random port chosen by the sender, typically from:
- 1024 to 65535  

#### Destination Port
A well-known port based on the service.

Examples:
- HTTP → 80  
- HTTPS → 443  
- SSH → 22  
- DNS → 53  

Example:  
If a laptop wants to browse a website using HTTP:
- Source Port may be 1025  
- Destination Port is 80  

If the user opens another tab to the same server:
- Source Port may become 1026  

This allows the device to distinguish between different sessions.

---

### TCP 3-Way Handshake

Before TCP starts sending data, it first establishes a session.

This happens through:
1. SYN  
2. SYN + ACK  
3. ACK  

Sequence:
- Laptop sends SYN  
- Server responds with SYN + ACK  
- Laptop responds with ACK  

Now the session is established and data transfer can begin.

This exchange also includes:
- Source Port  
- Destination Port  
- Window Size  

---

### Window Size

Window Size represents how many segments the receiver can accept at once.

Example:  
If the server says Window Size = 2  
It can receive Segment 1 and Segment 2 together, then send acknowledgment, then receive Segment 3.

This is part of Flow Control.

---

### Data Transmission in TCP

After session establishment:
- Data is divided into segments  
- Each segment is numbered  
- Each segment includes Source Port and Destination Port  
- Segments are sent to the receiver  
- Lost segments can be retransmitted  
- The receiver reassembles segments in order  

Thus, the full request arrives correctly.

---

### TCP 4-Way Handshake

When communication ends, the session is closed:

1. FIN  
2. ACK  
3. FIN  
4. ACK  

This ensures a proper and clean connection termination.

---

## 5) Network Layer

This is Layer 3.

Its main function:  
Assign logical addressing so data knows where to go across networks.

Here, the following are added:
- Source IP  
- Destination IP  

After this, the data is called:
**Packet**

Example:
- Source IP = Laptop IP  
- Destination IP = Server IP  

If:
- Laptop IP = 10.0.0.2  
- Server IP = 20.0.0.2  

The Network Layer includes these in the packet.

---

### Routed Protocol

Protocols that provide logical addressing:
- IPv4  
- IPv6  

---

### Routing Protocol

Protocols that help routers build routing tables:
- OSPF  
- BGP  
- Static Routing  

---

### Role of the Router

The router operates at Layer 3.

Its job:
Connect different networks.

Example:
- Network 10  
- Network 20  

If a packet is destined for Network 20, the router checks the Routing Table and decides:
- Which interface/port to send it through  

The router cares about:
- Destination IP  
- Target network  
- Best outgoing interface  

---

## 6) Data Link Layer

This is Layer 2.

Data Link Layer is used for hop-to-hop delivery of frames within the same network.

- MAC Address = Layer 2 (physical address)  
- Switch uses MAC Table to forward frames based on MAC Address  

Its function:  
Connect devices within the same network using MAC Addresses.

Here, the following are added:
- Source MAC  
- Destination MAC  

Now the data becomes:
**Frame**

---

### MAC Address

The MAC Address is a Layer 2 address.  
It is a physical address unique to each device or interface.

Examples:
- Laptop has a MAC  
- Server has a MAC  
- Router has a MAC per interface  
- Switch uses MAC addresses to forward frames  

---

### MAC Table

The switch uses:
**MAC Table**

It maps:
- MAC Address → Port  

Example:
- MAC A → Port 1  
- MAC B → Port 2  

If a frame arrives with Destination MAC = B  
The switch forwards it to Port 2.

---

### Why Destination MAC is Sometimes the Router

If the laptop wants to reach a device outside its network (e.g., Wikipedia):
- Destination IP = Server IP  
- Destination MAC (first hop) = Router MAC  

Because:
The laptop knows the destination is outside its network, so it sends the frame to the gateway (router).

So:
- IP stays end-to-end  
- MAC changes at every hop  

---

### Relationship Between IP and MAC

If the destination is inside the same network:
- Use the destination device’s MAC  

If outside:
- Destination IP = remote device  
- Destination MAC (first hop) = router  

Important:
- IP stays directed to final destination  
- MAC changes hop by hop  

---

## 7) End-to-End Process

On the laptop:

1. User types:  
   www.wikipedia.com  

2. Application Layer:  
   HTTP GET request is created  

3. Transport Layer:
   - Data is segmented  
   - Source Port and Destination Port are added  
   - Example:
     - Source Port = 1025  
     - Destination Port = 80  

4. Network Layer:
   - Source IP added  
   - Destination IP added  
   - Example:
     - Src IP = 10.x.x.x  
     - Dst IP = 20.x.x.x  

5. Data Link Layer:
   - Source MAC added  
   - Destination MAC added  
   - First hop → Destination MAC = router  

6. Switch forwards frame based on MAC Table  

7. Router:
   - Removes frame  
   - Checks Destination IP  
   - Re-encapsulates into new frame for next hop  

8. Request reaches server  

9. Server decapsulates:
   - Frame  
   - Packet  
   - Segment  
   - Data  

Finally, the Application Layer understands the request (Wikipedia page).

---

## 8) Lab

Using a tool like Wireshark and opening a site such as:
http://www.example.com  

You can observe outgoing packets.

You will see:
- Source IP  
- Destination IP  
- Source Port  
- Destination Port  
- TCP protocol  
- SYN / SYN-ACK / ACK  
- HTTP message  

Opening a packet shows layers:
- Application Layer  
- Transport Layer  
- Network Layer  
- Data Link Layer  

This proves that each layer actually adds its own information.

---

## Summary

A network consists of:
- Sender (Laptop)  
- Receiver (Wikipedia Server)  
- Switch (Layer 2)  
- Router (Layer 3)  

Full flow:
- User types URL  
- Application Layer prepares request  
- Transport Layer segments + adds ports  
- Network Layer adds IP addresses  
- Data Link Layer adds MAC addresses  
- Switch forwards via MAC Table  
- Router routes via Routing Table  
- Server receives and decapsulates  
- Server sends response back the same way  
