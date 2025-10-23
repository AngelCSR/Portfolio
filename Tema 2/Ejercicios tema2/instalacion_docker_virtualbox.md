# 1. Instalación de Ubuntu en VirtualBox

Para comenzar con la virtualización, se realizó la instalación de **Ubuntu** como sistema operativo invitado dentro de **VirtualBox**.  
A continuación se describen los pasos seguidos:

### Creación de una nueva máquina virtual
1. Abrir **VirtualBox** y hacer clic en **“Nueva”**.  
2. Asignar un nombre y seleccionar el tipo **“Linux”** y la versión **“Ubuntu (64-bit)”**.

### Configuración de la memoria RAM y el disco duro virtual
- Asignar al menos **2 GB de RAM** (recomendado **4 GB**).  
- Crear un disco duro virtual de tipo **VDI** con tamaño **dinámico** y un mínimo de **25 GB**.

### Carga del archivo ISO de Ubuntu
- En la configuración de la máquina virtual, seleccionar el archivo **ISO** de instalación de Ubuntu.

### Inicio del proceso de instalación
1. Iniciar la máquina virtual y seguir el asistente de instalación de Ubuntu.  
2. Seleccionar el idioma, zona horaria y crear el usuario principal.

### Configuración inicial del sistema
- Completar la instalación.


![foto1](https://github.com/AngelCSR/Portfolio/blob/main/Tema%202/imagenes/foto1.png)


---

# 2. Instalación de Docker Desktop en Ubuntu

Una vez instalado Ubuntu, se procedió a la instalación de **Docker Desktop**, una herramienta que permite crear y gestionar contenedores fácilmente.  
El proceso se desarrolló en varios pasos:

### Desinstalar versiones antiguas (si las hay)
En este cas no las hay, pero lo hacemos.
```bash
sudo apt remove docker docker-engine docker.io containerd runc
```
![foto2](https://github.com/AngelCSR/Portfolio/blob/main/Tema%202/imagenes/foto2.png)
### Actualizar los paquetes del sistema
```bash
sudo apt update
sudo apt upgrade -y
```
![foto](https://github.com/AngelCSR/Portfolio/blob/main/Tema%202/imagenes/foto3.png)


![foto](https://github.com/AngelCSR/Portfolio/blob/main/Tema%202/imagenes/foto4.png)
### Instalar dependencias necesarias
```bash
sudo apt install -y ca-certificates curl gnupg lsb-release
```
![foto](https://github.com/AngelCSR/Portfolio/blob/main/Tema%202/imagenes/foto5.png)

### Agregar la clave GPG oficial de Docker
```bash
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```
![foto](https://github.com/AngelCSR/Portfolio/blob/main/Tema%202/imagenes/foto6.png)


### Agregar el repositorio oficial de Docker
```bash
echo "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt update
```
![foto](https://github.com/AngelCSR/Portfolio/blob/main/Tema%202/imagenes/foto7.png)

### Instalar Docker Engine, CLI y containerd
```bash
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
![foto](https://github.com/AngelCSR/Portfolio/blob/main/Tema%202/imagenes/foto9.png)

### Verificar la instalación
```bash
sudo docker run hello-world
```
![foto](https://github.com/AngelCSR/Portfolio/blob/main/Tema%202/imagenes/foto10.png)

Si la instalación fue exitosa, se mostrará un mensaje de confirmación.

### Ejecutar Docker sin sudo
Se configura el usuario actual para usar Docker sin privilegios de administrador.
![foto](https://github.com/AngelCSR/Portfolio/blob/main/Tema%202/imagenes/foto11.png)
![foto](https://github.com/AngelCSR/Portfolio/blob/main/Tema%202/imagenes/foto12.png)

---

# 3. Creación y ejecución de contenedores

Con Docker instalado, se procedió a crear contenedores para ejecutar servicios web y de aplicaciones.  
En este caso, se usaron **Nginx** (servidor web) y **Tomcat** (servidor de aplicaciones).

### Buscar imágenes disponibles
```bash
docker search nginx
docker search tomcat
```
![foto](https://github.com/AngelCSR/Portfolio/blob/main/Tema%202/imagenes/foto13.png)
![foto](https://github.com/AngelCSR/Portfolio/blob/main/Tema%202/imagenes/foto14.png)

### Descargar e iniciar los contenedores
```bash
docker run -d -p 8080:80 --name webserver nginx
docker run -d -p 8081:8080 --name appserver tomcat
```
![foto](https://github.com/AngelCSR/Portfolio/blob/main/Tema%202/imagenes/foto15.png)
![foto](https://github.com/AngelCSR/Portfolio/blob/main/Tema%202/imagenes/foto16.png)

### Verificar contenedores activos
```bash
docker ps
```
![foto](https://github.com/AngelCSR/Portfolio/blob/main/Tema%202/imagenes/foto17.png)


### Probar los servicios en el navegador
- **http://localhost:8080** → Servidor web **Nginx**
- **http://localhost:8081** → Servidor de aplicaciones **Tomcat**

---
![foto](https://github.com/AngelCSR/Portfolio/blob/main/Tema%202/imagenes/foto18.png)
![foto](https://github.com/AngelCSR/Portfolio/blob/main/Tema%202/imagenes/foto19.png)

# 4. Requerimientos mínimos para implantar una aplicación web

Para desplegar una aplicación web mediante contenedores, es necesario contar con ciertos requisitos a nivel de hardware, software y red.

### Requisitos de hardware y software

**Hardware mínimo:**
- CPU de **2 núcleos** (4 recomendados)
- **4 GB de RAM** (8 GB recomendados)
- **20 GB de almacenamiento libre**

**Software necesario:**
- **Ubuntu 22.04 LTS** o superior
- **Docker Engine** y **Docker Compose**
- Navegador web actualizado (**Firefox**, **Chrome**, etc.)

### Infraestructura de red
- Acceso a **Internet** para descargar imágenes desde Docker Hub.
- Configuración de **puertos abiertos** (por ejemplo, 80, 8080, 443).
- Creación de **redes internas de Docker** para comunicación entre contenedores.

### Configuración del servidor web y de aplicaciones
- Contenedor **Nginx** configurado para servir contenido estático.
- Contenedor **Tomcat** encargado de la lógica de negocio.
- Ambos contenedores conectados a una misma **red Docker**.

### Seguridad y mantenimiento
- Actualizar imágenes regularmente con `docker pull`.
- Limitar permisos de ejecución de los contenedores.
- Configurar **HTTPS** mediante certificados **SSL/TLS**.
- Realizar **copias de seguridad** de volúmenes y bases de datos.
- **Monitorizar logs** y rendimiento del sistema.

---

# 5. Conclusión

La virtualización con **VirtualBox** y la gestión de contenedores mediante **Docker** permiten crear entornos de desarrollo reproducibles y escalables.  
Durante este proceso, se aprendió a:

- Instalar **Ubuntu** en una máquina virtual.
- Instalar y configurar **Docker Desktop**.
- Crear contenedores para servidores web y de aplicaciones.
- Comprender los requisitos y buenas prácticas para desplegar aplicaciones web.



---

# 6. Bibliografía

- [Documentación oficial de Docker](https://docs.docker.com/)
- [Documentación de Ubuntu](https://ubuntu.com/docs)
- Material de clase de **Virtualización - 2ºDAW**
