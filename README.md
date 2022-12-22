# predicting-titanic-survivors
Predicting titanic survivors using Random Forest.
# Normaliaztion
## Age
For column 'Age' there are some float numbers which would be a problem while filling the missing values. Therefore, I've converted them to int.
## Title 
I take titles from names and counted each value on train set:
| Title  | Value Count |
| ------------- | ------------- |
| Mr            |   517
| Miss          |   182
| Mrs           |   125
| Master        |    40
| Dr            |     7
| Rev           |     6
| Mlle          |     2
| Major         |     2
| Col           |     2
| the Countess  |     1
| Capt          |     1
| Ms            |     1
| Sir           |     1
| Lady          |     1
| Mme           |     1
| Don           |     1
| Jonkheer      |     1

As you can see there are a lot of single values. So, we should normalize them and merge some of them:

| Title  | Value Count |
| ------------- | ------------- |
| Mr            |   240
| Miss          |   78
| Mrs           |   72
| Master        |   21
| Col           |   2
| Rev           |   2
| Ms            |   1
| Dr            |   1
| Dona          |   1

# Missing Values
## Encoding
I've had encoded binary comlomns like Age, Title and Embarked. Result will be like table below:

| Sex_male  | Emabarked_Q | Embarked_S |	Title_Miss |	Title_Mr |	Title_Mrs |	Title_Officer |	Title_Royal |
| --------- | ------------| ---------- | ----------- | --------- | ---------- | ------------- |  ---------- |
| 1 |	0 |	1 |	0 |	1 |	0 |	0 |	0
|	0	| 0 |	0 |	0 |	0 |	1 |	0 |	0
|	0 |	0 |	1 |	1 |	0 |	0 |	0 |	0
|	0	| 0 |	1 |	0 |	0 |	1 |	0 |	0
|	1	| 0 |	1 |	0 |	1 |	0 |	0 |	0

## MinMaxScaler 
The MinMaxscaler is a type of scaler that scales the minimum and maximum values to be 0 and 1 respectively. While the StandardScaler scales all values between min and max so that they fall within a range from min to max.
|	PassengerId |	Pclass |	Age |	SibSp |	Parch |	Fare |	Sex_male |	Embarked_Q |	Embarked_S |	Title_Miss |	Title_Mr |	Title_Mrs |	Title_Officer |	Title_Royal |
| ----------- | ------ | ---- | ----- | ----- | ---- | --------- | ------------| ---------- | ----------- | --------- | ---------- | ------------- |  ---------- |
|	0.000000 |	1.0 |	0.2750 |	0.125 |	0.0 |	0.111538 |	1.0 |	0.0 |	1.0 |	0.0 |	1.0 |	0.0 |	0.0 |	0.0
|	0.001124 |	0.0 |	0.4750 |	0.125 |	0.0 |	NaN |	0.0 |	0.0 |	0.0 |	0.0 |	0.0 |	1.0 |	0.0 |	0.0
|	0.002247 |	1.0 |	0.3250 |  0.000 |	0.0	| 0.121923 |	0.0 |	0.0 |	1.0 |	1.0 |	0.0 |	0.0 |	0.0 |	0.0
|	0.003371 |	0.0 |	0.4375 |	0.125 |	0.0 |	0.816923 |	0.0 |	0.0 |	1.0 |	0.0 |	0.0 |	1.0 |	0.0 |	0.0
|	0.004494 |	1.0 |	0.4375 |	0.000	| 0.0 |	0.123846 |	1.0 |	0.0 |	1.0 |	0.0 |	1.0 |	0.0 |	0.0 |	0.0

## KNNImputer
The KNNImputer class provides imputation for completing missing values using the k-Nearest Neighbors approach. Each sample's missing values are imputed using values from n_neighbors nearest neighbors found in the training set. Note that if a sample has more than one feature missing, then the sample can potentially have multiple sets of n_neighbors donors depending on the particular feature being imputed.

Each missing feature is then imputed as the average, either weighted or unweighted, of these neighbors. Where the number of donor neighbors is less than n_neighbors, the training set average for that feature is used for imputation. The total number of samples in the training set is, of course, always greater than or equal to the number of nearest neighbors available for imputation, depending on both the overall sample size as well as the number of samples excluded from nearest neighbor calculation because of too many missing features (as controlled by row_max_missing).

We we will fill the missing value with KNNImputer.

# Model
## Random Forest
Random forest, like its name implies, consists of a large number of individual decision trees that operate as an ensemble. Each individual tree in the random forest spits out a class prediction and the class with the most votes becomes our model’s prediction.
# Result
| | precision |   recall |  f1-score |  support |
| ----------- | ------ | ---- | ----- | ----- | 
|  0 |      0.86 |     0.87 |     0.86 |      266 |
| 1 |      0.77 |     0.75 |     0.76 |      152 |
| accuracy |  |   |                     0.83 |       418 |
| macro avg |      0.81 |     0.81 |     0.81 |      418 |
| weighted avg |       0.82 |     0.83 |      0.82 |      418 |

## Random Forest
Random forest is a supervised learning algorithm. It has two variations – one is used for classification problems and other is used for regression problems. It is one of the most flexible and easy to use algorithm. It creates decision trees on the given data samples, gets prediction from each tree and selects the best solution by means of voting. It is also a pretty good indicator of feature importance.

Random forest algorithm combines multiple decision-trees, resulting in a forest of trees, hence the name Random Forest. In the random forest classifier, the higher the number of trees in the forest results in higher accuracy.
# Dataset
I've used [this dataset](https://www.kaggle.com/competitions/titanic/data) for the project.
