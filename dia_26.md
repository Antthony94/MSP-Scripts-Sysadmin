### 1. Tareas por Cliente y Proyecto
* **Empresa Overlap:**
  * Instalación de herramientas de recortes por medio de AnyDesk [1]. 
  * *Nota técnica:* Si no funciona la herramienta de recortes nativa de Windows, instalamos `lightshot` [1].
  * Gestioné el laboratorio virtual para VMware y Sophos [1].
* **Delegación Portugal:**
  * Alta de un nuevo usuario en el servidor [1].
  * Añadimos al nuevo usuario a la cuenta compartida [1].
  * En un equipo con 2 usuarios, se procedió a cambiar el idioma a portugués [1].
* **Empresa Bacci:**
  * Configuración para un nuevo usuario en remoto (Escáner e Impresora) [2].
  * *Pendiente:* Tarea o archivo "TxT. Bacci" (Pendiente Javi) [2].
* **Empresa Negocenter (16:30, tras la comida):**
  * Usamos el programa *Advance IP Scan* para rastrear la red [2].
  * Ejecución del comando `tracert` para "saber por dónde sale" la conexión [2].

### 2. Herramientas de Uso Diario
* **Gestión y Comunicación:** Jira (como gestionador de tickets) y Google Teams [1].
* **Seguridad y Credenciales:** Bitwarden (BitW) para almacenar y buscar accesos [1, 3].
* **Administración del Sistema:** Consola MMC para la creación y gestión de usuarios locales [3].

---

## Procedimiento Técnico: Configuración de "Escáner Completo" [3]

Protocolo paso a paso para configurar un escáner en red para que envíe documentos a un PC local [3]:

**Preparación en el equipo local:**
1. Crear una carpeta en la raíz del disco `C:\` llamada "Escaner" [3].
2. Dar permisos a la carpeta [3].
3. Compartir la carpeta en la red [3].
4. Usar la consola **MMC** para crear un usuario local específico llamado "Escaner" [3].

**Configuración en la interfaz web del escáner:**
5. Acceder a la interfaz del escáner por medio de su IP (buscando el acceso en Bitwarden) [3].
6. Iniciar sesión y acceder como administrador (`admin`) [3].
7. Ir al apartado de libreta de direcciones [3].
8. Poner la ruta de red utilizando el nombre del equipo y el nombre de la carpeta compartida [3].
9. Dar la ruta en la web del escáner introduciendo el usuario y la contraseña que fueron "previamente metidos en MMC" [3].