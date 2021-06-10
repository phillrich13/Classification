# Classifying Outcomes for Austin Animal Center Animal Intakes

## TOC
1. [SQL Code for making usable incoming dataset](https://github.com/phillrich13/Classification/blob/main/Animal%20Control%20SQL%20Code)
2. [Python Code for data ingestion, cleaning, and feature creation](https://github.com/phillrich13/Classification/blob/main/Austin%20Animal%20Center%20Data%20Cleaning.ipynb)
3. [Python Code for creating, training, and tuning Random Forest Models](https://github.com/phillrich13/Classification/blob/main/Tree%20Based%20Models.ipynb)
4. [Python Code for creating, training, and tuning XGB models](https://github.com/phillrich13/Classification/blob/main/XGBoost.ipynb)


## Abstract
My goal for this project was to predict the outcome for an animal that is received by the Austin Animal Center (AAC). The initial features were all based on the information that is collected on the intake of animals, and were then engineered into a set of 24 features. I started with a baseline random forest model, and then tuned the random forest model as well as created and tuned an xgboost model. The models were validated on using stratified 3-fold validation using the recall metric.  The main applications for this model would be to help prioritize triaging for animals predicted to be euthanized (prioritize medical care, or behavior rehabilitation), as well as animals predicted to be adopted (transfer to another shelter for space considerations).

## Design
The design for this classification project was to focus on predicting animal outcomes for the AAC. The focus was more on prediction than interpretability due to the shelter's commitment to a minimun 90% live outcome rate. It is ideal to find as many (preferably all) of the animals that will be Euthanized or be adopted, as these 2 outcomes represent material impacts to the operations of the AAC. Due to the desire for finding all the potential euthanized or potential adopted animals, recall is the primary evaluation metric. Since finding an animal that will be potentially euthanized will just kick off a triage to either medical or behavioral help, its okay to do so for animals that wouldn't be euthanized.

## Data
I used 2 datasets on the Austin Animal Center available from the Austin government data website. The first was [Animal Intakes](https://data.austintexas.gov/Health-and-Community-Services/Austin-Animal-Center-Intakes/wter-evkm) from 2013 to 2021, the 2nd was [Animal Outcomes](https://data.austintexas.gov/Health-and-Community-Services/Austin-Animal-Center-Outcomes/9t4d-g238) also ranging from 2013 to 2021. Each record in this data set represents 1 animal encounter. The same animal can be encountered multiple times over the course of the dataset, and each new encounter would be a new row. The data had ~125k records to start with 12 initial features. This data set consists of many outcomes (Adoption, Transfer, Return to Owner, Euthanasia, Death (non-Euthanasia)), but they have been rolled up into Adpotion, Euthanasia, and Transfer/RTO based on their time spent at shelter [seen here.](https://user-images.githubusercontent.com/75561764/121565590-6f71aa00-c9d1-11eb-9463-2e13154903fb.png)

The outcomes were [imbalanced](https://user-images.githubusercontent.com/75561764/121566061-fb83d180-c9d1-11eb-8cdd-373423d8623a.png), with euthanasia occurring ~4% of the time. Also the animal types were primarily cats and dogs (95% of them), and they had the longest stay time, so I only included cats and dogs.


## Algorithms
### Feature Engineering
* The data came with only categorical features, and most of the cleaning and feature engineering was parsing these strings
  * Converting the animal color field into 'Multi-Color' or not
  * Converting the breed into 'mixed breed' or not
  * Rolling up specific features into more holistic groupings
* One-hot encoded the features

### Models Tested
* Random Forests Model with balanced weights
  * Tuned hyper parameters using a combination of RandomSearchCV and GridSearchCV from sklearn
* XGBoost model with balanced sample weights
  * Tuned hyper parameters with a form of RandomSearchCV 

### Model Evaluation
All models were tested with a stratified 3 fold approach. The primary metric of concern was recall, and so models were evaluated using the macro recall.


## Tools
SQLLite - Used to join the 2 incoming files together on complex logic

Tableau - Used to do most of the EDA and understand differences in outcomes and their impacts. Produced simple visualizations

Python  - Used sklearn to create, train, tune, then test Random Forest Models. Used xgboost in conjunction with sklearn to create, train, tune, then test GBMs

## Communication
The main form of communication for this model is through slides and a presentation.
