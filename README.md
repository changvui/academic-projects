# Academic projects — Tiong Chang Vui

Final-year Software Engineering (Honours) student at Tunku Abdul Rahman University of
Management and Technology (TAR UMT), Malaysia. CGPA 3.59, Dean's List (2 semesters).

This repository collects the coursework I am allowed to publish. Everything here was built
for a university course; model weights and datasets are left out because of their size.

| # | Project | Course | Focus |
|---|---------|--------|-------|
| 1 | [MySTRA web application](01-mystra-web-app) | Collaborative Development | Multi-role web app, document workflow, data migration |
| 2 | [Obesity level prediction](02-data-science-obesity) | BMDS2003 Data Science | Data cleaning, feature encoding, model comparison |
| 3 | [Brain tumour MRI classification](03-ai-brain-tumour) | Artificial Intelligence | Transfer learning, evaluation, Streamlit demo |

## What each project shows

**MySTRA** — a short-term rental accommodation system for the Malaysian market. Hosts
register and upload compliance documents (SSM certificate, tax information, safety
certification); government administrators review, verify and audit submissions. Includes a
migration tool that imports records from a simulated legacy system.

**Obesity prediction** — a full data-science pipeline on a survey dataset: duplicate removal,
column standardisation, outlier analysis, label / ordinal / one-hot encoding, scaling, then
Logistic Regression, Decision Tree and Random Forest compared with manual hyperparameter
tuning and classification reports.

**Brain tumour classification** — fine-tuning a SegFormer-B0 vision model to sort MRI scans
into glioma, meningioma, pituitary tumour and no tumour, with per-class precision, recall and
a confusion matrix, plus a Streamlit interface for the demo. A teammate trained a ResNet-50
baseline in the same folder; the SegFormer notebooks are mine.

## Notes

- Report PDFs are not included: they contain teammates' student IDs. Available on request.
- Model weights (`.pth`, `.safetensors`), the MRI image dataset and training checkpoints are
  not included.
- Team projects are marked; individual contribution is described inside each folder.
