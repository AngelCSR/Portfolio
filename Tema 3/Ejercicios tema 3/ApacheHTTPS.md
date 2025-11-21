# Implementación de HTTPS en Apache2 sobre Ubuntu

## 1. Introducción

El objetivo de esta práctica es investigar, configurar e implementar el
protocolo HTTPS en un servidor web Apache2 ejecutándose sobre Ubuntu...

## 2. Investigación

### 2.1 Funcionamiento del protocolo HTTPS y su importancia

HTTPS (HyperText Transfer Protocol Secure) es la evolución segura del protocolo HTTP. Su función principal es cifrar la comunicación entre cliente y servidor mediante el uso de SSL/TLS (Secure Sockets Layer / Transport Layer Security).
Cuando un usuario accede a un sitio web mediante HTTPS, ocurre lo siguiente:
####      **Handshake TLS**:
-    El navegador y el servidor negocian la versión de TLS y los algoritmos criptográficos que usarán para la conexión.
#####  **Intercambio del certificado**: 
-   El servidor envía su certificado digital para demostrar su identidad.
##### **Verificación del certificado**:
-    El cliente comprueba si el certificado es válido (en certificados autofirmados esto falla, por eso aparece la advertencia).
##### **Generación de una clave simétrica**:
-    El cliente crea una clave temporal para cifrar la sesión y la envía cifrada al servidor.
##### **Comunicación cifrada**:
-    A partir de ese momento, todos los datos viajan encriptados.
   
#### Importancia de HTTPS:

-    Protege contra ataques Man-in-the-Middle (MITM).

-    Evita que datos sensibles puedan ser interceptados.

-    Aumenta la confianza del usuario.

-    Los navegadores marcan HTTP como "No seguro".

-    Google penaliza sitios sin HTTPS en su posicionamiento SEO.

Actualmente, el uso de HTTPS es obligatorio en cualquier entorno donde se transmitan datos privados (formularios, contraseñas, cookies de sesión, etc.).

### 2.2 Tipos de certificados SSL/TLS

-   **Autofirmado:** útil para pruebas, no confiable por navegadores.
    - Son generados por el propio servidor.
    - Son válidos a nivel técnico y permiten cifrado real.
    - No están firmados por una autoridad certificadora, por lo que los navegadores siempre muestran advertencias.   
-   **CA confiable:** reconocido por navegadores; Let's Encrypt es
    gratuito.
    - Totalmente confiables para los navegadores.
    - Permiten eliminar advertencias de seguridad.
    - Indispensables en sitios accesibles desde Internet.

### 2.3 Módulos necesarios en Apache2

-   mod_ssl:
   Es el módulo principal para habilitar SSL/TLS en Apache.
-   mod_headers:Permite añadir cabeceras de seguridad como HSTS.
-   mod_rewrite:Facilita reglas para redirigir tráfico HTTP a HTTPS.

## 3. Ejecución técnica

### 3.1 Instalación de Apache2

    sudo apt update
    sudo apt install apache2 -y
    sudo systemctl status apache2
Esta instalado, por lo que solo comprobamos:
![captura](https://github.com/AngelCSR/Portfolio/blob/main/Tema%203/imagenes/captura1.png)

### 3.2 Habilitar módulos

    sudo a2enmod ssl
    sudo a2enmod headers
    sudo a2enmod rewrite
    sudo systemctl restart apache2
![captura](https://github.com/AngelCSR/Portfolio/blob/main/Tema%203/imagenes/captura2.png)


### 3.3 Generación de certificado SSL/TLS

#### Opción A: Autofirmado
Al ser para pruebas en clase vamos a utilizar est
    sudo mkdir -p /etc/apache2/ssl
    sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/apache2/ssl/server.key -out /etc/apache2/ssl/server.crt
![captura](https://github.com/AngelCSR/Portfolio/blob/main/Tema%203/imagenes/captura3.png)
![captura](https://github.com/AngelCSR/Portfolio/blob/main/Tema%203/imagenes/captura4.png)


#### Opción B: Let's Encrypt

    sudo apt install certbot python3-certbot-apache -y
    sudo certbot --apache


### 3.4 Configuración VirtualHost HTTPS

    <VirtualHost *:443>
        ServerName yourdomain.com
        DocumentRoot /var/www/html
        SSLEngine on
        SSLCertificateFile /etc/apache2/ssl/server.crt
        SSLCertificateKeyFile /etc/apache2/ssl/server.key
    </VirtualHost>
![captura](https://github.com/AngelCSR/Portfolio/blob/main/Tema%203/imagenes/captura5.png)

Activamos el sitio SSL

    sudo systemctl reload apache2
    sudo a2ensite ssl-virtualhost.conf
    

![captura](https://github.com/AngelCSR/Portfolio/blob/main/Tema%203/imagenes/captura6.png)

### 3.5 Redirección HTTP→HTTPS

Editar sitio por defecto HTTP:

    sudo nano /etc/apache2/sites-available/000-default.conf

Añadir dentro del <VirtualHost *:80>:

    RewriteEngine On
    RewriteCond %{HTTPS} off
    RewriteRule ^(.*)$ https://%{HTTP_HOST}$1 [R=301,L]
 ![captura](https://github.com/AngelCSR/Portfolio/blob/main/Tema%203/imagenes/captura7.png)
  
Recargar:    

    sudo systemctl restart apache2

## 4. Validación

    curl -I https://192.168.21.204

Desde navegador:

  Accede a:

    https://192.168.21.204
Verás advertencia → pulsa “Avanzado” → “Aceptar el riesgo”.
![captura](https://github.com/AngelCSR/Portfolio/blob/main/Tema%203/imagenes/captura8.png)
![captura](https://github.com/AngelCSR/Portfolio/blob/main/Tema%203/imagenes/captura9.png)
![captura](https://github.com/AngelCSR/Portfolio/blob/main/Tema%203/imagenes/captura10.png)
![captura](https://github.com/AngelCSR/Portfolio/blob/main/Tema%203/imagenes/captura11.png)

Tambien podemos hacceder a localhost
![captura](https://github.com/AngelCSR/Portfolio/blob/main/Tema%203/imagenes/captura12.png)
![captura](https://github.com/AngelCSR/Portfolio/blob/main/Tema%203/imagenes/captura13.png)

## 5. Conclusiones

La implementación de HTTPS mediante un certificado autofirmado en Apache2 ha permitido comprender el proceso completo para añadir seguridad a un servidor web en Ubuntu. A lo largo de la práctica se han configurado los módulos necesarios, se ha generado un certificado SSL/TLS funcional y se ha creado un VirtualHost para servir contenido cifrado a través del puerto 443.

Aunque un certificado autofirmado no es reconocido como confiable por los navegadores, cumple perfectamente su finalidad educativa y demuestra que la comunicación puede establecerse de forma segura. Durante la práctica también se configuró la redirección automática desde HTTP a HTTPS, asegurando que todos los usuarios utilicen siempre el canal cifrado.

El proceso ayuda a comprender cómo funciona el protocolo HTTPS internamente, qué papel desempeñan los certificados digitales y cómo Apache gestiona la seguridad. Además, la verificación con navegador y herramientas como curl confirma que el servidor responde correctamente por HTTPS.

En general, la práctica proporciona una base sólida para futuras implementaciones con certificados de autoridades certificadoras reales como Let’s Encrypt, donde la seguridad queda completamente validada sin advertencias. El conocimiento adquirido aquí es fundamental para administrar servidores web modernos y garantizar comunicaciones seguras.
