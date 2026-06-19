# 🌐 Topic: The OSI Model

**Date:** 18-06-2026
**Status:** 🟢 Completed

## What I Learned

The OSI model is a conceptual framework and a standardization of how computers communicate. It contains 7 layers, each with a specific function. The independence of each layer allows for interoperability, so engineers can focus on their own area of expertise during technical issues. This also makes debugging easier, since identifying the faulty layer means the other layers don't have to be touched.

The TCP/IP stack, however, is not conceptual, it's the actual framework utilized in networking. It contains 4 layers which have similar function to the seven layers in the OSI model. Two of these four layers are almost like an abbreviation of the OSI model:

| TCP/IP Layer | Equivalent OSI Layer(s) |
|---|---|
| Application | Application, Presentation, Session |
| Transport | Transport |
| Internet | Network |
| Link | Data-link, Physical |

> [!NOTE]
> Despite TCP/IP being what's actually implemented, engineers would usually still refer to the OSI model when having conversations, for some reason.

## The Layers in Detail

- **Application Layer**: provides network services for application systems. It differs from other layers in that it does not provide services to other layers, it also establishes availability of the end-user host system.
- **Presentation Layer**: translates data in a way that ensures it's readable by the application layer of both end-users.
- **Session Layer**: establishes, manages and terminates sessions between two communicating hosts.
- **Transport Layer**: breaks data into segments for uninterrupted transmission, accounts for retransmission when an error is encountered (depending on the protocol used: UDP/TCP), and uses a port number to identify which application the data belongs to (e.g. port 80).
- **Network Layer**: provides connection between two hosts on different networks, sending data in packets, each containing an IP address.
- **Data-link Layer**: defines the format of data transmission and how data access is controlled. It matches MAC addresses to validate transmission of data between devices on the physical layer, switches also function at this layer.
- **Physical Layer**: the physical hardware that transfers data in bits through electrical signals (copper), light pulses (fiber), or radio waves (wireless).

## PDU (Protocol Data Unit)

| Layer | PDU |
|---|---|
| Application | Data |
| Transport | Segments |
| Network | Packets |
| Data-link | Frames |
| Physical | Bits |

The process of sending data from the sender's system down to the physical layer is called **encapsulation**. The process of sending data from the physical layer up to the application layer of the receiver is called **de-encapsulation**.

## Struggles / Questions

We're supposedly going to go deeper into the last four layers. For now I don't really have confusions, as this is just the basics of the foundation.
