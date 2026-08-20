# Descargo de Responsabilidad Legal

**Project894** es una herramienta de desarrollo independiente y **NO está afiliada, asociada, autorizada, endosada ni conectada oficialmente con el Servicio Nacional de Aprendizaje (SENA)** ni con la plataforma Zajuna/Territorium.

### 1. Uso de Credenciales
El software solicita las credenciales del usuario únicamente para fines de autenticación local y acceso a la plataforma institucional del usuario. El desarrollador no recolecta, almacena en servidores externos ni tiene acceso a ninguna de las contraseñas o datos personales ingresados en la aplicación.

### 2. Responsabilidad del Usuario
El uso de scripts de automatización o "scraping" puede estar sujeto a los términos de servicio de las plataformas del SENA. El usuario es el único responsable de:
* El uso ético y legal de sus credenciales.
* Cualquier sanción disciplinaria o técnica que la institución pudiera aplicar por el uso de herramientas de terceros.
* La integridad de sus datos académicos.

### 3. Sin Garantías
El desarrollador no garantiza que la herramienta funcione de manera ininterrumpida, ya que depende de cambios en el código fuente de plataformas externas fuera de su control. El uso de esta aplicación es bajo su propio riesgo.

### 4. Registros de Depuración (logs)

La aplicación genera archivos de registro (logs) para fines de depuración y diagnóstico, conserva los últimos 3 días y permite exportarlos desde **Configuración → Exportar logs** (se comprimen en un `.zip` que se comparte con el share sheet del sistema).

#### 4.1 Qué pueden contener los logs
- **Información del dispositivo:** fabricante, modelo y versión de Android (SDK), y versión de la aplicación.
- **Trazas de actividad:** marcas de tiempo y eventos de uso (login, sincronización, exportación, actualizaciones).
- **Identificadores de la plataforma:** ID de curso, códigos y títulos de evidencias, anuncios y eventos de calendario.
- **Detalles de red:** URLs de la plataforma Zajuna (zajuna.sena.edu.co), códigos de estado HTTP, tamaños de respuesta y mensajes de error de conexión (que pueden incluir nombres de host o IP en excepciones).
- **Mensajes de error y trazas de pila** de fallos internos.

#### 4.2 Qué NO contienen los logs
- Contraseñas ni credenciales de acceso (nunca se escriben en los registros; se almacenan cifradas solo en el dispositivo).
- Números de documento completos (se registran **enmascarados**, p. ej. `12***45`).
- El contenido de la base de datos local cifrada (SQLCipher) ni los datos académicos en su totalidad.

#### 4.3 Uso autorizado y responsabilidad
- Al exportar y compartir los registros, el usuario **autoriza al desarrollador a utilizarlos exclusivamente** con fines de depuración, corrección de fallos y desarrollo de Project894.
- El desarrollador **no los comparte con terceros** ni los utiliza con fines comerciales.
- Los registros pueden contener información sensible o institucional. **El usuario es responsable del uso, custodia y difusión** del archivo exportado; se recomienda eliminarlo tras el diagnóstico.
- Los registros no se envían automáticamente a ningún servidor: se exportan únicamente por acción explícita del usuario.

### 5. Propiedad Intelectual
Project894 es un **desarrollo privado** y **NO es código abierto**. Únicamente el **repositorio de distribución** y su contenido son públicos. Cualquier usuario puede solicitar una copia del código fuente, sugerir mejoras y reportar o corregir fallos, sujeto a la aprobación del desarrollador. El desarrollador **se reserva los derechos de aprobación o admisión**.

### 6. Enlaces a Repositorios y Contribuciones
- El **código fuente** se aloja en un **repositorio privado**.
- **Repositorio de distribución (público):** [github.com/ferdcard-ux/Project894](https://github.com/ferdcard-ux/Project894)
- Para mayor información sobre **contribuciones o contacto con el desarrollador**, consulte [`CONTRIBUTING.md`](https://github.com/ferdcard-ux/Project894/blob/master/CONTRIBUTING.md).
