# Actividad 4: Configuración de acceso anónimo (directorio limitado y solo lectura)

## 1️⃣ Edición del archivo de configuración

Primero abrí el archivo principal de configuración de vsftpd con:

    sudo nano /etc/vsftpd.conf

Dentro del archivo, añadí (o modifiqué) las siguientes líneas necesarias
para habilitar el acceso anónimo y limitarlo correctamente:

    anonymous_enable=YES
    anon_root=/srv/ftp/anon
    anon_world_readable_only=YES

    anon_upload_enable=NO
    anon_mkdir_write_enable=NO
    anon_other_write_enable=NO

Estas directivas permiten:

-   **anonymous_enable=YES**: activar el acceso mediante el usuario
    anonymous.\
-   **anon_root=/srv/ftp/anon**: definir el directorio al que estará
    restringido.\
-   **anon_world_readable_only=YES**: asegurar que solamente tenga
    permisos de lectura.\
-   Y dejar todas las opciones de escritura desactivadas, impidiendo que
    el usuario anónimo pueda subir, borrar o modificar archivos.

------------------------------------------------------------------------

## 2️⃣ Creación del directorio para el acceso anónimo

Después, creé el directorio que utilizará el usuario anónimo y configuré
sus permisos:

    sudo mkdir -p /srv/ftp/anon
    sudo chown -R ftp:ftp /srv/ftp/anon
    sudo chmod -R 755 /srv/ftp/anon

Estos comandos establecen correctamente la propiedad y los permisos.\
El usuario *ftp* (que es el que usa vsftpd para conexiones anónimas)
tendrá acceso de lectura, y el sistema evita que pueda escribir dentro
del directorio.

------------------------------------------------------------------------

## 3️⃣ Reinicio del servicio

Para aplicar los cambios, reinicié vsftpd:

    sudo systemctl restart vsftpd

------------------------------------------------------------------------

## 4️⃣ Prueba de acceso anónimo

Finalmente, probé la conexión desde un cliente FTP utilizando el puerto
que configuré previamente (2121):

    ftp 127.0.0.1 2121

En la pantalla de inicio de sesión introduje:

-   **Usuario:** anonymous\
-   **Contraseña:** (simplemente pulsé ENTER)

El resultado fue:

    230 Login successful.

Una vez dentro, ejecuté `ls` y pude listar el contenido del directorio
asignado.\
Tal como estaba previsto, el servidor solo me permitió leer y no
escribir, ya que al intentar subir un archivo obtuve:

    550 Permission denied.

Esto confirma que el acceso anónimo funciona correctamente, está
restringido al directorio asignado y únicamente tiene permisos de
lectura.
