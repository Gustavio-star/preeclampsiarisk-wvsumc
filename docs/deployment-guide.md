# Deployment Guide

**PreeclampsiaRisk · WVSUMC — Deployment Reference**  
*Last updated: March 2026 · Version 1.3.0*

---

## Overview

PreeclampsiaRisk is a **zero-dependency, single-file web application**. The entire
application — HTML structure, CSS styles, JavaScript logic, and print templates —
is contained within a single `index.html` file.

This means deployment is unusually straightforward: any method that serves a static
HTML file will work.

---

## Option 1 — GitHub Pages (Recommended for Demo / Review)

GitHub Pages serves static files directly from your repository at no cost.

### Setup

1. Go to your repository on GitHub
2. Navigate to **Settings → Pages**
3. Under **Source**, select **Deploy from a branch**
4. Set branch to `main` (or `master`) and folder to `/ (root)`
5. Click **Save**

Your app will be live at:
```
https://<your-username>.github.io/<repository-name>/
```

Deployments trigger automatically on every push to the selected branch.
Allow 1–3 minutes for the first deployment to propagate.

### Custom Domain (Optional)

To use a custom domain (e.g. `pe-risk.wvsumc.edu.ph`):

1. Add a `CNAME` file to the repository root containing your domain:
   ```
   pe-risk.wvsumc.edu.ph
   ```
2. Configure your DNS provider to point to `<your-username>.github.io`
3. Enable **Enforce HTTPS** in the Pages settings

---

## Option 2 — Local File (Air-Gapped / Ward Use)

The application runs fully offline when opened as a local file.

```bash
# Clone or download the repository
git clone https://github.com/<your-username>/preeclampsia-risk.git

# Open directly — no server required
open index.html          # macOS
start index.html         # Windows
xdg-open index.html      # Linux
```

**Offline Limitation:** Google Fonts (`fonts.googleapis.com`) will not load without
internet access. The application falls back to the system sans-serif font stack —
all functionality is preserved, only the Outfit typeface is affected.

To eliminate this dependency entirely, download Outfit from Google Fonts and
replace the `<link>` stylesheet with a local `@font-face` declaration.

---

## Option 3 — Static File Server (LAN / Intranet)

For deployment on a hospital intranet, shared server, or local area network:

### Python (no install required on macOS/Linux)

```bash
cd preeclampsia-risk/
python -m http.server 8080
```

Access from any device on the network:
```
http://<server-ip>:8080
```

### Node.js

```bash
npx serve . --port 8080
```

### Nginx (production intranet server)

```nginx
server {
    listen 80;
    server_name pe-risk.wvsumc.local;

    root /var/www/preeclampsia-risk;
    index index.html;

    # Security headers
    add_header X-Frame-Options "SAMEORIGIN";
    add_header X-Content-Type-Options "nosniff";
    add_header X-XSS-Protection "1; mode=block";
    add_header Referrer-Policy "strict-origin-when-cross-origin";

    # Cache static assets
    location / {
        try_files $uri $uri/ /index.html;
        expires 1h;
        add_header Cache-Control "public, must-revalidate";
    }
}
```

---

## Option 4 — iOS Home Screen App (Recommended for Ward Use)

The application is optimized for iOS via `<meta name="apple-mobile-web-app-capable">`
and behaves as a standalone app when added to the Home Screen.

### Installation on iPhone / iPad

1. Open Safari and navigate to the deployment URL (or open the file via Files app)
2. Tap the **Share** button (box with arrow)
3. Scroll down and tap **"Add to Home Screen"**
4. Name it `PreeclampsiaRisk` and tap **Add**

The app will launch full-screen without the Safari toolbar, indistinguishable
from a native app.

**Note:** `window.print()` is blocked in iOS Preview (`.qlpreview`) and
standalone WebApp mode. For print/PDF export from iOS, open in **Safari** then
use **Share → Print**.

---

## Option 5 — Docker Container

For containerized hospital infrastructure:

```dockerfile
FROM nginx:alpine

COPY index.html /usr/share/nginx/html/index.html

# Security headers
RUN echo 'server { \
    listen 80; \
    location / { \
        root /usr/share/nginx/html; \
        add_header X-Frame-Options SAMEORIGIN; \
        add_header X-Content-Type-Options nosniff; \
    } \
}' > /etc/nginx/conf.d/default.conf

EXPOSE 80
```

```bash
# Build and run
docker build -t preeclampsia-risk .
docker run -d -p 8080:80 --name pe-risk preeclampsia-risk
```

---

## Environment Notes

### Data Storage

Patient records are saved to the browser's `localStorage` under the key
`pe_log_v6`. This data is:

- **Local only** — never transmitted anywhere
- **Device-specific** — records saved on one device are not accessible on another
- **Session-persistent** — records survive browser/tab closure
- **Clearable** — users can delete individual records or use "Clear All"

If `localStorage` is unavailable (e.g., private browsing, WKWebView sandbox),
an in-memory fallback (`_memStore`) is used automatically. Records saved in
this mode are lost when the app is closed.

### Browser Support

| Browser | Minimum Version | Notes |
|---------|----------------|-------|
| Chrome | 90+ | Full support |
| Safari | 14+ | Full support; WKWebView-safe |
| Firefox | 88+ | Full support |
| Edge | 90+ | Full support |
| iOS Safari | 14+ | Recommended for iOS deployment |
| Samsung Internet | 14+ | Full support |

---

## Updating the Application

To update to a new version:

```bash
# Pull latest changes
git pull origin main

# If serving locally — refresh browser
# If deployed to GitHub Pages — push triggers auto-deploy
# If using a server — copy the updated index.html to the server root
```

No build step, no dependency installation, no cache invalidation beyond
a standard browser refresh (`Cmd/Ctrl + Shift + R`).

---

## Troubleshooting

| Issue | Cause | Fix |
|-------|-------|-----|
| Fonts not loading | No internet access | Expected offline behavior; functionality unaffected |
| Print dialog not appearing (iOS) | WKWebView blocks `window.print()` | Open in Safari, use Share → Print |
| Patient records lost after update | `localStorage` key mismatch | Records stored under `pe_log_v6` — check browser storage |
| Calculator not updating on input | WebKit input event issue | Ensure JS is enabled; hard-refresh the page |
| Blank white screen | JS error on load | Open browser console (F12) and check for errors |

---

*© 2026 GDD · Owner & Full-Stack Developer · All rights reserved.*  
*PreeclampsiaRisk · WVSUMC Late-Onset PE Calculator*
