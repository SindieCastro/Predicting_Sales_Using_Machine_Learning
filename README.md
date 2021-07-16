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

- <img src="https://github.com/get-icon/geticon/raw/master/icons/visual-studio-code.svg" alt="VScode" width="20px" height="20px"> VS Code

- <img src="https://github.com/get-icon/geticon/raw/master/icons/python.svg" alt="Python" width="20px" height="20px"> Python Libraries

- <img src="https://github.com/get-icon/geticon/raw/master/icons/postgresql.svg" alt="PostgreSQL" width="20px" height="20px"> PostgreSQL & pgAdmin
- <img src="https://maxgentechnologies.com/images/intern/python_machine_logo.jpg" width="px" height="20px"> Machine Learning 

- <img src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSLPEwocsaSWuRA1_rvsYXMsXCMzgSWVB956N1CKMQ&usqp=CAU" alt="Tableau" width="20px" height="20px"> Tableau Public  

- <img src="https://github.com/get-icon/geticon/raw/master/icons/javascript.svg" alt="JavaScript" width="20px" height="20px"> JavaScript
- <img src="https://brand.heroku.com/static/media/heroku-logotype-spacing-vertical.dc54b577.svg" alt="Heroku" width="20px" height="20px"> Heroku


## Communication Protocol

The team’s communication protocol will be relatively similar for all segments of the project. The team is aware of the importance of communicating with each other in order to achieve a successful outcome. The members will continue to respect lines communication, address any disagreements early on, and collectively work on assignments distributed according to function and expertise. The following communication protocol was established:

- Roles and requirements are clearly defined
- Use Slack channel to schedule meetings, discuss opinions, and findings 
- Inform the acting leader via Slack or text message on schedule conflicts
- Ask for help when stuck on an individual task
- Recognize and praise a member’s great work
- Maintain open communication and active listening to prevent conflicts 
- Schedule group meetings via Zoom as needed 
- Milestone status is regularly reported to the team
- Motivate each other


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

`**Will sales in Europe be greater than the target revenue?**`

<span style="color:red">Will sales in Europe be greater than the target revenue?</span>


## Machine Learning Model

#### Description of preliminary data preprocessing

The data was initially explored to determine which columns to keep as features and which columns to drop. The following are the columns dropped and retained for analysis.

- Dropped columns: Name, Year, Publisher, Other_Sales, Global Sales.
- Retained columns: Platform, Genre, NA_Sales, EU_Sales, JP_Sales

The columns Name and Publisher were dropped due to a large number of unique values and not very useful for the ML model. The Global_Sales column was dropped because it is a sum of the regional sales numbers. The team debated whether or not to keep Other_Sales column, but ultimately it was dropped. The Other_Sales column represented all sales outside of NA, EU, and JP, and the team felt that in a real-world application, this data would likely not be available prior to launching a video game in a major market. The data that was kept for analysis was reviewed for null values. Fortunately, no null values were found, so the team proceeded with the analysis.

#### Description of preliminary feature engineering and preliminary feature selection, including their decision-making process

The team strategically selected which columns to drop and keep to properly train the ML model. The features to make the prediction and target to predict the outcome changed from the original mockup model. The string columns were encoded into numerical values. Scaling was explored with the sales data, but it was found that scaling did not improve the accuracy of the ML model. The team believes this could be due to the heavily skewed distribution of the sales data as indicated by the EU_Sales histogram below. Further investigation is required.

#### Sales Data Columns
![sales_bf_norm.PNG](images/sales_bf_norm.png)

#### Histogram of EU_Sales
![EU_Sales_histogram.PNG](images/EU_Sales_histogram.png)

#### Description of how data was split into training and testing sets

The data was split into the training and testing sets using the *train_test_split*

#### Model choice, including limitations and benefits

After lengthy consideration, the team elected to go with a Logistic Regression model for this data. The Logistic Regression model was chosen because the question the team is trying to answer reduces the `problem` of EU_Sales to a binary classification problem for which Logistic Regression is well-suited. The Logistic Regression model is advantageous in this case because it is easy to implement and easy to understand. Furthermore, the data includes a limited number of features prior to categorical variable encoding, and the team was concerned that a complex model (e.g. Neural Network) might overfit the data as a result. 

One potential drawback to Logistic Regression model is related to the size of the data and the convergence of the model. Several optimizers were explored with the Logistic Regression model, and it was found that some optimizers required a significant number of iterations for the model to converge. Hyperparameter tuning was also investigated in an attempt to improve the model performance, but the team observed that there was not much to be gained in terms of model accuracy via hyperparameter tuning.


## QuickDBD Mockup

![db_schema](https://github.com/SindieCastro/Predicting_Sales_Using_Machine_Learning/blob/main/images/schema_1.PNG)


### Database layout and Design

To begin, the database structure was designed around the largest all inclusive data (regions, which includes all games and categories) and scaled down to the smallest segment of data (genres, limited to just generes of games). Every column from the dataset was either assigned to a broad category (regional sales) or got assigned an individual table (games, genre) based on the relationships to the dataset itself. 

The structure is going to be set up as many to one relationship between regions and region sales.  Although there are multiple sales in a region, the data is broken down by regional section (North American, Europe, Japan, Other) and will be considered as one value per region. Next, a one to many relationship from regional sales to game platforms is created. Every regional sales area will have multiple game platforms associated with it. This will also cover the possibilities of unique platforms in certain regions.  

From game platform two relationships are created – a one to one relationship to platforms (a game platform only has 1 platform), and a one to many to game publisher. Every platform can have multiple publishers. From game publisher, a one to many relationship is created into games (publishers can have multiple games). Finally, games will be have a one to one relationship with genre (one genre per game).

With this layout there will be an opportunity to create multiple joins to gather specific information for any related query.  For instance, we could pull every game publisher for the North American region by joining regional sales with game platform, platform, and game publisher using the specific ID's from each table.


## Google Slides
https://docs.google.com/presentation/d/1wRn_DMTICQlc5AWBJ5g96msv_DWjqQZWoBNYVVqalm4/edit?usp=sharing

## Storyboard
https://docs.google.com/presentation/d/1xscv3WHg-kAVCQeLhKaqSvw58ImNI4yrhc5Y1BQruPc/edit?usp=sharing

## Preliminary Tableau
https://public.tableau.com/app/profile/jacqueline.esbri/viz/FinalProjectTeamRed/Sheet6?publish=yes


## References

- <https://www.kaggle.com/gregorut/videogamesales?select=vgsales.csv>, accessed 2 July, 2021.

- <https://techcrunch.com/2015/10/31/the-history-of-gaming-an-evolving-community/>, accessed 3 July, 2021.

