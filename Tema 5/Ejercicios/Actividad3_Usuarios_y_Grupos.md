# Configuración de Usuarios y Grupos en vsftpd (Ubuntu)

## 1️⃣ Crear un grupo con permisos limitados

Creamos un grupo llamado `ftpgroup`:

```bash
sudo groupadd ftpgroup
```

Verificamos que se creó:

```bash
getent group ftpgroup
```

---

## 2️⃣ Crear usuarios asociados al grupo

Creamos dos usuarios `ftpuser1` y `ftpuser2`, asignándolos al grupo `ftpgroup` y definiendo sus directorios home:

```bash
sudo useradd -m -G ftpgroup -s /bin/false ftpuser1
sudo passwd ftpuser1

sudo useradd -m -G ftpgroup -s /bin/false ftpuser2
sudo passwd ftpuser2


Usuario: ftpuser1
Contraseña: usuari1contraseña

Usuario: ftpuser2
Contraseña: usuari2contraseña

```

> Nota: `-s /bin/false` evita que los usuarios inicien sesión en la terminal; solo FTP.

---

## 3️⃣ Definir directorio raíz de FTP

Creamos un directorio para los usuarios FTP:

```bash
sudo mkdir -p /srv/ftp
```

Cambiamos la propiedad y permisos del directorio:

```bash
sudo chown root:ftpgroup /srv/ftp
sudo chmod 770 /srv/ftp
```

> Esto permite **lectura, escritura y ejecución** al grupo `ftpgroup` y propietario root, pero no a otros usuarios.

---

## 4️⃣ Configurar `vsftpd` para usar chroot y límites

Editamos el archivo de configuración:

```bash
sudo nano /etc/vsftpd.conf
```

Aseguramos que existan estas líneas:

```text
listen=YES
local_enable=YES
write_enable=YES
chroot_local_user=YES
allow_writeable_chroot=YES
user_sub_token=$USER
local_root=/srv/ftp
max_clients=5
max_per_ip=2
```

Explicación:

* `chroot_local_user=YES`: limita al usuario a su directorio home.
* `allow_writeable_chroot=YES`: permite escribir en el directorio chroot.
* `max_clients=5`: máximo de 5 conexiones simultáneas al servidor.
* `max_per_ip=2`: máximo 2 conexiones por IP.

Guardamos y cerramos.

Reiniciamos vsftpd:

```bash
sudo systemctl restart vsftpd
```

---

## 5️⃣ Probar los usuarios

Desde otra terminal:

```bash
ftp 127.0.0.1
# Usuario: ftpuser1
# Contraseña: la que asignaste
```

Luego con `ftpuser2`:

```bash
ftp 127.0.0.1
# Usuario: ftpuser2
```

---

## 6️⃣ Permisos de usuario vs permisos de grupo

| Tipo de permiso         | Descripción                                                                                                                                                            |
| ----------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Permisos de usuario** | Aplican solo al propietario del archivo o directorio. Determinan si el dueño puede leer, escribir o ejecutar.                                                          |
| **Permisos de grupo**   | Aplican a todos los usuarios que pertenecen al grupo del archivo/directorio. Permiten coordinar acceso entre varios usuarios sin dar permisos a todos los del sistema. |

> Ejemplo: Si `/srv/ftp` pertenece al grupo `ftpgroup` y tiene permisos `770`, todos los miembros del grupo pueden leer, escribir y borrar archivos, mientras que otros usuarios no tienen acceso.

---

## 7️⃣ Resumen

* Grupo `ftpgroup` controla permisos colectivos.
* Usuarios `ftpuser1` y `ftpuser2` están limitados a su directorio raíz.
* Se establecen límites de conexión para seguridad.
* Se diferencian permisos de usuario y de grupo para controlar el acceso y mantener seguridad en el servidor FTP.
