# Análisis de Event ID y Telemetría Sysmon

📝 **Descripción del Proyecto**
Este módulo documenta la monitorización y el análisis forense de telemetría de Windows mediante **Sysmon** y **Wazuh SIEM**. El objetivo es auditar la actividad de procesos y la persistencia en un endpoint activo, rastreando eventos críticos para garantizar el cumplimiento de seguridad.

⚙️ **Componentes y Arquitectura de Logs**
La recolección de eventos se realiza a través del agente de Wazuh desplegado en la máquina objetivo, enviando los logs de forma centralizada al módulo de gestión.

* **Canal de Eventos:** Sysmon / Windows-Event-Log
* **Identificadores Clave:** Event ID 11 (File Create), Event ID 1 (Process Creation)
* **Técnicas Auditadas:** Persistencia (T1023), Evasión de defensas (T1089)

🔍 **Análisis Forense de la Alerta (Caso de Uso)**
El motor de reglas de Wazuh procesó y normalizó eventos correlacionados con políticas de seguridad específicas:

| Campo del SIEM | Valor Registrado | Significado Técnico |
| :--- | :--- | :--- |
| **Agent Name** | Windows-Fisico | Endpoint monitorizado de la infraestructura. |
| **Event ID** | 11 | Creación de archivos (.lnk) - Persistencia. |
| **Proceso** | cmd.exe | Ejecución de comandos no autorizados. |
| **Acción** | net stop | Intento de evasión de defensas. |

### 📸 Evidencias Técnicas

![Eventos de Sistema](Captura%20de%20pantalla%202026-06-02%20162212.png)
![Análisis de Logs](Captura%20de%20pantalla%202026-06-02%20162521.png)
![Visualización de Datos](Captura%20de%20pantalla%202026-06-02%20162752.png)
![Telemetría](Captura%20de%20pantalla%202026-06-02%20162903.png)
![Procesos](Captura%20de%20pantalla%202026-06-02%20163521.png)
![Detección net stop](Captura%20de%20pantalla%202026-06-02%20163953.png)
![Filtrado DQL](Captura%20de%20pantalla%202026-06-02%20164743.png)
![Mapeo T1023](Captura%20de%20pantalla%202026-06-02%20164854.png)
