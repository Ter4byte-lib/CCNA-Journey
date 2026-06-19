### Topic: The OSI model
#Date: 18-06-2026
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
System Bootstrap, Version 15.1(4)M4, RELEASE SOFTWARE (fc1)
Technical Support: http://www.cisco.com/techsupport
Copyright (c) 2010 by cisco Systems, Inc.
Total memory size = 512 MB - On-board = 512 MB, DIMM0 = 0 MB
CISCO2911/K9 platform with 524288 Kbytes of main memory
Main memory is configured to 72/-1(On-board/DIMM0) bit mode with ECC disabled

Readonly ROMMON initialized

program load complete, entry point: 0x80803000, size: 0x1b340
program load complete, entry point: 0x80803000, size: 0x1b340

IOS Image Load Test
___________________
Digitally Signed Release Software
program load complete, entry point: 0x81000000, size: 0x3bcd3d8
Self decompressing the image :
######################### [OK]
Smart Init is enabled
smart init is sizing iomem
                  TYPE      MEMORY_REQ
     Onboard devices &
          buffer pools      0x022F6000
-----------------------------------------------
                TOTAL:      0x022F6000
Rounded IOMEM up to: 36Mb.
Using 6 percent iomem. [36Mb/512Mb]

              Restricted Rights Legend

Use, duplication, or disclosure by the Government is
subject to restrictions as set forth in subparagraph
(c) of the Commercial Computer Software - Restricted
Rights clause at FAR sec. 52.227-19 and subparagraph
(c) (1) (ii) of the Rights in Technical Data and Computer
Software clause at DFARS sec. 252.227-7013.

           cisco Systems, Inc.
           170 West Tasman Drive
           San Jose, California 95134-1706

Cisco IOS Software, C2900 Software (C2900-UNIVERSALK9-M), Version 15.1(4)M5, RELEASE SOFTWARE (fc2)Technical Support: http://www.cisco.com/techsupport
Copyright (c) 1986-2007 by Cisco Systems, Inc.
Compiled Wed 18-Jul-07 04:52 by pt_team
Image text-base: 0x2100F918, data-base: 0x24729040

This product contains cryptographic features and is subject to United
States and local country laws governing import, export, transfer and
use. Delivery of Cisco cryptographic products does not imply
third-party authority to import, export, distribute or use encryption.
Importers, exporters, distributors and users are responsible for
compliance with U.S. and local country laws. By using this product you
agree to comply with applicable laws and regulations. If you are unable
to comply with U.S. and local laws, return this product immediately.

A summary of U.S. laws governing Cisco cryptographic products may be found at:
http://www.cisco.com/wwl/export/crypto/tool/stqrg.html

If you require further assistance please contact us by sending email to
export@cisco.com.

Cisco CISCO2911/K9 (revision 1.0) with 491520K/32768K bytes of memory.
Processor board ID FTX152400KS
3 Gigabit Ethernet interfaces
DRAM configuration is 64 bits wide with parity disabled.
255K bytes of non-volatile configuration memory.
249856K bytes of ATA System CompactFlash 0 (Read/Write)

Press RETURN to get started!



Router>








Router con0 is now available






Press RETURN to get started.













Router>en
Router#
```

