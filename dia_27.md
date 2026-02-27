# 📅 Día 6: Auditoría de Firewall Legacy y Alta Disponibilidad - Cliente LCC (27/02/2026)

## 🏢 Contexto del Cliente y Entorno
- **Cliente:** LCC (Empresa multinacional, entorno crítico de producción 24/7).
- **Dispositivo Auditado:** Firewall Sophos (Identificado como versión *legacy* **Sophos UTM 9**, previo a SFOS/XGS, detectado a través de los menús de Exportación/Backup).
- **Misión:** Realizar un mapeo y documentación de interfaces ("As-Built Documentation") en formato Excel sin alterar la configuración actual (*Read-Only Mindset*).

## 🔗 Redundancia y Alta Disponibilidad (HA)
- **Modo HA Activo-Pasivo:** El cliente cuenta con dos firewalls físicos idénticos unidos por un cable cruzado en un puerto dedicado (Puerto HA). 
  - **Máster (Activo):** Gestiona el tráfico principal a través de una línea FTTH de **Orange**.
  - **Esclavo (Pasivo):** Se mantiene a la espera con una línea FTTH de **Vodafone**.
  - *Mecánica:* Si la línea de Orange o el firewall Máster caen, el Esclavo asume el control de la red instantáneamente a través de Vodafone para evitar cortes en la producción.

## 🗺️ Mapeo de Redes y Servicios
- **Interfaces WAN y LAN:**
  - Las conexiones a Internet (WAN) tienen sus propias puertas de enlace hacia los routers de las operadoras.
  - El firewall actúa como **Puerta de Enlace (Gateway)** para las redes internas (ej. VLAN 125 para LCC, VLAN 249 para Tech Mahindra).
- **Servicio DHCP Offloaded:** Se detectó que el firewall no reparte IPs a la LAN. Este servicio está delegado a **dos Controladores de Dominio** (Windows Server) internos (Primario y Secundario).
- **Anomalías detectadas:** Se documentó un grupo LAG (Link Aggregation) configurado únicamente por un puerto físico (Port 4), mantenido así por ser infraestructura heredada.

## 🛡️ Auditoría de Reglas de Firewall y VPN
Se aplicó ingeniería inversa a la configuración heredada para documentar las reglas clave:
- **Regla 37:** Permite la salida a Internet a las redes de LCC y Tech Mahindra limitando servicios específicos (DNS, Mail, Transferencia de ficheros).
- **Bloqueo GeoIP:** Reglas restrictivas que bloquean todo el tráfico entrante proveniente de fuera de Europa (países marcados en "Off" como excepciones).
- **Túneles IPsec:** Identificadas conexiones VPN críticas hacia la sede de Sevilla, servicios directos de Orange y el CPD principal.

## 🤖 Técnicas de Extracción de Datos
- **Método Seguro de Exportación:** Al tratarse de un entorno *legacy* sin soporte nativo para exportación XML limpia, se utilizó la copia de tablas HTML (Copy-Paste con coincidencia de formato en Excel) desde la interfaz `Interfaces & Routing > Interfaces`.
- **Automatización con IA CLI:** Uso de **Claude Code** en consola local para la lectura de capturas de pantalla de la configuración y generación automática de archivos `.csv` delimitados por punto y coma (`;`), reduciendo el error humano en el volcado de datos.