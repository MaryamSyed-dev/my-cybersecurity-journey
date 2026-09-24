# OSI Model

## Layer 7 — Application Layer
The Application Layer is the top layer of the OSI model, where applications 
interact with network services. It uses protocols such as HTTP, HTTPS, FTP, 
SMTP, and DNS for different types of communication.

Example: When we enter www.facebook.com in a browser, the browser uses HTTPS 
to communicate securely with Facebook's server, which commonly listens on 
port 443. The application creates the request, while the Transport Layer adds 
the source and destination ports. The client normally uses a temporary source 
port, while the server receives the request on destination port 443. The 
server processes the request and sends a response back to the client's 
corresponding port, allowing the page to load. If the server or service is 
unavailable, or the response doesn't arrive within the timeout period, the 
browser may show a connection or timeout error.

### Protocols & Port Numbers
| Protocol | Port Number |
|----------|-------------|
| HTTP     | 80          |
| HTTPS    | 443         |
| FTP      | 21          |
| SSH      | 22          |
| DNS      | 53          |
| SMTP     | 25          |

*Note: These are common/well-known ports I've learned and can identify with 
their corresponding protocols.*

## Layer 6 — Presentation Layer
The Presentation Layer is responsible for preparing data before it's sent to 
the lower layers — formatting, encrypting, and compressing it when necessary.

**As Sender:** Data comes from the Application Layer → Presentation Layer 
translates/formats → encrypts → compresses → passes to lower layers.

**As Receiver:** Data comes from lower layers → Presentation Layer 
decompresses → decrypts → translates/formats back → passes to Application 
Layer, where the app/browser displays the original message.

**Easy way to remember:**
- Sender → Translation → Encryption → Compression
- Receiver → Decompression → Decryption → Translation

## Layer 5 — Session Layer
The Session Layer is responsible for establishing, managing, synchronizing, 
and terminating communication sessions between applications.

**Practical example:** Suppose we have Facebook, Gmail, and YouTube open in 
different browser tabs. Each application establishes its own communication 
session with its respective server. The Session Layer conceptually keeps 
these sessions separate and organized so data belonging to one session is 
associated with the correct application — a request from Facebook goes to 
the Facebook server, while Gmail and YouTube requests go to their own 
servers. When responses come back, the system uses connection information to 
deliver each response to the right application, preventing data from mixing 
(e.g., Gmail data should never appear in the Facebook tab).

The Session Layer can also provide synchronization — if a session is 
interrupted, synchronization points help it resume from an appropriate 
point. When a session is no longer needed, it's terminated.

**Important note:** IP addresses and source/destination ports are primarily 
handled by the Network and Transport Layers respectively — not the Session 
Layer. A timeout can also involve transport/application-level mechanisms 
rather than being solely a Session Layer function.

**In simple words:** The Session Layer manages the communication session and 
keeps different sessions separate so data belonging to one session doesn't 
get mixed with another.

## Layer 4 — Transport Layer

### Port Numbers
There are a total of 65,536 port numbers, ranging from 0 to 65,535.
Port numbers are commonly divided into two categories:

**1. Well-Known Ports (0–1023)**
Reserved for commonly used network services and protocols. For example:
- HTTP → Port 80
- HTTPS → Port 443
- FTP → Port 21
- SMTP → Port 25
- DNS → Port 53

**2. Dynamic/Private Ports (1024–65535)**
Generally used dynamically for temporary communication — e.g., when a 
browser opens a connection to a server, the client side uses a dynamically 
assigned port from this range.

**In simple words:** Well-known ports are associated with commonly used 
services, while ports from 1024 to 65535 can be dynamically used for 
temporary communication.

### What I Learned
The Transport Layer is responsible for end-to-end communication between 
applications. It uses port numbers to identify the application or service 
involved in communication.

**Segments & headers:** Suppose the Transport Layer receives 2000 bytes of 
data. In TCP, this data is divided into smaller units called segments, and a 
transport-layer header is added to each segment. This header contains 
information required for transport communication (TCP or UDP).

**MTU and MSS:** A network link may have an MTU (Maximum Transmission Unit) 
of 1500 bytes — the max IP packet size normally transmittable over that 
link. For TCP over IPv4, if the IP header is 20 bytes and TCP header is 20 
bytes:

`1500 − 20 (IP header) − 20 (TCP header) = 1460 bytes MSS`

So an MSS of 1460 bytes means a TCP segment can carry up to 1460 bytes of 
application data. Total packet size becomes:

`1460 (TCP data) + 20 (TCP header) + 20 (IP header) = 1500 bytes` — fitting 
within the 1500-byte MTU.

**TCP vs UDP:**
- **UDP** is faster with lower overhead — no guarantee data arrives, or 
  arrives in order. Used for real-time communication like voice/video calls, 
  where some lost data just means broken/missing parts rather than a failed 
  call.
- **TCP** provides reliable, ordered communication using acknowledgements, 
  sequence numbers, and retransmission — missing data gets resent and 
  delivered in correct order. Used when complete, correct data matters (e.g., 
  downloads).

**Sequence numbers:** TCP divides data into segments and uses sequence 
numbers to track them (Segment 1 → 2 → 3 → 4). Even if segments arrive out 
of order, TCP uses sequence numbers to reorder them and can request/
retransmit missing data.

**In simple words, the Transport Layer:**
- Uses port numbers to identify applications and services
- Divides application data into smaller units for transmission
- Adds a transport header
- Uses TCP or UDP
- TCP provides reliable and ordered communication
- UDP provides faster, connectionless communication without TCP's guarantees
- TCP uses sequence numbers to track data order
- Enables proper end-to-end communication between applications

### Three-Way Handshake and Sequence Numbers
Before sending actual data, the computer and server first establish a 
connection through a three-way handshake. During this process, both sides 
keep track of the other side's initial sequence number.

For example, the computer creates its own initial sequence number (e.g., 
10) and tells the server. The server records it. Similarly, the server 
creates its own initial sequence number (e.g., 20) and tells the computer, 
which records it. Both sides now maintain information about each other's 
sequence numbers as part of the established connection.

**Example exchange:**
Computer → Server: SYN (Initial Sequence Number = 10)
Server → Computer: SYN + ACK (Server's Sequence = 20, Acknowledging computer's sequence)
Computer → Server: ACK
After this, the TCP connection is established and data transmission begins.

**Purpose:** Keeps communication organized and helps both sides identify 
whether received data belongs to the established connection.

**In simple words:** Both the computer and server keep track of each 
other's sequence information so they can identify and manage the data 
belonging to their established TCP connection.

### Windowing in TCP
Windowing is a mechanism used in TCP to make data transmission faster and 
more efficient.

**The problem:** Sending one segment and waiting for its acknowledgement 
before sending the next works fine for a few segments, but becomes very 
slow with a large number (e.g., 100,000 segments).

**The solution:** TCP uses a window — the sender can send a certain number 
of segments without waiting for an acknowledgement after every single one.

**Example:** If the window size is 5, the sender sends Segment 1 → 2 → 3 → 
4 → 5 without individual acks in between. After the receiver successfully 
gets them, it sends an ACK indicating the next expected data — e.g., an ACK 
for 6 means segments up to 5 were received and segment 6 is now expected. 
The window then moves forward, allowing the next segments to be sent.

**If a segment is lost:** Suppose segments 1–5 are sent but Segment 3 is 
lost. The receiver indicates it's still expecting segment 3, the sender 
retransmits it, and once received, the window moves forward again.

**In simple words:** Instead of:
Send 1 → ACK → Send 2 → ACK → Send 3 → ACK

TCP uses a window:

Send 1, 2, 3, 4, 5 → ACK → Send the next segments

This reduces unnecessary waiting and improves transmission efficiency.
### Flow Control in TCP
Flow control is a mechanism used to control the amount of data sent by the 
sender according to the receiving side's capacity.

**Example:** Suppose a computer sends a large amount of data to a server, 
but the server has only 10 MB of available buffer space. If the computer 
sends faster than the server can process, the server's buffer may become 
full (buffer overflow).

**How it works:** In TCP, this is mainly done through the receive window 
(rwnd). The receiver tells the sender how much additional data it can 
currently accept.
- If the receiver's buffer has very little available space, it advertises 
  a smaller window, so the sender slows down or temporarily stops sending.
- When the receiver processes some data and more buffer space becomes 
  available, it advertises a larger window, and the sender can continue 
  sending more data.

**In simple words:** Flow control prevents a fast sender from overwhelming 
a slow receiver. The receiver essentially tells the sender: *"I have this 
much space available, so you can send this much data."* When more buffer 
space frees up, the sender is allowed to send more.

## Layer 3 — Network Layer
The Network Layer receives a **segment** from the Transport Layer. It adds a 
**logical IP address** — the source IP and destination IP. After this 
header is added, the segment becomes a **packet**.

`Transport Layer → Segment → Network Layer adds IP info → Packet`

The packet is then passed to the Data Link Layer.

## Layer 2 — Data Link Layer
The Data Link Layer takes the packet and adds its own header and trailer. 
It uses **MAC addresses** (physical/link-layer addresses) — source MAC and 
destination MAC — for delivery on the local network.

It also uses **FCS (Frame Check Sequence)** for error detection, helping 
the receiver determine if the frame was corrupted during transmission.

After the header and trailer are added, the packet becomes a **frame**.

`Network Layer → Packet → Data Link header/trailer → Frame`

## Layer 1 — Physical Layer
Responsible for transmitting the frame as **bits/signals** over the 
physical medium (cable, fiber, or wireless radio signal). The Physical 
Layer handles the actual transmission of bits/signals through the medium, 
and the data travels toward the next network device or destination.

---

## Complete Example: Sending a File via FTP

**Sender side (going down the layers):**
1. **Application Layer** — FTP requests/transfers the file
2. **Transport Layer** — TCP is used (FTP needs reliable delivery); adds 
   TCP header with port numbers and sequence info; data organized into 
   segments
3. **Network Layer** — adds source/destination IP; segment becomes a 
   **packet**
4. **Data Link Layer** — adds source/destination MAC for the current local 
   hop, plus FCS; packet becomes a **frame**
5. **Physical Layer** — converts frame into bits/signals, transmits through 
   the medium

**Receiver side (going up the layers, reverse direction):**
1. **Physical Layer** — receives signals/bits, passes data upward
2. **Data Link Layer** — checks MAC address info for the link, uses FCS to 
   detect corruption; if valid, removes header/trailer, passes packet up
3. **Network Layer** — examines destination IP; if this is the destination, 
   removes Network header, passes data up
4. **Transport Layer** — processes TCP/UDP header and ports; for FTP, TCP 
   ensures reliable, ordered delivery
5. **Session Layer** — manages the communication session, keeps it organized
6. **Presentation Layer** — handles translation/formatting, 
   encryption/decryption, compression/decompression as needed
7. **Application Layer** — data reaches the app; FTP delivers the requested 
   file to the user

### Complete Data Flow
**Sender:** Data → Segment → Packet → Frame → Bits
**Receiver:** Bits → Frame → Packet → Segment → Data → (Session → 
Presentation → Application)

**In simple words:** Data moves *down* the OSI layers at the sender and 
*up* the OSI layers at the receiver, with each layer performing its 
specific function (addressing, error-checking, session management, 
formatting) along the way.

## Notes to self
- OSI Model fully covered — Application through Physical ✅