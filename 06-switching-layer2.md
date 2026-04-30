# Switches, Hubs, Frames, Packets, Wireless

## 1. The Idea of the Lesson

Networks are not just devices connected to each other. Inside the network, there are devices that forward data between different devices, and the most important device in local networks is the Switch.

The main goal is to understand:

* What the Switch is
* How it differs from the Hub
* How data moves inside the network
* What a MAC Address means
* What the difference is between a Frame and a Packet
* Why wired Ethernet is better than Wireless in many cases

## 2. What Is a Switch?

A Switch is a device used to connect multiple devices within the same local network LAN.

For example:

```text
PC1 ----\
PC2 ----- Switch
PC3 ----/
```

Each device connects to the Switch using an Ethernet cable.

The function of the Switch is to allow devices to communicate with each other within the same network.

Example:

Laptop A wants to send data to Laptop B.

The data leaves the first device through the Ethernet cable, enters the Switch, and then the Switch sends it to the correct device.

## 3. Ethernet Cable and Electrical Signals

An Ethernet cable is not something magical. It is simply internal metal wires through which electrical signals pass.

This means that when one device sends data to another device, what actually happens is:

```text
Data → Electrical Signals → Ethernet Cable → Switch → Other Device
```

These electrical signals represent the data moving inside the network.

This part usually represents what is called:

```text
Layer 1 = Physical Layer
```

That is, the physical layer: the cable, the signals, the ports, the electricity.

## 4. Switch Sizes

A Switch can be small or large depending on the number of ports.

For example:

```text
8-Port Switch
```

This means it can connect 8 devices.

```text
48-Port Switch
```

This means it can connect 48 devices.

Each port can connect to a device such as:

* Computer
* Laptop
* Server
* Access Point
* Printer
* IP Phone

## 5. What Is a Hub?

Before the widespread use of the Switch, there was a device called a Hub.

A Hub looks similar to a Switch from the outside because it has Ethernet ports, but the difference in how it works is very large.

A Hub is a “dumb” device because it does not know where each device is located.

When it receives a message from one device, it does not know who it should send it to, so it sends it to الجميع.

Example:

Harry wants to send a message to Ron.

In a Hub environment, this happens:

```text
Harry → Hub → Ron
              → Hermione
              → Malfoy
```

This means the message goes to all devices, not only to the intended device.

## 6. Why Is the Hub Bad?

The Hub is bad for several reasons:

First: it does not send the message only to the correct device.  
If one device sends a message to another device, all devices receive a copy of it.  
Even if the message is not intended for them, it still reaches them.

Second: a security problem.  
Other devices may see data that does not belong to them.  
Of course, a normal device ignores messages that are not intended for it, but an attacker can exploit this to monitor the traffic.

Third: congestion and collisions.  
Because all messages are spread to everyone, there is major congestion in the network.

This leads to:

* Slowness
* Collisions
* Poor performance
* Weak security

## 7. Ping Test Inside a Hub Network

The `ping` tool is used to test whether another device is available and reachable.

For example:

```text
ping 10.1.1.2
```

The meaning is:

Is the device with IP `10.1.1.2` present and responding?

In a Hub environment:

Harry sends a ping to Ron.

But the Hub sends the message to everyone.

Then Ron replies, and the Hub also sends the reply to everyone.

This means even the reply does not go only to Harry, but is spread to all devices.

## 8. The Basic Difference Between Hub and Switch

A Hub works like this:

Any message enters → send it to all ports

A Switch works like this:

Any message enters → examine the destination → send it only to the correct port

That is why the Switch is smarter and better.

## 9. Ping Test Inside a Switch Network

In a Switch environment:

Johnny wants to send a ping to Mark.

The command may be:

```text
ping 10.1.1.2
```

The result:

```text
Johnny → Switch → Mark
```

And when Mark replies:

```text
Mark → Switch → Johnny
```

The message does not go to all devices.

And this is the correct behavior.

## 10. How Does the Switch Know Where Each Device Is?

The Switch has a “memory” in which it learns the location of each device.

This memory is called:

**CAM Table**

or:

**MAC Address Table**

Inside this table, the Switch stores information such as:

```text
MAC Address           Port
00D0.9752.8936        Fa0/2
00E0.B059.0897        Fa0/1
```

This means:

This device is located on this port.

## 11. What Is a MAC Address?

A MAC Address is a unique address for the device at Layer 2.

Every network card has its own MAC Address.

Example:

```text
00:D0:97:52:89:36
```

The Switch does not know the device by the name “Johnny” or “Mark”.

It knows it by its MAC Address.

For example:

```text
Johnny = 00D0.9752.8936
Mark   = 00E0.B059.0897
```

## 12. The Difference Between Layer 1 and Layer 2

### Layer 1 — Physical Layer

This layer is related to physical things:

* Ethernet cable
* Electrical signals
* Ports
* Wires
* Physical connection

Example:

The electrical signal passes inside the cable.

### Layer 2 — Data Link Layer

This layer deals with:

* MAC Address
* Switch
* Frames

The Switch operates mainly at Layer 2.

## 13. Why Does the Switch Not Use the IP Address?

The IP Address is a Layer 3 Address.

But the Switch is a Layer 2 device.

Therefore, the Switch does not care much about the IP Address when making the forwarding decision.

It depends on:

**MAC Address**

not:

**IP Address**

Example:

```text
ping 10.1.1.2
```

The IP is important for the devices that are communicating with each other, but internally the Switch makes the forwarding decision based on the MAC Address.

## 14. What Does the Switch See?

When the data reaches the Switch, it focuses on Layer 2 information.

This means it cares about:

* Source MAC Address
* Destination MAC Address

Example:

```text
From: MAC of Mark
To:   MAC of Lisa
```

If it knows the location of Lisa’s MAC, it sends the message directly to Lisa’s port.

## 15. What Happens When the Message Reaches the Final Device?

When the message reaches the intended device, the device can deal with higher layers such as Layer 3.

This means the device sees:

* Source IP
* Destination IP

Example:

```text
From: 10.1.1.2
To:   10.1.1.5
```

But while the message is passing through the Switch, the focus is on Layer 2.

## 16. The First Important Cisco CLI Command

You can enter the Switch command-line interface in Packet Tracer and then type:

```text
enable
```

After that, the symbol appears:

```text
#
```

Then we use the command:

```text
show mac-address-table
```

This command displays the table of MAC addresses that the Switch has learned.

Example idea:

```text
MAC Address           Type        Port
00D0.9752.8936        Dynamic     Fa0/2
00E0.B059.0897        Dynamic     Fa0/1
```

This means the Switch has learned that each device is located on a specific port.

## 17. How Does the Switch Learn?

The Switch learns from the movement of data.

When a device sends a message, the Switch sees the Source MAC Address and says:

This MAC came from this port.

Then it stores the information in the MAC Address Table.

Example:

Mark sent a message from `Fa0/1`.

The Switch records:

Mark’s MAC is located on `Fa0/1`.

Later, if someone wants to send a message to Mark, the Switch knows where to send it.

## 18. Frame vs Packet

### Frame

At Layer 2, the message is called:

**Frame**

So when we talk about the Switch and the MAC Address, we are usually talking about Frames.

Important rule:

```text
Layer 2 = Switch = MAC Address = Frame
```

### Packet

At Layer 3, the message is called:

**Packet**

And when we talk about the IP Address, we are usually talking about Packets.

Important rule:

```text
Layer 3 = IP Address = Packet
```

In practice, many people use the word Packet in a general way for any data moving in the network, but technically:

```text
Layer 2 → Frame
Layer 3 → Packet
```

## 19. Wireless Access Point

An Access Point is a device that allows wireless devices such as phones and laptops to connect to the network.

It is usually connected to the Switch through an Ethernet cable.

Example:

```text
Phone / Laptop / Tablet
        ↓ Wireless
Access Point
        ↓ Ethernet
Switch
```

This means the Access Point extends the wired network to wireless devices.

## 20. Why Is Wireless Similar to a Hub?

Wireless communication uses the air or radio waves.

When the Access Point sends a wireless signal, the signal spreads in the air and can reach more than one device.

So from the perspective of how the signal spreads, Wireless is more similar to a Hub than to a Switch.

Example:

The Access Point sends a message to Tablet 1.

But the signal may also reach:

* Tablet 2
* Laptop
* Phone

The unintended devices ignore the message, but the signal itself still spread in the wireless medium.

## 21. Why Is Ethernet Better Than Wireless?

Wired Ethernet is often better because it is:

* More stable
* Less exposed to interference
* Less congested
* Relatively more secure
* Better in performance
* It does not send the signal through the air like Wireless

That is why in important environments, it is preferred to use the cable whenever possible.

## 22. The Role of the Switch with the Access Point

Although the Access Point is similar to a Hub wirelessly in terms of signal spread, in the end it is connected to the Switch.

When the data reaches the Access Point from the wireless device, the Access Point sends it to the Switch.

Then the Switch behaves intelligently and sends it only to the correct device.

Example:

```text
Tablet → Access Point → Switch → Denny
```

The Switch does not send it to everyone, but sends it to the correct port according to the MAC Address Table.

## 23. Final Summary

The most important ideas:

Hub = a dumb device that sends messages to everyone

Switch = a smart device that sends messages only to the correct device

Switch operates at Layer 2

Layer 2 uses MAC Address

Layer 2 messages are called Frames

IP Address operates at Layer 3

Layer 3 messages are called Packets

The Switch learns the locations of devices through the MAC Address Table

```text
show mac-address-table
```

displays the Switch memory that contains MAC addresses and the associated ports.

A Wireless Access Point connects wireless devices to the network.

But wireless communication spreads in the air, so it is similar to a Hub in the sense that the signal can reach more than one device.

The best rule to memorize:

```text
Layer 1 = Cables / Signals
Layer 2 = Switch / MAC Address / Frames
Layer 3 = IP Address / Packets
```