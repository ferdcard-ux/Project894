# FAQ — Project894 Android

## ¿Qué hace Project894 Android?

Es una aplicación nativa Android que permite consultar, gestionar y dar seguimiento a evidencias académicas, calificaciones, anuncios y eventos de calendario desde la plataforma Zajuna SENA, todo desde tu dispositivo móvil.

## ¿Necesita internet?

Sí, para autenticarse y extraer datos de Zajuna. Algunas secciones funcionan offline si ya existe caché local válida (evidencias, anuncios y eventos previamente sincronizados).

## ¿Cómo inicio sesión?

1. Selecciona tu tipo de documento (Cédula de Ciudadanía, Cédula de Extranjería o Tarjeta de Identidad).
2. Ingresa tu número de documento y contraseña.
3. Presiona "Ingresar". La app abre un WebView invisible, inyecta las credenciales y navega automáticamente.
4. Al cerrar la app, las credenciales se almacenan cifradas localmente para auto-login en la siguiente apertura.

## ¿Qué pasa al abrir la app por primera vez?

Aparece un pop-up de **Términos y Condiciones** que debes leer completamente. La casilla de verificación se habilita solo cuando llegas al final del scroll. Si aceptas, la app procede al login. Si rechazas, la app se cierra.

## ¿Cómo se organizan las pantallas?

La app tiene 4 pantallas principales, accesibles desde la barra inferior:

| Pantalla | Descripción |
|---|---|
| **Evidencias** | Lista de evidencias con búsqueda, filtros por estado y ordenamiento. |
| **Notificaciones** | Eventos de calendario próximos y anuncios del foro. |
| **Configuración** | Ajustes de notificaciones, sincronización, exportación y actualización. |
| **Perfil** | Información de la sesión y cierre de sesión. |

## ¿Qué filtros y ordenamientos tiene la pantalla de Evidencias?

**Filtros por estado:**
- Todas, Pendientes, Evaluadas, Vencidas

**Ordenamiento (según filtro activo):**
- Todas/Pendientes/Vencidas: Default, Código A-Z, Código Z-A, Fecha ↑, Fecha ↓
- Evaluadas: Default, Código A-Z, Código Z-A, Calificación

Además, puedes buscar por título o código usando la barra de búsqueda.

## ¿Cómo se actualizan los datos?

La app usa un modelo **cache-first**: al abrir una pantalla, los datos se cargan instantáneamente desde la base de datos local (Room), y luego se sincronizan en segundo plano con Zajuna. También puedes forzar la sincronización manual con el botón de actualización.

Un **indicador visual** debajo de los filtros en la pantalla de Evidencias muestra el estado de la última sincronización (fecha, cantidad de evidencias y si fue exitosa).

La sincronización automática se programa después del login exitoso y puede configurarse en Ajustes (intervalo de 1 a 6 horas).

## ¿Qué notificaciones recibo?

La app tiene 4 canales de notificación:

| Canal | Disparador |
|---|---|
| Sincronización | Progreso de la sincronización en segundo plano |
| Alertas | Evidencias próximas a vencer (≤7 días) |
| Calendario | Eventos de calendario próximos |
| Anuncios | Nuevos anuncios del curso |

Puedes habilitar/deshabilitar cada tipo individualmente desde Ajustes > Notificaciones.

## ¿Cómo exporto mis datos?

- **Evidencias a Excel**: Desde Ajustes > Exportar a Excel. Se crea un archivo `.xlsx` con todas las evidencias.
- **Logs de depuración**: Desde Ajustes > Exportar logs. Copia el registro de la aplicación a la carpeta `Descargas/.Project894/`.

## ¿Cómo funciona la actualización in-app?

Al abrir Ajustes, la app consulta automáticamente los releases del repositorio oficial de GitHub. Si existe una versión más reciente de `Project894-android-*.apk`, muestra un diálogo con la nueva versión y las notas del release. Puedes descargar la actualización con barra de progreso e instalarla directamente desde la app.

También puedes forzar la verificación manual desde Ajustes > Buscar actualizaciones.

## ¿Dónde se guardan los datos localmente?

| Dato | Ubicación |
|---|---|
| Base de datos (Room + SQLCipher) | Almacenamiento interno privado de la app |
| Credenciales | EncryptedSharedPreferences (Android KeyStore) |
| Preferencias de usuario | DataStore (archivo interno) |
| Logs de depuración | `Descargas/.Project894/` |
| APK de actualización | Caché interna de la app (`cache/updates/`) |

## ¿Qué permisos necesita la app?

- **Internet**: Para conectarse a Zajuna y GitHub.
- **Notificaciones** (Android 13+): Para mostrar notificaciones push.
- **Instalar apps desconocidas** (solo para actualización): Al descargar una actualización, la app abre el instalador del sistema.

## ¿Qué pasa si Zajuna cambia su interfaz?

La app usa selectores HTML múltiples y estrategias de extracción resilientes. Si un selector falla, intenta con alternativos. Si la extracción completa falla, puedes intentar más tarde o contactar al desarrollador.

## ¿Puedo usar la app sin conexión?

Parcialmente. Los datos previamente sincronizados (evidencias, anuncios, eventos) están disponibles sin conexión gracias a la caché local. El login requiere conexión a Zajuna, pero si hay credenciales cacheadas válidas, la app puede permitir acceso offline.

## ¿Cómo cierro sesión?

Desde Ajustes, presiona el botón "Cerrar sesión" al final de la pantalla. Esto limpia los datos de la sesión actual.

## ¿Dónde reporto problemas o sugiero mejoras?

En el repositorio oficial: [github.com/ferdcard-ux/Project894](https://github.com/ferdcard-ux/Project894)
