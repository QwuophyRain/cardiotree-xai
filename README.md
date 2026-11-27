Explainable Machine Learning in Cardiology: Divergent Capabilities of Tree-Based Algorithms in Heart Failure Prognosis vs. Phenotyping

[!Python 3.9+](https://www.python.org/)
[!Scikit-Learn](https://scikit-learn.org/)
[!Explainability](https://shap.readthedocs.io/)
[!License: MIT](#license)

> Authors: Rainsford Kofi Senam (2324500011), Felix Otu Kofi Agyenkwah (2425500019), Michael Osei-Bobie (2425500237), and Abonga Salifu Bashiru (2425500046)  
> Affiliation: Faculty of Computing and Information Systems (FoCIS), School of Graduate Studies (SGSS), Ghana Communication Technology University (GCTU), Accra, Ghana  
> Date: January 22, 2026  
> Contact: senamrain@gmail.com

***
Overview

This repository accompanies our research study investigating the operational boundaries of routine Electronic Health Record (EHR) tabular biomarkers in heart failure machine learning. Using leak-free, fold-safe cross-validation pipelines across five model families (Random Forest, XGBoost, LightGBM, CatBoost, and regularized linear baselines), we contrast two clinical endpoints on the UCI Heart Failure Clinical Records cohort ($N = 299$) and a simulated multi-center domain-shift cohort ($n = 150$):

Structural LVEF Phenotyping (Regression & 3-Class Classification): Predicting continuous Left Ventricular Ejection Fraction (LVEF) and classifying ESC/AHA phenotypes (HFrEF $\le 40%$, HFmrEF $41\text{--}49%$, HFpEF $\ge 50%$).
All-Cause Mortality Prognosis: Predicting binary DEATH_EVENT with follow-up duration (time) strictly excluded to prevent temporal leakage.

Core Finding: Identical tree-based ensemble pipelines achieve strong discrimination and reasonable calibration for mortality prognosis (internal CV ROC-AUC up to 0.775; external domain-shift ROC-AUC 0.841, Brier score 0.177), yet fail systematically on continuous LVEF regression ($R^2 \le -0.063$) and 3-class structural phenotyping (0.00 recall for HFmrEF, external Macro-F1 0.25). Routine EHR biomarkers are effective for risk stratification, but cannot substitute for echocardiography in structural phenotyping.

***
Repository Structure

hf_xai_publication_package/
├── README.md                                  # Project documentation for GitHub
├── requirements.txt                           # Python dependencies
├── notebook/
│   └── hf_xai_prognosis_vs_phenotyping.ipynb  # Complete reproducible Google Colab notebook
├── manuscript/
│   ├── main.tex                               # Standard two-column LaTeX manuscript (pdflatex-ready)
│   ├── main_ieee.tex                          # IEEEtran conference LaTeX source (Overleaf-ready)
│   ├── main.pdf                               # Compiled two-column LaTeX PDF
│   └── figures/                               # Figures linked by LaTeX sources
├── report/
│   ├── ML_Research_Full_Report.pdf            # Publication-ready standalone ML Research Report (PDF)
│   └── ML_Research_Full_Report.docx           # Editable Word manuscript/report (DOCX)
└── figures/
    ├── fig1_shap_summary_lvef_regression.png
    ├── fig2_shap_importance_lvef_regression.png
    ├── fig3_confusion_matrix_lvef.png
    ├── fig4_shap_dependence_creatinine_age.png
    ├── fig5_shap_summary_mortality.png
    └── fig6_calibration_curve_external.png

***
Key Experimental Results

1. Continuous LVEF Regression (10-Fold CV, Consistent Across All 5 Clinical Splits)
Model	MAE (%)	RMSE (%)	$R^2$
Random Forest	9.210	11.709	-0.063
CatBoost	9.317	11.829	-0.087
Ridge Regression	9.447	12.051	-0.117
LightGBM	9.584	12.123	-0.145
XGBoost	9.767	12.218	-0.174
	2. Categorical LVEF Phenotyping (5-Fold Stratified CV)
Model	Accuracy	Macro-F1
CatBoost	0.559	0.346
XGBoost	0.726	0.338
Random Forest	0.719	0.333
LightGBM	0.542	0.309
Logistic Regression	0.324	0.269
	3. All-Cause Mortality Prognosis (5-Fold Stratified CV, time Excluded)
Model	ROC-AUC	Accuracy	F1-Score
Random Forest	0.775	0.729	0.536
Logistic Regression	0.769	0.686	0.564
XGBoost	0.746	0.729	0.518
LightGBM	0.746	0.729	0.609
CatBoost	0.740	0.723	0.565
	4. External Domain-Shift Validation ($n = 150$, XGBoost)
Endpoint	Metric	Result
Mortality Prognosis	ROC-AUC	0.841
Mortality Calibration	Brier Score	0.177
LVEF Phenotyping	HFrEF / HFmrEF / HFpEF Recall	0.89 / 0.00 / 0.00
LVEF Phenotyping	Macro-F1	0.25
	***
Key Visualizations

Hold-Out LVEF Confusion Matrix	External Mortality Calibration Curve
Confusion Matrix	Calibration Curve
	Mortality SHAP Summary	HFrEF Creatinine–Age Interaction
Mortality SHAP	SHAP Dependence
	***
Quickstart & Reproducibility

# 1. Clone repository
git clone https://github.com/QwuophyRain/hf-xai-prognosis-phenotyping.git
cd hf-xai-prognosis-phenotyping

# 2. Create virtual environment & install dependencies
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt

# 3. Launch Jupyter Notebook
jupyter notebook notebook/hf_xai_prognosis_vs_phenotyping.ipynb

Compiling the LaTeX Manuscript
cd manuscript
pdflatex main.tex
pdflatex main.tex
(For IEEE conference submission on Overleaf, upload manuscript/main_ieee.tex alongside the manuscript/figures/ directory.)

***
Citation

If you use this code, methodology, or findings in your research, please cite:

@article{senam2026explainable,
  title={Explainable Machine Learning in Cardiology: Divergent Capabilities of Tree-Based Algorithms in Heart Failure Prognosis versus Structural Phenotyping},
  author={Senam, Rainsford Kofi and Agyenkwah, Felix Otu Kofi and Osei-Bobie, Michael and Bashiru, Abonga Salifu},
  institution={Faculty of Computing and Information Systems (FoCIS), School of Graduate Studies (SGSS), Ghana Communication Technology University (GCTU)},
  address={Accra, Ghana},
  year={2026},
  month={January}
}

License
Released under the MIT License. The UCI Heart Failure Clinical Records dataset is publicly available via the UCI Machine Learning Repository.
