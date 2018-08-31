+++
# Date this page was created.
date = 2016-04-27T00:00:00

# Project title.
title = "Fraud Analytics: Fraud Score Calculation"

# Project summary to display on homepage.
summary = "Fraud Analytics: Unsupervised Learning and Fraud Score Calculation on New York property tax."

# Optional image to display on homepage (relative to `static/img/` folder).
image_preview = "headers/newyork.jpg"

# Tags: can be used for filtering projects.
# Example: `tags = ["machine-learning", "deep-learning", "spatial-visualization"]`
tags = ["Unsupervised Machine Learning"]

# Optional external URL for project (replaces project detail page).
external_link = ""

# Does the project detail page use math formatting?
math = false

# Optional featured image (relative to `static/img/` folder).
[header]
image = "headers/newyork.jpg"
caption = "Fraud Analytics: Unsupervised Learning"

+++



##### Description
This report provides a detailed analysis of ‘New York City Property Tax Valuation Data’ and also aims at
identifying potential fraudulent records from the data set using unsupervised machine learning methods.
The programming tools used for Data Cleaning were performed on Microsoft Excel and R. The original
dataset contains unique records of more than 1 million properties across the state of New York with 30
different fields, both numerical and categorical. Necessary feature analysis include:
● Data Understanding and Data Cleaning (estimating missing values of each fields)
● Data Modeling (creating expert variables) and Data Evaluation
● Fraud Score Calculation (Heuristic Algorithm and Autoencoder)

##### Project Goal
Our objective for this project is to use machine learning algorithms such as Autoencoder and Heuristic
Algorithms and calculate a fraud score for each of the New York Property data records to analyze
anomalies for potential fraud detection. By applying both of the unsupervised machine learning
methods, records with high scores show to be potentially fraudulent. The report will explain each step in
complete detail.

##### Key Findings
The two fraud detection algorithms we used, Heuristic and Autoencoder-Based Anomaly Detection, had
a considerably high overlap matching percentage among the top 1% of all records:
● Missing values were properly filled using reasonable data cleaning methodology.
● The 51 expert variables were carefully crafted to perform PCA analysis.
● After normalizing the fraud scores and visualizing the scores, we found both score distributions
to be right skewed.
● Among the top 10 highest fraud score records, anomalies were found in several fields.

<a href="https://drive.google.com/open?id=1-UvdR-EvZEsEr-Fjv4qaMBiuqFKvYwbq" download>Click to Download the full report</a>
