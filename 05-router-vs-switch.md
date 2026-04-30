# Router vs Switch

# 1) Introduction

To understand the difference between a **Router** and a **Switch** correctly, we need to connect the topic directly to the **OSI Model**.

The fundamental difference between them is:

* A **Router** operates at **Layer 3**
* A **Switch** operates at **Layer 2**

And this is not just a theoretical classification, but it is what determines:

* What each device examines
* What type of addresses it deals with
* And when we use it inside the network

---

# 2) Router

A **Router** is a device that operates at the **Network Layer (Layer 3)**.

Its main function is:

* Connecting **different networks**
* And making forwarding decisions based on the **IP Address**

This means that when a Packet reaches the router, it does not care about the MAC address as the main forwarding decision, but instead looks at:

* **Destination IP**
* Then compares it with the **Routing Table**
* Then decides from which Interface or Port it should send the Packet

---

# 3) How Do We Understand the Router Practically?

A router usually has multiple Interfaces or Ports.

And each Port on the router belongs to a **different Network**.

For example:

* Port 1 is connected to the network `10.0.0.0/24`
* Port 2 is connected to the network `20.0.0.0/24`

In this case:

* Port 1 gets an IP from network 10
* Port 2 gets an IP from network 20

For example:

* Port 1 = `10.0.0.1`
* Port 2 = `20.0.0.1`

This is a very important point:

**Each Interface on the router belongs to a different network, and gets an IP from that same network.**

---

# 4) Practical Example of a Router

We have:

* Laptop = `10.0.0.2`
* Router Port 1 = `10.0.0.1`
* Router Port 2 = `20.0.0.1`
* Server = `20.0.0.2`

Here, the laptop is in the network:

`10.0.0.0/24`

And the server is in the network:

`20.0.0.0/24`

Since the two devices are in **two different networks**, a Switch alone is not enough.  
We need a device that connects the two networks, and that is the role of the router.

---

# 5) What Does the Router Do When the Laptop Sends to the Server?

If the laptop `10.0.0.2` wants to send traffic to the server `20.0.0.2`:

Then the Packet will leave, for example, carrying:

* Source IP = `10.0.0.2`
* Destination IP = `20.0.0.2`

This Packet reaches the router.

The router does the following:

1. Looks at the **Destination IP**
2. Checks the **Routing Table**
3. Finds that the network `20.0.0.0/24` exists through **Port 2**
4. Sends the Packet out of **Port 2** toward the server

---

# 6) Routing Table

The **Routing Table** is the table the router depends on to make forwarding decisions.

A simple example:

| Port | Network       |
| ---- | ------------- |
| 1    | `10.0.0.0/24` |
| 2    | `20.0.0.0/24` |

If a Packet arrives destined for `20.0.0.2`, the router matches it with the network `20.0.0.0/24` and knows that it must go out from Port 2.

So the router does not send randomly, but depends on:

* IP Address
* Routing Table

---

# 7) Summary of the Router’s Function

The router:

* Layer 3 device
* Examines the **IP Address**
* Connects **Different Networks**
* Each Interface on it is in a **Different Network**
* Each Interface gets an **IP** from the network it belongs to
* Depends on the **Routing Table** to forward Packets

---

# 8) Switch

A **Switch** is a device that operates at the **Data Link Layer (Layer 2)**.

Its main function is:

* Connecting devices within the **same Layer 2 technology**
* And today, in practice, this usually means **Ethernet**

This means the Switch connects devices that exist in the same local network, and forwards Frames based on:

**MAC Address**

---

# 9) What Is the Layer 2 Technology Here?

The most common Layer 2 technology meant here is:

**Ethernet**

And Ethernet depends on:

* Frames
* MAC Addresses

Therefore, the switch works based on:

* Source MAC
* Destination MAC
* MAC Table

---

# 10) MAC Address

A **MAC Address** is a Layer 2 address.

It is usually written in this form:

`00:1A:2B:3C:4D:5E`

And it consists of:

* 12 Hex characters

And Hex means:

* Numbers from 0 to 9
* And letters from A to F

Example:

`00:1A:2B:3C:4D:5E`

This is a complete MAC address.

---

# 11) An Important Idea About the MAC Address

Usually:

* The first part of the MAC indicates the manufacturer
* And the remaining part identifies the device itself

And the MAC Address is associated with the network card, the **NIC**.

In the traditional meaning at this learning level:

* The MAC is fixed
* We do not deal with it like an IP
* بينما الـ IP can be changed depending on the network

---

# 12) How Does a Switch Work?

The switch receives a **Frame**.

Then it looks at:

* **Destination MAC**

After that, it compares this address with an internal table called:

**MAC Table**

Then it decides from which Port it should send the Frame.

---

# 13) MAC Table

The **MAC Table** is the table the switch uses to know:

* Which MAC Address exists on which Port

Example:

| Port | MAC |
| ---- | --- |
| 1    | A   |
| 2    | B   |

If a Frame arrives at the switch and the Destination MAC = B,  
then the switch sends the Frame out of Port 2.

---

# 14) Practical Example of a Switch

We have:

* Laptop A
* Server B
* A Switch between them

And both devices are in the **same network**.

For example:

* Laptop = `10.0.0.2`
* Server = `10.0.0.3`

Here, we do not need a Router for them to communicate, because they are already inside the **same network**.

What we need is only a Switch.

---

# 15) What Happens When the Laptop Sends to the Server Through a Switch?

If the laptop wants to send a request to the server:

Then at Layer 3 it may be:

* Source IP = `10.0.0.2`
* Destination IP = `10.0.0.3`

But when the data goes down to Layer 2, it becomes a Frame, and it contains:

* Source MAC = Laptop MAC
* Destination MAC = Server MAC

Then the Frame is sent to the switch.

The switch looks at:

* Destination MAC

Then it checks the MAC Table.

If it finds, for example:

* MAC A on Port 1
* MAC B on Port 2

And the Destination MAC is B,  
then it sends the Frame out of Port 2 to the server.

---

# 16) The Fundamental Point About the Switch

A switch does not connect different networks.

A switch connects **devices inside the same network**.

And this is the basic difference from the router.

Meaning:

* **Router**: between different networks
* **Switch**: between devices inside the same network

---

# 17) The Practical Difference Between Router and Switch

## Router

* Layer 3
* Deals with IP
* Connects different networks
* Uses Routing Table
* Each Interface on it is in a different network

## Switch

* Layer 2
* Deals with MAC
* Connects devices inside the same network
* Uses MAC Table
* Does not connect different networks in the same way as a router

---

# 18) A Direct Example That Shows the Difference

## Router Case

We have:

* Laptop = `10.0.0.2`
* Server = `20.0.0.2`

Here the two devices are in two different networks:

* `10.0.0.0/24`
* `20.0.0.0/24`

So we need:
**Router**

---

## Switch Case

We have:

* Laptop = `10.0.0.2`
* Server = `10.0.0.3`

Here the two devices are in the same network:

* `10.0.0.0/24`

So we need:
**Switch**

---

# 19) Does the Switch Get an IP?

In this basic explanation here:

The switch, as a Layer 2 device, does not make forwarding decisions based on IP, but based on MAC.

This means in its main role inside the data plane:

* It does not depend on IP for forwarding
* But depends on the MAC Table

---

# 20) Multilayer Switch (MLS)

There is an important type called:

**Multilayer Switch**  
or  
**Layer 3 Switch**

This device combines both functions:

* It works like a Switch at Layer 2
* And works like a Router at Layer 3

---

# 21) What Does a Multilayer Switch Do?

A Multilayer Switch can:

* Forward Frames based on MAC addresses
* Forward Packets based on IP addresses

Meaning:

* If the traffic is inside the same Layer 2 domain, it behaves like a Switch
* And if the traffic is between different networks, it can perform Routing like a Router

---

# 22) Why Do We Use a Multilayer Switch?

Because it is very practical in enterprise networks.

For example, inside a company you may have:

* VLAN Users
* VLAN Servers
* VLAN Voice
* VLAN Management

And you need a device that:

* Connects devices like a switch
* And performs Inter-VLAN Routing like a router

Here, the Multilayer Switch is an excellent solution.

---

# 23) The Difference Between a Switch and a Multilayer Switch

## Layer 2 Switch

* Forwards based on MAC only
* Does not perform Routing between networks

## Multilayer Switch

* Forwards based on MAC
* And can also route based on IP
* Combines the characteristics of a Switch and a Router

---

# 24) Final Summary

The final idea is as follows:

* **Router** operates at Layer 3

* It examines Destination IP

* It uses Routing Table

* It connects different networks

* Each Port on it is in a different Network

* **Switch** operates at Layer 2

* It examines Destination MAC

* It uses MAC Table

* It connects devices in the same network

* **Multilayer Switch** operates at Layer 2 and Layer 3

* It can forward using MAC

* And it can route using IP

---

# 25) Very Short Conclusion

If you ask yourself:

**Are the two devices in the same network?**

* Yes → usually Switch

**Are the two devices in two different networks?**

* Yes → you need a Router or a Multilayer Switch

