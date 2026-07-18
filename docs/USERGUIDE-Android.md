# Guía de Usuario — Project894 Android

## 1. Introducción

Project894 Android es una aplicación nativa que te permite consultar, gestionar y dar seguimiento a tus evidencias académicas, calificaciones, anuncios y eventos de calendario desde la plataforma Zajuna SENA, directamente desde tu dispositivo móvil.

### Requisitos del sistema

- Android 8.0 (API 26) o superior
- Conexión a internet para autenticación y sincronización

---

## 2. Instalación

1. Descarga el archivo `Project894-android-<version>.apk` desde la sección de releases del repositorio oficial:
   [github.com/ferdcard-ux/Project894/releases](https://github.com/ferdcard-ux/Project894/releases)

2. En tu dispositivo Android, si es la primera vez que instalas una app fuera de Google Play, habilita "Instalar apps desconocidas" cuando el sistema lo solicite.

3. Abre el archivo APK y presiona "Instalar".

4. Al abrir la app por primera vez, aparecerá un pop-up de **Términos y Condiciones**. Debes leer el documento completo (desplázate hasta el final), marcar la casilla "He leído y acepto los términos y condiciones" y presionar "Aceptar" para continuar. Si presionas "Rechazar", la app se cierra.

---

## 3. Inicio de Sesión

1. Selecciona tu **tipo de documento**:
   - Cédula de Ciudadanía
   - Cédula de Extranjería
   - Tarjeta de Identidad

2. Ingresa tu **número de documento** y **contraseña** de Zajuna SENA.

3. Presiona **"Ingresar"**.

4. La app abrirá un WebView invisible, inyectará tus credenciales y navegará automáticamente en la plataforma Zajuna.

5. Al completar el login exitoso:
   - Las credenciales se almacenan cifradas localmente (Android KeyStore)
   - Se programa la sincronización automática en segundo plano
   - Se redirige a la pantalla de Evidencias

6. En aperturas posteriores, la app detectará las credenciales cacheadas e intentará el auto-login automáticamente.

> **Nota:** Si el login falla por problemas de conexión o cambios en Zajuna, la app puede permitir acceso offline si existen credenciales cacheadas válidas.

---

## 4. Pantalla de Evidencias

Es la pantalla principal donde puedes ver y gestionar todas tus evidencias académicas.

### Barra de búsqueda
Escribe en la barra superior para filtrar evidencias por título o código en tiempo real. Para limpiar la búsqueda, borra el texto.

### Filtros por estado
Usa las pestañas debajo de la barra de búsqueda:
- **Todas**: Muestra todas las evidencias.
- **Pendientes**: Solo evidencias no entregadas.
- **Evaluadas**: Solo evidencias con calificación.
- **Vencidas**: Solo evidencias cuya fecha de cierre ya pasó.

### Ordenamiento
Presiona el ícono de ordenamiento para cambiar el criterio. Las opciones varían según el filtro activo:

| Filtro activo | Opciones de ordenamiento |
|---|---|
| Todas / Pendientes / Vencidas | Default, Código A-Z, Código Z-A, Fecha ↑, Fecha ↓ |
| Evaluadas | Default, Código A-Z, Código Z-A, Calificación (A→F) |

### Tarjeta de evidencia
Cada evidencia se muestra como una tarjeta con:
- **Título** (enlace web: presiona para abrir en el navegador)
- **Código** de la evidencia (seleccionable para copiar al portapapeles)
- **Descripción** textual
- **Estado** con badge de color:
  - Pendiente (amarillo)
  - Vencida (rojo)
  - Entregada (azul)
  - Evaluada (verde)
- **Fechas**: Apertura y Cierre
- **Calificación** (solo visible en filtro Evaluadas)
- **Instructor** asignado

### Sincronizar datos
Presiona el botón flotante (FAB) con ícono de actualizar para forzar una sincronización manual. Verás un indicador de progreso mientras se actualizan los datos.

### Indicador de sincronización
Debajo de los filtros, una barra visual muestra el estado de la última sincronización:
- **Check verde + "Última sync: hace X min (N evidencias)"**: Sincronización exitosa reciente.
- **Check rojo + "Sync fallida"**: La última sincronización encontró un error.
- **Spinner + "Sincronizando..."**: Sincronización en progreso.
- **Oculto**: La app nunca se ha sincronizado en esta sesión.

---

## 5. Pantalla de Notificaciones

Esta pantalla tiene dos secciones:

### Eventos de Calendario
Muestra los eventos académicos próximos extraídos de Zajuna. Cada evento incluye título y fecha. Presiona un evento para abrirlo en el navegador.

### Anuncios
Muestra los anuncios del foro del curso. Cada anuncio incluye título y fecha de publicación. Presiona un anuncio para ver su detalle completo (incluye el contenido HTML renderizado en un WebView). Desde el detalle puedes abrir el anuncio en el navegador.

> **Carga instantánea:** Los datos se cargan desde la caché local primero (instantáneo), y luego se sincronizan en segundo plano para actualizar la información.

---

## 6. Pantalla de Configuración

### 6.1 Notificaciones

| Opción | Descripción |
|---|---|
| Activar notificaciones | Interruptor global de todas las notificaciones |
| Progreso de evidencias | Notificar avance de sincronización de evidencias |
| Progreso de calendario | Notificar avance de sincronización de calendario |
| Progreso de anuncios | Notificar avance de sincronización de anuncios |
| Sincronización completa | Notificar cuando termina la sincronización |
| Alertas evidencias próximas a vencer | Notificar evidencias con ≤7 días al cierre |
| Nuevos anuncios | Notificar cuando hay un nuevo anuncio |
| Eventos de calendario | Notificar eventos próximos |

Los subtipos solo se muestran si el interruptor global está activado.

### 6.2 Sincronización

- **Sincronización automática**: Activa o desactiva la sincronización periódica en segundo plano.
- **Intervalo de sincronización**: Configura cada cuántas horas se sincroniza automáticamente (1 a 6 horas).

### 6.3 Inicio

- **Inicio automático al encender**: Permite que la app se reinicie automáticamente después de un reinicio del dispositivo (requiere configuración adicional según el fabricante).

### 6.4 Datos

| Opción | Descripción |
|---|---|
| Exportar a Excel | Crea un archivo Excel con todas las evidencias |
| Exportar logs | Copia el archivo de registro de depuración a `Descargas/.Project894/` |

### 6.5 Actualizaciones

- **Buscar actualizaciones**: Verifica si hay una versión más reciente disponible en GitHub. Si existe, puedes descargarla e instalarla directamente desde la app.

### 6.6 Acerca de

Muestra la versión instalada y enlaces al repositorio, descargo de responsabilidad y ayuda.

### 6.7 Cerrar sesión

Limpia los datos de la sesión actual y regresa a la pantalla de login.

---

## 7. Actualización In-App

1. Abre la pantalla de **Configuración**. La app verifica automáticamente si hay una nueva versión.

2. Si hay una actualización disponible, aparece un diálogo con:
   - Versión nueva y fecha de publicación
   - Notas del release
   - Botón **"Descargar"** y **"Más tarde"**

3. Presiona **"Descargar"** para iniciar la descarga. Verás una barra de progreso con el porcentaje.

4. Al completar la descarga, presiona **"Instalar ahora"** para abrir el instalador del sistema.

5. Confirma la instalación en la pantalla del sistema Android.

> **Nota:** Si no hay internet al verificar, la app no muestra ningún mensaje. Puedes forzar la verificación manual desde Ajustes > Buscar actualizaciones.

---

## 8. Exportación de Logs

1. Ve a **Configuración** > **Exportar logs**.

2. La app copia el archivo de registro del día a la carpeta `Descargas/.Project894/`.

3. Aparece un mensaje confirmando la ruta del archivo.

4. Puedes acceder al archivo desde cualquier gestor de archivos en `Descargas/.Project894/`.

> La app conserva automáticamente solo los 3 archivos de log más recientes. Los más antiguos se eliminan.

---

## 9. Solución de Problemas

### El login falla
- Verifica tu conexión a internet.
- Confirma que tus credenciales sean correctas.
- Si el error persiste, la app intentará el modo offline si hay credenciales cacheadas.

### Las evidencias no se actualizan
- Presiona el botón de sincronización manual.
- Verifica que la sincronización automática esté activada en Ajustes.
- Revisa tu conexión a internet.

### No llegan notificaciones
- Verifica que las notificaciones estén activadas en Ajustes.
- Revisa los permisos de la app en Ajustes del sistema > Notificaciones.
- En algunos dispositivos, puede ser necesario configurar el auto-inicio en los ajustes del fabricante.

### La app no encuentra actualizaciones
- Verifica tu conexión a internet.
- La app busca releases con el formato `Project894-android-*.apk` en el repositorio oficial.
- Puedes forzar la verificación desde Ajustes > Buscar actualizaciones.

---

## 10. Seguridad y Privacidad

- **Credenciales**: Se almacenan cifradas con Android KeyStore + EncryptedSharedPreferences.
- **Base de datos local**: Cifrada con SQLCipher (clave derivada del almacenamiento seguro).
- **Datos en tránsito**: Las conexiones a Zajuna usan SSL (TrustManager permisivo para certificados autofirmados del entorno educativo).
- **La app no recolecta ni transmite datos personales a servidores externos**. Toda la información se procesa y almacena localmente en tu dispositivo.
