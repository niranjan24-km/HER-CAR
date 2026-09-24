# HERCARE platform

HERCARE is now a local full-stack web app with a responsive, installable PWA shell, a Node.js HTTP API, and a persistent SQLite database. No dependency install is required. Use Node.js 22.13 or later.

## Start it

From this folder, run:

```sh
npm start
```

Open [http://localhost:3000](http://localhost:3000). The database and uploaded files are created under `data/` on first start. Set `PORT` to use another port. The service listens on localhost by default.

## Demo accounts

Sign in with any account below. The role selector signs into the corresponding demo account.

| Role | Email | Password |
| --- | --- | --- |
| Patient | `anaya@hercare.demo` | `Care2026!` |
| Doctor | `meera@hercare.demo` | `Care2026!` |
| Lab | `lab@hercare.demo` | `Care2026!` |

## Included platform flows

- Persistent patient, clinician, lab, pregnancy, visit, medication, consent, pain check-in, emergency alert, lab report, and access history data.
- Password verified sign-in with server sessions in HttpOnly, SameSite cookies.
- Role-limited API routes. Lab accounts can read only their assigned order and upload a report against that order. Clinician patient record access checks patient consent.
- Emergency contacts and location sharing are checked against saved consent before an alert record is created. The alert and “I'm Safe” action persist to the database.
- Pain check-ins save timestamped values and symptoms; the graph reads the saved sequence.
- Patient-facing responsive PWA shell, accessible at localhost and installable where the browser supports it.

The demo accounts are seeded on first launch. The database persists between runs; remove the local `data/` directory to reset demo data. Reports are stored locally under `data/uploads/` and metadata is recorded in SQLite.

## Production boundary

This is a competition prototype, not a production clinical service. Demo credentials and a local SQLite database are provided for evaluation. Alert records do not contact real people or send device location. Replace demo accounts and local data storage with managed identity, encrypted deployment storage, validated backup and retention processes, consent lifecycle management, notification delivery, and security monitoring before a live pilot. Configure clinical escalation rules with qualified clinicians. The platform does not diagnose.
