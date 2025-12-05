# Despliegue de la aplicación sample.war en Tomcat

## 1️⃣ Descargar el WAR de ejemplo
```bash
cd /tmp
wget https://tomcat.apache.org/tomcat-9.0-doc/appdev/sample/sample.war
```
![captura](https://github.com/AngelCSR/Portfolio/blob/main/Tema4/imagenes/Tomcat_Despliegue/foto1.png)
## 2️⃣ Despliegue del WAR en Tomcat

```bash
sudo mv sample.war /opt/tomcat/latest/webapps/
sudo chown tomcat:tomcat /opt/tomcat/latest/webapps/sample.war
```

- **Tomcat detecta automáticamente el WAR en webapps.** 
- **Crea la carpeta descomprimida sample/.**  
- **Inicializa el contexto de la aplicación y carga servlets y JSPs.** 
- **Ahora la aplicación está lista para ser accedida.** 

![captura](https://github.com/AngelCSR/Portfolio/blob/main/Tema4/imagenes/Tomcat_Despliegue/foto2.png)

## 3️⃣ Verificación de que Tomcat está corriendo
```bash
sudo systemctl status tomcat
```
![captura](https://github.com/AngelCSR/Portfolio/blob/main/Tema4/imagenes/Tomcat_Despliegue/foto3.png)


Estado active (running) confirma que el servidor está funcionando.

## 4️⃣ Verificación del despliegue automático
```bash

ls -l /opt/tomcat/latest/webapps/
```
![captura](https://github.com/AngelCSR/Portfolio/blob/main/Tema4/imagenes/Tomcat_Despliegue/foto4.png)

Aparecen ambos: sample.war y la carpeta sample/ descomprimida.

Esto confirma que Tomcat ha desplegado la aplicación automáticamente.

## 5️⃣ Acceder a la aplicación (desde el mismo servidor)

Abre en tu navegador:
```bash

http://localhost:8080/sample/
```

Si devuelve el HTML de la página “Hello World” o contenido del ejemplo, está funcionando.
![captura](https://github.com/AngelCSR/Portfolio/blob/main/Tema4/imagenes/Tomcat_Despliegue/foto5.png)
