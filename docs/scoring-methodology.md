# Scoring Methodology

**PreeclampsiaRisk · WVSUMC — Technical Reference**  
*Last updated: March 2026 · Version 1.3.0*

---

## Overview

The risk calculator uses a **composite additive scoring system** transformed
through a **sigmoid (logistic) function** to produce a probability estimate
between 1% and 99%.

This architecture reflects the statistical foundation of multivariable logistic
regression — the modeling strategy used in the underlying WVSUMC retrospective
cohort study — while using literature-derived proxy weights in lieu of final
study β-coefficients.

---

## Step 1: Raw Score Construction

Each input parameter is mapped to a discrete point value via piecewise threshold
functions. The raw score is the sum of all active parameter contributions:

```
score = sAge(age)
      + sBMI(bmi)
      + sMAP(map)
      + sCr(creatinine)
      + sPlt(platelets)
      + sLiver(ast, alt)
      + sUPCR(upcr)
      + sUric(uric_acid)
      + sParity(parity)
      + sHx()           ← clinical history flags
      + sGA(gestational_age)
      + sMulti()        ← multiple pregnancy flag
```

Missing values contribute **zero points** — the calculator degrades gracefully
with incomplete data rather than refusing to compute.

---

## Step 2: Parameter Scoring Functions

### Mean Arterial Pressure — `sMAP(x)`

```
MAP < 85       →  0 pts   (normal)
85 ≤ MAP < 90  →  4 pts   (borderline)
90 ≤ MAP < 95  →  8 pts   (stage 1)
95 ≤ MAP < 100 →  11 pts  (stage 2)
100 ≤ MAP < 105 → 14 pts  (severe range)
MAP ≥ 105      →  18 pts  (critical)
```

MAP is the **highest-weighted continuous parameter**, reflecting its centrality
to preeclampsia diagnosis (new-onset hypertension is a defining criterion).
Formula: `MAP = (SBP + 2 × DBP) / 3`

---

### UPCR — `sUPCR(x)`

```
UPCR < 0.15    →  0 pts   (normal)
0.15 ≤ x < 0.3 →  4 pts   (borderline proteinuria)
0.3 ≤ x < 0.5  →  8 pts   (significant — PE threshold)
0.5 ≤ x < 1.0  →  12 pts  (moderate proteinuria)
UPCR ≥ 1.0     →  17 pts  (severe proteinuria)
```

UPCR ≥ 0.3 is the accepted threshold for significant proteinuria per ACOG 2020
and ISSHP 2022. Scores escalate steeply above this cutoff.

---

### Platelet Count — `sPlt(x)`

```
PLT ≥ 150      →  0 pts   (normal)
100 ≤ x < 150  →  5 pts   (low — monitor)
75 ≤ x < 100   →  9 pts   (moderate thrombocytopenia)
PLT < 75       →  14 pts  (severe thrombocytopenia)
```

Thrombocytopenia is a hallmark of HELLP syndrome, a severe PE complication.
Platelet count below 100 is a diagnostic criterion for severe features.

---

### Serum Creatinine — `sCr(x)`

```
Cr < 0.8       →  0 pts   (normal)
0.8 ≤ x < 1.0  →  3 pts   (upper normal)
1.0 ≤ x < 1.1  →  5 pts   (borderline — PE threshold area)
1.1 ≤ x < 1.5  →  8 pts   (renal concern)
Cr ≥ 1.5       →  11 pts  (renal impairment)
```

Creatinine ≥ 1.1 mg/dL (in the absence of other renal disease) is a severe
feature criterion per ACOG 2020.

---

### Liver Enzymes — `sLiver(ast, alt)`

```
max(AST, ALT) < 40   →  0 pts   (normal)
40 ≤ max < 70        →  4 pts   (elevated)
70 ≤ max < 120       →  8 pts   (significantly elevated)
max ≥ 120            →  11 pts  (hepatic concern / HELLP range)
```

The function takes `max(AST, ALT)` — whichever is more abnormal drives the score.
AST ≥ 2× ULN is a severe feature criterion.

---

### Uric Acid — `sUric(x)`

```
Uric < 5.5     →  0 pts   (normal)
5.5 ≤ x < 6.0  →  3 pts   (borderline)
6.0 ≤ x < 7.0  →  5 pts   (elevated)
Uric ≥ 7.0     →  8 pts   (hyperuricemia)
```

Hyperuricemia has been reported as an independent predictor of PE severity and
adverse outcomes (Zheng et al. 2020; Cua-Lam & Ong 2025).

---

### BMI — `sBMI(x)`

```
BMI < 25       →  0 pts   (normal / underweight)
25 ≤ x < 30    →  2 pts   (overweight)
30 ≤ x < 35    →  5 pts   (obese class I)
BMI ≥ 35       →  9 pts   (obese class II+)
```

Pre-pregnancy or first-trimester BMI. Obesity is a recognized modifiable risk
factor for PE (OR ~2.5 for BMI ≥ 30; Bodnar et al.).

---

### Maternal Age — `sAge(x)`

```
Age < 20       →  5 pts   (adolescent pregnancy)
20 ≤ x ≤ 35   →  0 pts   (normal reproductive window)
35 < x ≤ 40   →  4 pts   (advanced maternal age)
Age > 40       →  7 pts   (very advanced maternal age)
```

Both extremes carry elevated risk via distinct pathophysiological mechanisms.

---

### Gestational Age — `sGA(x)`

```
GA < 28 wks    →  10 pts  (very preterm — high surveillance)
28 ≤ x < 32   →  7 pts   (preterm)
32 ≤ x < 34   →  5 pts   (late preterm)
34 ≤ x < 37   →  3 pts   (target late-onset PE window)
GA ≥ 37 wks   →  0 pts   (term)
```

Late-onset PE is defined as onset ≥ 34 weeks (ISSHP 2022). Earlier GA at
assessment, particularly if symptoms are already present, indicates higher concern.

---

### Parity — `sParity(x)`

```
Parity = 0     →  3 pts   (nulliparous)
Parity ≥ 1     →  0 pts
```

Nulliparity is a well-established PE risk factor; first-time pregnancies lack
the immunological tolerance thought to develop after first delivery.

---

### Clinical History — `sHx()`

```
Previous preeclampsia   →  +13 pts   (strongest single risk factor)
Chronic hypertension    →  +9 pts
Antiphospholipid / SLE  →  +8 pts
Pre-gestational DM      →  +5 pts
Family history of PE    →  +4 pts
Nulliparous (toggle)    →  +3 pts
```

These are additive — a patient with prior PE + chronic HTN accumulates 22 pts
from history alone before any lab values are considered.

---

### Multiple Pregnancy — `sMulti()`

```
Multiple pregnancy present  →  +7 pts
Singleton                   →  0 pts
```

Twins and higher-order pregnancies carry approximately 2–3× the PE risk of
singleton pregnancies due to increased placental mass and angiogenic factor load.

---

## Step 3: Logit Transform

The raw score is passed through a sigmoid function to produce a probability:

```
pct = clamp(1, 99,  round( 100 / (1 + e^(-k × (score - midpoint))) ))

where:
  midpoint = 20    (score at which output = 50%)
  k        = 0.168 (steepness of the curve)
```

This maps scores nonlinearly:

| Raw Score | Output % | Risk Level |
|-----------|----------|------------|
| 0         | ~4%      | Low        |
| 10        | ~12%     | Low        |
| 20        | ~50%     | Moderate   |
| 30        | ~88%     | High       |
| 40        | ~97%     | High       |
| 50        | ~99%     | High       |

---

## Step 4: Risk Stratification

```
pct < 20%    →  LOW RISK      Green   #30d158
20 ≤ pct < 45% → MODERATE RISK  Amber   #ff9f0a
pct ≥ 45%    →  HIGH RISK     Red     #ff453a
```

---

## Current Limitations

1. **Proxy weights only.** Current scoring thresholds are derived from published
   literature and expert consensus — not from the WVSUMC cohort data itself.
   Final β-coefficients from the multivariable logistic regression model will
   replace these upon study completion.

2. **No external validation.** The model has not been tested on an independent
   external dataset. It is subject to optimism and overfitting until bootstrap
   internal validation results are incorporated.

3. **Binary history flags.** Clinical history risk factors are treated as
   present/absent. Severity gradations (e.g., how well-controlled chronic HTN is)
   are not captured.

4. **No temporal modeling.** Serial measurements across gestational age are not
   modeled — each calculation is a single cross-sectional snapshot.

---

## References

- ACOG Practice Bulletin No. 222 · 2020
- ISSHP Classification, Diagnosis & Management · Magee et al. · 2022
- Jiménez-García et al. · *J Clin Med* · 2025
- Jhee JH et al. · *PLoS ONE* · 2019
- Riley RD et al. · Sample size for prediction models · *BMJ* · 2020
- Bodnar LM et al. · Obesity and PE risk · *Epidemiology* · 2005

---

*© 2026 GDD · Owner & Full-Stack Developer · All rights reserved.*  
*PreeclampsiaRisk · WVSUMC Late-Onset PE Calculator*
