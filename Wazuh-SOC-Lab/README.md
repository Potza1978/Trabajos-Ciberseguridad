# 🛡️ Despliegue de Laboratorio SOC & Monitoreo con Wazuh (SIEM/XDR)

## 📋 Descripción del Proyecto
Este proyecto documenta el diseño, despliegue y configuración de un entorno de laboratorio 
**SOC (Security Operations Center)** utilizando **Wazuh** como solución centralizada de **SIEM/XDR**. 
El objetivo principal es la centralización de logs, 
la monitorización de la seguridad operativa en entornos distribuidos y el 
análisis práctico de telemetría para la detección de incidentes y el cumplimiento normativo.

---

## 🛠️ Arquitectura e Infraestructura
El laboratorio consta de una arquitectura cliente-servidor con monitorización activa, 
sobre diferentes sistemas operativos:
* **SIEM/XDR Manager:** Servidor centralizado bajo Wazuh (`ubitor-VirtualBox`).
* **Endpoints Monitorizados:** Agentes distribuidos, incluyendo un entorno Windows de pruebas
* (`Windows_Lab` - IP `192.168.1.13`).
* **Protocolos y Orígenes:** Windows Event Logs, Syslog y auditoría de canales de seguridad corporativos.

---

## 🚀 Características y Capacidades Técnicas
* **Monitoreo de Autenticación:** Reglas específicas para el control de accesos,
* analizando de forma estricta tanto los inicios de sesión exitosos como las desviaciones y fallos.
* **Análisis Avanzado de Eventos (EventIDs):** Capacidad para desglosar la estructura de los eventos generados,
* por el sistema operativo, permitiendo identificar el comportamiento del usuario y posibles vectores de intrusión.
* **Correlación Normativa (Compliance):**
* Integración nativa con marcos de control internacionales para facilitar auditorías de seguridad en tiempo real.

---

## 🔍 Análisis de Telemetría Real (Caso de Uso)

A continuación se detalla un caso de uso real extraído de la monitorización del agente Windows, 
donde se analiza el ciclo de vida de una sesión y su implicación técnica:

### 📊 Desglose del Evento Registrado
| Campo en el SIEM | Valor Registrado | Significado y Relevancia Técnica |
| :--- | :--- | :--- |
| **Agent Name / ID** | `Windows_Lab` / `001` | Endpoint bajo monitorización activa. |
| **Agent IP** | `192.168.1.13` | Dirección IP de origen del activo. |
| **Windows EventID** | `4634` | **Windows User Logoff** (Se cerró sesión en una cuenta). |
| **Logon Type** | `7` | **Screen Unlock / Lock** (Indica el bloqueo/desbloqueo físico de la estación). |
| **Rule ID / Level** | `60137` / `Level 3` | Regla específica del motor de Wazuh para eventos de Logoff. |
| **Decoder** | `windows_eventchannel` | Decodificador nativo para el canal de seguridad de Windows. |

### ⚖️ Mapeo de Cumplimiento Regulatorio (Compliance)
Cada evento procesado por el motor de reglas se correlaciona automáticamente con estándares internacionales para garantizar la auditoría técnica:
* **GDPR / RGPD (Requisito IV_32.2):** Control estricto de accesos, integridad del tratamiento y trazabilidad de las sesiones de usuario.
* **NIST SP 800-53 (AC.7, AU.14):** Gestión de autenticación y revisión continua de los registros de auditoría de cuentas.
* **PCI-DSS (Requisito 10.2.5):** Registro obligatorio de todos los accesos, intentos de autenticación y cierres de sesión de los componentes del sistema.

---

## 📸 Evidencias del Entorno en Ejecución

### 1. Dashboard General de Eventos de Seguridad
![Wazuh Dashboard](1_wazuh_dashboard.png)

### 2. Estructura e Ingeniería del Log (Tabla y JSON)
![Log Parte 1](2_log_eventid4634.png)
![Log Parte 2](3_log_compliance.png)

---

## 📈 Conclusiones

Este laboratorio demuestra la viabilidad de centralizar eventos en un entorno corporativo simulado, 
permitiendo pasar de la teoría a la práctica mediante el triaje de alertas reales, 
el análisis de estructuras JSON de seguridad y el cumplimiento de normativas de protección de datos vigentes.
