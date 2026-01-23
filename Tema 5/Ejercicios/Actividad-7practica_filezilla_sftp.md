### Práctica de transferencia de archivos con FileZilla usando SFTP

**Usuario:** angel  
**Otros usuarios:** ftpuser1, ftpuser2

---

## 1️⃣ Configuración de la conexión guardada

Para la práctica, creamos un sitio guardado en FileZilla siguiendo estos pasos:

1. Abrimos **Archivo → Gestor de sitios → Nuevo sitio**.
2. Se asignó como nombre: **SFTP ftpuser1 (localhost)**.
3. Se configuraron los siguientes campos:

| Campo | Valor |
|-------|-------|
| Protocolo | SFTP – SSH File Transfer Protocol |
| Servidor | localhost |
| Puerto | 22 |
| Tipo de inicio de sesión | Normal |
| Usuario | ftpuser1 |
| Contraseña | usuari1contraseña |

4. Se pulsó **Conectar** para establecer la conexión.

Esto permite guardar la configuración y acceder rápidamente al servidor SFTP.

---

## 2️⃣ Transferencia bidireccional de archivos

### Subida de archivos (angel → ftpuser1)

1. En el **panel izquierdo (Sitio local)**, seleccionamos la imagen que se encuentra en la carpeta de descargas del usuario angel.
2. En el **panel derecho (Sitio remoto)**, navegamos a: `/home/ftpuser1/subidas`.  
3. Arrastramos la imagen desde el panel izquierdo al panel derecho o clic derecho → **Subir**.

### Descarga de archivos (ftpuser1 → angel)

1. En el **panel derecho**, seleccionamos la misma imagen que acabamos de subir.
2. En el **panel izquierdo**, confirmamos la carpeta de angel donde se guardará el archivo.
3. Arrastramos del panel derecho al izquierdo o clic derecho → **Descargar**.

De esta manera, la transferencia de archivos se realizó en **ambas direcciones**.

---

## 3️⃣ Observación de mensajes de estado

- La **cola de transferencias** muestra los archivos que se están subiendo o bajando.
- La pestaña **Transferencias satisfactorias** confirma que los archivos se transfirieron correctamente.
- Los mensajes en la parte superior indican: **"Transferencia completada"**.

Esto permite verificar que todo el proceso se realizó sin errores.

---

## 4️⃣ Captura de pantalla

La captura de pantalla incluida en la entrega muestra:

- Nombre del sitio: **SFTP ftpuser1 (localhost)**.
- Archivos visibles en **ambos paneles**: angel (local) y ftpuser1/subidas (remoto).
- Cola de transferencias mostrando éxito.
- Mensajes de estado indicando **Transferencia completada**.

Esto documenta que la práctica se realizó correctamente y que los archivos se pueden transferir de manera bidireccional usando SFTP con FileZilla.

