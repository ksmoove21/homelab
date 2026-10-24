# Networking

[← UNSC Homelab](../README.md) | [Homelab Projects](https://github.com/ksmoove21/homelab-projects)

UNSC connects physical infrastructure at home with Cybertron and Vultr New Jersey. Its network combines a redundant Internet edge, high-speed switching, routed security boundaries, and a Catalyst SD-WAN fabric.

## Infrastructure Overview

| Area | UNSC Implementation |
| --- | --- |
| **Internet Edge** | Xfinity and T-Mobile through `UNSC-EDGE-01` |
| **Core & Switching** | `UNSC-CORE-01` (MikroTik CRS326) and `UNSC-BORDER-01` (Cisco Nexus 92160YC-X) |
| **Routing & Security** | Cerberus (Palo Alto PA-5220) at home and Chimera (VM-Series) at Cybertron |
| **Inter-Site Networking** | Cisco Catalyst SD-WAN across the home, Cybertron, and Vultr New Jersey sites |
| **External Routing** | BGP, WireGuard, and the UNSC DN42 edge |
| **Visibility & Management** | Nexus Dashboard, UniFi Network Optimizer, LibreNMS, Graylog, and CrowdSec |

## Architecture

The home network uses a MikroTik core and Cisco Nexus border for aggregation and the server/storage data plane. The core-to-border and border-to-Cerberus links operate at **40 GbE**. Cerberus is the routed security and policy boundary for the protected lab domains.

Catalyst SD-WAN extends connectivity to Cybertron and Vultr New Jersey. Chimera provides Cybertron's local security boundary; Vultr hosts the DN42 edge and supporting network services.

The [main UNSC Homelab page](../README.md#architecture) contains the high-level topology.

## Related Projects

- [UNSC DN42](https://github.com/ksmoove21/unsc-dn42)
- [EVE-NG Automation](https://github.com/ksmoove21/eve-ng-automation)
- [All Homelab Projects](https://github.com/ksmoove21/homelab-projects)
