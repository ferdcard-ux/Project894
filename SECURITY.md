# Security

## Resumen

`Project894` maneja credenciales de acceso, caché local cifrada y una base de datos SQLite con información operativa. Por eso, cualquier cambio en seguridad debe tratarse con cuidado.

## Mecanismos actuales

- Derivación de claves con `PBKDF2HMAC`
- Cifrado de archivos con `Fernet`
- Caché local cifrada para cuentas usadas recientemente
- Clave dedicada para la base de datos local
- Soporte de compatibilidad para descifrar bases heredadas

## Archivos sensibles

Los siguientes archivos no deben compartirse públicamente:

- `data/project894.db`
- `data/app_db.key`
- `data/login_cache.bin`
- `data/login_cache.key`
- `data/salt.bin`

## Riesgos operativos conocidos

- La contraseña puede quedar disponible localmente en caché cifrada para habilitar acceso offline
- El scraping depende de una plataforma externa que puede cambiar selectores o flujos
- La base de datos permanece descifrada durante la sesión activa

## Buenas prácticas

- No commitear archivos de `data/` con información real
- No reutilizar los mismos archivos de claves entre entornos no controlados
- Hacer pruebas con cuentas no productivas cuando sea posible
- Revisar los cambios de seguridad junto con `src/core/security.py` y `src/ui/login_dialog.py`

## Reporte de hallazgos

Si detectas una vulnerabilidad o exposición de datos:

1. No la publiques junto con muestras reales.
2. Reproduce el caso en un entorno controlado.
3. Documenta alcance, impacto y pasos de mitigación.
4. Corrige primero la exposición de secretos antes de compartir cambios.
