# Actividad 9: Uso del navegador como cliente FTP

## 1. Acceso al servidor FTP desde un navegador

Intenté abrir el servidor FTP en Firefox con la dirección:

```
ftp://127.0.0.1:2121
```

Resultado mostrado en la captura:

![Captura navegador FTP](https://github.com/AngelCSR/Portfolio/blob/main/Tema%205/Imagenes/actividad9/foto1.png)

Mensaje del navegador:

```
No hay aplicaciones disponibles
No hay ninguna aplicación instalada que pueda abrir «ftp://127.0.0.1:2121/».
```

**Explicación:**
- Firefox no soporta FTPS explícito (TLS) obligatorio en el servidor.
- Los navegadores modernos solo permiten FTP en texto plano y, en Linux, requieren un programa externo para manejar FTP desde el navegador.

---

## 2. Limitaciones frente a un cliente FTP dedicado

| Funcionalidad | Navegador | Cliente FTP dedicado (FileZilla, WinSCP) |
|---------------|-----------|-----------------------------------------|
| FTPS/TLS | ❌ no soportado | ✅ soportado |
| Subir archivos | Limitado | ✅ soportado |
| Subir carpetas completas | Limitado o imposible | ✅ soportado |
| Transferencias en cola | ❌ no soportado | ✅ soportado |
| Reanudar descargas interrumpidas | ❌ no soportado | ✅ soportado |
| Configuración de puertos pasivos/activos | ❌ no soportado | ✅ soportado |
| Logs / registro de transferencias | ❌ no disponible | ✅ detallado |

---

## 3. Ventajas del navegador

- Acceso rápido y sin instalar software adicional.
- Útil para descargas puntuales de archivos públicos.

---

## 4. Desventajas del navegador

- No permite FTPS/SFTP → conexiones inseguras.
- Funcionalidad muy limitada: no se pueden subir carpetas, usar colas de transferencia ni reanudar descargas.
- Sin registro de actividad ni control avanzado de permisos.
- Dependencia de programas externos para FTP en navegadores modernos.

---

## 5. Conclusión

- Los navegadores pueden servir como clientes FTP básicos, pero no son adecuados para entornos seguros ni transferencias complejas.
- Para FTPS obligatorio y funcionalidades completas, es necesario un cliente FTP dedicado como FileZilla o WinSCP.
- Esta captura demuestra claramente la limitación del navegador frente a un cliente FTP profesional.

