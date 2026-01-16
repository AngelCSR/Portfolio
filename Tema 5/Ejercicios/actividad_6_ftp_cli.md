# Actividad 6: Pruebas con clientes en línea de comandos

## 1️⃣ Cliente: ftp (cliente básico de Linux)

### Conexión
```bash
ftp 127.0.0.1 2121
```
**Función:** Conecta al servidor FTP en el puerto 2121.

### Login
```
Name: ftpuser1
Password: usuari1contraseña
```
**Función:** Autentica al usuario en el servidor.

### Listar archivos
```bash
ls
```
**Función:** Muestra los archivos y carpetas en el directorio actual del servidor.

### Subir archivo
```bash
put prueba.txt
```
**Función:** Sube el archivo `prueba.txt` desde el cliente al servidor.

### Descargar archivo
```bash
get prueba.txt
```
**Función:** Descarga el archivo `prueba.txt` desde el servidor al cliente.

