# KB Studio CRM

Business management system for KB Studio Productions — client quotations, project pipeline, payments, and post-production tracking.

## Deployment

**This repo is the live site.** `index.html` in the `main` branch is auto-published to **crm.kbstudio.in** via GitHub Pages on every push — no separate manual upload step.

To ship a change:
1. Edit / replace `index.html` in this repo (via "Add file → Upload files", or a normal commit)
2. Push to `main`
3. GitHub Pages redeploys automatically within a few minutes
4. Check the **Deployments** panel on the repo homepage (right sidebar) to confirm the new deployment succeeded

There is no other deploy step, no build process, and no separate hosting to update — the file in this repo *is* what's live.

## Stack

Single-file HTML/CSS/JS app. Uses:
- Firebase Realtime Database (client data, projects, quotations, payments)
- Chart.js, jsPDF, html2canvas, SheetJS (xlsx), pdf.js — loaded via CDN

## Notes for future changes

- Quotation → Project conversion writes to two places (`crm_projects` and `crm_quotations`). Both writes now have error handling and retry — if you touch `convertQuotToProject()`, keep both writes verified before showing a success message to the user.
- Advance-payment display (`_quotLiveAdvance`, `_quotLinkedProject`) checks both current (`kb_advance`) and legacy (`p30`/`p20`/`p50a`/`cp0`) payment stage keys, and self-heals broken quotation↔project links on page load. See inline comments near those functions before modifying.
