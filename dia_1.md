# 🛠️ Día 1: Procedimientos Internos y Soporte N1/N2

## 🔑 Gestión de Credenciales y Accesos
- **Bitwarden**: Nuestro gestor de contraseñas principal.
  - *Procedimiento en mantenimientos*: Buscar por el nombre del cliente para sacar contraseñas de Administrador.
  - *Regla de oro web*: Iniciar sesión siempre en **modo incógnito** para evitar cruce de sesiones con cuentas personales u otros clientes.

## 📡 Herramientas de Conexión Remota
- **Splashtop**: Para conexión a servidores en background. Fundamental para pasar el "Check List" de mantenimiento de servidores.
- **AnyDesk**: Para soporte directo a usuario. *Uso típico*: Importar/exportar marcadores, o pedir al usuario que compruebe si un fix ha funcionado (ej. reenvíos de correo).

## 🖥️ Administración Local (Windows)
- **Consolas MMC y Admin. de Equipos**: Al abrir estas consolas en el PC del usuario, hay que hacerlo explícitamente **como Administrador**, pero cuidando de no perder la conexión de red/remota al elevar privilegios.
- **Seguridad**: Forzar siempre contraseñas seguras al crear/modificar usuarios.
- **Instalación SQL**: Despliegue de SQL Server en el ordenador local.

## 🖨️ Configuración Escáner a Carpeta (SMB/Red)
- **Pasos**: Acceder por IP al panel web del escáner -> Loguearse como Admin -> Ir a Libreta de Direcciones -> Configurar carpeta destino.
- **El Truco (Bulletproof)**: Crear un usuario local en Windows llamado `Escaner` dedicado solo a esto. Evita que el escáner deje de funcionar cuando el empleado cambia su contraseña de Windows.

## 💼 Workaround: Activación Local de Office
1. Abrir Word -> Archivo -> Cuenta.
2. Iniciar sesión con una cuenta de Admin que tenga licencia válida para activar el software.
3. Una vez activado, cambiar a la cuenta del usuario final.

## ⏱️ Buenas Prácticas Servidores
- Si un cliente tiene múltiples servidores, **NUNCA** programar tareas automáticas (apagados, reinicios, copias) a la misma hora. Separarlas por minutos/horas para no colapsar el hipervisor o la red.