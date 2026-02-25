# 📚 Cheat Sheet Avanzado: Redes y Firewalls en Entorno MSP

> Guía estructurada para entender redes como un técnico profesional (N1 → N3).
> Aplicable a Sophos, Fortinet, SonicWall, Cisco y cualquier firewall empresarial.

---

# 🌍 1️⃣ Fundamentos: Cómo Funciona Realmente la Red

## 🔹 WAN (Internet – "La Calle")

* Es la red externa.
* Es pública, hostil y llena de bots automatizados.
* Todo tráfico entrante debe estar bloqueado por defecto.

📌 Físicamente:

* Cable del router (Movistar/Vodafone)
* Normalmente conectado al Port 2 del firewall

---

## 🔹 LAN (Red Interna – "La Oficina")

* Es la red privada del cliente.
* Aquí viven PCs, impresoras y servidores.

📌 Físicamente:

* Sale normalmente por Port 1 hacia el switch principal.

---

# 🏷️ 2️⃣ Servicios Base Esenciales

## 🔹 DHCP (El Repartidor de Matrículas)

Asigna automáticamente:

* Dirección IP
* Máscara
* Puerta de enlace
* DNS

⚠️ Sin DHCP:

* Tendrías que configurar IP manualmente en cada equipo.

🚨 Incidencia típica MSP:

* Alguien conecta un router doméstico.
* Se genera un "Rogue DHCP".
* Dos dispositivos reparten IPs.
* Media oficina se queda sin red.

---

## 🔹 DNS (El Listín Telefónico)

Traduce nombres a IPs.

Ejemplo:

* google.com → 142.250.x.x

🛠 Diagnóstico clásico:

* Si 8.8.8.8 responde pero google.com no carga → problema de DNS.

---

# 🛡️ 3️⃣ Firewall – Cómo Piensa Realmente

Un firewall hace solo 3 preguntas:

1. ¿De dónde viene y a dónde va? (WAN / LAN)
2. ¿Hay una regla que lo permita?
3. ¿Necesita NAT?

## 🔹 Principio Base

* Default Deny (Denegación implícita)
* Si no está permitido → se bloquea (DROP)
* Las reglas se leen de ARRIBA hacia ABAJO

## 🔹 Regla Básica Universal

Permitir:

Origen: LAN
Destino: WAN
Servicio: ANY

---

# 🎭 4️⃣ NAT – El Disfraz

Internet no entiende IPs privadas (192.168.x.x).

## 🔹 SNAT / MASQ (Salida a Internet)

* Disfraza toda la LAN con la IP pública.
* Obligatorio para navegar.

Sin SNAT:

* El tráfico sale
* Pero no sabe cómo volver

---

## 🔹 DNAT (Port Forwarding)

Permite que alguien desde Internet entre a un servidor interno.

Ejemplo:
WAN:443 → LAN 192.168.1.50:443

⚠️ Alto riesgo si no se hace correctamente.

---

# 🚪 5️⃣ Puertos – Error Clásico de Junior

## 🔹 Puertos Físicos

* Port 1, Port 2, SFP
* Son agujeros del dispositivo

## 🔹 Puertos Lógicos (TCP/UDP)

Son puertas virtuales (1–65535).

Puertos comunes:

* 80 / 443 → Web
* 445 → SMB (Escáner a carpeta)
* 3389 → RDP 🚨 Nunca exponer directamente
* 1433 → SQL Server
* 123 UDP → NTP

---

# 🧠 6️⃣ Cómo Se Vive Esto en un MSP

## 🔹 Lo que realmente significa profesionalmente

Es tu "Piedra Rosetta".
Cuando un proveedor dice:

"Necesito un DNAT al puerto TCP 8000 hacia 192.168.1.200"

Tú lo traduces en configuración concreta en menos de 1 minuto.

---

# 🛠️ 7️⃣ Incidencias Reales del Día a Día

## 🔹 Doble NAT (El Enemigo Silencioso)

Router operadora hace NAT
+
Firewall hace NAT
=================

Problemas en:

* VPNs IPsec
* VoIP

✅ Solución profesional:
Poner router de operadora en modo Bridge.

---

## 🔹 "Tengo WiFi pero no Internet"

Posibles causas:

* DHCP no asigna IP
* DNS no resuelve
* Falta SNAT

---

## 🔹 Escáner no guarda en carpeta

* Puerto 445 bloqueado
* Regla incorrecta

---

# 🔎 8️⃣ Cómo Diagnostica un Técnico Senior

Nunca dispara a ciegas.

Divide mentalmente por capas OSI:

1️⃣ ¿Hay enlace físico?
2️⃣ ¿Tengo IP válida?
3️⃣ ¿Llego al firewall?
4️⃣ ¿El firewall hace NAT?
5️⃣ ¿DNS resuelve?

Herramientas clave:

* ping
* tracert 8.8.8.8

Si el paquete llega al firewall y muere → falta Regla o NAT.

---

# ❌ 9️⃣ Errores Típicos de Junior

## 🔴 Regla ANY-ANY

Permitir todo desde cualquier origen a cualquier destino.
Funciona… pero destruye la seguridad.

---

## 🔴 Abrir RDP (3389) a Internet

En 24–48h:

* Bot escanea IP pública
* Ataque fuerza bruta
* Ransomware

Solución correcta:
VPN (Sophos Connect u otra solución segura).

---

# 🚀 🔟 Cómo Subir a Nivel N3

## 🔹 Dejar de "abrir puertos"

Empieza a pensar en:

* Arquitectura
* Segmentación
* Políticas

---

## 🔴 Nivel Estratégico: WAF

En vez de DNAT simple:

Un N3 usa WAF (Web Application Firewall).

El WAF:

* Inspecciona tráfico HTTP/HTTPS
* Bloquea SQL Injection
* Bloquea XSS
* Protege antes de que llegue al servidor

Eso es ciberseguridad real.

---

# 🎯 Resumen Final

Si entiendes:

WAN + LAN
DHCP + DNS
Firewall + Reglas
SNAT + DNAT
Puertos lógicos
Diagnóstico por capas

Puedes trabajar en cualquier MSP.

El concepto es universal.
El fabricante cambia.
La lógica no.
-----------------------------------------------

# 📚 Cheat Sheet: Conceptos Core de Redes y Firewalls (MSP Edition)

> **Contexto:** Esta guía rápida traduce los conceptos académicos de redes a la realidad diaria de la administración de sistemas e infraestructura en un Managed Service Provider (MSP). Aplica a Sophos, Fortinet, SonicWall y cualquier firewall NGFW.

## 🌍 1. Zonas de Red: WAN vs LAN
* **WAN (Wide Area Network - "La Calle"):** Es la conexión a Internet. Es un entorno hostil y público. 
  * *Físicamente:* Suele conectarse al **Port 2** del firewall.
  * *Seguridad:* Todo el tráfico de entrada desde la WAN debe estar bloqueado por defecto.
* **LAN (Local Area Network - "La Oficina"):** Es la red interna y privada del cliente (PCs, impresoras, servidores).
  * *Físicamente:* Suele salir desde el **Port 1** hacia el switch principal.
  * *Seguridad:* Se confía en esta red, pero siempre controlando qué dispositivos tienen salida.

## 🏷️ 2. Servicios Base: DHCP y DNS
* **DHCP (Dynamic Host Configuration Protocol):** Es el "repartidor de matrículas". Asigna automáticamente direcciones IP, máscara de subred y puerta de enlace a los dispositivos que se conectan a la LAN.
  * *Avería típica MSP:* Un empleado conecta un router de su casa a la red de la oficina, creando un "Rogue DHCP" (dos repartidores peleándose). Media oficina se queda sin red.
* **DNS (Domain Name System):** El "listín telefónico". Traduce nombres (ej. `google.com`) a direcciones IP. Si el DNS falla, hay Internet (el ping a 8.8.8.8 funciona), pero las páginas web no cargan.

## 🛡️ 3. Reglas de Firewall (El Portero)
Un firewall funciona con el principio de **Denegación Implícita (Default Deny)**. Si no hay una regla que permita explícitamente el tráfico, el paquete se destruye (*Drop*).
* Las reglas se leen de **ARRIBA hacia ABAJO**. La primera regla que coincide con el tráfico, se aplica.
* *Regla básica de salida:* Permitir Origen `LAN` hacia Destino `WAN`.

## 🎭 4. NAT (Network Address Translation)
Internet no puede enrutar IPs privadas (ej. `192.168.1.50`). El NAT es el "disfraz" que usan las IPs locales para salir a la calle.
* **SNAT / MASQ (Source NAT / Masquerade):** Oculta toda tu LAN detrás de la IP pública del router/firewall. Es obligatorio para tener navegación a Internet.
* **DNAT / Port Forwarding (Destination NAT):** Es el proceso inverso. Permite que alguien desde Internet (WAN) atraviese el firewall para llegar a un servidor interno (LAN). *Peligro: Usar con extrema precaución.*

## 🚪 5. Puertos: Físicos vs Lógicos
No confundir el agujero físico del aparato con el canal de comunicación del software.
* **Puertos Físicos (Interfaces):** Port 1, Port 2, SFP... Son los conectores de hardware.
* **Puertos Lógicos (TCP/UDP):** Son "puertas" virtuales (del 1 al 65535). Indican qué servicio se está usando.
  * `80 / 443`: Navegación Web (HTTP / HTTPS).
  * `445`: Compartición de archivos SMB (Escáner a carpeta).
  * `3389`: Escritorio Remoto (RDP). **🚨 NUNCA exponer este puerto directamente a la WAN.**