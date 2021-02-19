# **Table of Contents**
  - [TCP, UDP](#TCP-UDP)

## **TCP, UDP**
  - [How TCP open a connection? What does it need to open a connection?](#How-TCP-open-a-connection-What-does-it-need-to-open-a-connection)
    - [What are the sequence number and the acknowledgement number? Why they have a send two "random" sequence number?](#What-are-the-sequence-number-and-the-acknowledgment-number-Why-they-have-a-send-two-random-sequence-number)
    - [Why there are three-way handshakes but not two-way?](#Why-there-are-three-way-handshakes-but-not-two-way)
    - [What is syn, ack mean?](#What-is-syn-ack-mean)
    - [What is the 3rd handshakes fail? How the server can detect it and what does it do in this case?](#What-is-the-3rd-handshakes-fail-How-the-server-can-detect-it-and-what-does-it-do-in-this-case)

  - [How TCP handles the connection?](#How-TCP-handles-the-connection)

## How TCP open a connection? What does it need to open a connection?
To open a connection, the server must first bind to and list at a port: this is called a passive open. Once the passive open is established,
the client may establish a connection by initiating an active open using three-way handshakes.
  - In the first step, the client establishes a connection with a server, so it sends a seqment with flag SYN and sets the segment's sequence number to a random **Initial Sequence Number** (ISN) is A.
  - The the server replies with flag SYN-ACK. The knowledgement number is set to one more than the received sequence number is A + 1 and set seqment's sequence number to a random **Initial Sequence Number** (ISN) is B.
  - Finally, the client send an ACK back to the server with the sequence number is A + 1 and the acknowledgement number is B + 1.
![](image/TCP_Init_Phase.png?raw=true)
Note: When a host initiates a TCP session, its initial sequence number is effectively random; it may be any value between 0 and 4,294,967,295, inclusive. However, protocol analyzers like **Wireshark** will typically display relative sequence and acknowledgement numbers in place of the actual values. These numbers are relative to the initial sequence number of that stream. This is much easier to keep track of relatively small, predictable numbers rather than the actual numbers sent on the wire.

#### *What are the sequence number and the acknowledgment number? Why they have a send two "random" sequence number?*
  - The sequence number is the byte number of first byte of data in the TCP packet sent and the acknowledgment number is the sequence number of the next byte that the receiver expected to receive.
  - 
#### *Why there are three-way handshakes but not two-way?*
  - Because a two-way handshakes would only allow one side to establish an ISN and the other side to acknowledgment it. Which means only on side can send data. However, TCP is bidirection communication protocol, which means either end ought to be able to send data reliably. Therefore, both sides need to establish an ISN, and both sides need to acknowledgment the other's ISN.
#### *What is syn, ack mean?*
  - syn is mean synchronize, ack is mean acknowledgment. Syn used to initiate and establish a connection, it also helps you to synchronize sequence numbers between devices, while Ack helps to confirm to the other side that it has received previous segment.
#### *What is the 3rd handshakes fail? How the server can detect it and what does it do in this case?*
  - If the 3rd handshakes fail, the clients returns the ACK message go to the server, but the server cannot receive the ACK message. Then the server will start the timeout retransmit mechanism and send SYN+ACK again after exceeding the specified time(). The number of retransmits is specified according to / proc/sys/net/ipv4/tcp_synack_retries. The default is 5. If the ACK response is not received after the specified number of retransmissions has arrived, the server automatically closes the connection after a period of time. But client thinks the connection has been established, and if client writes data to server, server will respond with RST package.
## How TCP handles the connection?