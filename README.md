# DietOpt-SLM

**DietOpt-SLM** is a solver-guided framework for personalized multi-day dietary planning under explicit nutritional, clinical, and preference constraints. The framework transforms semantic dietary inferences into structured quantitative representations and subsequently generates gram-specified 7-day meal plans through integer-programming optimization.

This repository accompanies the study:

> **DietOpt-SLM: A Solver-Guided Framework Based on a Dietary Language Model for Personalized Dietary Recommendation in Non-Communicable Diseases**

The repository is intended to support research transparency, reproducibility, and future prospective evaluation of DietOpt-SLM.

---

## Data Resources

DietOpt-SLM was developed using multiple data resources with different roles in model pre-training, supervised fine-tuning, knowledge construction, held-out evaluation, expert-panel validation, and human evaluation.

### Dietary Preference Dataset (DPD)

The Dietary Preference Dataset was constructed to support dietary-preference inference by Diet-SLM.

**DPD-PT** contains 99,000 instruction–response pairs used for domain pre-training. It was constructed from structured user-profile and dietary-context templates, with Qwen-Plus used to generate supervision samples representing diverse dietary preferences.

The input information includes demographic and anthropometric characteristics, dietary context, and user-profile descriptions. The outputs include structured personal and regional preferences related to ingredients, flavors, cooking methods, and dietary restrictions.

**DPD-FT** contains 11,000 instruction–response pairs selected from the synthetic DPD corpus and further reviewed by nutrition experts for supervised fine-tuning.

The DPD resources are training data and were not used as clinical evaluation datasets.

**Availability:**  
The DPD dataset and associated pre-training prompt templates will be made publicly available in this repository upon acceptance of the manuscript.

---

### Dietary Pattern Dataset (DPT)

The Dietary Pattern Dataset was constructed to support dietary-pattern inference by Diet-SLM.

**DPT-PT** contains 99,000 instruction–response pairs used for domain pre-training. It was constructed through **physics-guided and structured rule-based synthesis** based on **22 predefined dietary patterns** and their corresponding nutritional rules and constraints.

The outputs provide structured dietary-pattern recommendations and the corresponding reasoning for pattern selection.

**DPT-FT** contains 11,000 instruction–response pairs selected from the synthetic DPT corpus and further refined by nutrition experts for supervised fine-tuning.

The DPT resources were used for model training rather than runtime dietary inference. After training, Diet-SLM performs dietary-pattern inference from individual user profiles.

**Availability:**  
The DPT dataset and associated pre-training prompt templates will be made publicly available in this repository upon acceptance of the manuscript.

---

## Quantitative Food Knowledge Graph (QF-KG)

The **Quantitative Food Knowledge Graph (QF-KG)** provides structured food, nutrient, dietary, and health-related knowledge for DietOpt-SLM.

The current QF-KG contains approximately:

- **94,480 entities**
- **1,142,329 relationships**
- **16 entity types**
- **19 relationship types**

The graph includes information on:

- food ingredients and quantities;
- energy and macronutrients;
- micronutrients;
- amino acids and fatty acids;
- food categories;
- cooking methods;
- regional cuisine attributes;
- allergens;
- clinically contraindicated foods and attributes;
- dietary-preference relationships;
- meal-time suitability;
- food-combination relationships.

Within DietOpt-SLM, the QF-KG reasoner converts semantic dietary information and nutritional knowledge into structured quantitative representations, including a quantified candidate food pool and preference- and suitability-related indicators for downstream optimization.

**Availability:**  
The QF-KG schema will be publicly released in this repository upon acceptance.

---

## Nutritional Knowledge Resources

Additional resources used for domain pre-training and nutritional knowledge construction include:

### Nutrition Books (NB)

Digitized Chinese nutrition textbooks and professional reference books were used to provide foundational knowledge related to nutrition, food science, dietary principles, and clinical nutrition practice.

### Guidelines and Expert Consensus (GEC)

The GEC resource contains **212 formally issued or peer-reviewed clinical guidelines and expert-consensus documents**.

These materials support the definition of nutrient targets, dietary-pattern characteristics, disease-specific restrictions, food exclusions, and other clinically relevant dietary rules.

### Nutrition Articles (NA)

The NA corpus contains **36,800 nutrition-related articles** from journals, professional magazines, and curated professional nutrition platforms.

These articles were primarily used to enrich nutritional terminology, semantic representations, and broader domain knowledge during pre-training. Unverified online health-advice content was excluded.

**Availability:**  
These source materials are subject to the copyright, licensing, and availability restrictions of their original publishers and are therefore not redistributed in full through this repository.

---

## Clinical Nutrition Dataset (CND)

The Clinical Nutrition Dataset contains **2,000 de-identified clinical nutrition cases** from Fuwai Hospital.

It was divided before supervised fine-tuning into two independent subsets:

### CND-FT

- **1,500 expert-validated clinical nutrition cases**
- Used for supervised fine-tuning of Diet-SLM
- Includes demographic, anthropometric, clinical, biochemical, dietary-history, nutrition-assessment, and dietitian-derived intervention information

### CND-Test

- **500 de-identified clinical cases**
- Fixed before supervised fine-tuning
- Reserved exclusively for held-out evaluation
- Not used for training, fine-tuning, or parameter selection

The held-out cases include hypertension, diabetes mellitus, dyslipidemia, selected comorbidity combinations, and healthy individuals used for comparative evaluation.

All clinical records were de-identified before analysis.

**Availability:**  
CND-FT and CND-Test cannot be publicly released because of privacy, ethics, and institutional data-governance restrictions.

The data may be available from the corresponding author upon reasonable request and completion of applicable institutional data-access procedures, subject to ethics approvals **Nos. 2022-1781 and 2023-2021**.

---

## Dietary Logging Dataset (DLD)

The Dietary Logging Dataset contains **500 de-identified dietary records** from patients at Fuwai Hospital.

The records contain information including:

- food names;
- food quantities;
- ingredients;
- cooking methods;
- meal timing;
- related dietary information.

The dietary logs were verified by registered dietitians and used for supervised fine-tuning to improve alignment with real-world dietary records.

**Availability:**  
DLD cannot be publicly released because of privacy and institutional restrictions. Access may be considered upon reasonable request to the corresponding author, subject to applicable ethics, privacy, and institutional requirements.

---

## Expert-Panel Validation Set (EP-Val)

The **Expert-Panel Validation Set (EP-Val)** contains **108 de-identified, clinically characterized NCD cases** derived from an independent lifestyle-intervention randomized controlled trial cohort.

EP-Val was used exclusively for post hoc prescription-level methodological validation and was independent of model development.

It was not used for:

- Diet-SLM pre-training;
- supervised fine-tuning;
- CND-Test evaluation;
- QF-KG construction;
- solver-rule development;
- parameter selection.

For each EP-Val case, DietOpt-SLM was independently run three times using standardized patient information without access to dietitian-prescribed macronutrient targets.

Six senior registered dietitians independently prescribed energy and macronutrient targets for the same cases under blinded conditions. The dietitians did not have access to DietOpt-SLM outputs or to one another's prescriptions.

The **mean of the six independent dietitian prescriptions** was used as the external expert-panel reference.

**Availability:**  
EP-Val is covered by a separate institutional ethics approval (**No. 2021-1559**) and corresponding data-governance requirements.

The data may be available from the corresponding author upon reasonable request where permitted by the relevant ethics, privacy, and institutional requirements.

---

## Human Evaluation Data

### Volunteer User-Evaluation Dataset

A total of **153 volunteers** evaluated their own participant-specific DietOpt-SLM-generated 7-day meal plans.

Participants rated their meal plans on a 0–5 Likert scale across four dimensions:

- personalization;
- cultural appropriateness;
- practicality;
- dietary diversity.

This evaluation was designed to assess participant-perceived acceptability and should not be interpreted as evidence of clinical efficacy or long-term dietary adherence.

### Independent Dietitian Assessment

Three advanced registered dietitians independently evaluated **40 DietOpt-SLM-generated 7-day meal plans** selected from CND-Test.

The plans were evaluated in terms of:

- nutritional adequacy;
- dietary safety;
- completeness;
- guideline consistency.

This assessment was designed as an independent professional quality evaluation and was distinct from the six-dietitian EP-Val experiment.

**Availability:**  
Human-evaluation data may be available from the corresponding author upon reasonable request, subject to relevant privacy, ethics, and institutional requirements.

---

# Code Availability

The source code supporting the implementation and evaluation of DietOpt-SLM, together with documentation and example scripts, will be made publicly available through this repository upon acceptance of the manuscript.

The planned public release will include, where applicable:

- core DietOpt-SLM implementation;
- evaluation scripts;
- example scripts;
- usage documentation;
- pre-training prompt templates;
- synthetic DPD resources;
- synthetic DPT resources;
- QF-KG schema.

Clinical and human-participant datasets will **not** be included in the public repository and remain subject to the controlled-access procedures described above.

---

# DietOpt-SLM Mini Program

Based on the DietOpt-SLM framework, we have developed a research-oriented mini program to support its practical implementation.

<p align="center">
  <img src="assets/my_nutrition.png"
       alt="My Nutrition Mini Program QR Code"
       width="260">
</p>

<p align="center">
  <b>Scan the QR code to access the DietOpt-SLM mini program.</b>
</p>

Future prospective studies based on DietOpt-SLM will use this mini program for data collection, analysis, and validation of the framework.

---



# Data and Research Access

Requests for controlled-access datasets or research collaboration may be directed to the corresponding authors of the DietOpt-SLM study.

Access to human-derived datasets is subject to:

- ethical approval requirements;
- participant privacy protection;
- institutional data-governance policies;
- applicable data-access agreements.

---

# Repository

**DietOpt-SLM / HealthMetrix**

[https://github.com/Sean2HelloWorld/HealthMetrix](https://github.com/Health-Metrix/DietOpt-SLM)

---

## Important Notice

This repository is intended for scientific research and reproducibility.

DietOpt-SLM is an AI-assisted dietary-planning research framework. It is **not intended to replace professional medical diagnosis, individualized clinical treatment, or consultation with qualified healthcare professionals**.
