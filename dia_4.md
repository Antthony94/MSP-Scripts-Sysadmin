# 📅 Día 4: Ciberseguridad Perimetral y Endpoint (24/02/2026)

## 🎓 Logros y Certificaciones
Hoy he oficializado mis conocimientos en el Stack de Seguridad del MSP obteniendo dos certificaciones clave del fabricante:
- **Sophos Firewall Certified Engineer v22.0 (ET80)**
- **Sophos Endpoint Certified Engineer v6.0 (ET15)**

## 🛡️ Despliegue Práctico: Sophos XGS 108
Aplicación inmediata de la teoría documentando y configurando un firewall **Sophos XGS 108**. 
- *Contexto MSP:* Este equipo es la frontera principal de seguridad para Pymes, gestionando IPS, filtrado web y VPNs.
- *Gestión:* Interiorizado el uso del "Log Viewer" y la inspección de paquetes (DPI) para resolver bloqueos de tráfico en lugar de usar reglas permisivas (ANY-ANY).

## 🖨️ Profundización: Protocolo SMB (Escáner a Carpeta)
Resolución avanzada de configuración de impresoras por IP (ej. `172.xx.xx.xx`).
- **Problema de Privilegios:** Comprobado que la configuración de la Libreta de Direcciones y el mapeo de carpetas en Windows requiere estrictamente permisos de Administrador Local o de Dominio.
- **Troubleshooting:** Uso de la ruta UNC (`\\IP\Carpeta` o `\\Hostname\Carpeta`) para evitar errores de resolución, y aplicación del principio de menor privilegio creando un script en PowerShell para desplegar el usuario "Escaner" de forma segura y automatizada.