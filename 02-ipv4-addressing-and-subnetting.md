# 1) IPv4

IPv4 is a protocol that operates at **Layer 3**.

Its main function is:

- To provide a **Layer 3 address**
- Meaning it gives the packet a logical address
- And this address remains **End-to-End**
- In other words, it does not change from the beginning of the path to the end

This means that when a laptop sends a packet to a server:

- A **Source IP** is added
- And a **Destination IP** is added

Example:

- Laptop: `10.0.0.2`
- Server: `20.0.0.2`

So the packet leaves the laptop with:

- Source IP = `10.0.0.2`
- Destination IP = `20.0.0.2`

And these two addresses remain with the packet throughout the entire path until it reaches the server.

---

# 2) The Role of Routers with IPv4

Routers operate at **Layer 3**.

Their function is:

- To connect different networks together
- To forward packets from one network to another
- To choose the best path to reach the required network

You can think of the routers between the laptop and the server as a simplified image of the Internet.

Each router has:

- More than one interface
- A **Routing Table**

The Routing Table contains:

- Network Address
- And the path or interface through which the packet should be sent

Example:  
If the packet wants to reach a network that starts with `20`, then the router looks at:

- The Destination IP
- Then compares it with the Routing Table
- Then chooses the correct interface to continue the path

---

# 3) IPv4 and Network Address

IPv4 is not used only as a device address. It is also used to form something called a:

**Network Address**

This is very important because the router does not want to store every single IP individually inside the Routing Table. It is better to deal with networks as groups.

Example:

Instead of putting these inside the router:

- `20.0.0.1`
- `20.0.0.5`
- `20.0.0.6`
- `20.0.0.7`

It is better to say:

- Anything that starts with `20` or belongs to the network `20.0.0.0/8`
- Goes out through this direction

This makes the Routing Table smaller, clearer, and easier to use.

---

# 4) IPv4 Format

An IPv4 address has a length of:

**32 bits**

It is represented in two ways:

- Decimal
- Binary

And it consists of:

**4 Octets**

Each octet ranges:

- From `0` to `255`

Decimal example:  
`172.255.0.15`

Binary equivalent:  
`10101100.11111111.00000000.00001111`

This means the same address can be read in decimal format or binary format.

---

# 5) The Weights of the 8 Bits in Each Octet

Each octet contains 8 bits, and their weights are:

`128 64 32 16 8 4 2 1`

These weights are used when we want to convert:

- From Decimal to Binary
- Or from Binary to Decimal

---

# 6) How to Convert from Decimal to Binary

If we want to convert a number such as:  
`172`

We use the values:

`128 64 32 16 8 4 2 1`

And we check whether the number contains each value or not.

## Example: 172

- 172 contains 128 → write 1
- Remaining = 44
- 44 does not contain 64 → write 0
- 44 contains 32 → write 1
- Remaining = 12
- 12 does not contain 16 → write 0
- 12 contains 8 → write 1
- Remaining = 4
- 4 contains 4 → write 1
- Nothing remains
- Then we write 0 and 0

So it becomes:  
`10101100`

## Example: 255

The number 255 means all values are present, so:

`11111111`

## Example: 0

The number 0 means no value is present, so:

`00000000`

## Example: 15

The number 15 = 8 + 4 + 2 + 1

So it becomes:  
`00001111`

---

# 7) How to Convert from Binary to Decimal

We only look at the positions that contain `1` and add their weights.

Example:  
`10101100`

This means:

- 128 is present
- 32 is present
- 8 is present
- 4 is present

So the result is:  
`128 + 32 + 8 + 4 = 172`

Example:  
`11000000`

This means:

- 128 is present
- 64 is present

So the result is:  
`128 + 64 = 192`

---

# 8) Subnet Mask

The **Subnet Mask** is used to determine:

- What is the **Network Part**
- What is the **Host Part**

This means that when you see an IP address together with a Subnet Mask, you can identify:

- Which part is fixed and represents the network
- Which part is variable and represents the devices inside that network

---

# 9) Ways to Represent the Subnet Mask

The Subnet Mask can be written in several forms:

## 1. Slash Notation

Such as:

- `/8`
- `/16`
- `/24`
- `/26`

## 2. Binary

Such as:

- `/8` → `11111111.00000000.00000000.00000000`
- `/16` → `11111111.11111111.00000000.00000000`
- `/24` → `11111111.11111111.11111111.00000000`
- `/26` → `11111111.11111111.11111111.11000000`

## 3. Decimal

Such as:

- `/8` → `255.0.0.0`
- `/16` → `255.255.0.0`
- `/24` → `255.255.255.0`
- `/26` → `255.255.255.192`

---

# 10) The Meaning of /24 or /26

When we say:

`/24`

This means:

- The first 24 bits are the **Network Part**
- The remaining 8 bits are the **Host Part**

And when we say:

`/26`

This means:

- The first 26 bits are the **Network Part**
- The remaining 6 bits are the **Host Part**

---

# 11) Network Part and Host Part

Example:  
`10.0.0.0/8`

The meaning of `/8` is:

- The first 8 bits are the Network Part
- The last 24 bits are the Host Part

So all devices inside this network must share the first network portion.

This means that if the network is:  
`10.0.0.0/8`

Then possible devices inside it may be such as:

- `10.0.0.1`
- `10.0.0.2`
- `10.1.5.9`
- `10.20.30.40`

All of them share the network portion, which is the first 8 bits.

---

# 12) Network Address

The **Network Address** is the address of the network itself.

This address is used by the router inside the:  
**Routing Table**

The Network Address is identified by the bits that correspond to `1` in the Subnet Mask.

This means:

- The network bits stay as they are
- The host bits are converted to `0`

---

# 13) Host Address

The **Host Address** is the address assigned to devices inside the network, such as:

- Laptop
- PC
- Server

This part is identified by the bits that correspond to `0` in the Subnet Mask.

---

# 14) Broadcast Address

The **Broadcast Address** is a special address used by the network to send traffic to all devices inside the same network at once.

In this address:

- The Network bits remain unchanged
- All Host bits are converted to `1`

---

# 15) A Note About Classes

Historically, IPv4 was divided into classes:

## Class A

- First octet from `1` to `127`

Example:

- `10.0.0.0`

## Class B

- First octet from `128` to `191`

Example:

- `172.16.0.0`

## Class C

- First octet from `192` to `223`

Example:

- `192.168.1.0`

This idea is historical and useful for general understanding, but what matters more in practice is:

- Network
- Host
- Subnet Mask
- Subnetting

---

# 16) Summary

Up to this point, we have the following:

- IPv4 is a protocol that operates at Layer 3
- It gives each device a logical address
- This address is used for communication inside the same network or with another network
- Routers use the Network Address inside the Routing Table
- IPv4 has a length of 32 bits
- It consists of 4 Octets
- The Subnet Mask determines the Network Part and the Host Part
- There is a Network Address, a Host Address, and a Broadcast Address

---

# 17) Exercise 1

We have:

`10.0.1.5/24`

And we need to find:

- Network Address
- Number of IPs
- Number of usable Hosts
- Broadcast Address
- Host Range

---

## Step 1: Understand /24

`/24` means:

- The first 24 bits are for the network
- The last 8 bits are for the host

So the Subnet Mask is:

`255.255.255.0`

---

## Step 2: Find the Network Address

In `/24`:

- The first 3 octets are the Network Part
- The last octet is the Host Part

We have:  
`10.0.1.5`

So:

- The network portion remains the same: `10.0.1`
- The host portion becomes 0

So it becomes:

**Network Address = `10.0.1.0/24`**

---

## Step 3: Number of IPs

We still have 8 host bits.

So:

`2^8 = 256`

Therefore:

**Total IPs = 256**

---

## Step 4: Broadcast Address

In the Broadcast Address:

- The Network Part stays the same
- All host bits become 1

The last octet has 8 bits, all set to 1:  
`11111111 = 255`

So:

**Broadcast Address = `10.0.1.255`**

---

## Step 5: Number of Usable Hosts

We have 256 total addresses, but 2 addresses are reserved:

- One for the Network Address
- One for the Broadcast Address

So:

`256 - 2 = 254`

**Usable Hosts = 254**

---

## Step 6: Host Range

The first usable host comes right after the Network Address:

- First Host = `10.0.1.1`

The last usable host comes right before the Broadcast Address:

- Last Host = `10.0.1.254`

So:

**Host Range = `10.0.1.1 - 10.0.1.254`**

---

# 18) Subnetting

**Subnetting** means dividing one network into several smaller networks.

Example:  
We have the network:

`10.0.0.0/24`

And we want to divide it into:

**4 Subnets**

Why do we do this?

Because `/24` gives 256 addresses, and we may not need all of them in one place.  
So instead of keeping one large network, we can divide it into smaller and more organized networks.

---

# 19) How to Divide /24 into 4 Subnets

Originally, we have:

`10.0.0.0/24`

And in `/24`:

- The first 24 bits are for the network
- The last 8 bits are for the host

If we want 4 subnets, we need:

`2^2 = 4`

So we take:
**2 bits from the Host Part**
and add them to the Network Part

So it becomes:

`/26`

Because:

- It was `/24`
- We borrowed 2 bits
- So it became `/26`

---

# 20) Number of Addresses in Each Subnet

In `/26`:

- We have 6 host bits left

So:

`2^6 = 64`

Therefore each subnet has:

**64 Total IPs**

And the number of usable hosts is:

`64 - 2 = 62`

---

# 21) The First Network

## Subnet 1

**Network Address:**  
`10.0.0.0/26`

**Broadcast Address:**  
`10.0.0.63`

**Host Range:**  
`10.0.0.1 - 10.0.0.62`

**Usable Hosts:**  
`62`

---

# 22) The Second Network

## Subnet 2

**Network Address:**  
`10.0.0.64/26`

**Broadcast Address:**  
`10.0.0.127`

**Host Range:**  
`10.0.0.65 - 10.0.0.126`

**Usable Hosts:**  
`62`

---

# 23) The Third Network

## Subnet 3

**Network Address:**  
`10.0.0.128/26`

**Broadcast Address:**  
`10.0.0.191`

**Host Range:**  
`10.0.0.129 - 10.0.0.190`

**Usable Hosts:**  
`62`

---

# 24) The Fourth Network

## Subnet 4

**Network Address:**  
`10.0.0.192/26`

**Broadcast Address:**  
`10.0.0.255`

**Host Range:**  
`10.0.0.193 - 10.0.0.254`

**Usable Hosts:**  
`62`

---

# 25) The General Rule in Subnetting

If you borrow `n` bits from the Host Part and use them for the Network Part:

## Number of Subnets

`2^n`

## Number of Addresses in Each Subnet

`2^(number of remaining host bits)`

## Number of Usable Hosts

`2^(number of remaining host bits) - 2`

---

# 26) One More Quick Example

If we have:

`10.0.0.8/27`

Then `/27` means:

- 27 bits for the network
- 5 bits for the host

So:

- Total IPs = `2^5 = 32`
- Usable Hosts = `32 - 2 = 30`

In this type of example:

- The Network Address starts at the first matching block
- The Broadcast Address is the last address in that block
- And the Host Range is between them

In the given example:

- **Network Address = `10.0.0.0/27`**
- **Broadcast Address = `10.0.0.31`**
- **Host Range = `10.0.0.1 - 10.0.0.30`**
- **Total IPs = 32**
- **Usable Hosts = 30**

---

# 27) Summary

Now the full idea becomes:

- IPv4 is a logical address that operates at Layer 3
- It has a length of 32 bits
- It consists of 4 Octets
- It can be represented in Decimal or Binary
- The Subnet Mask determines the Network Part and the Host Part
- The Network Address is used in the Routing Table
- The Host Address is assigned to devices
- The Broadcast Address is used to reach all devices in the same network
- `/24` means 24 bits for the network and 8 bits for the host
- Subnetting means dividing one large network into smaller networks

