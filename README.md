# Final Project

In this project, we focus on predicting sepsis, a medical condition where the immune system damages the body as a result of fighting infection. We introduce and replicate a Long Short-Term Memory (LSTM) neural network model that uses patient features from the Medical Information Mart for Intensive Care (MIMIC)-III dataset for early identification and prediction of sepsis, as defined by Sepsis-3. Ultimately, this report highlights the approach and results for sepsis prediction.


# Reproducing the above studies

This project uses scripts in the ETL folder to generate the cohort for the Sepsis-3 model then uses a RNN model following the script in Model to produce the predictive model. The ETL steps utilizes PySpark in a Google Cloud environment, while the script in the Model step can be executed on a a Google Colab environment. 
The data needed to run the model are saved in the Dataset folder, under the files: features_v1.csv (Trial #3) and sepsis3-df.xlsx

## Clone the repository

You will need a local copy of the code in this repository. The easiest way to acquire this is to use `git` to clone the data locally. 
```
git clone https://github.com/qasimnazir/LSTM-based-Sepsis-Prediciton.git

```
## Identify the Sepsis-3 patients
This study utilizes the steps set up by Alistar et. al to identify case and control patients for the sepsis-3 diagnosis. This step will ultimately generate a csv file that is similar to the sepsis3-df.xlsx file in the Datasets. 
Please follow the code instructions listed in this link: https://github.com/alistairewj/sepsis3-mimic
The main notebook used in the Alistar et. al study is the sepsis-3-get-data.ipynb note book. 

## ETL Google Cloud Dataproc

The output of the ETL steps is the feature_v1.csv file. 
To run the codes in the ETL folder you will need to set up a Google Cloud Project
Please follow the instructions from this medium article to set up a Google Cloud Environment
https://medium.com/google-cloud/apache-spark-and-jupyter-notebooks-made-easy-with-dataproc-component-gateway-fa91d48d6a5a

The ETL files are organized into 3 main features generation files:
- lab_features.ipynb -> generates the lab features for the model
- ClinicalFeatures.ipynb -> generates the clinical features of the model
- CohortDiagnosis.ipynb -> generates the cohort and diagnostic features for the model

Each of the ETL files utilizes concept creation scripts listed in: https://github.com/MIT-LCP/mimic-code/blob/master/concepts/README.md or resulting Derived Tables. The data are loaded into Google Cloud DataProc through Big Query or through a cluster from CSV downloaded from MIMICIII website. Set up MIMICIII on BigQuery follow : https://mimic.physionet.org/tutorials/intro-to-mimic-iii-bq/

The output of the 3 ETL files is then combined through Features.ipynb to generate **feature_v1.csv**


## RNN Predictive Model

Once the ETL steps are done, the output is **feature_v1.csv**. This columns in this dataframe is described in the "Features Checklist" excel file. This file consists of the cohort of patients to create the predictive Sepsis-3 model.
The results of the RNN model can be re-produced using the **feature_v1.csv** as input data and the Model script housed in the Model folder.

# Model Performance

![Confusion Matrix & AUC Curve](Model_Performance.PNG)

# Team Members
Hao Lee, Michael Hur, Qasim Nazir, David Wu

Original Repo: https://github.gatech.edu/hlee873/CSE6250_Team11.git
