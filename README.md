# INM706_Coursework

## Disease Prognosis Prediction using Longitudinal Electronic Health Records and Gated Recurrent Units

Dependencies:
Windows 10 Home 64-bit
Python: 3.8.7 (tags/v3.8.7:6503f05, Dec 21 2020, 17:59:51)
Numpy Version: 1.2.1
Pandas Version: 1.19.5
PyTorch Version: 1.7.1+cu110
Matplotlib Version: 3.3.3
Seaborn Version: 0.11.1

NOTE: I cannot upload the original MIMIC-III CSV files to GitHub or Moodle as per the privacy agreement. However, the main data extracted from from the CSVs during data preprocessing is uploaded after being pickled. You can start the code from the Preparation of data, labels section after importing the data.encoded_icd9s file.

TO RUN, IMPORT THE NECESSARY LIBRARIES AND RUN ALL THE FUNCTION AND CLASS CELLS STARTING FROM THE DATA PREPARATION SECTION AND THEN SKIP TO THE EVALUATION SECTION TO RUN A TEST ON THE MODEL

MIMIC-III is a large, freely-available database comprising deidentified health-related data associated with over 40,000 patients who stayed in critical care units of the Beth Israel Deaconess Medical Center between 2001 and 2012. The MIMIC-III Clinical Database is available on PhysioNet. Though deidentified, MIMIC-III contains detailed information regarding the care of real patients, and as such requires credentialing before access.

My goal is to attempt to predict future ICD9 (diagnosis) codes from patients using a GRU. The model can be found in the Model section and Results can be found in the training and evaluation sections. As we can see, the training and validation losses decrease well. However, we can see the model is overfitting, even with dropout layers etc. I focus on Recall results, but Accuracy, Precision and F1-Score were also computed for the train, test and validation sets. In general, the model achieved a very high recall score and a very low precision score. Since the context of this prediction is biomedical in nature, having a high recall is not necessarily bad since the benefit of a patient being told they may progress in a certain way outweighs the risk of a sudden disease onset with no warning. On the other hand, if the prediction is incorrect, this may have caused unnecessary panic and preparation.

Since each unique hospital visit for a patient is assigned a unique HADM_ID, the ADMISSIONS table can be considered as a definition table for HADM_ID.
Each row of this table contains a unique HADM_ID, which represents a single patient’s admission to the hospital. HADM_ID ranges from 1000000 - 1999999. It is possible for this table to have duplicate SUBJECT_ID, indicating that a single patient had multiple admissions to the hospital. The ADMISSIONS table can be linked to the PATIENTS table using SUBJECT_ID.

https://mimic.physionet.org/mimictables/admissions/ - info about admissions table
