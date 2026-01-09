# Documentación Final de Tomcat

## 1️ Arquitectura básica de Tomcat

Tomcat es un servidor de aplicaciones Java que implementa los estándares **Servlet** y **JSP**. Su arquitectura se divide en varios componentes principales:

* **Catalina**: Contenedor de servlets que maneja la ejecución de las aplicaciones web.
* **Coyote**: Conector HTTP que permite la comunicación entre clientes y Tomcat.
* **Jasper**: Compilador de JSP a servlets.
* **Manager y Host Manager**: Interfaces web para desplegar, detener, recargar aplicaciones y administrar hosts virtuales.

**Diagrama básico de flujo**:

```
Cliente HTTP --> Coyote (Conector) --> Catalina (Servlet Container) --> Aplicación Web
```

---

## 2️ Configuración del servidor

### Archivo principal: `server.xml`

Ubicación típica: `/opt/tomcat/latest/conf/server.xml`

Secciones importantes:

* **Connector**: Configura puerto, número de hilos (`maxThreads`), conexiones (`maxConnections`), tiempo de espera (`connectionTimeout`).
* **Host**: Define hosts virtuales y sus aplicaciones.

Ejemplo de conector optimizado:

```xml
<Connector port="8080"
    maxThreads="300"
    minSpareThreads="25"
    maxConnections="10000"
    acceptCount="1000"
    connectionTimeout="20000"
    keepAliveTimeout="15000"
    maxKeepAliveRequests="100" />
```

---

## 3️ Integración con servidor web (Reverse Proxy)

Apache HTTP Server puede actuar como **reverse proxy** hacia Tomcat:

1. Instalar Apache: `sudo apt install apache2`
2. Habilitar módulos: `proxy`, `proxy_http`
3. Configurar virtual host:

```apache
<VirtualHost *:80>
    ServerName localhost
    ProxyPass /sample http://localhost:8080/sample
    ProxyPassReverse /sample http://localhost:8080/sample
</VirtualHost>
```

4. Reiniciar Apache: `sudo systemctl restart apache2`

Permite balanceo, SSL y mejor control de peticiones.

---

## 4️ Seguridad aplicada

* Configurar **roles y usuarios** en `tomcat-users.xml`.
* Limitar el acceso a **Manager y Host Manager**.
* Deshabilitar directorios y recursos innecesarios.
* Configurar **SSL/TLS** para HTTPS.
* Mantener Java y Tomcat actualizados.

---

## 5️ Pruebas de rendimiento (ApacheBench)

Pruebas realizadas sobre `http://localhost/sample/`:

| Prueba | Requests | Concurrencia | RPS Antes | RPS Después | Latencia Antes | Latencia Después |
| ------ | -------- | ------------ | --------- | ----------- | -------------- | ---------------- |
| Ligera | 1000     | 20           | 1384.16   | 86.36       | 14.449 ms      | 231.6 ms         |
| Media  | 3000     | 100          | 2221.88   | 2064.08     | 45.007 ms      | 48.448 ms        |
| Pesada | 5000     | 200          | 2617.58   | 3042.72     | 76.407 ms      | 65.731 ms        |

**Conclusión:** Tras ajustar `server.xml`, el rendimiento en cargas altas mejora significativamente.

---

## 6️ Recomendaciones de administración

* Monitorear logs en `logs/catalina.out` y `logs/manager.*`
* Realizar **backups** periódicos de `webapps` y configuraciones
* Ajustar parámetros de `server.xml` según carga real
* Usar herramientas de monitoreo: **JConsole**, **VisualVM**, **Prometheus + Grafana**
* Mantener los permisos de usuario restrictivos

---

## 7️ Despliegue en contenedores (Docker)

1. Descargar imagen oficial:

```bash
docker pull tomcat:latest
```

2. Crear carpeta para WAR:

```bash
mkdir -p ~/myapp
cp /opt/tomcat/latest/webapps/sample.war ~/myapp/
```

3. Levantar contenedor:

```bash
docker run -d --name tomcat-contenedor -p 8081:8080 \
  -v ~/myapp:/usr/local/tomcat/webapps \
  tomcat:latest
```

4. Verificar aplicación: `http://localhost:8081/sample/`

**Ventajas del contenedor:**

* Portabilidad y reproducibilidad
* Aislamiento del host
* Escalabilidad y fácil despliegue
* Configuración mediante volúmenes y variables de entorno

**Tabla comparativa con Tomcat nativo:**

| Característica | Tomcat Nativo          | Tomcat en Contenedor                    |
| -------------- | ---------------------- | --------------------------------------- |
| Instalación    | Directa en SO          | Java + Tomcat preconfigurado            |
| Dependencias   | Manual                 | Preconfigurado                          |
| Portabilidad   | Limitada               | Alta, funciona en cualquier host Docker |
| Escalabilidad  | Difícil                | Fácil, compatible con Kubernetes        |
| Reinicios      | Afecta otros servicios | Aislado, reinicia contenedor            |
| Rendimiento    | Acceso directo         | Ligera sobrecarga                       |
