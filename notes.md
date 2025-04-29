# TCP & UDP

---

## Basics of Layer 4 ##

- **Responsible for end-to-end communication** between hosts.
- Handles **segmentation**, **reassembly**, **error recovery**, and **flow control**.
- Supports **multiple simultaneous sessions** through **port numbers**.
- Uses protocols like:
  - **TCP** – reliable, connection-oriented.
  - **UDP** – unreliable, connectionless.

---

## Port Numbers ##

- Identify specific **applications/services** on a host.
- **Well-known ports (0–1023)**: reserved for common protocols.
  - e.g., HTTP (80), HTTPS (443), SSH (22), DNS (53), FTP (20/21)
- **Ephemeral ports (49152–65535)**: auto-assigned to clients.
- **Allows multiplexing** — many apps can share one IP address.

---

## Session Multiplexing ##

- Enables multiple active connections from a single device/IP.
- Combines:
  - Source IP
  - Destination IP
  - Source Port
  - Destination Port
- Each connection is uniquely identified by this **4-tuple**.

---

## TCP Header Basics ##

- Includes:
  - **Source Port / Destination Port**
  - **Sequence Number**
  - **Acknowledgement Number**
  - **Flags** (SYN, ACK, FIN, RST, etc.)
  - **Window Size** (flow control)
  - **Checksum**
- Larger and more complex than UDP.

---

## TCP 3-Way Handshake ##

Used to establish a reliable session:

1. **SYN** – Client → Server: “Let’s start a session.”
2. **SYN-ACK** – Server → Client: “Sure, I’m ready.”
3. **ACK** – Client → Server: “Great, let’s begin.”

After this, data transfer starts.

---

## TCP 4-Way Handshake (Termination) ##

Used to close a session cleanly:

1. **FIN** – Client → Server: “I’m done.”
2. **ACK** – Server → Client: “Got it.”
3. **FIN** – Server → Client: “I’m also done.”
4. **ACK** – Client → Server: “Confirmed.”

Ensures both sides shut down properly.

---

## TCP Sequencing & Acknowledgement ##

- **Sequencing** tracks data chunks (segments) to ensure proper reassembly.
- **Acknowledgement Numbers** confirm receipt of specific byte ranges.
- Allows for retransmission of **lost or out-of-order packets**.
- Ensures **reliability** and **data integrity**.

---

## Flow Control ##

- Prevents overwhelming a receiver.
- **TCP Window Size** tells the sender how much data it can transmit.
- Can dynamically **increase or decrease** based on network conditions.

---

## Basics of UDP ##

- **User Datagram Protocol**
- **Connectionless** and **unreliable** — no setup, no guaranteed delivery.
- Minimal overhead: faster and lighter than TCP.
- Common in:
  - Streaming (video, audio)
  - VoIP
  - DNS lookups
  - TFTP

---
