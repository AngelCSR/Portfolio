# 🏫 Instalación y Configuración de Apache 2 en Ubuntu 24.04

## 📑 ÍNDICE

1. 🏫 Introducción
   * [Contexto](#contexto)
   * [Motivación](#motivación)

2. ⚙️ Configuración inicial del servidor
   * [1. Actualizar el sistema](#1-actualizar-el-sistema)
   * [2. Instalar Apache 2](#2-instalar-apache-2)
   * [3. Verificar la instalación](#3-verificar-la-instalación)
   * [4. Configurar el usuario y grupo de Apache](#4-configurar-el-usuario-y-grupo-de-apache)
   * [5. Configurar el directorio raíz](#5-configurar-el-directorio-raíz)
   * [6. Habilitar módulos de Apache](#6-habilitar-módulos-de-apache)
   * [7. Establecer permisos del directorio](#7-establecer-permisos-del-directorio)
   * [8. Reiniciar Apache](#8-reiniciar-apache)
   * [9. Comprobación Apache](#9-comprobación-apache)

3. 🌐 Creación de una página web personalizada
   * [Acceder al directorio raíz](#accedemos-al-directorio-raíz)
   * [Eliminación de la página predeterminada](#eliminación-de-la-página-predeterminada)
   * [Creación del nuevo index.html](#creamos-nuestro-propio-indexhtml)
   * [Prueba en el navegador](#si-todo-está-correcto-se-mostrará-la-página-personalizada)

4. 🧩 Configuración de un Virtual Host
   * [Acceso al directorio de configuración](#accedemos-al-directorio)
   * [Copia de la configuración por defecto](#copiamos-la-configuración-base)
   * [Creación del archivo gci.conf](#editamos-el-nuevo-archivo)
   * [Definición de directivas](#configuramos)
   * [Creación del directorio raíz](#creamos-el-directorio-raíz)
   * [Activación del Virtual Host](#4-activación-del-archivo-virtualhost)
   * [Modificación de /etc/hosts](#editamos-etchosts)

5. 🔐 Implementación adicional: Control de acceso
   * [Creación del archivo .htpasswd](#crear-archivo-de-contraseñas)
   * [Configuración del archivo .htaccess](#en-varwwwgci-crear-htaccess)
   * [Reinicio del servicio Apache](#reiniciar-apache)
   * [Banco de pruebas](#probar-el-acceso-desde-otro-equipo-en-la-red)

6. 📊 Resultados y valoración
   * [Resultados obtenidos](#resultados-obtenidos)
   * [Valoración técnica](#valoración-técnica)
   * [Valoración personal](#valoración-personal)

7. 🧩 Conclusión

8. 📚 Bibliografía

---

## 🏫 Introducción

### Contexto

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

El propósito de este proyecto es aprender el proceso completo de **instalación, configuración y verificación de un servidor web real**, utilizando Apache como ejemplo.  
Comprender cómo se despliega y configura un servicio HTTP es esencial para el perfil profesional del desarrollador web, ya que permite **publicar aplicaciones, probar proyectos en entorno real y gestionar servidores Linux**.

---

## ⚙️ 1. Configuración inicial del servidor

Durante la práctica se siguieron los pasos descritos a continuación, para instalar y poner en marcha Apache 2 en Ubuntu 24.04:


### 1. Actualizar el sistema
```bash
sudo apt update
sudo apt upgrade -y
```

### 2. Instalar Apache 2
```bash
sudo apt install apache2 -y
```

### 3. Verificar la instalación
Para comprobar que el servicio está activo y en ejecución:
```bash
hostname -I
```
![captura](https://github.com/AngelCSR/Portfolio/blob/main/Tema%203/imagenes/foto1.png)

Y acceder a `http://localhost` para confirmar la página de bienvenida.
![captura](https://github.com/AngelCSR/Portfolio/blob/main/Tema%203/imagenes/foto2.png)

### 4. Configurar el usuario y grupo de Apache
```bash
sudo nano /etc/apache2/envvars
```
Modificar:
```
export APACHE_RUN_USER=angel
export APACHE_RUN_GROUP=angel
```

### 5. Configurar el directorio raíz
```bash
sudo nano /etc/apache2/apache2.conf
```
Contenido:
```apache
<Directory /var/www/>
    Options Indexes FollowSymLinks
    AllowOverride All
    Require all granted
</Directory>
```

### 6. Habilitar módulos de Apache
```bash
sudo a2enmod headers
sudo a2enmod rewrite
```

###  7. Establecer permisos del directorio
```bash
sudo chown -R $USER:$USER /var/www/html
```

### 8. Reiniciar Apache
```bash
sudo systemctl restart apache2
```

### 9. Comprobación Apache
```bash
sudo systemctl status apache2
```
![captura](https://github.com/AngelCSR/Portfolio/blob/main/Tema%203/imagenes/foto3.png)

---

## 2. Creación de una página web personalizada

1. Accedemos al directorio raíz:
```bash
cd /var/www/html
```

2. Eliminamos el archivo de ejemplo:
```bash
sudo rm index.html
```

3. Creamos nuestro propio `index.html`:
![captura](https://github.com/AngelCSR/Portfolio/blob/main/Tema%203/imagenes/foto4.png)

```bash
sudo nano index.html
```


4. Contenido personalizado:
```html
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
```
![captura](https://github.com/AngelCSR/Portfolio/blob/main/Tema%203/imagenes/foto5.png)

Abrimos en el navegador:  
👉 `http://localhost`

---
Si todo está correcto, se mostrará la página personalizada.
![captura](https://github.com/AngelCSR/Portfolio/blob/main/Tema%203/imagenes/foto6.png)



## 3. Configuración de un Virtual Host

1. Accedemos al directorio:
```bash
cd /etc/apache2/sites-available/
```
       
Desde aquí se gestionan los diferentes Virtual Hosts que Apache puede servir.
![captura](https://github.com/AngelCSR/Portfolio/blob/main/Tema%203/imagenes/fotoo.png)

2. Copiamos la configuración base:
```bash
sudo cp 000-default.conf gci.conf
```

3. Editamos el nuevo archivo:
```bash
sudo nano /etc/apache2/sites-available/gci.conf
```

Configuramos:
```
ServerAdmin angelcamposanchezrey@gmail.com
DocumentRoot /var/www/gci/
ServerName gci.example.com
```
![captura](https://github.com/AngelCSR/Portfolio/blob/main/Tema%203/imagenes/foto7.png)

4. Creamos el directorio raíz:
```bash
sudo mkdir -p /var/www/gci
sudo chown -R angel:angel /var/www/gci
```

---


## 4. Activación del archivo VirtualHost

```bash
sudo a2ensite gci.conf
```
![captura](https://github.com/AngelCSR/Portfolio/blob/main/Tema%203/imagenes/foto8.png)

```bash

sudo systemctl reload apache2
```
No funciona

![captura](https://github.com/AngelCSR/Portfolio/blob/main/Tema%203/imagenes/foto9.png)


Editamos `/etc/hosts`:
```
127.0.0.1   localhost
127.0.1.1   angel-VirtualBox
127.0.0.1   gci.example.com
```
![captura](https://github.com/AngelCSR/Portfolio/blob/main/Tema%203/imagenes/foto10.png)

El archivo /etc/hosts permite asociar nombres de dominio locales con direcciones IP.
Al añadir:

    127.0.0.1   gci.example.com


le estamos diciendo al sistema que cada vez que se escriba http://gci.example.com en el navegador, apunte a la IP local (tu servidor Apache en el propio equipo).



Reiniciar Apache:
```bash
sudo systemctl restart apache2
```

Y probar:  
👉 `http://gci.example.com`

---
Funciona!
![captura](https://github.com/AngelCSR/Portfolio/blob/main/Tema%203/imagenes/fotogit.png)


## 5. Implementación adicional: Control de acceso

1. Crear archivo de contraseñas:
```bash
sudo htpasswd -c /etc/apache2/.htpasswd angel
```

2. En `/var/www/gci` crear `.htaccess`:
```
AuthType Basic
AuthName "Zona Restringida"
AuthUserFile /etc/apache2/.htpasswd
Require valid-user
```

3. Reiniciar Apache:
```bash
sudo systemctl restart apache2
```

4. Probar el acceso desde otro equipo en la red.  
Solo los usuarios definidos en `.htpasswd` podrán entrar.
    1. Acceso desde otro ordenador de la red local, un compañero (Diego)realizó un intento de acceso desde otro equipo para confirmar la disponibilidad y el correcto           funcionamiento del control de acceso.
    2.  (http://gci.example.com) o .(http://gci.example2.com)(otra sencilla que he hecho)
    3. Verificación de autenticación: se comprobó que el acceso solo se permite tras introducir usuario y contraseña válidos.

**Ver logs:**
```bash
sudo tail -f /var/log/apache2/access.log
sudo tail -f /var/log/apache2/error.log
```

---
![captura](https://github.com/AngelCSR/Portfolio/blob/main/Tema%203/imagenes/foto12.png)
![captura](https://github.com/AngelCSR/Portfolio/blob/main/Tema%203/imagenes/foto13.png)

## 6. Resultados y valoración

**Resultados obtenidos:**
- Apache 2 instalado correctamente.  
- Página personalizada creada.  
- VirtualHost funcional configurado.  
- Control de acceso implementado.  

**Valoración técnica:**  
El proceso fue fluido, aunque con algunos errores, y permitió comprender a fondo la configuración de Apache en Ubuntu.

**Valoración personal:**  
Fue una práctica muy completa.  
Los problemas menores de permisos se solucionaron.  
La parte de seguridad fue especialmente interesante.

---

## 7. Conclusión

Apache es una herramienta esencial en el desarrollo web.  
Su instalación en Ubuntu 24.04 permite entender conceptos clave de administración de servidores, permisos, y despliegue de sitios web.  
Esta práctica refuerza la importancia del software libre en la formación técnica.

---

## 8. Bibliografía

- [Ubuntu Tutorials – Install and Configure Apache](https://ubuntu.com/tutorials/install-and-configure-apache)  
- [Apache HTTP Server Documentation](https://httpd.apache.org/docs/)  
- [DigitalOcean – Password Authentication with Apache](https://www.digitalocean.com/community/tutorials/apache-password-authentication)  
- [Apache Software Foundation](https://httpd.apache.org/)  
- [Ubuntu Server Docs](https://ubuntu.com/server/docs)  
- [Wikipedia – Apache HTTP Server](https://es.wikipedia.org/wiki/Apache_HTTP_Server)  
- Apuntes personales y práctica de clase (2º DAW – Despliegue de Aplicaciones Web)
