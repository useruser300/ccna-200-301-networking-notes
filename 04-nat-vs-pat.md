# NAT

Sure, this is the content in the same professional and organized style, as a network engineer explanation, while keeping the same sequence of ideas: NAT, then Static NAT, then Dynamic NAT, then PAT.

# 1) What is NAT?

NAT stands for:

**Network Address Translation**

And it means:

**Translating network addresses**

The main idea is that a device operating at Layer 3, such as:

* Router
* Firewall
* Layer 3 Device

changes the IP address inside the Packet Header.

NAT is often used to translate:

```text
Private IP  ->  Public IP
```

The goal is to allow devices that use Private IP addresses inside the network to access the Internet.

---

# 2) Why Do We Need NAT?

In the previous lesson, we learned that:

* Private IP is not routed on the Internet
* Public IP is the address that can be used on the Internet

Example:

Inside a home or company, devices usually get Private IPs such as:

```text
10.0.0.2
10.0.0.3
192.168.1.10
```

But the Internet cannot deal with these addresses directly.

So when an internal device wants to access the Internet, the router or firewall performs NAT.

This means it takes the Private IP and translates it into a Public IP that can be routed on the Internet.

---

# 3) Practical Home Example

At home, you have:

* Laptop
* Mobile
* TV
* Printer

All these devices usually get Private IPs from the router, such as:

```text
192.168.1.10
192.168.1.11
192.168.1.12
```

The router itself is connected to the service provider, such as:

* Vodafone
* Telekom
* O2
* Any other ISP

The service provider gives the router a Public IP.

When the laptop goes out to the Internet, it does not appear with its internal address `192.168.1.10`.

Instead, the router translates the address and makes it go out using the Public IP configured on the router.

---

# 4) What Does NAT Change Inside the Packet?

We have a Packet that contains an IP Header.

Inside the IP Header, there is:

* Source IP
* Destination IP

When the internal device wants to go out to the Internet, it may look like this:

```text
Source IP      = 10.0.0.2
Destination IP = Facebook
```

The router performs NAT and changes the Source IP:

```text
Source IP      = Public IP
Destination IP = Facebook
```

This means the server on the Internet does not see the internal address `10.0.0.2`.

It only sees the Public IP from which the request came.

---

# 5) Types of NAT

In this part, we focus on three main ideas:

* Static NAT
* Dynamic NAT
* PAT

Each one has a different use case.

---

# 6) Static NAT

Static NAT means:

**One-to-One Mapping**

Meaning:

```text
One Private IP  <->  One Public IP
```

This means we map an internal device to a fixed Public IP address.

---

# 7) When Do We Use Static NAT?

We use Static NAT when we have a device inside the private network and we want it to be reachable from the Internet.

Example:

We have a company, and inside the company there is a Web Server with a Private IP:

```text
Web Server Private IP = 10.0.0.3
```

And we want users from the Internet to be able to reach this server.

But users on the Internet cannot directly reach:

```text
10.0.0.3
```

because it is a Private IP.

So we configure Static NAT and map this server to a Public IP, such as:

```text
10.0.0.3  <->  20.0.0.3
```

So internally, the server has the address:

```text
10.0.0.3
```

But from the Internet, it appears as:

```text
20.0.0.3
```

---

# 8) NAT Table in Static NAT

The router or firewall keeps a table called:

**NAT Table**

In Cisco, we often hear terms such as:

* Inside Local
* Inside Global

## Inside Local

This is the real internal address of the device inside the network.

Example:

```text
10.0.0.3
```

## Inside Global

This is the address that this device appears with on the Internet.

Example:

```text
20.0.0.3
```

So the table may look like this:

| Inside Local | Inside Global |
| ------------ | ------------- |
| `10.0.0.3`   | `20.0.0.3`    |

---

# 9) How Does Static NAT Work When a Request Comes from the Internet?

If a device on the Internet wants to reach the server, it will send the request to:

```text
20.0.0.3
```

The router receives the Packet and sees:

```text
Destination IP = 20.0.0.3
```

Then it checks the NAT Table and finds that:

```text
20.0.0.3  ->  10.0.0.3
```

So it changes the Destination IP inside the IP Header:

```text
Destination IP = 10.0.0.3
```

Then it sends it to the internal server.

---

# 10) What Happens Inside the Header?

Before NAT:

```text
Source IP      = Client Public IP
Destination IP = 20.0.0.3
```

After NAT:

```text
Source IP      = Client Public IP
Destination IP = 10.0.0.3
```

Notice that the router did not change the idea of the request itself. It only changed the destination address inside the IP Header so the request can reach the correct internal server.

---

# 11) Dynamic NAT

Dynamic NAT means that the router has a group of Public IPs called:

**Pool**

And it temporarily assigns these addresses to internal devices when they want to access the Internet.

This means instead of having a permanent fixed mapping for every device, a Public IP is assigned from the Pool when needed.

In the image, Dynamic NAT has a Pool of Public IPs and assigns them to private devices inside the network.

---

# 12) The Idea of Dynamic NAT

We have an internal network with devices such as:

```text
Laptop 1 = 10.0.0.2
Laptop 2 = 10.0.0.3
Laptop 3 = 10.0.0.4
```

And the router has a Pool of Public IPs such as:

```text
20.0.0.2
20.0.0.3
20.0.0.4
```

When an internal device goes out to the Internet, the router gives it an available Public IP from the Pool.

Example:

```text
10.0.0.2  ->  20.0.0.2
10.0.0.3  ->  20.0.0.3
10.0.0.4  ->  20.0.0.4
```

This is recorded inside the NAT Table.

---

# 13) NAT Table in Dynamic NAT

Example of a Dynamic NAT table:

| Inside Local | Inside Global |
| ------------ | ------------- |
| `10.0.0.2`   | `20.0.0.2`    |
| `10.0.0.3`   | `20.0.0.3`    |
| `10.0.0.4`   | `20.0.0.4`    |

This means:

* Device `10.0.0.2` temporarily went out using `20.0.0.2`
* Device `10.0.0.3` temporarily went out using `20.0.0.3`
* Device `10.0.0.4` temporarily went out using `20.0.0.4`

When the reply comes back from the Internet to `20.0.0.2`, the router knows it must send it back to `10.0.0.2`.

---

# 14) How Does Dynamic NAT Work Step by Step?

Assume the device:

```text
10.0.0.2
```

wants to reach Facebook.

Before NAT, the Packet is approximately:

```text
Source IP      = 10.0.0.2
Destination IP = Facebook IP
```

The router receives the Packet, then searches in the Public IP Pool for an available address.

If it finds that:

```text
20.0.0.2
```

is available, it uses it.

After NAT, it becomes:

```text
Source IP      = 20.0.0.2
Destination IP = Facebook IP
```

For Facebook, the request came from:

```text
20.0.0.2
```

not from:

```text
10.0.0.2
```

because `10.0.0.2` is an internal address that is not visible on the Internet.

---

# 15) Why Do We Use Dynamic NAT?

Because we may have many internal devices, but not all of these devices access the Internet at the same time.

Example:

Inside the company, we have:

```text
255 devices
```

It is not necessary to buy 255 Public IPs.

We may only have:

```text
10 or 20 Public IPs
```

The router gives a Public IP to the device that needs Internet access at that moment.

This saves Public IPs, because Public IPv4 addresses are expensive and limited.

---

# 16) The Problem with Dynamic NAT

Although Dynamic NAT is better than buying a Public IP for every device, it still needs a number of Public IPs.

If you have 20 Public IPs in the Pool, this means only 20 devices can access the Internet at the same time using Dynamic NAT.

If device number 21 comes and there is no available Public IP, it will not be able to get a translation until an address from the Pool is released.

For this reason, a more important and more commonly used type appeared:

**PAT**

---

# 17) PAT

PAT stands for:

**Port Address Translation**

It is considered the most important type used practically in homes and companies.

Sometimes it is also called:

**NAT Overload**

The main idea:

Multiple devices inside the network can access the Internet using the same Public IP, but with different ports.

Meaning:

```text
Many Private IPs  ->  One Public IP + Different Ports
```

---

# 18) Why is PAT Important?

Because PAT allows a large number of devices to use only one Public IP.

Example:

Inside the network, we have:

```text
10.0.0.2
10.0.0.3
10.0.0.4
```

And all of them go out to the Internet using one Public IP:

```text
20.0.0.3
```

But the router distinguishes between them using ports.

---

# 19) The Idea of Ports in PAT

In TCP or UDP, every connection uses:

* Source Port
* Destination Port

HTTP example:

```text
Destination Port = 80
```

The Source Port is usually a temporary number chosen by the device.

When the router performs PAT, it does not translate only the IP. It also translates the Port.

---

# 20) PAT Example for the First Device

Assume the device:

```text
10.0.0.2
```

wants to open Facebook using HTTP.

Before PAT:

```text
Source IP        = 10.0.0.2
Source Port      = 10001
Destination IP   = Facebook
Destination Port = 80
```

The router performs PAT and changes the Source IP and Source Port.

After PAT:

```text
Source IP        = 20.0.0.3
Source Port      = 40001
Destination IP   = Facebook
Destination Port = 80
```

For Facebook, the request came from:

```text
20.0.0.3:40001
```

not from:

```text
10.0.0.2:10001
```

---

# 21) NAT/PAT Table for the First Device

The router records this in the translation table:

| Inside Local      | Inside Global     |
| ----------------- | ----------------- |
| `10.0.0.2:10001`  | `20.0.0.3:40001`  |

This means:

Any reply that returns to:

```text
20.0.0.3:40001
```

is sent internally to:

```text
10.0.0.2:10001
```

---

# 22) When Facebook Replies

Facebook replies to the address it saw:

```text
Destination IP   = 20.0.0.3
Destination Port = 40001
```

The router receives the reply and checks the PAT Table.

It finds:

```text
20.0.0.3:40001  ->  10.0.0.2:10001
```

So it changes the Destination IP and Destination Port to the correct internal device:

```text
Destination IP   = 10.0.0.2
Destination Port = 10001
```

Then it sends the reply to the laptop.

The laptop does not see the translation that happened in the middle.  
From its perspective, it sent a request and received the reply normally.

---

# 23) PAT Example for a Second Device

Assume a second device:

```text
10.0.0.4
```

also wants to reach Facebook.

Before PAT:

```text
Source IP        = 10.0.0.4
Source Port      = 10001
Destination IP   = Facebook
Destination Port = 80
```

The router uses the same Public IP:

```text
20.0.0.3
```

But it gives it a different Source Port, such as:

```text
40005
```

After PAT:

```text
Source IP        = 20.0.0.3
Source Port      = 40005
Destination IP   = Facebook
Destination Port = 80
```

---

# 24) How Does Facebook See the Devices?

Facebook sees the two requests as follows:

```text
20.0.0.3:40001
20.0.0.3:40005
```

From Facebook’s perspective, both requests came from the same Public IP, but from different ports.

But in reality, they came from two different devices inside the network:

```text
10.0.0.2
10.0.0.4
```

The router is the one that knows the difference through the PAT Table.

---

# 25) PAT Table with More Than One Device

Example PAT table:

| Inside Local      | Inside Global     |
| ----------------- | ----------------- |
| `10.0.0.2:10001`  | `20.0.0.3:40001`  |
| `10.0.0.2:10002`  | `20.0.0.3:40002`  |
| `10.0.0.3:10001`  | `20.0.0.3:40003`  |
| `10.0.0.3:10002`  | `20.0.0.3:40004`  |
| `10.0.0.4:10001`  | `20.0.0.3:40005`  |

This table shows that the same Public IP can serve multiple devices and multiple sessions, because the distinction is done using the Port Number.

---

# 26) The Difference Between Static NAT, Dynamic NAT, and PAT

| Type        | Idea                              | Number of Private IPs | Number of Public IPs | Usage                                      |
| ----------- | --------------------------------- | --------------------- | -------------------- | ------------------------------------------ |
| Static NAT  | Fixed One-to-One mapping          | One                   | One                  | Publishing an internal server to the Internet |
| Dynamic NAT | Public IP from a Pool when needed | Multiple devices      | Multiple Public IPs  | Internal devices going out using a Pool    |
| PAT         | IP + Port translation             | Multiple devices      | Usually one Public IP | Many devices going out to the Internet     |

---

# 27) Practical Comparison

## Static NAT

```text
10.0.0.3  <->  20.0.0.3
```

Suitable if you have an internal Web Server and you want users from the Internet to reach it.

## Dynamic NAT

```text
10.0.0.2  ->  20.0.0.2
10.0.0.3  ->  20.0.0.3
10.0.0.4  ->  20.0.0.4
```

Suitable if you have a Pool of Public IPs and you want to temporarily assign them to devices that go out to the Internet.

## PAT

```text
10.0.0.2:10001  ->  20.0.0.3:40001
10.0.0.3:10001  ->  20.0.0.3:40003
10.0.0.4:10001  ->  20.0.0.3:40005
```

Suitable when you want a large number of devices to access the Internet using one Public IP.

This is what is commonly used in home networks, small companies, and even in many practical environments.

---

# 28) What Happens to the Packet During NAT/PAT?

The main idea is that the router or firewall does not change the application content itself.

For example, if the request is HTTP, the HTTP Request remains the same.

But the change happens in the headers, especially:

## In NAT

**IP Header**

```text
Source IP or Destination IP
```

## In PAT

**IP Header + TCP/UDP Header**

```text
Source IP + Source Port
```

Or in the reply:

```text
Destination IP + Destination Port
```

Therefore, NAT and PAT depend on understanding Layer 3, and PAT also needs information from Layer 4 such as TCP/UDP Ports.

---

# 29) Very Important Point

NAT is mostly used for going out from the internal network to the Internet.

But if you want a user from the Internet to enter an internal server, you often need:

* Static NAT
* Or Port Forwarding
* Or Load Balancer
* Or Reverse Proxy
* Or Firewall Publishing Rule

depending on the design used.

## Example

A connection starts from the Internet to the inside.

A user on the Internet wants to access a Web Server inside your company.

The internal server has a Private IP:

```text
10.0.0.3
```

Here, the problem is that the external user cannot send directly to:

```text
10.0.0.3
```

because it is a Private IP.

In this case, you need a method that tells the router:

Any request that comes to a specific Public IP, translate it to the internal server `10.0.0.3`.

Here we use things such as:

* Static NAT
* Port Forwarding
* Load Balancer
* Reverse Proxy
* Firewall Publishing Rule

---

# 30) Summary

The final idea is:

* NAT means Network Address Translation
* NAT changes the IP Address inside the Packet Header
* The main goal is to allow devices with Private IPs to access the Internet
* Static NAT performs One-to-One Mapping between a Private IP and a Public IP
* Static NAT is suitable for publishing an internal server to the Internet
* Dynamic NAT uses a Pool of Public IPs and assigns them when needed
* Dynamic NAT saves addresses, but it still needs more than one Public IP
* PAT means Port Address Translation
* PAT allows multiple devices to access the Internet using one Public IP
* PAT distinguishes between devices and sessions using Ports
* PAT is the most commonly used type in home networks and companies
* The router or firewall keeps a NAT/PAT Table so it knows how to return the reply to the correct internal device