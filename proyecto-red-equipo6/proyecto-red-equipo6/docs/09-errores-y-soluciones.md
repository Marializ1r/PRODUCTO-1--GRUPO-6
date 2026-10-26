# 🐞 09 · Errores y soluciones

[⬅️ Volver al README](../README.md)

| ❗ Problema | 🔎 Causa | 🛠️ Solución |
|---|---|---|
| FIN1 no recibía IP por DHCP | La ACL `FINANZAS-SEGURIDAD` (in en `e0/0.50`) bloqueaba el DHCPDISCOVER antes de llegar a R2 | `5 permit udp any eq bootpc any eq bootps` al inicio de la ACL |
| VTP no sincroniza SW y SWA13 | No están conectados entre sí | SW-SERVICIOS en modo transparente con VLANs locales |

