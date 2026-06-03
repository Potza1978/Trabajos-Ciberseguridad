🛡️ Detección de Amenazas con Sysmon y Evaluación de Hardening (SCA) en Windows📋 Descripción del ProyectoEste módulo documenta la simulación de amenazas avanzadas y la 
auditoría de configuraciones en un activo crítico (Windows_Lab) Utilizando Wazuh (SIEM/XDR) integrado con Microsoft Windows Sysmon. 
El foco principal es la detección en tiempo real del abuso de binarios legítimos del sistema operativo (técnicas Living off the Land) y la 
evaluación del nivel de blindaje del endpoint bajo estándares de seguridad globales.⚙️ Componentes y Orígenes de TelemetríaLa recolección de eventos avanzados se realiza, 
cruzando canales especializados del endpoint:Canal de Detección Activa: Microsoft-Windows-Sysmon/OperationalIdentificador 
Clave: Sysmon Event ID 11 (FileCreated)Módulo de Auditoría Pasiva: Módulo SCA (Security Configuration Assessment) de Wazuh.

🔍 Análisis Forense del Incidente (Caso de Uso: Abuso de PowerShell)Durante el ejercicio de monitorización, el motor de correlación de Wazuh detectó una actividad de máxima prioridad: 
Una alerta de Nivel 15 (ID: 92213).Campo del SIEMValor Registrado en el LogSignificado Operativo (Forense)Proceso Origenpowershell.exe (PID: 14588)Abuso de herramientas de 
administración nativas para evadir controles.Cuenta de UsuarioDESKTOP-10UHGTL\UsuarioContexto de identidad bajo el cual se ejecutó el comando.
Archivo Creado__PSScriptPolicyTest_ftbemaeq.5y4.ps1Payload/Script volcado directamente en disco duro.Ruta del DropperAppData\Local\Temp\Directorio de alta volatilidad, 
comúnmente explotado por malware.

📊 Cobertura Táctica (Mapeo MITRE ATT&CK)El comportamiento del binario fue clasificado automáticamente por el SIEM bajo el marco de MITRE, 
identificando los siguientes vectores:Táctica: Command and Control (TA0011)Técnica: Ingress Tool Transfer (T1105)Adicionalmente, 
se correlacionaron eventos de Nivel 9 (Rule 92205) relativos a la creación de archivos en directorios raíz y alertas de borrado masivo de claves del Registro (Event IDs 597 y 751), 
patrones típicos de una fase de Evasión de Defensas.

📊 Auditoría de Configuración de Seguridad (CIS Benchmark)Para analizar por qué el endpoint permitió este tipo de ejecuciones anómalas, 
se procesó una auditoría basada en la norma CIS Microsoft Windows 11 Enterprise Benchmark v1.0.0:Métricas de Cumplimiento (Score): 31% de éxito general (122 checks superados / 264 fallidos).
Deficiencias Críticas de Configuración Detectadas:Directivas de Contraseñas (ID 2600 / 2603): Ausencia de historial de claves y longitud mínima inferior a 14 caracteres.
Umbral de Bloqueo (ID 2606 / 2607): Cuenta vulnerable a fuerza bruta debido a la falta de restricciones ante intentos fallidos de autenticación.Estado de Cuentas (ID 2609): 
La cuenta predecible de Administrador local integrada permanece activa en el sistema.📸 Evidencias de LaboratorioPanel de Visualización del Incidente Crítico 
(Filtro PowerShell)Desglose Forense del Log de Sysmon (Nivel 15)Escaneo General del Módulo SCA (CIS Benchmark)Inventario de Directivas de Cuentas,
FallidasConfiguración de Políticas de RestricciónDetalle de Eventos de Evasión (ID 597/751)Análisis del Payload detectado en AppDataDetalle de métricas de cumplimiento 
(SCA)Visualización de Alertas de Nivel 9 (Evasión de Defensas)Resumen de Seguridad Post-Laboratorio

📈 Conclusiones y Plan de RemediaciónEl laboratorio demuestra que disponer únicamente de monitorización reactiva es insuficiente si las bases del sistema operativo no están bien protegidas. 
Para mitigar los riesgos evidenciados por las alertas de PowerShell, se prescribe la implementación urgente de las siguientes contramedidas:Políticas de Restricción de Software: 
Configurar AppLocker para bloquear la ejecución de scripts interactivos en rutas de usuario (\Temp).Hardening de Cuentas: Aplicar un umbral de bloqueo de cuentas de un máximo de 5 intentos y 
deshabilitar el usuario Administrador local mediante Directivas de Grupo (GPO).
