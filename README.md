# preeclampsiarisk-wvsumc

<div align="center">

<br/>

```
██████╗ ██████╗ ███████╗███████╗ ██████╗██╗      █████╗ ███╗   ███╗██████╗ ███████╗██╗ █████╗ ██████╗ ██╗███████╗██╗  ██╗
██╔══██╗██╔══██╗██╔════╝██╔════╝██╔════╝██║     ██╔══██╗████╗ ████║██╔══██╗██╔════╝██║██╔══██╗██╔══██╗██║██╔════╝██║ ██╔╝
██████╔╝██████╔╝█████╗  █████╗  ██║     ██║     ███████║██╔████╔██║██████╔╝███████╗██║███████║██████╔╝██║███████╗█████╔╝ 
██╔═══╝ ██╔══██╗██╔══╝  ██╔══╝  ██║     ██║     ██╔══██║██║╚██╔╝██║██╔═══╝ ╚════██║██║██╔══██║██╔══██╗██║╚════██║██╔═██╗ 
██║     ██║  ██║███████╗███████╗╚██████╗███████╗██║  ██║██║ ╚═╝ ██║██║     ███████║██║██║  ██║██║  ██║██║███████║██║  ██╗
╚═╝     ╚═╝  ╚═╝╚══════╝╚══════╝ ╚═════╝╚══════╝╚═╝  ╚═╝╚═╝     ╚═╝╚═╝     ╚══════╝╚═╝╚═╝  ╚═╝╚═╝  ╚═╝╚═╝╚══════╝╚═╝  ╚═╝
```

<br/>

**`WVSUMC · College of Medicine · MG4 Research Prototype · 2026`**

<br/>

[![Status](https://img.shields.io/badge/STATUS-PROTOTYPE-ff453a?style=for-the-badge&labelColor=0a0a0a)](.)
[![Institution](https://img.shields.io/badge/WVSUMC-COM%20MG4-5ac8fa?style=for-the-badge&labelColor=0a0a0a)](.)
[![Platform](https://img.shields.io/badge/PLATFORM-WEB%20%2F%20iOS-30d158?style=for-the-badge&labelColor=0a0a0a)](.)
[![License](https://img.shields.io/badge/LICENSE-ALL%20RIGHTS%20RESERVED-ff9f0a?style=for-the-badge&labelColor=0a0a0a)](.)
[![Built By](https://img.shields.io/badge/BUILT%20BY-GDD-ffffff?style=for-the-badge&labelColor=0a0a0a)](.)

<br/>

> *"Clinical risk stratification for late-onset preeclampsia in Filipino pregnant women — built for the ward, designed for precision."*

<br/>

---

</div>

<br/>

## `01` &nbsp; Overview

**PreeclampsiaRisk** is a web-based clinical decision-support tool for **late-onset preeclampsia (PE) risk stratification** in Filipino pregnant women. Built as the digital companion to a retrospective cohort study conducted at West Visayas State University Medical Center (WVSUMC), it operationalizes multivariable logistic regression models into a real-time, mobile-ready risk calculator.

This is not a generic health app. It was engineered from the ground up for the **obstetric ward environment** — fast inputs, immediate output, printable clinical reports, and an interface that performs on both desktop browsers and iOS WebKit.

```
Target Population  →  Filipino pregnant women, ≥ 34 weeks GA
Study Design       →  Retrospective cohort, Jan 2016 – Dec 2025
Outcome Variable   →  New-onset hypertension ≥ 34 weeks (ISSHP 2022)
Validation Method  →  Bootstrap internal validation, 1,000 replications (TRIPOD)
Sample Size Target →  1,160 records (EPP ≥ 9, 90% shrinkage, Riley et al. 2020)
PE Prevalence Est. →  6.4% in WVSUMC analysis
```

<br/>

---

## `02` &nbsp; Features

| Feature | Description |
|---|---|
| **Real-time Risk Gauge** | Animated SVG arc gauge updates live as values are entered — no submit button |
| **Composite Scoring Engine** | 12-parameter weighted scoring with sigmoid logit transform |
| **Clinical Flag System** | Per-parameter interpretation with severity classification (Normal / Borderline / Concerning) |
| **Patient Log** | Persistent local session log; save, load, and delete patient records |
| **Print-to-PDF Report** | Full hospital-grade A4 clinical report: header, meta strip, risk banner, parameter grid, reference table, flags, and disclaimer |
| **iOS WKWebView Compatible** | Native-safe modal system replaces browser `alert/confirm/prompt`; localStorage fallback; input event re-binding for WebKit |
| **Loader + Iris Reveal** | Apple-style splash loader with iris wipe transition using Canvas API |
| **Zero Dependencies** | Pure HTML/CSS/JS — no framework, no bundler, no CDN required |

<br/>

---

## `03` &nbsp; Risk Parameters

The scoring engine incorporates **12 clinical and laboratory predictors**, each with evidence-based weight tiers derived from obstetric literature pending replacement with final study β-coefficients.

```
┌─────────────────────────────┬──────────────────┬──────────────────┬──────────────┐
│ PARAMETER                   │ NORMAL           │ CONCERNING       │ WEIGHT       │
├─────────────────────────────┼──────────────────┼──────────────────┼──────────────┤
│ Mean Arterial Pressure      │ < 90 mmHg        │ ≥ 105 mmHg       │ HIGH   ●●●   │
│ UPCR                        │ < 0.15           │ ≥ 0.30           │ HIGH   ●●●   │
│ Platelet Count              │ 150–400 ×10³/µL  │ < 100 ×10³/µL   │ HIGH   ●●●   │
│ Serum Creatinine            │ 0.5–0.9 mg/dL    │ ≥ 1.1 mg/dL     │ MOD    ●●    │
│ AST / ALT                   │ < 40 U/L         │ ≥ 70 U/L        │ MOD    ●●    │
│ Uric Acid                   │ < 5.5 mg/dL      │ ≥ 6.0 mg/dL     │ MOD    ●●    │
│ BMI (pre-pregnancy)         │ 18.5–24.9 kg/m²  │ ≥ 35 kg/m²      │ LOW    ●     │
│ Gestational Age             │ ≥ 37 weeks       │ < 34 weeks       │ MOD–HI ●●    │
│ Prior PE / HTN / DM / APS   │ Absent           │ Present          │ MOD–HI ●●    │
│ Multiple Pregnancy          │ Singleton        │ Twins / Higher   │ MOD    ●●    │
│ Nulliparity                 │ —                │ First pregnancy  │ LOW    ●     │
│ Maternal Age                │ 20–35 years      │ > 40 years       │ LOW–MOD ●    │
└─────────────────────────────┴──────────────────┴──────────────────┴──────────────┘
```

### Risk Stratification Thresholds

```
  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░
  ▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓  LOW   < 20%   ──── Routine prenatal monitoring
  ▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓  MOD   20–44%  ──── Increased surveillance + aspirin prophylaxis
  ▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓▓  HIGH  ≥ 45%   ──── Urgent clinical review + specialist referral
  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░
```

<br/>

---

## `04` &nbsp; Technical Architecture

```
preeclampsia-risk/
│
├── index.html              ← Entire application (single-file architecture)
│   │
│   ├── <style>             ← ~900 lines of production CSS
│   │   ├── Animated background (orb system, GPU transforms)
│   │   ├── iOS 26-style liquid glass toggle components
│   │   ├── SVG gauge with stroke-dashoffset animation
│   │   ├── Responsive grid (desktop / tablet / mobile)
│   │   └── Full @media print styles for A4 clinical report
│   │
│   └── <script>            ← ~500 lines of vanilla JS
│       ├── Scoring engine  (sAge, sBMI, sMAP, sCr, sPlt, sLiver, sUPCR, sUric...)
│       ├── Logit transform (sigmoid, midpoint=20, k=0.168)
│       ├── Patient log     (localStorage with in-memory fallback)
│       ├── Print system    (dynamic HTML injection → window.print())
│       ├── Modal system    (WKWebView-safe alert/confirm/prompt replacement)
│       └── Iris reveal     (Canvas API wipe animation, rAF loop)
│
└── README.md               ← You are here
```

### Scoring Logic

```js
// Composite raw score
score = sAge(age) + sBMI(bmi) + sMAP(map) + sCr(cr) + sPlt(plt)
      + sLiver(ast, alt) + sUPCR(upcr) + sUric(uric) 
      + sParity(par) + sHx() + sGA(ga) + sMulti();

// Sigmoid transform → probability (0–99%)
pct = clamp(1, 99, round( 1 / (1 + e^(-0.168 × (score - 20))) × 100 ));
```

> ⚠️ Current weights are **literature-derived proxy thresholds**. Final β-coefficients from the WVSUMC retrospective cohort will replace these upon study completion.

<br/>

---

## `05` &nbsp; Clinical Report Output

The print system generates a structured **A4 clinical risk report** containing:

- **Institution header** — WVSUMC · Department of Obstetrics & Gynecology
- **Meta strip** — Patient ID, date, time, requesting clinician
- **Risk banner** — Large percentage display + stratification scale with pip indicator
- **12-parameter grid** — Values, reference ranges, and status pills (Normal / Borderline / Concerning)
- **Clinical history checklist** — 7 binary risk factors with visual indicators
- **Pregnancy-adjusted reference table** — MAP, UPCR, platelets, creatinine, liver enzymes, uric acid, BMI
- **Clinical flags panel** — Auto-generated interpretation flags with severity icons
- **Formal disclaimer** — Prototype limitations, ACOG/ISSHP compliance notice
- **Document footer** — Auto-generated document ID (format: `WVSUMC-PE-YYYYMMDD-HHMM`)

<br/>

---

## `06` &nbsp; Compatibility

| Environment | Status |
|---|---|
| Chrome / Edge (desktop) | ✅ Full support |
| Safari (macOS / iOS) | ✅ Full support, WKWebView-safe |
| Firefox | ✅ Full support |
| iOS Preview (WKWebView) | ✅ Modal system, localStorage fallback, print detection |
| Mobile (Android / iOS) | ✅ Responsive, touch-optimized, `inputmode="decimal"` |
| Print / PDF export | ✅ `@media print` styles, A4 layout |

<br/>

---

## `07` &nbsp; Usage

No build step. No dependencies. No server required.

```bash
# Clone the repository
git clone https://github.com/<your-username>/preeclampsia-risk.git

# Open directly in any browser
open index.html
```

Or serve locally:

```bash
# Python 3
python -m http.server 8080

# Node.js (npx)
npx serve .
```

Navigate to `http://localhost:8080` — the app runs entirely client-side.

<br/>

---

## `08` &nbsp; Research Context

```
Study Title   :  Risk Stratification Model for Predicting Late-Onset Preeclampsia
                 Using Clinical and Laboratory Data from Filipino Pregnant Women
                 Admitted to WVSUMC

Institution   :  West Visayas State University Medical Center
                 College of Medicine — Medical Group 4

Timeline      :  Data Collection: January 2016 – December 2025
                 Thesis Presentation: February 2026

Methodology   :  Retrospective Cohort Design
                 Multivariable Logistic Regression
                 Bootstrap Internal Validation (TRIPOD, B=1,000)
                 Heuristic Development Set (EPP ≥ 9, Riley et al. 2020)

Guidelines    :  ACOG Practice Bulletin 2020
                 ISSHP Classification 2022
```

### References

- ACOG Practice Bulletin No. 222 · *Gestational Hypertension and Preeclampsia* · 2020
- Magee LA et al. · ISSHP Classification, Diagnosis & Management · *Pregnancy Hypertens* · 2022
- Jiménez-García et al. · Preeclampsia Prediction Models · *J Clin Med* · 2025
- Jhee JH et al. · Prediction of Preeclampsia Using Machine Learning · *PLoS ONE* · 2019
- Zhang et al. · Biochemical Markers in PE Risk · *Biomedicines* · 2025
- Zhu et al. · BMJ Open · 2021
- Cua-Lam & Ong · *Philippine Journal of Obstetrics & Gynecology* · 2025
- Riley RD et al. · Sample Size Guidance for Prediction Models · *BMJ* · 2020

<br/>

---

## `09` &nbsp; Disclaimer

> **This application is a clinical decision-support prototype and must not be used as the sole basis for clinical management decisions.**
>
> All outputs must be interpreted in the context of complete clinical history, physical examination, and physician judgment. Current scoring weights are literature-derived proxies — final β-coefficients are pending study completion. This tool has not been formally validated for individual clinical use.
>
> Adherence to ACOG 2020 and ISSHP 2022 guidelines is recommended for all clinical decisions.

<br/>

---

## `10` &nbsp; License & Ownership

```
Copyright © 2026 GDD. All rights reserved.

Unauthorized reproduction, redistribution, or commercial use of this
software, in whole or in part, is strictly prohibited without prior
written permission from the owner.
```

**Owner & Full-Stack Developer:** GDD  
**Contact:** [gdddevelopers.dev@gmail.com](mailto:gdddevelopers.dev@gmail.com)

<br/>

---

<div align="center">

<br/>

```
╔══════════════════════════════════════════════════════════╗
║  PreeclampsiaRisk · WVSUMC Late-Onset PE Calculator      ║
║  © 2026 GDD · Owner & Full-Stack Developer               ║
║  WVSUMC College of Medicine · MG4 Research · 2026        ║
╚══════════════════════════════════════════════════════════╝
```

*Built with precision. Designed for the ward.*

<br/>

</div>
