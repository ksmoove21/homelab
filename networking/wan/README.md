<p align="center">
  <img src="../../assets/banners/wan.webp" alt="UNSC WAN and External Routing" width="100%" />
</p>

# WAN & External Routing

[← Networking](../README.md) | [UNSC Homelab](../../README.md) | [Architecture & Design Decisions](../architecture/README.md)

UNSC is more than an internal LAN. It has multiple Internet transports, routed public IPv4 space, IPv6 connectivity, an autonomous system on DN42, and a Catalyst SD-WAN fabric connecting local and remote infrastructure.

## WAN Connectivity

| Network | Use |
| --- | --- |
| **Xfinity** | Primary household and lab Internet transport |
| **T-Mobile 5G** | Backup Internet transport |
| **Free Range Cloud** | Public IPv4 prefixes routed over WireGuard to the home edge |
| **Hurricane Electric** | IPv6 tunnel-based reachability through the Maryland ISR and Cerberus |
| **Vultr New Jersey** | Cloud site with independent global IPv6 routing and SD-WAN integration |
| **DN42** | External overlay routing and service-provider experimentation |

## Routing Identity

| ASN | Scope |
| --- | --- |
| **AS4242421995** | Registered DN42 autonomous system and external overlay peering identity |
| **AS65000** | Private BGP autonomous system on the home UDM-SE |

These are distinct routing contexts. The DN42 ASN is not presented as a globally assigned Internet transit ASN; future public-ASN and multihoming designs are excluded from this current-state overview.

## Public IPv4 Addressing

UNSC currently uses two **Free Range Cloud /29** blocks:

| Prefix | Architectural role |
| --- | --- |
| **142.202.91.216/29** | Public DMZ segment connected at the UDM-SE edge |
| **142.202.91.96/29** | Public block routed onward from the UDM-SE toward Cerberus |

Free Range Cloud functions as a **routed public upstream over WireGuard**, not merely an outbound consumer VPN. Public source addresses are preserved where intended, and inbound access remains subject to edge and firewall policy.

## IPv6 Networks

| Prefix | Context |
| --- | --- |
| **2602:fed2:719c::/48** | Global IPv6 allocation, routed and advertised via the Vultr New Jersey upstream |
| **fd16:2e38:95d2::/48** | Registered DN42 IPv6 allocation, used within the DN42 routing domain |
| **2001:470:e15a::/48** | Hurricane Electric routed IPv6 space used by the home-side IPv6 environment |

The first two represent different kinds of address resources: globally routable IPv6 and DN42 overlay addressing. The Hurricane Electric prefix is **provider-routed space**, not being claimed here as independently held address space.

At home, the HE 6in4 path terminates on **c4331-md01** and exchanges IPv6 reachability through Cerberus. The separate Vultr-routed global prefix is not assumed to use that same home-side tunnel.

## Inter-Site Routing

**Catalyst SD-WAN** connects three primary environments:

| Location | Network role |
| --- | --- |
| **UNSC Home** | Shared edge, Cerberus policy boundary, and Maryland SD-WAN edge |
| **Cybertron** | Remote virtualization and Chimera security boundary, with its own SD-WAN edge |
| **Vultr New Jersey** | Cloud SD-WAN edge, DN42 routing, and supporting services |

The SD-WAN fabric carries selected network reachability between sites. It does not remove the requirement for the local firewall boundaries to enforce access policy.

## Externally Consumable Services

The routed WAN design allows selected services to be published or reached through approved public and overlay paths. A prefix being routable does **not** mean all addresses or services are exposed. Publication is intentional and policy-controlled at the UDM-SE and Palo Alto boundaries.

For the external routing and enclave design, see [UNSC DN42](https://github.com/ksmoove21/unsc-dn42).

[Back to Networking](../README.md) · [View Network Architecture](../architecture/README.md)
