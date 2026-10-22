# Engineering decisions

[Back to the showcase](../README.md)

## 1. Separate annual dates from timed events

An event at a particular time, a day off, and a birthday do not share the same time semantics. Timed events retain instants and an origin zone; all-day records use civil dates. Birthdays and anniversaries retain month/day and project annual occurrences without persisting another row each year.

An optional origin year supports meaningful counts without forcing users to invent a year. A February 29 policy makes non-leap-year behavior explicit.

## 2. Validate an entire copy operation before saving

Copying a day can produce several records. The batch is fully validated before one Room transaction, and its successful application advances the store version once. Each copy receives a new ID and initial revision. Reminder reconciliation runs after the change.

Copies preserve local clock time on the destination date, including overnight duration semantics. Daylight-saving gaps and overlaps need explicit resolution; adding a fixed 24-hour offset would not preserve local time in every zone.

The finite daily option creates independent records over at most 366 days. This keeps later edits straightforward, at the cost of not providing a general recurring-series editor or RFC 5545 recurrence engine.

## 3. Treat reminders as reconciled state

An alarm scheduled once can become stale after a time-zone change, edit, reboot, or permission change. Reconciliation recalculates the desired state. Delivery deduplication includes the account, record revision, occurrence date, and trigger.

Exact alarms are used when permitted; the application reports an approximate fallback otherwise. Notification permission, channel settings, privacy options, and device power policies remain relevant to actual delivery.

## 4. Make background photos portable

A file URI can stop working after reinstalling or moving to another device. Véspera normalizes the image and carries it in the full snapshot with opacity and blur. Recovery therefore works without the original photo or a surviving permission grant.

The payload is bounded, older snapshots remain accepted, and contrast treatment keeps the calendar usable. Including image data makes snapshots larger than record-only exports; the fixed size limit bounds that tradeoff.

## 5. Retry the original backup request

A server may commit a request even if the client loses its response. Regenerating the snapshot during a retry could silently change the content associated with a revision. Véspera persists the pending payload, device, revision, and generation before sending it and retries those values unchanged.

A canonical content hash excludes the export timestamp. The server can distinguish an identical retry from conflicting content. Generation checks reject uploads left over from before a remote-backup deletion. Session-epoch checks before and after requests prevent stale results from affecting a different session.

## 6. Share identity while separating app data

Nimbo Player and Véspera share username/password identity and visual foundations. Véspera owns its calendar store, backup service, and logical database boundary. Its token is encrypted through Android Keystore; this is token protection, not a claim of end-to-end encrypted calendar backups.

The current scope includes deleting Véspera's remote backups. Coordinated global account deletion across the app family remains a separate integration milestone. Neither a shared identity nor device backup implies a multi-user shared calendar.

## 7. Build checks around failure cases

Tests cover annual projection, date/time edge cases, transactional persistence, duplicate prevention, session boundaries, durable backup retries, and photo portability. Compose journeys exercise multi-step behavior instead of only checking labels. Private CI runs Android unit tests, lint and debug assembly plus Python lint, format and isolated tests; instrumented UI journeys are run separately.

[Validation evidence and limits](VALIDATION.md)
