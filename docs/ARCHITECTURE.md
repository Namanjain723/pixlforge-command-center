# Architecture

The Business Command Center is a **serverless web application** built entirely on the Google
Workspace platform. There is no traditional backend, no database server and no hosting cost.

## The three layers

### 1. Data layer — Google Sheets
A single **Master Sheet** acts as the database. Each tab is a table:
- `Employees` — name, location, department, FMS access, photo, email
- `Tasks` / `Delegation` — assignments, deadlines, status, scoring
- `MIS` — weekly performance scores per employee
- `Alteration FMS` — live job pipeline rows
- `Messages`, `Notices`, `Training` — operational content

Non-technical managers maintain everything from a familiar spreadsheet.

### 2. API layer — Google Apps Script Web Apps
Several Apps Script projects expose the sheets as JSON APIs via `doGet(e)` endpoints,
addressed with `?action=...` query parameters. Examples:
- `?action=all` — full sync payload for the dashboard
- `?action=getMISReport&week=WEEK-8` — performance scores
- `?action=getTasksForEmployee&name=...` — delegation tasks
- `?action=updateEmployeeStatus&...` — mark a task done

Each web app is deployed once and keeps a stable URL, so the frontend never changes when
data updates.

### 3. Presentation layer — single-file dashboard
The entire UI is one portable `index.html`:
- **Vanilla JavaScript** — zero framework, instant load, trivial to host anywhere.
- **Chart.js** — HR, FMS, revenue and performance charts.
- **Web Speech API** — the voice assistant (speech recognition + text-to-speech).
- **CSS variables** — the dark/light theming system.

It can be hosted on **Netlify** (drag-and-drop) or served directly from **Apps Script** as a
web app embedded over the sheets.

## Demo Mode (this repository)
When the dashboard detects that no live Apps Script URLs are configured, it activates a
self-contained **Demo Mode** that synthesizes realistic scores, alteration jobs and staff
activity on the fly — so the public demo is fully interactive with no backend at all.

```
Manager edits Sheet ──▶ Apps Script doGet returns JSON ──▶ Dashboard renders live
        ▲                                                          │
        └──────────────  Mark Done / Delegate / Message  ◀─────────┘
```

## Why this stack
- **Ownership** — the business owns its data and tools outright; nothing to cancel.
- **Zero recurring cost** — no SaaS subscription, no server bill.
- **Familiar** — managers keep using Google Sheets; staff use a clean web app.
- **Portable** — the frontend is one file; the backend is copy-paste Apps Script.
