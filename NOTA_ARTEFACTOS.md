# Nota sobre la limpieza de artefactos

**Fecha:** 2026-10-12

## Que sucedio

Se retiraron los **assets binarios** de las releases Android anteriores a la version `2.0.12`,
incluida la `2.0.11` (cuyo artefacto `Project894-android-2.0.11.apk` fue retirado del release `v2.0.11`
tras publicarse la `2.0.12`). Se conserva unicamente el artefacto:

- `Project894-android-2.0.12.apk` (release `v2.0.12`)

El historial de releases, sus notas y los tags de version se mantienen intactos. Solo se retiraron los
archivos binarios adjuntos.

## Por que se eliminaron

- **Linux y Windows:** las versiones publicadas (`v1.1.0`, `v1.2.0`, `v1.3.0`) son antiguas y a la
  fecha presentan fallos graves de funcionalidad y seguridad. Mantener descargables binarios con esos
  problemas expone a los usuarios a versiones defectuosas.
- **Android anterior a 2.0.12:** aunque muchas de esas versiones son funcionales, conservan algunos
  fallos conocidos que ya estan corregidos en la `2.0.12`. Se deja disponible unicamente la version
  estable y corregida.
- **Android 2.0.10 y 2.0.11:** retiradas porque la `2.0.12` las reemplaza (misma firma que 2.0.10/2.0.11,
  orden A-Z por defecto, contadores por pestana, etiquetas multiples, detalle in-app de notificaciones,
  exportacion XLSX sin dependencias).

## Que se esta haciendo al respecto

Se esta trabajando en el desarrollo de las **nuevas versiones para Linux y Windows** con las
correcciones correspondientes. Estas nuevas compilaciones se publicaran en este repositorio cuando
esten validadas y listas para distribucion.

## Estado actual de los artefactos disponibles

| Plataforma | Version | Artefacto | Estado |
|---|---|---|---|
| Android | 2.0.12 | `Project894-android-2.0.12.apk` | Disponible (release `v2.0.12`) |
| Linux | — | `Project894-x86_64.AppImage` | En desarrollo (retirado temporalmente) |
| Windows | — | `Project894.exe` | En desarrollo (retirado temporalmente) |

## Notas

- La actualizacion in-app de Android sigue funcionando: los dispositivos con versiones anteriores a
  la `2.0.12` detectan la `2.0.12` como ultima version y pueden actualizar normalmente.
  La rotacion del certificado de firma de la `2.0.10` implica que el primer paso desde `2.0.9`
  requiere instalacion manual (una unica vez); desde la `2.0.10` en adelante la actualizacion in-app
  vuelve a funcionar con normalidad (misma firma 2.0.10 -> 2.0.11 -> 2.0.12).
- Para soporte o reporte de problemas, consulta [CONTRIBUTING.md](CONTRIBUTING.md) y
  [SECURITY.md](SECURITY.md).
