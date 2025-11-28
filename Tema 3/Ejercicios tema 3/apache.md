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
   * [Accedemos al directorio de configuración](#accedemos-al-directorio-de-configuración)
   * [Copia de la configuración base](#copia-de-la-configuración-base)
   * [Editamos el nuevo archivo](#editamos-el-nuevo-archivo)
   * [Creamos el directorio raíz](#creamos-el-directorio-raíz)
   * [Activación del Virtual Host](#activación-del-virtual-host)
   * [Modificación del archivo /etc/hosts](#modificación-del-archivo-etchosts)
   * [Pruebas de acceso](#pruebas-de-acceso)

5. 🔐 Implementación adicional: Control de acceso
   * [Crear archivo de contraseñas](#crear-archivo-de-contraseñas)
   * [Crear archivo .htaccess](#crear-archivo-htaccess)
   * [Reinicio del servicio Apache](#reinicio-del-servicio-apache)
   * [Banco de pruebas](#banco-de-pruebas)

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
