# Reflexión sobre la Unidad 4: Tomcat

## Qué he aprendido
En esta unidad he aprendido sobre la arquitectura y funcionamiento de Tomcat. Entendí para qué sirven los componentes principales: **Catalina** (el motor de servlets), **Coyote** (conector HTTP), **Jasper** (compilador JSP), y las herramientas de administración **Manager y Host Manager**. También aprendí a identificar los archivos de configuración importantes (`server.xml`, `web.xml`, `tomcat-users.xml`, `context.xml`) y su función dentro del servidor. Practiqué el despliegue de aplicaciones web mediante WAR y comprendí cómo Tomcat gestiona la carga automática de aplicaciones.

## Qué no entiendo
Todavía me resulta un poco confuso el flujo interno completo de cómo Catalina maneja múltiples contenedores y aplicaciones simultáneamente, y cómo interactúa con AJP y reverse proxy de manera interna.

## Qué es lo que más me ha gustado y qué es lo que menos
Lo que más me ha gustado es ver cómo una aplicación JSP se despliega automáticamente y cómo se puede administrar todo desde **Manager y Host Manager**. También me ha resultado interesante la posibilidad de probar Tomcat en contenedores Docker.

Lo que menos me ha gustado es que la configuración de seguridad y HTTPS requiere varios pasos y conceptos nuevos que al principio resultan liosos, especialmente manejar keystores y roles de usuarios.

## Qué más me gustaría saber relacionado con la Unidad habiendo hecho este ejercicio
Me gustaría profundizar en cómo optimizar el rendimiento de Tomcat bajo carga usando ajustes en `server.xml`, así como explorar más sobre el despliegue en entornos cloud y contenedores a gran escala. También quiero aprender a automatizar el despliegue y la gestión de aplicaciones mediante scripts y herramientas CI/CD.

