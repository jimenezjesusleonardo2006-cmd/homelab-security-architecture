🛡️ Enterprise-Grade HomeLab: Arquitectura de Seguridad y Nube Privada
📌 Resumen del Proyecto
Diseño, despliegue y administración de una infraestructura de nube privada orientada a la seguridad (Security-First). Este entorno simula una arquitectura empresarial escalable, implementando segmentación de red, almacenamiento seguro, acceso remoto cifrado y monitoreo continuo.

🎯 Objetivos
Construir una infraestructura resiliente de alta disponibilidad (Hypervisor tipo 1).

Implementar seguridad perimetral y políticas de enrutamiento estrictas.

Centralizar la gestión de identidad, control de acceso (ACLs) y almacenamiento masivo.

Desarrollar un entorno seguro para prácticas de Blue Teaming (SIEM/Monitoreo) y Red Teaming (Pentesting).

🛠️ Stack Tecnológico (Tech Stack)
Virtualización y Cómputo: Proxmox VE, Contenedores LXC, VMs.

Redes y Seguridad Perimetral: pfSense (Firewall/Router principal), WireGuard (VPN), Pi-hole (DNS Sinkhole).

Almacenamiento y Datos: TrueNAS (SMB, ZFS), control estricto de ACLs.

Acceso y Automatización: DuckDNS (Cron automatizado para IP Dinámica), Nginx Proxy Manager (Próximamente).

Seguridad Defensiva: Wazuh SIEM (En despliegue).

🏗️ Arquitectura de Red (Topología)

graph TD
    A[Internet / ISP] -->|Doble NAT resuelto| B(pfSense Firewall)
    B --> C[TP-Link AP Wi-Fi]
    B --> D[Proxmox VE]
    
    subgraph Servidor Proxmox
    D --> E[Pi-hole DNS]
    D --> F[TrueNAS Storage]
    D --> G[DuckDNS Cron]
    D --> H[Wazuh SIEM]
    end
    
    subgraph Acceso Externo
    I[Laptop/Móvil Remoto] -->|Túnel WireGuard UDP 51820| B
    end
🚀 Fases de Implementación y Logros Técnicos
Fase 1: Infraestructura y Ruteo Base
Despliegue de Proxmox VE sobre hardware compacto (HP EliteDesk), optimizando recursos mediante el uso de contenedores ligeros (LXC) frente a máquinas virtuales completas.

Resolución de problemas de ruteo interno (Múltiples Default Gateways en Linux Bridge) asegurando la correcta salida a internet del hipervisor a través del firewall interno.

Fase 2: Perímetro y Control de Acceso
Implementación de pfSense como núcleo de enrutamiento, delegando el hardware comercial (TP-Link) exclusivamente a funciones de Access Point.

Resolución de bloqueos de tráfico por Doble NAT y reenvío de puertos (Port Forwarding), permitiendo el establecimiento de túneles VPN estables desde el exterior.

Automatización de resolución de IP dinámica (DDNS) mediante un script cron y la API de DuckDNS, garantizando alta disponibilidad del acceso remoto.

Fase 3: Gestión Segura de Datos (Storage)
Optimización de consumo de CPU/RAM desmantelando servicios monolíticos (Nextcloud) a favor de protocolos de transferencia nativos.

Migración de datasets y aplicación de principios de Mínimo Privilegio: Configuración de recursos compartidos SMB protegidos por credenciales únicas e integridad de permisos ACL recursivos.

Fase 4: Monitoreo y Próximos Pasos (Roadmap)
[En Progreso] Observabilidad: Implementación de agentes Wazuh para recolección de logs de firewall y file integrity monitoring en el NAS.

[En Progreso] Reverse Proxy: Despliegue de Nginx Proxy Manager con certificados SSL (Let's Encrypt) para acceso web seguro sin exposición de puertos.

[Futuro] Segmentación: Creación de VLANs 802.1Q para aislar el tráfico de IoT, red personal y laboratorios de pentesting.

👨‍💻 Sobre el Autor
Estudiante de Ingeniería en Sistemas Computacionales. Apasionado por la arquitectura en la nube y la ciberseguridad.

Certificaciones: Google Cybersecurity Professional Certificate (Octubre 2025).