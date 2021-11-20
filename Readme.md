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
<ul>
 <li> observed covariates
 <li> time-to-event(s),
 <li> a label indicating the type of event (e.g., deathor adverse clinical event) including right-censoring.  
</ul>


## Survival Function
![image](https://user-images.githubusercontent.com/8698342/142727652-206130ee-f98b-4c30-9168-39a808b2ebe0.png)


## Implementation of Predictive Models
Multiple ML Models are applied to predict the survival function:
<ul>
 <li> Support Vector Machine (svm.SVC)
 <li> KNeighborsClassifier
 <li> DecisionTreeClassifier
 <li> Gaussian Naive Bayes
 <li>  LinearDiscriminantAnalysis
</ul>

In addition to this, we also implemented Random Survival Forest to predict the survival function in two ways. 
* Using the python library `Random Survival Forest`
* Native Implementation by defining Indicator variables for various values of `t`, and using Regression models to predict these, and calculating survival function as in above formula. 

## COBRA Implementation and Results

Cobra implementation is done from scratch by defining a class in python and using various models to combine them through voting. 

Applying Random Survival Forest yielded an `R^2` value of 0.65. Later, applying Cobra increased the `R^2` value to 0.77. 

In addition to `R^2` analysis, the survival function is plotted against the time in days, and it agrees with the mathematical behavior and python implementation of Random Survival Forest.

COBRA:

![image](https://user-images.githubusercontent.com/14922339/140705220-c430000f-347f-434d-97aa-869ecc019812.png)

<!-- ![image](https://user-images.githubusercontent.com/50804314/140694209-2c29fe58-440c-408d-aa9f-b3fdf2fd473f.png)
 -->
Random Survival Forest:

![image](https://user-images.githubusercontent.com/14922339/140705401-5f681711-289d-4c77-8a47-db3c9a146355.png)



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

