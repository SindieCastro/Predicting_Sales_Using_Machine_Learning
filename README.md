<p align='center'>
    <img src=images/readme6.png width="1000" height="600">
</p>

# Predicting Sales Using Machine Learning

## Overview

The video games industry continues to grow at a rapid pace, and shows no signs of slowing down in the years to come. As a result, many companies want to be part of the growing revenue stream. 

A team of data analytics consultants, referred to as the "Red Team," has been tasked to transform data into information that provides profit-maximizing business insight for video game sales. To accomplish this task, the team will build and evaluate several ML models or algorithms (e.g.,Logistic regression, Neural Network). Using ML will enable the team to leverage existing algorithms to learn from the data and lead to more accurate predictions.

## Purpose

For this project, the team will analyze the potential profits for a video game launch in the European region. The team will build a predictive ML model to find patterns in existing and new sales data. Once the model is created, its performance will be evaluated to see how well it predicts the data. 

In addition, the team will attempt to market the algorithm to existing companies in the gaming sector or organizations looking to get involved in the industry.

## Resources

- <img src="https://github.com/get-icon/geticon/raw/master/icons/visual-studio-code.svg" alt="VScode" width="20px" height="25px"> VS Code

- <img src="https://github.com/get-icon/geticon/raw/master/icons/python.svg" alt="Python" width="25px" height="20px"> Python Libraries

- <img src="https://github.com/get-icon/geticon/raw/master/icons/postgresql.svg" alt="PostgreSQL" width="25px" height="25px"> PostgreSQL & pgAdmin

- <img src="https://maxgentechnologies.com/images/intern/python_machine_logo.jpg" width="px" height="25px"> Machine Learning 

- <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSLPEwocsaSWuRA1_rvsYXMsXCMzgSWVB956N1CKMQ&usqp=CAU" alt="Tableau" width="25px" height="20px"> Tableau Public  

- <img src="https://github.com/get-icon/geticon/raw/master/icons/javascript.svg" alt="JavaScript" width="25px" height="20px"> JavaScript

- <img src="https://brand.heroku.com/static/media/heroku-logotype-spacing-vertical.dc54b577.svg" alt="Heroku" width="30px" height="30px"> Heroku

## Reason for Topic Selection

Predicting video game sales was considered to be an interesting and fun topic to analyze. Video games have been around for many years and have evolved significantly over time. Game development is also becoming increasingly common in many organizations. It is also a huge market that provides entertainment for children and adults alike. 

## Data Description

A CSV dataset, named vgsales.csv, will be used for the analysis. The dataset contains 16,599 rows and the following columns: 

- Rank: The ranking of overall sales
- Name: The name of the games
- Platform: The platform of the games release
- Year: The year the game was released
- Genre: The genre of the game
- Publisher: The publisher of the game
- Sales (NA, EU, JP, Other, Global): Sales in North America, Sales in Europe, Sales in Japan, Sales in the rest of the world, and Total worldwide sales

## Project Question

**Will sales in Europe be greater than the target revenue?**


## Machine Learning Model

#### Description of data preprocessing

The data was initially explored to determine which columns to keep as features and which columns to drop. The following are the columns dropped and retained for analysis.

- Dropped columns: Name, Year, Publisher, Other_Sales, Global Sales.
- Retained columns: Platform, Genre, NA_Sales, EU_Sales, JP_Sales

The columns Name and Publisher were dropped due to a large number of unique values and not very useful for the ML model. The Global_Sales column was dropped because it is a sum of the regional sales numbers. The team debated whether or not to keep Other_Sales column, but ultimately it was dropped. The Other_Sales column represented all sales outside of NA, EU, and JP, and the team felt that in a real-world application, this data would likely not be available prior to launching a video game in a major market. The data that was kept for analysis was reviewed for null values. Fortunately, no null values were found, so the team proceeded with the analysis.

#### Description of feature engineering and feature selection, including their decision-making process

The team strategically selected which columns to drop and keep to properly train the ML model. The features to make the prediction and target to predict the outcome changed from the original mockup model. The string columns were encoded into numerical values. Scaling was explored with the sales data, but it was found that scaling did not improve the accuracy of the ML model. The team believes this could be due to the heavily skewed distribution of the sales data as indicated by the EU_Sales histogram below. Further investigation is required.

#### Histogram of EU_Sales
![EU_Sales_histogram.PNG](images/EU_Sales_histogram.png)

#### Sales Data Columns
![sales_data.PNG](images/sales_data.png)

#### Total Regional Sales
![sales_all_locations2.PNG](images/sales_all_locations2.png)

#### Description of how data was split into training and testing sets

The target data was segregated from the feature data, and these two datasets were split into the training and testing sets using the *train_test_split* method built into scikit-learn as shown below.

![ML_train_test_split](https://user-images.githubusercontent.com/78306719/126913097-4d984f11-a17c-42e2-80f1-ee68b1e9de73.png)

The *stratify* parameter was set to *y* to maintain the same proportion of 0 and 1 values between the training and test sets. Notice the class imbalance between *0* instances and *1* instances in our training data. This was handled with random oversampling as described below.

#### Model choice, including limitations and benefits

After lengthy consideration, the team elected to go with a Logistic Regression model for this data. The Logistic Regression model was chosen because the question the team is trying to answer is a binary classification problem for which Logistic Regression is well-suited. The Logistic Regression model is advantageous in this case because it is easy to implement and easy to understand. Furthermore, the data includes a limited number of features prior to categorical variable encoding, and the team was concerned that a complex model might overfit the data as a result. 

One potential drawback to Logistic Regression model is related to the size of the data and the convergence of the model. Several optimizers were explored with the Logistic Regression model, and it was found that some optimizers required a significant number of iterations for the model to converge. Hyperparameter tuning was also investigated in an attempt to improve the model performance, but the team observed that there was not much to be gained in terms of model accuracy via hyperparameter tuning.

#### Explanation of changes in model choice (if changes occurred between the Segment 2 and Segment 3 deliverables) 

There was no change in model choice between the Segment 2 and Segment 3 deliverables.

#### Description of how they have trained the model thus far, and any additional training that will take place

As mentioned previously, the training data in its raw form contained a fairly large class imbalance between *0* instances and *1* instances. In order to mitigate the class imbalance and optimize the model performance, random oversampling was used to balance the values in the *0* class and the *1* class as shown in the image below.

![oversample_and_train](https://github.com/SindieCastro/Predicting_Sales_Using_Machine_Learning/blob/main/images/ML_oversampling.png)

The image above also shows the training method used for the logistic regression model. The model was trained on the resampled training data using the *lbfgs* solver with a maximum of 200 iterations.

#### Description of current accuracy score

The current accuracy score is approximately 88% as shown in the figure below. The precision for 0 and 1 instances are 0.93 and 0.74, respectively, and the recall for 0 and 1 instances 0.91 and 0.78, respectively.

![report](https://github.com/SindieCastro/Predicting_Sales_Using_Machine_Learning/blob/main/images/ML_classification_report.png)

#### How the model addresses the question

This model addresses our question of whether or not sales in Europe will meet threshold sales by predicting a *1* or a *0* where a *1* indicates that European sales is expected to exceed the threshold, and a *0* indicates that European sales is not expected to exceed the threshold.

To investigate the model performance, the histograms below show the probability scores for *0* predictions and *1* predictions.

#### *0* Predictions Probability Histogram

![LR0](https://github.com/SindieCastro/Predicting_Sales_Using_Machine_Learning/blob/main/images/LR_0_probability_hist.png)

For *0* predictions, the probability histogram shows that most probabilities were above 0.75 to predict a 0.

#### *1* Predictions Probability Histogram

![LR1](https://github.com/SindieCastro/Predicting_Sales_Using_Machine_Learning/blob/main/images/LR_1_probability_hist.png)

For *1* predictions, the probability histogram shows a fairly even distribution of probabilities until the probability approaches 1 where a significant number of probabilities were at or near 1. This indicates that the model was very confident in its ability to predict *1* values, but the strong concentration of very high probabilities invites further investigation.

To gain further insight into the model performance, the image below shows the *0*/*1* predictions along with a line plot showing the corresponding probabilities. Note that this data supports the histograms above for the *0* and *1* predictions where the *0* portion of the probability curve shows a relatively flat slope from near 0 to roughly 0.25, and the *1* portion of the probability curve shows a rapid slope from 0.5 to nearly 1 where the curve flattens out.

![LRPred](https://github.com/SindieCastro/Predicting_Sales_Using_Machine_Learning/blob/main/images/LR_predictions_and_regression.png)

## QuickDBD Mockup

ERD:

![ERD](https://github.com/SindieCastro/Predicting_Sales_Using_Machine_Learning/blob/main/images/schema_1.PNG)


### Database layout and Design

The team has decided to utilize Heroku for the online database. After cleaning the data and considering the constraints from Heroku regarding row limits, the data was divided into three categories: games, platforms, and genres. Once these categories were established, three CSV files were generated (using vg_db_csv_creator.ipynb) to populate the table data in pgAdmin and uploaded into the Heroku database.    

CSV Data Imported into pgAdmin:

![game_table](https://github.com/SindieCastro/Predicting_Sales_Using_Machine_Learning/blob/main/images/Game_table_verification.PNG)

Data Uploaded into Heroku:

![Heroku_1](https://github.com/SindieCastro/Predicting_Sales_Using_Machine_Learning/blob/main/images/heroku_db_verification.PNG)

After the data was loaded into Heroku, a connection was established using heroku_db_connection.ipynb. Using SQL to query the online database, the team was able to perform two INNER JOINS and reconstruct the data needed for the machine learning and pass it into the logistic regression model for processing (DB_VG_LR_resample_Final.ipynb).

## Dashboard

![Dashboard image](https://user-images.githubusercontent.com/78306719/126910401-3af718d8-c2bc-485e-b280-0b30595c9522.PNG)


## Google Slides
https://docs.google.com/presentation/d/1wRn_DMTICQlc5AWBJ5g96msv_DWjqQZWoBNYVVqalm4/edit?usp=sharing

## Storyboard
https://docs.google.com/presentation/d/1xscv3WHg-kAVCQeLhKaqSvw58ImNI4yrhc5Y1BQruPc/edit?usp=sharing

## Tableau Workbook
https://public.tableau.com/app/profile/jacqueline.esbri/viz/FinalProjectTeamRedPresentation_16270732094330/TitlePage?publish=yes

## References

- <https://www.kaggle.com/gregorut/videogamesales?select=vgsales.csv>, accessed 2 July, 2021.

- <https://techcrunch.com/2015/10/31/the-history-of-gaming-an-evolving-community/>, accessed 3 July, 2021.

- <https://github.com/get-icon/geticon/raw/master/icons/visual-studio-code.svg>, accessed 15 July, 2021.

- <https://github.com/get-icon/geticon/raw/master/icons/python.svg>, accessed 15 July, 2021.

- <https://github.com/get-icon/geticon/raw/master/icons/postgresql.svg>, accessed 15 July, 2021.

- <https://maxgentechnologies.com/images/intern/python_machine_logo.jpg>, accessed 15 July, 2021.

- <https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSLPEwocsaSWuRA1_rvsYXMsXCMzgSWVB956N1CKMQ&usqp=CAU>, accessed 15 July, 2021.

- <https://github.com/get-icon/geticon/raw/master/icons/javascript.svg>, accessed 15 July, 2021.

- <https://brand.heroku.com/static/media/heroku-logotype-spacing-vertical.dc54b577.svg>, accessed 15 July, 2021.
