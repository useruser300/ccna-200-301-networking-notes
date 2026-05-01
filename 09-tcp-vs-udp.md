# TCP vs UDP

# 1) Introduction

**TCP** and **UDP** are two protocols that operate at:

**Transport Layer (Layer 4)**

The role of this layer is to transfer data between two endpoints, but the method of transport is very different between TCP and UDP.

The fundamental difference between them is:

* **TCP** focuses on **reliability and order**
* **UDP** focuses on **speed and simplicity**

Therefore, it cannot be said that one is always “better” than the other. Each one is suitable for a different scenario.

---

# 2) TCP

**TCP** stands for:

**Transmission Control Protocol**

It is a **Reliable** protocol.

This means that when the sender transmits data to the receiver, TCP tries to ensure:

* that the data arrived
* that it arrived in the correct order
* and that missing parts can be detected and retransmitted

---

# 3) Why Is TCP Considered Reliable?

Because TCP does not just send data only, but also tracks the session and verifies the state of the transmission.

It achieves this through a set of core ideas:

* **Error Detection / Correction**
* **Sequencing**
* **Acknowledgment**
* **Flow Control**
* **Session Establishment**
* **Session Termination**

---

# 4) Sequencing

When the data is large, TCP does not send it as one single piece, but divides it into:

**Segments**

Then it gives each Segment a number or an order.

The goal of this is:

* if the data arrives in a different order, it can be reordered
* and if a certain Segment is lost, it is possible to know exactly which part is missing

This means that instead of the receiver saying:

* “The data is incomplete”

it can say:

* “I did not receive Segment number 2”

And this makes TCP more precise in handling transmission.

---

# 5) Error Detection / Correction

If a Segment is lost on the way, TCP does not ignore that.

Instead, it relies on:

* Sequence Numbers
* ACKs

to know that a part did not arrive, then retransmits it.

That is why TCP is suitable for cases where data loss is unacceptable.

Such as:

* downloading files
* opening websites
* sending important data between systems

---

# 6) TCP Is Slower Than UDP

This is not a design problem, but a logical result.

TCP is relatively slower because it performs:

* 3-way handshake
* Sequence tracking
* ACK handling
* Retransmission
* Flow control
* Session close management

So the lower speed here is the price of higher reliability.

---

# 7) The Most Common Uses of TCP

TCP is used in services that require accuracy and data integrity.

Important examples:

* **HTTP** → Port 80
* **HTTPS** → Port 443
* **FTP** → Ports 20, 21

These protocols are not suitable for random data loss, so they rely on TCP.

---

# 8) TCP Session Establishment

Before TCP starts sending data, it does not send it directly.

First, it opens a Session through:

**TCP 3-Way Handshake**

This is one of the most important things that must be understood in TCP.

---

# 9) TCP 3-Way Handshake

The 3-Way Handshake consists of three messages:

1. **SYN**
2. **SYN + ACK**
3. **ACK**

---

# 10) The First Message: SYN

The sender starts the connection and sends:

**SYN**

In this message, it defines important things such as:

* **Source Port**
* **Destination Port**
* **Window Size**

Example in the case of HTTP:

* Source Port = `1025`
* Destination Port = `80`

The Source Port is usually a temporary port selected by the device from the high range.  
The Destination Port is based on the application.

Since we are talking about HTTP:

* Destination Port = `80`

---

# 11) The Second Message: SYN + ACK

The receiver responds with a message:

**SYN + ACK**

Here, it says to the sender logically:

* I received the request to open the session
* and I am also ready
* and here is my information as well

And it logically reverses the ports:

* Source Port = `80`
* Destination Port = `1025`

Because the server replies from the service port to the client port.

---

# 12) The Third Message: ACK

After that, the client sends:

**ACK**

Here, the session becomes open.

After this moment, the actual data exchange begins.

---

# 13) Why Is the 3-Way Handshake Important?

Because it achieves more than one thing:

* it confirms that both endpoints exist
* it confirms that both endpoints are ready to communicate
* it establishes the session
* it identifies the ports used by each side
* it allows agreement on values such as Window Size

This means TCP does not operate randomly, but opens the session in an organized way before starting transmission.

---

# 14) Window Size

This is a very important point in TCP.

**Window Size** means:

how many Segments the other side can receive before it needs to send an ACK

This means if the receiver says:

```text
Window Size = 2
```

then this means:

* send me Segment 1 and Segment 2
* then wait for my acknowledgment

If the Window Size becomes larger:

* a greater number of Segments can be sent before waiting for an ACK

So Window Size is part of:

**Flow Control**

---

# 15) Flow Control

The function of **Flow Control** is to regulate the sending speed according to the ability of the other side to receive.

This means the goal is not for the sender to transmit at maximum speed all the time, but to send at a speed that matches:

* receiving capacity
* network condition
* the ability of the other side

This prevents:

* flooding
* data loss due to over-receiving
* imbalance between sender and receiver

---

# 16) Example of Data Transmission in TCP

Suppose the laptop wants to send a Request to Wikipedia.

After the 3-Way Handshake is completed, TCP starts sending Segments.

If the Window Size = 2:

* it sends Segment 1
* it sends Segment 2
* then it waits for an ACK

If the receiver replies, for example:

**ACK 3**

this means:

* I received 1 and 2
* and I am now expecting Segment 3

And if it also says that the Window Size has become 5:

* the sender can now send 5 consecutive Segments before waiting for a new ACK

---

# 17) The Meaning of ACK 3

If the receiver says:

**ACK 3**

the meaning is not only “I acknowledge”

but the more accurate meaning is:

* I received everything up to before 3
* and I am now waiting for Segment number 3 from you

This is a very important point in understanding TCP logic.

---

# 18) TCP Session Termination

After data exchange is complete, TCP does not leave the session open forever.

Instead, it closes it in an organized way through:

**TCP 4-Way Handshake**

---

# 19) TCP 4-Way Handshake

Closing the session happens through four messages:

1. **FIN**
2. **ACK**
3. **FIN**
4. **ACK**

---

# 20) What Does This Mean in Practice?

The first side says:

* **FIN**
* meaning: I am finished sending

The second side replies:

* **ACK**
* meaning: I received the termination request

Then if it is also finished:

* it sends **FIN**

Then the first side replies:

* **ACK**

In this way, the session is closed completely.

---

# 21) TCP Summary

So TCP is characterized by being:

* Reliable
* Ordered
* Uses Sequencing
* Uses ACKs
* Uses Flow Control
* Relatively slower
* Suitable for data that must arrive accurately

---

# 22) UDP

**UDP** stands for:

**User Datagram Protocol**

It is also a protocol that operates at:

**Layer 4**

But its idea is very different from TCP.

UDP was designed to be:

* **Fast**
* **Simple**
* **Low overhead**

---

# 23) Why Is UDP Fast?

Because UDP does not do everything that TCP does.

UDP does not rely on:

* 3-Way Handshake
* complex Session establishment
* Sequencing in the same TCP logic
* Retransmission
* ACK-based reliability
* Flow control in the same way

It simply sends the data and does not wait much to confirm that it arrived completely.

That is why it is faster.

---

# 24) UDP Is Not Ordered

In UDP, there is no same strict ordering logic that exists in TCP.

Therefore:

* the data may arrive in a different order
* some Packets may be lost
* and this is not necessarily corrected by the protocol itself

---

# 25) UDP Is Not Reliable

This does not mean that it is “bad”, but it means that it does not guarantee delivery like TCP.

If a Packet is lost:

* UDP does not say: retransmit it
* and it does not establish the session with the same level of tracking

So if data is lost, the application itself usually handles the result if it needs to do so.

---

# 26) Why Do We Accept That in UDP?

Because there are applications where:

* delay is worse than minor loss

Example:  
In a live voice or video call, if a small Packet is lost, it is usually better for the stream to continue rather than stop and wait for retransmission.

That is why UDP is very suitable for cases that require:

* speed
* low latency
* continuous flow

even if there is slight loss in some data.

---

# 27) The Most Common Uses of UDP

UDP is widely used with services where speed is more important than absolute reliability.

Common examples:

* **Voice calls**
* **Video calls**
* **Live streaming**
* **Online gaming**

In these cases, extra delay harms the experience more than losing a small piece of data.

---

# 28) Practical Example of UDP

Suppose there is a Video Call between two devices.

The first device sends:

* audio
* video
* continuous rapid updates

If some Packets are lost:

* UDP will not wait to retransmit them
* instead, it continues sending

The result that the user may notice could be:

* slight audio cutting
* slight video cutting
* temporary reduction in quality

But the call remains continuous and fast.

And this is usually better than having the call stop while waiting for every lost Packet to be retransmitted.

---

# 29) Why Do Games and Voice/Video Use UDP So Much?

Because these applications need:

* Low latency
* Fast delivery
* Real-time response

In an online game, for example:  
if a small old piece of information is lost, what usually matters is the newest current state.

And in a video call:  
it is better to hear the current audio with slight interruption, rather than have the audio delayed by several seconds because of retransmission.

---

# 30) Direct Comparison Between TCP and UDP

| Comparison      | TCP               | UDP                             |
| --------------- | ----------------- | ------------------------------- |
| Layer           | Layer 4           | Layer 4                         |
| Reliability     | High              | Low                             |
| Order           | Preserves order   | May not preserve order          |
| Retransmission  | Yes               | No                              |
| ACKs            | Yes               | Not in the same TCP logic       |
| Handshake       | Exists            | Does not exist in the same form |
| Speed           | Relatively slower | Faster                          |
| Use cases       | Web, HTTPS, FTP   | Voice, Video, Gaming, Streaming |

---

# 31) The Very Fundamental Difference

If you ask yourself:

**Do I want the data to arrive correctly and completely even if that is slower?**  
then the choice is usually:

* **TCP**

**Do I want speed and continuity even if some data is lost?**  
then the choice is usually:

* **UDP**

---

# 32) Clear Engineering Example

## Case 1: Downloading a File

If you are downloading a file:

* you do not accept that part of it is missing
* you do not accept that its parts arrive in the wrong order

Here we need:

* **TCP**

## Case 2: Video Call

If you are in a Video Call:

* you want the audio and video with the least delay possible
* some slight loss is acceptable

Here we usually need:

* **UDP**

---

# 33) The Relationship with Ports

Both protocols use Ports, but the common examples mentioned here with TCP are:

* HTTP → TCP/80
* HTTPS → TCP/443
* FTP → TCP/20,21

As for UDP, the focus here was more on the type of use than memorizing port numbers.

---

# 34) Very Important Point

It does not mean that because UDP does not retransmit, it is not useful.

On the contrary, it is excellent when:

* speed matters more
* the stream is real-time
* small loss is acceptable

And it also does not mean that TCP is always better.

Rather, TCP is excellent when:

* accuracy matters more
* order is important
* loss is unacceptable

---

# 35) Summary

The final idea is as follows:

* **TCP** and **UDP** operate at Layer 4

* **TCP** is a Reliable protocol

* TCP guarantees order and uses Sequencing, ACK, and Flow Control

* TCP requires a 3-Way Handshake to open the session

* TCP uses a 4-Way Handshake to close the session

* TCP is relatively slower because of its high reliability

* Among its most common uses are:

  * HTTP
  * HTTPS
  * FTP

* **UDP** is a faster and simpler protocol

* UDP does not rely on the same level of acknowledgment and ordering found in TCP

* UDP does not retransmit lost data

* It is very suitable for real-time applications such as:

  * Voice
  * Video
  * Live streaming
  * Online gaming

* If the priority is **data integrity** → use **TCP**

* If the priority is **speed and low latency** → use **UDP**