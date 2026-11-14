# FAQ — Project894 Android

## ¿Qué hace Project894 Android?

Es una aplicación nativa Android que permite consultar, gestionar y dar seguimiento a evidencias académicas, calificaciones, anuncios y eventos de calendario desde la plataforma Zajuna SENA, todo desde tu dispositivo móvil. Incluye además notificaciones nativas de Zajuna (mensajes privados, foros, tareas, quizzes y calificaciones) y los juicios evaluativos de Sofía Plus.

## ¿Necesita internet?

Sí, para autenticarse y extraer datos de Zajuna. Algunas secciones funcionan offline si ya existe caché local válida (evidencias, anuncios y eventos previamente sincronizados).

## ¿Cómo inicio sesión?

1. Selecciona tu tipo de documento (Cédula de Ciudadanía, Cédula de Extranjería o Tarjeta de Identidad).
2. Ingresa tu número de documento y contraseña.
3. Presiona "Ingresar". La app abre un WebView invisible, inyecta las credenciales y navega automáticamente.
4. Al cerrar la app, las credenciales se almacenan cifradas localmente para auto-login en la siguiente apertura.
5. En aperturas posteriores, si la sesión persistida sigue activa, la app entra directo sin volver a pasar por el WebView (fast-path).

## ¿Qué pasa al abrir la app por primera vez?

Aparece un pop-up de **Términos y Condiciones** que debes leer completamente. La casilla de verificación se habilita solo cuando llegas al final del scroll. Si aceptas, la app procede al login. Si rechazas, la app se cierra. El documento incluye la sección 9 "Registros de Depuración" (resumen) con remisión al [DISCLAIMER.md](../DISCLAIMER.md).

## ¿Cómo se organizan las pantallas?

La app tiene 3 pantallas principales: **Evidencias** (inicio), accesible desde la barra superior con
iconos de **Notificaciones** y **Configuración**; **Notificaciones** muestra eventos de calendario,
anuncios y notificaciones del sistema; **Configuración** contiene los ajustes. Desde Notificaciones
se accede al **Detalle de Anuncio** y al **Detalle de Notificación** (in-app). Desde Evidencias se
accede al **Detalle de Evidencia** (in-app) tocando la tarjeta.

| Pantalla | Descripción |
|---|---|
| **Evidencias** | Lista de evidencias con búsqueda, filtros por estado y ordenamiento; incluye la pestaña **SofiaPlus** con los juicios evaluativos. |
| **Notificaciones** | Eventos de calendario próximos y anuncios del foro. |
| **Configuración** | Ajustes de notificaciones, sincronización, exportación y actualización. |

## ¿Qué filtros y ordenamientos tiene la pantalla de Evidencias?

**Filtros por estado** (cada pestaña muestra su contador, p. ej. "Todas: 211"):
- Todas, Pendientes, Evaluadas, Por evaluar, Vencidas
- La última pestaña de la fila, **SofiaPlus**, no filtra evidencias: muestra los juicios de Sofía Plus

**Ordenamiento** (por defecto **Código A-Z**; según filtro activo):
- Todas/Pendientes/Por evaluar/Vencidas: Default, Código A-Z, Código Z-A, Fecha ↑, Fecha ↓
- Evaluadas: Default, Código A-Z, Código Z-A, Calificación

Al tocar una pestaña, la lista vuelve al inicio. La Calificación y el Comentario del instructor solo
se muestran en la pestaña **Evaluadas**. Además, puedes buscar por título o código usando la barra de búsqueda.

## ¿Cómo veo el detalle de una evidencia?

Toca la tarjeta (no el título) en cualquiera de las pestañas de evidencias: **Todas**, **Pendientes**,
**Evaluadas**, **Por evaluar** o **Vencidas**. Se abrirá dentro de la app con el contenido limpio de la evidencia, incluida la
sección **"Estado de la entrega"** (intento, estado de la entrega, estado de la calificación, tiempo
restante, última modificación, archivos enviados y comentarios) y, si está calificada, la tabla con la
nota, la fecha, el docente y sus comentarios. El bloque de arriba cambia según la pestaña desde la que
abriste la evidencia.

El título de la tarjeta sigue abriendo la evidencia en el navegador, igual que antes. Las imágenes no
se muestran en el detalle porque en Zajuna son imágenes decorativas que no cargan.

## ¿Puedo descargar los archivos que adjunté?

Sí. En la fila **"Archivos enviados"** del detalle, toca el nombre del archivo: la app abre el diálogo
para que elijas dónde guardarlo y lo descarga con tu sesión de Zajuna. El resto de enlaces del detalle
se abren en el navegador.

## ¿Qué son las etiquetas manuales?

En la pestaña **"Todas"**, cada tarjeta tiene un botón de etiqueta en su esquina inferior derecha. Al
tocarlo se despliegan cuatro opciones predefinidas: **ENVIADA**, **NO ASIGNADA**, **PENDIENTE** y
**VENCIDA**. Aplican estas reglas para no duplicar información:

- **EVALUADA no se puede asignar a mano**: es el estado real de Zajuna.
- Si la evidencia ya tiene esa etiqueta asignada automáticamente, la opción aparece **bloqueada con candado**.
- Si Zajuna pasa la evidencia a **EVALUADA**, la etiqueta manual **se retira sola** en la siguiente sincronización.
- Las etiquetas manuales se conservan al sincronizar.

## ¿Por qué una evidencia sale EVALUADA si en Zajuna no está calificada?

Ya no debería ocurrir. Se corrigió en la 2.0.13: antes se marcaba como evaluada **toda fila** del
reporte de notas, incluidas las actividades sin calificar (celda "-"). Ahora solo se consideran las que
tienen una nota real. Si encuentras un caso, sincroniza y revisa el código del informe para confirmar
el formato.

## ¿Qué muestra la pestaña "Por evaluar"?

Las evidencias que ya entregaste (tienen recursos cargados en Zajuna) y que el instructor todavía no ha
calificado. La app lo consulta en el índice de tareas del curso durante cada sincronización. También
aparecen ahí las que marcaste a mano como **ENVIADA**.

Una evidencia entregada **no pasa a "Vencida"** aunque su fecha de cierre ya haya pasado: se queda en
"Por evaluar" hasta que tenga calificación, y entonces pasa a "Evaluadas".

## ¿Qué es la pestaña SofiaPlus?

Muestra tus **juicios evaluativos de Sofía Plus**: por cada competencia del programa, sus resultados de
aprendizaje y el juicio de cada uno (**APROBADO**, **POR EVALUAR** o **NO APROBADO**). Tiene filtros
propios y puedes buscar por competencia o por resultado.

La primera vez la app te pide autorización; después los juicios se actualizan solos **una vez al día**
y quedan guardados para consultarlos sin conexión. Puedes forzar la actualización con el botón de
sincronizar estando en esa pestaña.

## ¿Tengo que ingresar otra clave para Sofía Plus?

No. Sofía Plus y Zajuna comparten los datos de ingreso, así que la app usa las credenciales que ya
guardaste al iniciar sesión. Si Sofía Plus las rechaza (por ejemplo, porque cambiaste la clave solo en
uno de los portales), la pestaña lo indica y la actualización diaria se pausa hasta que vuelvas a
intentarlo manualmente, para no bloquear tu cuenta con reintentos.

## ¿Es segura la conexión con Sofía Plus?

**No está cifrada, y no depende de la app:** Sofía Plus solo ofrece HTTP. Al ingresar, tu documento y
tu clave viajan sin cifrar, igual que cuando entras desde un navegador. Por eso:

- La app **no entra a Sofía Plus hasta que lo autorizas** en el aviso de la primera extracción.
- El tráfico sin cifrar está permitido **únicamente** para `senasofiaplus.edu.co`; Zajuna y GitHub
  siguen usando HTTPS.
- Conviene evitar la extracción en redes Wi-Fi públicas.

## ¿Cómo se actualizan los datos?

La app usa un modelo **cache-first**: al abrir una pantalla, los datos se cargan instantáneamente desde la base de datos local (Room), y luego se sincronizan en segundo plano con Zajuna. También puedes forzar la sincronización manual con el botón de actualización.

La sincronización automática se programa después del login exitoso y puede configurarse en Ajustes (intervalo de 1 a 6 horas). Los juicios de Sofía Plus son la excepción: aunque la sincronización corra cada pocas horas, solo se extraen una vez al día.

## ¿Qué notificaciones recibo?

La app tiene **5 canales de notificación**:

| Canal | Disparador |
|---|---|
| Sincronización | Progreso de la sincronización en segundo plano |
| Alertas | Evidencias próximas a vencer (≤7 días) y **eventos que vencen hoy** |
| Calendario | Eventos de calendario próximos |
| Anuncios | Nuevos anuncios del curso |
| **Notificaciones del sistema Zajuna** | Mensajes privados, foros, tareas, quizzes, calificaciones, avisos del sistema |

Puedes habilitar/deshabilitar cada tipo individualmente desde Ajustes > Notificaciones.

## ¿Por qué no me vuelve a avisar de algo que ya vi?

Porque cada evento se notifica **una sola vez**. La app lleva un registro de todo lo que ya conoce
(eventos de calendario, anuncios, notificaciones de Zajuna, vencimientos y sesión expirada):

- un evento ya avisado no se repite en las siguientes sincronizaciones, ni tras reiniciar el teléfono;
- al instalar la app, lo que ya existía en Zajuna se toma como historial y no genera avisos;
- si Zajuna no responde, la app no avisa de lo que tiene guardado como si fuera nuevo;
- una evidencia por vencer avisa como mucho dos veces: al entrar en la ventana de 1-3 días y el día del cierre;
- el progreso de sincronización usa una sola notificación que se actualiza, en lugar de varias;
- "Sesión expirada" solo aparece cuando Zajuna rechaza tus credenciales (no por caídas del portal) y se retira sola al recuperar la sesión.

Todo sigue visible en el panel de Notificaciones de la app aunque no genere aviso en el teléfono.

Las **notificaciones del sistema Zajuna** se obtienen vía AJAX (`message_popup_get_popup_notifications`
con `sesskey`, con fallback al popover HTML) y se muestran en una sección dedicada en la pantalla de
Notificaciones (con contador de no leídas, tarjeta clickeable para abrir el detalle in-app + mark-as-read,
y long-press para acciones). El push nativo usa el canal `channel_zajuna_notifications` (importancia HIGH).

Las cabeceras de las tres secciones del panel se apilan progresivamente al deslizar (sin ocultarse
unas a otras); solo se contrae el contenido de cada sección.

## ¿Cómo exporto mis datos?

- **Evidencias a Excel**: Desde Ajustes > Exportar a Excel. Eliges qué exportar —todas, pendientes, evaluadas, por evaluar o vencidas— y se crea un archivo `.xlsx`.
- **Juicios de Sofía Plus a Excel**: en el mismo diálogo, la opción "Juicios evaluativos (Sofía Plus)" crea `Project894_Juicios_SofiaPlus.xlsx` con las columnas Competencia, Resultado de Aprendizaje y Juicio de Evaluación. Requiere haber extraído los juicios antes.
- **Logs de depuración**: Desde Ajustes > Exportar logs. Tras confirmar la advertencia, comprime los registros de los últimos 3 días en un `.zip` y abre el share sheet para compartirlo/guardarlo.

## ¿Cómo funciona la actualización in-app?

Al abrir Ajustes, la app consulta automáticamente los releases del repositorio oficial de GitHub. Si existe una versión más reciente de `Project894-android-*.apk`, muestra un diálogo con la nueva versión y las notas del release. Puedes descargar la actualización con barra de progreso e instalarla directamente desde la app.

También puedes forzar la verificación manual desde Ajustes > Buscar actualizaciones.

## ¿Cómo sé que el APK que descargué es auténtico?

Todos los APK oficiales desde la `2.0.10` están firmados con el mismo certificado, cuya huella SHA-256 es
`bdcf8658236171733ef576587db4db2303a64e9d270e66e9b0c6f3ea6e82e25b`. Puedes comprobarla con
`apksigner verify --print-certs <apk>`. Además, la app verifica su propia firma al iniciar y se bloquea
si fue re-firmada. Por usar siempre la misma firma, la actualización in-app instala las nuevas versiones
sin desinstalar ni perder datos.

## ¿Dónde se guardan los datos localmente?

| Dato | Ubicación |
|---|---|
| Base de datos (Room + SQLCipher) | Almacenamiento interno privado de la app |
| Credenciales | EncryptedSharedPreferences (Android KeyStore) |
| Preferencias de usuario | DataStore (archivo interno) |
| Logs de depuración | Directorio privado de la app (`Android/data/<pkg>/.logs/`); exportación manual vía share sheet |
| APK de actualización | Caché interna de la app (`cache/updates/`) |

## ¿Qué permisos necesita la app?

- **Internet**: Para conectarse a Zajuna, Sofía Plus y GitHub.
- **Notificaciones** (Android 13+): Para mostrar notificaciones push.
- **Instalar apps desconocidas** (solo para actualización): Al descargar una actualización, la app abre el instalador del sistema. Si el permiso no está concedido (Android 8+), la app muestra "Instalación bloqueada" y te guía a Ajustes para activarlo; al volver, la instalación continúa automáticamente.

## ¿Qué pasa si Zajuna cambia su interfaz?

La app usa selectores HTML múltiples y estrategias de extracción resilientes. Si un selector falla, intenta con alternativos. Si la extracción completa falla, puedes intentar más tarde o contactar al desarrollador.

## ¿Puedo usar la app sin conexión?

Parcialmente. Los datos previamente sincronizados (evidencias, anuncios, eventos y juicios de Sofía Plus) están disponibles sin conexión gracias a la caché local. El login requiere conexión a Zajuna, pero si hay credenciales cacheadas válidas, la app puede permitir acceso offline.

## ¿Cómo cierro sesión?

Desde Ajustes, presiona el botón "Cerrar sesión" al final de la pantalla. Esto limpia los datos de la sesión actual.

## ¿Dónde reporto problemas o sugiero mejoras?

En el repositorio oficial: [github.com/ferdcard-ux/Project894](https://github.com/ferdcard-ux/Project894)
