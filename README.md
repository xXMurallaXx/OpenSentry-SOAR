# 🛡️ OpenSentry SOAR

> **Status:** 🚧 In Active Development / En Desarrollo | **Version:** 0.5.0-alpha

## 📖 Visión General del Proyecto
**OpenSentry** es una plataforma SOAR (Security Orchestration, Automation, and Response) personalizada y de código abierto. Está diseñada para automatizar el ciclo de vida de respuesta a incidentes (DFIR) y reducir la fatiga de alertas de los analistas de Nivel 1 (L1 SOC Analysts).

El objetivo de este proyecto es demostrar cómo integrar de forma programática soluciones EDR, Firewalls Perimetrales, y Threat Intelligence (CTI) mediante un motor de decisiones desacoplado basado en playbooks YAML.

![Dashboard Preview](images/dashboard.png)
*Vista previa del Case Management Dashboard.*

## 🏗️ Arquitectura del Laboratorio SOC
Las pruebas de integración y respuesta activa se están desarrollando sobre un entorno corporativo simulado en VMware:
* **SIEM / EDR:** Wazuh Manager (Ubuntu) y Wazuh Agents.
* **Gestión de Identidad:** Windows Server 2022 (Active Directory).
* **Seguridad Perimetral:** FortiGate Firewall.
* **Red Team / Threat Hunting:** Kali Linux.
* **Core del SOAR:** Python 3 (Flask, SQLite, APScheduler).

## ✨ Capacidades Desarrolladas (Hasta la fecha)

1.  **Motor de Playbooks YAML Desacoplado:** El "cerebro" del SOAR evalúa alertas entrantes sin código *hardcodeado*, permitiendo crear reglas de respuesta modificando simples archivos de texto.
2.  **Respuesta Activa en Endpoints (EDR):** Aislamiento automático de hosts comprometidos manipulando las reglas del Firewall de Windows a través de la API nativa de Wazuh (Ej: Contención de Ransomware).
3.  **Threat Intelligence Multiplexer:** Auto-enriquecimiento de IPs consultando de forma simultánea APIs de VirusTotal, AbuseIPDB y AlienVault OTX.
4.  **Case Management & Ticketing:** Dashboard web en tiempo real para visualizar incidentes, métricas CTI y liberar cuarentenas con un solo clic.
5.  **ChatOps y Human-in-the-Loop:** Integración bidireccional con un Bot de Telegram. El SOAR notifica bloqueos autónomos y solicita autorización humana para comportamientos dudosos.
6.  **Pipeline Anti-Phishing (En memoria):** Extracción de IOCs (URLs y Hashes) de buzones de reporte trabajando directamente en memoria RAM para evitar infecciones del propio sistema.
7. **Cyber Deception & Active Defense (Honeytokens):** Implementación de una capa de engaño mediante archivos señuelo estratégicamente situados en Windows Server 2022. La telemetría se basa en la auditoría avanzada de objetos del SO (SACLs), permitiendo al SOAR detectar y aislar intrusos en fases tempranas de reconocimiento (Táctica MITRE Discovery).
8. **EDR Active Response (Process Termination):** Interrupción en tiempo real de binarios maliciosos. El SOAR analiza la telemetría de ejecución de procesos y, ante un IoC confirmado, instruye al agente EDR para aniquilar el proceso (kill process) a nivel de sistema operativo en milisegundos.

## 🚀 Pruebas de Concepto (PoC) Exitosas
- [x] Intercepción de ataque Ransomware simulado (borrado de *Shadow Copies* vía `vssadmin`).
- [x] Ejecución de script de cuarentena PowerShell a través del agente EDR.
- [x] Corte total de conectividad de red del atacante manteniendo la telemetría viva con el SIEM.
- [x] Despliegue de Honeytokens con monitorización FIM y auditoría de acceso a objetos en Windows.
- [x] Detección y terminación automática de procesos maliciosos en memoria a través de PowerShell gestionado por el EDR.

![Terminal Containment](images/consola.png)

![Terminal Containment](images/general-failure.png)
*Demostración de Respuesta Activa: Aislamiento de red automático tras alerta crítica.*

## 🗺️ Roadmap Futuro
- [ ] Refactorización del módulo Anti-Phishing para integrarlo al motor YAML.
- [ ] Integración de un Gestor de Secretos Enterprise (HashiCorp Vault / Infisical) para proteger las API Keys.
- [ ] Implementación de Cyber Deception (Honeytokens) vinculados al SOAR.

---
*Nota: El código fuente se publicará de forma progresiva a medida que los módulos superen la fase de pruebas y se implementen medidas de seguridad para los secretos de la aplicación.*

📫 **Conecta conmigo en LinkedIn:** (https://www.linkedin.com/in/francisco-jose-alpuente-santos-/)