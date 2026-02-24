# ☁️ Día 3: Resolución Exchange Online - Cliente Oualap (23/02/2026)

## 📝 Descripción de la Petición
- El usuario solicitaba 2 cuentas adicionales y quería que todo el correo de esas cuentas llegara a su bandeja de entrada principal.

## ❌ El Problema (Lo que no hay que hacer)
- Se crearon inicialmente como **Alias** del correo personal de trabajo. Esto generó problemas de enrutamiento y gestión al ser configurados previamente así.

## ✅ La Solución (Procedimiento Correcto)
1. **Limpieza**: Borrar los alias incorrectos.
2. **Creación**: Crear **Buzones Compartidos** (Shared Mailboxes) nuevos con los nombres solicitados en los dominios correspondientes.
   - *Ruta*: Centro de administración Exchange -> Destinatarios -> Buzones.
3. **PowerShell**: Entrar por PowerShell de Exchange Online para forzar comandos y cambios de nombres si la interfaz web se atasca.
4. **Permisos y Enrutamiento**:
   - Quitar permisos de Lectura y Administración (Full Access) si no queremos que el buzón aparezca en el Outlook.
   - Configurar un **Reenvío (Forwarding)** desde las opciones de Administración de Buzones apuntando al correo original del usuario.
5. **Verificación**: Contactar al usuario vía AnyDesk, pedirle que haga una prueba de envío/recepción y comprobar que todo funciona.

## 💻 Script PowerShell: De Alias a Buzón Compartido con Reenvío

**Requisito previo:** Estar conectado a Exchange Online (`Connect-ExchangeOnline`).
**Variables del caso:** - Usuario principal: `usuario@empresa.com`
- Alias a convertir: `info@empresa.com`

```powershell
# 1. Quitamos el alias problemático de la cuenta principal
Set-Mailbox -Identity "usuario@empresa.com" -EmailAddresses @{Remove="info@empresa.com"}

# 2. Creamos el Buzón Compartido nuevo directamente
New-Mailbox -Shared -Name "Info Empresa" -PrimarySmtpAddress "info@empresa.com"

# 3. Configuramos el reenvío hacia el usuario principal y NO guardamos copia (para no llenar los 50GB tontamente)
Set-Mailbox -Identity "info@empresa.com" -ForwardingSmtpAddress "usuario@empresa.com" -DeliverToMailboxAndForward $false

# 4. (Opcional pero recomendado) Le damos permiso para ENVIAR COMO ese buzón, por si tiene que responder
Add-RecipientPermission -Identity "info@empresa.com" -Trustee "usuario@empresa.com" -AccessRights SendAs -Confirm:$false

Y ahora, la radiografía Senior de este script para que entiendas **por qué** lo hacemos así en el MSP:

### 🔹 1. Qué es esto realmente en un entorno MSP
Esto es **eficiencia y rentabilidad**. En un MSP el tiempo es dinero. Si cobras una tarifa plana al cliente, todo el tiempo que ahorres resolviendo incidencias es beneficio puro para tu empresa. Además, los comandos de PowerShell se comunican directamente con el *backend* de Microsoft; no sufren los típicos cuelgues, botones grises o tiempos de carga de la interfaz web.

### 🔹 2. Dónde lo voy a tocar en el día a día
* **Onboarding/Offboarding:** Cuando entra un empleado nuevo o se va uno viejo y hay que reestructurar quién recibe los correos de un departamento.
* **Arreglando desastres heredados:** Cuando cogéis un cliente nuevo que venía de otro informático que le configuró todo mal (como el caso de meter correos genéricos como alias de un usuario).

### 🔹 3. Incidencias típicas relacionadas
* **"Error: The proxy address is already being used"**: Esto pasa si intentas crear el buzón compartido (paso 2) ANTES de que Microsoft haya procesado que has borrado el alias (paso 1).
* **El usuario se queja de que le salen buzones que no quiere ver:** Tu apunte decía "Eliminamos los permisos de lectura". En la web, cuando das permisos totales, el buzón le aparece automáticamente en el Outlook al usuario (AutoMapping). Por PowerShell, al no darle permiso de lectura explícito o al controlarlo por código, te evitas este problema.

### 🔹 4. Cómo lo diagnostica un técnico bueno
Un técnico N2/N3 confía en PowerShell por encima de lo que dice el portal web. Si la web falla, el técnico bueno lanza un `Get-Mailbox -Identity "usuario@empresa.com" | Select-Object -ExpandProperty EmailAddresses` para ver *realmente* qué direcciones tiene pegadas ese buzón por debajo. La consola no miente.

### 🔹 5. Qué errores comete un técnico junior
* **La impaciencia gráfica:** Hacer el cambio en la web, ver que no funciona, volver a tocar, borrar, volver a crear... Al final corrompe el objeto en Entra ID/Exchange. En PowerShell, lanzas el comando y sabes que está hecho, solo hay que esperar la replicación normal.
* **Dejar copias innecesarias:** Un junior configura el reenvío pero deja marcada la opción de "Guardar una copia de los mensajes reenviados". Resultado: el buzón compartido se llena de spam y correos inútiles con los años, llega a 50GB, y deja de recibir correo. El comando `-DeliverToMailboxAndForward $false` que te he puesto arriba evita esto.

### 🔹 6. Cómo subir al siguiente nivel en esta área
🔴 **[ESTRATÉGICO Y CLAVE PARA N3]** 🔴
El siguiente nivel es coger esos 4 comandos que te he pasado y convertirlos en un **Script Parametrizado** (`.ps1`). 

Un técnico N3 crea un script donde al ejecutarlo, la consola simplemente te pregunte:
`"Introduce el correo del usuario:"`
`"Introduce el nombre del nuevo buzón compartido:"`
Y el script haga todo el proceso automáticamente, con validaciones de errores por si te equivocas al teclear. Si consigues hacer herramientas así para que las usen los técnicos N1 de tu empresa, tu jefe te va a mirar con muy buenos ojos.

¿Has instalado ya el módulo de `ExchangeOnlineManagement` en tu portátil del trabajo o prefieres que te indique cuál es la forma correcta (y segura) de prepararte el entorno PowerShell para conectar a los clientes del MSP?