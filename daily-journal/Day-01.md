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
- we are supposedly going to go deeper into the last four layers, as for now i dont rlly have confusions as this is just the basics of the foundation


# Topic: The IOS (Internetwork Operating System)
**Status:** 🟢 

**What I learned:**
- The operating system has been used since the inception of the Cisco organisation; it is now the propeitry doftware used in cisco routers and switches
- there are other software that differ slightly from the IOS in that the IOS features a monolithic kernel whereas other operaring system like: NX-OS, IOS-XE, IOS-XS feature a micro kernel
- This means that IOS runs its process in such a way that if one process crashes , other processes crash aswell whereas the varieted OS runs each process in protected memory adress space, so if one process crashes, it does not affect the other process
- When connecting to cisco device (router/switch) over the netwrok its usually done using the software "Putty"; the software allows for an SSH(Secure Shell) or Telnet connection type. which are almost identical (everything is "almost" identical 🤔), they differ in the aspect of security where SSH is more secure than Telnet this is because SSH encrypts the data being sent whereas Telnet doesnt (so hackers could gain unaurthorised accees to data such as password and usernames); along with the connection types security logins are also enforced through integration with AAA(Autentication, Atthourisation and Accounting) servers. when the putty software has been setup , the IP adress of the device to be configure is entered so configuration begins
- When making intial connections however; direct connection is needed as the device does not have an ip adress so it can be connected to over a network
- this direct connction is done using cables: DB-9 to RJ45 , DB-9 to RJ45 addapted with a USB to Serial DB-9(to accomodate the lack of DB9 ports on modern laptops) , and modernly the USB to mini-USB is used.
- The same sfotware is used for initial config (Putty); however this time the type of connection used is the "Serial", The serial line can be found on the device manager info on the computer (the driver for the ports need to be installed before this can happen) and other settins can be left as default
- the direct connection could aslo be used during troubleshooting for instance when the device cant be conneted to over a network where its IP adress is unresponsive. it could als be use d to configure the bootup process of the device where SSH connection cant becuse the IP adress would need to be live meaning its already booted up

##### Navigating the IOS - Lab excercise (Atlas, some coding 😮‍💨)

![alt text](image.png)

### [Exploring User Exec Mode and CLI command help]

```diff
+Router>?
Exec commands:
  <1-99>      Session number to resume
  connect     Open a terminal connection
  disable     Turn off privileged commands
  disconnect  Disconnect an existing network connection
  enable      Turn on privileged commands
  exit        Exit from the EXEC
  logout      Exit from the EXEC
  ping        Send echo messages
  resume      Resume an active network connection
  show        Show running system information
  ssh         Open a secure shell client connection
  telnet      Open a telnet connection
  terminal    Set terminal line parameters
  traceroute  Trace route to destination
```
the user exec - ">" has limited commands so we will majorly carry out tasks in the previleged exec - "#" mode 


### [Exploring previliged Exec mode and context sensitive help]
```diff

Router>enable (entering previleged exec mode)
Router#disable (exiting previleged exec mode)
Router>en (abbrevaitions could be used)
Router#di
% Ambiguous command: "di"
Router#di? ("?" used to see all commands available with the keyword entered.)
dir  disable  disconnect  
Router#disa
Router>en
Router#sh?
show  
Router#sh
% Incomplete command.
Router#sh ?
  aaa                Show AAA values
  access-lists       List access lists
  arp                Arp table
  cdp                CDP information
  class-map          Show QoS Class Map
  clock              Display the system clock
  controllers        Interface controllers status
   --More-- 
    -- output truncated -- (pressing the "Enter" key outputs the additional commands line by line (tedious) )
  flow               Flow information
  frame-relay        Frame-Relay information
  history            Display the session command history
  hosts              IP domain-name, lookup style, nameservers, and host table
  interfaces         Interface status and configuration
  ip                 IP information
  ipv6               IPv6 information
  license            Show license information
  line               TTY line information
   --More-- 
    -- output truncated -- (pressing the "Spacebar" key outputs additional caommands page by page)
  spanning-tree      Spanning tree topology
  ssh                Status of SSH server connections
  standby            standby configuration
  startup-config     Contents of startup configuration
  storm-control      Show storm control configuration
  tcp                Status of TCP connections
  tech-support       Show system information for 
   --More-- 
   -- output truncated --
  vtp                Configure VLAN database
  zone               Zone Information
  zone-pair          Zone pair information
Router#sh aaa ?
  local     Show AAA local method options
  sessions  Show AAA sessions as seen by AAA Session MIB
  user      Show users active in AAA subsystem
Router#sh aaa us
% Incomplete command.
Router#sh aaa us
Router#sh aaa user all
Router#sh aaa usor all
                ^
% Invalid input detected at '^' marker.
	
Router#
```

### [Exploring Global Configuration mode]

```diff
Router#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
Router(config)#ip host server1 1.1.1.1 (meaning of commands taught in further lessons ↓)
Router(config)#ip host server2 2.2.2.2
Router(config)#R1(delibrate error)
                ^
% Invalid input detected at '^' marker.
	
Router(config)#hostname R1(instead of retyping the whole comman again jsut hit the  "Up-Arrow" key to go back to most recent command, scrolling back through entire history is possible with this but only the history as far as the in the current level of command hierachy. "ctrl-a" could also be used to go to the extreme beginning of the command , "ctrl-e" is used to go to the extreme end of the command entered (life-saving shortcuts🫡))
R1(config)#show ip interface brief("show"only possible in previleged exec mode)
            ^
% Invalid input detected at '^' marker.
	
R1(config)#do show ip interface brief("do" is used to override this however)
Interface              IP-Address      OK? Method Status                Protocol 
GigabitEthernet0/0     unassigned      YES NVRAM  administratively down down 
GigabitEthernet0/1     unassigned      YES NVRAM  administratively down down 
GigabitEthernet0/2     unassigned      YES NVRAM  administratively down down 
Vlan1                  unassigned      YES NVRAM  administratively down down
R1(config)# interface gigabitEthernet 0/0(entering interface config mode)
R1(config-if)#exit() (going down the command hierachy at a one level interval )
R1(config)# interface gigabitEthernet 0/0
R1(config-if)#end(bypasing the one level interval and goin straight to the previleged exec mode - also achievebel with "ctrl-c")
R1#
%SYS-5-CONFIG_I: Configured from console by console

R1# show running-config (viewing entire device configuration)
Building configuration...

Current configuration : 741 bytes
!
version 15.1
no service timestamps log datetime msec
no service timestamps debug datetime msec
no service password-encryption
!
hostname R1
!
line con 0
!
line aux 0
!
line vty 0 4
 login
!
!
    -- output truncated--
	
R1#sh run | begin Hostname (viewing entire config starting with "Hostname", no instance of "Hostname so no output")	
R1#sh run | begin hostname
hostname R1
!
!
!
no ip cef
no ipv6 cef
!
!
!
license udi pid CISCO2911/K9 sn FTX152457FX
!
!
!
!
    --output truncated--

R1#sh run | include interface (view config lines wich include the word "interface")
interface GigabitEthernet0/0
interface GigabitEthernet0/1
interface GigabitEthernet0/2
interface Vlan1
R1#sh run | exclude interface (not including "interface")
Building configuration...

Current configuration : 741 bytes
!
version 15.1
no service timestamps log datetime msec
no service timestamps debug datetime msec
no service password-encryption
!
hostname R1
!
!
!
!
!
!
!
!
no ip cef
no ipv6 cef
!
!
    -- output truncated --
R1#
```

### [IOS Configuration Management]
```diff
R1#copy run start (copying running config to startup config)
Destination filename [startup-config]? 
Building configuration...
[OK]
R1#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
R1(config)#hostname RouterX(changing hostname)
RouterX(config)#do show startup-config (checking host that would be used during after startup)
Using 741 bytes
!
version 15.1
no service timestamps log datetime msec
no service timestamps debug datetime msec
no service password-encryption
!
hostname R1(hostname to be used after satrtup, commands take effect immediately but are only temporary until we save them )
!
!
!
!
!
!
!
!
no ip cef
no ipv6 cef
!
!
!
!
    --output truncated--
RouterX#copy run start (saving curren running config to startup config)
Destination filename [startup-config]? 
Building configuration...
[OK]
RouterX#show start (to verify what hostname would be used after startup)
Using 746 bytes
!
version 15.1
no service timestamps log datetime msec
no service timestamps debug datetime msec
no service password-encryption
!
hostname RouterX (verified)
!
!
!
!
!
!
!
!
no ip cef
no ipv6 cef
!
!
!
!

RouterX#copy run flash (backing up current running config to flash memory(not a good idea 🙂‍↔️))
Destination filename [running-config]? 
Building configuration...
[OK]
RouterX#copy run tftp(backing up to external TFTP server)
Address or name of remote host []? 10.10.10.10 
Destination filename [RouterX-confg]? 

Writing running-config........
%Error opening tftp://10.10.10.10/RouterX-confg (Timed out) (connectivity to TFTP server in lab was nt set up so timed failed to backup)
RouterX#reload (evidenting shange in startup configurations)
Proceed with reload? [confirm]
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
########################################################################## [OK]
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



RouterX>
```