# **Table of Contents**
  - [TCP, UDP](#TCP-UDP)

## **TCP, UDP** 
  *reference question [vietnakid/learning-material](#https://github.com/vietnakid/learning-material)*
  - [How TCP open a connection? What does it need to open a connection?](#How-TCP-open-a-connection-What-does-it-need-to-open-a-connection)
    - [What are the sequence number and the acknowledgement number? Why initial sequence number is generated randomly?](#What-are-the-sequence-number-and-the-acknowledgment-number-Why-initial-sequence-number-is-generated-randomly)
    - [Why there are three-way handshakes but not two-way?](#Why-there-are-three-way-handshakes-but-not-two-way)
    - [What is syn, ack mean?](#What-is-syn-ack-mean)
    - [What is the 3rd handshakes fail? How the server can detect it and what does it do in this case?](#What-is-the-3rd-handshakes-fail-How-the-server-can-detect-it-and-what-does-it-do-in-this-case)

  - [How does TCP handle data sequencing?](#How-does-TCP-handle-data-sequencing)
    - [What happens if some bits are wrong due to connection errors? How to detect them and fix them?](#What-happens-if-some-bits-are-wrong-due-to-connection-errors-How-to-detect-them-and-fix-them)
    - [How the timeout is handled? what if the timeout is expired?]()
    - [What will happen if some "packet" is missing on the way?]()
    - [How to detect the appropriate number of packets to send (speed of sending packet)?]()
  - [How TCP close a connection?](#How-TCP-close-a-connection)
  - [Compare TCP and UDP? Which case we use each protocol?](#[Compare-TCP-and-UDP-Which-case-we-use-each-protocol])

## How TCP open a connection? What does it need to open a connection?
To open a connection, the server must first bind to and list at a port: this is called a passive open. Once the passive open is established,
the client may establish a connection by initiating an active open using three-way handshakes.
  - In the first step, the client establishes a connection with a server, so it sends a seqment with flag SYN and sets the segment's sequence number to a random **Initial Sequence Number** (ISN) is A.
  - The the server replies with flag SYN-ACK. The knowledgement number is set to one more than the received sequence number is A + 1 and set seqment's sequence number to a random **Initial Sequence Number** (ISN) is B.
  - Finally, the client send an ACK back to the server with the sequence number is A + 1 and the acknowledgement number is B + 1.
![](image/TCP_Init_Phase.png?raw=true)
Note: When a host initiates a TCP session, its initial sequence number is effectively random; it may be any value between 0 and 4,294,967,295, inclusive. However, protocol analyzers like **Wireshark** will typically display relative sequence and acknowledgement numbers in place of the actual values. These numbers are relative to the initial sequence number of that stream. This is much easier to keep track of relatively small, predictable numbers rather than the actual numbers sent on the wire.

#### *What are the sequence number and the acknowledgment number? Why initial sequence number is generated randomly?*
  - The sequence number is the byte number of first byte of data in the TCP packet sent and the acknowledgment number is the sequence number of the next byte that the receiver expected to receive.
  - ISN is generated randomly because to avoid accidental conllision between seperate sessions. It can cause security issuses like connection spoofing, connection resetting and data injection. (ref: [tcp-hijacking](https://www.techrepublic.com/article/tcp-hijacking/))
#### *Why there are three-way handshakes but not two-way?*
  - Because a two-way handshakes would only allow one side to establish an ISN and the other side to acknowledgment it. Which means only on side can send data. However, TCP is bidirection communication protocol, which means either end ought to be able to send data reliably. Therefore, both sides need to establish an ISN, and both sides need to acknowledgment the other's ISN.
#### *What is syn, ack mean?*
  - syn is mean synchronize, ack is mean acknowledgment. Syn used to initiate and establish a connection, it also helps you to synchronize sequence numbers between devices, while Ack helps to confirm to the other side that it has received previous segment.
#### *What is the 3rd handshakes fail? How the server can detect it and what does it do in this case?*
  - If the 3rd handshakes fail, the clients returns the ACK message go to the server, but the server cannot receive the ACK message. Then the server will start the timeout retransmit mechanism and send SYN+ACK again after exceeding the specified time. The number of retransmits is specified according to /proc/sys/net/ipv4/tcp_synack_retries(linux). The default is 5. If the ACK response is n1ot received after the specified number of retransmissions has arrived, the server automatically closes the connection after a period of time. But client thinks the connection has been established, and if client writes data to server, server will respond with RST package.
## How does TCP handle data sequencing?
  - TCP breaks user data into segments, numbers each segment, places them in the correct sequence, and sends each one in order, waiting for an acknowledgement before sending the next segment.
#### *What happens if some bits are wrong due to connection errors? How to detect them and fix them?*

#### 

## How TCP close a connection?
  - It is also possible to terminate the connection by a 3-way handshake, when host A sends a FIN and host B replies with a FIN & ACK (merely combines 2 steps into one) and host A replies with an ACK.

  - Some operating systems, such as Linux and H-UX, implement a half-duplex close sequence in the TCP stack. If the host actively closes a connection, while still having unread incoming data available, the host sends the signal RST (losing any received data) instead of FIN. This assures a TCP application that the remote process has read all the transmitted data by waiting for the signal FIN, before it actively closes the connection. The remote process cannot distinguish between an RST signal for connection aborting and data loss. Both cause the remote stack to lose all data received.

## Compare TCP and UDP? Which case we use each protocol?
  - TCP is connection-oriented protocol, which means that the communicating devices should establish a connection before transmitting data and close a connection after transmitting data. UDP is a simpler, connectionless protocol.
  - TCP is reliable as it guarantees delivery of data to the destination router, while the delivery of data cannot be guaranteed in UDP. If there is a lost packet, TCP will retransmission the lost packet but there is no retrasmission of lost packet in UDP.
  - TCP provides extensive error checking mechanism and packets arrive in-order at the receiver while UDP has only the basic error checking mechanism using checksums and there is no sequencing of data.
  - UDP is faster, simple and more efficient than TCP. 
  - UDP supports Broadcasting but TCP don't support.
  - UDP is used for application like DNS, SNMP, game, VoIP, DHCP,..., while TCP is used for application that need guarantee data like email, message, http, ftp, www,...