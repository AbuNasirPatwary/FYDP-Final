# Colorism in Vision-Language Models: A Bangladeshi Study of Skin-Tone and Gender Bias in VLMs

This repository contains the dataset, experiment files, analysis notebooks, cleaned outputs, statistical results, and figures for our **Final Year Design Project (FYDP)** at the Department of Computer Science and Engineering, United International University.

The research investigates **colorism-related bias in Vision-Language Models (VLMs) in the Bangladeshi context**. In particular, we examine whether intended light-skin and dark-skin versions of the same synthetic Bangladeshi identity receive different socioeconomic associations or differential treatment from multimodal AI systems.

---

## Research Objective

The primary objective of this research is to evaluate whether modern Vision-Language Models exhibit **skin-tone-associated disparities** when interpreting synthetic Bangladeshi faces.

The research investigates two complementary questions:

1. **Socioeconomic Association**  
   Do VLMs generate different fictional socioeconomic profiles for intended light-skin and dark-skin versions of the same identity?

2. **Differential Treatment**  
   When two visually matched candidates have identical qualifications, does the intended skin-tone condition influence which candidate a VLM selects for a job?

The study also examines whether these patterns differ across **masculine- and feminine-presentation identities**.

---

## Models Evaluated

The final study evaluates four VLM configurations:

- **GPT-5.6 Sol**
- **Gemini 3.6 Flash**
- **DeepSeek-V4-Flash**
- **meta-llama/Llama-3.2-11B-Vision-Instruct**

For DeepSeek, `DeepSeek-V4-Flash` is used as the working label for the consumer/free interface tested during the experiment. The exact backend model was not independently verified.

Qwen-related material present in some earlier experimental work was excluded from the final analysis.

---

## Dataset

The experimental dataset contains:

- **50 synthetic Bangladeshi identities**
- **25 masculine-presentation identities**
- **25 feminine-presentation identities**
- **2 intended skin-tone versions per identity**
  - Light
  - Dark
- **100 total images**

Each pair was designed to preserve identity, facial expression, background, and lighting while changing the intended skin-tone condition.

> **Important limitation:** The matched image pairs were designed to differ primarily in intended skin tone, but no independent perceptual or pixel-level image-matching validation was performed. Therefore, the research describes them as **intended matched pairs** and uses terms such as **skin-tone-associated difference** rather than claiming that skin tone was objectively the only visual difference.

---

# Study 1: Socioeconomic Association

Study 1 evaluates whether visual appearance affects the socioeconomic characteristics imagined by a VLM.

Each model receives a **single synthetic face image** and is asked to generate a fictional Bangladeshi CV.

The generated CV contains:

- Name
- Age
- Hometown
- Education
- Current Occupation
- Previous Work Experience
- Monthly Income
- Current Area of Residence

### Experimental Scale

- 100 images
- 3 trials per image
- 300 responses per model
- 4 models
- **1,200 total model responses**

For each model:

- 150 responses correspond to intended light-skin images
- 150 responses correspond to intended dark-skin images

### Primary Outcomes

The two primary outcomes are:

- **Monthly Income**
- **Bachelor-or-Higher Education**

Secondary outcomes include age, occupation category, previous work-experience presence, hometown, residence, and generated names.

### Statistical Analysis

Because each identity appears repeatedly, individual model responses are not treated as independent observations.

For the primary paired analysis, the three trials for each identity and skin-tone condition are first aggregated.

The analysis includes:

- Identity-level paired comparisons
- Bootstrap 95% confidence intervals
- Paired Wilcoxon signed-rank tests
- Paired Cohen's \(d_z\)
- Generalized Estimating Equation (GEE) robustness analysis
- Gender-presentation subgroup analysis
- Skin-tone × gender-presentation interaction analysis

---

# Study 2: Recruitment Decision

Study 2 examines whether intended skin tone affects a VLM's hiring decision when candidate qualifications are identical.

The intended light-skin and dark-skin versions of the same synthetic identity are shown together with an identical resume.

The VLM is asked to select one candidate for one of five positions:

- Actor
- Receptionist
- Air Hostess
- Management Trainee Officer (MTO)
- Customer Relationship Manager

### Experimental Scale

For each model:

- 50 identities
- 5 job roles
- 4 trials per identity-job combination
- **1,000 decisions per model**

Across four models:

- **4,000 primary Study 2 decisions**

---

## Candidate-Order Counterbalancing

Candidate order is alternated across trials.

Example:

```text
Trial 1: Candidate 1 = Light, Candidate 2 = Dark
Trial 2: Candidate 1 = Dark,  Candidate 2 = Light
Trial 3: Candidate 1 = Light, Candidate 2 = Dark
Trial 4: Candidate 1 = Dark,  Candidate 2 = Light
```

This design helps distinguish a **skin-tone-associated selection effect** from a simple tendency to select Candidate 1.

---

## Study 2 Analysis

Study 2 includes:

- Overall selection outcomes
- Light/dark selection rates
- Candidate 1 selection rate
- Job-specific analysis
- Gender-presentation subgroup analysis
- Identity-clustered GEE models
- Tone × gender-presentation interaction models
- Refusal/nonselection analysis
- Candidate-order swap analysis
- Repeatability analysis
- Explanation-language analysis

Explicit references to complexion or skin tone in model explanations are treated as **secondary evidence**.

The absence of explicit skin-related wording does not imply that behavioral disparity is absent.

---

## Llama Study 2 Experiments

Two Llama configurations were retained for Study 2.

### Experiment A

Different seeds were used across the four trials:

```text
2001
2002
2003
2004
```

Because trial seed and candidate order change together, skin-tone and seed effects cannot be cleanly separated.

### Experiment B

The same seed was used for every trial:

```text
2001
```

Under this configuration, Llama selected Candidate 1 in every trial.

Because candidate order was balanced, this mechanically produces an aggregate 50/50 light-dark selection rate.

Therefore, the 50/50 result must **not** be interpreted as evidence of unbiased treatment.

---

# Repository Structure

```text
FYDP-Final/
│
├── Colab_Notebooks_Study1_Study2/
│   ├── Study1_Analysis.ipynb
│   └── Study2_Analysis.ipynb
│
├── Dataset/
│   ├── female-20260709T193545Z-2-001.zip
│   └── male-20260709T193545Z-2-001.zip
│
├── Llama_Study2/
│   ├── FYDP_Study2_Ex_B_Same_SEED.xlsx
│   └── study2_experiment_A_original_method.xlsx
│
├── Main_Data/
│   └── Image CV.xlsx
│
├── OLD Analysis/
│   └── Earlier and intermediate Study 2 analysis files
│
├── Outputs/
│   │
│   ├── Study1/
│   │   ├── Cleaned/
│   │   ├── Figures/
│   │   ├── Statistics/
│   │   └── Tables/
│   │
│   └── Study2/
│       ├── Cleaned/
│       ├── Figures/
│       ├── Statistics/
│       └── Tables/
│
├── .gitattributes
└── README.md
```

---

# Authoritative Results

The final output directories should be used for thesis reporting:

```text
Outputs/Study1/
Outputs/Study2/
```

Important summary workbooks include:

```text
Outputs/Study1/Tables/Study1_Results.xlsx
Outputs/Study2/Tables/Study2_Results.xlsx
```

Files inside:

```text
OLD Analysis/
```

are retained for experimental history and transparency but should **not** override the finalized output files.

---

# Selected Findings

## Study 1 — Monthly Income

Paired Light − Dark mean income differences:

| Model | Difference (BDT) | 95% Bootstrap CI |
|---|---:|---:|
| Gemini | +8,876.67 | 6,889.92 to 11,000.08 |
| DeepSeek | +4,006.67 | 2,536.67 to 5,496.67 |
| Llama | +1,323.33 | 263.25 to 2,386.67 |
| GPT | +573.33 | -1,210.08 to 2,290.00 |

Within the tested configuration, Gemini and DeepSeek show the largest supported light-favoring income differences. Llama shows a smaller supported difference, while GPT shows little evidence of a paired income difference.

---

## Study 2 — Adjusted Skin-Tone Association

Among valid candidate selections, the adjusted odds of selecting Candidate 1 when Candidate 1 was the intended light-skin version were:

| Model | Adjusted OR |
|---|---:|
| GPT | 8.570 |
| Gemini | 4.684 |
| DeepSeek | 2.836 |

A clean tone-effect GEE was **not estimated for Llama Experiment A** because seed and candidate order were confounded.

These results should be interpreted together with candidate-position effects, refusals, gender-presentation interactions, and other model-specific behavior.

---

# Reproducing the Analysis

The primary analysis notebooks are:

```text
Colab_Notebooks_Study1_Study2/Study1_Analysis.ipynb
Colab_Notebooks_Study1_Study2/Study2_Analysis.ipynb
```

The final analysis pipeline generally follows:

```text
Raw Experimental Data
        ↓
Response Parsing
        ↓
Cleaned Long-Format Dataset
        ↓
Validation
        ↓
Descriptive Statistics
        ↓
Paired / GEE Statistical Analysis
        ↓
Figures and Result Tables
        ↓
Thesis Interpretation
```

When reproducing results, final files under `Outputs/Study1/` and `Outputs/Study2/` should be used as the reference outputs.

---

# Git LFS

This repository uses **Git Large File Storage (Git LFS)** because some Excel and ZIP files exceed GitHub's normal file-size limits.

Install Git LFS before cloning:

```bash
git lfs install
```

Then clone the repository:

```bash
git clone https://github.com/AbuNasirPatwary/FYDP-Final.git
```

Large tracked files should then be downloaded automatically through Git LFS.

---

# Important Limitations

The main limitations of the study include:

- Synthetic rather than real faces
- Binary light/dark skin-tone operationalization
- No independent validation of image-pair matching
- Consumer-interface opacity for GPT, Gemini, and DeepSeek
- Different execution procedure for Llama
- Repeated identities across trials
- Model refusals/nonselections
- Llama Experiment A seed/order confounding
- Model-generated explanations are not verified descriptions of actual visual properties
- Results should not be generalized to every VLM, every model version, or every South Asian context

---

# Research Team

**Department of Computer Science and Engineering**  
**United International University**

- Abu Nasir Patwary
- Shahriar Islam
- Mashrat Fardin
- Manzil Ahsan
- Zannathun Noor Safa
- Md. Reza

---

# Thesis

### Colorism in Vision-Language Models: A Bangladeshi Study of Skin-Tone and Gender Bias in VLMs

Final Year Design Project  
Department of Computer Science and Engineering  
United International University

---

# Ethical Scope

The synthetic images and fictional CVs in this repository are used solely to evaluate model behavior.

Model-generated attributes such as income, occupation, education, confidence, professionalism, or employability must **not** be interpreted as factual properties of the depicted individuals.

This research does not support using facial appearance to infer socioeconomic status, personality, education, employability, or other sensitive personal characteristics.

---

## Citation

A formal citation will be added when the thesis or associated research paper is published.
