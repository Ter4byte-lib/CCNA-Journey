# Day 1 — OSI Model & Cisco IOS

**Date:** 18-06-2026
**Status:** 🟢 Complete

---

## 📘 Topic 1: The OSI Model

### What I Learned

- The OSI model is a conceptual framework and a standardization of how computers communicate. It contains 7 layers, each with a specific function. The independence of each layer allows for interoperability, so engineers can focus on their own area of expertise when troubleshooting. This also makes debugging easier, since identifying the faulty layer means the other layers don't have to be touched.
- The TCP/IP stack, however, is not conceptual — it's the actual framework used in networking. It contains 4 layers with functions similar to the seven layers in the OSI model. Two of these four layers essentially condense multiple OSI layers into one:
  - The **Application layer** in the TCP/IP stack covers the Application, Presentation, and Session layers of the OSI model.
  - The **Link layer** in the TCP/IP stack covers the Data Link and Physical layers of the OSI model.
- Despite this, engineers usually still refer to the OSI model in conversation — likely because its extra granularity gives a shared, precise vocabulary for describing exactly where a problem sits.

**The layers in detail:**

| Layer | Function |
|---|---|
| **Application** | Provides network services to application software. Unlike other layers, it doesn't provide services to another layer — it's the only layer that interfaces directly with the end-user process. Also establishes availability of the communicating host. |
| **Presentation** | Translates/formats data so it's readable by the application layer on both ends (e.g. encryption, compression, character encoding). |
| **Session** | Establishes, manages, and terminates sessions between two communicating hosts. |
| **Transport** | Breaks data into segments for reliable transmission and handles retransmission of lost data — though this depends on the protocol used (TCP does, UDP doesn't). Uses port numbers to identify which application the data belongs to (e.g. port 80). |
| **Network** | Provides logical addressing and routing between hosts on different networks, sending data in packets — each packet carries source and destination IP addresses. |
| **Data Link** | Defines how data is framed and how access to the physical medium is controlled. Uses MAC addresses to identify devices on the local segment. Switches operate at this layer. |
| **Physical** | The physical hardware that transmits data as bits — via electrical signals (copper), light pulses (fiber), or radio waves (wireless). |

**PDU (Protocol Data Unit)** — the unit of data each layer works with:

| Layer | PDU |
|---|---|
| Application | Data |
| Transport | Segments |
| Network | Packets |
| Data Link | Frames |
| Physical | Bits |

- The process of data moving from the sender's application layer down to the physical layer is called **encapsulation**. The reverse — from the physical layer back up to the receiver's application layer — is called **de-encapsulation**.

### Struggles / Questions

We're going deeper into the last four layers next, but for now I don't have any major confusions — this is just the foundation.

---

## 🖥️ Topic 2: The IOS (Internetwork Operating System)

### What I Learned

- IOS has been used since the inception of Cisco and is now the proprietary software running on Cisco routers and switches.
- Other Cisco operating systems differ slightly: IOS uses a **monolithic kernel**, while newer systems like **NX-OS** and **IOS-XR** use a more modular/microkernel-style architecture. *(Note: corrected "IOS-XS" → "IOS-XR" — there's no Cisco OS called IOS-XS.)*
- This matters because in a monolithic kernel, all processes share the same memory space — so if one process crashes, it can take others down with it. In the modular OS, each process runs in its own protected memory space, so a single crash doesn't bring down the rest of the system.
- Connecting to a Cisco device (router/switch) over the network is usually done with **PuTTY**, which supports both **SSH** (Secure Shell) and **Telnet** connections. The two are functionally similar but differ in security: SSH encrypts the data it sends, while Telnet doesn't — meaning Telnet traffic (including usernames and passwords) can be intercepted. Logins are also commonly enforced through integration with **AAA** (Authentication, Authorisation, and Accounting) servers. Once PuTTY is set up, you just enter the IP address of the device to begin configuration.
- For the *initial* connection, though, a direct connection is required — the device doesn't have an IP address yet, so it can't be reached over the network.
- This direct connection uses one of: DB-9 to RJ45, DB-9 to RJ45 adapted with a USB-to-Serial-DB-9 (to work around modern laptops lacking DB-9 ports), or — more commonly today — USB to mini-USB.
- PuTTY is still used for this initial config, but with the connection type set to **Serial** instead. The serial (COM) line can be found in Device Manager (port drivers need to be installed first) — other settings can be left as default.
- A direct connection is also useful for troubleshooting — e.g. when a device can't be reached over the network because its IP is unresponsive — or for configuring the boot process, which can't be done over SSH since that requires the device to already be live (i.e. already booted).

### Lab Exercise — Navigating the IOS *(Packet Tracer)*

![Packet Tracer lab topology](image.png)

#### Exploring User EXEC Mode and CLI Command Help

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

User EXEC mode (`>`) has limited commands, so most tasks happen in **Privileged EXEC mode** (`#`).

#### Exploring Privileged EXEC Mode and Context-Sensitive Help

```diff
Router>enable                     (entering privileged EXEC mode)
Router#disable                    (exiting privileged EXEC mode)
Router>en                         (abbreviations can be used)
Router#di
% Ambiguous command: "di"
Router#di?                        ("?" shows all commands matching the entered keyword)
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
    -- output truncated -- (pressing "Enter" outputs additional commands one line at a time — tedious)
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
    -- output truncated -- (pressing "Spacebar" outputs additional commands page by page)
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
Router#sh aaa user all
Router#sh aaa usor all
                ^
% Invalid input detected at '^' marker.
	
Router#
```

#### Exploring Global Configuration Mode

```diff
Router#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
Router(config)#ip host server1 1.1.1.1      (meaning of these commands covered in later lessons ↓)
Router(config)#ip host server2 2.2.2.2
Router(config)#R1                           (deliberate error)
                ^
% Invalid input detected at '^' marker.
	
Router(config)#hostname R1                  (instead of retyping a command, hit "Up Arrow" to recall the last one — only within the current command-hierarchy level. "Ctrl+A" jumps to the start of the line, "Ctrl+E" to the end — life-saving shortcuts 🫡)
R1(config)#show ip interface brief          ("show" only works in privileged EXEC mode)
            ^
% Invalid input detected at '^' marker.
	
R1(config)#do show ip interface brief       ("do" overrides this restriction)
Interface              IP-Address      OK? Method Status                Protocol 
GigabitEthernet0/0     unassigned      YES NVRAM  administratively down down 
GigabitEthernet0/1     unassigned      YES NVRAM  administratively down down 
GigabitEthernet0/2     unassigned      YES NVRAM  administratively down down 
Vlan1                  unassigned      YES NVRAM  administratively down down
R1(config)#interface gigabitEthernet 0/0    (entering interface config mode)
R1(config-if)#exit                          (moving down the hierarchy one level at a time)
R1(config)#interface gigabitEthernet 0/0
R1(config-if)#end                           (skipping straight to privileged EXEC mode — also achievable with "Ctrl+C")
R1#
%SYS-5-CONFIG_I: Configured from console by console

R1#show running-config                      (viewing the entire device configuration)
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
    -- output truncated --
	
R1#sh run | begin Hostname              (viewing config starting from "Hostname" — no match found, so no output)
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

R1#sh run | include interface           (view only config lines containing "interface")
interface GigabitEthernet0/0
interface GigabitEthernet0/1
interface GigabitEthernet0/2
interface Vlan1
R1#sh run | exclude interface           (exclude lines containing "interface")
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

#### IOS Configuration Management

```diff
R1#copy run start                       (copying running-config to startup-config)
Destination filename [startup-config]? 
Building configuration...
[OK]
R1#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
R1(config)#hostname RouterX             (changing the hostname)
RouterX(config)#do show startup-config  (checking what hostname would apply after a reload)
Using 741 bytes
!
version 15.1
no service timestamps log datetime msec
no service timestamps debug datetime msec
no service password-encryption
!
hostname R1                             (hostname after startup — changes take effect immediately, but are temporary until saved)
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
RouterX#copy run start                  (saving current running-config to startup-config)
Destination filename [startup-config]? 
Building configuration...
[OK]
RouterX#show start                      (verifying the hostname that will apply after startup)
Using 746 bytes
!
version 15.1
no service timestamps log datetime msec
no service timestamps debug datetime msec
no service password-encryption
!
hostname RouterX                        (verified)
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

RouterX#copy run flash                  (backing up the running-config to flash memory — not a great idea 🙂‍↔️)
Destination filename [running-config]? 
Building configuration...
[OK]
RouterX#copy run tftp                   (backing up to an external TFTP server)
Address or name of remote host []? 10.10.10.10 
Destination filename [RouterX-confg]? 

Writing running-config........
%Error opening tftp://10.10.10.10/RouterX-confg (Timed out)   (TFTP server wasn't set up in the lab, so the backup timed out)
RouterX#reload                          (confirming the change to startup config persists)
Proceed with reload? [confirm]
System Bootstrap, Version 15.1(4)M4, RELEASE SOFTWARE (fc1)
Technical Support: http://www.cisco.com/techsupport
Copyright (c) 2010 by cisco Systems, Inc.
 --output truncated-- 

Press RETURN to get started!

RouterX> 
```
