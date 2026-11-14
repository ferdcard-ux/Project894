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

4. Al abrir la app por primera vez, aparecerá un pop-up de **Términos y Condiciones**. Debes leer el documento completo (desplázate hasta el final), marcar la casilla "He leído y acepto los términos y condiciones" y presionar "Aceptar" para continuar. Si presionas "Rechazar", la app se cierra. El documento incluye la sección 9 "Registros de Depuración" (resumen) con remisión al [DISCLAIMER.md](../DISCLAIMER.md).

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

6. En aperturas posteriores, la app detectará las credenciales cacheadas e intentará el auto-login automáticamente. Si la sesión persistida sigue activa, entra directo sin repetir el WebView.

> **Nota:** Si el login falla por problemas de conexión o cambios en Zajuna, la app puede permitir acceso offline si existen credenciales cacheadas válidas.

---

## 4. Pantalla de Evidencias

Es la pantalla principal donde puedes ver y gestionar todas tus evidencias académicas.

### Barra de búsqueda
Escribe en la barra superior para filtrar evidencias por título o código en tiempo real. Para limpiar la búsqueda, borra el texto.

### Filtros por estado
Usa las pestañas debajo de la barra de búsqueda. Cada pestaña muestra entre paréntesis el total de evidencias que contiene (por ejemplo **Todas: 211**, **Pendientes: 4**, **Evaluadas: 199**, **Vencidas: 3**), recalculado automáticamente cada vez que cambian los datos:
- **Todas**: Muestra todas las evidencias.
- **Pendientes**: Solo evidencias no entregadas.
- **Evaluadas**: Solo evidencias con calificación.
- **Por evaluar**: Evidencias que ya entregaste (tienen recursos cargados en Zajuna) y todavía no registran evaluación. Incluye también las que marcaste a mano como **ENVIADA**.
- **Vencidas**: Solo evidencias cuya fecha de cierre ya pasó y que no entregaste.
- **SofiaPlus**: No son evidencias de Zajuna, sino tus juicios evaluativos de Sofía Plus (ver [Pestaña SofiaPlus](#pestaña-sofiaplus-juicios-evaluativos)).

La fila de pestañas se desliza hacia los lados: **Por evaluar**, **Vencidas** y **SofiaPlus** quedan a la derecha.

> Una evidencia entregada **no pasa a "Vencida"** aunque su fecha de cierre ya haya pasado: se queda en **Por evaluar** hasta que el instructor la califique.

Al tocar una pestaña, la lista se recarga y vuelve al inicio de forma inmediata (no espera una nueva extracción).

### Ver el detalle de una evidencia

**Toca la tarjeta** (no el título) y se abrirá dentro de la app el contenido de la evidencia. Verás:

- **Título, código, etiquetas de estado y fechas** arriba.
- Un **aviso según la pestaña desde la que abriste**: en *Pendientes* los días que faltan para el cierre; en *Evaluadas* la calificación y el comentario; en *Vencidas* el cierre y los días vencidos.
- La **descripción** de la actividad.
- La sección **"Estado de la entrega"**: número de intento, estado de la entrega, estado de la calificación, tiempo restante, última modificación, **archivos enviados** y comentarios.
- En evidencias calificadas, la tabla con la calificación, la fecha, el docente y sus comentarios.

Desde la barra superior puedes **recargar** el contenido o **abrir la evidencia en el navegador** (esta última opción sigue disponible también tocando directamente el título de la tarjeta).

> Las imágenes de la descripción no se muestran en esta vista: en Zajuna son imágenes decorativas que no cargan.

### Etiquetas manuales (pestaña "Todas")

En la pestaña **"Todas"**, cada tarjeta tiene un pequeño botón de etiqueta en su esquina inferior derecha. Al tocarlo se despliega la lista:

| Etiqueta | Cuándo usarla |
|---|---|
| **ENVIADA** | La entregaste y está pendiente de calificar |
| **NO ASIGNADA** | Aún no tiene docente asignado |
| **PENDIENTE** | Te falta entregarla |
| **VENCIDA** | Ya pasó la fecha de cierre |

Reglas del sistema:

- **`EVALUADA` no se puede asignar a mano**: es el estado real en Zajuna y se actualiza solo.
- Si la evidencia **ya tiene esa etiqueta puesta automáticamente**, la opción aparece bloqueada con un candado, para no repetirla.
- Si Zajuna pasa la evidencia a **EVALUADA**, tu etiqueta manual **se quita sola** en la siguiente sincronización: manda el estado real.
- Las etiquetas manuales se conservan aunque sincronices o cambies de dispositivo con la misma cuenta.

### Ordenamiento
Por defecto la lista se ordena **Código A-Z** (orden natural: GA1, GA2… GA10…, EV01, EV02…). Presiona el ícono de ordenamiento para cambiar el criterio. Las opciones varían según el filtro activo:

| Filtro activo | Opciones de ordenamiento |
|---|---|
| Todas / Pendientes / Por evaluar / Vencidas | Default, Código A-Z, Código Z-A, Fecha ↑, Fecha ↓ |
| Evaluadas | Default, Código A-Z, Código Z-A, Calificación (A→F) |
| SofiaPlus | Sin ordenamiento: conserva el orden de Sofía Plus |

### Tarjeta de evidencia
Cada evidencia se muestra como una tarjeta con:
- **Título** (enlace web: presiona para abrir en el navegador)
- **Código** de la evidencia (seleccionable para copiar al portapapeles)
- **Descripción** textual
- **Estado** con insignias de color (puede mostrar **más de una** cuando aplican varias, por ejemplo **Evaluada + Vencida** si está calificada pero su fecha ya pasó):
  - Pendiente / Por vencer (amarillo)
  - Vencida (rojo)
  - Entregada (azul)
  - Por evaluar (morado)
  - Evaluada (verde)
- **Fechas**: Apertura y Cierre
- **Calificación y comentario del instructor** (solo visibles en la pestaña Evaluadas; en Todas quedan ocultos)
- **Instructor** asignado

### Sincronizar datos
Presiona el botón flotante (FAB) con ícono de actualizar para forzar una sincronización manual. Verás un indicador de progreso mientras se actualizan los datos.

Si la pestaña activa es **SofiaPlus**, ese mismo botón actualiza los juicios de Sofía Plus en lugar de las evidencias de Zajuna.

### Pestaña SofiaPlus (juicios evaluativos)

La pestaña **SofiaPlus** muestra los juicios evaluativos que registra Sofía Plus para tu ficha: el estado oficial de cada resultado de aprendizaje.

**Primera vez.** Al tocar la pestaña sin datos, la app muestra un aviso y te pide autorización. Si aceptas con **"Extraer ahora"**, ingresa a Sofía Plus con las mismas credenciales que guardaste para Zajuna (no tienes que escribirlas de nuevo) y trae los juicios. Tarda unos segundos.

> **Conexión sin cifrar:** Sofía Plus no ofrece conexión segura (solo HTTP). Al ingresar, tu documento y tu clave viajan sin cifrar, igual que cuando entras desde un navegador. Evita hacer la extracción en redes Wi-Fi públicas. La app nunca entra a Sofía Plus sin que lo hayas autorizado.

**Qué verás:**

- Una **tarjeta por competencia**, con el número de resultados aprobados (por ejemplo *2 de 4 resultados aprobados*).
- Dentro de cada tarjeta, cada **resultado de aprendizaje** con su juicio:
  - **APROBADO** (verde)
  - **POR EVALUAR** (naranja)
  - **NO APROBADO** (rojo)
- Filtros propios: **Todos**, **Aprobados**, **Por evaluar** y, si existe alguno, **No aprobados**, cada uno con su contador.
- La barra de búsqueda busca por competencia o por resultado de aprendizaje.

**Actualización.** Los juicios cambian poco, así que la app los revisa sola **una vez al día**, dentro de la sincronización en segundo plano. Puedes forzar la actualización cuando quieras con el botón de sincronizar. La franja superior indica cuándo fue la última actualización.

**Sin conexión.** Los juicios quedan guardados en el dispositivo. Si una actualización falla, se conservan los últimos datos.

> Si Sofía Plus rechaza tus credenciales (por ejemplo, porque allí tienes una clave distinta a la de Zajuna), la actualización diaria se pausa para no bloquear tu cuenta con reintentos. Se reanuda cuando actualices manualmente y el ingreso funcione.

---

## 5. Pantalla de Notificaciones

Esta pantalla tiene **tres secciones**. Las tres cabeceras se **apilan progresivamente** al deslizar: cada una se fija arriba y las siguientes se colocan debajo sin ocultar ni empujar a las anteriores; solo se contrae el contenido de cada sección y, al volver arriba, se despliega de nuevo.

### Eventos de Calendario
Muestra los eventos académicos próximos extraídos de Zajuna. Cada evento incluye título y fecha.
La **tarjeta completa es clickeable**: presiona para abrir el evento en el navegador (no hay botón
separado). Mantén presionada la tarjeta para abrir el diálogo de acciones.

### Anuncios
Muestra los anuncios del foro del curso. Cada anuncio incluye título, fecha de publicación e
instructor en líneas separadas. Presiona un anuncio para ver su detalle completo (incluye el
contenido HTML renderizado en un WebView). Mantén presionado un anuncio para abrir el diálogo de
acciones ("Seleccionar texto", "Compartir anuncio", "Abrir en navegador", "Cancelar").

En el detalle, también puedes mantener presionado el contenido del anuncio (incluidos los links del
cuerpo) para abrir el mismo diálogo: "Seleccionar texto" copia el contenido al portapapeles,
"Compartir anuncio" comparte el enlace, "Abrir en navegador" abre el anuncio en el navegador.

### Notificaciones del Sistema Zajuna
Muestra las notificaciones nativas de la plataforma Zajuna/Moodle (mensajes privados, suscripciones a foros, tareas, quizzes, calificaciones, avisos del sistema). Cada notificación incluye:
- **Tipo** con icono: Mensaje (sobre), Foro (burbuja), Tarea (lista), Quiz (cuestionario), Calificación (estrella), Sistema (engranaje), General (campana).
- **Título** y **fecha/hora**.
- **Contador de no leídas** en la cabecera de la sección.
- **Tarjeta clickeable**: presiona para abrir el **detalle dentro de la app** (título + fecha + mensaje, con el mismo formato limpio que los anuncios) y marcarla como leída. Desde la barra superior del detalle puedes abrir la URL original en el navegador.
- **Mantener presionado**: abre diálogo con "Seleccionar texto" (copia al portapapeles), "Compartir notificación", "Abrir en navegador", "Cancelar".

> **Push nativo:** Cuando llega una nueva notificación del sistema, la app muestra una notificación push (canal `channel_zajuna_notifications`, importancia HIGH). Tocar la push abre directamente esta sección del panel con deep link.

> **Toggle en Configuración:** "Notificaciones del sistema Zajuna" para habilitar/deshabilitar individualmente.

> **Carga instantánea:** Los datos se cargan desde la caché local primero (instantáneo), y luego se sincronizan en segundo plano para actualizar la información.

---

## 6. Pantalla de Configuración

### 6.1 Notificaciones

| Opción | Descripción |
|---|---|---|
| Activar notificaciones | Interruptor global de todas las notificaciones |
| Progreso de evidencias | Notificar avance de sincronización de evidencias |
| Progreso de calendario | Notificar avance de sincronización de calendario |
| Progreso de anuncios | Notificar avance de sincronización de anuncios |
| Sincronización completa | Notificar cuando termina la sincronización |
| Alertas evidencias próximas a vencer | Notificar evidencias con ≤7 días al cierre |
| Nuevos anuncios | Notificar cuando hay un nuevo anuncio |
| Eventos de calendario | Notificar eventos próximos |

Los subtipos solo se muestran si el interruptor global está activado.

> **Evento vence hoy:** además, cuando un evento de calendario vence el día actual, la app muestra
> una notificación fija "Evento vence hoy" (no descartable) que se retira automáticamente cuando
> ya no hay eventos que venzan hoy.

> **Sin avisos repetidos:** cada evento (calendario, anuncio, notificación de Zajuna, vencimiento o
> sesión expirada) se notifica en el teléfono **una sola vez**, aunque reinicies el dispositivo. Al
> instalar la app, lo que ya existía se toma como historial. Una evidencia por vencer avisa como mucho
> dos veces (al entrar en la ventana de 1-3 días y el día del cierre). Los avisos de progreso de
> sincronización se muestran en una única notificación que se actualiza. "Sesión expirada" solo
> aparece si Zajuna rechaza tus credenciales y desaparece sola cuando la sesión se recupera.

### 6.2 Sincronización

- **Sincronización automática**: Activa o desactiva la sincronización periódica en segundo plano.
- **Intervalo de sincronización**: Configura cada cuántas horas se sincroniza automáticamente (1 a 6 horas).

### 6.3 Inicio

- **Inicio automático al encender**: Permite que la app se reinicie automáticamente después de un reinicio del dispositivo (requiere configuración adicional según el fabricante).

### 6.4 Datos

| Opción | Descripción |
|---|---|
| Exportar a Excel | Crea un archivo Excel con los datos que elijas (ver la lista de abajo) |
| Exportar logs | Pide confirmación y comparte un `.zip` con los registros de depuración de los últimos 3 días |

Al tocar **Exportar a Excel** eliges qué exportar y luego dónde guardar el archivo:

| Opción | Archivo sugerido | Contenido |
|---|---|---|
| Todas las evidencias | `Project894_Evidencias_Todas.xlsx` | Todo el inventario |
| Evidencias pendientes | `Project894_Evidencias_Pendientes.xlsx` | Las no entregadas |
| Evidencias evaluadas | `Project894_Evidencias_Evaluadas.xlsx` | Las calificadas |
| Evidencias por evaluar | `Project894_Evidencias_PorEvaluar.xlsx` | Las entregadas sin evaluación |
| Evidencias vencidas | `Project894_Evidencias_Vencidas.xlsx` | Las vencidas sin entrega |
| Juicios evaluativos (Sofía Plus) | `Project894_Juicios_SofiaPlus.xlsx` | Competencia, Resultado de Aprendizaje y Juicio de Evaluación |

Para exportar los juicios primero debes haberlos extraído desde la pestaña **SofiaPlus**.

### 6.5 Actualizaciones

- **Buscar actualizaciones**: Verifica manualmente si hay una versión más reciente disponible en GitHub. Si existe, puedes descargarla e instalarla directamente desde la app.
- **Verificación automática**: La app verifica nuevas versiones en segundo plano cada 12 horas. Si hay una actualización, recibirás una notificación en la bandeja del sistema. Al abrir la app, el diálogo de actualización se muestra automáticamente desde cualquier pantalla.

### 6.6 Acerca de

Muestra la versión instalada y enlaces al repositorio, descargo de responsabilidad y ayuda.

### 6.7 Cerrar sesión

Limpia los datos de la sesión actual y regresa a la pantalla de login.

---

## 7. Actualización In-App

La app verifica nuevas versiones de dos formas:

### Automática (segundo plano)
- Cada 12 horas, la app consulta GitHub en segundo plano.
- Si hay una nueva versión, aparece una notificación en la bandeja del sistema.
- Al abrir la app, el diálogo de actualización se muestra automáticamente desde cualquier pantalla.

### Manual
1. Abre la pantalla de **Configuración**.
2. Presiona **"Buscar actualizaciones"**.
3. Si hay una actualización disponible, aparece un diálogo con:
   - Versión nueva y fecha de publicación
   - Notas del release
   - Botón **"Descargar"** y **"Más tarde"**

### Descarga e instalación
1. Presiona **"Descargar"** para iniciar la descarga. Verás una barra de progreso con el porcentaje.
2. Al completar la descarga, presiona **"Instalar ahora"** para abrir el instalador del sistema.
3. Confirma la instalación en la pantalla del sistema Android.
4. En Android 8+, si "Instalar apps desconocidas" no está permitido para la app, aparece el diálogo **"Instalación bloqueada"**: toca **"Abrir ajustes"**, activa el permiso y vuelve a la app; la instalación se reintenta automáticamente.

> **Nota:** Si no hay internet al verificar, la app no muestra ningún mensaje. Puedes forzar la verificación manual desde Ajustes > Buscar actualizaciones.

---

## 8. Exportación de Logs

1. Ve a **Configuración** > **Exportar logs**.

2. Aparece un diálogo de advertencia con la información que pueden contener los registros (dispositivo, curso, trazas de actividad). Presiona **"Aceptar"** para continuar o **"Cancelar"** para abortar.

3. Se comprimen los registros de los últimos 3 días en `Project894_logs_<fecha>.zip` y se abre el **share sheet** del sistema.

4. Elige la aplicación de destino (correo, almacenamiento, etc.) para compartir o guardar el archivo.

> La app conserva automáticamente solo los 3 archivos de log más recientes. Los más antiguos se eliminan. Los registros no se envían a ningún servidor: solo se comparten por acción explícita del usuario. Consulta la sección 4 de [DISCLAIMER.md](../DISCLAIMER.md) para el detalle del descargo de responsabilidad.

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

### La pestaña SofiaPlus no trae juicios
- Lee el mensaje de la franja superior de la pestaña: indica la causa.
- **"Sofía Plus rechazó las credenciales"**: tu clave de Sofía Plus no coincide con la guardada para Zajuna. Verifica que sea la misma en ambos portales y vuelve a intentar con el botón de sincronizar.
- **"No se pudo conectar con Sofía Plus"**: el portal puede estar caído o lento; inténtalo más tarde. Los juicios ya guardados no se pierden.
- **"La cuenta no tiene disponible el rol Aprendiz"**: Sofía Plus no muestra ese rol para tu usuario; confírmalo entrando al portal desde un navegador.

### No llegan notificaciones
- Verifica que las notificaciones estén activadas en Ajustes.
- Revisa los permisos de la app en Ajustes del sistema > Notificaciones.
- En algunos dispositivos, puede ser necesario configurar el auto-inicio en los ajustes del fabricante.

### La app no encuentra actualizaciones
- Verifica tu conexión a internet.
- La app busca releases con el formato `Project894-android-*.apk` en el repositorio oficial.
- Puedes forzar la verificación desde Ajustes > Buscar actualizaciones.
- La verificación automática en segundo plano puede tardar hasta 12 horas en ejecutarse. Si acabas de instalar la app, espera o usa la verificación manual.

---

## 10. Seguridad y Privacidad

- **Credenciales**: Se almacenan cifradas con Android KeyStore + EncryptedSharedPreferences.
- **Base de datos local**: Cifrada con SQLCipher (clave aleatoria protegida por el almacenamiento seguro del dispositivo).
- **Datos en tránsito**: Las conexiones a Zajuna usan TLS real (certificados del sistema + ancla Sectigo para SENA). No se aceptan certificados arbitrarios en producción.
- **Sofía Plus (excepción)**: ese portal solo ofrece HTTP, así que su tráfico —incluidos el documento y la clave al ingresar— viaja sin cifrar. La app lo permite únicamente para `senasofiaplus.edu.co`, lo advierte antes de la primera extracción y no entra a Sofía Plus sin tu autorización. Los juicios extraídos se guardan en la misma base de datos cifrada.
- **La app no recolecta ni transmite datos personales a servidores externos**. Toda la información se procesa y almacena localmente en tu dispositivo.
