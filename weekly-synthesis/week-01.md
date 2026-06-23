# Week 1: OSI Model, Cisco IOS & Layers 3-4 Fundamentals

### 🔍 Technical Summary
This week was about building the map before walking the territory. The OSI model gives you a 7-layer conceptual breakdown of how two devices actually talk to each other, but TCP/IP is what's really running under the hood, just compressed into 4 layers. Once that framework was in place, I dropped into the IOS itself, the actual OS Cisco routers and switches run, and got comfortable moving between EXEC modes and reading/filtering running-config. Then I went deeper into two specific layers: Transport (flow control, port numbers, TCP vs UDP, how stateful firewalls track sessions) and Network (IP addressing, traffic types, subnet masks, slash notation). The throughline is that everything from here on is really just zooming into one of those 7 layers at a time.

### 💡 Reflection
* **The "Aha!" Moment:** Realising a stateful firewall isn't doing anything magic, it's just remembering the source/dest IP (Layer 3) and port (Layer 4) of outbound traffic, then checking incoming traffic against that record. A fresh SYN with no matching session just gets dropped. *(swap this if something else landed harder for you)*
* **The Challenge:** Subnet masks. Specifically why they always need contiguous 1s, how that connects to slash notation, and what's actually happening with the network/host address split (still confused on why the first usable host is `.1` and last is `.254`). Haven't cracked this one yet, it's carrying into Week 2.
* **Real-world connection:** Every company with a firewall is running the session-tracking logic from Day 2 right now. And the IOS commands from Day 1 (`show ip interface brief`, `sh run | include`) aren't theoretical, they're what a network engineer or SOC analyst is typing into a terminal on an actual shift.

### 💻 Labs Completed
* [Add your .pkt filename(s) here, if you saved any from the IOS lab]
* Diagrams referenced: `types-of-traffics.png`, `subnet-masking.png`, `address-notations.png`, `Session-multiplexing.png`, `port-numbers.png`, `TCP-header.png`, `connection-setup.png`, `UDP-header.png`