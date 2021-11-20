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

We use the Transbig Dataset to predict the survival function for distant metastasis in breast cancer patients using survival analysis and combined regression strategies. 


## Dataset

* The data from `TRANSBIG` validation study of 198 patients is used to perform the analysis.
* In TRANSBIG, the datasets `Patient Characteristic and Diagnostic Details`, and `Gene Features` are joined.
* Patient Characteristic and Diagnostic Details contains the clinical information of the patients.
* The observations in this dataset are censored, in the sense that for some units the event of interest has not occured at the time the data was analyzed or collected.
* Gene Features dataset contains the information of 22283 genes features of the patients.

 
## What is Survival Function?

By definition survival function is a function that gives the probability that a patient will survive beyond any specified time. 
Mathematically, if T is a continuous random variable with pdf f(t) and cdf F(t). Then the probability that the patient suffered distant metastasis by time duration t is nothing but the survival function. 

![image](https://user-images.githubusercontent.com/50804314/140692638-e80749d1-3662-4d80-9b99-a638ab61483b.png)

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
MA691-COBRA-3
|
└───README.md
|   
│
└───Documentation  // TRANSBIG Dataset README and other documentations
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

## References
1. Biau, Gérard, et al. "COBRA: A combined regression strategy." Journal of Multivariate Analysis 146 (2016): 18-28.

2. Hikichi, Shiori, Masahiro Sugimoto, and Masaru Tomita. "Correlation-centred variable selection of a gene expression signature to predict breast cancer metastasis." Scientific reports 10.1 (2020): 1-8.

3. Wang, Yixin, et al. "Gene-expression profiles to predict distant metastasis of lymph-node-negative primary breast cancer." The Lancet 365.9460 (2005): 671-679.

4. Ishwaran, Hemant, et al. "Random survival forests." The annals of applied statistics 2.3 (2008): 841-860.

5. Desmedt, Christine, et al. "Strong time dependence of the 76-gene prognostic signature for node-negative breast cancer patients in the TRANSBIG multicenter independent validation series." Clinical cancer research 13.11 (2007): 3207-3214.

6. [Hazard Function](https://www.statisticshowto.com/hazard-function/)

7. [Survuval Analysis](https://en.wikipedia.org/wiki/Survival_analysis)
 
8. [Hazard and cumulative hazard plotting](https://www.itl.nist.gov/div898/handbook/apr/section2/apr222.htm)

9. [Intuition for cumulative hazard function](https://stats.stackexchange.com/questions/60238/intuition-for-cumulative-hazard-function-survival-analysis/138185)
