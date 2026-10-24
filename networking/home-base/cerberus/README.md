<p align="center">
  <img src="../../../assets/banners/architecture.webp" alt="UNSC Cerberus Routing and Security" width="100%" />
</p>

# Cerberus | Routing & Security Domains

[← Home Base](../README.md) | [Nexus VRFs & BGP](../nexus/README.md) | [Networking](../../README.md) | [WAN](../../wan/README.md)

**Cerberus**, a Palo Alto PA-5220, is the routing and security center of the Maryland lab. The 40 GbE connection to the Nexus carries its segmented lab handoffs, while additional interfaces connect WAN, SD-WAN, management, and externally routed services.

## Virtual Routers

| Virtual Router | Domain |
| --- | --- |
| **Blueline** | Production and shared infrastructure |
| **Greenline** | Personal services and EVE-NG development |
| **Redline** | Experimental workloads |
| **Mgmt** | Infrastructure management |
| **Blackline** | Remote-access services |
| **WAN** | Internet, public-address services, and WAN transit |
| **DN42** | DN42 transit and protected enclave routing |

These seven routing domains let Cerberus apply policy between distinct parts of the lab while connecting them to the shared physical network.

## BGP Architecture

### Shared Internet Edge

`UNSC-EDGE-01` participates in eBGP as **AS65000**. It exchanges routes with three Cerberus routing domains:

| Cerberus Virtual Router | ASN | BGP Peer |
| --- | --- | --- |
| **Greenline** | **AS65100** | UNSC-EDGE-01, AS65000 |
| **Redline** | **AS65200** | UNSC-EDGE-01, AS65000 |
| **Blueline** | **AS65300** | UNSC-EDGE-01, AS65000 |

This provides separate routing relationships for production, personal, and experimental networks while retaining a shared upstream Internet edge.

### Catalyst SD-WAN and DN42

The **DN42 virtual router uses AS4200001995**. It exchanges DN42 routes with **c4331-md01**, which transports the external and trusted intersite DN42 routing contexts over Catalyst SD-WAN.

The DN42 connection passes through Cerberus before the corresponding services join the protected lab routing domains. Blueline also participates in the site's SD-WAN and upstream IPv6 reachability.

## Policy Boundaries

Cerberus combines its virtual routers with security zones and explicit traffic policy. The WAN and DMZ are separated from trusted lab segments; management and remote access have dedicated routing contexts; and public-facing services pass through their relevant security controls.

The physical Nexus fabric moves traffic among attached systems, while Cerberus handles routed traffic crossing these security domains.

[← Maryland | Home Base](../README.md) · [Explore the WAN](../../wan/README.md)
