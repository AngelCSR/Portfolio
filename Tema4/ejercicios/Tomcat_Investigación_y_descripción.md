# Tomcat: Investigación y descripción

**Tomcat no es solo un servidor web, sino un contenedor de servlets totalmente funcional compuesto por varios módulos especializados. Cada uno cumple una función específica para recibir peticiones, procesarlas y generar respuestas dinámicas.**

## Catalina
Catalina es el **contenedor de servlets** de Tomcat; es el corazón del servidor donde se ejecutan las aplicaciones web Java (servlets y JSP). Gestiona ciclos de vida, seguridad, sesiones y despliegue. Se define y configura mediante los archivos de la carpeta **conf/**, especialmente **server.xml**. Es responsable del funcionamiento interno de los contenedores (**Engine**, **Host**, **Context**) que organizan las aplicaciones.

## Coyote
Coyote es el **conector HTTP** de Tomcat. Actúa como servidor web y se encarga de recibir peticiones HTTP/HTTPS, interpretarlas y pasarlas a Catalina. También puede funcionar como conector para AJP (mod_jk). Su configuración se encuentra en **conf/server.xml**, donde se definen los `<Connector>` que escuchan en puertos como el **8080**.

## Jasper
Jasper es el **motor de compilación de JSP**. Convierte archivos `.jsp` en servlets Java y luego los compila para que Catalina los ejecute. Jasper se integra internamente en Tomcat: no es un proceso separado, pero su configuración se encuentra dentro del entorno de Catalina y las bibliotecas que lo soportan están en **lib/**.

## Manager y Host Manager
El **Manager** permite administrar aplicaciones (desplegar, parar, recargar) desde una consola web en `/manager`.  
El **Host Manager** permite crear y gestionar *virtual hosts* desde `/host-manager`.  
Ambos son aplicaciones web ubicadas dentro de **webapps/manager** y **webapps/host-manager**, y requieren roles definidos en **conf/tomcat-users.xml**.

## Estructura básica de directorios
- **bin/** → Scripts de inicio/parada (`startup.sh`, `catalina.bat`).  
- **conf/** → Configuración principal (`server.xml`, `web.xml`, `tomcat-users.xml`).  
- **webapps/** → Aplicaciones desplegadas (ROOT, manager, aplicaciones del usuario).  
- **lib/** → Librerías de Tomcat y dependencias compartidas.  
- **logs/** → Archivos de log (`catalina.out`, `localhost.log`, etc).

## Flujo interno de funcionamiento
Las peticiones llegan primero a **Coyote**, que actúa como servidor HTTP. Este las entrega a **Catalina**, donde los contenedores **Engine → Host → Context** identifican la aplicación destino. Catalina invoca el servlet o JSP correspondiente (compilado por Jasper si es necesario). Las aplicaciones se despliegan automáticamente si se colocan en **webapps/** o mediante **Manager**. Finalmente, la respuesta se envía de vuelta a través de Coyote.
