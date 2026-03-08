# Research Background

**PreeclampsiaRisk · WVSUMC — Research Context**  
*Last updated: March 2026 · Version 1.3.0*

---

## The Study

```
Title       :  Risk Stratification Model for Predicting Late-Onset Preeclampsia
               Using Clinical and Laboratory Data from Filipino Pregnant Women
               Admitted to West Visayas State University Medical Center

Institution :  West Visayas State University Medical Center (WVSUMC)
               College of Medicine — Medical Group 4

Data Period :  January 2016 – December 2025
Presented   :  February 2026

Design      :  Retrospective Cohort Study
               Multivariable Logistic Regression
               Bootstrap Internal Validation (TRIPOD, B = 1,000 replications)
```

---

## Background

### Preeclampsia as a Public Health Problem

Preeclampsia (PE) is a hypertensive disorder of pregnancy affecting 2–8% of
pregnancies globally and is a **leading cause of maternal and perinatal morbidity
and mortality** worldwide. In the Philippines, it remains among the top causes
of direct maternal death.

PE is clinically defined as **new-onset hypertension (≥ 140/90 mmHg) at or
after 20 weeks of gestation** accompanied by evidence of systemic organ
involvement — proteinuria, renal impairment, hepatic dysfunction, hematological
abnormalities, or uteroplacental dysfunction (ISSHP 2022).

### Early-Onset vs. Late-Onset Preeclampsia

The clinical and pathophysiological distinction between subtypes is increasingly
recognized as essential for both prediction and management:

| Feature | Early-Onset PE (< 34 wks) | Late-Onset PE (≥ 34 wks) |
|---------|--------------------------|--------------------------|
| Prevalence | ~25–30% of all PE | ~70–75% of all PE |
| Pathophysiology | Primarily placental | Mixed placental + maternal |
| Uteroplacental Doppler | Often abnormal | Often normal |
| Maternal disease | Severe, multi-organ | Variable, often milder |
| Fetal growth restriction | Common | Less common |
| Predictive biomarkers | PlGF, sFlt-1, uterine PI | Less sensitive |
| Clinical course | Rapid deterioration possible | Slower progression |

Late-onset PE, despite being more prevalent, is **paradoxically harder to predict**
using first-trimester biomarker algorithms (e.g., the FMF combined test) because
placental biomarkers perform less well in this subtype. This creates a gap that
clinical and laboratory parameters assessed at admission can help fill.

### The Philippine Context

Filipino pregnant women present demographic, nutritional, and healthcare access
characteristics that differ meaningfully from Western European populations on
which most existing PE prediction models were developed. Specifically:

- Higher background rates of undernutrition and micronutrient deficiency
- High prevalence of pre-gestational diabetes and metabolic syndrome
- Delayed first antenatal visit and incomplete prenatal care
- Limited access to biomarkers such as PlGF and sFlt-1
- Higher rates of late presentation to tertiary care centers

A **locally derived and validated** risk stratification model using **routine
clinical and laboratory parameters** — MAP, UPCR, complete blood count, liver
enzymes, creatinine, uric acid, and clinical history — is therefore both more
appropriate and more practically deployable in the Philippine hospital setting
than imported biomarker-dependent algorithms.

---

## Study Design

### Population

- **Setting:** West Visayas State University Medical Center, Iloilo City, Philippines
- **Inclusion:** Pregnant women admitted to the OB-GYN service, January 2016 – December 2025
- **Outcome:** New-onset hypertension ≥ 34 weeks with systemic features (ISSHP 2022)
- **Exclusion:** Pre-existing PE diagnosis, incomplete records, multiple admissions
  for the same pregnancy episode

### Sample Size Calculation

Sample size was estimated using the **Riley et al. (2020)** framework for
prediction model development:

```
EPP (Events Per Parameter)  ≥ 9
Shrinkage target             ≥ 0.90 (90%)
Estimated PE prevalence      6.4%
Number of candidate parameters  12
Required events              ≥ 108
Required total sample        ≥ 1,160 records
```

A conservative shrinkage target of 0.90 (10% optimism correction) was applied
to reduce overfitting in the final model.

### Statistical Approach

1. **Univariable analysis** — individual association of each candidate predictor
   with late-onset PE outcome (chi-squared, Fisher's exact, Mann-Whitney U)

2. **Multivariable logistic regression** — backward stepwise selection with
   Akaike Information Criterion (AIC) for model parsimony; final model retains
   predictors with p < 0.05 after adjustment

3. **Model performance** — assessed via:
   - Area Under the ROC Curve (AUC / C-statistic)
   - Sensitivity and specificity at optimal Youden threshold
   - Positive and negative predictive values
   - Hosmer-Lemeshow goodness-of-fit test (calibration)
   - Calibration plot (observed vs. predicted probabilities)

4. **Bootstrap internal validation** — 1,000 bootstrap replications (TRIPOD
   guideline); optimism-corrected AUC and calibration slope reported

5. **Risk stratification** — final model output categorized into Low / Moderate /
   High risk tiers with clinically meaningful thresholds

### Reporting Standard

The study follows the **TRIPOD (Transparent Reporting of a multivariable
prediction model for Individual Prognosis Or Diagnosis)** statement for
prediction model development and reporting.

---

## Candidate Predictors

The following 12 parameters were selected as candidate predictors based on
biological plausibility, evidence from the literature, and routine availability
at WVSUMC:

| # | Parameter | Rationale |
|---|-----------|-----------|
| 1 | Mean Arterial Pressure | Central PE diagnostic criterion |
| 2 | UPCR | Proteinuria — key PE feature |
| 3 | Platelet Count | Thrombocytopenia — severe feature / HELLP |
| 4 | Serum Creatinine | Renal involvement — severe feature |
| 5 | AST | Hepatic involvement — severe feature |
| 6 | ALT | Hepatic involvement — supporting |
| 7 | Uric Acid | Renal urate clearance; severity marker |
| 8 | BMI | Modifiable metabolic risk factor |
| 9 | Maternal Age | U-shaped risk curve (adolescent + AMA) |
| 10 | Gestational Age | Late-onset PE window definition |
| 11 | Parity | Nulliparity as established risk factor |
| 12 | Clinical History | Prior PE, HTN, DM, APS, FHx, multiples |

---

## Prototype Limitations

The current calculator is a **prototype** with the following acknowledged limitations:

1. **Proxy weights.** Scoring thresholds are derived from published literature,
   not from the WVSUMC cohort regression model. They will be replaced by final
   β-coefficients upon study completion.

2. **Internal validation only.** Bootstrap internal validation corrects for
   optimism but does not replace external validation on an independent dataset
   from a separate institution or time period.

3. **Single-center data.** Results may not generalize to other Philippine
   hospitals with different patient populations, clinical protocols, or
   laboratory reference ranges.

4. **Retrospective design.** Unmeasured confounders inherent to retrospective
   data cannot be fully controlled.

5. **No first-trimester biomarkers.** Predictors such as PlGF, sFlt-1, and
   uterine artery Doppler PI — which improve early-onset PE prediction — were
   not included due to limited availability in the study population.

6. **Binary history flags.** Clinical comorbidities are captured as present/absent.
   Severity gradations (e.g., controlled vs. uncontrolled chronic hypertension)
   are not modeled.

---

## Literature Summary

Key studies informing the parameter selection and scoring structure:

| Study | Key Finding | Relevance |
|-------|------------|-----------|
| Jiménez-García et al. *JCM* 2025 | Systematic review of PE prediction models; MAP, UPCR, platelets most consistent predictors | Parameter selection |
| Jhee JH et al. *PLoS ONE* 2019 | Machine learning PE prediction; uric acid and creatinine significant | Uric acid, creatinine inclusion |
| Zhang et al. *Biomedicines* 2025 | Biochemical marker performance in PE risk | Liver enzyme thresholds |
| Zhu et al. *BMJ Open* 2021 | PE risk factors in Asian populations | Population relevance |
| Cua-Lam & Ong *PJOG* 2025 | Filipino PE cohort; uric acid and BMI associations | Local population data |
| Magee et al. *Preg Hypertens* 2022 | ISSHP 2022 classification | Diagnostic definitions |
| ACOG Practice Bulletin 222, 2020 | Severe feature criteria, management thresholds | Clinical thresholds |
| Riley RD et al. *BMJ* 2020 | Sample size guidance for prediction models | Study design |
| Duckitt & Harrington *BMJ* 2005 | Risk factors for PE — systematic review | History flag weights |
| Bodnar LM et al. *Epidemiology* 2005 | Obesity and PE risk — dose-response | BMI scoring |

---

## Contact

For research collaboration, clinical feedback, or methodology inquiries:

**GDD — Owner & Full-Stack Developer**  
[gdddevelopers.dev@gmail.com](mailto:gdddevelopers.dev@gmail.com)

---

*© 2026 GDD · Owner & Full-Stack Developer · All rights reserved.*  
*PreeclampsiaRisk · WVSUMC Late-Onset PE Calculator*
