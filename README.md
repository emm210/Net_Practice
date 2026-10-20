*This project has been created as part of the 42 curriculum by iait-mou*

# NetPractice

## Description

NetPractice is a network-configuration training project from the 42 curriculum. Unlike most 42 projects, it involves no code to write — the "exercise" is purely about understanding and correctly applying TCP/IP networking fundamentals inside a graphical training tool.

The tool presents a series of levels, each one a diagram of a small network: a mix of hosts (client machines), switches, routers, and sometimes a simulated "Internet" node. Every level comes with one or more **goals**, written as plain statements such as "Host A needs to communicate with Host B." Some fields in the diagram (IP addresses, subnet masks, static routes) are already filled in and locked; others are left blank, or intentionally filled with a wrong value, and it is the user's job to find and fix them.

The purpose of the project is to build real, hands-on intuition for how IP networks are addressed and routed — not just to memorize formulas, but to understand, for a given topology, why a particular address, mask, or route is required for two machines to actually be able to reach each other, and why a single wrong digit anywhere can silently break communication across the entire network.

### What makes a level pass or fail

Every level is validated independently for each goal. The tool simulates what would really happen to a packet sent from the source machine to the destination: it shows, hop by hop, whether the packet is accepted, whether it matches a route, whether it reaches the destination, and whether the **reply** manages to find its way back (many bugs only break the return path, not the outgoing one). Reading this trace carefully is the main debugging method used throughout the project — the tool effectively tells you, step by step, where communication stops working.

## Instructions

### Running the training interface

The training interface is launched locally with the provided script:

```bash
./run.sh
```

This starts the tool and opens it in a browser. Each level is accessed in order, and each one must be fully solved (all goals showing **OK**) before moving to the next.

## Resources

### Networking concepts studied

This project is a practical application of the following concepts, all of which had to be understood (not just looked up) to solve the levels:

- **IP addressing (IPv4)** — how an address is structured, and what distinguishes a network address from a host address.
- **Subnet masks and CIDR notation** — converting between dotted-decimal masks (e.g., `255.255.255.192`) and prefix length (e.g., `/26`), and what each actually restricts.
- **Subnetting mechanics** — computing block size, network address, broadcast address, and the usable host range for a given IP/mask pair.
- **VLSM (Variable Length Subnet Masking)** — splitting one address block into several smaller, differently-sized, non-overlapping subnets to match the actual number of hosts each network segment needs, rather than wasting addresses on a single fixed size everywhere.
- **Default gateways and routing** — why a host's gateway must be an address inside its own subnet, and what a "default route" (`0.0.0.0/0`) means for a host versus for a router.
- **Static and connected routes** — the difference between a route a router learns automatically because an interface is directly configured on that network, versus one that must be manually added to reach a network the router isn't directly wired to.
- **Routers vs. switches** — why a switch keeps every connected device in the same subnet/broadcast domain (it operates at layer 2, forwarding by MAC address), while only a router separates one subnet from another (it operates at layer 3, forwarding by IP address).
- **Point-to-point links** — why a link between two routers typically only needs a `/30` subnet (2 usable addresses, one per router interface).
- **The OSI and TCP/IP models** — how data is encapsulated going down the stack (application data → segments → packets → frames → bits) and de-encapsulated on the way back up, and which layer is responsible for which addressing (MAC at layer 2, IP at layer 3, ports at layer 4).

### References

- Cisco Networking Academy, *Introduction to Networks* — course chapters on IP addressing and subnetting
- [subnetting.net](https://subnetting.net) — interactive subnetting practice

### AI usage

An AI assistant (Claude, by Anthropic) was used as a **study and debugging aid** throughout this project, not as a source of final answers. Concretely, it was used for:

- **Concept explanations**: walking through binary conversion of IP addresses and masks, the meaning of CIDR prefixes, how to compute block size/network/broadcast/usable range by hand, and the mechanics of VLSM.
- **OSI/TCP-IP model walkthrough**: explaining each layer's responsibility and how encapsulation works between two communicating hosts.
- **Trace interpretation**: helping interpret the training tool's hop-by-hop packet trace output (e.g., distinguishing an "invalid route" error caused by an off-link gateway from a "multiple interface match" error caused by two overlapping subnets on the same router) to narrow down which specific field was misconfigured in a given level.
- **Verification of reasoning**: double-checking manually-derived subnet calculations (network address, broadcast address, valid host range) before entering them into the tool.
