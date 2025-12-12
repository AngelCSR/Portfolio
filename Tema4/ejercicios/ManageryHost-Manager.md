# Ficha descriptiva de interfaces Tomcat

## 1. Tomcat Manager

**URL:**

```
https://localhost:8443/manager/html
```

**Acceso:**
Usuario(angel) con rol `manager-gui`.

**Funciones principales:**

| Función                    | Descripción                                                                                                                                           |
| -------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- |
| Despliegue de aplicaciones | Permite subir un archivo WAR o desplegar desde un directorio existente en el servidor.                                                                |
| Recarga (Reload)           | Recarga una aplicación web específica sin reiniciar todo el servidor. Esto aplica cambios en archivos de configuración o código sin downtime general. |
| Parada (Stop)              | Detiene una aplicación web específica, liberando recursos y dejando la aplicación inaccesible hasta reiniciarla.                                      |
| Eliminación (Undeploy)     | Elimina completamente una aplicación desplegada, borrando archivos temporales y WAR asociados.                                                        |
| Estado de aplicaciones     | Lista todas las aplicaciones desplegadas con su estado actual (running/stopped).                                                                      |
| Información del servidor   | Permite consultar estadísticas como memoria, threads y sesiones activas.                                                                              |
| Scripts de gestión         | La sección `/text/*` permite operaciones vía línea de comandos usando `curl` u otros clientes HTTP.                                                   |

**Notas:**

* Se recomienda usar HTTPS para mayor seguridad.
* Ideal para administradores que gestionan aplicaciones individualmente.

![captura](https://github.com/AngelCSR/Portfolio/blob/main/Tema4/imagenes/manageryhostmanage/foto1.png)
![captura](https://github.com/AngelCSR/Portfolio/blob/main/Tema4/imagenes/manageryhostmanage/foto2.png)
![captura](https://github.com/AngelCSR/Portfolio/blob/main/Tema4/imagenes/manageryhostmanage/foto3.png)


## 2. Tomcat Host Manager

**URL:**

```
https://localhost:8443/host-manager/html/list;jsessionid=7E52DF64C28F90B3A9BA25B37ADE1C4B?org.apache.catalina.filters.CSRF_NONCE=361D9E5CBC4307FC9400E209C3631564
```

**Acceso:**
Usuario(angel) con rol `admin-gui`.

**Funciones principales:**

| Función                  | Descripción                                                                                            |
| ------------------------ | ------------------------------------------------------------------------------------------------------ |
| Crear hosts virtuales    | Permite crear nuevos hosts virtuales (nuevos dominios o subdominios dentro del mismo servidor Tomcat). |
| Listar hosts virtuales   | Muestra todos los hosts configurados en Tomcat y su estado.                                            |
| Eliminar hosts virtuales | Permite borrar hosts virtuales existentes.                                                             |
| Despliegue por host      | Permite desplegar aplicaciones directamente en hosts virtuales específicos.                            |
| Gestión centralizada     | Facilita la administración de múltiples hosts desde una sola interfaz.                                 |

**Notas:**

* Solo accesible a administradores con permisos completos.
* Útil en entornos de múltiples dominios o aplicaciones independientes en un mismo servidor.

![captura](https://github.com/AngelCSR/Portfolio/blob/main/Tema4/imagenes/manageryhostmanage/foto4.png)
![captura](https://github.com/AngelCSR/Portfolio/blob/main/Tema4/imagenes/manageryhostmanage/foto5.png)

## Resumen

Manager se centra en la gestión de aplicaciones web existentes dentro de Tomcat.

Host Manager se centra en la administración de hosts virtuales y dominios múltiples.

Ambos requieren acceso autenticado y es recomendable usar HTTPS para seguridad.
