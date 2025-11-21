# Implementación de HTTPS en Apache2 sobre Ubuntu

## 1. Introducción

El objetivo de esta práctica es investigar, configurar e implementar el
protocolo HTTPS en un servidor web Apache2 ejecutándose sobre Ubuntu...

## 2. Investigación

### 2.1 Funcionamiento del protocolo HTTPS y su importancia

HTTPS utiliza SSL/TLS para cifrar la comunicación entre cliente y
servidor, garantizando confidencialidad, integridad y autenticidad.

### 2.2 Tipos de certificados SSL/TLS

-   **Autofirmado:** útil para pruebas, no confiable por navegadores.
-   **CA confiable:** reconocido por navegadores; Let's Encrypt es
    gratuito.

### 2.3 Módulos necesarios en Apache2

-   mod_ssl
-   mod_headers
-   mod_rewrite

## 3. Ejecución técnica

### 3.1 Instalación de Apache2

    sudo apt update
    sudo apt install apache2 -y
    sudo systemctl status apache2

### 3.2 Habilitar módulos

    sudo a2enmod ssl
    sudo a2enmod headers
    sudo a2enmod rewrite
    sudo systemctl restart apache2

### 3.3 Generación de certificado SSL/TLS

#### Opción A: Autofirmado

    sudo mkdir -p /etc/apache2/ssl
    sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout /etc/apache2/ssl/server.key -out /etc/apache2/ssl/server.crt

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

### 3.5 Redirección HTTP→HTTPS

    RewriteEngine On
    RewriteCond %{HTTPS} off
    RewriteRule ^(.*)$ https://%{HTTP_HOST}$1 [R=301,L]

## 4. Validación

    curl -I https://yourdomain.com

## 5. Conclusiones

HTTPS garantiza la seguridad mediante SSL/TLS. Let's Encrypt simplifica
la configuración y automatiza la renovación. Apache2 permite una
implementación robusta con los módulos adecuados.
