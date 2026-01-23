# Actividad 8: Configuración de FTP seguro (FTPS)

## 1. Generación del certificado TLS

Se generó un certificado autofirmado para el servidor FTP usando OpenSSL:

```bash
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
-keyout /etc/ssl/private/vsftpd.key \
-out /etc/ssl/private/vsftpd.crt
```

Datos introducidos en el certificado:

| Campo | Valor |
|-------|-------|
| País (C) | ES |
| Provincia (ST) | Ciudad Real |
| Localidad (L) | Alcázar |
| Organización (O) | Bosco |
| Unidad organizativa (OU) | Daw2 |
| Common Name (CN) | Angel |
| Email | angel |

Se verificó con:

```bash
sudo openssl x509 -in /etc/ssl/private/vsftpd.crt -text -noout
```

---

## 2. Configuración de vsftpd para FTPS explícito

Archivo `/etc/vsftpd.conf` modificado:

```
listen=YES
listen_ipv6=NO
listen_port=2121
ssl_enable=YES
allow_anon_ssl=NO
force_local_data_ssl=YES
force_local_logins_ssl=YES
rsa_cert_file=/etc/ssl/private/vsftpd.crt
rsa_private_key_file=/etc/ssl/private/vsftpd.key
ssl_tlsv1=YES
ssl_sslv2=NO
ssl_sslv3=NO
local_enable=YES
write_enable=YES
chroot_local_user=YES
pasv_enable=YES
pasv_min_port=30000
pasv_max_port=31000
anonymous_enable=NO
```

Se reinició el servicio:

```bash
sudo systemctl restart vsftpd
```

---

## 3. Conexión con FileZilla Client (FTPS)

Configuración en FileZilla:

| Campo | Valor |
|-------|-------|
| Protocolo | FTP |
| Encriptación | Usar FTP sobre TLS explícito |
| Servidor | 127.0.0.1 |
| Puerto | 2121 |
| Usuario | angel |
| Contraseña | (contraseña de angel) |

![captura](https://github.com/AngelCSR/Portfolio/blob/main/Tema%205/Imagenes/actividad8/foto1.png)

Resultado esperado:

```
Estado: Conexión TLS establecida
```

- Indica que la conexión es **cifrada y segura**.

---
![captura](https://github.com/AngelCSR/Portfolio/blob/main/Tema%205/Imagenes/actividad8/foto2.png)

## 4. Intento de conexión insegura (FTP sin TLS)

Al intentar conectarse sin TLS desde FileZilla Client:

```
Error: Se ha recibido una alerta TLS del servidor: Error de decodificación (50)
Error: No se pudo leer desde el socket: ECONNABORTED - Conexión abortada
Error: Desconectado del servidor
```
![captura](https://github.com/AngelCSR/Portfolio/blob/main/Tema%205/Imagenes/actividad8/foto4.png)

- Esto ocurre porque el servidor tiene activadas las opciones:

```
force_local_logins_ssl=YES
force_local_data_ssl=YES
```

- Las cuales **obligan a que todas las sesiones locales usen TLS**.  
- La conexión FTP normal (sin TLS) es **rechazada inmediatamente**, demostrando que el servidor protege las sesiones.

Desde terminal usando `ftp` también se muestra:

```
530 Non-anonymous sessions must use encryption.
ftp: Login failed
```
![captura](https://github.com/AngelCSR/Portfolio/blob/main/Tema%205/Imagenes/actividad8/foto3.png)

✅ Esto confirma que **FTP inseguro está bloqueado** y **FTPS explícito funciona correctamente**.

---

## 5. Conclusión

- Se generó un certificado TLS autofirmado.  
- Se configuró **vsftpd para FTPS explícito** en el puerto 2121.  
- Se obligó el uso de **conexión segura para todos los usuarios locales**.  
- Verificación:  
  - **FTP inseguro** → rechazado (FileZilla muestra alertas TLS/ECONNABORTED)  
  - **FTPS explícito** → aceptado y cifrado (TLS establecido)  

---


