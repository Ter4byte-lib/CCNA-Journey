# Topic: The OSI model
### Date: 18-06-2026

**Status:** 🟢 

**What I learned:**
- The OSI model is a conceptual framework and a standardization of how computers communicate. it contains 7 layers, each with a specific function. The independence of each layer allows for interoperability so engineers could focus on their area of their expertise during technical issues; this also makes debugging easy as identifying the faulty layer would mean other layers dont have to be tampered with.
- The TCP/IP Stack however is not conceptual; its the actual framework utilized in networking. It contains 4 layers of which have similar function with the seven layers present in the OSI model. 2 layers of these 4 are almost like an abbreviation of the OSI model:
    - The Application layer in the TCP/IP stack covers - the application layer, the presentation and the session layer of the OSI model.
    - The Link layer in the TCP/IP stack covers - the data link layer and the physical layer. 
- despite this engineers would usually still refer to the OSI model when having conversations for some reason 
- The Layers in detail include:
    - Application Layer: this layer provides network services for the application systems; it differ from other layers as it does not provide services to other layers, it also establishes availability of the end user host system
    - Presentation Layer: translates data in a way that ensures the data is readable by the application layer of both end-users  
    - Session Layer: establishes, manages and terminates sessions between two communicating hosts 
    - Transport Layer: breaks down data into segments for uninterrupted transmission also accounts for data retransmission when error is encountered depending on the type of protocol used (UDP/TCP), and uses a port number to identify which application the data belongs to (e.g. port 80)  
    - Network Layer: provides connection between two hosts that are geographically separated; sending data in packets each containing an IP address
    - Data-link Layer: defines the format of data transmission and how data access is controlled, it matches MAC addresses to validate transmission of data between the physical layer, the switch also functions in this layer
    - Physical Layer: The physical hardware that transfers data in bits through electrical signals (copper), light pulses (fiber), or radio waves (wireless)
- The PDU(protocol data unit) is the specific unit of data each layer uses in transmission:
    - Application Layer: Data
    - Transport Layer: Segments
    - Network Layer: Packets
    - Data-link Layer: Frames
    - Physical Layer: Bits
- the process by which the data is sent from the sender's system down to the physical layer is called encapsulation whereas the process of sending the data from the physical layer to the application layer of receiver is called de-encapsulation  

**Struggles/Questions:**
- we are supposedly going to go deeper into the last four layers, as for now i dont rlly have confusions as this is just the basic of the foundations 

**Goal for tomorrow:**
- [One specific thing]

```python

```
