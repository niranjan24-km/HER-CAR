# HERCARE platform

HERCARE is now a local full-stack web app with a responsive, installable PWA shell, a Node.js HTTP API, and a persistent SQLite database. No dependency install is required. Use Node.js 22.13 or later.

## Put it online from GitHub with Render

The repository must contain the project files directly in its top level. Do not upload only the ZIP: Render needs to see `render.yaml`, `server.js`, and `package.json` in the repository. Upload the extracted files from `HERCARE-platform-upload.zip` to the root of the GitHub repository.

1. Create or sign in to a Render account at [render.com](https://render.com).
2. In the Render dashboard choose **New → Blueprint**.
3. Connect your GitHub account if asked, then select `niranjan24-km/HER-CARE`.
4. Review the planned service. The `render.yaml` file creates a Node web service and a 1 GB persistent disk for the SQLite database and uploaded reports.
5. This configuration uses Render's paid Starter service so the local SQLite database persists. The current listed price is about $7/month for the service plus $0.25/month for the 1 GB disk; check [Render pricing](https://render.com/pricing) before deploying because prices can change.
6. Wait for deployment to finish, then open the `onrender.com` address shown on the service page.

The app is also installable from the browser's install control once opened over its secure Render URL. Render Blueprints are created from **New → Blueprint** and use the `render.yaml` file at the repository root, as described in [Render's Blueprint guide](https://render.com/docs/infrastructure-as-code).

## Start it

From this folder, run:

```sh
npm start
```

On Windows PowerShell, if `npm start` is blocked by the system script setting, run `node server.js` instead.

Open [http://localhost:3000](http://localhost:3000). The database and uploaded files are created under `data/` on first start. Set `PORT` to use another port. The service listens on port 3000 by default.

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

The demo accounts are seeded on first launch. The database persists between local runs; remove the local `data/` directory to reset demo data. On Render, database and report files use the configured persistent disk at `/var/data`.

## Production boundary

This is a competition prototype, not a production clinical service. Demo credentials and illustrative patient data are provided for evaluation. Anyone who can reach the deployed demo can use its published demo credentials. Do not enter real patient information. Alert records do not contact real people or send device location. Replace demo accounts and local data storage with managed identity, encrypted deployment storage, validated backup and retention processes, consent lifecycle management, notification delivery, and security monitoring before a live pilot. Configure clinical escalation rules with qualified clinicians. The platform does not diagnose.
