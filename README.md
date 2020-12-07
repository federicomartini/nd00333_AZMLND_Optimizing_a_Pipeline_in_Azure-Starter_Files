# Optimizing an ML Pipeline in Azure

## Overview
This project is part of the Udacity Azure ML Nanodegree.
In this project, we build and optimize an Azure ML pipeline using the Python SDK and a provided Scikit-learn model.
This model is then compared to an Azure AutoML run.

## Summary
**In 1-2 sentences, explain the problem statement: e.g "This dataset contains data about... we seek to predict..."**

This dataset contains data about bank customers with all the features we can use to make predictions. The goal is to predict if a customer is eligible for a loan. Thus, we have to deal with this problem with a classification algorithm, because we have to predict a discrete value that, in this case, admit two values (binary): eligible for a loan, or not eligible for a loan.

The feature we had in the dataset were: age, job, marital, education, default, housing, loan, contact, month, day_of_week, duration, campaign, pdays, previous, poutcome, emp.var.rate, cons.price.idx,cons.conf.idx, euribor3m, nr.employed, y (this last parameter contains the result of the prediction with a yes/no based on if the customer is considered eligible or not for a loan).

To solve this problem and provide the best prediction, we have taken advantage of **HyperDrive** to automatically tune the hyperparameters for a given algorithm. Then, we have taken advantage of **AutoML** and we have compared the outcomes of the two methods.

**In 1-2 sentences, explain the solution: e.g. "The best performing model was a ..."**

The best performing model in these experiments was the **VotingEnsemble** found by **AutoML** which reached an accuracy of **0.91654**

## Scikit-learn Pipeline
**Explain the pipeline architecture, including data, hyperparameter tuning, and classification algorithm.**

The Scikit-learn Pipeline implemented to find the best predictor for the customers elibigle to take a loan goes through the steps below:
* Get the dataset from the **CSV file** available [here](https://automlsamplenotebookdata.blob.core.windows.net/automl-sample-notebook-data/bankmarketing_train.csv).
* Clean data in the dataset and apply the **One Hot Encode** to transform data into numeric format so that they can be used in an algorithm.
* Split **train** and **test** data in two dataset following the classic rule 80:20 (80% for the training and 20% for the tests).
* Use the train dataset to feed the **LogisticRegression** algorithm (taking advantage of the Scikit-Learn library).
* Apply two hyperparameters to the **LogisticRegression**, that are:
  * **--C**: Inverse of the regularization strength. Smaller values cause stronger regularization [0.05, 1]
  * **--max_iter**: Maximum number of iterations to converge [20; 40; 60; 80; 100; 1000]
* Take advantage of **Hyperdrive** to automatically tune the hyperparmeters within the admitted ranges passed in inputs to the **LogisticRegression** to find the best predictor.

Below is the best predictor found after completing the training phase described above:

![](Images/HyperDrive_BestRun.PNG)


**What are the benefits of the parameter sampler you chose?**

**What are the benefits of the early stopping policy you chose?**

## AutoML
**In 1-2 sentences, describe the model and hyperparameters generated by AutoML.**

## Pipeline comparison
**Compare the two models and their performance. What are the differences in accuracy? In architecture? If there was a difference, why do you think there was one?**

## Future work
**What are some areas of improvement for future experiments? Why might these improvements help the model?**

## Proof of cluster clean up
**If you did not delete your compute cluster in the code, please complete this section. Otherwise, delete this section.**
**Image of cluster marked for deletion**
