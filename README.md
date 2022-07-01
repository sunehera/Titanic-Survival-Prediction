#  Who survived the Titanic?



In this project I will use machine learning to develop a predictive model to determine who would have survived the Titanic.




## About the dataset



For this project, I will be exploring a dataset about the passengers on the *Titanic*, the British passenger liner that crashed into an iceberg during its maiden voyage and sank early in the morning on April 15, 1912.
The tragedy stands out in history as one of the deadliest commercial maritime disasters during peacetime.
More than half of the passengers and crew died, due in large part to poor safety standards, such as not having enough lifeboats or not ensuring all lifeboats were filled to capacity during evacuation.

This dataset presents the most up-to-date knowledge about the passengers that were on the *Titanic*, including whether or not they survived. The dataset was downloaded from Kaggle.com and has already been split into a training set (in the `train.csv` file) and test set (in the `train.csv` file).
This dataset is frequently used to introduce using machine learning techniques that take multiple inputs and use them to predict an outcome, in this case whether a passenger is likely to have survived.



 I will Create a first *logistic regression* model using the `glm` function using the `train_imputed` dataframe with the `Survived` column as the target value (i.e. response variable), and `age_imputed` as the only feature (i.e. explanatory variable).
    
     let's calculate the model's predictions on the training data (`train_imputed`) and Store the output dataframe with the two new columns (`pred` and `outcome`) in a variable called `model_1_preds`.
      
    
  
    The accuracy calculated on the training data will often appear to be unusually high, because we have created the model explicitly to predict this data.

    Therefore, Ie will use k-fold cross-validation to measure our model's performance on data that is has not seen. We will do this using the `cv.glm` function from the `boot` package. 
   
    

    Then I will Train a second, multivariate logistic regression model, using the `age_imputed`, `SibSp`, `Pclass`, and `Sex` variables as predictor variables.

      Run cross-validation on this model to calculate its error, which you should report.
    
    Now, let's train a third logistic regression model with interaction between some of the variables.
    
      


This Titanic data was downloaded from [Kaggle.com](https://www.kaggle.com/c/titanic/overview), a website for data science competitions. Kaggle has already divided the data into training and test sets for us. The training data was in the `train.csv` file which we loaded in Exercise 1. The test data is in a file called `test.csv`, which contains all the same columns as the training set except for the  `Survived` column.
    
    Using the the multivariate model, I will make run a prediction and save the results in a csv file then I will upload to Kaggle.
