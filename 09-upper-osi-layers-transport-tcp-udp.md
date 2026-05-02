# Upper OSI Layers — Application, Presentation, Session, Transport

## 1. The Idea

When you watch a video on YouTube or open any website, there are many processes happening inside the network before the page appears or the video starts.

In the previous lessons, the focus was on the lower layers of the OSI Model:

* Layer 1 - Physical
* Layer 2 - Data Link
* Layer 3 - Network

These layers are related to things such as:

* Cables
* Switches
* Routers
* MAC Addresses
* IP Addresses
* Frames
* Packets

Here, however, the focus is on the upper layers:

* Layer 7 - Application
* Layer 6 - Presentation
* Layer 5 - Session
* Layer 4 - Transport

These layers are the closest to the applications used by the user, such as:

* Web Browser
* YouTube
* Spotify
* Online Games
* Video Calls

## 2. The Scenario Used

We have a device that wants to open YouTube and watch a video.

The user opens the browser and types:

```text
youtube.com
```

or opens a specific video on YouTube.

From the user’s point of view, the matter is simple:

Open the browser → Type the website → Watch the video

But from the network’s point of view, there are several layers and protocols working together until the page is loaded and the video is played.

## 3. The Layers We Focus on Here

The upper layers are:

* Layer 7 - Application
* Layer 6 - Presentation
* Layer 5 - Session
* Layer 4 - Transport

In a simplified way:

```text
Application  = the application or protocol that uses the network
Presentation = data formatting and encryption
Session      = managing the communication session
Transport    = the method of transporting data between the two endpoints
```

## 4. Layer 7 — Application Layer

The Application Layer is the closest layer to the user and the programs.

This layer works when you have a program that needs to use the network.

Examples:

* Web Browser
* YouTube App
* Spotify
* Online Game
* Email Client
* SSH Client

If the application wants to communicate with another device over the network, it uses the Application Layer.

Example:

The browser wants to open `youtube.com`

Here, the browser uses Application Layer protocols such as:

* HTTP
* HTTPS
* DNS

## 5. The Function of the Application Layer

The Application Layer is not the application itself directly, but it is the layer that allows the application to interact with the network.

For example, the browser says:

I want the page `youtube.com`

Then the Application Layer starts preparing an appropriate request, such as:

**HTTP/HTTPS GET Request**

Its meaning is:

Send me this page or this resource.

## 6. Example of the Application Layer

When you type:

```text
youtube.com
```

the browser needs to communicate with the YouTube server.

So it starts creating a request such as:

```text
GET /
```

or other requests to retrieve:

* HTML
* CSS
* JavaScript
* Images
* Video content
* Thumbnails

All these requests begin at the Application Layer.

## 7. Layer 6 — Presentation Layer

After the application data is prepared, the data logically moves to:

**Layer 6 - Presentation Layer**

This layer is concerned with how the data becomes “understandable” to the other side.

The two most important functions here are:

* Data Format
* Encryption

## 8. Data Format

Data Format means the form or format of the data.

A simple example:

* PDF
* JPG
* PNG
* HTML
* XML
* JSON
* MP4

If someone sends you a file called:

```text
document.pdf
```

your device knows how to open it because PDF is a known format.

But if someone sends you a file in a strange unknown format, your device may not know how to handle it.

The same idea applies in networks.

Devices and applications need to agree on understandable data formats.

## 9. Examples of Presentation Layer Formats

On the web, we see formats such as:

* HTML
* CSS
* JavaScript
* JSON
* XML
* JPG
* PNG
* GIF
* MP4

For example, YouTube sends an HTML page to the browser, and the browser knows how to read it and display it.

So the Presentation Layer helps make the data into a format that is understandable and suitable for the receiving side.

## 10. Encryption in the Presentation Layer

The Presentation Layer is also concerned with encryption.

When you use a website that starts with:

```text
https://
```

this means that the connection is encrypted.

Encryption prevents anyone in the path from reading the data easily.

For example, instead of the data appearing like this:

```text
username=ali
password=123456
```

it becomes encrypted and unreadable to an observer.

## 11. SSL / TLS

Among the terms related to encryption are:

* SSL = Secure Sockets Layer
* TLS = Transport Layer Security

In practice today, TLS is the one widely used, but you will often hear people say SSL in a general sense.

Its function is:

**Encrypting the connection between the browser and the server**

Example:

```text
Browser ← encrypted HTTPS → YouTube Server
```

## 12. Layer 5 — Session Layer

After the Presentation Layer comes:

**Layer 5 - Session Layer**

The function of this layer is to manage the session between two sides.

This means:

* Starting the connection
* Maintaining it
* Organizing it
* Terminating it

## 13. What Does Session Mean?

Session means a logical communication session between two applications.

For example:

* Your browser talks to YouTube
* Spotify talks to the Spotify Server
* A VPN program talks to a VPN Server
* A calling application talks to a Call Server

Each of these connections can be considered a Session.

## 14. The Function of the Session Layer

The Session Layer is concerned with keeping the connection organized.

For example:

* Opening the session
* Continuing the conversation
* Ensuring that the connection remains active
* Closing the session when finished

From the point of view of the lower layers, the data may pass through many Routers and Switches.

But from the point of view of the Session Layer, there is an ongoing “conversation” between one application and another application.

## 15. Examples of Session Layer Protocols

Among the protocols or technologies that may be associated with this layer are:

* L2TP
* RTCP
* H.245
* SOCKS

### L2TP

Layer 2 Tunneling Protocol

It is widely used in VPN connections.

### RTCP

Real-time Transport Control Protocol

It helps control audio and video sessions.

### H.245

It is used in setting up and managing some video calls.

### SOCKS Proxy

It is used as a Proxy to forward the connection through an intermediary, and may be used for privacy purposes or hiding the source.

## 16. The Upper Three Layers in TCP/IP

In the OSI Model, we have:

* Application
* Presentation
* Session

But in the TCP/IP Model, they are often all grouped under:

**Application Layer**

This means when we say Application Layer in TCP/IP, it logically includes things such as:

* Application protocols
* Data formatting
* Encryption
* Session management

## 17. Layer 4 — Transport Layer

After the data becomes ready from the upper layers, it reaches:

**Layer 4 - Transport Layer**

This layer is very important in networks.

Its main function is:

**Determining the method of transporting data between the two devices**

The basic question in this layer is:

Do we want reliable transport or fast transport?

## 18. The Main Protocols in the Transport Layer

The two most important protocols in the Transport Layer are:

* TCP
* UDP

And they determine the style of transport.

## 19. TCP

TCP = Transmission Control Protocol

TCP is used when we want to ensure that the data arrives correctly.

TCP characteristics:

* Reliable
* Connection-oriented
* Uses acknowledgments
* Retransmits lost data
* Uses three-way handshake

This means TCP is concerned with verification and acknowledgment.

## 20. How Does TCP Work in a Simplified Way?

If the server sends a file or part of a page, it waits for an acknowledgment from the receiving device.

Example:

* Server: I sent you this part, did it arrive?
* Client: Yes, it arrived.
* Server: Excellent, I will send the next part.

If the acknowledgment does not arrive, TCP retransmits the data.

That is why TCP is suitable for things that must arrive completely and correctly.

## 21. Examples of Using TCP

TCP is suitable for applications such as:

* Web browsing
* HTTPS
* HTTP
* SSH
* FTP
* Email
* File downloads

Because we do not want these things to be incomplete or corrupted.

For example, when downloading a file, you do not want any part of it to be missing.

## 22. Three-Way Handshake

Before TCP starts sending data, it creates a connection between the two endpoints.

This process is called:

**TCP Three-Way Handshake**

And it consists of three steps:

* SYN
* SYN-ACK
* ACK

## 23. Explanation of SYN / SYN-ACK / ACK

### 1. SYN

The first device starts the connection:

```text
Client → Server: SYN
```

Its meaning is:

I want to start a connection with you.

### 2. SYN-ACK

The server replies:

```text
Server → Client: SYN-ACK
```

Its meaning is:

Your request arrived, and I agree to start the connection.

### 3. ACK

The first device replies one final time:

```text
Client → Server: ACK
```

Its meaning is:

Confirmed, let us start data transfer.

After that, data exchange begins.

## 24. Why Is TCP Relatively Slower Than UDP?

TCP has additional steps, such as:

* Establishing a connection
* Confirming delivery
* Retransmitting lost data
* Ordering data
* Flow control

These things make it reliable, but they add extra time and effort.

That is why TCP is not always the fastest choice.

## 25. UDP

UDP = User Datagram Protocol

UDP is simpler and faster than TCP.

But it does not provide the same level of reliability.

UDP characteristics:

* Connectionless
* Faster
* No three-way handshake
* No delivery guarantee
* No retransmission by default

This means UDP sends the data without waiting for confirmation that the other side received it.

## 26. How Does UDP Work in a Simplified Way?

UDP works like this:

Send the data and that is it.

There is no:

* Did it arrive?
* Do you want retransmission?
* Are we formally connected?

That is why it is faster, but if some data is lost, it will not retransmit it in the same way TCP does.

## 27. Examples of Using UDP

UDP is suitable for applications that need speed and low response time.

Such as:

* Video streaming
* Live streaming
* Voice calls
* Video calls
* Online gaming
* DNS usually
* DHCP
* TFTP

In these cases, sometimes it is better that new data continues to arrive instead of retransmitting old data that is no longer useful.

## 28. Why Might Video Use UDP?

When you watch a video, the data arrives continuously.

If a small part is lost, there may be slight stuttering or a brief drop in quality.

But if we use TCP and retransmit the missing part, the video may be delayed or stop.

Example:

### UDP:

The video continues, and you may lose a small part.

### TCP:

It waits for the missing part or retransmits it, and this may cause freezing or delay.

That is why UDP is very useful in Real-time applications.

## 29. Why Might YouTube Use TCP and UDP Together?

When opening YouTube, it is not only the video that is being loaded.

There are many things being loaded:

* HTML page
* Buttons
* Menus
* Thumbnails
* JavaScript
* CSS
* User interface
* Video stream
* Ads
* Recommendations
* Comments

The page itself usually needs TCP/HTTPS because it must arrive correctly.

As for the video itself, or some parts of real-time transport, it may use UDP or technologies built to take advantage of speed and reduce delay.

So you may see a connection using:

* TCP
* UDP

depending on the type of data and the stage.

## 30. What Happens When Opening the YouTube Page?

When you open YouTube, the browser first needs to load the site page.

This includes:

* HTML
* CSS
* JavaScript
* Images
* Buttons
* Menus

These data usually move using:

**HTTPS over TCP**

because the page must arrive correctly.

Then when the video is played, different transport methods may be used to improve speed and continuity.

## 31. Wireshark and Understanding Traffic

A tool such as:

**Wireshark**

can be used to monitor real traffic on the device.

Through it, you can see things such as:

* Source IP
* Destination IP
* Protocol
* Source Port
* Destination Port
* TCP Handshake
* UDP Traffic

For example, when opening YouTube, you may see a connection to an IP belonging to a YouTube server, and notice the use of TCP or UDP depending on the connection type.

## 32. What Are Ports?

In the Transport Layer, there are very important numbers called:

**Ports**

A Port identifies the service or application inside the device.

Because one server may run more than one service.

For example, the same server may have:

* Web Server
* SSH Server
* FTP Server
* RDP Server
* Game Server

So how does the server know that the intended request is for the Web service and not SSH?

Through the Port Number.

## 33. Example of Ports

If you want to open an HTTPS website:

```text
https://youtube.com
```

you are usually connecting to port:

**443**

If you want SSH:

```text
ssh user@server
```

you are usually connecting to port:

**22**

If you want FTP:

```text
ftp server
```

the common port is:

**21**

## 34. Destination Port

When your device sends a request to YouTube, it contains:

```text
Destination Port = 443
```

Its meaning is:

I want the HTTPS service on this server.

That is, when the server sees Port 443, it passes the request to the Web Server / HTTPS service.

## 35. Source Port

In addition to the Destination Port, there is also:

**Source Port**

It is the temporary port that your device opens locally for this connection.

For example:

```text
Source Port = 57095
Destination Port = 443
```

Its meaning is:

My device is sending from temporary port 57095 to the HTTPS service on server Port 443.

## 36. Why Do We Need Source Port?

Your device is usually not connected to only one service.

At the same time, it may be:

* Watching YouTube
* Using Spotify
* Opening Google
* Opening GitHub
* Using Discord

Each connection needs a way to identify the replies.

Therefore, the browser or the system chooses a temporary Source Port for each connection.

When the server replies, it sends the reply back to the same Source Port so that your device knows which application or connection this reply belongs to.

## 37. Ephemeral Port

The temporary Source Port is called:

**Ephemeral Port**

Its meaning is:

A temporary port used by the device during the connection and then released later.

Example:

```text
Client: 192.168.1.10:57095
Server: 173.194.191.167:443
```

This identifies the connection precisely.

## 38. How Is the Connection Identified?

A connection can be identified using a set of information:

* Source IP
* Source Port
* Destination IP
* Destination Port
* Protocol

Example:

```text
192.168.1.10:57095 → 173.194.191.167:443 TCP
```

This represents a specific connection between your device and a YouTube server.

## 39. Port Range

Port numbers range from:

```text
0 to 65535
```

Ports from:

```text
0 to 1023
```

are often called:

**Well-known Ports**

They are assigned to well-known services.

## 40. Examples of Important Ports

```text
FTP       21/TCP
SSH       22/TCP
Telnet    23/TCP
SMTP      25/TCP
DNS       53/TCP and UDP
DHCP      67/UDP and 68/UDP
HTTP      80/TCP
POP3      110/TCP
NTP       123/UDP
HTTPS     443/TCP
SMB       445/TCP
RDP       3389/TCP usually
TFTP      69/UDP
SNMP      161/UDP
```

You do not need to memorize all ports at the beginning, but in CCNA there are core ports that you should know.

## 41. Why Does the Server Need Ports?

Because the IP Address alone gets you to the device, but it does not identify the required service inside the device.

Example:

```text
IP Address = the building address
Port       = the door number or office number inside the building
```

If you reach the server, you need to say:

I want HTTPS

and that is done through:

**Port 443**

or:

I want SSH

and that is done through:

**Port 22**

## 42. Transport Layer Header

When the data reaches the Transport Layer, a Header is added containing information such as:

* TCP or UDP
* Source Port
* Destination Port

Example:

```text
Protocol = TCP
Source Port = 57095
Destination Port = 443
```

After this Header is added, the data becomes:

**Segment**

## 43. What Happens After the Transport Layer?

After the Transport Layer, the Segment is sent to the Network Layer.

There, an IP Header is added:

* Source IP
* Destination IP

So the message becomes:

**Packet**

Then, in the Data Link Layer, MAC Addresses are added, and it becomes:

**Frame**

Then, in the Physical Layer, it is transformed into signals on the cable or wireless waves.

## 44. A Full Example of a YouTube Request

When the device opens YouTube, the logical form may be like this:

### Application Layer:

HTTPS request to open YouTube

### Presentation Layer:

Data formatting and perhaps encryption

### Session Layer:

Managing the communication session

### Transport Layer:

TCP + temporary Source Port + Destination Port 443

### Network Layer:

Source IP of your device + Destination IP of YouTube

### Data Link Layer:

Source MAC of your device + Destination MAC of the Next Hop

### Physical Layer:

Bits / Signals moving through the network

## 45. When the Request Reaches YouTube

When the request reaches the YouTube server, it is opened in reverse:

```text
Frame
↓
Packet
↓
Segment
↓
Application Data
```

In the Transport Layer, the server sees:

```text
Destination Port = 443
```

So it knows that the request goes to the HTTPS/Web Server service.

Then in the Application Layer, the request is processed and the page, video, or required data is sent back.

## 46. Application Layer Protocols and Their Link to TCP or UDP

Some protocols use TCP, some use UDP, and some use both.

Important examples:

* DNS → TCP and UDP
* DHCP → UDP
* FTP → TCP
* HTTP → TCP
* SMTP → TCP
* SNMP → UDP
* TFTP → UDP

## 47. DNS Uses TCP and UDP

DNS usually uses UDP because it is fast and lightweight.

But it can use TCP in certain cases, such as:

* Zone Transfers
* Large DNS responses

So DNS can be:

* TCP/53
* UDP/53

## 48. DHCP Uses UDP

DHCP is used to distribute network settings to devices, such as:

* IP Address
* Subnet Mask
* Default Gateway
* DNS Server

And it usually uses:

* UDP 67
* UDP 68

## 49. TFTP Uses UDP

TFTP = Trivial File Transfer Protocol

It is a very simple version of file transfer.

It uses:

**UDP Port 69**

## 50. TCP and UDP Comparison

### TCP:

* Reliable
* Requires a connection
* Uses Three-Way Handshake
* Retransmits lost data
* Suitable for web, SSH, FTP, Email

### UDP:

* Faster
* Does not require a prior connection
* Does not guarantee delivery
* Does not use Three-Way Handshake
* Suitable for video, voice, gaming, DNS, DHCP, TFTP

## 51. Why Do Real-time Applications Prefer UDP?

In real-time applications such as:

* Online Games
* Video Calls
* Live Streams
* Voice Calls

time is more important than retransmitting old data.

For example, in an online game, if an old movement is lost, there is no benefit in sending it later because the game has already moved beyond that moment.

That is why UDP is suitable for cases where delay is more harmful than losing a small part of the data.