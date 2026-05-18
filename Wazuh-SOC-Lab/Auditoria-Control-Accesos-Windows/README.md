## 📋 Descripción del Proyecto
Este módulo documenta la monitorización y el análisis forense de logs de control de acceso en entornos corporativos utilizando **Wazuh SIEM**. 
El objetivo es auditar y verificar el ciclo de vida de las sesiones de usuario en un endpoint activo (`Windows_Lab`), 
astreando la telemetría de los eventos de cierre de sesión y bloqueos de estaciones de trabajo para garantizar el cumplimiento normativo.

---

## ⚙️ Componentes y Arquitectura de Logs
La recolección de eventos se realiza a través del agente de Wazuh desplegado en la máquina objetivo, 
enviando los logs de seguridad de Windows de forma centralizada al módulo de gestión.
* **Canal de Eventos:** `Security`
* **Identificador Clave:** `Event ID 4634` (An account was logged off)
* **Tipo de Inicio de Sesión Auditado:** `Logon Type 7` (Bloqueo/Desbloqueo de pantalla / Screen Saver)

---

## 🔍 Análisis Forense de la Alerta (Caso de Uso)

El motor de reglas de Wazuh procesó y normalizó un evento de nivel de alerta 3 correlacionado con políticas de seguridad específicas:

| Campo del SIEM | Valor Registrado | Significado Técnico |
| :--- | :--- | :--- |
| **Agent Name** | `Windows_Lab` | Endpoint monitorizado de la infraestructura. |
| **Event ID** | `4634` | Notificación nativa de Windows: Destrucción de sesión. |
| **Logon Type** | `7` | La sesión finaliza o se suspende por el bloqueo de la estación de trabajo (`Win + L`). |
| **TargetLogonId** | `0x9678e8` | Identificador alfanumérico único para realizar correlación de tiempo con el Event ID 4624. |
| **Rule Description** | `Windows User Logoff.` | Regla interna de Wazuh (ID: 60137) encargada de clasificar el evento. |

### 📊 Mapeo de Cumplimiento Regulatorio (Compliance)
La correcta ingesta de este log permite automatizar las auditorías de cumplimiento exigidas por los estándares internacionales presentes en el evento:
* **GDPR / RGPD:** Cumplimiento de la directiva **IV_32.2** (Seguridad en el tratamiento de datos y control de accesos de usuarios).
* **NIST SP 800-53:** Control de accesos e identificación y autenticación (**AC.7, AU.14**).
* **PCI-DSS:** Requisito **10.2.5** (Registro y trazabilidad de todos los accesos e intentos de identificación de usuarios).

---

## 📸 Evidencias de Laboratorio

### 1. Panel de Control Operativo (Evolución de Alertas)
![Wazuh Dashboard](1_dashboard.png)

### 2. Desglose Forense del Evento Estructurado (Vista de Tabla)
![Desglose del Evento](2_event_table.png)

### 3. Enriquecimiento y Mapeo Normativo (Campos del SIEM)
![Mapeo Compliance](3_compliance_fields.png)

---

## 📈 Conclusiones Operativas
El análisis automatizado del **Event ID 4634** demuestra que la infraestructura cuenta con visibilidad total sobre la actividad de los usuarios. 
l registrar con precisión el código único `TargetLogonId`, el SOC tiene la capacidad de mapear líneas temporales completas de actividad, 
impidiendo el repudio de acciones y asegurando que las estaciones de trabajo huérfanas o bloqueadas queden registradas debidamente frente a auditorías externas.
