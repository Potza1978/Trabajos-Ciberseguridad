# 🛡️ Portafolio y Playbooks de Respuesta a Incidentes (SOC)

Repositorio centralizado de documentación técnica, procedimientos operativos estandarizados (SOPs) y playbooks de respuesta a incidentes orientados a operaciones defensivas de ciberseguridad (Blue Team / SOC).

---

## 📂 Contenido del Repositorio

El repositorio incluye la documentación completa y estructurada de los siguientes entregables técnicos:

### 1. Portafolio SOC Profesional (`SOC_Portfolio_Completo.pdf`)
* **Descripción:** Visión general de competencias técnicas, metodologías de análisis de seguridad, diseño de topologías y gestión de alertas y registros (Wazuh, Sysmon).

### 2. Playbooks de Respuesta a Incidentes
Cada playbook detalla el flujo completo de actuación bajo fases estandarizadas (Preparación, Detección, Contención, Erradicación, Recuperación y Lecciones Aprendidas), incluyendo diagramas de flujo y consultas de detección/correlación:

* **[SOC-IR-041] Incidente de Phishing (`SOC-IR-041_Completo.pdf`)**
  * *Enfoque:* Análisis de cabeceras de correo, extracción e inspección de URLs maliciosas y archivos adjuntos, aislamiento rápido de endpoints afectados y revocación de credenciales comprometidas.
* **[SOC-IR-042] Incidente de Ransomware (`SOC-IR-042_Completo.pdf`)**  
  * *Enfoque:* Contención inicial de la propagación en red, identificación de vectores de infección inicial (como RDP expuesto o credenciales robadas), aislamiento de sistemas críticos y validación de respaldos.
* **[SOC-IR-043] Incidente de Denegación de Servicio - DDoS (`SOC-IR-043_Completo.pdf`)**
  * *Enfoque:* Mitigación de saturación de ancho de banda y recursos, análisis de tráfico mediante flujos, colaboración con proveedores de mitigación/ISP y recuperación del servicio web o de infraestructura.

---

## 🛠️ Tecnologías y Estándares Aplicados
* **Monitoreo y SIEM:** Wazuh, Sysmon, correlación de logs de Windows/Linux.
* **Metodología de Respuesta:** NIST SP 800-61 / Ciclo de vida de gestión de incidentes.
* **Documentación:** Estructuración técnica orientada a auditores, analistas Tier 1/2 y equipos de ingeniería defensiva.

---
*Autor: Martin Dalla Pozza*
