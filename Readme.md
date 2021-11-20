# Dynamic Cobra Survival Analysis - DeepLearning and Statistical Methods

## Contents
1. Objective
2. Dataset
3. Survival Function
4. Survival Machines
5. COBRA Implementation
7. Directory Structure
8. References

## Objective

In this project,we analyse the CF dataset which is a longitudinal data which was collectedby the UK Cystic Fibrosis Registry.  We use multiple regression strategies topredict the survival function and then employ COBRA to combine all thesemethods to predict the survival function. 


## Dataset

* The Longitudnal dataset from `UK Cystic Fibrosis Registry`  of 312 patients measured across 16 different time intervals.
* This time-to-event (survival) dataprovides three pieces of information for each subject:  
<ol>
 <li> observed covariates
 <li> time-to-event(s),
 <li> a label indicating the type of event (e.g., deathor adverse clinical event) including right-censoring.  
</ol>


## Survival Function
![image](https://user-images.githubusercontent.com/8698342/142727652-206130ee-f98b-4c30-9168-39a808b2ebe0.png)


## Survival Machines
Multiple ML Models are applied to predict the survival function:
<ul>
 <li> KMF : Kaplan-Meier (KM) Function
 <li> Dynamic-DeepHit  is  a  multi-task  RNN based network
 <li> Random survival forest (RSF) an ensemble of trees
 <li> Cox-Time : Time-varying covariance
 <li> Multi-Task Logistic Regression (MTLR) 
</ul>


## COBRA Implementation and Results

Cobra implementation is done from scratch by defining a class in python and using various models to combine them through voting. 

Applying Random Survival Forest yielded an `R^2` value of 0.65. Later, applying Cobra increased the `R^2` value to 0.77. 

In addition to `R^2` analysis, the survival function is plotted against the time in days, and it agrees with the mathematical behavior and python implementation of Random Survival Forest.

COBRA:
Using the above machines we obtain survival functions which measures prob-ability of patient surviving after a given time 'τ'.
It is a cumulative probabilitymeasure used in most of the survival analysis methods.  We create a pickledictionary to store values of survival function at pre-defined eventtimes foreach of '312' patients which can be used to make prediction.  Thus we get anarray of '312 * 113' prediction i.e Patients x Times.
![image](https://user-images.githubusercontent.com/8698342/142727839-9f3a9d1c-5160-4410-bf8c-4033498176ed.png)
![image](https://user-images.githubusercontent.com/8698342/142727846-80daa29e-8b04-4bd1-89cb-5468ba543ccd.png)

## Directory Tree:

```
MA691-COBRA-5
|
└───README.md
|   
│
└───Papers //   Papers utilized for understanding related concepts and References
|
│
└───Data
│   │   GSE7390_family.soft.gz    // TRANSBIG Dataset
│   │   cleaned_data.csv          // Cleaned Data with all patient characterstics and gene features 
│   │   gene.csv                  // List of 76 most important genes to analyze time to distant metastasis
|   |   selected.csv              // Subset of cleaned data containing only 76 important gene features and patient characteristics
│      
└───Literature   // Various research papers that we used and implemented in our work
│   
│   
└───Notebooks
|   │   cobra.ipynb            // COBRA Implementation 
|   │   data_cleaning.ipynb    // Cleaning and extracting relevant data from TRANSBIG zip
|   │   indicators.ipynb       // Native Implementation to predict Survival Function
|   │   regression.ipynb       // Application of various regression models to predict time to distant metastasis
|   │   survival.ipynb         // Application of Random Survival Forest of Scikit-learn
|
|
└───Scripts
|   │   cobra_estimator.py     // Definition of Cobra Class
|   │   data_clean.py          // Script to extract, clean and save relevant data in a new csv file
|   │   main.py                // Main script which calls the COBRA model
|   │   random_survival.py     // Script that runs in-built Random Survival Forest 
|
```

