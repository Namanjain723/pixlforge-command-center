# Data, Privacy & Anonymization

This repository is a **public showcase** of a system that was originally built for a real
client. Protecting that client's data was a hard requirement, so this demo was produced from a
sanitized copy in which **no real data exists**.

## What was removed and replaced

| Real (private) | In this public demo |
|---|---|
| Employee names | Fictional names (randomly generated) |
| Employee photos | Generated **initials avatars** — no images leave any system |
| Employee / manager emails | `@metroretail.demo` placeholders |
| Company & store branding | A fictional brand, **Metro Retail Co.** |
| Master Google Sheet ID | Removed |
| Live Apps Script web-app URLs (5) | Removed |
| Weather / third-party API keys | Removed |
| Google Drive / Sheet file IDs | Removed |
| Phone numbers | Removed |

## How the demo still works without real data
The dashboard ships with an embedded, fictional staff directory and a **Demo Mode** module that
generates believable performance scores and alteration jobs at runtime. No network backend is
contacted, so there is nothing to leak.

## Production security model
In a real deployment:
- Apps Script web apps are deployed under the **owner's Google account**.
- Manager-only actions are gated server-side.
- The master sheet is shared only with the operations team.
- The dashboard is hosted privately (Netlify or Apps Script) behind the company's access.

## A note for evaluators
Because the sample data is fictional, **none of the figures, names or scores in this demo are
real**. They exist purely to demonstrate the interface and capability of the system.
