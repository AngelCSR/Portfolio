# Configuración de acceso autenticado a Tomcat Manager con HTTPS

## 1. Crear usuario y roles

Editar `tomcat-users.xml`:

```bash
sudo nano /opt/tomcat/latest/conf/tomcat-users.xml
```

Añadir o modificar:

```xml
<tomcat-users>
    <role rolename="manager-gui"/>
    <role rolename="manager-script"/>
    <role rolename="admin-gui"/>
    <user username="angel" password="angel" roles="manager-gui,manager-script,admin-gui"/>
</tomcat-users>
```
![captura](https://github.com/AngelCSR/Portfolio/blob/main/Tema4/imagenes/Configuraci%C3%B3n-de-seguridad-en-Tomcat/Definir-roles-y-usuario.png)


Guardar y salir (`CTRL+O`, `ENTER`, `CTRL+X`).

---

## 2. Verificar restricciones en el Manager

Editar `web.xml`:

```bash
sudo nano /opt/tomcat/latest/webapps/manager/WEB-INF/web.xml
```

Asegurarse de que existan bloques como:

```xml
<security-constraint>
    <web-resource-collection>
        <web-resource-name>Manager</web-resource-name>
        <url-pattern>/html/*</url-pattern>
    </web-resource-collection>
    <auth-constraint>
        <role-name>manager-gui</role-name>
    </auth-constraint>
</security-constraint>

<security-constraint>
    <web-resource-collection>
        <web-resource-name>Manager Script</web-resource-name>
        <url-pattern>/text/*</url-pattern>
    </web-resource-collection>
    <auth-constraint>
        <role-name>manager-script</role-name>
    </auth-constraint>
</security-constraint>
```
![captura](https://github.com/AngelCSR/Portfolio/blob/main/Tema4/imagenes/Configuraci%C3%B3n-de-seguridad-en-Tomcat/Verificar-restricciones-en-el-Manager.png)

---

## 3. Generar keystore para HTTPS

```bash
sudo keytool -genkey -alias tomcat -keyalg RSA -keystore /opt/tomcat/latest/conf/keystore.jks -validity 3650
```

* Contraseña: `angel24`
* Completar datos de la organización (puedes usar defaults o locales).

Resultado: `/opt/tomcat/latest/conf/keystore.jks`

---

![captura](https://github.com/AngelCSR/Portfolio/blob/main/Tema4/imagenes/Configuraci%C3%B3n-de-seguridad-en-Tomcat/Generar-un-keystore(angel24).png)


## 4. Configurar conector HTTPS

Editar `server.xml`:

```bash
sudo nano /opt/tomcat/latest/conf/server.xml
```

Añadir o modificar:

```xml
<Connector port="8443" protocol="org.apache.coyote.http11.Http11NioProtocol"
           maxThreads="150" SSLEnabled="true">
    <SSLHostConfig>
        <Certificate certificateKeystoreFile="conf/keystore.jks"
                     certificateKeystorePassword="angel"
                     type="RSA"/>
    </SSLHostConfig>
</Connector>
```

Guardar y cerrar.

---
![captura](https://github.com/AngelCSR/Portfolio/blob/main/Tema4/imagenes/Configuraci%C3%B3n-de-seguridad-en-Tomcat/conector.png)

## 5. Reiniciar Tomcat

```bash
sudo systemctl restart tomcat
```

---

## 6. Acceso al Manager desde navegador

Abrir:

```
https://localhost:8443/manager/html
```

* Usuario: `angel`
* Contraseña: `angel`

> Nota: El navegador puede advertir sobre certificado auto-firmado, es normal.

---
![captura](https://github.com/AngelCSR/Portfolio/blob/main/Tema4/imagenes/Configuraci%C3%B3n-de-seguridad-en-Tomcat/ver2.png)
![captura](https://github.com/AngelCSR/Portfolio/blob/main/Tema4/imagenes/Configuraci%C3%B3n-de-seguridad-en-Tomcat/AccesoalManagerdesdenavegador0.png)
![captura](https://github.com/AngelCSR/Portfolio/blob/main/Tema4/imagenes/Configuraci%C3%B3n-de-seguridad-en-Tomcat/AccesoalManagerdesdenavegador1.png)




