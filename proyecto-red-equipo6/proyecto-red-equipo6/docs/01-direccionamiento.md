# 🔢 01 · Direccionamiento

[⬅️ Volver al README](../README.md)

**Bloque del Equipo 6:** IPv4 `172.26.0.0/15` (172.26.0.0 – 172.27.255.255) · IPv6 `2001:25:26::/48`

**Método VLSM:** ordenar de mayor a menor número de hosts, elegir el prefijo más pequeño que alcance y asignar de forma consecutiva sin solapamientos.

## 🏢 Bloque R1-CORE

| VLAN | Nombre | Hosts req. | Subred | Máscara | Gateway (HSRP) | SWM1 | SWM2 |
|:---:|---|:---:|---|---|---|---|---|
| 10 | DOCENTES | 164 | `172.26.8.0/24` | 255.255.255.0 | `172.26.8.1` | `.2` | `.3` |
| 20 | ESTUDIANTES | 1500 | `172.26.0.0/21` | 255.255.248.0 | `172.26.0.1` | `.2` | `.3` |
| 30 | GESTION | 29 | `172.26.10.64/27` | 255.255.255.224 | `172.26.10.65` | `.66` | `.67` |
| 40 | VOZ | 16 | `172.26.10.96/27` | 255.255.255.224 | `172.26.10.97` | `.98` | `.99` |
| 999 | BLACKHOLE | 10 | — (VLAN de descarte, sin interfaz IP) | — | — | — | — |

## 🏫 Bloque R2

| VLAN | Nombre | Hosts req. | Subred | Máscara | Gateway (subinterfaz R2) |
|:---:|---|:---:|---|---|---|
| 50 | FINANZAS | 64 | `172.26.9.128/25` | 255.255.255.128 | `172.26.9.130` (e0/0.50) |
| 60 | ACADEMICOS | 80 | `172.26.9.0/25` | 255.255.255.128 | `172.26.9.2` (e0/0.60) |
| 70 | DATACENTER | 44 | `172.26.10.0/26` | 255.255.255.192 | `172.26.10.2` (e0/1.70) |
| 999 | BLACKHOLE | 10 | — (VLAN de descarte) | — | — |

## 🔗 Enlaces punto a punto

| Enlace | Red | Extremo A | Extremo B |
|---|---|---|---|
| R1-CORE ↔ R2 | `172.26.10.160/30` | R1-CORE `s3/0` → `.161` | R2 `s3/0` → `.162` |
| R1-CORE ↔ SWM1 | `172.26.10.164/30` | R1-CORE `e0/0` → `.165` | SWM1 `e0/0` → `.166` |
| R1-CORE ↔ SWM2 | `172.26.10.168/30` | R1-CORE `e0/1` → `.169` | SWM2 `e0/0` → `.170` |
| R1-CORE ↔ ISP | `203.0.113.0/30` | ISP → `.1` | R1-CORE `e0/2` → `.2` |

## 📐 ¿Por qué ese tamaño?

| Prefijo | Máscara | Hosts utilizables | Se usó en |
|:---:|---|:---:|---|
| /21 | 255.255.248.0 | 2,046 | Estudiantes (un /22 solo da 1,022) |
| /24 | 255.255.255.0 | 254 | Docentes (un /25 solo da 126) |
| /25 | 255.255.255.128 | 126 | Académicos y Finanzas (un /26 da 62) |
| /26 | 255.255.255.192 | 62 | Datacenter |
| /27 | 255.255.255.224 | 30 | Gestión y Voz |
| /28 | 255.255.255.240 | 14 | Blackhole |
| /30 | 255.255.255.252 | 2 | Enlaces punto a punto |

> 💡 En cada subred se restan 2 direcciones (red y broadcast). Con HSRP se reservan 3 más para infraestructura (IP virtual + una por switch).

## 🌐 IPv6

Cada VLAN recibe un `/64`. El orden sigue el tamaño de las redes IPv4 (la red de 1,500 hosts es la primera).

| N° | Red | Hosts IPv4 | Subred IPv6 | Asignación | Gateway |
|:---:|---|:---:|---|---|---|
| 1 | Estudiantes | 1500 | `2001:25:26:10::/64` | SLAAC + DHCPv6 | `fe80::1` |
| 2 | Docentes | 164 | `2001:25:26:20::/64` | SLAAC + DHCPv6 | `fe80::1` |
| 3 | Académicos | 80 | `2001:25:26:30::/64` | SLAAC + DHCPv6 | `fe80::2` |
| 4 | Finanzas | 64 | `2001:25:26:40::/64` | Estática + DHCPv6 | `fe80::2` |
| 5 | Datacenter | 44 | `2001:25:26:50::/64` | Solo estática | `fe80::2` |
| 6 | Gestión | 29 | `2001:25:26:60::/64` | Estática | `fe80::1` |
| 7 | Voz | 16 | `2001:25:26:70::/64` | SLAAC | `fe80::1` |
| 8 | Blackhole (R1) | 10 | `2001:25:26:80::/64` | Estática | `fe80::1` |
| 9 | Blackhole (R2) | 10 | `2001:25:26:90::/64` | Estática | `fe80::2` |
| 10 | P2P R1↔R2 | 2 | `2001:25:26:FF::/64` | Manual | — |


