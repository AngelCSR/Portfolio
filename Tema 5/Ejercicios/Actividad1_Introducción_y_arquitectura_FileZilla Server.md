# Documentación
Un pequeño resumen de los conceptos clave

## 1️⃣ Conceptos clave

**FTP (File Transfer Protocol):**

* Protocolo estándar para transferencia de archivos.
* No cifra datos ni credenciales.

**FTPS (FTP Secure):**

* FTP con soporte de SSL/TLS.
* Los datos y contraseñas pueden ir cifrados.

**SFTP (SSH File Transfer Protocol):**

* Transferencia de archivos sobre SSH.
* Diferente a FTP/FTPS; solo usa un puerto (22) y todo es seguro.

---

## 2️⃣ Arquitectura cliente–servidor

* **Servidor FTP/FTPS:** Espera conexiones de clientes, gestiona usuarios y archivos.
* **Cliente FTP:** Solicita conexión, envía comandos y recibe archivos.

**Comunicación basada en dos canales:**

* **Canal de control:** Para comandos y respuestas (usuario, contraseña, listar archivos, etc.).
* **Canal de datos:** Para transferir archivos reales.

---

## 3️⃣ Puertos implicados

| Modo           | Canal | Puerto típico                    |
| -------------- | ----- | -------------------------------- |
| Control        | TCP   | 21                               |
| Datos (activo) | TCP   | Cliente elige >1023, servidor 20 |
| Datos (pasivo) | TCP   | Servidor elige un puerto >1023   |

---

## 4️⃣ Modo activo vs pasivo

| Característica           | Activo                            | Pasivo                          |
| ------------------------ | --------------------------------- | ------------------------------- |
| Inicia conexión de datos | Servidor al cliente               | Cliente al servidor             |
| Control de firewall      | Difícil (cliente recibe conexión) | Más fácil (cliente inicia todo) |
| Uso común                | Redes internas                    | Internet / NAT                  |


# Esquema del flujo de conexión FTP

## Modo Activo

| Cliente            | Servidor                             |
| ------------------ | ------------------------------------ |
| Conexión Control → | TCP 21                               |
| ← OK/Respuesta     |                                      |
| USER/PASS →        |                                      |
| ← 230 Login OK     |                                      |
| PORT 5000 →        | Cliente indica puerto local          |
| ← 200 OK           |                                      |
| RETR archivo →     | Servidor conecta al cliente TCP 5000 |
| ← Datos ↔          |                                      |
| Cerrar datos →     |                                      |

**Datos:** En modo activo, el servidor se conecta al cliente para la transferencia de datos.

---

## Modo Pasivo

| Cliente                     | Servidor                      |
| --------------------------- | ----------------------------- |
| Conexión Control →          | TCP 21                        |
| ← OK/Respuesta              |                               |
| USER/PASS →                 |                               |
| ← 230 Login OK              |                               |
| PASV →                      | Solicita puerto pasivo        |
| ← 227 192.168.x.x:5050-5055 |                               |
| Conexión Datos →            | Cliente conecta a puerto 5050 |
| ← Transferencia Datos       |                               |
| Cerrar datos →              |                               |

**Datos:** En modo pasivo, el cliente se conecta al servidor para la transferencia de datos.

---

**Nota:** El puerto de control siempre es el 21 (FTP estándar).
