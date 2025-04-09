# Healthcare Diabetes Prediction Project

## Overview
This project demonstrates how to predict high-risk diabetes patients using **Alteryx**. The workflow integrates three datasets related to patient information, hypertension-related tests, and lab results. Using logistic regression, the project segments patients into high, medium, and low-risk categories for diabetes, based on their medical data.

---

## Description
### Datasets Used:
1. **Predicting_diabetes.diagnosis.csv**: Contains patient IDs and hypertension-related test results (0 or 1).
2. **Predicting_diabetes.patients.yxdb**: Contains patient IDs, details, smoking status, and medication information (Lipitor, Lisinopril, Simvastatin).
3. **Predicting_diabetes.lab_results.csv**: Contains patient IDs and their corresponding HL7 test results.

### Workflow Process:
1. **Joins Workflow**:
   - The datasets are joined based on the patient ID, creating a unified dataset named `Diabetes.yxdb` as the output. This dataset combines all relevant patient data for the next steps in the analysis.
![image](https://github.com/user-attachments/assets/51be8679-0ddb-43b3-ae74-40d3b8cb6fae)

2. **HighRiskDiabetesPatients Workflow**:
   - Data cleansing is performed to handle missing or invalid values.
   - The dataset is split into training (50%) and validation (50%) samples.
   - Logistic regression is applied to the estimation sample to predict the probability of diabetes (target variable: DMIndicator).
   - A scoring tool is used to calculate the probabilities for each patient:
     - `score0`: Probability of **not** having diabetes.
     - `score1`: Probability of having **diabetes**.
   
3. **Risk Segmentation**:
   - Based on the value of `score1`, patients are categorized into:
     - **High Risk**: If score1 > 0.6
     - **Medium Risk**: If 0.3 < score1 ≤ 0.6
     - **Low Risk**: If score1 < 0.3
   - High-risk patients are filtered for further analysis or potential intervention.

---

## How to Run the Project

### Requirements:
- Alteryx Designer (or Alteryx Server)
- The dataset files (`.csv`, `.yxdb`) must be accessible in the specified directory structure.

### Running the Workflows:
1. Download or clone this repository to your local machine.
2. Open **Alteryx Designer**.
3. Load the **`Joins.yxmd`** workflow to join the datasets and generate the `Diabetes.yxdb` output.
4. Load the **`HighRiskDiabetesPatients.yxmd`** workflow for data cleansing, modeling, and risk segmentation.
5. The final output will be available in the **Output** folder as `Diabetes.yxdb`.

---

## Results
After running the workflow, high-risk diabetes patients are successfully identified based on the logistic regression model. This segmentation can help healthcare professionals prioritize care for high-risk individuals and improve patient outcomes.



## Project Structure
![image](https://github.com/user-attachments/assets/d07bbc70-2b09-4789-b5dc-33bbee0ad5f6)

```plaintext
- /Healthcare_Diabetes_Prediction
    ├── /Data
    │   ├── Predicting_diabetes.diagnosis.csv
    │   ├── Predicting_diabetes.patients.yxdb
    │   ├── Predicting_diabetes.lab_results.csv
    ├── /Workflows
    │   ├── Joins.yxmd
    │   ├── HighRiskDiabetesPatients.yxmd
    ├── /Output
    │   ├── Diabetes.yxdb        # Output from 'Joins' workflow

