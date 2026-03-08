# Changelog

All notable changes to **PreeclampsiaRisk · WVSUMC** are documented in this file.

Format follows [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).  
Versioning follows [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

---

## [1.3.0] — 2026-03-01

### Added
- Full A4 clinical print report with dynamic document ID (`WVSUMC-PE-YYYYMMDD-HHMM`)
- Requesting clinician name prompt before print (WKWebView-safe modal)
- Pregnancy-adjusted normal reference table in print output
- Per-parameter status pills in print grid (Normal / Borderline / Concerning)
- Risk scale bar with pip position indicator in print banner

### Changed
- Print system rewritten: HTML injected into `#printChart` div instead of new window
- iOS `afterprint` event detection with fallback alert for Preview.app environments

### Fixed
- `window.print()` silently failing in iOS WKWebView — added 400ms detection timeout
- Print banner color classes (`mod`, `hi`) not applying correctly on first render

---

## [1.2.0] — 2026-02-15

### Added
- Patient log with persistent `localStorage` storage (`pe_log_v6`)
- In-memory `_memStore` fallback when `localStorage` is blocked (WKWebView sandbox)
- Save, load, and delete individual patient records
- Clear All log function with confirmation modal
- Log items restore full form state including all toggles

### Changed
- Patient name field repositioned into dedicated patient bar above form
- Save / New / Print actions consolidated into patient bar row
- Log section auto-shows/hides based on saved record count

---

## [1.1.0] — 2026-02-01

### Added
- Custom modal system replacing native `alert()` / `confirm()` / `prompt()`
  — fully compatible with WKWebView sandbox restrictions
- iOS input event re-binding (`input`, `change`, `keyup`, `blur`) for WebKit reliability
- Iris wipe transition using Canvas API (`requestAnimationFrame` loop)
- Apple-style splash loader with animated rings, floating icon, and dot indicators

### Changed
- Gauge glow now applied via SVG parent `filter` property (iOS-safe; avoids `drop-shadow` on `<circle>`)
- All `backdrop-filter` removed from animated background layer to prevent iOS scroll stutter
- Toggle knob spring animation upgraded to `cubic-bezier(.34, 1.5, .64, 1)`

### Fixed
- SVG `stroke-dashoffset` not animating on first render in Safari
- Toggle `.on` state not persisting after `loadEntry()` restores a saved patient

---

## [1.0.0] — 2026-01-15

### Added
- Initial release of PreeclampsiaRisk · WVSUMC Late-Onset PE Calculator
- 12-parameter composite scoring engine with sigmoid logit transform
- Live SVG arc gauge with color-coded risk stratification (Low / Moderate / High)
- Seven clinical history toggles (iOS 26-style liquid glass switch components)
- Per-parameter clinical flag system with severity classification
- Clinical advice text block linked to risk level
- Fully responsive layout: desktop two-column grid, tablet/mobile stacked
- `@media print` CSS for basic print support
- Animated background orb system (GPU-only transforms)
- Single-file architecture — zero dependencies, zero build step

### Research Context
- Study: *Risk Stratification Model for Predicting Late-Onset Preeclampsia Using
  Clinical and Laboratory Data from Filipino Pregnant Women Admitted to WVSUMC*
- Institution: WVSUMC College of Medicine — Medical Group 4
- Data window: January 2016 – December 2025
- Scoring weights: Literature-derived proxies (ACOG 2020, ISSHP 2022)
- Final β-coefficients pending study completion

---

## Legend

| Symbol | Meaning |
|--------|---------|
| `Added` | New features or files introduced |
| `Changed` | Changes to existing functionality |
| `Fixed` | Bug fixes |
| `Removed` | Features or files removed |
| `Security` | Vulnerability patches |

---

*© 2026 GDD · Owner & Full-Stack Developer · All rights reserved.*
