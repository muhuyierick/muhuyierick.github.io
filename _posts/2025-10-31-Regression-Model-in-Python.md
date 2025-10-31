---
layout: post
title: "Regression Modelling in Python"
date: 2025-10-31
categories: [regression-modeling, python, data-exploration, data-cleaning]
author: Muhuyi Erick
---

## Introduction

This post describes a small regression project completed as part of the "Data and AI" program by Cyber Shujaa. The work shows how I explored a few small datasets, selected a suitable one for a simple linear regression model, trained the model, evaluated its performance, and visualized the results. The write-up explains each step in plain English so readers with basic Python knowledge can follow along.

## Project overview

The goal of this project was to build a simple linear regression model that predicts home prices from the house area. I started with three CSV files containing small example datasets. I read these files into pandas DataFrames, inspected their structure and contents, and then decided which dataset was most suitable for a single-feature linear regression. After selecting the dataset, I split it into training and test sets, trained a scikit-learn LinearRegression model, measured standard error metrics, and plotted the predicted regression line against actual test points.

## Step 1 — import required libraries

The first step is to import the Python libraries required for working with data, building models, and drawing charts. I used `pandas` for reading CSV files and managing tabular data, `numpy` for basic number operations, `scikit-learn` for the regression model and evaluation metrics, and `matplotlib` for plotting charts. Importing these libraries sets up the environment so the rest of the notebook can use standard functions for training and evaluating the model.

## Step 2 — load the datasets

I loaded three CSV files into pandas DataFrames: `areas.csv`, `homeprices-m.csv`, and `homeprices.csv`. Each CSV represents a small example dataset. Loading data into DataFrames lets us preview rows, compute summary statistics, and check for missing values easily before deciding which dataset to use for modeling.

## Step 3 — explore the data

After loading the data, I displayed the first few rows of every DataFrame to get a feel for the structure and values. I also checked for missing values and printed descriptive statistics such as mean and standard deviation. This exploration showed that `df_homeprices` contains two columns (`area` and `price`) with no missing values and therefore fits the simple linear regression setup (one input feature and one target). The other datasets either contained more features or missing values, which make them better suited for multiple regression or extra cleaning.

## Step 4 — visualize relationships

To better understand the relationship between area and price, I plotted scatter charts. One plot compared area vs. price for `df_homeprices` and another for `df_homeprices_m`. Scatter plots let you quickly see whether a roughly linear relationship exists between the feature and the target; in our case `area` and `price` appeared related enough to try a linear model on `df_homeprices`.

## Step 5 — choose the dataset for modeling

From the exploration and plots, I selected `df_homeprices` because it has a single input column `area` and a target column `price`. This makes it the most suitable for a straightforward linear regression example. The selection is also practical: with one feature the model is easy to explain and visualize.

## Step 6 — prepare the chosen dataset

Before training, I performed a final missing-value check on the selected DataFrame and then separated the inputs and the target. The input (features) is the `area` column and the target is the `price` column. Because scikit-learn expects a 2D array for features, I kept `X` as a DataFrame with a single `area` column and `y` as a Series of prices. Then I split the data into a training set and a test set using an 80/20 split. Because the original dataset is very small (5 rows), the resulting test set had only one data point, which is an important limitation when interpreting evaluation metrics.

## Step 7 — train the linear regression model

I used scikit-learn's `LinearRegression` class to create a simple linear model and trained it on the training data with the `fit` method. The model learns two parameters: the slope and the intercept, which together define the straight line that best fits the training data in the least-squares sense.

## Step 8 — evaluate model performance

To measure how well the model predicts prices, I used standard regression metrics: Mean Absolute Error (MAE), Mean Squared Error (MSE), Root Mean Squared Error (RMSE), and R-squared (R²). MAE gives the average absolute difference between predicted and actual values, MSE squares those differences and averages them (which penalizes larger errors more), and RMSE is the square root of MSE, giving error in the same units as the target (USD in this case). R² describes how much of the target variance the model explains compared with a simple mean predictor.

Because the test set contains only one data point, R² cannot be calculated reliably and will return `nan` (Not a Number). The numerical results shown in the notebook reflect the small dataset: MAE and RMSE are large relative to the price scale, indicating prediction errors are substantial for this tiny sample. The key takeaway is that with very few data points the evaluation metrics are noisy and not robust — a larger dataset is needed for trustworthy model assessment.

## Step 9 — visualize predictions

Finally, I plotted the test points and the regression line learned from the training data. Showing the regression line together with actual points helps visualize where the model predicts relative to the true prices. With such a small dataset the visualization confirms the model fits the training data but the single test point does not provide a strong validation of generalization.

## Data analysis and important observations

The notebook includes a short analysis and summary. It notes the sizes and characteristics of each CSV: `df_areas` had only an `area` column, `df_homeprices-m` had multiple features and a missing value, and `df_homeprices` had `area` and `price` with no missing data. Because `df_homeprices` only had 5 rows, the test split produced a single test sample and resulted in unreliable R². The error metrics (MAE, MSE, RMSE) are included in the notebook and are useful to inspect, but they should be treated cautiously because of the small sample size.

## Summary

This project is a compact demonstration of the end-to-end steps required to build a simple linear regression model in Python: import libraries, load and inspect data, visualize relationships, select a suitable dataset, split into training and testing sets, train a linear model, evaluate with standard metrics, and visualize the results. The main limitation here is the extremely small dataset, which prevents reliable evaluation and calls for more data collection or use of cross-validation techniques on larger samples. For production or more confident conclusions, use more records, consider feature engineering, and if multiple inputs exist, use multiple regression.

## Interactive Colab notebook

Run the full notebook interactively on Google Colab (click the link or paste it into your browser):

https://colab.research.google.com/drive/1I8bzIbeeq7laZaq0-vbtyUPqODLR94VM?usp=sharing

---
This project was completed as part of the "Data and AI" program by Cyber Shujaa. The course gave a practical framework to practice end-to-end model building and helped me understand what is needed for reliable model evaluation.
