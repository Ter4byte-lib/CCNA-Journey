# 📅 Week 1 Synthesis: Foundations (OSI, IOS, Transport & Network Layers)

**Dates:** 18-06-2026 – 20-06-2026
**Days completed:** 3 (incomplete week, just getting started)
**Status:** 🟢

## Overview

| Day | Date | Topic(s) |
|---|---|---|
| 1 | 18-06 | OSI Model + Cisco IOS |
| 2 | 19-06 | Layer 4: Transport |
| 3 | 20-06 | Layer 3: Network |

## What Connected This Week

- Day 1 set up the seven-layer map, so Day 2 and Day 3 were really just zooming into two of those layers in detail
  - Transport (Day 2) and Network (Day 3) both build directly off the encapsulation idea from Day 1, segments becoming packets as data moves down the stack
- Day 2's port numbers and Day 3's IP addressing are the two halves of how a stateful firewall actually tracks a session, source/dest IP from Layer 3 plus source/dest port from Layer 4
- The IOS lab from Day 1 (navigating EXEC modes, `show ip interface brief`) is the same command you'll lean on once you're actually configuring subnets in later sections

## Hands-on / Labs

<details>
<summary>🧪 IOS navigation practiced this week</summary>

- User EXEC → Privileged EXEC → Global Config → Interface Config, moving up/down with `exit`, `end`, `do`
- Config management: `copy run start`, `show start`, `copy run tftp` (timed out, no TFTP server set up in the lab)
- Filtering running-config output: `sh run | include`, `sh run | exclude`, `sh run | begin`
- Manual decimal-to-binary conversion for IP addresses (236 → `11101100`, 179 → `10110011`)

</details>

## Open Questions (carrying into Week 2)

> [!NOTE]
> These are still unresolved and likely get answered once subnetting goes deeper.

- Network address vs host address, specifically why the first usable host is `.1` and the last is `.254`
- What "contiguous 1s" actually means for a subnet mask, and how that connects to slash notation
- Whether a mask like `11111111.00001111.11110000.11111111` is legal, and what `0.0.0.0` / `255.255.255.255` masks would even mean
- The difference between "data" and "traffic" as terms, they keep getting used interchangeably

## Next Week Focus

- Subnetting is one of the six heavier sections, budget more time than the video runtime suggests
- [what's next on your course, ACLs / more Layer 3, or something else?]