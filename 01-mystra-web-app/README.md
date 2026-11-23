# MySTRA â€” Malaysia Short-Term Rental Accommodation system

Coursework project for **Collaborative Development**. A browser-based system that lets
short-term rental hosts register their properties and keep their compliance documents in one
place, and lets government administrators verify and audit them.

## What it does

**Host side**
- Register / login, with email verification and password reset
- Upload and manage compliance documents (SSM business certificate, tax information, safety
  certification)
- View submission status and government feedback
- Location and map view for registered properties

**Government / admin side**
- Dashboard with submission counts and status
- Review and verify uploaded documents
- Audit trail of admin actions
- Reports and feedback handling

**Data migration**
- A migration engine that maps records from a simulated legacy system into the new schema
- Batch / daily migration scripts and a legacy compare page, so old records can be checked
  against the new ones after import

## Stack

Plain HTML, CSS and JavaScript (no framework), Supabase for authentication and storage,
and a small set of Node scripts for the migration jobs.

## How to run

The pages are static. Serve the folder with any static server, for example:

```bash
python -m http.server 8080
```

then open `http://localhost:8080/index.html`. Supabase keys live in `supabase-config.js`;
replace them with your own project's values before running against a real backend.

## My contribution

I built the **government admin side**: the review queue (inspect a PENDING submission,
approve or reject it), the audit log that records each admin decision, the reports and
feedback pages, and the session guard on every admin page. The host portal and the legacy
migration engine were built by my teammate.

## Note

Built as a team project for the course. The sample files in `samples/` are dummy documents
used for the demo, not real business records.
