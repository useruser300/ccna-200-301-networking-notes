# DHCP / DNS / ARP / Default Gateway

## 1) The Basic Idea

When a Client wants to send data to a Web Server, it needs four pieces of information:

```text
SRC IP
DST IP
SRC MAC
DST MAC
```

At Layer 3, we need:

```text
Source IP
Destination IP
```

And at Layer 2, we need:

```text
Source MAC
Destination MAC
```

The important rule is:

```text
IP  = End-to-End
MAC = Hop-to-Hop
```

---

## 2) What Happens Before Transmission?

If the Client wants to open a website:

At Layer 7, the following is prepared:

```text
HTTP Request
```

At Layer 4, TCP adds:

```text
Source Port      = Random Port
Destination Port = 80
```

After that, Layer 3 needs:

```text
Source IP
Destination IP
```

Then Layer 2 needs:

```text
Source MAC
Destination MAC
```

---

## 3) Source MAC

The Source MAC comes from the NIC inside the device.

Example:

```text
Client MAC = A
```

So when building the Frame:

```text
SRC MAC = A
```

The Source MAC does not need DHCP or DNS or ARP, because the device already knows the MAC of its network card directly.

---

## 4) Source IP

The Source IP is the address of the device itself.

It can be obtained in two ways:

```text
Static IP
DHCP
```

### Static IP

In this case, the settings are entered manually:

```text
IP Address      = 192.168.1.199
Subnet Mask     = 255.255.255.0
Default Gateway = 192.168.1.1
```

This means:

```text
IP Address      = the address of the device
Subnet Mask     = the size of the network
Default Gateway = the router used to go outside the network
```

### DHCP

DHCP stands for:

```text
Dynamic Host Configuration Protocol
```

Its function is to give the device network settings automatically, such as:

```text
IP Address
Subnet Mask
Default Gateway
DNS Server
```

Example:

```text
IP Address      = 10.0.0.2
Subnet Mask     = 255.255.255.0
Default Gateway = 10.0.0.1
DNS Server      = 10.0.0.10
```

The well-known DHCP process is called DORA:

```text
Discover
Offer
Request
ACK
```

This means:

1. The Client asks: Is there a DHCP Server?
2. The server offers an IP and settings.
3. The Client requests to use the offer.
4. The server confirms the settings.

After that, the device has a Source IP.

---

## 5) Destination IP

The Destination IP is the address of the device or server that we want to reach.

If you already know the IP directly, it can be used directly:

```text
DST IP = 10.0.0.4
```

But usually, the user types a website name such as:

```text
google.com
```

Here we need DNS.

---

## 6) DNS

DNS stands for:

```text
Domain Name System
```

Its function is:

```text
Name -> IP
```

Example:

```text
google.com -> 55.1.1.1
```

The device asks the DNS Server:

```text
What is the IP of google.com?
```

Then DNS replies:

```text
55.1.1.1
```

So it becomes:

```text
DST IP = 55.1.1.1
```

Very important:

```text
DNS does not provide a MAC Address
DNS only provides an IP Address
```

---

## 7) ARP

After the device knows:

```text
SRC IP
DST IP
SRC MAC
```

it still needs:

```text
DST MAC
```

Here comes the role of ARP.

ARP stands for:

```text
Address Resolution Protocol
```

Its function is:

```text
IP -> MAC
```

But only inside the same local network.

Example:

```text
Client IP = 10.0.0.2
Server IP = 10.0.0.4
```

The Client wants to know the MAC of the server, so it sends:

```text
Who has 10.0.0.4?
Tell 10.0.0.2
```

This message is Broadcast:

```text
FF:FF:FF:FF:FF:FF
```

The server replies:

```text
10.0.0.4 is at MAC C
```

So it becomes:

```text
DST MAC = C
```

---

## 8) Default Gateway

The Default Gateway is the device to which we send traffic when the destination is outside our network.

It is usually the router.

Example:

```text
Client IP       = 10.0.0.2/24
Default Gateway = 10.0.0.1
```

The network is:

```text
10.0.0.0/24
```

Any device inside this network would be such as:

```text
10.0.0.x
```

If the target is inside the same network, we use ARP to find the MAC of the target itself.

If the target is outside the network, we use ARP to find the MAC of the Default Gateway.

---

## 9) Example: The Target Is Inside the Same Network

We have:

```text
Client IP  = 10.0.0.2/24
Client MAC = A

Server IP  = 10.0.0.4
Server MAC = C
```

The Client checks:

```text
Is 10.0.0.4 inside 10.0.0.0/24?
```

The answer:

```text
Yes
```

So it performs ARP on the server IP:

```text
Who has 10.0.0.4?
```

The server replies:

```text
10.0.0.4 is at MAC C
```

The final values:

```text
SRC IP  = 10.0.0.2
DST IP  = 10.0.0.4
SRC MAC = A
DST MAC = C
```

Here we do not use the router’s MAC, because the target is inside the same network.

---

## 10) Example: The Target Is Outside the Network

We have:

```text
Laptop IP       = 10.0.0.2/24
Laptop MAC      = A
Default Gateway = 10.0.0.1
Gateway MAC     = B
Google IP       = 55.1.1.1
```

The Laptop checks:

```text
Is 55.1.1.1 inside 10.0.0.0/24?
```

The answer:

```text
No
```

So the traffic must be sent to the Default Gateway.

But the Laptop needs the MAC of the router, so it performs ARP:

```text
Who has 10.0.0.1?
```

The router replies:

```text
10.0.0.1 is at MAC B
```

The final values in the first Hop:

```text
SRC IP  = 10.0.0.2
DST IP  = 55.1.1.1
SRC MAC = A
DST MAC = B
```

Notice:

```text
DST IP  = Google
DST MAC = Default Gateway
```

Because Google is outside the local network.

---

## 11) Why Is Destination MAC Not Google’s MAC?

Because Frames work only inside the local network or the local segment.

The device cannot send a Frame directly to Google.

So it sends the Frame to the router first.

The router takes the Packet, then builds a new Frame for the next Hop.

Therefore:

```text
IP  = End-to-End
MAC = Hop-to-Hop
```

---

## 12) Where Does Each Piece of Information Come From?

| Information     | Where does it come from?             |
| --------------- | ------------------------------------ |
| Source MAC      | From the NIC                         |
| Source IP       | Static or DHCP                       |
| Destination IP  | DNS or already known                 |
| Destination MAC | ARP for the target or the Default Gateway |

---

## 13) The Difference Between DHCP, DNS, and ARP

| Protocol | The question it answers                         | The result              |
| -------- | ----------------------------------------------- | ----------------------- |
| DHCP     | What are my network settings?                   | IP, Mask, Gateway, DNS  |
| DNS      | What is the IP of this name?                    | Destination IP          |
| ARP      | What is the MAC of this IP inside the network?  | Destination MAC         |

---

## 14) Summary

For a Client to send data to a Web Server, it needs:

```text
SRC IP
DST IP
SRC MAC
DST MAC
```

How they are obtained:

```text
SRC MAC  -> from the network card
SRC IP   -> Static or DHCP
DST IP   -> DNS or already known
DST MAC  -> ARP
```

If the target is inside the same network:

```text
DST MAC = MAC of the target device
```

If the target is outside the network:

```text
DST MAC = MAC of the Default Gateway
```

The golden rule:

```text
IP  = End-to-End
MAC = Hop-to-Hop
```