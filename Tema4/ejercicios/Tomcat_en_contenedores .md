# Tomcat en contenedores

## 1️⃣ Crear una carpeta para tu aplicación

Vamos a crear una carpeta en el home para colocar el WAR:

```bash
mkdir -p ~/myapp
```

Ahora copiamos el WAR que encontramos:

```bash
cp /opt/tomcat/latest/webapps/sample.war ~/myapp/
```

verificamos que esté allí:

```bash
ls ~/myapp
```

**Salida esperada:**

```
sample.war
```

![captura](https://github.com/AngelCSR/Portfolio/blob/main/Tema4/imagenes/Tomcat-en-contenedores/foto1.png)

---

## 2️⃣ Levantar Tomcat en Docker con tu WAR

```bash
docker run -d --name tomcat-contenedor -p 8081:8080 \
  -v ~/myapp:/usr/local/tomcat/webapps \
  tomcat:latest
```

* `-d` → ejecuta en segundo plano.
* `--name tomcat-contenedor` → nombre del contenedor.
* `-p 8081:8080` → mapea el puerto 8080 del contenedor al host 8081.
* `-v ~/myapp:/usr/local/tomcat/webapps` → monta tu WAR dentro de Tomcat.

![captura](https://github.com/AngelCSR/Portfolio/blob/main/Tema4/imagenes/Tomcat-en-contenedores/foto2.png)

---

## 3️⃣ Verificar que Tomcat funciona

Abrimos el navegador y entramos a:

```
http://localhost:8081/sample/
```

Si todo está bien, veremos la aplicación desplegada.

También puedes probar con curl desde la terminal:

```bash
curl http://localhost:8081/sample/
```

![captura](https://github.com/AngelCSR/Portfolio/blob/main/Tema4/imagenes/Tomcat-en-contenedores/foto3.png)

---

## 4️⃣ Diferencias entre Tomcat nativo y Tomcat en contenedor

| Característica              | Tomcat Nativo                        | Tomcat en Contenedor (Docker)                                   |
| --------------------------- | ------------------------------------ | --------------------------------------------------------------- |
| Instalación                 | Directa en el sistema operativo      | Incluye Java + Tomcat en la imagen                              |
| Dependencias                | Debes instalar Java, configurar PATH | Todo viene preconfigurado en la imagen                          |
| Aislamiento                 | Comparte recursos con el host        | Aislado del host, fácil de mover                                |
| Portabilidad                | Limitado a SO donde se instaló       | Funciona igual en cualquier host con Docker                     |
| Escalabilidad               | Difícil, requiere nuevas VMs         | Fácil de escalar con Docker Compose o Kubernetes                |
| Reinicios y actualizaciones | Puede afectar otros servicios        | Contenedor puede reiniciarse sin afectar el host                |
| Configuración               | Archivos locales, edición manual     | Variables de entorno y volúmenes facilitan reproducibilidad     |
| Rendimiento                 | Acceso directo al hardware           | Ligera sobrecarga por capa de contenedor, casi igual que nativo |
