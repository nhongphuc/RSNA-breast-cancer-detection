# 

![alt text](
https://github.com/nhongphuc/RSNA-breast-cancer-detection/blob/main/TitlePic.png?raw=true)


The goal of this project is to diagnose breast cancer by training models on screening mammograms. We hope to help radiologists to be more efficient with the diagnosis process. In particular, we hope to achieve a false positive rate (FPR) lower than 25%, because false positives lead to unnecessary, costly medical procedures for the patient.

## Data

The data comes from this Kaggle competition:
https://www.kaggle.com/competitions/rsna-breast-cancer-detection. 

## Data Wrangling

- We found that there are two kinds of mammograms: with a white background or with a black background, corresponding to two different photometric interpretations (MONOCHROME1 or MONOCHROME2). The two kinds also have different numbers of pixels. We converted all images to white background, and resized them to size (512,512).
- We found that 'view' has 6 values ('CC', 'MLO', 'ML', 'LM', 'AT', 'LMO'), but it should only take 2 values: 'CC' for the cranio-caudal view, and 'MLO' for the mediolateral oblique view. We fixed 'ML', 'LM' and 'LMO' to 'MLO' and deleted 'AT'.
- We dropped rows with missing data.
- We used get_dummies (one-hot encoding) to convert categorical columns to numerical columns.

## EDA

- We saw that the median age of patients with cancer is higher than the median age of patients without cancer.
- We saw that patients with breast implant have a lower chance of getting breast cancer compared to patients without breast implant (but we think there is some confounding factor which explains this).
- We found that around 10% of patients have breast density A, around 43% have density B, around 42 % have density C, and around 5% have density D. The fractions we found are close to the distribution of breast density among the general population.

## Preprocessing

- We used the HOG method (histogram of oriented gradients) to devise features, instead of using the values of the pixels directly.
- Because the data is highly imbalanced (there are many more images without cancer than with cancer), we used a combination of undersampling and oversampling with SMOTE.
- We scaled the data with MinMaxScaler.
- We used 100 PCA components to train the models.

## Modelling
- We trained 3 models: a Logistic Regression one, a Random Forest one, and a Boosted Gradient one.
- We used 5-fold cross-validation, with the following parameter searches:
* for Logistic Regression: 'C',
* for Random Forest: "min_samples_split", "max_depth", "criterion", "max_features", "bootstrap"
* for Gradient Boosting: "learning_rate", "learning_rate", "max_depth", "criterion", "max_features"
- We used the F1-score as the main performance metric.
- Logistic Regression has the best F1-score on the test data (0.64). The other two classifiers have mediocre F1-scores (0.26 and 0.35). So we choose Logistic Regression.
- We also looked at the ROC-AUC for Logistic Regression. The AUC is an excellent 0.91.
- We also plotted the FPR versus the threshold for Logistic Regression, and saw that for the standard threshold of 0.5, the FPR is lower than the desired 
value of 0.25.

![alt text](
https://github.com/nhongphuc/RSNA-breast-cancer-detection/blob/main/LogRegROC.png?raw=true)

## Conclusion and future improvement
The Logistic Regression classifier suits our needs best. Future improvements include using more images to train models (had we used more images in our analysis, we would have run into memory issues with the Kaggle kernel), a more thorough hyperparameter search, as well as using neural networks.
