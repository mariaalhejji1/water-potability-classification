# Water Potability Classification Using Machine Learning

An end-to-end Machine Learning classification project designed to automate the assessment of drinking water safety based on its physicochemical properties. This project evaluates multiple predictive models, handles data quality deficiencies, and deploys the optimal predictive architecture as an interactive web application to support rapid screening of water quality.

## Project Overview and Problem Statement
Access to safe drinking water is a critical public health concern and a key sustainability priority. Traditional laboratory testing of water quality is often time-consuming, expensive, and inaccessible in remote areas. 

This project addresses the challenge by leveraging data-driven classification algorithms to analyze measurable water attributes such as pH, hardness, solids, chloramines, sulfate, conductivity, organic carbon, trihalomethanes, and turbidity. By training algorithms to recognize patterns within these attributes, the system provides a fast, scalable, and cost-effective screening tool for water safety assessment.

## Tech Stack and Core Components
* Programming Language: Python
* Framework for Deployment: Streamlit
* Core ML Libraries: Scikit-Learn, Pandas, NumPy
* Visualizations: Matplotlib, Seaborn
* Model Preservation: Joblib
* Execution Environments: Google Colab, Jupyter Notebook

## Data Engineering and Exploratory Data Analysis
The dataset contains 3276 water samples characterized by 9 continuous numerical features and a binary target variable (Potability). The data engineering workflow involved:
1. Missing Value Imputation: Handled missing entries in pH (491), Sulfate (781), and Trihalomethanes (162) columns by applying mean imputation to maintain data distributions.
2. Outlier Treatment: Identified extreme statistical anomalies across all continuous attributes using box plots. Values exceeding the Interquartile Range boundaries ($Q1 - 1.5 \times IQR$ and $Q3 + 1.5 \times IQR$) were capped at the respective statistical limits.
3. Class Imbalance Resolution: Addressed severe class skewness (approximately 2000 non-potable vs 1250 potable records) by implementing Synthetic Minority Over-sampling Technique (SMOTE) to balance the target classes during training.

## Data Pipeline and Model Architectures
The analytical pipeline evaluates four distinct classification architectures split into an 80/20 train-test ratio:
* Random Forest Classifier: An ensemble tree method selected to capture non-linear feature interactions and reduce overfitting.
* Support Vector Classifier (SVC): Evaluated with MinMax data scaling to maximize hyperplane margin separation.
* K-Nearest Neighbors (KNN): A distance-based instance classifier utilizing spatial proximity for local classification.
* Decision Tree Classifier: An interpretable hierarchical structure selected for baseline modeling and feature traceability.

## Model Performance and Hyperparameter Tuning
Hyperparameters were systematically optimized through 5-fold cross-validation using GridSearchCV. Model training revealed distinct patterns of overfitting in default tree architectures and underfitting in unscaled support vector baselines, which were successfully corrected.

### Experimental Evaluation Matrix
* Random Forest (Default): 69.25% Accuracy
* Random Forest (Tuned): 71.13% Accuracy (Optimal Model)
* Support Vector Classifier (Default): 51.25% Accuracy
* Support Vector Classifier (Tuned and Scaled): 68.14% Accuracy
* K-Nearest Neighbors (Default): 60.75% Accuracy
* K-Nearest Neighbors (Tuned): 62.13% Accuracy
* Decision Tree (Default): 60.00% Accuracy
* Decision Tree (Tuned): 59.38% Accuracy

## Interactive Web Deployment and Live Demo
The optimal Random Forest model was exported as a serialized payload using Joblib and integrated into a production environment. 

The interactive web interface utilizes numerical input widgets for real-time customer data entry, processes inputs against the saved model metrics, and generates an instantaneous water classification label accompanied by intuitive color coding for seamless user experience.

### Live Application Link
You can access and test the deployed model in real-time here: [Live Water Potability Prediction Web App](https://waterpotabilityapp-bkeisfzx2wf8bhgg5pptdx.streamlit.app/)

### Web Application Interface Previews

Dashboard Preview - Safe / Potable Water Classification:
<img width="663" height="938" alt="Screenshot 2026-07-04 044637" src="https://github.com/user-attachments/assets/b72bd1aa-a36b-43b3-be88-7c2007de68d1" />

Dashboard Preview - Unsafe / Non-Potable Water Classification:
<img width="677" height="943" alt="Screenshot 2026-07-04 044301" src="https://github.com/user-attachments/assets/fa3791ca-228e-4f6a-ba07-72edefa35a3f" />

## AI Ethics and Responsible Development
This project incorporates critical ethical standards based on corporate and public safety frameworks:
* Reliability and Safety: Evaluation focus was directed toward minimizing False Negatives (unsafe water falsely classified as potable), as hidden water contamination represents a direct threat to human health.
* Privacy: The analytical dataset complies with modern privacy principles as it contains only environmental and physicochemical properties, with zero personal metadata exposure.
* Transparency: Interpretability metrics including Random Forest feature importance maps and Decision Tree paths allow engineers to trace classification results.
* Human Oversight and Limitations: The deployed model is clearly framed as a statistical screening support tool and does not substitute for certified chemical and laboratory evaluation.
