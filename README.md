# Optimizing an ML Pipeline in Azure

## Overview

This project is part of the Udacity Azure ML Nanodegree.
In this project, we build and optimize an Azure ML pipeline using the Python SDK and a provided Scikit-learn model.
This model is then compared to an Azure AutoML run.

## Summary

### Problem Statement

Using the [Bank Marketing Dataset](https://automlsamplenotebookdata.blob.core.windows.net/automl-sample-notebook-data/bankmarketing_train.csv), the aim was to develop a prediction model for proper classification of clients' term subscription.

### Solution

The solution is to utilize two approaches to solve the classfication task using the Microsoft Azure `Hyperdrive ` and `AutoML` to train the dataset, the process will be explained below.

## Scikit-learn Pipeline

SKlearn is a robust library that features various classification, regression and clustering algorithms. In this classification task, the approach is as follow.

### Load Data

Using the `TabularDatasetFactory`, the bankmarketing dataset was loaded into the workspace.

### Data Processsing and Modeling

After loading the dataset, it needs to be processed, and the approach is using a fucntion `cleandata` to perform the preprocessing task. To preprocess the categorical features, one-hot encoding was done. Then next step splits the data into train and test sets, for the modelling task. To train the model, the logistic regression algorithm was used, which is an algorith, for a classification problem.
The Logisitc regression hyperparameters, `C & max_iter` were utilized.

**RandomParameterSampling**
The parameter sampler used is the `RandomParameterSampling`, a class that defines random sampling over a hyperparameter search space. The parameter values are choosen from a set of discrete values or a distribution over a continuous range. So this makes the computation less expensive.

**BanditPolicy**
`BanditPolicy`, an early termination policy which is based on `slack factor/slack amount` and `evaluation_interval`. If the primary metric is not within the specified ``slack factor/slack amount`, the policy terminates any runsm and this is done with respect to the best performing training run.

## AutoML

With an accuracy score of `91.7%`, the best model is `VotingEnsemble` classifer. After preprocessing, that is, spliting the data into train & test dataset, and concatenating the training data together. The automl config takes the training data, labelled data, cross validation is set to 5. For the model the stopping criteria is at iteration 50

## Pipeline comparison

The architecture for both model determined the model score for each algorithm. The model accuracy for the `hyperdrive` model is `91.5%` and the accuracy score for the AutoML is `91.7%`, which is an `0.2%` difference in metric score. The pipeline for hyperdrive didnot give the flexibility of exploring other algorithm, because after the preprocessing task, the data was passed into a classfication model - Logistic regression.

For the AutoML model, there is the flexilibilty of selecting the best training run out of others.

## Future work

For future work, it would be nice to explore more into the data, by carrying out data cleaning process and feature engineering activities. Accuracy is not the only evaluation metric process, it would also be nice to explore some other statistical evaluation metrics.

## Proof of cluster clean up

![cleanup](https://github.com/bleso-a/nd00333_AZMLND_Optimizing_a_Pipeline_in_Azure-Starter_Files/blob/master/cleanup.png)
