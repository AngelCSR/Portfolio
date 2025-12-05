# Tomcat: Identificación de archivos de configuración 

## 1️⃣ Ubicación de los archivos

En nuestra instalación (`/opt/tomcat/latest`), los archivos se encuentran en:

- `/opt/tomcat/latest/conf/server.xml` → `server.xml`  
- `/opt/tomcat/latest/conf/web.xml` → `web.xml`  
- `/opt/tomcat/latest/conf/tomcat-users.xml` → `tomcat-users.xml`  
- `/opt/tomcat/latest/conf/context.xml` → `context.xml`
  
![captura](https://github.com/AngelCSR/Portfolio/blob/main/Tema4/imagenes/identificacionConf/foto1.png)


## 2️⃣ Función y configuración de cada archivo

### a) server.xml

**Función:** Archivo principal de configuración del servidor Tomcat.  

**Qué se configura:**

- **Conectores (Connector):** puerto HTTP, HTTPS, AJP  
- **Hosts virtuales (Host):** dominios y nombres de aplicaciones  
- **Servicios y motores (Service, Engine):** configuración global de la instancia  
- **Valves y recursos:** logs, seguridad, etc.  

![captura](https://github.com/AngelCSR/Portfolio/blob/main/Tema4/imagenes/identificacionConf/foto2.png)

### b) web.xml

**Función:**Configuración global de aplicaciones web; actúa como el descriptor estándar para todas las aplicaciones.  

**Qué se configura:**

- **Servlets y filtros globales**  
- **Parámetros de contexto**
- **Manejo de errores y seguridad **

![captura](https://github.com/AngelCSR/Portfolio/blob/main/Tema4/imagenes/identificacionConf/foto3.png)

### c)tomcat-users.xml

**Función:**Define usuarios y roles para acceso a la administración y paneles de Tomcat. 

**Qué se configura:**

- **Usuarios (user):** nombre, contraseña y roles  
- **Roles (role):** como manager-gui, admin-gui, etc.

![captura](https://github.com/AngelCSR/Portfolio/blob/main/Tema4/imagenes/identificacionConf/foto4.png)

### d)context.xml

**Función:**Define la configuración del contexto de la aplicación, es decir, cada aplicación desplegada.

**Qué se configura:**

- **Recursos JNDI:** bases de datos, conexiones, etc.
- **Sesiones y parámetros de contexto.**
- **Seguridad y control de acceso por aplicación**
  
![captura](https://github.com/AngelCSR/Portfolio/blob/main/Tema4/imagenes/identificacionConf/foto5.png)

## 3️⃣ Mapa visual de dependencias

```text
               +----------------+
               |   server.xml   |
               |  (config global)|
               +--------+-------+
                        |
         +--------------+----------------+
         |                               |
   +-----v-----+                   +-----v-----+
   |   web.xml |                   | context.xml|
   | (global   |                   |(app-level)|
   |  servlets)|                   |  context) |
   +-----------+                   +-----------+
                        |
                        v
               +----------------+
               | tomcat-users.xml|
               |  (usuarios/roles)|
               +----------------+
```
### Explicación del flujo:

- **server.xml**→ define el motor, hosts y conectores globales 
- **web.xml**→ aplica reglas globales a todas las aplicaciones
- **context.xml** → personaliza cada aplicación (puede sobreescribir web.xml)
- **tomcat-users.xml** → controla acceso a paneles y administración, usado por Tomcat cuando se autentica

 

 






