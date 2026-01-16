# Prueba de conexión FTP en modo pasivo y activo

## 1️⃣ Conexión al servidor FTP

Abrí la terminal y me conecté a mi servidor FTP:

```bash
ftp 127.0.0.1 2121
```

Ingresé el usuario y contraseña:

```
Name: ftpuser1
Password: usuari1contraseña
```

El servidor respondió:

```
230 Login successful.
ftp>
```

✅ Conexión exitosa.

---

## 2️⃣ Activar modo pasivo

En el prompt del cliente FTP, escribí:

```
passive
```

El cliente respondió:

```
Passive mode: off; fallback to active mode: off.
```

> Nota: En mi versión del cliente FTP, el modo pasivo ya estaba activo por defecto, así que el mensaje indica que se usará modo pasivo automáticamente.

---

## 3️⃣ Probar transferencia de datos

Listé el contenido del directorio:

```
ftp> ls
229 Entering Extended Passive Mode (|||30645|)
150 Here comes the directory listing.
drwxr-xr-x    2 0        124          4096 Jan 16 16:20 anon
226 Directory send OK.
```

- El directorio `anon` aparece listado correctamente.
- Esto confirma que **modo pasivo está funcionando** y se usa el puerto dentro del rango configurado (30000–31000).

---

## 4️⃣ Probar subida de archivo

Intenté subir un archivo para verificar permisos:

```
ftp> put prueba.txt
```

- Como estoy en mi directorio home de `ftpuser1`, se subió correctamente si tengo permisos.
- Si estuviera en el directorio de solo lectura de `anonymous`, el resultado habría sido:

```
550 Permission denied.
```

---

## ✅ Resumen de comandos usados

```bash
ftp 127.0.0.1 2121   # Conexión
Name: ftpuser1        # Usuario
Password: usuari1contraseña
ftp> passive          # Activar modo pasivo (ya activo por defecto)
ftp> ls               # Listar archivos
ftp> put prueba.txt   # Subir archivo (verificar permisos)
```

---

## 5️⃣ Tabla comparativa Modo Activo vs Modo Pasivo

| Característica | Modo Activo | Modo Pasivo |
|----------------|------------|-------------|
| Quién inicia la conexión de datos | Servidor → Cliente | Cliente → Servidor |
| Necesidad de puertos abiertos en el cliente | Sí, puerto >1024 | No |
| Necesidad de puertos abiertos en el servidor | Solo puerto 21 (control) | Puerto 21 + rango pasivo (30000–31000) |
| Funcionamiento detrás de firewall/NAT | Puede fallar si el firewall bloquea la conexión entrante | Funciona siempre, porque el cliente abre la conexió