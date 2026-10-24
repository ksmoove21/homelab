<p align="center">
  <img src="../../assets/banners/architecture.webp" alt="UNSC Network Architecture" width="100%" />
</p>

# Network Architecture & Design Decisions

[← Networking](../README.md) | [UNSC Homelab](../../README.md) | [WAN & External Routing](../wan/README.md)

UNSC has a shared household edge and a more deliberately isolated engineering environment. The important design decision is not simply which devices are deployed, but **which responsibility each one owns**.

## Where the Lab Begins: Cerberus

**Cerberus**, a Palo Alto PA-5220, defines the routed security boundary for the protected lab. Its virtual routers provide the routing handoffs for traffic moving between lab domains, upstream networks, and the remote sites. The [Security documentation](../../security/README.md) covers zone-policy enforcement.

The UDM-SE and parts of the physical core support both household and lab connectivity. Those shared roles are intentional. Cerberus owns the lab's routed inter-domain handoffs while shared upstream devices provide physical connectivity.

Traffic within the same Layer 2 segment can stay on the Nexus fabric; traffic moving between routing domains follows the relevant Nexus and Cerberus route tables.

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
| **Cerberus** | Virtual-router aggregation, external routing exchange, and routed lab handoffs |
| **UNSC-BORDER-01** | High-speed server, storage, and firewall data plane |
| **Chimera** | Remote-site virtual routers and SD-WAN routing handoff at Cybertron |

This separation lets shared household services and dedicated lab routing coexist while keeping each site's routing responsibilities distinct.

## Explore Site Architecture

- [Maryland | Home Base](../home-base/README.md)
- [Cybertron](../cybertron/README.md)
- [Vultr Cloud](../vultr-cloud/README.md)

[View the site-level diagram](../../README.md#architecture) · [Explore WAN connectivity](../wan/README.md)
