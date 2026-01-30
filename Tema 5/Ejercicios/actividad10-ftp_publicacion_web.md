## Publicación Web Usando FTP + Apache con el Usuario ftpuser1 (FTPS)

### 🔹 Descripción del flujo completo

El flujo de publicación web usando FTPS y Apache funciona de la siguiente manera:

1. **Usuario crea contenido web:**
   El usuario (`ftpuser1`) crea archivos HTML, CSS o imágenes en su computadora local.

2. **Subida de archivos vía FTPS:**
   El usuario se conecta al servidor usando un cliente FTP como **FileZilla** con FTPS explícito.

   * Datos de conexión:

     * Usuario: `ftpuser1`
     * Contraseña: `usuari1contraseña`
     * Servidor: `localhost` o `127.0.0.1`
     * Puerto: `2121`
   * En FileZilla se selecciona la opción de FTP sobre TLS explícito.
   * El directorio remoto es `/var/www/html`, que coincide con el DocumentRoot de Apache.

3. **Permisos y propiedad de archivos:**

   * Todos los archivos subidos son propiedad de `ftpuser1`.
   * Apache, que corre como usuario `www-data`, puede leer los archivos gracias a los permisos configurados (`755`).

4. **Servidor Apache sirve los archivos:**

   * Apache tiene su **DocumentRoot** configurado en `/var/www/html`.
   * Cuando alguien accede al servidor vía navegador (`http://127.0.0.1/index.html`), Apache busca el archivo en `/var/www/html` y lo entrega al navegador.

5. **Actualización instantánea:**

   * Cada vez que `ftpuser1` sube o reemplaza archivos vía FTPS, Apache los sirve inmediatamente.
   * Esto permite que cualquier cambio hecho localmente se vea reflejado en el navegador sin necesidad de reiniciar Apache.

**Resumen gráfico del flujo:**

```
Usuario (PC)
    │
    │ Crea archivos HTML/CSS/JS
    ▼
FTPS (FileZilla)
    │
    │ Sube archivos al DocumentRoot (/var/www/html)
    ▼
Servidor Linux (/var/www/html)
    │
    │ Apache lee los archivos
    ▼
HTTP (Navegador)
    │
    │ Muestra la página web
    ▼
Usuarios finales pueden ver el contenido actualizado
```

---

### 🔹 Pasos realizados para la práctica

1. **Preparación del usuario FTP (`ftpuser1`):**

* Usuario existente: `ftpuser1:x:1002:1003::/srv/ftp:/bin/bash` (home inicial).
* DocumentRoot de Apache: `/var/www/html`.
* Se mantuvo `/srv/ftp` como home de usuario pero FTPS apunta a `/var/www/html`.

2. **Configuración del servidor FTP (vsftpd):**

Archivo `/etc/vsftpd.conf` ajustado:

```ini
listen=YES
listen_ipv6=NO
listen_port=2121
ssl_enable=YES
allow_anon_ssl=NO
force_local_data_ssl=YES
force_local_logins_ssl=YES
rsa_cert_file=/etc/ssl/private/vsftpd.crt
rsa_private_key_file=/etc/ssl/private/vsftpd.key
local_enable=YES
write_enable=YES
chroot_local_user=YES
allow_writeable_chroot=YES
pasv_enable=YES
pasv_min_port=30000
pasv_max_port=31000
anonymous_enable=NO
local_root=/var/www/html
```

Reiniciar vsftpd:

```bash
sudo systemctl restart vsftpd
```

3. **Ajuste de permisos del DocumentRoot:**

```bash
sudo chown -R ftpuser1:ftpuser1 /var/www/html
sudo chmod -R 755 /var/www/html
```

4. **Subida del archivo HTML vía FTP:**

### Opción 1: FileZilla

1. Conectar usando:

   * Protocolo: FTP
   * Encriptación: Usar FTP sobre TLS explícito
   * Servidor: `127.0.0.1` o `localhost`
   * Puerto: 2121
   * Usuario: `ftpuser1`
   * Contraseña: `usuari1contraseña`
2. Panel izquierdo: carpeta local con `index.html`.
3. Panel derecho: `/var/www/html` (DocumentRoot).
4. Arrastrar `index.html` de izquierda a derecha.

### Opción 2: Terminal

```bash
ftp -p -P 2121 127.0.0.1
# login: ftpuser1 / usuari1contraseña
cd /var/www/html
put index.html
ls
bye
```

5. **Acceso desde el navegador:**

Abrir:

```
http://127.0.0.1/index.html
```

Se debe mostrar la página HTML subida.
![Captura navegador FTP](https://github.com/AngelCSR/Portfolio/blob/main/Tema%205/Imagenes/actividad10/foto3.png)


---

### 🔹 Flujo completo de publicación

1. **Preparación:** Apache con DocumentRoot y usuario FTP con permisos.
2. **Conexión segura:** Cliente FTP usa FTPS al puerto 2121.
3. **Subida de contenido:** Archivos HTML enviados al DocumentRoot.
4. **Publicación:** Apache sirve los archivos, accesibles vía HTTP.

---

### 🔹 Conclusión

* Se configuró un servidor FTP seguro (FTPS) vinculado a Apache.
* Se subió un archivo HTML al DocumentRoot (`/var/www/html`).
* El archivo es accesible desde cualquier navegador mediante HTTP.
* La integración FTP → Apache → Navegador quedó funcional y segura.

