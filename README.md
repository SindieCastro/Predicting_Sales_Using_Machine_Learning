<p align='center'>
    <img src=images/readme6.png width="1000" height="600">
</p>

# Predicting Sales Using Machine Learning

# Segment One:


## Overview

A team of analysts referred to as the "Red Team" has been tasked for this project. The goal of the project is to predict sales of video games using Machine Learning (ML) based on sales in Europe, genres, and platforms.


## Purpose

The gaming industry is immensely large and it is continuing to grow. As such, many companies want to be part of the growing revenue stream. The Red Team will build a predictive ML model to find patterns in existing and new sales data. Using ML will enable the team to leverage existing algorithms to learn from the data and lead to more accurate predictions.

To accomplish this task, the team will build and evaluate several ML models or algorithms (e.g.,Logistic regression, Neural Network). Once the model is created, its performance will be evaluated to see how well it predicts the data. The ultimate goal is to market the algorithm to existing companies in the gaming sector or organizations looking to get involved in the industry.


## Resources

The technologies planned to be used for this project include the following:

- Python & Pandas library
- PostgreSQL & pgAdmin 
- mlenv (Numpy, SciPy, Scikit-Learn)
- Imbalanced-learn Package
- Tableau
- JavaScript


## Communication Protocol

To prepare for this project Team Red created the following communication protocol: 

- Discuss role distribution
- Use Slack channel to schedule meetings, discuss opinions and findings 
- Inform the acting leader via Slack or text message on schedule conflicts
- Ask for help when stuck on an individual task
- Inform the acting leader if the task will be completed late
- Inform the acting leader when emergency task reassignment will need to take place
- Praise a team member for good work
- Team leader will update team members of any changes due to emergencies or a team member needing help with a task
- Maintain open communication and active listening to prevent conflicts 


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

The team have launched a video game (genre/platform) in North America (NA) and Japan (JP). The sales data for those regions is accessible, and the team is considering launching the game in Europe. The product launch team has an anticipated cost for the European launch, but need the Red Team to analyze if it would be profitable to launch in Europe.

**Will sales in Europe be greater than the target revenue?**


## Machine Learning Model

<s> This text is crossed out The team plans to investigate Logistic Regression and Neural Network and assess both for accuracy and computation time. One advantage to Logistic Regression is that it could use it without binning the sales data and encode the categorical variables. The neural network on the other hand may give us better accuracy, but we would need to bin the sales data. </s>

To properly build the model, a desired sales amount threshold for <s>North America</S> Europe? will be determined; this would become the target variable. <s>So we would bin the sales data for the rest of the world, and categorize the NA_Sales data as a greater than threshold or less than threshold.</s> For example, the team can pick $500,000 in sales. The NA_Sales column would become "NA_Sales_greater_than_0.5" (data is in $ Millions), and label as 0 or 1 for each entry. As a result, the model becomes a binary classification problem.


## GitHub Repository Management

For better management and organization of the repository, the team agreed to create feature branches of project versus individual branches for team members. team members will submit (add) any documents to designated feature branches of the project, and provide detailed description on “commit” message.

#### Note: 

- **Schema image is located in database_files branch**
- **Machine Learning code is located in ML-model_files branch**


## References

- <https://www.kaggle.com/gregorut/videogamesales?select=vgsales.csv>, accessed 2 July, 2021.

- <https://techcrunch.com/2015/10/31/the-history-of-gaming-an-evolving-community/>, accessed 3 July, 2021.

# End of Segment One



# Segment Two:

## Overview

The team made great strides in building the different pieces of the project. All members continue to evaluate what is and is not working during progress of the project.


## Communication Protocols

The team’s communication protocols will be relatively similar for all segments of the project. The team is aware of the importance of communicating with each other in order to achieve a successful outcome. The members will continue to respect lines communication, address any disagreements early on, and collectively work on assignments distributed according to function and expertise. 

For segment two, the following communication protocols were established:

- Discuss the team’s goals and objectives during the given segment
- Roles and requirements are clearly defined
- Set regular communication goals, types, and schedules
- Increase group meetings via Zoom to clearly define scope, resources, and timeline
- Continue group messages in Slack 
- Milestone status is regularly reported to the team
- Attend office hours to ask questions and ensure the project is on the right track
- Motivate each other
- Recognize and praise a member’s great work


## Machine Learning Model
During this segment, the team transitioned the mockup ML model to a functioning model using the data as outlined below.

#### Description of preliminary data preprocessing

The data was initially explored to determine which columns to keep as features and which columns to drop. The following are the columns dropped and retained for analysis.

- Dropped columns: Name, Year, Publisher, Other_Sales, Global Sales.
- Kept columns: Platform, Genre, NA_Sales, EU_Sales, JP_Sales

The columns Name and Publisher were dropped due to a large number of unique values and not very useful for the ML model. The Global_Sales column was dropped because it is a sum of the regional sales numbers. The team debated whether or not to keep Other_Sales column, but ultimately it was dropped. The Other_Sales column represented all sales outside of NA, EU, and JP, and the team felt that in a real-world application, this data would likely not be available prior to launching a video game in a major market. The data that was kept for analysis was reviewed for null values. Fortunately, no null values were found, so the team proceeded with the analysis.

#### Description of preliminary feature engineering and preliminary feature selection, including their decision-making process

The team strategically selected which columns to drop and keep to properly train the ML model. The features to make the prediction and target to predict the outcome changed from the original mockup model. The string columns were encoded into numerical values. Scaling was explored with the sales data, but it was found that scaling did not improve the accuracy of the ML model. The team believes this could be due to the heavily skewed distribution of the sales data as indicated by the EU_Sales histogram below. Further investigation is required.

#### Sales Data Columns
![sales_bf_norm.PNG](images/sales_bf_norm.png)

#### Histogram of EU_Sales
![EU_Sales_histogram.PNG](images/EU_Sales_histogram.png)

#### Description of how data was split into training and testing sets

The data was split into the training and testing sets using the *train_test_split*

#### Explanation of model choice, including limitations and benefits

After lengthy consideration, the team elected to go with a Logistic Regression model for this data. The Logistic Regression model was chosen because the question the team is trying to answer reduces the problem of EU_Sales to a binary classification problem for which Logistic Regression is well-suited. The Logistic Regression model is advantageous in this case because it is easy to implement and easy to understand. Furthermore, the data includes a limited number of features prior to categorical variable encoding, and the team was concerned that a complex model (e.g. Neural Network) might overfit the data as a result. 

One potential drawback to Logistic Regression model is related to the size of the data and the convergence of the model. Several optimizers were explored with the Logistic Regression model, and it was found that some optimizers required a significant number of iterations for the model to converge. Hyperparameter tuning was also investigated in an attempt to improve the model performance, but the team observed that there was not much to be gained in terms of model accuracy via hyperparameter tuning.

## QuickDBD Mockup

![db_schema](https://github.com/SindieCastro/Predicting_Sales_Using_Machine_Learning/blob/main/images/schema_1.PNG)


### Database layout and Design
To begin, the database structure was designed around the largest all inclusive data (regions, which includes all games and categories) and scaled down to the smallest segment of data (genres, limited to just generes of games). Every column from the dataset was either assigned to a broad category (regional sales) or got assigned an individual table (games, genre) based on the relationships to the dataset itself. 

The structure is going to be set up as many to one relationship between regions and region sales.  Although there are multiple sales in a region, the data is broken down by regional section (North American, Europe, Japan, Other) and will be considered as one value per region. Next, a one to many relationship from regional sales to game platforms is created. Every regional sales area will have multiple game platforms associated with it. This will also cover the possibilities of unique platforms in certain regions.  

From game platform two relationships are created – A one to one relationship to platforms (a game platform only has 1 platform), and a one to many to game publisher. Every platform can have multiple publishers. From game publisher, a one to many relationship is created into games (publishers can have multiple games). Finally, games will be have a one to one relationship with genre (one genre per game).  

With this layout there will be an opportunity to create multiple joins to gather specific information for any related query.  For instance, we could pull every game publisher for the North American region by joining regional sales with game platform, platform, and game publisher using the specific ID's from each table.


## Google Slides
https://docs.google.com/presentation/d/1wRn_DMTICQlc5AWBJ5g96msv_DWjqQZWoBNYVVqalm4/edit?usp=sharing

## Storyboard
https://docs.google.com/presentation/d/1xscv3WHg-kAVCQeLhKaqSvw58ImNI4yrhc5Y1BQruPc/edit?usp=sharing



