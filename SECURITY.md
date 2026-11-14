# Security

## Resumen

Este repositorio público no almacena código fuente ni datos operativos de usuarios. Aun así, la publicación de binarios y documentación debe tratarse con cuidado para evitar exposición de información sensible.

## Qué no debe publicarse aquí

No deben incluirse en este repositorio:

- bases de datos locales de usuarios
- archivos de caché o credenciales
- claves, sales o secretos de cifrado
- rutas privadas de compilación
- código fuente interno o artefactos intermedios de desarrollo

## Autenticidad del APK de Android

Todos los APK oficiales desde la `2.0.10` están firmados con el mismo certificado:

- SHA-256: `bdcf8658236171733ef576587db4db2303a64e9d270e66e9b0c6f3ea6e82e25b`

La huella es pública; la clave privada y su contraseña nunca se publican y se custodian fuera de cualquier repositorio. Verifica con `apksigner verify --print-certs <apk>`. La app también comprueba su propia firma al iniciar y bloquea copias re-firmadas.

## Riesgos relevantes para el repositorio público

- publicar por error un binario incorrecto o no validado
- exponer documentación con instrucciones internas o rutas privadas
- adjuntar archivos con datos operativos reales a un release público
- mezclar artefactos de plataformas o versiones distintas en una misma release

## Buenas prácticas de publicación

- verificar nombre, versión y plataforma de cada artefacto antes de subirlo
- en Android, confirmar con `apksigner` que la huella SHA-256 del APK es la indicada arriba; nunca publicar un APK con otra firma
- publicar únicamente binarios finales destinados a distribución
- revisar que `README.md`, `CHANGELOG.md` y `RELEASE_NOTES.md` coincidan con la versión publicada
- mantener separados los procesos internos de build del repositorio público

## Reporte de hallazgos

Si detectas una exposición o error de publicación:

1. retira o reemplaza el artefacto comprometido lo antes posible
2. evita compartir públicamente datos sensibles del incidente
3. documenta alcance, impacto y mitigación
4. corrige primero la exposición antes de ampliar la comunicación pública
