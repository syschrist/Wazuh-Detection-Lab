# 🛡️ Laboratorio SOC: Implementación de Wazuh SIEM/XDR

Este repositorio contiene la documentación detallada de un entorno de monitorización y respuesta ante incidentes. El objetivo fue securizar un endpoint mediante el despliegue de **Wazuh**, integrando análisis de integridad de archivos y detección de malware mediante inteligencia externa.

## 📊 Arquitectura y Recursos
El laboratorio se sustenta sobre una arquitectura de cliente-servidor virtualizada.
- **Hipervisor:** Oracle VirtualBox
- **Sistemas:** Ubuntu Server (Manager), Ubuntu Desktop (Victim) y Kali Linux (Attacker).

## ⚙️ Configuración del Sistema
La lógica del SIEM reside en el archivo `ossec.conf`, donde se definieron las reglas de detección y los comandos de respuesta activa.

![Configuración ossec.conf](screenshots/ossec.conf.png)

## 🛡️ Capacidades de Detección

### 1. Monitorización de Integridad de Archivos (FIM)
Se configuró el módulo `syscheck` para detectar adiciones y modificaciones en rutas críticas.
- **Prueba realizada:** Modificación del archivo `/etc/shadow` y creación de `test_fim.txt`.
- **Resultado:** Identificación inmediata en el panel de eventos de Wazuh.

![Eventos de FIM](screenshots/FIM.png)

### 2. Detección de Malware (Integración VirusTotal)
Se implementó una automatización que envía los hashes de archivos nuevos a la API de VirusTotal.
- **Infección simulada:** Descarga del archivo malicioso EICAR mediante `curl`.
- **Veredicto:** El sistema disparó una alerta crítica (Nivel 12) al confirmar la amenaza con 65 motores antivirus.

![Descarga de Malware](screenshots/VirusTotal_Curl_File.png)
![Alerta Crítica VirusTotal](screenshots/VirusTotal_Dashboard_W.png)

## ⚡ Respuesta Activa ante Ataques (Pentesting)
Para validar la resiliencia del sistema, se ejecutó un ataque de fuerza bruta por SSH desde Kali Linux.

- **Ataque:** Uso de Hydra para intentar vulnerar el acceso root.
- **Detección:** Wazuh identificó el ataque de fuerza bruta en tiempo real.
- **Acción:** El servidor ejecutó el comando `host-deny`, bloqueando la IP del atacante.

![Ataque SSH y Respuesta Activa](screenshots/pentesting_active-response.png)
![Conexión rechazada por el servidor](screenshots/ssh-refused.png)

## 🏁 Conclusión
Este despliegue demuestra la capacidad de **Wazuh** para no solo alertar, sino actuar de forma autónoma ante amenazas, reduciendo drásticamente el tiempo de respuesta ante incidentes (MTTR).

---
**Christ** | *Estudiante de Montaje y Mantenimiento de Instalaciones*
