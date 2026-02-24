# 🏢 Día 2: Cliente Alcalá de Henares (20/02/2026)

## 📌 Contexto de la Infraestructura
- **Virtualización**: Tienen un servidor virtual propio bajo el hipervisor **VMware ESXi**.
- **Hardware**: Hay un servidor físico en la oficina ("habitación").
- **Almacenamiento/Backups**: Tienen un RAID 1 manual. Las copias se hacen mediante una aplicación a la que nos conectamos por Splashtop para programarlas de forma manual.

## 🛠️ Herramientas Detectadas
- **OCS Inventory**: Sistema montado sobre **Ubuntu (Linux)**. 
  - *Función*: Administrar equipos y sacar el inventario de hardware/software del cliente.

## 🚨 Incidencias / Tareas On-Site
- Actualizaciones de sistema operativo a Windows 11.
- Revisión de impresora que falla (pantalla negra).