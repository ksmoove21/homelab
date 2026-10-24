<p align="center">
  <img src="../../../assets/banners/architecture.webp" alt="UNSC Cerberus Routing and Security" width="100%" />
</p>

# Cerberus | Routing & BGP

[← Home Base](../README.md) | [Nexus VRFs & BGP](../nexus/README.md) | [Networking](../../README.md) | [WAN](../../wan/README.md)

**Cerberus**, a Palo Alto PA-5220, provides the routed-domain handoffs for the Maryland lab. The 40 GbE connection to the Nexus carries its segmented lab handoffs, while additional interfaces connect WAN, SD-WAN, management, and externally routed services.

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

These seven virtual routers maintain the site's separate route tables and inter-domain connectivity.

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

DN42 routes reach Cerberus through the Maryland SD-WAN edge and its separate routed DN42 handoffs. Blueline also participates in the site's SD-WAN and upstream IPv6 reachability.

## Service VRF Routing

Nexus service VRFs establish their BGP peerings with the matching Cerberus virtual-router domains. The Nexus routes service networks within its individual VRF tables; Cerberus maintains the corresponding upstream and inter-domain route exchange.

For service-zone mappings, firewall rules, and east-west access enforcement, see [Cerberus Security](../../../security/cerberus/README.md).

[← Maryland | Home Base](../README.md) · [Explore the WAN](../../wan/README.md)
