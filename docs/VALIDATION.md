# Validation and release evidence

[Back to the showcase](../README.md)

## Reviewed baseline

This case study reviews **Véspera Calendar 1.1.0**, Android version code 3, against private source revision **71ff38c586096885899f10d3e9f793eb05840514**. The review took place on October 21, 2026, Costa Rica time; some report timestamps fall on October 22 in UTC.

The source and original reports remain private. Counts below come from inspected Android report files and the project's release record; they are not a claim that this documentation-only repository runs the private application tests.

| Evidence | Result | Provenance |
| --- | --- | --- |
| Android unit tests | 31 passed, zero failures/errors/skips | Five JUnit XML suites inspected: backup (6), photo (3), store (8), calendar domain (10), and event copies (4). |
| Compose instrumented journeys | 3 passed, zero failures/errors/skips | Connected-test XML inspected for Android 16 / API 36 emulator. |
| Python server tests | 14 passed | Recorded in the 1.1.0 release validation; isolated storage/authentication test fixtures. |
| Private CI | Android and server jobs passed | Workflow run 39714944787 for reviewed revision 71ff38c; success inspected in GitHub. |
| Static checks | Debug/Release Android lint and Python Ruff/format passed | Release and project validation records. |
| Distribution | Signed APK/AAB, alignment, and upgrade installation passed | Recorded 1.1.0 delivery checks; binaries and signing data remain separate. |
| Integration | HTTPS/MySQL backup and recovery, including background photo | Release record documents preserved records, image/opacity/blur recovery, and removal of temporary test data. |

## Behavior covered

- Annual dates, optional year, leap-day policies, search, and range behavior.
- Room save/replace/import behavior and account-separated stores.
- Copying one event and a day, finite daily copies, independent IDs, overnight intervals, daylight-saving transitions, and atomic failure behavior.
- Background image persistence, validation, recovery without the source file, and blur compatibility on Android 8.0.
- Durable pending backups, identical retries, revisions, generation changes, and stale-session rejection.
- Compose journeys for editing and recreation, event/day copies, photo controls, and persistence after activity recreation.

## CI boundary

The private GitHub Actions workflow runs Android unit tests, lint, and debug assembly with JDK 17 / Android SDK 36. The Python job runs Ruff, formatting checks, and unittest with isolated fixtures. Instrumented Compose journeys and signed release verification are separate checks.

The reviewed revision passed private workflow run **39714944787**: Android completed in 4m 58s and server in 12s, with total duration 5m 7s. Both job results were inspected in GitHub. This showcase documents that evidence without displaying a public CI badge for a private repository. The inspected local reports provide the unit and instrumented-test counts above.

## Scope and remaining milestones

- Physical-device coverage across manufacturers and store publication are separate milestones.
- Reminder timing depends on permissions and Android/device power policies; approximate fallback is exposed in the app.
- Remote backup retains the latest complete snapshot per device, not unlimited revision history or live collaborative synchronization.
- Daily repetition creates independent events; full recurring-series rules and editing are outside this reviewed scope.
- Coordinated global identity deletion across the app family remains a separate integration milestone.

## Showcase checks

The public presentation is checked for valid local image/document references, parsable SVG, complete English/Spanish README sections, safe file types, image provenance, and accidental credentials. No production endpoints, private source history, database contents, or signing material are copied into this repository.
