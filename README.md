# IT Systems Ltd — Support Site

A single-file, mobile-friendly support hub suitable for Microsoft CSP enrollment. Host at `https://support.itsystems.ltd`.

## Files
- `index.html` — the entire site
- `assets/logo.svg` — editable SVG logo
- `assets/favicon.svg` — favicon
- `assets/site.webmanifest` — PWA basics

## Quick Deploy Options

### GitHub Pages (static hosting)
1. Create a new repo (e.g. `itsystems-support`).
2. Upload all files from this folder.
3. In repo settings → Pages → set branch to `main`, folder `/root`.
4. Map your DNS `support.itsystems.ltd` (CNAME) to `<username>.github.io`.
5. Visit `https://support.itsystems.ltd`.

### Any cPanel / NGINX / IIS
- Copy all files to the site root folder.
- Ensure HTTPS is enabled (Let's Encrypt or your provider's certificate).
- Test: open `/index.html`.

## Contact Form (two paths)
- **No backend:** the form falls back to a `mailto:` link and opens the user's email client addressed to `support@itsystems.ltd`.
- **Recommended:** connect to **Azure Logic Apps** or **Power Automate** (HTTP trigger) and set `FORM_ENDPOINT` in `index.html`.

### Sample JSON payload sent to your endpoint
```json
{ "name": "Jane Doe", "email": "jane@example.com", "subject": "License change", "message": "Please assign M365 E3" , "source": "support.itsystems.ltd"}
```

### Example: Azure Logic Apps quick setup
1. Create Logic App (Consumption) → **HTTP Request** trigger.
2. Schema (optional): accept any JSON.
3. Add action **Send an email (V2)** to `support@itsystems.ltd`.
4. Save the app → copy the **HTTP POST URL**.
5. Edit `index.html` and set:
```js
const FORM_ENDPOINT = "https://YOUR-LOGIC-APP-URL";
```
6. Commit & deploy. Submit a test ticket.

## Customise
- Edit header title, FAQ, SLA targets inside `index.html`.
- Replace `assets/logo.svg` with your brand (keep the same filename).
- Update contact details globally (email, phone, hours) at the top of this README and within the HTML (search for placeholders).

## Verification tips (Microsoft CSP)
- Use a branded subdomain `https://support.itsystems.ltd`.
- Ensure the page shows contact email, phone, and hours.
- Keep the form functional (either `mailto:` fallback or webhook).

© 2025 IT Systems Ltd. All rights reserved.
