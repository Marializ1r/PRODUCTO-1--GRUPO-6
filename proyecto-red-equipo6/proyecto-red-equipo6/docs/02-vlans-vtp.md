# 🏷️ 02 · VLANs y VTP

[⬅️ Volver al README](../README.md)

## VLANs

| VLAN | Nombre | Bloque | Subred |
|:---:|---|---|---|
| 10 | DOCENTES | R1-CORE | `172.26.8.0/24` |
| 20 | ESTUDIANTES | R1-CORE | `172.26.0.0/21` |
| 30 | GESTION | R1-CORE | `172.26.10.64/27` |
| 40 | VOZ | R1-CORE | `172.26.10.96/27` |
| 50 | FINANZAS | R2 | `172.26.9.128/25` |
| 60 | ACADEMICOS | R2 | `172.26.9.0/25` |
| 70 | DATACENTER | R2 | `172.26.10.0/26` |
| 999 | BLACKHOLE | Ambos | Puertos sin uso (descarte) |

## Dominios VTP

| Dominio | Switch | Rol | Versión | VLANs |
|---|---|---|:---:|---|
| `EQUIPO6-CORE` | SWM1 | 🟢 Servidor | 2 | 10, 20, 30, 40, 999 |
| `EQUIPO6-CORE` | SWM2 | 🟡 Servidor (redundancia) | 2 | 10, 20, 30, 40, 999 |
| `EQUIPO6-CORE` | SWAC1 · SWAC2 · SWAC3 | 🔵 Cliente | 2 | Recibe del servidor |
| `EQUIPO6-R2` | SWA13 | 🟢 Servidor | 2 | 50, 60, 999 |
| — | SW-SERVICIOS | ⚪ Transparente | — | 70, 999 (locales) |

> ℹ️ SW-SERVICIOS y SWA13 no están conectados entre sí (cada uno va solo a R2), por eso VTP no puede sincronizarlos; SW-SERVICIOS usa modo transparente.

## 🔌 Mapa de puertos

### Troncales

| Switch | Puerto | Destino | VLANs permitidas |
|---|---|---|---|
| SWM1 | e0/1-3 (Po1) | SWM2 | 10, 20, 30, 40, 999 |
| SWM1 | e1/0 · e1/1 · e1/2 | SWAC1 · SWAC2 · SWAC3 | 10, 20, 30, 40, 999 |
| SWM2 | e0/1-3 (Po1) | SWM1 | 10, 20, 30, 40, 999 |
| SWM2 | e1/0 · e1/1 · e1/2 | SWAC1 · SWAC2 · SWAC3 | 10, 20, 30, 40, 999 |
| SWAC1/2/3 | e0/0 | SWM1 | 10, 20, 30, 40, 999 |
| SWAC1/2/3 | e0/1 | SWM2 | 10, 20, 30, 40, 999 |
| SWA13 | e0/0 | R2 (e0/0) | 50, 60, 999 |
| SW-SERVICIOS | e0/0 | R2 (e0/1) | 70, 999 |

### Puertos de acceso

| Switch | Puerto | Equipo | VLAN | Protección |
|---|---|---|---|---|
| SWAC1 | e1/0 | DOC1 | 10 · DOCENTES | PortFast + BPDU Guard |
| SWAC2 | e2/0 | EST1 | 20 · ESTUDIANTES | PortFast + BPDU Guard |
| SWAC3 | e3/0 | GES1 | 30 · GESTION | PortFast + BPDU Guard |
| SWA13 | e1/0 | ACA1 | 60 · ACADEMICOS | PortFast + BPDU Guard |
| SWA13 | e2/0 | FIN1 | 50 · FINANZAS | PortFast + BPDU Guard |
| SW-SERVICIOS | e0/1 | SERVICIOS | 70 · DATACENTER | PortFast + BPDU Guard |

📎 Scripts: [`configs/`](../configs/)
