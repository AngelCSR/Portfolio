## Actividad 11: Disponibilidad y Buenas Prácticas para un Servidor FTP

### Objetivo
Garantizar la disponibilidad, seguridad y correcto funcionamiento de un servidor FTP/FTPS en producción, minimizando riesgos y asegurando la continuidad del servicio.

### Recomendaciones basadas en las actividades anteriores

**Límites de conexión y control de usuarios**
- Configurar un número máximo de conexiones simultáneas (`max_clients`) para evitar sobrecarga.
- Limitar conexiones por IP (`max_per_ip`) para prevenir ataques de fuerza bruta.
- Revisar y auditar periódicamente la lista de usuarios y grupos creados (Actividad 3).
- Deshabilitar acceso anónimo si no es necesario (Actividad 4).

**Logs y auditoría**
- Activar registros detallados de conexiones, transferencias y errores (Actividad 2 y 5).
- Rotar y archivar logs regularmente para evitar saturación del disco.
- Analizar logs para detectar accesos sospechosos o fallos recurrentes.
- Mantener un registro de pruebas realizadas en clientes gráficos y línea de comandos (Actividades 6 y 7).

**Copias de seguridad**
- Realizar backups periódicos de archivos de usuarios y configuraciones del servidor.
- Incluir certificados TLS/SSL usados en FTPS (Actividad 8).
- Probar restauraciones periódicas para asegurar integridad de datos.

**Firewall y NAT**
- Permitir solo los puertos necesarios: 2121 (FTP), puerto pasivo configurado (Actividad 5 y 8).
- Configurar NAT correctamente si el servidor está detrás de un router.
- Bloquear accesos no autorizados desde internet, dejando solo los clientes permitidos.

**Seguridad y buenas prácticas adicionales**
- Usar FTPS para cifrar la comunicación entre cliente y servidor (Actividad 8).
- Mantener actualizado el servidor y sus dependencias.
- Revisar permisos de directorios y archivos: los usuarios deben poder escribir solo en su home o DocumentRoot, y Apache solo debe tener permisos de lectura si se integra con web (Actividad 10).
- Deshabilitar usuarios que no se usen y limpiar grupos innecesarios.

**Pruebas periódicas**
- Probar conexiones en modo activo y pasivo (Actividad 5) para asegurar que todos los clientes pueden conectarse.
- Realizar transferencias con clientes gráficos y línea de comandos (Actividades 6 y 7) para verificar que todo funciona correctamente.
- Comprobar la publicación web vía Apache si se integra FTP con DocumentRoot (Actividad 10).

**Monitoreo y mantenimiento**
- Configurar alertas por fallo de conexión o saturación del servidor.
- Revisar logs y estadísticas periódicamente.
- Documentar cambios en configuración, usuarios, certificados y rutas de backup.

### Resumen gráfico del flujo seguro y disponible

```
Usuario (Cliente FTP)
    │
    │ Conexión segura FTPS
    ▼
Servidor FTP/FTPS
    │
    │ Control de usuarios, límites y auditoría
    │
    │ Logs y backups automáticos
    ▼
Archivos en /srv/ftp o /var/www/html
    │
    │ Apache o servicio de entrega (si aplica)
    ▼
HTTP (Navegador)
    │
    │ Página web o archivos accesibles
```

### Conclusión
Implementando estas buenas prácticas se garantiza que un servidor FTP/FTPS sea seguro, confiable y disponible, con capacidad de recuperación ante fallos, registros completos para auditoría, y una integración correcta con servicios web si es necesario. Se consolidan todos los aprendizajes de la UT 5: usuarios, grupos, permisos, FTPS, pruebas y publicación web.

