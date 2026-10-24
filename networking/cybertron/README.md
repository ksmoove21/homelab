<p align="center">
  <img src="../../assets/banners/networking.webp" alt="UNSC Networking, Cybertron" width="100%" />
</p>

# Cybertron

[← Networking](../README.md) | [Home Base](../home-base/README.md) | [Vultr Cloud](../vultr-cloud/README.md)

**Cybertron** is UNSC's dedicated remote infrastructure host at **MyInterServer**. One physical ESXi server runs the site's virtualization, network security, SD-WAN, identity, backup, and hosted application workloads.

## How Cybertron Connects

Cybertron has its own provider Internet attachment and the public IPv4 block **64.20.53.0/29**. Its external-facing and internal service networks are separated through VMware virtual switching and Chimera's routed security architecture.

| Platform | Role |
| --- | --- |
| **MyInterServer** | Dedicated server hosting and Internet connectivity |
| **Cybertron** | Physical ESXi virtualization host |
| **Chimera** | Palo Alto VM-Series firewall and site security boundary |
| **C8000V-NY01** | Cisco Catalyst 8000V participating in the UNSC SD-WAN fabric |

The hosted SD-WAN router exchanges remote UNSC routes with Chimera. Chimera manages local gateways, internal routing, public service publication, and firewall policy.

## Chimera Routing Design

Chimera uses two primary Palo Alto virtual routers:

| Virtual Router | Responsibility |
| --- | --- |
| **External** | Public Internet connectivity, service publication, and outside routing |
| **Internal** | Protected service networks, local gateways, and SD-WAN handoff |

The internal environment is divided into enterprise management, identity, and web service networks. This allows Cybertron to publish application services while keeping its management and directory-service traffic under dedicated routing and security policy.

## Hosted Infrastructure

- Active Directory domain controllers
- Two Windows NPS servers
- Veeam backup services
- Dedicated GoGo web application servers
- Chimera and the Catalyst SD-WAN virtual edge

Cybertron also provides an independent location for supporting infrastructure outside the primary Maryland rack. The physical host is the common compute foundation for these virtual services.

[← Networking](../README.md) · [WAN & External Routing](../wan/README.md)
