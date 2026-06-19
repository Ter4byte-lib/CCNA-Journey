# 🖥️ Topic: The IOS (Internetwork Operating System)

**Status:** 🟢 Completed

## What I Learned

The operating system has been used since the inception of the Cisco organisation, it is now the proprietary software used in Cisco routers and switches.

There are other operating systems that differ slightly from IOS: IOS features a monolithic kernel, whereas systems like NX-OS, IOS-XE, and IOS-XR feature a microkernel.


| | IOS | NX-OS / IOS-XE / IOS-XR |
|---|---|---|
| Kernel | Monolithic | Microkernel |
| Process memory | Shared | Protected / isolated |
| If one process crashes | Other processes can crash too | Other processes are unaffected |

When connecting to a Cisco device (router/switch) over the network, it's usually done using the software **PuTTY**. The software allows for an SSH (Secure Shell) or Telnet connection type, which are almost identical (everything is "almost" identical 🤔). They differ in the aspect of security, SSH is more secure than Telnet because it encrypts the data being sent, whereas Telnet doesn't (so hackers could gain unauthorised access to data such as passwords and usernames). Security logins are also enforced through integration with **AAA** (Authentication, Authorisation and Accounting) servers. Once PuTTY has been set up, the IP address of the device to be configured is entered so configuration begins.

> [!IMPORTANT]
> SSH > Telnet, always. Telnet sends everything, including your password, in plain text.

When making initial connections, however, a direct connection is needed, as the device doesn't have an IP address yet so it can't be reached over the network. This direct connection is done using cables:
- DB-9 to RJ45
- DB-9 to RJ45 adapted with a USB-to-Serial-DB-9 (to accommodate the lack of DB-9 ports on modern laptops)
- USB to mini-USB (more common on modern devices)

The same software (PuTTY) is used for initial config, but the connection type used is **Serial**. The serial line can be found in Device Manager on the computer (the port driver needs to be installed first), and other settings can be left as default.

A direct connection is also useful during troubleshooting, for instance when the device can't be reached over the network because its IP address is unresponsive. It's also used to configure the boot process of the device, since SSH can't be used there, as the IP address would need to already be live, meaning the device has already booted up.

## Lab: Navigating the IOS *(Atlas, some coding 😮‍💨)*

![initiating configuration](getting-started.png)

<details>
<summary>🧪 Exploring User EXEC Mode and CLI command help</summary>

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

</details>

> [!NOTE]
> The user exec prompt `>` has limited commands, so most tasks happen in privileged exec mode `#`.

<details>
<summary>🧪 Exploring Privileged EXEC Mode and context-sensitive help</summary>

```diff
Router>enable                    (entering privileged exec mode)
Router#disable                   (exiting privileged exec mode)
Router>en                        (abbreviations could be used)
Router#di
% Ambiguous command: "di"
Router#di?                       ("?" used to see all commands available with the keyword entered)
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
    -- output truncated -- (pressing "Enter" outputs additional commands line by line, tedious)
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

</details>

<details>
<summary>🧪 Exploring Global Configuration Mode</summary>

```diff
Router#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
Router(config)#ip host server1 1.1.1.1     (meaning of commands taught in later lessons ↓)
Router(config)#ip host server2 2.2.2.2
Router(config)#R1                          (deliberate error)
                ^
% Invalid input detected at '^' marker.
	
Router(config)#hostname R1
R1(config)#show ip interface brief         ("show" only works in privileged exec mode)
            ^
% Invalid input detected at '^' marker.
	
R1(config)#do show ip interface brief      ("do" overrides this restriction)
Interface              IP-Address      OK? Method Status                Protocol 
GigabitEthernet0/0     unassigned      YES NVRAM  administratively down down 
GigabitEthernet0/1     unassigned      YES NVRAM  administratively down down 
GigabitEthernet0/2     unassigned      YES NVRAM  administratively down down 
Vlan1                  unassigned      YES NVRAM  administratively down down
R1(config)#interface gigabitEthernet 0/0   (entering interface config mode)
R1(config-if)#exit                         (going down the command hierarchy one level at a time)
R1(config)#interface gigabitEthernet 0/0
R1(config-if)#end                          (skipping straight to privileged exec mode, also achievable with "ctrl-c")
R1#
%SYS-5-CONFIG_I: Configured from console by console

R1#show running-config                     (viewing entire device configuration)
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
	
R1#sh run | begin Hostname                 (viewing config starting at "Hostname", no match, so no output)	
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
    -- output truncated --

R1#sh run | include interface              (view config lines which include "interface")
interface GigabitEthernet0/0
interface GigabitEthernet0/1
interface GigabitEthernet0/2
interface Vlan1
R1#sh run | exclude interface              (exclude lines including "interface")
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

</details>

> [!TIP]
> "Up Arrow" recalls your last command (within the current hierarchy level only), `Ctrl+A` jumps to the start of the line, `Ctrl+E` jumps to the end, life-saving shortcuts 🫡

<details>
<summary>🧪 IOS Configuration Management</summary>

```diff
R1#copy run start                          (copying running config to startup config)
Destination filename [startup-config]? 
Building configuration...
[OK]
R1#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
R1(config)#hostname RouterX                (changing hostname)
RouterX(config)#do show startup-config     (checking the hostname that would be used after startup)
Using 741 bytes
!
version 15.1
no service timestamps log datetime msec
no service timestamps debug datetime msec
no service password-encryption
!
hostname R1                                (still R1, changes take effect immediately but are temporary until saved)
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
    -- output truncated --
RouterX#copy run start                     (saving current running config to startup config)
Destination filename [startup-config]? 
Building configuration...
[OK]
RouterX#show start                         (verifying the hostname that will be used after startup)
Using 746 bytes
!
version 15.1
no service timestamps log datetime msec
no service timestamps debug datetime msec
no service password-encryption
!
hostname RouterX                           (verified)
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

RouterX#copy run flash                     (backing up current running config to flash memory, not a good idea 🙂‍↔️)
Destination filename [running-config]? 
Building configuration...
[OK]
RouterX#copy run tftp                      (backing up to an external TFTP server)
Address or name of remote host []? 10.10.10.10 
Destination filename [RouterX-confg]? 

Writing running-config........
%Error opening tftp://10.10.10.10/RouterX-confg (Timed out)   (TFTP server wasn't set up in the lab, so the backup timed out)
RouterX#reload                             (confirming the startup config change survives a reload)
Proceed with reload? [confirm]
System Bootstrap, Version 15.1(4)M4, RELEASE SOFTWARE (fc1)
    -- output truncated --
Press RETURN to get started!



RouterX>
```

</details>
