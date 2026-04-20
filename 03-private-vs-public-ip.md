# Private IP vs Public IP

# 1) Review

In the previous lesson, we explained that **IPv4** is a protocol that operates at **Layer 3**.

Its main function is to give devices a logical address called:

**IP Address**

This address allows devices to communicate with each other inside the same network or across different networks.

IPv4 consists of:

**32 bits**

This gives us an approximate number of addresses:

```text
2^32 = 4,294,967,296 IP addresses
```

This means around 4.3 billion IPv4 addresses.

In theory, this number looks large, but in practice, it is no longer enough because every device needs a unique address. With the increasing number of devices such as laptops, phones, servers, cameras, cars, and IoT devices, the number of IPv4 addresses became insufficient to cover all devices globally.

This is where the idea of dividing IPv4 addresses into two main types appeared:

* **Private IP Addresses**
* **Public IP Addresses**

---

# 2) Private IP Addresses

A **Private IP Address** is an address used only inside internal networks.

This means it is used inside:

* A home network
* A company network
* A training lab network
* An internal data center network
* An internal Cloud network such as a VPC or VNet

The main idea is that this address is not routed directly over the Internet.

In other words:

```text
Private IP addresses are not routable on the Internet.
```

This means public Internet routers do not treat these addresses as global destinations.

---

# 3) Why is Private IP Not Routable on the Internet?

Because Private IP addresses can be reused in millions of networks around the world.

Example:

Inside your home, your device might be:

```text
192.168.1.10
```

In another person’s home, they may have a device with the same address:

```text
192.168.1.10
```

In another company, they may also have the same address.

This does not cause a problem because these addresses are used inside private and separate networks, not as direct global addresses on the Internet.

But if we tried to route these addresses on the Internet, a huge conflict would happen because the same address exists in many places.

That is why Private IPs are prevented from being routed on the public Internet.

---

# 4) Private IP Ranges

Three main IPv4 ranges were reserved for use as private addresses.

## Range 1

```text
10.0.0.0 - 10.255.255.255
```

Written in CIDR notation as:

```text
10.0.0.0/8
```

Any address that starts with `10` is considered a Private IP.

Examples:

```text
10.0.0.2
10.1.5.10
10.20.30.40
10.255.255.254
```

---

## Range 2

```text
172.16.0.0 - 172.31.255.255
```

Written in CIDR notation as:

```text
172.16.0.0/12
```

This means the private range starts from:

```text
172.16.0.0
```

And ends at:

```text
172.31.255.255
```

Examples:

```text
172.16.0.1
172.17.10.20
172.20.5.50
172.31.255.200
```

Very important here:

Not every address that starts with `172` is Private.

Only this range is private:

```text
172.16.0.0 - 172.31.255.255
```

---

## Range 3

```text
192.168.0.0 - 192.168.255.255
```

Written in CIDR notation as:

```text
192.168.0.0/16
```

Any address that starts with `192.168` is considered a Private IP.

Examples:

```text
192.168.0.1
192.168.1.10
192.168.100.50
192.168.255.254
```

---

# 5) Private IP Ranges Table

| Private Range                   |  CIDR | Common Use                             |
| ------------------------------- | ----: | -------------------------------------- |
| `10.0.0.0 - 10.255.255.255`     |  `/8` | Large companies, Cloud VPC/VNet        |
| `172.16.0.0 - 172.31.255.255`   | `/12` | Medium internal networks, often Docker |
| `192.168.0.0 - 192.168.255.255` | `/16` | Home networks and small offices        |

---

# 6) Example of an Internal Network Using Private IP

Assume we have a simple internal network inside a company:

```text
Laptop  ->  Switch  ->  Server
```

We can assign the following addresses to the devices:

```text
Laptop: 10.0.0.2
Server: 10.0.0.3
```

As long as both devices are inside the same network, or there is correct internal routing between them, they can communicate using these addresses.

In this case, we do not need a Public IP because the communication is internal only.

Example:

The laptop wants to reach the internal server:

```text
10.0.0.2  ->  10.0.0.3
```

This connection stays inside the private network.

---

# 7) Public IP Addresses

A **Public IP Address** is an address used on the public Internet.

This address is:

* Global
* Routable over the Internet
* Must not be duplicated globally for the same use at the same time
* Used to reach devices or services over the Internet

Meaning:

```text
Public IP addresses are globally unique and routable on the Internet.
```

Example:

```text
Laptop: 30.0.0.2
Server: 20.0.0.3
```

If both devices are on the public Internet, they need Public IP addresses so the Internet can route traffic between them.

---

# 8) Who Manages Public IP Addresses?

Public IP addresses are not chosen randomly.

They are organized globally by authorities responsible for address allocation. The most well-known central authority in this field is:

**IANA**

The idea is that Public IP distribution must be organized so that conflicts do not happen between networks around the world.

In real-world practice, distribution happens at multiple levels:

* IANA
* Regional Internet Registries
* Internet Service Providers
* Then companies or users

But the main idea here is that Public IPs are managed globally, unlike Private IPs, which can be used freely inside internal networks.

---

# 9) When Do We Use a Public IP?

We use a Public IP when we want a device or service to be reachable from the Internet.

Examples:

* Web Server available to users
* VPN Gateway
* Public Load Balancer
* External Firewall
* Router connected to the Internet
* Cloud Instance that needs direct access from the Internet

Practical example:

You have a Web Server that serves a website to users.

For a user outside the company to reach it, there must be a Public IP or a Public-facing service such as a Load Balancer in front of it.

---

# 10) When Do We Use a Private IP?

We use a Private IP when the communication is internal.

Examples:

* Employee device inside the company
* Internal Database Server
* Application Server behind a Load Balancer
* Devices inside a VPC in AWS
* Devices inside a VNet in Azure
* Home devices behind the router

Simple architecture example:

```text
User on Internet
      |
 Public IP
      |
Load Balancer
      |
Private IP
      |
Application Server
      |
Private IP
      |
Database Server
```

In professional designs, we usually do not give everything a Public IP.

Usually:

* Only the external entry point is Public
* Internal servers use Private IPs
* Databases remain Private only

---

# 11) Practical Difference Between Private IP and Public IP

| Comparison                            | Private IP                                | Public IP                             |
| ------------------------------------- | ----------------------------------------- | ------------------------------------- |
| Where it is used                      | Inside internal networks                  | On the public Internet                |
| Routable on the Internet              | No                                        | Yes                                   |
| Can be repeated in different networks | Yes                                       | No, not in the same global context    |
| Example                               | `10.0.0.2`                                | `20.0.0.3`                            |
| Usage                                 | Internal devices, internal servers, VPC/VNet | Web servers, routers, load balancers |
| Management                            | You choose it inside your network         | Assigned by ISP/Cloud Provider        |

---

# 12) Why Do We Not Give Every Device a Public IP?

From a network design perspective, this is not practical and not secure.

The reasons are:

First: IPv4 addresses are limited.  
There are not enough Public IPv4 addresses for all devices in the world.

Second: Security.  
It is not a good idea for every device inside a company to be directly exposed to the Internet.

Third: Organization.  
Using Private IP internally makes network design easier, and you can divide networks into internal subnets such as:

```text
10.0.1.0/24  -> Users
10.0.2.0/24  -> Servers
10.0.3.0/24  -> Databases
```

Fourth: Reuse.  
The same Private Ranges can be used in different companies, homes, and Cloud environments without conflict because they are not globally routed.

---

# 13) How Do Private IP Devices Reach the Internet?

Here comes a very important idea:

**NAT**

Short for:

**Network Address Translation**

The idea is that internal devices use Private IPs, but when they want to go out to the Internet, their internal address is translated into a Public IP.

Example inside the network:

```text
Laptop: 10.0.0.2
Server: 10.0.0.3
Mobile: 10.0.0.4
```

When these devices go out to the Internet, they do not appear with these private addresses.

Instead, they go out through a Public IP that exists on the router, firewall, or NAT Gateway.

Example:

```text
10.0.0.2  ->  Public IP  ->  Internet
10.0.0.3  ->  Public IP  ->  Internet
10.0.0.4  ->  Public IP  ->  Internet
```

This way, multiple internal devices can share one Public IP or multiple Public IPs to access the Internet.

NAT details come in the next lesson.

---

# 14) Complete Engineering Example

We have a small company network:

```text
Laptop: 10.0.0.2
Internal Server: 10.0.0.3
Default Gateway / Router: 10.0.0.1
```

These devices communicate internally using Private IPs.

If the laptop wants to reach an internal server:

```text
10.0.0.2 -> 10.0.0.3
```

The traffic stays inside the network.

But if the laptop wants to access a website on the Internet, such as an external Web Server:

```text
10.0.0.2 -> Internet Server
```

The laptop sends the traffic to the Default Gateway.

Then the router or NAT Device translates the internal address into a Public IP and sends the traffic to the Internet.

---

# 15) Summary

The final idea is:

* IPv4 consists of 32 bits
* The number of IPv4 addresses is around 4.3 billion
* This number is not enough for all devices in the world
* Therefore, usage was divided into Private IP and Public IP
* Private IP is used inside internal networks
* Private IP is not routable on the public Internet
* Public IP is used on the Internet
* Public IP is globally unique and routable
* Private IP Ranges are:

```text
10.0.0.0/8
172.16.0.0/12
192.168.0.0/16
```

* Internal devices use Private IPs
* Services that need Internet access require a Public IP or must be behind a Public-facing service
* NAT allows devices with Private IPs to access the Internet using a Public IP
* This design is the foundation used in homes, companies, and Cloud providers such as AWS and Azure