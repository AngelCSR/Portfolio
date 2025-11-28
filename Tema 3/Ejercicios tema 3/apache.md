# 🏫 Instalación y Configuración de Apache 2 en Ubuntu 24.04

## 📑 ÍNDICE

1. 🏫 Introducción
   * [Contexto](#contexto)
   * [Motivación](#motivación)

2. ⚙️ Configuración inicial del servidor
   * [Actualizar el sistema](#actualizar-el-sistema)
   * [Instalar Apache 2](#instalar-apache-2)
   * [Verificar la instalación](#verificar-la-instalación)
   * [Configurar el usuario y grupo de Apache](#configurar-el-usuario-y-grupo-de-apache)
   * [Configurar el directorio raíz](#configurar-el-directorio-raíz)
   * [Habilitar módulos de Apache](#habilitar-módulos-de-apache)
   * [Establecer permisos del directorio](#establecer-permisos-del-directorio)
   * [Reiniciar Apache](#reiniciar-apache)
   * [Comprobación Apache](#comprobación-apache)

3. 🌐 Creación de una página web personalizada
   * [Accedemos al directorio raíz](#accedemos-al-directorio-raíz)
   * [Eliminamos el archivo de ejemplo](#eliminamos-el-archivo-de-ejemplo)
   * [Creamos nuestro propio index.html](#creamos-nuestro-propio-indexhtml)
   * [Contenido personalizado](#contenido-personalizado)
   * [Prueba en el navegador](#prueba-en-el-navegador)

4. 🧩 Configuración de un Virtual Host
   * [Accedemos al directorio](#accedemos-al-directorio)
   * [Copiamos la configuración base](#copiamos-la-configuración-base)
   * [Editamos el nuevo archivo](#editamos-el-nuevo-archivo)
   * [Creamos el directorio raíz](#creamos-el-directorio-raíz)
   * [Activación del Virtual Host](#activación-del-virtual-host)
   * [Modificación del archivo /etc/hosts](#modificación-del-archivo-etchosts)
   * [Pruebas de acceso](#pruebas-de-acceso)

5. 🔐 Implementación adicional: Control de acceso
   * [Crear archivo de contraseñas](#crear-archivo-de-contraseñas)
   * [Crear archivo .htaccess](#crear-archivo-htaccess)
   * [Reiniciar Apache](#reinicio-del-servicio-apache)
   * [Probar el acceso desde otro equipo](#banco-de-pruebas)

6. 📊 Resultados y valoración
   * [Resultados obtenidos](#resultados-obtenidos)
   * [Valoración técnica](#valoración-técnica)
   * [Valoración personal](#valoración-personal)

7. 🧩 Conclusión

8. 📚 Bibliografía

---

## 🏫 Introducción

### Contexto
<a name="contexto"></a>
Este trabajo se realiza en el módulo de **Despliegue de Aplicaciones Web** del segundo curso del ciclo formativo de **Desarrollo de Aplicaciones Web (2º DAW)**.  
El objetivo de la práctica es instalar y configurar el servidor web **Apache 2** en un sistema operativo **Ubuntu 24.04**, comprendiendo su funcionamiento y los pasos necesarios para dejarlo operativo.

#### ¿Qué es Apache?
**Apache HTTP Server** es un servidor web de código abierto desarrollado por la *Apache Software Foundation*.  
Es una de las tecnologías más utilizadas para alojar sitios web y aplicaciones, ya que permite servir contenido mediante el protocolo **HTTP/HTTPS**.  
Su arquitectura modular y su gran compatibilidad con distintos lenguajes (como PHP o Python) lo hacen muy versátil.  
Surgió en 1995 y sigue siendo una pieza clave en la infraestructura de Internet.

**Alternativas a Apache:**
- **Nginx:** más ligero y rápido en conexiones simultáneas.  
- **Lighttpd:** servidor eficiente y minimalista.  
- **Caddy:** moderno y con HTTPS automático.  
- **IIS (Microsoft):** integrado en Windows Server.

### Motivación
<a name="motivación"></a>
El propósito de este proyecto es aprender el proceso completo de **instalación, configuración y verificación de un servidor web real**, utilizando Apache como ejemplo.  
Comprender cómo se despliega y configura un servicio HTTP es esencial para el perfil profesional del desarrollador web, ya que permite **publicar aplicaciones, probar proyectos en entorno real y gestionar servidores Linux**.

---

## ⚙️ Configuración inicial del servidor

### Actualizar el sistema
<a name="actualizar-el-sistema"></a>
```bash
sudo apt update
sudo apt upgrade -y
Instalar Apache 2
<a name="instalar-apache-2"></a>

bash
Copiar código
sudo apt install apache2 -y
Verificar la instalación
<a name="verificar-la-instalación"></a>

bash
Copiar código
hostname -I


Acceder a http://localhost para confirmar la página de bienvenida.


Configurar el usuario y grupo de Apache
<a name="configurar-el-usuario-y-grupo-de-apache"></a>

bash
Copiar código
sudo nano /etc/apache2/envvars
Modificar:

arduino
Copiar código
export APACHE_RUN_USER=angel
export APACHE_RUN_GROUP=angel
Configurar el directorio raíz
<a name="configurar-el-directorio-raíz"></a>

bash
Copiar código
sudo nano /etc/apache2/apache2.conf
Contenido:

apache
Copiar código
<Directory /var/www/>
    Options Indexes FollowSymLinks
    AllowOverride All
    Require all granted
</Directory>
Habilitar módulos de Apache
<a name="habilitar-módulos-de-apache"></a>

bash
Copiar código
sudo a2enmod headers
sudo a2enmod rewrite
Establecer permisos del directorio
<a name="establecer-permisos-del-directorio"></a>

bash
Copiar código
sudo chown -R $USER:$USER /var/www/html
Reiniciar Apache
<a name="reiniciar-apache"></a>

bash
Copiar código
sudo systemctl restart apache2
Comprobación Apache
<a name="comprobación-apache"></a>

bash
Copiar código
sudo systemctl status apache2


🌐 Creación de una página web personalizada
Accedemos al directorio raíz
<a name="accedemos-al-directorio-raíz"></a>

bash
Copiar código
cd /var/www/html
Eliminamos el archivo de ejemplo
<a name="eliminamos-el-archivo-de-ejemplo"></a>

bash
Copiar código
sudo rm index.html
Creamos nuestro propio index.html
<a name="creamos-nuestro-propio-indexhtml"></a>

bash
Copiar código
sudo nano index.html


Contenido personalizado
<a name="contenido-personalizado"></a>

html
Copiar código
<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>Servidor Apache de Ángel</title>
    <style>
        body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(to right, #74ebd5, #ACB6E5);
            text-align: center;
            padding-top: 100px;
            animation: fadeIn 2s ease-in;
            color: #fff;
        }
        h1 {
            color: #ffffff;
            font-size: 3em;
            margin-bottom: 20px;
            text-shadow: 2px 2px #2e86de;
        }
        p {
            font-size: 1.2em;
            color: #f0f0f0;
        }
        .emoji {
            font-size: 2em;
            animation: bounce 1.5s infinite;
        }
    </style>
</head>
<body>
    <h1>🚀 ¡Bienvenido a mi servidor Apache!</h1>
    <p>Servidor configurado correctamente en <strong>Ubuntu 24.04</strong> por Ángel 🖥️</p>
</body>
</html>


Prueba en el navegador
<a name="prueba-en-el-navegador"></a>
Abrimos en el navegador: http://localhost
Si todo está correcto, se mostrará la página personalizada.


🧩 Configuración de un Virtual Host
Accedemos al directorio
<a name="accedemos-al-directorio"></a>

bash
Copiar código
cd /etc/apache2/sites-available/


Copiamos la configuración base
<a name="copiamos-la-configuración-base"></a>

bash
Copiar código
sudo cp 000-default.conf gci.conf
Editamos el nuevo archivo
<a name="editamos-el-nuevo-archivo"></a>

bash
Copiar código
sudo nano /etc/apache2/sites-available/gci.conf
Configurar:

swift
Copiar código
ServerAdmin angelcamposanchezrey@gmail.com
DocumentRoot /var/www/gci/
ServerName gci.example.com


Creamos el directorio raíz
<a name="creamos-el-directorio-raíz"></a>

bash
Copiar código
sudo mkdir -p /var/www/gci
sudo chown -R angel:angel /var/www/gci
Activación del Virtual Host
<a name="activación-del-virtual-host"></a>

bash
Copiar código
sudo a2ensite gci.conf
sudo systemctl reload apache2



Modificación del archivo /etc/hosts
<a name="modificación-del-archivo-etchosts"></a>

text
Copiar código
127.0.0.1   localhost
127.0.1.1   angel-VirtualBox
127.0.0.1   gci.example.com


Pruebas de acceso
<a name="pruebas-de-acceso"></a>
Abrir http://gci.example.com


🔐 Implementación adicional: Control de acceso
Crear archivo de contraseñas
<a name="crear-archivo-de-contraseñas"></a>

bash
Copiar código
sudo htpasswd -c /etc/apache2/.htpasswd angel
Crear archivo .htaccess
<a name="crear-archivo-htaccess"></a>
En /var/www/gci:

bash
Copiar código
AuthType Basic
AuthName "Zona Restringida"
AuthUserFile /etc/apache2/.htpasswd
Require valid-user
Reinicio del servicio Apache
<a name="reinicio-del-servicio-apache"></a>

bash
Copiar código
sudo systemctl restart apache2
Banco de pruebas
<a name="banco-de-pruebas"></a>

Acceso desde otro ordenador de la red local.

Verificación de autenticación: solo usuarios válidos pueden acceder.

Logs:

bash
Copiar código
sudo tail -f /var/log/apache2/access.log
sudo tail -f /var/log/apache2/error.log



📊 Resultados y valoración
Resultados obtenidos
<a name="resultados-obtenidos"></a>

Apache 2 instalado correctamente.

Página personalizada creada.

VirtualHost funcional configurado.

Control de acceso implementado.

Valoración técnica
<a name="valoración-técnica"></a>
El proceso fue fluido, aunque con algunos errores, y permitió comprender a fondo la configuración de Apache en Ubuntu.

Valoración personal
<a name="valoración-personal"></a>
Fue una práctica muy completa.
Los problemas menores de permisos se solucionaron.
La parte de seguridad fue especialmente interesante.
