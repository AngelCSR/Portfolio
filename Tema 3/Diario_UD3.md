


### Qué he aprendido

A lo largo de esta unidad he aprendido a instalar y configurar Apache 2 en Ubuntu 24.04, comprendiendo cómo funciona un servidor web desde cero. He aprendido a:

* Actualizar el sistema y preparar el entorno para Apache.
* Configurar el usuario y grupo de Apache y establecer los permisos correctos en los directorios.
* Crear páginas web personalizadas y gestionar Virtual Hosts para múltiples sitios.
* Implementar control de acceso mediante archivos `.htaccess` y `.htpasswd`.
* Generar e implementar certificados SSL/TLS, tanto autofirmados como con Let's Encrypt, para habilitar HTTPS.
* Redirigir tráfico HTTP hacia HTTPS para mejorar la seguridad.

### Qué no entiendo

Aunque he logrado configurar Apache y HTTPS con éxito, todavía me resulta un poco complejo:

* Comprender a fondo la interacción de todos los módulos de Apache y sus dependencias en configuraciones avanzadas.
* La gestión de certificados con autoridades certificadoras reales, más allá del certificado autofirmado de pruebas.
* Algunas configuraciones específicas de redirección y seguridad (por ejemplo, HSTS o redirecciones condicionales complejas).

### Qué es lo que más me ha gustado y qué es lo que menos

**Lo que más me ha gustado:** ver cómo un servidor web se pone en marcha desde cero y cómo puedo publicar mi propia página web, controlar el acceso y asegurar la comunicación con HTTPS. La parte de seguridad y control de acceso me pareció especialmente interesante.

**Lo que menos me ha gustado:** los problemas menores de permisos y configuración que surgieron al principio, ya que a veces pequeños errores pueden hacer que Apache no funcione, lo que resulta frustrante hasta que se identifica la causa.

### Qué más me gustaría saber relacionado con la Unidad

Me gustaría profundizar en:

* La configuración avanzada de Virtual Hosts, incluyendo múltiples dominios con SSL.
* Automatización de certificados HTTPS usando Let's Encrypt y renovación automática.
* Mejores prácticas de seguridad en Apache, incluyendo cabeceras HTTP, firewall, y protección contra ataques comunes (DDoS, inyección, etc.).
* Integración de Apache con lenguajes de servidor (PHP, Python) y bases de datos para desplegar aplicaciones web completas.
