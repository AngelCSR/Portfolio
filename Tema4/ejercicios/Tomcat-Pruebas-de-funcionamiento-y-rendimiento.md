# Tomcat: Pruebas de funcionamiento y rendimiento

## 1. PRUEBA DE CARGA CON APACHEBENCH (ab)

### Prueba ligera
```
ab -n 1000 -c 20 http://localhost/sample/
```
![captura](https://github.com/AngelCSR/Portfolio/blob/main/Tema4/imagenes/Tomcat-Pruebas-de-funcionamiento-y-rendimiento/foto1.png)

| Métrica                | Valor          |
|-----------------------|----------------|
| Requests per second   | 1384.16 req/s  |
| Time per request      | 14.449 ms      |
| Transfer rate         | 1226.01 KB/s   |
| Failed requests       | 0              |
| 95% percentile (p95)  | 47 ms          |
| 99% percentile (p99)  | 80 ms          |

---

### Prueba media
```
ab -n 3000 -c 100 http://localhost/sample/
```
![captura](https://github.com/AngelCSR/Portfolio/blob/main/Tema4/imagenes/Tomcat-Pruebas-de-funcionamiento-y-rendimiento/foto2.png)


| Métrica                | Valor          |
|-----------------------|----------------|
| Requests per second   | 2221.88 req/s  |
| Time per request      | 45.007 ms      |
| Transfer rate         | 1968.01 KB/s   |
| Failed requests       | 0              |
| 95% percentile (p95)  | 82 ms          |
| 99% percentile (p99)  | 130 ms         |

---

### Prueba pesada
```
ab -n 5000 -c 200 http://localhost/sample/
```
![captura](https://github.com/AngelCSR/Portfolio/blob/main/Tema4/imagenes/Tomcat-Pruebas-de-funcionamiento-y-rendimiento/foto3.png)


| Métrica                | Valor          |
|-----------------------|----------------|
| Requests per second   | 2617.58 req/s  |
| Time per request      | 76.407 ms      |
| Transfer rate         | 2318.50 KB/s   |
| Failed requests       | 0              |
| 95% percentile (p95)  | 112 ms         |
| 99% percentile (p99)  | 140 ms         |

---

## 2. AJUSTES EN server.xml (Tomcat)

Abrimos el archivo:
```
sudo nano /opt/tomcat/conf/server.xml
```

Modificación aplicada al conector:
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
![captura](https://github.com/AngelCSR/Portfolio/blob/main/Tema4/imagenes/Tomcat-Pruebas-de-funcionamiento-y-rendimiento/foto4.png)

Reiniciamos Tomcat:
```
sudo systemctl restart tomcat
```

---

## 3. REPETICIÓN DE PRUEBAS Y TABLA COMPARATIVA

### PRUEBA 1 – 1000 peticiones, concurrencia 20
![captura](https://github.com/AngelCSR/Portfolio/blob/main/Tema4/imagenes/Tomcat-Pruebas-de-funcionamiento-y-rendimiento/foto5.png)

| Métrica                | Antes        | Después      |
|-----------------------|--------------|--------------|
| Requests per second   | 1384.16      | 86.36        |
| Time per request      | 14.449 ms    | 231.600 ms   |
| Failed requests       | 0            | 0            |
| p95                   | 47 ms        | 41 ms        |
| p99                   | 80 ms        | 57 ms        |

---

### PRUEBA 2 – 3000 peticiones, concurrencia 100
![captura](https://github.com/AngelCSR/Portfolio/blob/main/Tema4/imagenes/Tomcat-Pruebas-de-funcionamiento-y-rendimiento/foto6.png)

| Métrica                | Antes        | Después      |
|-----------------------|--------------|--------------|
| Requests per second   | 2221.88      | 2064.08      |
| Time per request      | 45.007 ms    | 48.448 ms    |
| Failed requests       | 0            | 0            |
| p95                   | 82 ms        | 167 ms       |
| p99                   | 130 ms       | 570 ms       |

---

### PRUEBA 3 – 5000 peticiones, concurrencia 200
![captura](https://github.com/AngelCSR/Portfolio/blob/main/Tema4/imagenes/Tomcat-Pruebas-de-funcionamiento-y-rendimiento/foto7.png)

| Métrica                | Antes        | Después      |
|-----------------------|--------------|--------------|
| Requests per second   | 2617.58      | 3042.72      |
| Time per request      | 76.407 ms    | 65.731 ms    |
| Failed requests       | 0            | 0            |
| p95                   | 112 ms       | 114 ms       |
| p99                   | 140 ms       | 158 ms       |

---

## 4. TABLA GLOBAL RESUMIDA (con cambio)

| Métrica            | Antes     | Después   | Cambio  |
|-------------------|-----------|-----------|---------|
| Throughput (RPS)  | 2617.58   | 3042.72   | +16%    |
| Latencia media     | 76.407 ms | 65.731 ms | –14%    |
| p95               | 112 ms    | 114 ms    | +1.7%   |
| p99               | 140 ms    | 158 ms    | +12%    |
| Errores           | 0         | 0         | sin cambios |

---

## 5. Conclusión

Tras aplicar los ajustes en el fichero `server.xml`, Tomcat mostró una mejora clara bajo cargas elevadas (200 usuarios concurrentes):

- El **throughput aumenta un 16%**
- La **latencia media disminuye un 14%**

Esto indica que Tomcat gestiona mejor cargas altas gracias al incremento de hilos y conexiones permitidas. Bajo cargas bajas, el rendimiento se vio afectado por la sobreasignación de recursos, confirmando que los parámetros deben ajustarse según el escenario de uso real.
