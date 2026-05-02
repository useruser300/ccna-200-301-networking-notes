# Router, ARP, Gateway, DNS, Routing

## 1. The Idea

In local networks, the Switch allows devices within the same network to communicate with each other.

But the problem begins when a device wants to communicate with another device located in a different network.

Here we need another device called:

**Router**

The function of the Router is to connect different networks together.

## 2. Quick Review of the Switch’s Role

The Switch connects devices within the same network.

Example:

* Johnny
* Mark
* Denny
* Lisa

They are all connected to the same Switch, and they are all inside the same network.

Therefore, Johnny can communicate with Mark, Lisa, or Denny directly within the same LAN.

But if Johnny wants to reach a Web Server located in another network, the Switch alone is not enough.

## 3. What Is a Router?

A Router is a device that connects one Network to another Network.

Example:

```text
Network A  ---- Router ---- Network B
```

Or:

```text
Home Network ---- Router ---- Internet
```

This means the router is the device that allows a device inside your network to reach external networks.

## 4. Why Is Connecting a Switch to Another Switch Not Enough?

We may think of directly connecting the Switch of the first network to the Switch of the second network.

But the problem is not only about cables or the number of switches.

The main problem is that the devices exist in different IP groups.

Example:

Network 1:

```text
10.1.1.0 - 10.1.1.255
```

Network 2:

```text
23.227.38.0 - 23.227.38.255
```

These are two different networks.

The Switch deals with Layer 2 and MAC Addresses, but it does not connect different IP networks.

That is why we need a Router, because it operates at Layer 3.

## 5. The Meaning of Network in This Context

When we say “Network”, we usually mean a group of IP Addresses that belong to the same range.

Example:

```text
10.1.1.0/24
```

This means approximately:

```text
10.1.1.0 to 10.1.1.255
```

Any device with an IP within this range is considered to be inside the same network.

But a device with the address:

```text
23.227.38.65
```

is outside this network, and a Router is required to reach it.

## 6. What Is ARP?

Before a device sends data within the same network, it must know the MAC Address of the target device.

Therefore, it uses a protocol called:

**ARP = Address Resolution Protocol**

Its function is:

**Converting an IP Address to a MAC Address within the same network**

Example:

Johnny wants to reach Mark.

Mark IP = `10.1.1.2`

But the Switch does not understand IP. It understands MAC.

So Johnny needs to know:

What is the MAC Address of `10.1.1.2`?

## 7. How Does ARP Work Within the Same Network?

Johnny sends a Broadcast message:

```text
Who has 10.1.1.2?
```

This message goes to all devices within the same network.

The other devices ignore it, but Mark replies:

I am the owner of `10.1.1.2`, and this is my MAC Address.

After that, Johnny can send the data to Mark.

## 8. What Is the Broadcast MAC Address?

When the device does not know the MAC Address of the destination, it sends ARP to the Broadcast Address:

```text
FF:FF:FF:FF:FF:FF
```

Its meaning is:

Send this message to everyone inside the local network.

The Switch receives it and sends it to all ports.

## 9. What Happens When the Target Is Outside the Network?

If Johnny tries to reach:

```text
23.227.38.65
```

he knows that this address is not inside his network:

```text
10.1.1.0/24
```

So he does not try to look for the MAC Address of the server directly.

Instead, he tries to reach the:

**Default Gateway**

## 10. What Is the Default Gateway?

The Default Gateway is the address of the router inside the device’s network.

Example:

```text
Johnny IP: 10.1.1.3
Gateway: 10.1.1.1
```

Its meaning is:

If you want to reach an external network, send the data to `10.1.1.1`.

And the address `10.1.1.1` is usually the router interface inside the same network.

## 11. What Happens Without a Router?

Johnny tries to reach an external network.

So he looks for the MAC Address of the Gateway:

```text
Who has 10.1.1.1?
```

But if there is no Router present at this address, nobody will reply.

The result:

The external network cannot be reached.

## 12. How Does the Router Solve the Problem?

When we add a Router between the two networks:

```text
10.1.1.0/24 ---- Router ---- 23.227.38.0/24
```

Johnny now has a path to leave his network.

When he wants to reach the server:

```text
23.227.38.65
```

he does the following:

```text
Johnny → Switch → Router → Switch → Server
```

## 13. What Happens in Detail?

Johnny knows that the server is outside his network.

So he looks for the MAC Address of the Gateway:

```text
Who has 10.1.1.1?
```

The router replies:

I am `10.1.1.1`, and this is my MAC Address.

After that, Johnny sends the data to the router.

But very importantly:

At Layer 3:

```text
Source IP = Johnny
Destination IP = Coffee Server
```

At Layer 2:

```text
Source MAC = Johnny
Destination MAC = Router
```

This means Johnny is saying:

Switch, deliver this Frame to the router.

And then the Router takes responsibility for delivering the Packet to the other network.

## 14. The Difference Between Layer 2 and Layer 3 During Transmission

### Layer 2

It is related to movement within the same local network.

It uses:

**MAC Address**

And the message is called:

**Frame**

### Layer 3

It is related to movement between networks.

It uses:

**IP Address**

And the message is called:

**Packet**

Important rule:

**Switch understands Layer 2**  
**Router understands Layer 3**

## 15. What Does the Router Do When It Receives a Packet?

When the router receives the data, it looks at the Destination IP:

```text
23.227.38.65
```

Then it searches in the Routing Table and decides:

Which Interface should I use to send this data?

If the server’s network is directly connected to the router, it sends it through the correct port.

## 16. The Router Also Needs ARP

The router knows that the server exists in the other network, but it needs the MAC Address of the server so it can send a Frame to it within that network.

So the router sends ARP:

```text
Who has 23.227.38.65?
```
(so he sendes the arp message to the switch and the switch broadcast it out )

The server replies:

I am the owner of this IP, and this is my MAC Address.

After that, the router can send the data to the server.

## 17. The Form of the Data During the Journey

From Johnny to Router:

Layer 3:

```text
Source IP = Johnny
Destination IP = Server
```

Layer 2:

```text
Source MAC = Johnny
Destination MAC = Router
```

From Router to Server:

Layer 3:

```text
Source IP = Johnny
Destination IP = Server
```

Layer 2:

```text
Source MAC = Router
Destination MAC = Server
```

Notice that the IP continues to represent the original source and the final destination, but the MAC changes from one step to another.

## 18. The Return of the Reply from the Server

When the server receives the request, it replies to Johnny.

But because Johnny is in a different network, the server sends the reply to its own Gateway.

The path becomes:

```text
Server → Switch → Router → Switch → Johnny
```

This is how communication happens between two different networks.

## 19. What Is DNS?

When we type a website such as:

```text
www.example.com
```

the device cannot use the name directly to reach the server.

Networks need an IP Address.

Therefore, we use:

**DNS = Domain Name System**

Its function is:

**Converting the website name into an IP Address**

Example:

```text
www.example.com → 23.227.38.65
```

## 20. How Does DNS Work in This Example?

Johnny types the site name in the browser.

The device needs to know the IP of the site.

So it sends a question to the DNS Server:

What is the IP of `www.example.com`?

But before sending the question, it needs to know the MAC Address of the DNS Server.

So it uses ARP first.

Then it sends the DNS Query.

The DNS Server replies:

```text
www.example.com = 23.227.38.65
```

After that, Johnny can send the HTTP Request to the Web Server.

## 21. What Is an HTTP Request?

After the device knows the IP of the website, it sends a request to the server.

Example:

**HTTP GET Request**

Its meaning is:

Give me the web page.

The server replies with the content of the site, and then the page appears in the browser.

## 22. Why Is ARP Not Repeated Every Time?

Devices do not perform ARP from scratch every time.

After the device learns the MAC Address, it stores it temporarily in the Cache.

Example:

* Johnny remembers the MAC of the router
* The Router remembers the MAC of the server

So in the next requests, they do not need to repeat all ARP steps immediately.

But after some time, this information expires and is learned again.

## 23. How Is This Similar to the Real Internet?

In the example, we have one router between two networks.

But in the real Internet, the path may be:

```text
Home Router
→ ISP Router
→ Internet Router
→ Another Router
→ Data Center Router
→ Web Server
```

This means the data may pass through several Routers before it reaches the website.

But the fundamental idea is the same:

**Routers connect networks.**

## 24. The First Important Command on the Router

To see the Routing Table inside the router, we use:

```text
enable
show ip route
```

The command:

```text
show ip route
```

displays the map of the networks known by the router.

Example:

```text
10.1.1.0/24 is directly connected, GigabitEthernet0/0
23.227.38.0/24 is directly connected, GigabitEthernet0/1
```

Its meaning is:

Network `10.1.1.0/24` exists on interface `Gi0/0`  
Network `23.227.38.0/24` exists on interface `Gi0/1`

## 25. How Does the Router Decide the Path?

When a Packet reaches the router, it looks at the Destination IP.

Example:

```text
Destination IP = 23.227.38.65
```

Then it searches in the Routing Table:

Do I know the network `23.227.38.0/24`?

If it finds it, it sends the Packet through the correct Interface.

## 26. What Is the Routing Table?

The Routing Table is a table inside the router that contains a map of the networks.

Simplified example:

| Network           | Exit Interface |
| ----------------- | -------------- |
| `10.1.1.0/24`     | `Gi0/0`        |
| `23.227.38.0/24`  | `Gi0/1`        |

This means the router knows:

If the destination belongs to this network, send it out of this port.

## 27. What Is BGP Briefly?

In the real Internet, large routers contain a huge number of routes.

One of the most important routing protocols on the Internet is:

**BGP = Border Gateway Protocol**

Its function is to help large routers know the paths to different Internet networks.

In a simple environment, the Routing Table is small.

But on the Internet, it may contain a very large number of Routes.

## 28. Final Summary

The most important rules:

Switch connects devices within the same network.

Router connects different networks.

Switch = Layer 2 = MAC Address = Frame

Router = Layer 3 = IP Address = Packet

ARP converts IP to MAC within the same network.

DNS converts a website name to an IP Address.

Default Gateway is the router to which we send data when the destination is outside the network.

```text
show mac-address-table
```

is used on a Switch to view MAC Addresses.

```text
show ip route
```

is used on a Router to view the Routing Table.

And the core idea is:

When the target device is inside the same network, we use a Switch and a MAC Address.

When the target device is outside the network, we use a Router and the Default Gateway.

The most important mental path to memorize:

```text
Website name
→ DNS converts it to IP
→ The device sends to the Gateway
→ Router determines the path
→ Data reaches the server
→ The server replies
→ The page appears in the browser
```
