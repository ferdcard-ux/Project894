# Nota sobre la limpieza de artefactos

**Fecha:** 2026-11-14

## Que sucedio

Se retiraron los **assets binarios** de las releases Android anteriores a la version vigente.
La version activa es la `2.0.14`:

- `Project894-android-2.0.14.apk` (release `v2.0.14`)

El historial de releases, sus notas y los tags de version se mantienen intactos. Solo se retiran los
archivos binarios adjuntos de las versiones reemplazadas.

## Por que se eliminaron

- **Linux y Windows:** las versiones publicadas (`v1.1.0`, `v1.2.0`, `v1.3.0`) son antiguas y a la
  fecha presentan fallos graves de funcionalidad y seguridad. Mantener descargables binarios con esos
  problemas expone a los usuarios a versiones defectuosas.
- **Android anterior a la version vigente:** aunque muchas de esas versiones son funcionales,
  conservan fallos conocidos que ya estan corregidos. Se deja disponible unicamente la version
  estable y corregida.
- **Android 2.0.13:** reemplazada por la `2.0.14` (misma firma que 2.0.10 en adelante, juicios de
  Sofia Plus, pestana "Por evaluar", avisos sin repeticiones y conservacion de estados ante fallos de
  Zajuna).

## Que se esta haciendo al respecto

Se esta trabajando en el desarrollo de las **nuevas versiones para Linux y Windows** con las
correcciones correspondientes. Estas nuevas compilaciones se publicaran en este repositorio cuando
esten validadas y listas para distribucion.

## Estado actual de los artefactos disponibles

| Plataforma | Version | Artefacto | Estado |
|---|---|---|---|
| Android | 2.0.14 | `Project894-android-2.0.14.apk` | Disponible (release `v2.0.14`) |
| Linux | — | `Project894-x86_64.AppImage` | En desarrollo (retirado temporalmente) |
| Windows | — | `Project894.exe` | En desarrollo (retirado temporalmente) |

## Notas

- La actualizacion in-app de Android sigue funcionando: los dispositivos con versiones anteriores
  detectan la `2.0.14` como ultima version y pueden actualizar normalmente.
  La rotacion del certificado de firma de la `2.0.10` implica que el primer paso desde `2.0.9`
  requiere instalacion manual (una unica vez); desde la `2.0.10` en adelante la actualizacion in-app
  funciona con normalidad (misma firma 2.0.10 -> ... -> 2.0.13 -> 2.0.14).
- Para soporte o reporte de problemas, consulta [CONTRIBUTING.md](CONTRIBUTING.md) y
  [SECURITY.md](SECURITY.md).
