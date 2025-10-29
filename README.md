
# Prediction of Ventricular Arrhythmias in Non-Ischemic Cardiomyopathy Using a 12-Lead ECG-Based Machine Learning Model

## Project Overview

Arrhythmic risk stratification in **non-ischemic cardiomyopathy (NICM)** remains a major clinical challenge. Traditional predictors—such as **left ventricular ejection fraction (LVEF < 35%)**, **late gadolinium enhancement (LGE)**, and **genetic markers**—have limited accuracy in identifying patients at risk of **sustained ventricular arrhythmias (SVA)**.

This project develops and evaluates an **ECG-based machine learning (ECG-ML)** model capable of predicting SVA in NICM patients, outperforming established clinical predictors.

---

## Background

* **Cohort:** 314 patients with NICM, no prior SVA.
* **Data:** Baseline 12-lead ECGs, cardiac MRI (for LGE), and genetic testing results.
* **Outcome:** Sustained ventricular arrhythmia (SVA), defined as sudden cardiac death, sustained VT, or appropriate ICD intervention.

* **Approach:**

  * Neural network trained on 80% of ECGs.
  * Validation on an independent 20% test set.
  * Two model variants:

    1. **ECG-only model (ECG-ML)**
    2. **ECG + Age**

---

## Repository Structure

├── data_processing/          # Scripts for ECG data preprocessing and feature extraction
├── evaluation/               # Model evaluation scripts and performance metrics
├── explainability/           # Model interpretability (e.g., Grad-CAM, SHAP)
├── models_training/          # Neural network training pipelines
├── pre_trained_models/       # Saved trained models and weights
├── requirements.txt          # Python dependencies
└── README.md                 # Project documentation (this file)


##  Methods Summary

* **Model architecture:** Neural network trained on raw and processed ECG signals.
* **Training strategy:** Multiple ECGs per patient were included to capture intra-individual variability, and both upsampling and downsampling techniques were applied to prevent overfitting.
* **Comparison:** ECG-ML model vs. a multivariate clinical model including:

  * LVEF
  * LGE (presence and high-risk type)
  * Pathogenic genetic variants
* **Evaluation metric:** AUC (area under the ROC curve) and sensitivity/specificity balance.


## Results

| Metric       |   ECG-ML (ECG only)  |  Clinical Model  |
| :----------- | :------------------: | :--------------: |
| Sensitivity  |          75%         |         —        |
| Specificity  |          85%         |         —        |
| AUC (95% CI) | **0.86 (0.57–1.00)** | 0.53 (0.24–0.82) |

The ECG-ML model demonstrated strong predictive performance, significantly exceeding traditional risk factor–based models. No combination of clinical covariates improved upon ECG-ML performance.

---

##  Installation

### Prerequisites

* Python ≥ 3.8
* GPU (recommended for model training)

### Install dependencies

pip install -r requirements.txt


---

##  Usage

### 1. Preprocess the multivariate clinical and get ECGs for each patient 

 data_processing/NICM_Data.ipynb


### 2. Train the Models


models_training/NICM_WorkSpaceTF_ECG_.ipynb
models_training/NICM_WorkSpaceTF_ECG_With_vars.ipynb


### 3. Evaluate Performance

evaluation/NICM_evaluation.ipynb

### 4. Explain Model Predictions

explainability/NICM_Expl.ipynb

### 5. Use the pre-trained models
pre_trained_models/model_Resnet_50_ecg_With_Vars.h5
pre_trained_models/model_Resnet_50_ecg.h5

## Key Findings

* ECG-ML achieved **AUC 0.86** for predicting sustained ventricular arrhythmia in NICM patients.
* **No clinical variable** (LVEF, LGE, genotype) independently improved performance.
* The model highlights the potential of **ECG-based deep learning** for risk stratification in cardiomyopathy.


## Limitations

* Retrospective, single-center cohort
* Modest sample size (n = 314)
* Requires **external validation** on larger, multicenter datasets before clinical use






