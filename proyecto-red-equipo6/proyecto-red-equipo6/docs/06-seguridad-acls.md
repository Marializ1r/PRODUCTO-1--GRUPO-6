# 🔐 06 · Seguridad y ACLs

[⬅️ Volver al README](../README.md)

## ACLs implementadas

| 🔒 ACL | Tipo | Equipo | Aplicada en | Política |
|---|---|---|---|---|
| `SOLO-GESTION` | Estándar | SWM1, SWM2 | `line vty 0 4` (in) | Solo `172.26.10.64/27` entra por SSH |
| `BLOQUEO-ADMIN` | Extendida | SWM1, SWM2 | `interface vlan 20` (in) | **Estudiantes ✗ Gestión**; lo demás se permite |
| `FINANZAS-SEGURIDAD` | Extendida | R2 | `e0/0.50` (in) | **Finanzas ✗ Estudiantes**; lo demás se permite. Incluye regla DHCP (UDP 68→67) |

## Matriz de accesos (orígenes con ACL)

| Origen ↓ / Destino → | Docentes | Estudiantes | Gestión | Finanzas | Académicos | Datacenter | Internet |
|---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
| **Estudiantes** | ✅ | ✅ | ❌ | ✅ | ✅ | ✅ | ✅ |
| **Finanzas** | ✅ | ❌ | ✅ | ✅ | ✅ | ✅ | ✅ |

> ✅ permitido · ❌ bloqueado por ACL.

## Hardening

| Medida | Dónde |
|---|---|
| SSH únicamente (`transport input ssh`) + `login local` | VTY de SWM1 y SWM2 |
| PortFast + **BPDU Guard** | Puertos de acceso |
| VLAN 999 BLACKHOLE | Puertos sin uso |
| Banner MOTD | Todos los equipos |

```text
AVISO: ACCESO SOLO A PERSONAL AUTORIZADO - EQUIPO 6
```

📎 Pasos de prueba: [`comandos/pruebas-seguridad.txt`](../comandos/pruebas-seguridad.txt)
