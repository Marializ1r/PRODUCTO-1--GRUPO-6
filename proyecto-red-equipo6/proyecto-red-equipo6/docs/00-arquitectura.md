# 🧱 00 · Arquitectura

[⬅️ Volver al README](../README.md)

## Diagrama lógico

```mermaid
graph TD
    ISP(("☁️ ISP<br/>203.0.113.1/30")):::cloud
    R1["🔀 R1-CORE<br/>RID 1.1.1.1"]:::router
    R2["🔀 R2<br/>RID 2.2.2.2"]:::router
    SWM1["🧠 SWM1 · L3<br/>STP root · HSRP activo"]:::core
    SWM2["🧠 SWM2 · L3<br/>STP backup · HSRP standby"]:::core
    SWAC1["SWAC1"]:::acc
    SWAC2["SWAC2"]:::acc
    SWAC3["SWAC3"]:::acc
    SWA13["SWA13"]:::acc
    SW["SW-SERVICIOS"]:::acc
    DOC1["💻 DOC1<br/>VLAN 10"]:::pc
    EST1["💻 EST1<br/>VLAN 20"]:::pc
    GES1["💻 GES1<br/>VLAN 30"]:::pc
    ACA1["💻 ACA1<br/>VLAN 60"]:::pc
    FIN1["💻 FIN1<br/>VLAN 50"]:::pc
    SRV["🗄️ SERVICIOS<br/>VLAN 70"]:::pc

    ISP ---|"e0/2 · 203.0.113.0/30"| R1
    R1 ---|"s3/0 · 172.26.10.160/30"| R2
    R1 ---|"e0/0 · 172.26.10.164/30"| SWM1
    R1 ---|"e0/1 · 172.26.10.168/30"| SWM2
    SWM1 ===|"Port-Channel 1 · LACP · e0/1-3"| SWM2
    SWM1 --- SWAC1
    SWM1 --- SWAC2
    SWM1 --- SWAC3
    SWM2 --- SWAC1
    SWM2 --- SWAC2
    SWM2 --- SWAC3
    SWAC1 --- DOC1
    SWAC2 --- EST1
    SWAC3 --- GES1
    R2 ---|"e0/0 · trunk 50,60,999"| SWA13
    R2 ---|"e0/1 · trunk 70,999"| SW
    SWA13 --- ACA1
    SWA13 --- FIN1
    SW --- SRV

    classDef cloud fill:#0d1117,stroke:#ff00e5,stroke-width:2px,color:#ff00e5
    classDef router fill:#0d1117,stroke:#39ff14,stroke-width:2px,color:#39ff14
    classDef core fill:#0d1117,stroke:#7b2ff7,stroke-width:3px,color:#c9a7ff
    classDef acc fill:#0d1117,stroke:#00f0ff,stroke-width:2px,color:#00f0ff
    classDef pc fill:#161b22,stroke:#8b949e,color:#e6edf3
```

## Bloques de la red

```mermaid
flowchart LR
    subgraph CORE["🏢 Bloque R1-CORE · DOMINIO_CORE"]
        direction TB
        D["Docentes · VLAN 10"]
        E["Estudiantes · VLAN 20"]
        G["Gestión · VLAN 30"]
        V["Voz · VLAN 40"]
        B1["Blackhole · VLAN 999"]
    end
    subgraph R2B["🏫 Bloque R2"]
        direction TB
        F["Finanzas · VLAN 50"]
        A["Académicos · VLAN 60"]
        DC["Datacenter · VLAN 70"]
        B2["Blackhole · VLAN 999"]
    end
    CORE <-->|"OSPF área 0 · P2P R1↔R2"| R2B
    CORE -->|"Ruta por defecto"| NET(("🌐 ISP"))
    R2B -->|"Vía R1-CORE"| NET
    classDef default fill:#0d1117,stroke:#00f0ff,color:#00f0ff
```

## Dispositivos y roles

| 🖥️ Dispositivo | Tipo | Rol |
|---|---|---|
| ISP | Switch L3 | Simula Internet, ruta de retorno `172.26.0.0/16` |
| R1-CORE | Router | Enlaces enrutados a SWM1, SWM2, R2 e ISP; origina ruta por defecto |
| R2 | Router | Subinterfaces 802.1Q y DHCP del bloque R2 |
| SWM1 | Switch L3 | Raíz STP (4096), HSRP activo (110), servidor VTP, DHCP del core |
| SWM2 | Switch L3 | Raíz secundaria (8192), HSRP en espera (100) |
| SWAC1 · SWAC2 · SWAC3 | Acceso | Clientes VTP: DOC1, EST1, GES1 |
| SWA13 | Acceso | Servidor VTP del dominio R2: ACA1, FIN1 |
| SW-SERVICIOS | Acceso | VLAN 70, servidor SERVICIOS |
