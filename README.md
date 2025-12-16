## Building a DDoS Anomaly-Detect Pipeline (detect malicious traffic)

Recently, I worked on a side task, an anomaly-detection project, which I focused on detecting DDoS traffic in a large network dataset (approx 250k records and 79 features) with two classes: Benign (97686) vs DDoS (128025)

What I did: 
  - Data Cleaning
  - Dimensionality reduction: to reduce noise and improve model performance. 
  - Modelling approaches:
      - Gaussian anomaly detection (multivariate Gaussian with threshold tuned using F1 score )
      - SVM baseline classifier
    
These are the lessons I learnt from the project. 
One result surprised me about preprocessing:
  - When I applied PCA on the unstandardized dataset, only 6 components captured about 99.4% of the variance
  - After standardizing/scaling the dataset, PCA needed 27 components to have a similar variance level. 
Point: feature scaling can reshape the variance structure, which directly impacts the number of PCA components required. 

What I learned about Gaussian anomaly detection
I implemented Gaussian anomaly detection by:
  - estimated mean and variance from the training set, 
  - computed probabilities using a multivariate Gaussian,
  - selected anomaly threshold (epsilon) that maximises F1. 
Point: When the anomalies are not rare or are close to the normal cases, Gaussian performs poorly because it uses mean / variance

SVM (baseline)
I tested an SVM approach and evaluated it using ROC_AUC and classification performance metrics. 
The model performed strongly better, and SVM is a reliable baseline for datasets with large features. 

#MachineLearning #Cybersecurity #AnomalyDetection #DataScience #Python
