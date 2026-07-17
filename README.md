# ASESII Group 06 24A02 Project-Based Quiz 1: Reproduction Guide

## 1. Archive Folder Layout

To reproduce this analysis without path errors, ensure your directory exactly matches this structure:
```
STAT02-Lab-Project/
├── ASESII_24A02_ProjectExam_Ridge_Lasso_ProblemStatement.pdf
├── data/
    └── prostate.csv
├── README.md     
└── templates/
    ├── ASESII_24A02_ProjectExam_SampleSubmission.Rmd        
    ├── ASESII_24A02_ProjectExam_SampleSubmission.pdf
    ├── Group06_AI_Log.csv       
    └── references.bib
```


## 2. Declared Software & Dependencies

This analysis requires R (>= 4.1.0) and the following declared packages:

tidyverse 
glmnet
broom
knitr
rmarkdown 

Note: The R Markdown setup chunk automatically checks for these packages and will stop execution with an informative prompt if any are missing.

## 3. Step-by-Step Reproduction Instructions

To compile the final report from a clean session:

Open a Clean Session: Launch RStudio and select Session -> Restart R (or run rm(list = ls()); gc() in the console) to ensure the workspace is completely empty.

Set Working Directory: Set your working directory to the folder containing Group06_ProjectQuiz1.Rmd.

Render Report: Execute the following command in the R console:
```
rmarkdown::render("templates/ASESII_24A02_ProjectExam_SampleSubmission.Rmd", output_format = "all")
```

Verify Output: Check the directory for the generated Group06_ProjectQuiz1.html (and/or .pdf) file.

## 4. Methodological Audit & Data Leakage Safeguards

Fixed Random Seeds: All random processes are hardcoded to group-assigned seeds (split = 240206, cv = 240306, features = 240406) to ensure 100% numerical reproducibility across runs.

Holdout Response Quarantine Boundary: To prevent target leakage, the test response vector y_test is generated during the initial 80/20 partition in Section 1B (split-and-scale) but is strictly quarantined throughout all exploratory analysis, OLS fitting, regularized cross-validation, and non-linear feature engineering.

Point of First Computation: The holdout responses y_test enter mathematical computation for the first and only time in Section 4D (final-holdout-evaluation), where they are evaluated against locked candidate predictions to generate the final RMSE/MAE comparison table.