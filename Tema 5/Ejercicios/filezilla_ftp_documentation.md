Documentación: Servidor FTP/FTPS con FileZilla

1. Instalación del servidor FTP (vsftpd) en Ubuntu

1.1 Actualizar repositorios e instalar vsftpd:

sudo apt update
sudo apt install vsftpd -y

1.2 Verificar versión instalada:

vsftpd -v

1.3 Iniciar y habilitar el servicio:

sudo systemctl start vsftpd
sudo systemctl enable vsftpd
sudo systemctl status vsftpd

Salida esperada: Active: active (running)

---

2. Configuración básica del servidor

Editar archivo de configuración principal:

sudo nano /etc/vsftpd.conf

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

sudo systemctl restart vsftpd

---

3. Usuarios y permisos

3.1 Crear grupo FTP limitado:

sudo groupadd ftpgroup
getent group ftpgroup

3.2 Crear usuarios asociados al grupo:

sudo useradd -m -G ftpgroup -s /bin/false ftpuser1
sudo passwd ftpuser1

sudo useradd -m -G ftpgroup -s /bin/false ftpuser2
sudo passwd ftpuser2

3.3 Directorio raíz y permisos:

sudo mkdir -p /srv/ftp
sudo chown root:ftpgroup /srv/ftp
sudo chmod 770 /srv/ftp

---

4. Seguridad: Configuración FTPS

4.1 Generar certificado TLS autofirmado:

sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 \
-keyout /etc/ssl/private/vsftpd.key \
-out /etc/ssl/private/vsftpd.crt

4.2 Configurar vsftpd para FTPS:

ssl_enable=YES
allow_anon_ssl=NO
force_local_data_ssl=YES
force_local_logins_ssl=YES
rsa_cert_file=/etc/ssl/private/vsftpd.crt
rsa_private_key_file=/etc/ssl/private/vsftpd.key

Reiniciar servicio:

sudo systemctl restart vsftpd

4.3 Comprobación:
- FTP normal → Rechazado
- FTPS explícito → Conexión segura establecida

---

5. Modos de transferencia: activo vs pasivo

| Característica | Activo | Pasivo |
|----------------|--------|--------|
| Quién inicia la conexión de datos | Servidor → Cliente | Cliente → Servidor |
| Control de firewall | Difícil | Más fácil |
| Puertos requeridos | Cliente >1023, Servidor 20 | Servidor 30000–31000 |
| Uso típico | Redes internas | Internet/NAT |

---

6. Clientes utilizados

6.1 Línea de comandos (ftp)

ftp 127.0.0.1 2121

Comandos frecuentes:

- ls → listar archivos
- put archivo → subir archivo
- get archivo → descargar archivo
- passive → activar/desactivar modo pasivo

6.2 FileZilla (SFTP/FTPS)

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

7. Integración web con Apache

- DocumentRoot: /var/www/html
- Usuario FTP sube archivos vía FTPS a /var/www/html
- Permisos:

sudo chown -R ftpuser1:ftpuser1 /var/www/html
sudo chmod -R 755 /var/www/html

Acceso desde navegador: http://127.0.0.1/index.html

---

8. Recomendaciones de administración y buenas prácticas

- Limitar max_clients y max_per_ip
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

9. Conclusión

- Servidor FTP seguro configurado con vsftpd.
- FileZilla permite transferencias fiables con FTPS y SFTP.
- Integración con Apache permite publicar contenido web de manera inmediata.
- Buenas prácticas aseguran seguridad, confiabilidad y administración eficiente.

