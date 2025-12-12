# Reverse Proxy Apache → Tomcat

## Configuración y verificación del funcionamiento

## 1️⃣ Activación de módulos necesarios en Apache

``` bash
sudo a2enmod proxy
sudo a2enmod proxy_http
sudo a2enmod proxy_ajp   # opcional, solo si se desea usar AJP
sudo systemctl restart apache2
```

## 2️⃣ Creación del VirtualHost para redirigir a Tomcat

Crear el archivo:

``` bash
sudo nano /etc/apache2/sites-available/tomcat.conf
```

Contenido del archivo:

``` apache
<VirtualHost *:80>
    ServerName localhost

    # Reverse proxy hacia Tomcat
    ProxyPass /sample http://localhost:8080/sample
    ProxyPassReverse /sample http://localhost:8080/sample
</VirtualHost>
```
Esto solo funciona para sample
## Redirigir todas las rutas hacia Tomcat automáticamente

### 1️⃣ Editar la configuración de Apache

Abrir el archivo de configuración:

```bash
sudo nano /etc/apache2/sites-available/tomcat.conf
```

### 2️⃣ Contenido del archivo

```apache
<VirtualHost *:80>
    ServerName localhost

    ProxyPreserveHost On

    ProxyPass / http://localhost:8080/
    ProxyPassReverse / http://localhost:8080/
</VirtualHost>
```

### 3️⃣ Recargar Apache

```bash
sudo systemctl reload apache2
```

### ✅ Resultado

Todas las aplicaciones desplegadas en Tomcat serán accesibles automáticamente a través de Apache sin necesidad de añadir cada ruta individualmente.


## 3️⃣ Activación del sitio y recarga de Apache

``` bash
sudo a2ensite tomcat.conf
sudo systemctl reload apache2
```

## 4️⃣ Verificación del funcionamiento

### Comprobación desde consola:

``` bash
curl http://localhost/sample
```

### Comprobación desde navegador:

http://localhost/sample

## 5️⃣ Resultado final

Apache funciona como **reverse proxy** para Tomcat.\
La aplicación `sample.war` es accesible desde Apache por el puerto
**80**, redirigiendo internamente a Tomcat en el puerto **8080**.
