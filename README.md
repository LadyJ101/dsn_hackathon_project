# DSN HACKATHON PROJECT QUALIFICATION
## Project Overview
  This project was developed for the Data Science Nigeria (DSN) Hackathon and focuses on predicting car prices based on various features such as brand, model, year, mileage, fuel type, and more. The goal is to build a robust machine learning model that accurately estimates car prices, which can be useful for both buyers and sellers in the automotive market.

## Key Objectives:
  Performes comprehensive exploratory data analysis (EDA) to understand the dataset.
  Preprocessed the data to handle missing values, encode categorical variables, and scale numerical features.
  Built and trained an XGBoost regression model to predict car prices.
  Optimized the model using hyperparameter tuning with Optuna.
  Generated predictions on the test set and prepare a submission file.

## Dataset Description

The dataset consists of two main files:
  train.csv: Contains 188,533 records with 13 features, including the target variable price.
  test.csv: Contains 125,690 records with 12 features (excluding price).

## *Features:*

    id: Unique identifier for each car.
  
    brand: Manufacturer of the car (e.g., Toyota, Honda).
  
    model: Specific model of the car.
  
    model_year: Year the car was manufactured.
  
    milage: Mileage of the car (in miles).
    
    fuel_type: Type of fuel the car uses (e.g., Gasoline, Diesel).
   
    engine: Description of the car's engine.
  
    transmission: Type of transmission (e.g., Automatic, Manual).
  
    ext_col: Exterior color of the car.
  
    int_col: Interior color of the car.
  
    accident: Whether the car has been in an accident.
  
    clean_title: Whether the car has a clean title.
  
    price: Target variable (price of the car).

## *Missing Values:*
  
    fuel_type: 5,083 missing in train, 3,383 in test.
  
    accident: 2,452 missing in train, 1,632 in test.
  
    clean_title: 21,419 missing in train, 14,239 in test.

#  Exploratory Data Analysis (EDA)
  
  ## *Summary Statistics:*
    
      The average car price is approximately $43,878, with a minimum of $2,000 and a maximum of $2.95 million.
      The average mileage is 65,705 miles, and the average model year is 2015.

  ## *Visualizations:*
  
      Distribution of Numerical Features:

      Model Year: Most cars are from 2010 onwards.
    
      Mileage: Right-skewed distribution, indicating most cars have lower mileage.
  
      Price: Highly right-skewed, with most cars priced below $100,000.


      This image above shows how features like accident and fuel type affect the price of the vehicle

      


  ## *Categorical Features:*
  
      Brand: 57 unique brands, with Toyota, Ford, and Chevrolet being the most common.
    
      Model: 1,897 unique models.
  
      Fuel Type: 7 unique types, with Gasoline being the most common.

## *Insights:*
      
      Newer cars and lower mileage are correlated with higher prices.
      
      Cars with accident history tend to have lower prices.
  
      Diesel and Hybrid cars are generally more expensive than Gasoline cars.


# Data Preprocessing

## Steps:

    Handled Missing Values:

    print(" SMART MISSING VALUE HANDLING")
print("=" * 40)

## Handled missing values: 

    fuel_type: Filled with "most common fuel".
  
    accident: Filled with "None reported".
    
    clean_title: Filled with "No" (assuming missing implies not clean).

  ## Encode Categorical Variables:
  
      Label Encoding for ordinal features.
  
      One-Hot Encoding for nominal features.  

  ## Scale Numerical Features:
  
      StandardScaler for model_year and milage.
    
 ## Feature Engineering:
  
      Extracted horsepower and engine_size from the engine column using regex.
  
      Created age feature from model_year.
      
    Preprocessing Pipeline:
  
      python
  
      numeric_features = ['model_year', 'milage', 'horsepower', 'engine_size', 'age']
  
      numeric_transformer = Pipeline(steps=[  ('imputer', SimpleImputer(strategy='median')),
        ('scaler', StandardScaler())])

      categorical_features = ['brand', 'model', 'fuel_type', 'transmission', 'ext_col', 'int_col', 'accident', 'clean_title']

      categorical_transformer = Pipeline(steps=[
          ('imputer', SimpleImputer(strategy='constant', fill_value='unknown')), ('onehot', OneHotEncoder(handle_unknown='ignore'))])

      preprocessor = ColumnTransformer(
        tansformers=[('num', numeric_transformer, numeric_features),('cat', categorical_transformer, categorical_features)])

# Model Building

 ##  Algorithm: XGBoost Regressor
    
      Why XGBoost?: Handles mixed data types, captures non-linear relationships, and provides high accuracy.
  
      Hyperparameter Tuning: Used Optuna to optimize parameters such as max_depth, learning_rate, and n_estimators.

## Optuna Study:

  Objective: Minimize Root Mean Squared Error (RMSE).

  Trials: 100 iterations.
  
  Best Parameters:
    
    n_estimators=2500,
    
    learning_rate=0.01,
    
    max_depth=5,
    
    subsample=0.6,
    
    colsample_bytree=0.8,
    
    random_state=0,
    
    n_jobs=-1,
    
    eval_metric='rmse'
  
## Feature Importance:
https://via.placeholder.com/600x400?text=Feature+Importance+Plot

### Top features: model_year, milage, horsepower, and brand.

Predictions:

  Generated predictions for the test set and saved to submission.csv.

###  Future Improvements Suggestions

  Feature Engineering: Create more features like turbo, brand popularity, model rarity, etc.

  Advanced Models: Experiment with Neural Networks or Ensemble methods.
  
  Geographic Data: Include location-based features if available.

  Deployment: Build a web app for real-time price predictions.

# Author
Developed for the Data Science Nigeria (DSN) Hackathon.
