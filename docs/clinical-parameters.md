# Clinical Parameters Reference

**PreeclampsiaRisk · WVSUMC — Clinical Reference Document**  
*Last updated: March 2026 · Version 1.3.0*

---

## Purpose

This document provides pregnancy-adjusted normal reference ranges, clinical
significance thresholds, and literature citations for each parameter used in
the PreeclampsiaRisk calculator.

All reference ranges reflect **third-trimester or late-pregnancy norms** where
applicable. Standard (non-pregnant) laboratory reference ranges should not be
applied to this tool.

---

## Parameters

---

### Mean Arterial Pressure (MAP)

**Formula:** `MAP = (SBP + 2 × DBP) / 3`

| Classification | MAP Value | Interpretation |
|---|---|---|
| Normal | < 90 mmHg | No hypertensive concern |
| Borderline | 90–104 mmHg | Elevated — monitor closely |
| Concerning | ≥ 105 mmHg | Severe-range — urgent review |

**Clinical Significance**  
New-onset hypertension (BP ≥ 140/90 mmHg on two occasions ≥ 4 hours apart)
at or after 34 weeks gestation is the defining diagnostic criterion for
late-onset preeclampsia. MAP consolidates systolic and diastolic readings
into a single pressure load metric.

Severe-range hypertension is defined as SBP ≥ 160 or DBP ≥ 110 mmHg, corresponding
to MAP ≥ approximately 127 mmHg — a clinical emergency requiring acute management.

**References:** ACOG 2020; ISSHP 2022; Magee et al. *Hypertension* 2014

---

### UPCR (Urine Protein-to-Creatinine Ratio)

| Classification | UPCR | Interpretation |
|---|---|---|
| Normal | < 0.15 | Physiological range |
| Borderline | 0.15–0.29 | Borderline proteinuria |
| Significant | ≥ 0.30 | PE-threshold proteinuria |
| Severe | ≥ 0.50 | Moderate-to-severe proteinuria |
| Nephrotic range | ≥ 1.0 | Severe proteinuria |

**Clinical Significance**  
UPCR ≥ 0.3 is equivalent to ≥ 300 mg protein per 24-hour urine collection —
the accepted threshold for significant proteinuria in preeclampsia diagnosis.
UPCR offers the practical advantage of being measurable on a spot urine sample.

Proteinuria is no longer required for PE diagnosis under ISSHP 2022 criteria
when other severe features are present, but remains an important risk marker.

**References:** ACOG 2020; Papanna et al. *Obstet Gynecol* 2008; ISSHP 2022

---

### Platelet Count

| Classification | Value (×10³/µL) | Interpretation |
|---|---|---|
| Normal | 150–400 | Normal range in pregnancy |
| Low | 100–149 | Monitor; repeat in 48 hours |
| Moderate thrombocytopenia | 75–99 | Severe feature threshold breached |
| Severe thrombocytopenia | < 75 | HELLP / DIC concern |

**Clinical Significance**  
Thrombocytopenia (platelets < 100 × 10³/µL) is a severe feature of preeclampsia
per ACOG 2020. It may also signal HELLP syndrome (Hemolysis, Elevated Liver
enzymes, Low Platelets) — a life-threatening PE complication.

Mild thrombocytopenia is common in normal pregnancy (gestational thrombocytopenia),
making the trend and rate of decline clinically more informative than a single value.

**References:** ACOG Practice Bulletin 222; Sibai BM *Clin Obstet Gynecol* 1990

---

### Serum Creatinine

| Classification | Value (mg/dL) | Interpretation |
|---|---|---|
| Normal | 0.5–0.9 | Expected range in pregnancy |
| Upper normal | 0.9–1.09 | Watch trend |
| Borderline | 1.0–1.09 | Borderline renal concern |
| Elevated | ≥ 1.1 | Severe feature — renal impairment |
| Significant | ≥ 1.5 | Moderate-to-severe AKI concern |

**Clinical Significance**  
Serum creatinine values in normal pregnancy are lower than in non-pregnant adults
due to increased GFR (by ~50%) and expanded plasma volume. Values that appear
"normal" for non-pregnant adults (e.g., 1.0–1.2 mg/dL) may already represent
relative renal impairment in a pregnant woman.

Creatinine ≥ 1.1 mg/dL (with no prior renal disease) is a severe feature
criterion per ACOG 2020. Doubling of creatinine from a prior value is also
clinically significant.

**References:** ACOG 2020; Helewa ME *J Obstet Gynaecol Can* 2008

---

### AST (Aspartate Aminotransferase)

| Classification | Value (U/L) | Interpretation |
|---|---|---|
| Normal | < 40 | Within pregnancy norms |
| Elevated | 40–69 | Borderline hepatic concern |
| Significantly elevated | 70–119 | Liver involvement |
| Severe | ≥ 120 | HELLP range |

**Pregnancy Reference Range:** 10–30 U/L (slightly lower than non-pregnant)

**Clinical Significance**  
AST elevation indicates hepatocellular injury. In the context of preeclampsia,
AST ≥ 2× upper limit of normal (typically ≥ 70–80 U/L) is a severe feature
and may indicate early HELLP syndrome. AST is typically more elevated than ALT
in PE-related hepatic involvement.

**References:** ACOG 2020; Knox TA *Hepatology* 1991

---

### ALT (Alanine Aminotransferase)

| Classification | Value (U/L) | Interpretation |
|---|---|---|
| Normal | < 35 | Within pregnancy norms |
| Elevated | 35–69 | Borderline hepatic concern |
| Significantly elevated | 70–119 | Hepatic involvement |
| Severe | ≥ 120 | HELLP range |

**Pregnancy Reference Range:** 7–35 U/L

**Clinical Significance**  
ALT is more liver-specific than AST. Combined elevation of AST and ALT with
thrombocytopenia and hemolysis constitutes the HELLP syndrome triad. The
calculator uses `max(AST, ALT)` to ensure the more abnormal value drives scoring.

**References:** ACOG 2020; Sibai BM *Am J Obstet Gynecol* 2004

---

### Uric Acid

| Classification | Value (mg/dL) | Interpretation |
|---|---|---|
| Normal | 2.4–5.4 | Normal in pregnancy |
| Borderline | 5.5–5.9 | Mildly elevated |
| Elevated | 6.0–6.9 | Associated with PE severity |
| High | ≥ 7.0 | Hyperuricemia — significant concern |

**Clinical Significance**  
Hyperuricemia in pregnancy correlates with reduced renal urate clearance due to
placental-mediated uric acid overproduction and decreased renal blood flow.
Multiple studies have associated elevated uric acid with preeclampsia severity,
adverse fetal outcomes (SGA, preterm birth), and progression to HELLP.

While not a diagnostic criterion, uric acid is a useful ancillary marker for
risk monitoring and is included as a moderate-weight predictor.

**References:** Cua-Lam & Ong *PJOG* 2025; Zheng et al. *Hypertens Pregnancy* 2020;
Thangaratinam et al. *BJOG* 2006

---

### BMI (Body Mass Index)

**Formula:** `BMI = weight (kg) / height² (m²)`  
*Use pre-pregnancy or first-trimester BMI only*

| Classification | BMI (kg/m²) | Interpretation |
|---|---|---|
| Underweight | < 18.5 | Not scored |
| Normal | 18.5–24.9 | Reference — 0 points |
| Overweight | 25.0–29.9 | Mildly elevated risk |
| Obese Class I | 30.0–34.9 | Elevated risk |
| Obese Class II+ | ≥ 35.0 | Significantly elevated risk |

**Clinical Significance**  
Obesity is a modifiable risk factor for preeclampsia with a dose-response
relationship. Meta-analyses show OR ~2.5 for BMI ≥ 30 and OR ~3.3 for BMI ≥ 35.
The mechanism involves adipokine dysregulation, insulin resistance, chronic
low-grade inflammation, and endothelial dysfunction — all overlapping pathways
with PE pathophysiology.

**References:** Bodnar LM et al. *Epidemiology* 2005;
Duckitt & Harrington *BMJ* 2005; ACOG 2020

---

### Gestational Age (GA)

*Gestational age at time of assessment, in completed weeks*

| GA | Interpretation |
|---|---|
| < 28 weeks | Very preterm — high concern if symptoms present |
| 28–31 weeks | Preterm |
| 32–33 weeks | Late preterm / early late-preterm |
| 34–36 weeks | **Target late-onset PE window** |
| ≥ 37 weeks | Term — lower late-onset PE risk per se |

**Clinical Significance**  
Late-onset preeclampsia is defined as PE onset at or after **34 completed weeks**
of gestation (ISSHP 2022). The scoring penalizes lower GA at assessment because
symptoms presenting earlier in pregnancy, if already present, indicate a more
severe clinical trajectory.

**References:** ISSHP 2022 (Magee et al.); Brown et al. *Pregnancy Hypertens* 2018

---

### Clinical History Flags

| Flag | Weight | Evidence Basis |
|---|---|---|
| Previous preeclampsia | Highest (13 pts) | RR 7.2 (95% CI 5.8–9.1); ACOG 2020 |
| Chronic hypertension | High (9 pts) | RR 5.1; Duckitt & Harrington *BMJ* 2005 |
| Antiphospholipid / SLE | High (8 pts) | RR 9.7 for APS; ACOG 2020 |
| Pre-gestational DM | Moderate (5 pts) | RR ~3.5; Garovic et al. 2022 |
| Family history of PE | Moderate (4 pts) | RR 2.9; Cnossen et al. *BJOG* 2006 |
| Nulliparous | Low (3 pts) | RR 2.9 vs multiparous; Duckitt 2005 |
| Multiple pregnancy | Moderate-High (7 pts) | RR 2.9–3.7; twin vs singleton |

**Notes on Prior PE:**  
A history of preeclampsia in a prior pregnancy is the strongest clinical predictor
of recurrence. Risk varies by severity (severe PE → higher recurrence), gestational
age of prior onset (earlier → higher recurrence), and interpregnancy interval.

---

## Diagnostic Criteria for Reference

### Preeclampsia (ISSHP 2022)

New-onset hypertension (≥ 140/90 mmHg on two readings) at ≥ 20 weeks GA **plus**
one or more of:

- Proteinuria (UPCR ≥ 0.3 or ≥ 300 mg/24h or dipstick ≥ 2+)
- Maternal organ dysfunction (renal, hepatic, neurological, hematological)
- Uteroplacental dysfunction (FGR, abnormal Doppler)

### Severe Features (ACOG 2020) — any one of:

- SBP ≥ 160 or DBP ≥ 110 mmHg (on two readings ≥ 4h apart)
- Thrombocytopenia (platelets < 100 × 10³/µL)
- Renal insufficiency (creatinine > 1.1 mg/dL or doubling)
- Liver enzyme elevation (≥ 2× ULN) ± severe right upper quadrant pain
- New-onset severe headache / visual disturbances
- Pulmonary edema

---

*© 2026 GDD · Owner & Full-Stack Developer · All rights reserved.*  
*PreeclampsiaRisk · WVSUMC Late-Onset PE Calculator*
