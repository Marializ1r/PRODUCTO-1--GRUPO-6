<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0D1117,50:7B2FF7,100:00F0FF&height=220&section=header&text=RED%20EMPRESARIAL%20SEGURA&fontSize=44&fontColor=00F0FF&animation=fadeIn&fontAlignY=38&desc=VLANs%20%C2%B7%20HSRP%20%C2%B7%20EtherChannel%20%C2%B7%20OSPFv2%20%C2%B7%20ACLs&descSize=18&descAlignY=60" alt="header"/>

<img src="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=600&size=20&pause=1200&color=00F0FF&center=true&vCenter=true&width=700&lines=Conmutaci%C3%B3n+y+Enrutamiento+(TI-203);Equipo+6+%7C+PNETLab;Alta+disponibilidad+%2B+Segmentaci%C3%B3n+%2B+Seguridad" alt="typing"/>

<br/>

![ITLA](https://img.shields.io/badge/ITLA-Redes%20y%20Seguridad-00F0FF?style=for-the-badge&labelColor=0D1117)
![PNETLab](https://img.shields.io/badge/Plataforma-PNETLab-7B2FF7?style=for-the-badge&labelColor=0D1117)
![OSPF](https://img.shields.io/badge/OSPFv2-%C3%81rea%200-39FF14?style=for-the-badge&labelColor=0D1117)
![HSRP](https://img.shields.io/badge/HSRP-Gateway%20redundante-FF00E5?style=for-the-badge&labelColor=0D1117)
![STP](https://img.shields.io/badge/Rapid--PVST%2B-STP-00F0FF?style=for-the-badge&labelColor=0D1117)
![ACL](https://img.shields.io/badge/ACLs-Seguridad-FF3B3B?style=for-the-badge&labelColor=0D1117)

**Profesor:** Onel Luis Pelegrino &nbsp;|&nbsp; **Materia:** Conmutación y Enrutamiento (TI-203) &nbsp;|&nbsp; **Producto 1**

</div>

---

## 🎯 ¿De qué trata?

Red para una **empresa mediana**, confiable, segura y escalable, con:

| 🧩 Pilar | 🔧 Tecnología |
|---|---|
| Segmentación por departamento | VLANs + VTP |
| Gateway siempre disponible | HSRP |
| Enlaces redundantes | EtherChannel (LACP) + Rapid-PVST+ |
| Enrutamiento interior | OSPFv2 (área 0) + ruta por defecto |
| Control de accesos | ACLs, SSH, BPDU Guard, banners |

---

## 👥 Equipo de trabajo

> ✏️ **Completa esta tabla con los datos del equipo.**

| 👤 Integrante | 🆔 Matrícula | 🛠️ Aporte principal |
|---|---|---|
| Valerie Echavarría | 2024-0319 | Configuración general |
| Randolf Medina | 2025-1620 | Configuracion general |
| Jeiren Reyes | 2025-0732 | Explicación y documentación del Sprint 2 |
| Ely Sanchez | 2025-0819 | Explicación y documentación del Sprint 1 |
| Marializ Beltre | 2025-0189 | Seguimiento y documentacion del producto |

---

## 🗺️ Topología


<div align="center">

<img width="1170" height="659" alt="topologia" src="https://github.com/user-attachments/assets/e779b9ad-b482-41e4-baf6-6a8cf51b4f21" />

<sub>Figura 1. Topología implementada en PNETLab</sub>

</div>

| 🖥️ Equipo | Rol |
|---|---|
| **ISP** | Simula Internet (`203.0.113.1/30`) |
| **R1-CORE** | Núcleo: enlaces a SWM1, SWM2, R2 e ISP; origina la ruta por defecto |
| **R2** | Router-on-a-stick: Finanzas, Académicos y Datacenter |
| **SWM1 / SWM2** | Switches L3 del core: HSRP, STP, EtherChannel |
| **SWAC1-3** | Acceso de Docentes, Estudiantes y Gestión |
| **SWA13 / SW-SERVICIOS** | Acceso de Académicos, Finanzas y Datacenter |

➡️ Diagrama lógico completo en [`docs/00-arquitectura.md`](docs/00-arquitectura.md)

---

## 📚 Documentación por tema

| # | 📄 Documento | Qué encontrarás |
|:---:|---|---|
| 00 | [Arquitectura](docs/00-arquitectura.md) | Diagramas lógicos y flujo entre bloques |
| 01 | [Direccionamiento](docs/01-direccionamiento.md) | IPv4 con VLSM, IPv6 y enlaces P2P |
| 02 | [VLANs y VTP](docs/02-vlans-vtp.md) | Dominios, roles y mapa de puertos |
| 03 | [EtherChannel y STP](docs/03-capa2-etherchannel-stp.md) | Redundancia de capa 2 |
| 04 | [HSRP](docs/04-hsrp.md) | Gateways virtuales y failover |
| 05 | [OSPF e Internet](docs/05-ospf-internet.md) | Enrutamiento y salida al ISP |
| 06 | [Seguridad y ACLs](docs/06-seguridad-acls.md) | ACLs, SSH, matriz de accesos |
| 07 | [DHCP](docs/07-dhcp.md) | Pools y exclusiones |
| 08 | [Pruebas y evidencias](docs/08-pruebas.md) | Tabla de pruebas con capturas |
| 09 | [Errores y soluciones](docs/09-errores-y-soluciones.md) | Problemas encontrados |

---

## 🗃️ Archivos del proyecto

| 📂 Carpeta | Contenido |
|---|---|
| [`configs/`](configs/) | ⚙️ **Scripts de configuración** por equipo (listos para pegar) |
| [`running-configs/`](running-configs/) | 💾 **Running-config final** de cada equipo (pega aquí el `show running-config`) |
| [`comandos/`](comandos/) | ⌨️ TXT con los comandos usados, verificación, pruebas de failover y seguridad |
| [`capturas/`](capturas/) | 📸 Una carpeta por prueba para subir las capturas |
| [`img/topologia/`](img/topologia/) | 🖼️ Imagen de la topología |
| [`docs/`](docs/) | 📄 Documentación por tema + [`sprints/`](docs/sprints/) para los PDFs de entrega |

---


<div align="center">

**🎓 Instituto Tecnológico de Las Américas (ITLA)** · Centro de Excelencia de Redes y Seguridad
*Conmutación y Enrutamiento (TI-203) · Equipo 6*

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:00F0FF,50:7B2FF7,100:0D1117&height=120&section=footer" alt="footer"/>

</div>
