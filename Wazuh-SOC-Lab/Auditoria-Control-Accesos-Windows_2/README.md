# 🛡️ Auditoría de Logoff y Cierre de Sesiones en Windows (EventID 4634)

## 🔍 Análisis de Telemetría Real
Desglosamos el evento de cierre de sesión capturado en tiempo real desde el módulo *Discover* en el agente monitorizado:

| Atributo en Wazuh | Valor Capturado | Significado Técnico y Relevancia Operativa |
| :--- | :--- | :--- |
| **Agent Name / ID** | `DESKTOP-10UHGTL / 003` | Endpoint Windows bajo supervisión persistente en el SOC. |
| **Source IP** | `192.168.1.13` | Dirección IP interna asignada al host evaluado. |
| **Windows EventID** | `4634` | **An explicit logoff occurred.** Cierre de sesión efectivo de la cuenta. |
| **Logon Type** | `7` | **Screen Unlock.** Desbloqueo de la estación de trabajo (salida de protector de pantalla/suspensión). |
| **Logon Process** | `User32` | Subsistema operativo encargado de la interacción y gestión de sesión interactiva. |
| **Proceso Origen** | `C:\Windows\System32\svchost.exe` | Componente del sistema que aloja el servicio de auditoría de logs. |
| **Status Code** | `%2304` | Identificador de control interno para la gestión del estado de la sesión. |

---

## 📊 Métricas del SOC y Gestión de Severidad
Volumen general de eventos y triaje de alertas reflejado en el Dashboard principal del SIEM en las últimas 24 horas de actividad:

* **Eventos Ingeridos:** `1,331` logs totales procesados por el motor de reglas de Wazuh.
* **Alertas Críticas (Level 12+):** `7` incidentes de alta prioridad bajo análisis y contención inmediata.
* **Alertas de Severidad Alta (Level 12-14):** `9` detecciones operativas en cola de triaje.
* **Balance de Autenticaciones:** `7` inicios de sesión autorizados frente a `3` anomalías/fallos de accesos bloqueados.

---

## 🗺️ Mapeo Táctico MITRE ATT&CK
La telemetría recolectada se alinea con la matriz de conocimiento táctico para identificar comportamientos maliciosos o evasivos:

* **Tácticas Detectadas:** Defense Evasion (Evadir Defensas), Command and Control (C2) e Impact.
* **Técnicas bajo Monitorización:** Auditoría estricta sobre ejecuciones de scripts en `PowerShell`, manipulación de registros del sistema (`Modify Registry`) y el uso indebido de credenciales legítimas (`Valid Accounts`).

---

## ⚖️ Marcos de Cumplimiento Normativo (Compliance)
Cada registro procesado se asocia automáticamente con estándares internacionales para auditorías técnicas:

* **GDPR / RGPD:** Control estricto de accesos y trazabilidad técnica completa del ciclo de vida de las sesiones de usuario.
* **NIST SP 800-53:** Gestión de autenticación, limitación de intentos de acceso y revisión continua de logs (AC-7, AU-14).
* **PCI-DSS:** Registro inmutable obligatorio de cierres de sesión e intentos de acceso en componentes críticos de la red (Requisito 10.2.5).

---

## 📸 Evidencias del Laboratorio en Ejecución

### 1. Ingesta de Logs e Ingeniería del Evento
![Ingeniería de Telemetría](./1.png)

### 2. Estructura de Datos y Mapeo del JSON Crudo
![Estructura JSON Forense](./2.png)

### 3. Panel General de Threat Hunting y Evolución Temporal
![Módulo Threat Hunting](./3.png)

### 4. Matriz de Cobertura Táctica (MITRE ATT&CK)
![Matriz MITRE](./4.png)

### 5. Dashboards de Control y Severidad del Framework
![Panel Severidad](./5.png)
