<p align="center">
  <img src="../../assets/banners/architecture.webp" alt="UNSC Network Architecture" width="100%" />
</p>

# Network Architecture & Design Decisions

[← Networking](../README.md) | [UNSC Homelab](../../README.md) | [WAN & External Routing](../wan/README.md)

UNSC has a shared household edge and a more deliberately isolated engineering environment. The important design decision is not simply which devices are deployed, but **which responsibility each one owns**.

## Where the Lab Begins: Cerberus

**Cerberus**, a Palo Alto PA-5220, defines the routed security boundary for the protected lab. It provides inter-zone routing, segmentation and access policy, and the control point for traffic moving between the lab's routed domains and outside networks.

The UDM-SE and parts of the physical core support both household and lab connectivity. Those shared roles are intentional. Cerberus owns the lab's routed security policy while shared upstream devices provide physical connectivity.

Traffic within the same Layer 2 segment can stay on the Nexus fabric; traffic that crosses the protected lab's routed policy boundaries is handled by Cerberus.

## Why the MikroTik Core?

The **UDM-SE has two 10 GbE SFP+ interfaces**. In this design, one serves WAN connectivity, leaving a single high-speed LAN handoff. Both the household network and lab need access to some shared infrastructure and subnets.

**UNSC-CORE-01**, a MikroTik CRS326, gives these networks a common physical aggregation point rather than asking the UDM-SE to provide separate high-speed uplinks for every domain. Household traffic can traverse the same switching platform without becoming part of the protected lab.

The core is therefore shared *physically*, but its design direction is increasingly lab-centric. The next planned extension is direct WireGuard tunnel termination on the core.

## Why the Nexus Border?

**UNSC-BORDER-01**, a Cisco Nexus 92160YC-X, concentrates the lab's compute, storage, and firewall-facing traffic.

The physical TrueNAS system has **dual 25 GbE** connectivity, while physical ESXi hosts use **dual 10 GbE** connections. That provides headroom for shared storage and simultaneous host activity, including bursts during backup windows. With many 10 GbE ports already occupied, the Nexus's 40 GbE uplinks are particularly useful.

- **Core ↔ Border:** 40 GbE
- **Border ↔ Cerberus:** 40 GbE

Those are the **physical** links. Logically, Cerberus remains the routed security boundary for protected lab domains. The 40 GbE links preserve 10 GbE front-panel capacity and provide aggregate headroom for concurrent workloads.

## How the Roles Fit Together

| Component | Architectural reason |
| --- | --- |
| **UNSC-EDGE-01** | Shared Internet entry and WAN failover |
| **UNSC-CORE-01** | Common aggregation for household and lab connectivity |
| **Cerberus** | Routed policy and security boundary defining the protected lab |
| **UNSC-BORDER-01** | High-speed server, storage, and firewall data plane |
| **Chimera** | Independent remote-site security boundary at Cybertron |

This separation lets the household retain its own shared infrastructure while lab routing, segmentation, and experiments follow dedicated security boundaries.

[View the site-level diagram](../../README.md#architecture) · [Explore WAN connectivity](../wan/README.md)
