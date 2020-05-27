---
title: Building an ML Classifier!
date: '2020-05-25'
spoiler: A KNN Classifier for Predicting Breast Cancer.
---

Hey there, based on my predictions, I believe you are in either of these 3 categories;
* A beginner / novice about Machine Learning or even programming
* You have an 'okay' knowledge of programming, but maybe not deeply into ML
* You have some sort of experience in Programming / Machine Learning.🙌

In this project, I will be using several Python libraries to make a K-Nearest Neighbor classifier that is trained to predict whether a patient has breast cancer. Guess what else? It classifies it as "Malignant" or "Benign"

In case you want to setup your local machine  [Click here](https://medium.com/@GalarnykMichael/install-python-on-windows-anaconda-c63c7c3d1444).

Alright let's get to it already!

---

First Let’s begin by importing the breast cancer data from `sklearn`
Our goal is to import the function `load_breast_cancer` from `sklearn.datasets`

Then, load the data into a variable called `breast_cancer_data` and set it equal to the function `load_breast_cancer()`
You should have this



---
## Next, an important question is what are we trying to classify? Let’s print both
--
`breast_cancer_data.target` and `breast_cancer_data.target_names`
--
Note: `target`gives you the labels of every data point (with `0` as the first) & `target_names` showa that `0` corresponds to malignant, and `1` to benign 

---

