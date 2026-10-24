# UNSC Homelab

UNSC is my multi-site infrastructure homelab, built around systems, storage, networking, and virtualization. It brings together enterprise hardware, virtualized platforms, and cloud services for hands-on engineering and experimentation.

## Architecture

```mermaid
%%{init: {'theme':'dark','themeVariables': {'background':'#111113','primaryColor':'#19191c','primaryTextColor':'#f3e7e8','primaryBorderColor':'#d77b85','lineColor':'#d77b85','clusterBkg':'#121215','clusterBorder':'#ae626b'}}}%%
flowchart TB
    X(["Xfinity"])
    T(["T-Mobile"])

    subgraph HOME["UNSC HOME"]
        direction TB
        EDGE["UNSC-EDGE-01"]
        CORE["UNSC-CORE-01"]
        CER["Cerberus"]
        BORDER["UNSC-BORDER-01"]
        MD["c4331-md01"]

        subgraph LAB["LAB"]
            direction LR
            COMPUTE["Mercury · Neptune · Uranus"]
            EVE["Earth · Jupiter · Mars<br/>Reach · Titan · Venus"]
            ALPHA["Alpha"]
            JANUS["Janus · Hornet"]
        end

        EDGE --> CORE
        CORE --> CER
        CORE <-. "40 GbE" .-> BORDER
        CER <-->|"40 GbE"| BORDER
        BORDER --- COMPUTE
        BORDER --- EVE
        BORDER --- ALPHA
        BORDER --- JANUS
        CER --- MD
    end

    subgraph CYBER["CYBERTRON"]
        direction TB
        NY["C8000V-NY01"]
        CHIM["Chimera"]
        ESXI["Cybertron"]
        NY --- CHIM
        CHIM --- ESXI
    end

    subgraph NJ["VULTR NEW JERSEY"]
        direction TB
        NJEDGE["C8000V-NJ01"]
        DN42["UNSC-DN42-EDGE02"]
        CS["CrowdSec"]
        DASH["Dashy"]
        FIT["fitgibbon"]
        NJEDGE --- DN42
    end

    FABRIC(["SD-WAN"])
    X --> EDGE
    T -.-> EDGE
    MD --- FABRIC
    NY --- FABRIC
    NJEDGE --- FABRIC

    classDef device fill:#19191c,stroke:#d77b85,color:#f3e7e8,stroke-width:1.5px
    classDef security fill:#2b1a20,stroke:#ff929d,color:#fff3f4,stroke-width:2px
    classDef service fill:#211c29,stroke:#b991d5,color:#f3e7f7,stroke-width:1.3px
    class X,T,EDGE,CORE,BORDER,MD,COMPUTE,EVE,ALPHA,JANUS,NY,ESXI,NJEDGE,DN42,FABRIC device
    class CER,CHIM security
    class CS,DASH,FIT service
    style HOME fill:#111113,stroke:#ae626b,color:#f3e7e8
    style LAB fill:#161619,stroke:#77717f,color:#f3e7e8
    style CYBER fill:#111113,stroke:#ae626b,color:#f3e7e8
    style NJ fill:#111113,stroke:#ae626b,color:#f3e7e8
```

*Core to Border and Border to Cerberus are 40 GbE physical links. Cerberus is the routed security boundary for protected lab networks.*

## Hardware & Platforms

| Category | Platforms |
| --- | --- |
| Networking | Cisco Nexus, Cisco ISR/C8000V, MikroTik, UniFi |
| Security | Palo Alto PA-5220, VM-Series |
| Compute | Dell PowerEdge, Cisco UCS |
| Virtualization | VMware vSphere, Microsoft Hyper-V, EVE-NG |
| Storage | TrueNAS SCALE, QNAP, Windows Storage Spaces |
| Services | Active Directory, DNS, PKI, Veeam, Graylog, CrowdSec, Dashy |

## Related Projects

- [EVE-NG Automation](https://github.com/ksmoove21/eve-ng-automation)
- [UNSC DN42](https://github.com/ksmoove21/unsc-dn42)
