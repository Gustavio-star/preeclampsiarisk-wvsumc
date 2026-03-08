# Frequently Asked Questions

**PreeclampsiaRisk · WVSUMC — FAQ**  
*Last updated: March 2026 · Version 1.3.0*

---

## General

---

**Q: What is this calculator?**

PreeclampsiaRisk is a clinical decision-support prototype for risk stratification
of late-onset preeclampsia (PE onset ≥ 34 weeks) in Filipino pregnant women.
It was built as the digital companion to a retrospective cohort study at West
Visayas State University Medical Center (WVSUMC), College of Medicine, MG4.

---

**Q: Can I use this to diagnose preeclampsia?**

No. This tool does not diagnose preeclampsia. It produces a **risk probability
estimate** based on clinical and laboratory inputs — it is a decision-support
aid, not a diagnostic instrument.

Preeclampsia diagnosis requires clinical assessment, serial blood pressure
measurements, laboratory interpretation, and physician judgment in accordance
with ACOG 2020 and ISSHP 2022 criteria.

---

**Q: Are the risk scores clinically validated?**

The current version uses **literature-derived proxy weights** based on published
evidence (ACOG 2020, ISSHP 2022, Jiménez-García et al. 2025, Jhee et al. 2019,
and others). These are intentional placeholders.

Final β-coefficients from the WVSUMC retrospective cohort study (multivariable
logistic regression with bootstrap internal validation, B=1,000, TRIPOD) will
replace the proxy weights upon study completion. Until then, the numerical output
should be interpreted with appropriate caution.

---

**Q: What does the percentage score represent?**

The percentage is a **composite risk probability estimate** — it represents the
tool's assessment of the likelihood that the entered clinical profile is
consistent with a high-risk late-onset PE presentation.

It is produced by passing a weighted raw score through a sigmoid (logistic)
function. It is not a direct population-derived probability from validated
outcome data at this stage.

See [`docs/scoring-methodology.md`](./scoring-methodology.md) for the full
mathematical derivation.

---

**Q: Why does the score change even when I only change one value?**

The scoring system is additive and continuous — every parameter contributes
independently. Changing MAP by 5 mmHg, for example, can shift the raw score
by up to 7 points, which in the steep region of the sigmoid curve can noticeably
change the output percentage.

This sensitivity is intentional: it reflects the clinical reality that small
changes in key parameters (especially MAP, UPCR, and platelets) can have
significant prognostic implications.

---

## Clinical Parameters

---

**Q: What MAP value should I enter?**

Mean Arterial Pressure is calculated as:

```
MAP = (SBP + 2 × DBP) / 3
```

Use the most recent blood pressure reading. If multiple readings are available,
use the higher value as a conservative estimate. Do not average multiple
readings if there is significant variation — the highest reading is more
clinically relevant for PE risk.

---

**Q: The UPCR field — which sample should I use?**

Use the **spot urine protein-to-creatinine ratio** from a random midstream
sample. UPCR ≥ 0.3 is equivalent to ≥ 300 mg/24-hour urine protein and is
the accepted screening threshold.

If a 24-hour urine is available, UPCR may be approximated as:
`UPCR ≈ 24-hr protein (mg) / 1000`

---

**Q: What if I don't have a uric acid result?**

Uric acid is marked as optional. Leave the field blank — it will contribute
zero points to the score. The calculator functions with any combination of
available values; missing fields do not block calculation.

---

**Q: Which BMI should I enter — current or pre-pregnancy?**

Enter **pre-pregnancy BMI** or first-trimester BMI if available. Current
third-trimester weight is heavily confounded by fluid retention, edema, and
fetal weight, and is not appropriate for this field.

If pre-pregnancy weight is unknown, use the earliest documented weight from
the antenatal record.

---

**Q: Should I toggle "Nulliparous" AND enter Parity = 0?**

Both inputs capture nulliparity through different mechanisms. The parity
number field (`sParity`) and the nulliparous toggle (`sHx`) both add points.
If the patient is truly nulliparous (first pregnancy), enabling both is
appropriate — this reflects the clinical significance of first pregnancy as
a risk factor through two evidence streams.

---

## Technical

---

**Q: Does the app send any data to a server?**

No. The application runs entirely client-side. No patient data is ever
transmitted to any server, API, or analytics service. The only network request
at runtime is the Google Fonts stylesheet for the Outfit typeface.

Patient records saved via the "Save" button are stored in the browser's
`localStorage` on the user's own device.

---

**Q: Does it work offline?**

Yes, with one minor exception. All calculation, display, and print functionality
works offline. The only feature that requires internet is loading the Outfit
font from Google Fonts — if offline, the app falls back to the system font.

For fully offline deployment (e.g., hospital intranet without internet access),
see the font self-hosting instructions in
[`docs/deployment-guide.md`](./deployment-guide.md).

---

**Q: Why does printing not work on iOS?**

`window.print()` is intentionally blocked by Apple in several iOS contexts:

- **iOS Preview / QuickLook** (`.qlpreview`) — no print support
- **WKWebView standalone mode** — restricted print API
- **Added to Home Screen (WebApp mode)** — blocked in some iOS versions

**Workaround:** Open the application in **Safari** (not Preview), then use
**Share → Print**. The app detects when `window.print()` fails and shows a
modal with these instructions automatically.

---

**Q: Patient records disappeared after I cleared my browser data.**

Patient records are stored in `localStorage`, which is cleared when you:

- Use "Clear browsing data" / "Clear history" in your browser
- Use Private / Incognito mode (records are session-only)
- Clear site data specifically for the app's domain

This is expected browser behavior. For persistent record-keeping in a clinical
setting, use the **Print** function to generate a permanent PDF for each patient
and store it in the hospital's document management system.

---

**Q: Can the app be installed on multiple devices and share patient records?**

Not in the current version. `localStorage` is device and browser-specific.
Records saved on one device are not accessible on another. This is a deliberate
design choice at the prototype stage — no backend infrastructure means no data
transmission and no privacy exposure.

---

## Research & Licensing

---

**Q: Can I use this calculator in my own research or hospital?**

Not without written permission. This is proprietary software under a restrictive
license. Unauthorized reproduction, redistribution, or clinical deployment is
prohibited.

Contact [gdddevelopers.dev@gmail.com](mailto:gdddevelopers.dev@gmail.com) for
licensing and permission inquiries.

---

**Q: Can I fork the repository?**

GitHub's fork functionality is technically available, but forking does not grant
any license rights. Forked copies remain subject to the same restrictive license.
See [`LICENSE`](../LICENSE) for the full terms.

---

**Q: When will the final validated model be released?**

The WVSUMC retrospective cohort study (January 2016 – December 2025) is targeting
completion in 2026. Upon finalization of β-coefficients from the multivariable
logistic regression model, this calculator will be updated with validated weights.

The validated version will include updated documentation, a formal performance
metrics report (AUC, sensitivity, specificity, calibration), and a revised
clinical disclaimer.

---

*© 2026 GDD · Owner & Full-Stack Developer · All rights reserved.*  
*PreeclampsiaRisk · WVSUMC Late-Onset PE Calculator*
