<p align="center">
  <img src="../assets/banners/networking.webp" alt="UNSC Networking" width="100%" />
</p>

# Networking

[← UNSC Homelab](../README.md) | [Homelab Projects](https://github.com/ksmoove21/homelab-projects)

UNSC connects its Maryland home base, a dedicated ESXi host at Cybertron, and cloud infrastructure at Vultr New Jersey. Each environment serves a different purpose, with shared routing and SD-WAN connectivity bringing the network together.

## Explore the Sites

<table>
<tr>
<td width="33%" valign="top">
<h3><a href="home-base/README.md">Maryland | Home Base</a></h3>
<p>UDM-SE, MikroTik core, Cerberus, Nexus border, and the physical lab.</p>
</td>
<td width="33%" valign="top">
<h3><a href="cybertron/README.md">Cybertron</a></h3>
<p>MyInterServer, dedicated ESXi, Chimera, identity services, and hosted applications.</p>
</td>
<td width="33%" valign="top">
<h3><a href="vultr-cloud/README.md">Vultr Cloud</a></h3>
<p>Cloud routing, DN42, CrowdSec, Dashy, and remote access.</p>
</td>
</tr>
</table>

## Explore the Design

<table>
<tr>
<td width="50%" valign="top">
<h3><a href="architecture/README.md">Architecture & Design Decisions</a></h3>
<p>How the shared edge, routed security boundaries, and high-speed lab fabric fit together.</p>
</td>
<td width="50%" valign="top">
<h3><a href="wan/README.md">WAN & External Routing</a></h3>
<p>UNSC Net, public address space, Internet providers, BGP, and intersite connectivity.</p>
</td>
</tr>
</table>

## Network at a Glance

| Domain | Platforms |
| --- | --- |
| **Shared Internet edge** | UDM-SE, Xfinity, T-Mobile |
| **Core & fabric** | MikroTik CRS326, Cisco Nexus 92160YC-X |
| **Security boundaries** | Cerberus PA-5220, Chimera VM-Series |
| **Intersite routing** | Cisco Catalyst SD-WAN |
| **External connectivity** | UNSC Net, Free Range Cloud, Hurricane Electric, DN42 |

[View the UNSC topology](../README.md#architecture) · [All Homelab Projects](https://github.com/ksmoove21/homelab-projects)
