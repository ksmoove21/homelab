<p align="center">
  <img src="../assets/banners/networking.webp" alt="UNSC Networking" width="100%" />
</p>

# Networking

[← UNSC Homelab](../README.md) | [Homelab Projects](https://github.com/ksmoove21/homelab-projects)

UNSC connects a shared home Internet edge, a dedicated lab security boundary, high-speed server and storage networking, and remote sites. The design reflects where infrastructure is shared, where it is isolated, and why the switching and routing platforms serve different purposes.

## Explore Networking

<table>
<tr>
<td width="50%" valign="top">
<h3><a href="architecture/README.md">Architecture & Design Decisions</a></h3>
<p>Cerberus, the shared edge, the MikroTik core, and the Nexus border.</p>
</td>
<td width="50%" valign="top">
<h3><a href="wan/README.md">WAN & External Routing</a></h3>
<p>Internet access, public IPv4, IPv6, BGP, DN42, and Catalyst SD-WAN.</p>
</td>
</tr>
</table>

## The Network at a Glance

| Domain | Role |
| --- | --- |
| **Shared edge** | UDM-SE, Xfinity, T-Mobile |
| **Physical aggregation** | MikroTik CRS326 |
| **Lab boundary** | Cerberus PA-5220 |
| **High-speed fabric** | Nexus 92160YC-X, 40 GbE core and firewall handoffs |
| **Remote connectivity** | Catalyst SD-WAN, Cybertron, Vultr New Jersey |
| **External routing** | BGP, Free Range Cloud public IPv4, IPv6, DN42 |

The [main architecture diagram](../README.md#architecture) provides the site-level view. These pages explain the reasoning behind it without publishing device configurations or internal addressing.

## Related Projects

- [UNSC DN42](https://github.com/ksmoove21/unsc-dn42)
- [EVE-NG Automation](https://github.com/ksmoove21/eve-ng-automation)
