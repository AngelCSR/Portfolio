# Tomcat: Identificación de archivos de configuración 

## 1️⃣ Ubicación de los archivos

En nuestra instalación (`/opt/tomcat/latest`), los archivos se encuentran en:

- `/opt/tomcat/latest/conf/server.xml` → `server.xml`  
- `/opt/tomcat/latest/conf/web.xml` → `web.xml`  
- `/opt/tomcat/latest/conf/tomcat-users.xml` → `tomcat-users.xml`  
- `/opt/tomcat/latest/conf/context.xml` → `context.xml`  

## 2️⃣ Función y configuración de cada archivo

### a) server.xml

**Función:** Archivo principal de configuración del servidor Tomcat.  

**Qué se configura:**

- **Conectores (Connector):** puerto HTTP, HTTPS, AJP  
- **Hosts virtuales (Host):** dominios y nombres de aplicaciones  
- **Servicios y motores (Service, Engine):** configuración global de la instancia  
- **Valves y recursos:** logs, seguridad, etc.  

**Ejemplo de elemento:**

```xml
<Connector port="8080" protocol="HTTP/1.1" connectionTimeout="20000" redirectPort="8443" />
<Host name="localhost" appBase="webapps" unpackWARs="true" autoDeploy="true" />

