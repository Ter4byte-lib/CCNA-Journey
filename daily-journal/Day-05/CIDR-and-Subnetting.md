# Topic: CIDR and Subnetting
**Date:** 24-06-2026 - 26-06-2026

---

## CIDR (Classless Interdomain Routing)

CIDR was introduced to prevent the problem of dedicating too much host address space to a company. For instance, if a company had 1000 hosts, they would be allocated a Class B address, meaning 64,534 host addresses would be wasted. CIDR removed the fixed subnet mask by allowing subnetting, so instead of being restricted to /16 or /24, you could have /20. This allows companies to be allocated addresses close to what they actually need without wastage. It also enables route summarisation, which reduces memory usage, restricts issues to the local part of the network, and reduces CPU load.

---

## Borrowing Host Bits

Subnetting involves moving some host bits to the network portion.

**Formula - borrowed bits:**
> `borrowed bits = given prefix - default prefix of that class`

**Formula - number of subnets:**
> `2 ^ borrowed bits`

**Examples:**
- Class C (`/24` default) using `/28`: `28 - 24 = 4` borrowed bits -> `2^4 = 16` subnets
- Class B (`/16` default) using `/28`: `28 - 16 = 12` borrowed bits -> `2^12 = 4096` subnets

---

## Calculating Number of Host Addresses

**Formula:**
> `(2 ^ host bits) - 2`

We subtract 2 because the network address and broadcast address can't be assigned to hosts.

**Examples:**
- Class C using `/28`: `32 - 28 = 4` host bits -> `(2^4) - 2 = 14` hosts
- Class B using `/28`: `32 - 28 = 4` host bits -> `(2^4) - 2 = 14` hosts per subnet

---

## IP Subnet Zero

IP subnet zero is enabled by default on Cisco routers. It overrides the older limitation that prevented use of the all-zeros and all-ones subnets, which would otherwise waste two subnets per allocation.

---

## Special Subnet Masks (Class C)

### /31 - `255.255.255.254`
- Borrows 7 bits from the host portion (`31 - 24 = 7`)
- Leaves **1 bit** for hosts -> 2 host addresses per subnet
- `2^7 = 128` subnets
- Breaks the standard IP addressing rule, but is supported on Cisco routers for **point-to-point links** (which have no need for a network or broadcast address)
- If allocated `200.15.10.0/24`, valid addresses using /31 run from `200.15.10.0` to `200.15.10.255`

### /30 - `255.255.255.252`
- Block size: `256 - 252 = 4`
- Leaves 2 bits for hosts -> `2^2 - 2 = 2` hosts per subnet
- Borrows 6 bits -> `2^6 = 64` subnets
- Standard and commonly used for point-to-point links

### /29 - `255.255.255.248`
- Host bits: `32 - 29 = 3` -> `2^3 - 2 = 6` hosts per subnet
- Borrowed bits: `29 - 24 = 5` -> `2^5 = 32` subnets
- Block size: `256 - 248 = 8`

**Valid host ranges for `200.15.10.0/29`:**

| Network | First Host | Last Host | Broadcast |
|---------|------------|-----------|-----------|
| .0      | .1         | .6        | .7        |
| .8      | .9         | .14       | .15       |
| .16     | .17        | .22       | .23       |
| ...     | ...        | ...       | ...       |
| .248    | .249       | .254      | .255      |

---

### /31 vs /30

| Feature             | /31          | /30                    |
|---------------------|--------------|------------------------|
| Hosts per subnet    | 2            | 2                      |
| Number of subnets   | 128          | 64                     |
| Address efficiency  | Higher       | Lower                  |
| Standard compliance | Non-standard | Standard               |
| CCNA exam default   | No           | Yes - use /30 for 2 hosts |

---

## Class C Subnet Reference

| Prefix | Subnet Mask     | Subnets | Hosts Each |
|--------|-----------------|---------|------------|
| /25    | 255.255.255.128 | 2       | 126        |
| /26    | 255.255.255.192 | 4       | 62         |
| /27    | 255.255.255.224 | 8       | 30         |
| /28    | 255.255.255.240 | 16      | 14         |
| /29    | 255.255.255.248 | 32      | 6          |
| /30    | 255.255.255.252 | 64      | 2          |
