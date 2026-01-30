# Reflexión sobre la Unidad 5: FileZilla y Servidores FTP

## Qué he aprendido
En esta unidad he aprendido a instalar y configurar un servidor FTP usando `vsftpd` en Ubuntu. También aprendí a crear usuarios y grupos, asignarles permisos y limitar el acceso de forma segura. He visto cómo funciona el FTP en **modo activo y pasivo**, y cómo configurar los puertos para que las transferencias funcionen correctamente. Además, he probado clientes de línea de comandos (`ftp`) y gráficos como FileZilla para subir y bajar archivos, y he comprobado cómo se puede integrar FTP seguro (FTPS) con Apache para publicar páginas web desde el servidor.

## Qué no entiendo
Todavía me cuesta un poco entender cómo funcionan los firewalls y NAT cuando se usa **modo activo**, y cómo hacer que todo funcione automáticamente si hay muchos usuarios o varias conexiones a la vez.

## Qué es lo que más me ha gustado y qué es lo que menos
Lo que más me ha gustado es que con FileZilla puedo ver los archivos de manera gráfica y moverlos entre mi ordenador y el servidor sin complicaciones. También me ha gustado ver cómo Apache puede servir los archivos que subo vía FTP directamente en el navegador.

Lo que menos me ha gustado es que configurar FTPS y los certificados TLS es un poco lioso al principio, y que el FTP en línea de comandos se queda corto comparado con clientes gráficos. También me ha parecido un poco complicado dejar seguro el acceso anónimo.

## Qué más me gustaría saber relacionado con la Unidad habiendo hecho este ejercicio
Me gustaría aprender a **automatizar la creación de usuarios y permisos**, y probar más a fondo cómo funciona SFTP frente a FTPS. También me interesa saber cómo mantener un servidor FTP seguro y disponible todo el tiempo, aunque haya varios usuarios conectados a la vez, sin que haya errores en las transferencias.

