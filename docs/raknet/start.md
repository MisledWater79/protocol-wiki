---
prev:
    text: 'Learning MCBE Protocol'
next:
    text: 'Learning Data Types'
    link: '/raknet/data-types'
---

# RakNet Protocol

Latest documentation on the RakNet protocol mainly for Minecraft Bedrock Edition(s). Explains packets, their data types, and their formatation.

## What is RakNet?

RakNet is a UDP transfer layer. It is mainly used in Minecraft Bedrock, but is used in and can be used in other games. This document will cover RakNet as a whole, but the main focus is MCBE implementation.

## How does RakNet work?

Again, RakNet protocol uses UDP, this means that the [Packets]() that are sent, might not always make it. Things like [Pings]() and [Pongs](), this doesn't matter! But for more important information, we want to make sure the clients(players) get that data. To combat this, RakNet uses [Frame Set]() packets. These split data up if its too big and also keeps track of what data didn't make it to the client and will resend it. This uses [ACK]() & [NACK]() packets which the client sends to either say it got this part of the data or is missing this part of the data.

## Handshake sequence

This is what happens for every client wanting to connect.

---

* Clients Ping the server, and the Server sends back Pongs
* A client would then send a [Open Connection Request 1]()
* Server responds by sending a [Open Connection Reply 1]()
* Client sends a [Open Connection Request 2]()
* Server replys with a [Open Connection Reply 2]()

> [!NOTE]
> From here, the connection is made and now we start sending packets in [Frame Sets]()

* Clients send Connected Pings, and the Server back send Connected Pongs (If stopped we lost connection)
* Client sends a [Connection Request]()
* Server responds with a [Connection Request Accepted]()
* Lastly, Client sends a [New Incoming Connection]()

---

Now, all data recieved from frame sets are a [Game Packet](). The data recieve from the game packet is now delt with by the [Bedrock Protocol]() (We will go over it after RakNet).

This is the barebones of RakNet, so do not worry if you do not understand. Our next part is going to go over the [Data Types]() used by RakNet.

---

#### Resources

[[Jenkin Software RakNet Docs](http://www.jenkinssoftware.com/raknet/manual/systemoverview.html)]: Information on how RakNet works & communicates

[[wiki.vg](https://wiki.vg/Raknet_Protocol)]: Information on handshake sequence