# Documentación: Servidor FTP/FTPS con FileZilla

## Instalación del servidor

### Pasos de instalación de vsftpd en Ubuntu

```bash
sudo apt update
sudo apt install vsftpd -y
vsftpd -v
sudo systemctl start vsftpd
sudo systemctl enable vsftpd
sudo systemctl status vsftpd
```
- Salida esperada: `Active: active (running)`

---

## Configuración básica

Editar archivo de configuración principal:

```bash
sudo nano /etc/vsftpd.conf
```

Parámetros recomendados:

- listen=YES
- listen_ipv6=NO
- local_enable=YES
- write_enable=YES
- chroot_local_user=YES
- listen_port=2121
- pasv_enable=YES
- pasv_min_port=30000
- pasv_max_port=31000

Reiniciar servicio:

```bash
sudo systemctl restart vsftpd
```

---

## Usuarios y permisos

### Crear grupo FTP limitado

```bash
sudo groupadd ftpgroup
getent group ftpgroup
```

### Crear usuarios asociados al grupo

```bash
sudo useradd -m -G ftpgroup -s /bin/false ftpuser1
sudo passwd ftpuser1

sudo useradd -m -G ftpgroup -s /bin/false ftpuser2
sudo passwd ftpuser2
```
- `-s /bin/false` evita acceso a terminal, solo FTP.

### Directorio raíz y permisos

```bash
sudo mkdir -p /srv/ftp
sudo chown root:ftpgroup /srv/ftp
sudo chmod 770 /srv/ftp
```
- Miembros del grupo `ftpgroup` pueden leer, escribir y ejecutar.
- Otros usuarios no tienen acceso.

---

## Seguridad (FTPS)

### Generar certificado TLS autofirmado

```bash
sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
-keyout /etc/ssl/private/vsftpd.key \
-out /etc/ssl/private/vsftpd.crt
```

### Configurar vsftpd para FTPS

```ini
ssl_enable=YES
allow_anon_ssl=NO
force_local_data_ssl=YES
force_local_logins_ssl=YES
rsa_cert_file=/etc/ssl/private/vsftpd.crt
rsa_private_key_file=/etc/ssl/private/vsftpd.key
```
Reiniciar servicio:

```bash
sudo systemctl restart vsftpd
```

- FTP normal → Rechazado
- FTPS explícito → Conexión segura establecida

---

## Modos activo/pasivo

| Característica | Activo | Pasivo |
|----------------|--------|--------|
| Quién inicia la conexión de datos | Servidor → Cliente | Cliente → Servidor |
| Control de firewall | Difícil | Más fácil |
| Puertos requeridos | Cliente >1023, Servidor 20 | Servidor 30000–31000 |
| Uso típico | Redes internas | Internet/NAT |

---

## Clientes utilizados

### Línea de comandos (ftp)

```bash
ftp 127.0.0.1 2121
```
Comandos frecuentes:
- `ls` → listar archivos
- `put archivo` → subir archivo
- `get archivo` → descargar archivo
- `passive` → activar/desactivar modo pasivo

### FileZilla (SFTP/FTPS)

Configuración de sitio:
- Protocolo: SFTP o FTP sobre TLS explícito
- Servidor: localhost
- Puerto: 22 (SFTP) o 2121 (FTPS)
- Usuario: ftpuser1
- Contraseña: definida previamente

Funcionalidades:
- Transferencia bidireccional
- Colas de transferencia
- Reanudar descargas
- Gestión de directorios remotos y locales

---

## Integración web

- DocumentRoot: /var/www/html
- Usuario FTP sube archivos vía FTPS a /var/www/html
- Permisos:

```bash
sudo chown -R ftpuser1:ftpuser1 /var/www/html
sudo chmod -R 755 /var/www/html
```

- Acceso desde navegador: `http://127.0.0.1/index.html`

---

## Recomendaciones de administración

- Limitar `max_clients` y `max_per_ip`
- Auditar usuarios y grupos
- Deshabilitar acceso anónimo si no necesario
- Usar FTPS para cifrar conexiones
- Revisar permisos de archivos y directorios
- Mantener certificados actualizados
- Activar registros detallados y rotarlos regularmente
- Realizar backups periódicos
- Configurar firewall y NAT correctamente
- Probar modo activo/pasivo y transferencias regularmente

---

## Conclusión

- Servidor FTP seguro configurado con vsftpd.
- FileZilla permite transferencias fiables con FTPS y SFTP.
- Integración con Apache permite publicar contenido web de manera inmediata.
- Buenas prácticas aseguran seguridad, confiabilidad y administración eficiente.
