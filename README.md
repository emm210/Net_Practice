*This project has been created as part of the 42 curriculum by iait-mou.*

# NetPractice

## Description

NetPractice is a pedagogical project designed to reinforce the fundamentals of computer networking through a series of practical, puzzle-style exercises. The goal of this project is not to write code, but to correctly configure a set of virtual network topologies — assigning IP addresses, subnet masks, default gateways, and static routes to hosts, switches, and routers — so that every machine in the topology can successfully communicate according to the goals defined at each level.

Each level presents an increasingly complex network diagram (hosts, switches, routers, and sometimes a simulated Internet node) with some fields pre-filled and others left blank or intentionally misconfigured. The objective is to identify and correct the configuration so that all communication goals for that level pass.

This project builds practical intuition for how real networks are designed and debugged: how addressing and subnetting work, how routers decide where to forward traffic, and why a single misconfigured mask or gateway can silently break connectivity across an entire network.

## Instructions

### Running the training interface

1. Clone this repository and navigate to its root.
2. Launch the training interface with:
```bash
   ./run.sh
```
3. The interface opens in your browser, presenting the levels in order. Each level displays a topology diagram along with a list of goals (e.g., "Host A needs to communicate with Host B").
4. Fill in the editable fields (IP addresses, subnet masks, routes) directly in the diagram.
5. Click **"Check again"** to validate your configuration against the level's goals. The status of each goal (OK/KO) and a packet-trace log are shown to help debug any failure.

### Exporting configurations

Once all goals for a level show **OK**, use the **"Get my config"** button in the interface to export that level's configuration file.

### Submission requirements

- **10 exported configuration files** (one per level) must be placed at the **root of this repository**.
- Each file must correspond exactly to a completed, validated level (all goals passing).
- Ensure the repository is clean of any unrelated or intermediate files before submission.

## Resources

### Networking concepts studied

- TCP/IP addressing (IPv4)
- Subnet masks and CIDR notation
- Subnetting and VLSM (Variable Length Subnet Masking)
- Network, broadcast, and usable host address calculation
- Default gateways and static/default routes
- Routers vs. switches, and broadcast domains
- Point-to-point links between routers
- The OSI model and the TCP/IP model (layers, encapsulation)
- Multicast and reserved address ranges

### References

- [RFC 791 – Internet Protocol](https://www.rfc-editor.org/rfc/rfc791)
- [RFC 950 – Internet Standard Subnetting Procedure](https://www.rfc-editor.org/rfc/rfc950)
- [RFC 1918 – Address Allocation for Private Internets](https://www.rfc-editor.org/rfc/rfc1918)
- Cisco Networking Academy, *Introduction to Networks* course materials
- [Subnetting practice — subnetting.net](https://subnetting.net)

### AI usage

An AI assistant (Claude, by Anthropic) was used strictly as a **learning and verification aid**, not to generate or determine the final submitted configurations. Specifically, it was used to:

- Explain subnetting mechanics (converting masks to binary, computing block sizes, network/broadcast/host ranges, CIDR notation).
- Walk through the OSI model and encapsulation process layer by layer.
- Help interpret the training interface's packet-trace output (e.g., distinguishing "invalid route" vs. "multiple interface match" errors) to identify which specific configuration field was likely misconfigured.
- Explain general networking concepts (multicast, VLSM, routers vs. switches) on request.

All final IP/mask/route values entered into the training interface, and all exported configuration files submitted, were determined and validated by the author(s) using the interface's own "Check again" feedback.