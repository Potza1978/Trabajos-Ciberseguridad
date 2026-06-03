# 🛡️ Event ID de Windows Sysmon: Detección y Análisis

## 📋 Descripción del Proyecto
Este módulo documenta la simulación de amenazas avanzadas y la auditoría de configuraciones en un activo crítico (`Windows_Lab`) utilizando **Wazuh (SIEM/XDR)** integrado con 
**Microsoft Windows Sysmon**. El objetivo principal es la detección en tiempo real del abuso de binarios legítimos del sistema operativo (*Living off the Land*) y la 
evaluación del nivel de blindaje del endpoint bajo estándares de seguridad globales.

---

## ⚙️ Componentes y Orígenes de Telemetría
La recolección de eventos avanzados se realiza cruzando canales especializados del endpoint:
* **Canal de Detección Activa**: `Microsoft-Windows-Sysmon/Operational`.
* **Identificador Clave**: Sysmon Event ID 11 (`FileCreated`) y Event ID 1 (`ProcessCreation`).
* **Módulo de Auditoría Pasiva**: Módulo SCA (*Security Configuration Assessment*) de Wazuh.

---

## 🔍 Análisis Forense del Incidente (Caso de Uso: Abuso de PowerShell)
Durante el ejercicio de monitorización, el motor de correlación de Wazuh detectó una actividad de máxima prioridad: una alerta de **Nivel 15 (ID: 92213)**.

| Campo del SIEM | Valor Registrado | Significado Operativo (Forense) |
| :--- | :--- | :--- |
| **Proceso Origen** | `powershell.exe` (PID: 14588) | Abuso de herramientas nativas para evadir controles. |
| **Cuenta de Usuario** | `DESKTOP-10UHGTL\Usuario` | Contexto de identidad bajo el cual se ejecutó. |
| **Archivo Creado** | `__PSScriptPolicyTest...ps1` | Payload/Script volcado directamente en disco. |
| **Ruta del Dropper** | `AppData\Local\Temp\` | Directorio de alta volatilidad explotado por malware. |

---

## 📊 Cobertura Táctica (Mapeo MITRE ATT&CK)
El comportamiento del binario fue clasificado automáticamente por el SIEM bajo el marco de MITRE, identificando los siguientes vectores:
* **Táctica**: Command and Control (TA0011).
* **Técnica**: Ingress Tool Transfer (T1105).

Adicionalmente, se correlacionaron eventos de **Nivel 9 (Rule 92205)** relativos a la creación de archivos en directorios raíz y alertas de borrado masivo de claves del Registro 
(Event IDs 597 y 751), patrones típicos de una fase de Evasión de Defensas.

---

## 📊 Auditoría de Configuración de Seguridad (CIS Benchmark)
Se procesó una auditoría basada en la norma **CIS Microsoft Windows 11 Enterprise Benchmark v1.0.0** para evaluar el endpoint:
* **Métricas de Cumplimiento (Score)**: 31% de éxito general (122 checks superados / 264 fallidos).
* **Deficiencias Críticas**:
    * **Directivas de Contraseñas**: Ausencia de historial de claves y longitud mínima inadecuada.
    * **Umbral de Bloqueo**: Vulnerable a ataques de fuerza bruta.
    * **Estado de Cuentas**: Usuario Administrador local integrado permanece activo.

---

## 📈 Conclusiones y Plan de Remediación
El laboratorio demuestra que la monitorización reactiva es insuficiente si las bases del sistema no están protegidas.
* **Mitigación**: Implementar **AppLocker** para bloquear scripts en rutas de usuario y aplicar GPOs para deshabilitar el Administrador local,
* limitando los intentos de inicio de sesión a un máximo de 5.
