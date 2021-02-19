# **Table of Contents**
  - [TCP, UDP](#TCP,-UDP)

## **TCP, UDP**
  - [How TCP open a connection? What does it need to open a connection?](#How-TCP-open-a-connection?-What-does-it-need-to-open-a-connection?)
    - [What are the sequence number and the acknowledgement number?](#What-are-the-sequence-number-and-the-acknowledgment-number?)
    - [Why there are three-way handshakes but not two-way?](#Why-there-are-three-way-handshakes-but-not-two-way?)
    - [What is syn, ack mean?](#What-is-syn,-ack-mean?)
    - [Why they have a send two "random" sequence number? The purpose of this sequence number?](#Why-they-have-a-send-two-"random"-sequence-number?-The-purpose-of-this-sequence-number?)
    - [What is the 3rd handshakes fail? How the server can detect it and what does it do in this case?](#What-is-the-3rd-handshakes-fail?-How-the-server-can-detect-it-and-what-does-it-do-in-this-case?)
  - [How TCP handles the connection?](#How-TCP-handles-the-connection?)

## How TCP open a connection? What does it need to open a connection?
To open a connection, the server must first bind to and list at a port: this is called a passive open. Once the passive open is established,
the client may establish a connection by initiating an active open using three-way handshakes.
  - In the first step, the client establishes a connection with a server, so it sends a seqment with flag SYN and sets the segment's sequence number to a random **Initial Sequence Number** (ISN) is A.
  - The the server replies with flag SYN-ACK. The knowledgement number is set to one more than the received sequence number is A + 1 and set seqment's sequence number to a random **Initial Sequence Number** (ISN) is B.
  - Finally, the client send an ACK back to the server with the sequence number is A + 1 and the acknowledgement number is B + 1.

![](image/TCP_Init_Phase.png?raw=true)

#### *What are the sequence number and the acknowledgment number?*
  - The sequence number is the byte number of first byte of data in the TCP packet sent and the acknowledgment number is the sequence number of the next byte that the receiver expected to receive.
#### *Why there are three-way handshakes but not two-way?*
  - Because a two-way handshakes would only allow one party to establish an ISN and the other party to acknowledgment it. Which means only on party can send data. However, TCP is bidirection communication protocol, which means either end ought to be able to send data reliably. Therefore, both parties need to establish an ISN, and both parties need to acknowledgment the other's ISN.
#### *What is syn, ack mean?*
  - 
#### *Why they have a send two "random" sequence number? The purpose of this sequence number?*
  - 
#### *What is the 3rd handshakes fail? How the server can detect it and what does it do in this case?*
  - 
## How TCP handles the connection?