# Nota sobre la limpieza de artefactos

**Fecha:** 2026-08-20

## Que sucedio

Se eliminaron los **assets binarios** de todas las releases anteriores a la version Android `2.0.10`,
incluida la `2.0.9` (cuyo artefacto `Project894-android-2.0.9.apk` fue retirado del release `v2.0.9`).
Se conserva unicamente el artefacto:

- `Project894-android-2.0.10.apk` (release `v2.0.10`)

El historial de releases, sus notas y los tags de version se mantienen intactos. Solo se retiraron los
archivos binarios adjuntos.

## Por que se eliminaron

- **Linux y Windows:** las versiones publicadas (`v1.1.0`, `v1.2.0`, `v1.3.0`) son antiguas y a la
  fecha presentan fallos graves de funcionalidad y seguridad. Mantener descargables binarios con esos
  problemas expone a los usuarios a versiones defectuosas.
- **Android anterior a 2.0.10:** aunque muchas de esas versiones son funcionales, conservan algunos
  fallos conocidos que ya estan corregidos en la `2.0.10`. Se deja disponible unicamente la version
  estable y corregida.
- **Android 2.0.9:** retirado porque la `2.0.10` la reemplaza (mismo certificado de firma heredado
  desde `2.0.9`, hardening anti-ingenieria inversa y correccion de Terminos/DISCLAIMER).

## Que se esta haciendo al respecto

Se esta trabajando en el desarrollo de las **nuevas versiones para Linux y Windows** con las
correcciones correspondientes. Estas nuevas compilaciones se publicaran en este repositorio cuando
esten validadas y listas para distribucion.

## Estado actual de los artefactos disponibles

| Plataforma | Version | Artefacto | Estado |
|---|---|---|---|
| Android | 2.0.10 | `Project894-android-2.0.10.apk` | Disponible (release `v2.0.10`) |
| Linux | — | `Project894-x86_64.AppImage` | En desarrollo (retirado temporalmente) |
| Windows | — | `Project894.exe` | En desarrollo (retirado temporalmente) |

## Notas

- La actualizacion in-app de Android sigue funcionando: los dispositivos con versiones anteriores a
  la `2.0.10` detectan la `2.0.10` como ultima version y pueden actualizar normalmente.
  La rotacion del certificado de firma de la `2.0.10` implica que el primer paso desde `2.0.9` requiere
  instalacion manual (una unica vez); desde la `2.0.10` en adelante la actualizacion in-app vuelve a
  funcionar con normalidad.
- Para soporte o reporte de problemas, consulta [CONTRIBUTING.md](CONTRIBUTING.md) y
  [SECURITY.md](SECURITY.md).
