# Dynamic Cobra Survival Analysis - DeepLearning and Statistical Methods

## Contents
1. Objective
2. Dataset
3. Survival Function
4. Survival Machines
5. COBRA Implementation
6. References

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


COBRA:
Using the above machines we obtain survival functions which measures prob-ability of patient surviving after a given time 'τ'.
It is a cumulative probabilitymeasure used in most of the survival analysis methods.  We create a pickledictionary to store values of survival function at pre-defined eventtimes foreach of '312' patients which can be used to make prediction.  Thus we get anarray of '312 * 113' prediction i.e Patients x Times.

Since  our  time  dimension  is  constant  we  iterate  on  our  event times  top erform Cobra Aggregation learning method which takes average of commonpoints within 'epsilon' range. Where 'epsilon'  is chosen to be most optimal at '10^−3'.  We perform Cobra Aggregation for each time step to get an cobraprediction dictionary with 'Patients x Time' dimension.

Results:
![image](https://user-images.githubusercontent.com/8698342/142727839-9f3a9d1c-5160-4410-bf8c-4033498176ed.png)
![image](https://user-images.githubusercontent.com/8698342/142727846-80daa29e-8b04-4bd1-89cb-5468ba543ccd.png)


## References

[1]  G ́erard  Biau,  Aur ́elie  Fischer,  Benjamin  Guedj,  and  James  D.  Malley.Cobra: A combined regression strategy.Journal of Multivariate Analysis,146:18–28, Apr 2016.

[2]  Frank  Emmert-Streib  and  Matthias  Dehmer.   Introduction  to  survivalanalysis  in  practice.Machine Learning and Knowledge Extraction,1(3):1013–1038, 2019.

[3]  H ̊avard Kvamme, Ørnulf Borgan, and Ida Scheel.  Time-to-event predic-tion with neural networks and cox regression, 2019.

[4]  Changhee  Lee,  Jinsung  Yoon,  and  Mihaela  van  der  Schaar.   Dynamic-deephit:  A  deep  learning  approach  for  dynamic  survival  analysis  withcompeting  risks  based  on  longitudinal  data.IEEE Transactions onBiomedical Engineering, 67(1):122–133, 2020.

[5]  Chun-Nam  Yu,  Russell  Greiner,  Hsiu-Chin  Lin,  and  Vickie  Baracos.Learning patient-specific cancer survival distributions as a sequence of de-pendent regressors. In J. Shawe-Taylor, R. Zemel, P. Bartlett, F. Pereira,and K. Q. Weinberger, editors,Advances in Neural Information Process-ing Systems, volume 24. Curran Associates, Inc., 2011.
