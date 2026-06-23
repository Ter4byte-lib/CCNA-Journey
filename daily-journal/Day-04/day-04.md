# Topic: IP Classes
**Date:** 20-06-2026

**Status:** 🟢 / 🟡 / 🔴

## What I Learned

The bigger the host portion, the more host addresses are available.
- In subnet mask `/8`, there are 24 bits available to allocate to hosts
- In `/24`, there are 8 bits available to allocate to hosts

When companies want to communicate over the internet, they apply for a range of IP addresses. The IANA (Internet Assigned Numbers Authority) is responsible for IPv4 addressing and assigns IP addresses to them.

Class A addresses are intended for a large number of hosts, so they have a small network portion and a large host portion.

**Class A:**
- Always start with `0` in binary, so the first octet has a range of 1 to 126
- Default subnet mask: `/8`
- Valid network address range: `1.0.0.0` to `126.0.0.0`
- Allows for 126 networks and 16,777,214 hosts per network
- `0.0.0.0/8` is reserved
  - `0.0.0.1` to `0.255.255.255` are invalid host addresses
- `127.0.0.0/8` is reserved for the loopback address
  - `127.0.0.1` to `127.255.255.255` are invalid host addresses — this wiped 33,554,428 host addresses
- To verify TCP/IP function on a computer, we can ping the loopback address: `127.0.0.1`
- Companies usually subnet their total address space to improve performance and security

**Class B:**
- Assigned to medium to large-scale networks
- Always begin with `1 0` in binary
- Default subnet mask: `/16`
- Valid range: `128.0.0.0` to `191.255.0.0`
- Allows for 16,384 networks and 65,534 hosts per network
- Also subnetted into smaller networks

**Class C:**
- Assigned to small networks
- Always start with `1 1 0` in binary
- Default subnet mask: `/24`
- Network address range: `192.0.0.0` to `223.255.255.0`
- Allows for 2,097,152 networks and 254 hosts per network
- Can be subnetted or used as-is

**Private addresses** are reserved within each class. They were originally designed for networks with no internet connectivity. More on this in a later lesson.
- Class A: `10.0.0.0` to `10.255.255.255`
- Class B: `172.16.0.0` to `172.31.255.255`
- Class C: `192.168.0.0` to `192.168.255.255`

These are valid to assign but are not routable on the public internet. A use case would be a school where students can use computers and connect to each other, but are blocked from the internet — so they are for closed networks with no internet connectivity. They are also free to use.

**Class D:**
- Reserved for multicast addresses
- Always start with `1 1 1 0` in binary
- No default subnet mask, no host portion
- Valid range: `224.0.0.0` to `239.255.255.255`

**Class E:**
- Experimental and reserved for future use
- Always begin with `1 1 1 1` in binary
- Not allocated to hosts, no default subnet mask
- Range: `240.0.0.0` to `255.255.255.254`
- `255.255.255.255` is the limited broadcast address (broadcasts to all hosts on the local network)

## Questions