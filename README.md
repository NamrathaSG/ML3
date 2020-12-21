# Cubic Zirconia 

## Problem Statement 

You are hired by a company Gem Stones co ltd, which is a cubic zirconia manufacturer. You are provided with the dataset containing the prices and other attributes of almost 27,000 cubic zirconia (which is an inexpensive diamond alternative with many of the same qualities as a diamond). The company is earning different profits on different prize slots. You have to help the company in predicting the price for the stone on the bases of the details given in the dataset so it can distinguish between higher profitable stones and lower profitable stones so as to have better profit share. Also, provide them with the best 5 attributes that are most important.

## Exploratory Data Analysis

Loading the data file, we see that the first column is a serial number and we drop the column. Then looking at duplicates we see that there are 34 duplicate rows so we remove them. Now shape of our data frame is 26,933 x 10.
Out of 10 data fields, cut, color and clarity are categorical variables. All others are continuous variables. Analysing the continuous variables, we see that depth and carat seem to have more outliers than the others. 

Going by definition of Skewness:
Fairly Skewed (between -0.5 and 0.5).
Moderately Skewed (between -1 and – 0.5 or between 0.5 and 1).
Highly Skewed (less than -1 or greater than 1). None of them seem to be highly skewed.
Fairly Skewed: length and depth
Moderately Skewed: table
Highly Skewed: carat, width, height and price
Mean and median are pretty close to each other except for price column.
Going by definition of Kurtosis (Normal distribution has a Kurtosis of 3 and Kurtosis value higher than 3 means the distribution has a thicker tail than a normal distribution), we see that carat, table, length and price are normally distributed. Depth, width and hight have thicker tails.
A box plot of all the continuous variables are done after treating for outliers and Null values. Outlier treatment is done only for the independent variables. Outlier treatment is done so that values above upper range is set to the upper whisker and values below the lower range is set to lower whisker. Feature Depth has Null/NAN values. So treated NaN values with median because the column is treated for outliers. If we treat a column for outliers, the mean of that feature gets affected based on how bad the outliers are. So, we set NaN values with Median. 

## Missing Value Treatment 

There are few records 2 records with length zero, 2 records with width zero and 8 records with height zero. Since we are talking about length, width and height of cubic zirconia, these values seem to be bad/error data. Since there are very few records, we can safely drop these records.
There are null values only in “depth” field. Since we have treated depth column for outliers, we impute NaN values with Median value of depth column. There are 697 rows in depth column with null values that will be imputed with median value.
Yes. Feature scaling is required since we have different units in independent variables. Carat is in weight and length/width/height are in mm. Also, the model learned weights/coefficients (Beta Coefficients) will depend on the magnitude of the feature. By bringing all features to the same scale, we eliminate the problem of weights depending on the magnitude of the value and will be able to interpret the model better.
Also, we are going to apply Linear Regression on this data set. Linear Regression uses Gradient Descent to converge. With scaling, convergence will be faster.
After all clean up, we are left with a data frame of shape 26,925 x 10 

## Inference and conclusions:

From the above analysis, we infer the following:
1. Adjusted R Square and RMSE are about the same for both Train and Test data sets. So we can say that there is no
over/under fitting of the model.
2. R square value indicates 91.8% percent of variation in the target variable (Price) is explained by 7 predictors in the
model. Carat, Color, Cut, Clarity, Depth, Table and Length.
3. Among these 7 predictors, based on the coefficient values OLS Regression Results, Carat and Length are the top
two predictors. Clarity and Color are the next two good predictors. Depth, Table and Cut do not affect the price of
cubic zirconia very much.
4. The 5 best attributes that can predict the price of the stone are Carat, Length, Width, height and Clarity.
5. Adjusted R-squared penalizes the model for the inclusion of predictors. But in our out put we see that R Square
and Adjusted R Square are the same. From this we can infer that the 7 predictors that we have selected are actually useful and none of them are useless. If any of them were useless then R Square would have a higher value than Adj. R Square.
6. Point made in #4 above is confirmed by looking at p-value for each of the predictors. The p-value for each predictor tests the null hypothesis that the coefficient is equal to zero (no effect). A low p-value (< 0.05) indicates that you can reject the null hypothesis. In other words, a predictor that has a low p-value is likely to be a meaningful addition to our model.
7. We can recommend Gem Stones co ltd. to mainly focus on Carat and length/width/height of the gem stone to increase/decrease price of the stone.
8. We can recommend Gem Stones co ltd. to ignore too much focus on Cut, Depth and Table of the gem stone to try to change price of gem stone.
9. Since the data is scaled, the intercept of the model is 0.002 which is expected. But is not useful in our case.
