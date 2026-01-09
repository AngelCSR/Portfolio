# Instalación y Configuración de Servidor FTP en Ubuntu

## 1 Instalación de vsftpd

Actualizamos los repositorios e instalamos `vsftpd`:

```bash
sudo apt update
sudo apt install vsftpd -y
```

Verificamos la versión instalada:

```bash
vsftpd -v
```

---
![captura](https://github.com/AngelCSR/Portfolio/blob/main/Tema%205/Imagenes/Actividad%202/foto1.png)


## 2 Configuración del servidor

Editamos el archivo principal de configuración:

```bash
sudo nano /etc/vsftpd.conf
```

Se recomienda ajustar los siguientes parámetros:

| Parámetro           | Valor | Explicación                                   |
| ------------------- | ----- | --------------------------------------------- |
| `listen`            | YES   | Escucha conexiones IPv4                       |
| `listen_ipv6`       | NO    | Desactiva IPv6 si no se usa                   |
| `anonymous_enable`  | NO    | Desactiva acceso anónimo                      |
| `local_enable`      | YES   | Permite acceso a usuarios locales             |
| `write_enable`      | YES   | Permite subir archivos                        |
| `chroot_local_user` | YES   | Mantiene a los usuarios en su directorio home |

Opcional: cambiar el puerto FTP (por defecto 21):

```text
listen_port=2121
```

Guardamos y cerramos el archivo (`Ctrl+O`, `Enter`, `Ctrl+X`).

---
![captura](https://github.com/AngelCSR/Portfolio/blob/main/Tema%205/Imagenes/Actividad%202/FOTO2.png)

## 3 Iniciar y habilitar el servicio

Iniciamos y habilitamos el servicio para que arranque automáticamente:

```bash
sudo systemctl start vsftpd
sudo systemctl enable vsftpd
sudo systemctl status vsftpd
```

**Salida esperada:**

```
Active: active (running)
```


![captura](https://github.com/AngelCSR/Portfolio/blob/main/Tema%205/Imagenes/Actividad%202/foto3.png)


---

## 4 Probar la conexión

Desde otra terminal o cliente FTP:

```bash
ftp 127.0.0.1

```
![captura](https://github.com/AngelCSR/Portfolio/blob/main/Tema%205/Imagenes/Actividad%202/foto4.png)

Si la conexión es exitosa, podrás listar y transferir archivos en tu directorio home.

---



## 5 Explicación de pasos

> Se instaló `vsftpd` como servidor FTP en Ubuntu. Se configuró el puerto de escucha 21, se habilitó el acceso a usuarios locales y se activó el servicio para iniciar automáticamente al arrancar el sistema. Se verificó que el servidor estaba activo mediante `systemctl status vsftpd`.

---


