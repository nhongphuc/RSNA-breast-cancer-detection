# 

![alt text](
https://github.com/nhongphuc/RSNA-breast-cancer-detection/blob/main/TitlePic.png?raw=true)


The goal of this project is to diagnose breast cancer by training models on screening mammograms. We hope to help radiologists to be more efficient with the
diagnosis process.

## Data

The data comes from this Kaggle competition:
https://www.kaggle.com/competitions/rsna-breast-cancer-detection. 

## Data Wrangling

- We found that there are two kinds of mammograms: with a white background or with a black background, corresponding to two different photometric interpretations (MONOCHROME1 or MONOCHROME2). The two kinds also have different numbers of pixels. We converted all images to white background, and resized them to size (512,512).
- We found that 'view' has 6 values ('CC', 'MLO', 'ML', 'LM', 'AT', 'LMO'), but it should only take 2 values: 'CC' for the cranio-caudal view, and 'MLO' for the mediolateral oblique view. We fixed 'ML', 'LM' and 'LMO' to 'MLO' and deleted 'AT'.
- We dropped rows with missing data.
- We used get_dummies (one-hot encoding) to convert categorical columns to numerical columns.

## EDA

## Preprocessing

## Modelling

## Conclusion and future improvement
