# Security Policy

## Scope

**PreeclampsiaRisk · WVSUMC** is a client-side web application. It runs entirely
in the browser — there is no server, no API, no database, and no network requests.

Patient data entered into the calculator is:
- Never transmitted to any external server
- Stored only in the browser's `localStorage` on the user's own device
- Cleared when the user explicitly deletes records or clears browser data

This significantly limits the attack surface. However, security reports related
to the following are still taken seriously.

---

## Supported Versions

| Version | Supported |
|---------|-----------|
| 1.3.x   | ✅ Current |
| 1.2.x   | ⚠️ Critical fixes only |
| < 1.2   | ❌ Not supported |

---

## Reporting a Vulnerability

**Do not open a public GitHub Issue for security vulnerabilities.**

If you discover a security issue — including but not limited to XSS vectors,
malicious input handling, localStorage data exposure, or print injection — please
report it privately.

**Contact:** [gdddevelopers.dev@gmail.com](mailto:gdddevelopers.dev@gmail.com)  
**Subject line:** `[SECURITY] PreeclampsiaRisk — <brief description>`

Include in your report:

1. A description of the vulnerability
2. Steps to reproduce
3. Potential impact assessment
4. Suggested remediation (if any)

You will receive an acknowledgment within **72 hours**. If the issue is confirmed,
a patch will be prioritized and credited to you in the `CHANGELOG.md` unless you
prefer to remain anonymous.

---

## Out of Scope

The following are not considered security vulnerabilities for this project:

- Absence of HTTPS when running locally (`file://` or `localhost`)
- `localStorage` data being accessible to the device owner
  *(this is expected browser behavior — data stays local by design)*
- Self-XSS requiring physical access to the user's own browser console
- Issues affecting browsers that are end-of-life or unsupported

---

## Data & Privacy

This application does not collect, transmit, or store any data remotely.
No analytics, no telemetry, no third-party scripts are loaded at runtime.
The only external resource fetched is the **Google Fonts stylesheet** at load time
(`fonts.googleapis.com`), which is subject to Google's own privacy policy.

---

*© 2026 GDD · Owner & Full-Stack Developer · All rights reserved.*
