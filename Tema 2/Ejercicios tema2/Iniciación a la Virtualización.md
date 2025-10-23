# Iniciación a la Virtualización  
**Autor:** Ángel Campo Sánchez-Rey  
**Curso:** 2º DAW  

---

## 1. Instalación de Ubuntu en VirtualBox

Para comenzar con la virtualización, se realizó la instalación de **Ubuntu** como sistema operativo invitado dentro de **VirtualBox**.  
A continuación se describen los pasos seguidos:

1. **Creación de una nueva máquina virtual.**
   - Abrir VirtualBox y hacer clic en “Nueva”.
   - Asignar un nombre y seleccionar el tipo “Linux” y la versión “Ubuntu (64-bit)”.

2. **Configuración de la memoria RAM y el disco duro virtual.**
   - Se recomienda asignar al menos 2 GB de RAM y 25 GB de espacio en disco.

3. **Carga del archivo ISO de Ubuntu.**
   - En la configuración de la máquina virtual, seleccionar la imagen ISO de Ubuntu descargada.

4. **Inicio de la instalación.**
   - Iniciar la máquina y seguir el asistente de instalación de Ubuntu.

5. **Configuración inicial del sistema.**
   - Crear usuario, establecer contraseña y realizar las actualizaciones iniciales.

![foto1](foto1.png)

---

## 2. Instalación de Docker Desktop en Ubuntu

Una vez instalado Ubuntu, se procedió a instalar **Docker Desktop** para gestionar contenedores.  
Los pasos seguidos fueron los siguientes:

### 1️⃣ Desinstalar versiones antiguas (si las hay)

```bash
sudo apt remove docker docker-engine docker.io containerd runc
