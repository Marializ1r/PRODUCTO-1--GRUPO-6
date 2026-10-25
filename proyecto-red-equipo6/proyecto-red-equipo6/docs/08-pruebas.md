# 🧪 08 · Pruebas y evidencias

[⬅️ Volver al README](../README.md)

> ✏️ Completa **Resultado obtenido** y sube cada captura en su carpeta de [`capturas/`](../capturas/).

| N° | 🔍 Prueba | ⌨️ Comando / acción | 🎯 Esperado | 📝 Obtenido | 📸 Captura |
|:---:|---|---|---|---|---|
| 1 | VTP sincronizado | `show vtp status` · `show vlan brief` en clientes | Dominio `EQUIPO6-CORE`; VLANs 10, 20, 30, 40, 999 | _completar_ | [📁](../capturas/01-vtp) |
| 2 | Troncales | `show interfaces trunk` | Troncales hacia SWM y SWAC activos | _completar_ | [📁](../capturas/02-trunks) |
| 3 | EtherChannel | `show etherchannel summary` | Po1 con puertos en **P** | _completar_ | [📁](../capturas/03-etherchannel) |
| 4 | STP | `show spanning-tree summary` | Rapid-PVST+; SWM1 raíz | _completar_ | [📁](../capturas/04-stp) |
| 5 | HSRP | `show standby brief` | SWM1 activo en todas las VLAN | _completar_ | [📁](../capturas/05-hsrp) |
| 6 | DHCP | `ip dhcp` · `show ip` en PCs | Cada PC recibe IP de su pool | _completar_ | [📁](../capturas/06-dhcp) |
| 7 | Gateway | `ping` al gateway | Respuesta correcta | _completar_ | [📁](../capturas/07-gateway) |
| 8 | Failover HSRP | Ping continuo; apagar `interface vlan 10` en SWM1 | SWM2 pasa a activo; pocos pings perdidos | _completar_ | [📁](../capturas/08-failover-hsrp) |
| 9 | Failover de enlace | Apagar `e0/1` de SWM1 durante un ping | El ping continúa | _completar_ | [📁](../capturas/09-failover-enlace) |
| 10 | OSPF | `show ip ospf neighbor` · `show ip route ospf` | Vecinos FULL; rutas propagadas | _completar_ | [📁](../capturas/10-ospf) |
| 11 | Ruta por defecto | `show ip route` en R2 y SWM1 | `O*E2 0.0.0.0/0` vía R1-CORE | _completar_ | [📁](../capturas/11-ruta-default) |
| 12 | Internet | `ping 203.0.113.1` / `203.0.113.2` | Respuesta correcta | _completar_ | [📁](../capturas/12-internet) |
| 13 | ACL Estudiantes ✗ Gestión | `ping` de EST1 a GES1 | ❌ Bloqueado | _completar_ | [📁](../capturas/13-acl-estudiantes-gestion) |
| 14 | ACL Finanzas ✗ Estudiantes | `ping` de FIN1 a EST1 | ❌ Bloqueado | _completar_ | [📁](../capturas/14-acl-finanzas-estudiantes) |
| 15 | SSH solo Gestión | `ssh` desde GES1 y otra VLAN | ✅ Gestión / ❌ resto | _completar_ | [📁](../capturas/15-ssh) |
| 16 | Extremo a extremo | `ping` / `trace` entre departamentos | Respuesta correcta | _completar_ | [📁](../capturas/16-extremo-a-extremo) |

> 🔄 Tras cada falla se restaura el equipo o enlace y se confirma que HSRP devuelve el rol al principal (`preempt`).

📎 Guías: [`pruebas-failover.txt`](../comandos/pruebas-failover.txt) · [`pruebas-seguridad.txt`](../comandos/pruebas-seguridad.txt) · [`verificacion.txt`](../comandos/verificacion.txt)
