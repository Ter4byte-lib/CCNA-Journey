# Topic: RFC 1918 and NAT
**Date:** 24-06-2026 - 26-06-2026

---

## RFC 1918 - Private Address Ranges

RFC 1918 is an IETF (Internet Engineering Task Force) standard defining IP address ranges that are not routable on the public internet.

| Class | Range                         | CIDR Notation  | Subnet Mask   |
|-------|-------------------------------|----------------|---------------|
| A     | 10.0.0.0 - 10.255.255.255     | 10.0.0.0/8     | 255.0.0.0     |
| B     | 172.16.0.0 - 172.31.255.255   | 172.16.0.0/12  | 255.240.0.0   |
| C     | 192.168.0.0 - 192.168.255.255 | 192.168.0.0/16 | 255.255.0.0   |

Different organisations can use the same private addresses because private networks don't communicate directly with each other on the internet. Public addresses have to be globally unique because they require internet connectivity.

---

## IPv4 Exhaustion

IPv4 provides 4.3 billion addresses, which engineers initially thought would be more than enough. Addresses like `127.0.0.0` (loopback) were reserved without much concern for wastage. Towards the 1980s though, it was predicted that addresses were going to run out, so IPv6 was introduced as a long-term solution, providing approximately 7.9 x 10^28 times as many addresses as IPv4.

The migration from IPv4 was a very slow process though, so NAT was implemented as a temporary alternative and progressively became a permanent implementation even as IPv6 grew.

---

## NAT (Network Address Translation)

NAT is a process that runs on an organisation's router, allowing private IPv4 addresses to communicate on the internet via a shared public address.

**How it works:**
- The public address acts as an ambassador for the private addresses
- When a single public address is used for multiple private addresses, each session is differentiated through **port numbers** (this is technically PAT - Port Address Translation - but is commonly referred to as NAT)
- The router maintains a translation table mapping each private IP and port to a public port, so replies get forwarded to the right internal host

**Why organisations still prefer RFC 1918 + NAT over IPv6:**
- NAT improves security because internal host addresses are hidden by default
- Network engineers are more experienced with IPv4
- IPv6 adoption has been slow despite IPv4 exhaustion

IPv6 is more commonly found on service provider networks and in countries like India and China, which adopted the internet and mobile services later and could do so on IPv6 natively. IPv4 public addresses are now exhausted, so IPv6 is still the future path.

---

## Common Subnet Assignments

| Use Case             | Prefix | Notes                             |
|----------------------|--------|-----------------------------------|
| End host subnets     | /24    | Most common in organisations      |
| Point-to-point links | /30    | 2 usable hosts                    |
| Loopback interfaces  | /32    | Single host, no network/broadcast |

Complex VLSM designs are more common in enterprises, which may also use public IP addresses on their inside network to maximise utilisation.
