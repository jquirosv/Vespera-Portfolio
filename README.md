<p align="center"><img src="https://raw.githubusercontent.com/jquirosv/Vespera-Portfolio/d169cb45068af73a812abd000e258477ce130af6/docs/assets/00-cover.svg" alt="Véspera Calendar — Your days, your way." width="100%"></p>

# Véspera Calendar

**A native Android calendar for everyday plans, meaningful dates, and a style of your own.**

Bring events, birthdays, and anniversaries into one place. Shape the experience with personal colors, typography, and a photo background, then keep a complete backup of your calendar and its appearance.

**Kotlin · Jetpack Compose · Room · AlarmManager · Python / Flask · MySQL**

[Product tour](docs/PRODUCT_TOUR.md) · [Architecture](docs/ARCHITECTURE.md) · [Engineering decisions](docs/ENGINEERING.md) · [Validation](docs/VALIDATION.md) · [Español](#español)

## The experience

<p align="center">
  <img src="docs/assets/01-calendar.png" alt="Véspera Calendar monthly view with the current calendar mark" width="30%">
  &nbsp;
  <img src="docs/assets/02-styles.png" alt="Dark appearance screen with six style presets and a personal style" width="30%">
  &nbsp;
  <img src="docs/assets/03-photo-background.png" alt="Photo background preview with opacity and blur controls" width="30%">
</p>

<p align="center"><sub>Calendar · Personal styles · Photo background. Actual app captures; the style screen comes from an earlier build. See <a href="docs/assets/README.md">versions and asset provenance</a>.</sub></p>

## Why I built it

I wanted a calendar that makes everyday organization feel personal, while treating birthdays and anniversaries as dates that matter every year. Véspera combines that visual approach with careful handling of time, reminders, local data, and recovery.

I developed the Android application and its backup API, including the interface, calendar domain, persistence, reminders, account integration, and delivery workflow. **Véspera Calendar 1.1.0** supports **Android 8.0 and later**.

Véspera belongs to the same app family as [Nimbo Player](https://github.com/jquirosv/Nimbo-Portfolio). They share a visual language and username/password identity; each app keeps its own session, local data, and backup service.

## What it does

| Area | Capabilities |
| --- | --- |
| Daily planning | Month and agenda views, date navigation, accent-insensitive search, and filters by record type. |
| Events | Timed, all-day, and multi-day events with written location, notes, and reminders. |
| Copies and repetition | Copy one event or a day's visible events; repeat a daily schedule over a finite period of up to 366 days as independent events. |
| Special dates | Birthdays and anniversaries, optional origin year, annual projection, and a configurable February 29 policy. |
| Personalization | Six presets, personal light/dark styles, custom colors, 33 offline fonts, and a background photo with opacity and blur. |
| Reminders | Local scheduling, permission status, exact-alarm support where permitted, approximate fallback, and notification privacy settings. |
| Account separation | Shared Nimbo identity, encrypted session tokens, and separate local databases for each account. |
| Backup and recovery | Complete JSON file export/import, manual and scheduled remote backup, and restore previews including appearance and background photo. |

An account is required for initial access. After sign-in, calendar viewing and editing work offline; account checks and remote backups use a network connection. The backend retains the latest complete snapshot per device. Daily repetition creates separately editable events, and remote backup is snapshot-based rather than continuous collaborative synchronization.

## A closer look

<p align="center">
  <img src="docs/assets/04-event-copies.png" alt="Calendar after copying two fictional rehearsal events to another day" width="30%">
  &nbsp;
  <img src="docs/assets/05-account-backup.png" alt="Demo account screen with manual backup and restore controls" width="30%">
</p>

<p align="center"><sub>Event copies · Account and recovery. The rehearsal events and the “journey” identity are automated-test fixtures.</sub></p>

## Engineering highlights

- **Dates modeled by meaning.** Timed events retain their instant and origin time zone; all-day events use civil dates. Annual dates are projected without saving a duplicate for every year.
- **Atomic calendar changes.** Event-copy batches validate before a Room transaction, preserve local clock time across dates, and account for daylight-saving gaps and overlaps.
- **Reminder reconciliation.** Alarm scheduling responds to boot, clock, time-zone, and permission changes. Delivery keys include account, record revision, occurrence, and trigger to suppress duplicates.
- **Recoverable personalization.** A normalized background image is included in the full snapshot, so recovery does not depend on access to the original photo file.
- **Stable backup retries.** Pending requests retain their payload and revision. Content hashes support idempotent retries; session and generation checks prevent stale work from crossing account or deletion boundaries.

[Read the architecture](docs/ARCHITECTURE.md) · [Explore the tradeoffs](docs/ENGINEERING.md)

## Technology stack

| Layer | Technologies |
| --- | --- |
| Interface and state | Kotlin, Jetpack Compose, Material 3, ViewModel, StateFlow, coroutines |
| Local calendar | Room / SQLite, KSP, java.time |
| Android integration | AlarmManager, notifications, WorkManager, Android Keystore, native photo picker |
| Backup service | Python, Flask, Gunicorn, PyMySQL, MySQL, Docker |
| Quality and delivery | JUnit, Robolectric, Compose UI tests, Python unittest, Ruff, Gradle, GitHub Actions |

## Quality and scope

The reviewed 1.1.0 release records **31 Android unit tests, 14 server tests, and 3 Compose UI journeys passing**. The Android unit and connected-test XML reports were inspected for this showcase. Release records also cover Debug/Release lint, signed APK/AAB generation, upgrade installation, and backup/restore integration over HTTPS/MySQL.

The [validation notes](docs/VALIDATION.md) distinguish inspected test reports, recorded release checks, and CI coverage. Physical-device coverage and store publication are separate milestones.

## About this repository

This is a public product and engineering case study. Application source, production configuration, signing material, and installable releases are maintained separately. This repository contains presentation text, diagrams, and reviewed images.

**Author:** [José Pablo Quirós Vásquez](https://github.com/jquirosv) · [LinkedIn](https://www.linkedin.com/in/jquirosv/)

[Asset provenance](docs/assets/README.md) · [Copyright](COPYRIGHT.md)

---

## Español

<details>
<summary>Español — presentación completa</summary>

## Véspera Calendar en español

**Un calendario nativo para Android que reúne tus planes, las fechas importantes y tu propio estilo.**

Organiza eventos, cumpleaños y aniversarios en un mismo lugar. Personaliza colores, tipografía y foto de fondo, y conserva una copia completa del calendario con su apariencia.

**Kotlin · Jetpack Compose · Room · AlarmManager · Python / Flask · MySQL**

### La experiencia

<p align="center">
  <img src="docs/assets/01-calendar.png" alt="Vista mensual de Véspera Calendar con su marca actual" width="30%">
  &nbsp;
  <img src="docs/assets/02-styles.png" alt="Estilos oscuros y estilo personal en una compilación anterior" width="30%">
  &nbsp;
  <img src="docs/assets/03-photo-background.png" alt="Vista previa de la foto de fondo con opacidad y desenfoque" width="30%">
</p>

Calendario, estilos personales y foto de fondo. Son capturas reales de la aplicación; la pantalla de estilos pertenece a una compilación anterior. Las versiones y los datos de demostración se detallan en la [guía de recursos](docs/assets/README.md).

### Por qué lo desarrollé

Quería un calendario que hiciera más personal la organización diaria y tratara los cumpleaños y aniversarios como fechas importantes cada año. Véspera combina esa propuesta visual con un manejo cuidadoso del tiempo, los recordatorios, los datos locales y la recuperación.

Desarrollé la aplicación Android y su API de respaldos: interfaz, lógica del calendario, persistencia, recordatorios, integración de cuentas y flujo de entrega. **Véspera Calendar 1.1.0** funciona desde **Android 8.0**.

Forma parte de la misma familia que [Nimbo Player](https://github.com/jquirosv/Nimbo-Portfolio). Comparten el lenguaje visual y la identidad mediante usuario y contraseña; cada aplicación conserva su propia sesión, datos locales y servicio de respaldos.

### Funciones

| Área | Capacidades |
| --- | --- |
| Organización diaria | Vista mensual y agenda, navegación por fechas, búsqueda sin distinción de acentos y filtros por tipo. |
| Eventos | Con horario, de todo el día o de varios días, con ubicación escrita, notas y recordatorios. |
| Copias y repetición | Copiar un evento o los eventos visibles de un día; repetir un horario en un período de hasta 366 días mediante eventos independientes. |
| Fechas especiales | Cumpleaños y aniversarios, año de origen opcional, proyección anual y política configurable para el 29 de febrero. |
| Personalización | Seis estilos, estilos personales claros y oscuros, colores, 33 fuentes sin conexión y foto de fondo con opacidad y desenfoque. |
| Recordatorios | Programación local, estado de permisos, alarmas exactas cuando están permitidas, alternativa aproximada y privacidad de las notificaciones. |
| Separación por cuenta | Identidad compartida con Nimbo, tokens de sesión cifrados y bases locales independientes por cuenta. |
| Respaldo y recuperación | Exportación e importación JSON completas, respaldo remoto manual y programado, y vista previa de recuperación con apariencia y foto. |

El acceso inicial requiere una cuenta. Después del ingreso, la consulta y la edición funcionan sin conexión; las comprobaciones de cuenta y los respaldos remotos usan la red. El servidor conserva la última copia completa por dispositivo. La repetición diaria crea eventos editables por separado y el respaldo funciona mediante instantáneas, sin sincronización colaborativa continua.

### Más de cerca

<p align="center">
  <img src="docs/assets/04-event-copies.png" alt="Calendario después de copiar dos ensayos ficticios a otro día" width="30%">
  &nbsp;
  <img src="docs/assets/05-account-backup.png" alt="Cuenta de demostración con controles de respaldo y recuperación" width="30%">
</p>

Copias de eventos y recuperación. Los ensayos y la identidad “journey” pertenecen a las pruebas automatizadas.

### Decisiones técnicas destacadas

- **Cada fecha tiene su significado.** Los eventos con horario conservan su instante y zona de origen; los de todo el día usan fechas civiles. Las fechas anuales se proyectan sin guardar un duplicado por año.
- **Cambios atómicos.** Las copias se validan antes de una transacción Room, mantienen la hora local y contemplan los saltos y las ambigüedades del horario de verano.
- **Conciliación de recordatorios.** La programación se revisa tras reinicios y cambios de hora, zona o permisos. Las claves de entrega incluyen cuenta, revisión, ocurrencia y disparador para evitar duplicados.
- **Personalización recuperable.** La imagen normalizada se incluye en la copia completa; restaurarla no depende del archivo original.
- **Reintentos estables.** Los envíos pendientes conservan contenido y revisión. Las huellas del contenido permiten reintentos idempotentes, y las comprobaciones de sesión y generación descartan trabajo obsoleto.

### Tecnologías

| Capa | Tecnologías |
| --- | --- |
| Interfaz y estado | Kotlin, Jetpack Compose, Material 3, ViewModel, StateFlow, corrutinas |
| Calendario local | Room / SQLite, KSP, java.time |
| Integración Android | AlarmManager, notificaciones, WorkManager, Android Keystore, selector de fotos nativo |
| Servicio de respaldos | Python, Flask, Gunicorn, PyMySQL, MySQL, Docker |
| Calidad y entrega | JUnit, Robolectric, pruebas Compose, Python unittest, Ruff, Gradle, GitHub Actions |

### Calidad y alcance

La entrega revisada 1.1.0 registra **31 pruebas unitarias Android, 14 del servidor y 3 recorridos Compose aprobados**. Para esta presentación se inspeccionaron los informes XML de las pruebas Android y de interfaz. El registro de entrega también documenta análisis Debug/Release, generación de APK/AAB firmados, instalación de actualización y recuperación real mediante HTTPS/MySQL.

Las [notas de validación](docs/VALIDATION.md) distinguen los informes inspeccionados, las comprobaciones registradas y la cobertura de CI. La cobertura en teléfonos físicos y la publicación en tiendas son hitos separados.

### Sobre este repositorio

Esta es la presentación pública del producto y sus decisiones técnicas. El código, la configuración de producción, las claves de firma y las distribuciones se mantienen por separado. Aquí se publican documentación, diagramas e imágenes revisadas.

**Autor:** [José Pablo Quirós Vásquez](https://github.com/jquirosv) · [LinkedIn](https://www.linkedin.com/in/jquirosv/)

Documentación técnica ampliada en inglés: [recorrido](docs/PRODUCT_TOUR.md), [arquitectura](docs/ARCHITECTURE.md), [decisiones](docs/ENGINEERING.md) y [validación](docs/VALIDATION.md).

</details>
