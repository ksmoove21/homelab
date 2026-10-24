<p align="center">
  <img src="../../assets/banners/wan.webp" alt="UNSC Networking, Vultr Cloud" width="100%" />
</p>

# Vultr Cloud

[← Networking](../README.md) | [Home Base](../home-base/README.md) | [Cybertron](../cybertron/README.md)

**Vultr New Jersey** is UNSC's cloud-based networking and services location. It combines Catalyst SD-WAN connectivity, external BGP and DN42 routing, and operational services that support the wider multi-site environment.

## Cloud Architecture

| Platform | Role |
| --- | --- |
| **C8000V-NJ01** | Catalyst SD-WAN edge and private site integration |
| **UNSC-DN42-EDGE02** | MikroTik CHR providing DN42 public-edge routing |
| **CrowdSec** | Central threat-event processing and threat-list distribution |
| **Dashy** | Service dashboard |
| **fitgibbon** | Windows Remote Desktop Gateway |

## Routing & Connectivity

The **Catalyst 8000V** connects the Vultr site to Home Base and Cybertron over the UNSC SD-WAN fabric. Its service routing separates the normal private site connection from external DN42 transport.

The **MikroTik CHR** participates in DN42 as **AS4242421995** and maintains external WireGuard/eBGP peerings. DN42 route exchange is transported toward Maryland for Cerberus policy enforcement.

Vultr also provides independent IPv6 connectivity for **2602:fed2:719c::/48**, routed through the cloud site's upstream.

## Shared Services

**CrowdSec** collects and correlates security events from the wider UNSC environment, including PAN-OS and UniFi sources. It distributes threat intelligence to Cerberus, Chimera, and the home edge.

**Dashy** provides a service dashboard, while **fitgibbon** supports remote administration across the private site integration path.

This location extends UNSC's operational capabilities beyond the primary rack and Cybertron's dedicated ESXi server.

[← Networking](../README.md) · [WAN & External Routing](../wan/README.md) · [UNSC DN42](https://github.com/ksmoove21/unsc-dn42)
