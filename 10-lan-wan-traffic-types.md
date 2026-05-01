# LAN vs WAN + Unicast / Broadcast / Multicast

## 1) LAN

LAN stands for:

**Local Area Network**

And it means:

**A local network**

The basic idea is that you have a group of devices connected to each other within a small or limited area.

Example:

* Home
* Office
* Small company
* One floor inside a company
* One building
* Small campus

Inside this network, you may have:

* Laptop
* Server
* Printer
* Mobile
* Access Point
* Switch

All of these devices are connected within the same local environment.

## 2) Practical Example of a LAN

Suppose you have an office that contains:

* Laptop
* Server
* Printer
* Switch

These devices are connected to each other through a Switch.

Here we are inside a local network, because the devices are close to each other and located in the same place.

Example:

```text
Laptop  ->  Switch  ->  Server
Printer ->  Switch
```

This environment is called:

**LAN**

## 3) Characteristics of LAN

A LAN has three important characteristics:

### Scope

A LAN is limited to a small area.

Example:

* Single building
* Office
* Home
* Campus

This means it is not a network stretched across cities or countries.

### Speed

LAN speed is usually very high compared to WAN.

The reason is that the distance is short, and the devices are connected locally through Ethernet or Wi-Fi.

Example speeds that may exist inside a LAN:

* 1 Gbps
* 10 Gbps
* 40 Gbps
* 100 Gbps

At home, you will usually see 1 Gbps or less depending on the devices.  
In companies and data centers, the speeds may reach 10 Gbps or more.

### Uses

LAN is used to connect devices inside the same place.

Examples:

* Connecting employee devices to internal servers
* Connecting printers
* Connecting office devices
* Sharing files internally
* Connecting home devices to the router and switch
* Connecting Access Points to the network

## 4) What Technology Does LAN Use?

In current reality, the most common technology used in LAN is:

**Ethernet**

Ethernet operates at Layer 2 and depends on:

* MAC Address
* Frames
* Switches

This means that when devices inside a LAN communicate at Layer 2, they use MAC Addresses.

## 5) LAN and MAC Address

Inside a LAN, when one device sends to another device within the same network, transmission at Layer 2 depends on:

* Source MAC
* Destination MAC

Example:

A Laptop wants to send data to a Server inside the same network.

A Frame will be built containing:

```text
Source MAC      = MAC of the Laptop
Destination MAC = MAC of the Server
```

And the Switch uses the MAC Table to know from which Port it should send the Frame.

## 6) WAN

WAN stands for:

**Wide Area Network**

And it means:

**A wide-area network**

A WAN connects networks that are located far away from each other.

Example:

* Connecting an office in Dortmund with an office in Berlin
* Connecting a company branch in one country with another branch in another country
* Connecting the company network to the Internet
* Connecting more than one LAN together through a service provider

## 7) The Basic Idea of WAN

Inside the office, you have a LAN.

But to leave this local network and go to the outside world, you need a WAN connection.

Example:

```text
LAN  ->  Customer Edge Router  ->  Provider Network  ->  Internet
```

This means the WAN begins from the point where you exit the local network toward the service provider or remote networks.

## 8) Customer Edge - CE

The Customer Edge or CE is the router located at the customer side or inside the company.

This means the router that is on your side.

Example:

Inside the company, you have a Router connected on one side to the LAN, and on the other side to the service provider.

This router is called:

**Customer Edge Router**

Or in short:

**CE**

## 9) Provider Edge - PE

The Provider Edge or PE is the router located at the service provider side.

The service provider is the company that gives you external connectivity, such as:

* ISP
* Telecom provider
* WAN provider
* Internet provider

Your CE connects to the PE at the provider.

The logical structure becomes:

```text
LAN -> CE -> WAN Provider -> PE -> Internet / Remote Network
```

## 10) WAN Switch

Inside the provider environment, there may be a device or a part called a WAN Switch or WAN equipment.

The idea here is not like a LAN Switch inside your office, but rather a part of the provider network that connects you to other networks.

This means that you may receive a Port or Link from the service provider, and this link connects you to the provider network, and from there to the Internet or to another branch.

## 11) Characteristics of WAN

### Scope

WAN covers a large area.

Example:

* Between buildings
* Between cities
* Between countries
* Worldwide

This means it can be between two places that are very far apart.

### Speed

WAN speed is usually lower than LAN.

The reasons are:

* The distances are longer
* Traffic passes through a service provider
* There are several networks in the path
* The connection is usually more expensive
* There may be bandwidth limitations

Example:

In a LAN, you may see:

* 1 Gbps
* 10 Gbps

But in a WAN, the connection may be:

* 5 Mbps
* 20 Mbps
* 100 Mbps
* 1 Gbps

depending on the contract with the service provider.

### Uses

WAN is used to connect distant networks.

Examples:

* Connecting one company branch to another branch
* Connecting the company to the Internet
* Connecting offices in different cities
* Connecting global sites
* Connecting a data center to the cloud or to another site

## 12) The Difference Between LAN and WAN

| Comparison | LAN | WAN |
| ---------- | --- | --- |
| Name | Local Area Network | Wide Area Network |
| Scope | Small area | Large area |
| Examples | Home, office, building | City, country, Internet |
| Speed | Usually higher | Usually lower than LAN |
| Devices | Switches, APs, local servers | Routers, provider links, CE/PE |
| Use | Connecting devices in the same place | Connecting distant networks or reaching the Internet |
| Management | Usually managed by you | Usually involves the service provider in its management |

## 13) Full Example of LAN + WAN

Inside the office, you have:

* Laptop
* Server
* Printer
* Switch

This part is:

**LAN**

Then you have a Router at the company side:

**Customer Edge Router**

This router connects you to the service provider.

After that there is:

**Provider Edge Router**

Then the Internet.

The complete structure:

```text
Laptop / Server / Printer
        |
      Switch
        |
       LAN
        |
Customer Edge Router
        |
       WAN
        |
Provider Edge Router
        |
     Internet
```

## 14) LAN Interface and WAN Interface

The router located at the company usually has more than one Interface.

### LAN Interface

This is the side connected to the internal network.

Example:

```text
Router LAN Interface -> Switch -> Internal Devices
```

### WAN Interface

This is the side connected to the service provider or the Internet.

Example:

```text
Router WAN Interface -> ISP / Provider
```

So:

* LAN Interface looks inward
* WAN Interface looks outward

## 15) Summary: LAN vs WAN

The short idea:

* LAN is the internal network inside the home, office, or building
* WAN is the network or the link that connects you to distant networks or to the Internet
* LAN is usually faster and shorter
* WAN is usually wider and relatively slower
* LAN depends heavily on Switches and Ethernet
* WAN depends on Routers and service providers

## 16) Unicast

Unicast means:

**One-to-One**

That is:

**One device sends to only one device**

Example:

```text
10.0.0.1  ->  10.0.0.2
```

A device with the address `10.0.0.1` wants to send data to a device with the address `10.0.0.2`.

Here, the Destination IP is one specific device.

## 17) Example of Unicast

Suppose you have:

* Laptop A = `10.0.0.1`
* Laptop B = `10.0.0.2`

If Laptop A wants to send a message only to Laptop B, then it will be:

```text
Source IP      = 10.0.0.1
Destination IP = 10.0.0.2
```

This is a Unicast message because it is from one device to one device.

## 18) When Do We Use Unicast?

Most of the daily traffic that you deal with is Unicast.

Examples:

* Opening a website
* SSH to a server
* Downloading a file from a server
* Sending a Request to an API
* A direct connection from one device to another

In all these cases, there is usually:

**One sender -> One receiver**

## 19) Broadcast

Broadcast means:

**One-to-All**

That is:

**One device sends to all devices inside the same network or the same Broadcast Domain**

The idea is that the message is not directed to only one device, but to all devices in the same network segment.

## 20) Broadcast IP Address

The well-known general Broadcast address inside the local network is:

```text
255.255.255.255
```

When a device sends a Packet to this address, the meaning is that it wants to send it to all devices inside the local network.

## 21) Broadcast at Layer 2

At Layer 2, there is also a Broadcast MAC Address.

It is:

```text
FF:FF:FF:FF:FF:FF
```

This address means:

Send the Frame to all devices inside the same Layer 2 segment.

So in the case of Broadcast, you may see:

```text
Layer 3 Broadcast IP  = 255.255.255.255
Layer 2 Broadcast MAC = FF:FF:FF:FF:FF:FF
```

## 22) Example of Broadcast

Suppose the device:

```text
10.0.0.1
```

wants to send a message to all devices inside the network.

Instead of sending to each device individually:

```text
10.0.0.2
10.0.0.3
10.0.0.4
```

it uses Broadcast.

Example:

```text
Source IP       = 10.0.0.1
Destination IP  = 255.255.255.255
Destination MAC = FF:FF:FF:FF:FF:FF
```

All devices inside the same network receive this message.

## 23) Where Is Broadcast Used?

Broadcast is important in some protocols inside the LAN.

Common examples:

* ARP
* DHCP Discover

Example of DHCP:

A new device entered the network and does not know who the DHCP Server is, so it sends a Broadcast saying:

Is there a DHCP Server?

All devices may receive the message, but the DHCP Server is the one that replies.

## 24) Important Point About Broadcast

Broadcast usually does not cross routers.

This means Broadcast stays inside the same network or the same Broadcast Domain.

And here the role of the router appears in separating networks.

If you have two networks:

```text
10.0.0.0/24
20.0.0.0/24
```

Broadcast inside network 10 does not automatically move to network 20.

## 25) Multicast

Multicast means:

**One-to-Many**

But not to all devices.

Rather, to a specific group of devices that are interested in receiving this kind of traffic.

This means it is somewhere between:

* Unicast: one to one
* Broadcast: one to all
* Multicast: one to a specific group

## 26) Multicast Range

The IPv4 Multicast range is:

```text
224.0.0.0 - 239.255.255.255
```

Any IP within this range is considered a Multicast Address.

```text
239.0.0.1
```

This is a Multicast IP.

## 27) How Does Multicast Work Logically?

Suppose you have four devices.

Three of them are interested in a certain application, such as:

* A multiplayer game
* Video streaming
* Internal stream
* Routing protocol updates
* IPTV

These devices join a Multicast Group with an address such as:

```text
239.0.0.1
```

When a device sends to:

```text
Destination IP = 239.0.0.1
```

only the devices subscribed to this group receive the traffic.

As for the device that is not subscribed to the group, it does not care about this message.

## 28) Example of Multicast

We have a sending device:

```text
Sender = 10.0.0.1
```

and it wants to send data to a group of devices subscribed to the Group:

```text
239.0.0.1
```

So it becomes:

```text
Source IP      = 10.0.0.1
Destination IP = 239.0.0.1
```

The devices subscribed to this group receive the message.

As for devices not subscribed, they do not receive it as traffic directed to them.

## 29) Why Do We Use Multicast Instead of Broadcast?

Because Broadcast sends to all devices, even the devices that are not interested.

And this may cause:

* Resource consumption
* Increased traffic
* Disturbance for all devices

But Multicast sends only to the interested group.

This means instead of sending to everyone:

**One-to-All**

you send only to the required group:

**One-to-Many specific receivers**

## 30) Why Do We Sometimes Use Multicast Instead of Unicast?

If you have one source that wants to send the same traffic to 100 devices, then using Unicast it would need to send 100 copies.

But using Multicast:

* It sends one copy to the Multicast Group
* And the network delivers it to the interested members according to the design

That is why Multicast is useful in:

* Video and streaming
* Some audio applications
* IPTV
* Some network protocols
* Some games or group applications

## 31) Comparison of Unicast, Broadcast, and Multicast

| Type | Pattern | Meaning | Example |
| ---- | ------- | ------- | ------- |
| Unicast | One-to-One | One device to one device | `10.0.0.1 -> 10.0.0.2` |
| Broadcast | One-to-All | One device to all devices in the same network | `10.0.0.1 -> 255.255.255.255` |
| Multicast | One-to-Many | One device to a specific group | `10.0.0.1 -> 239.0.0.1` |

## 32) Practical Example Combining All Three

### Unicast

A Laptop opens a Web Server:

```text
10.0.0.1 -> 10.0.0.2
```

The message is directed to only one device.

### Broadcast

A Laptop searches for a DHCP Server:

```text
10.0.0.1 -> 255.255.255.255
```

The message goes to all devices in the same network.

### Multicast

A device sends a stream to a group of devices subscribed to a Group:

```text
10.0.0.1 -> 239.0.0.1
```

The message goes only to the devices subscribed to this group.

## 33) The Important Difference Between LAN/WAN and Unicast/Broadcast/Multicast

These are different concepts, but they are related.

### LAN/WAN

They talk about the scope of the network:

* Is the network local?
* Or is it stretched across large distances?

### Unicast/Broadcast/Multicast

They talk about the method of sending traffic:

* Am I sending to one device?
* To all devices?
* To a specific group?

This means that inside a LAN, you may have:

* Unicast
* Broadcast
* Multicast

And inside a WAN or across larger networks, you may have:

* Unicast
* Multicast in some cases
* But Broadcast usually remains limited inside the local network and does not naturally cross routers

## 34) Summary

The final idea is as follows:

* LAN is a local network inside a small area such as a home, office, or building
* LAN is usually high-speed because it is short and direct
* LAN is used to connect internal devices such as Laptops, Servers, and Printers
* WAN is a wide network that connects distant networks or connects you to the Internet
* WAN is usually slower than LAN because it crosses long distances and service providers
* CE is the router located at the customer side
* PE is the router located at the service provider side
* Unicast means one device sends to one device
* Broadcast means one device sends to all devices inside the same network
* Multicast means one device sends to a specific group of devices
* The common Broadcast IP is `255.255.255.255`
* The Broadcast MAC is `FF:FF:FF:FF:FF:FF`
* The Multicast Range is `224.0.0.0 - 239.255.255.255`
* Unicast is the most common in daily communications
* Broadcast is important in protocols such as ARP and DHCP
* Multicast is useful when we want to send the same data to a specific group without sending a separate copy to each device