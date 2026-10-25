# 🛡️ 04 · HSRP

[⬅️ Volver al README](../README.md)

SWM1 y SWM2 comparten una **IP virtual por VLAN**. El de mayor prioridad es el activo; con `preempt`, el principal recupera el rol al restablecerse.

| VLAN | Red | IP virtual (gateway) | SWM1 | SWM2 | Prioridad SWM1 / SWM2 | Activo |
|:---:|---|---|---|---|:---:|:---:|
| 10 | Docentes | `172.26.8.1` | `172.26.8.2` | `172.26.8.3` | 110 / 100 | SWM1 |
| 20 | Estudiantes | `172.26.0.1` | `172.26.0.2` | `172.26.0.3` | 110 / 100 | SWM1 |
| 30 | Gestión | `172.26.10.65` | `172.26.10.66` | `172.26.10.67` | 110 / 100 | SWM1 |
| 40 | Voz | `172.26.10.97` | `172.26.10.98` | `172.26.10.99` | 110 / 100 | SWM1 |

```mermaid
sequenceDiagram
    participant PC as 💻 Host
    participant S1 as 🧠 SWM1 (Activo · 110)
    participant S2 as 🧠 SWM2 (Standby · 100)
    PC->>S1: Tráfico al gateway virtual
    S1-->>S2: Hello HSRP
    Note over S1: ❌ Falla SWM1 / interfaz VLAN
    S2->>S2: Toma la IP virtual (Active)
    PC->>S2: Mismo gateway, sin reconfigurar
    Note over S1: ✅ SWM1 se recupera
    S1->>S2: preempt: recupera el rol activo
```

📎 Pasos de la prueba: [`comandos/pruebas-failover.txt`](../comandos/pruebas-failover.txt)
