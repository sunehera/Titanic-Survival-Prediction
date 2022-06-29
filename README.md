# Assignment 10: Who survived the Titanic?

> #### Install new packages
> 
> Please install the `ggmosaic` package by running this line in the RStudio Console:
>
> `install.packages("ggmosaic")`

## Instructions

In this assignment you will use machine learning to develop a predictive model to determine who would have survived the Titanic.

**Make sure to answer the exercises in this assignment using full sentences and paragraphs, and proper spelling and punctuation.**

Read the [About the dataset](#about-the-dataset) section to get some background information on the dataset that you'll be working with.
Each of the below [exercises](#exercises) are to be completed in the provided spaces within your starter file `titanic.Rmd`.
Then, when you're ready to submit, follow the directions in the **[How to submit](#how-to-submit)** section below.


## About the dataset

![Picture of the Titanic](/img/titanic-photograph.jpg)

For this homework assignment, you will be exploring a dataset about the passengers on the *Titanic*, the British passenger liner that crashed into an iceberg during its maiden voyage and sank early in the morning on April 15, 1912.
The tragedy stands out in history as one of the deadliest commercial maritime disasters during peacetime.
More than half of the passengers and crew died, due in large part to poor safety standards, such as not having enough lifeboats or not ensuring all lifeboats were filled to capacity during evacuation.

This dataset presents the most up-to-date knowledge about the passengers that were on the *Titanic*, including whether or not they survived. The dataset was downloaded from Kaggle.com and has already been split into a training set (in the `train.csv` file) and test set (in the `train.csv` file).
This dataset is frequently used to introduce using machine learning techniques that take multiple inputs and use them to predict an outcome, in this case whether a passenger is likely to have survived.

The dataset contains the following variables:

| Variable    | Description                                                           |
| :-----------| :-------------------------------------------------------------------- |
| `PassengerId`    | A unique number identifying each passenger.                          |
| `Survived`  | Whether this passenger survived (0 = No; 1 = Yes). (This variable is not present in the test dataset file.)                     |
| `Pclass`    | Passenger Class (1 = 1st; 2 = 2nd; 3 = 3rd)                           |
| `Name`      | Name                                                                  |
| `Sex`       | Sex                                                                   |
| `Age`       | Age                                                                   |
| `SibSp`     | Number of Siblings or Spouses Aboard                                     |
| `Parch`     | Number of Parents or Children Aboard                                     |
| `Ticket`    | Ticket Number                                                         |
| `Fare`      | Passenger Fare (British pound)                                        |
| `Cabin`     | Cabin                                                                 |
| `Embarked`  | Port of Embarkation (C = Cherbourg; Q = Queenstown; S = Southampton)  |


Also note that the following definitions were used for `SibSp` and `Parch`:

| Label        | Definition                                                                   |
| :----------- | :--------------------------------------------------------------------        |
| Sibling      | Brother, Sister, Stepbrother, or Stepsister of Passenger Aboard Titanic      |
| Spouse       | Husband or Wife of Passenger Aboard Titanic (Mistresses and Fiances Ignored) |
| Parent       | Mother or Father of Passenger Aboard Titanic                                 |
| Child        | Son, Daughter, Stepson, or Stepdaughter of Passenger Aboard Titanic          |




## Exercises

**You must answer written questions with full sentences (and paragraphs where appropriate).**

1. 
    i. First, we need to load the training dataset from the *train.csv* file. We will do this using the `read_csv(...)` function.
    
      > #### Important
      >
      > You should **not** try to load the dataset by clicking the file `train.csv` in the *File Explorer* panel or by using *File → Import Dataset*.
      Instead, make sure to use the `read_csv(...)` function as in this example,
      >
      > ```r
      > train_df <- read_csv(file = "train.csv")
      > ```
      >
      > which reads the datafile and assigns the loaded dataset to a variable called `train_df`.

      However, reading in the dataset using `read_csv(file = "train.csv")` causes some of the columns to be converted into inconvenient data types.
    Fix this so that your later analysis does not run into problems.
    Use the `col_types = cols()` argument within `read_csv()` as explained in this section of *R for Data Science*, <http://r4ds.had.co.nz/data-import.html#problems>, to change the data type defaults for the following columns:

      *   Convert `Pclass` to the character data type

      *   Convert `SibSp` to the character data type

      *   Convert `Parch` to the character data type
    
      After you get the inputs to `read_csv()` to work correctly, assign the dataset to a variable called `train_df`.

    ii. Using the `mutate` function, add a column to `train_df` containing a new variable called `did_survive`. This should simply convert the `Survived` column to the logical datatype, which you can do using the `as.logical` function, e.g. `as.logical(Survived)`.
    
      Make sure that your dataset contains both the original `Survived` column as well as the new `did_survive` column, as we will need both. You should store this in the same `train_df` variable that you created in part (i).
    
    Once you have finished this exercise, commit your answers.

2. Let's take a look at how the chance of survival is affected by different continuous variables in the dataset.

    `pivot_longer()` the continuous explanatory variables (`Age` and `Fare`), and then create a histogram of their distributions depending on whether the passengers survived or not. In other words, you should use the `fill = did_survive` argument, and facet over the original variables so that you have separate sub-plots for `Age` and `Fare`. Here is some starter code - you will need to fill in the ellipses:
    
    ```r
    train_df %>%
      pivot_longer(..., names_to="...", values_to = "...") %>%
      ggplot() +
      geom_histogram(aes(x = ..., fill = did_survive), ...) +
      facet_wrap(~ ..., scales = "free")
    ```
    
    Using your graphs, how do the distributions of the `Age` and `Fare` variables differ between survivors and non-survivors? Do you think these differences will be helpful for predicting who survived?
    
    Once you have finished this exercise, commit your answers.

3. Let's take a look at how the chance of survival is affected by different categorical variables in the dataset.

    `pivot_longer()` four of the categorical explanatory variables (`Pclass`, `Sex`, `Parch`, and `SibSp`) and create a bar plot of each one using the `geom_bar` function and faceting over the original explanatory variables to create a subplot for each (as you did in the previous question). Again, use the `fill = did_survive` argument:
    
    ```r
    train_df %>%
      pivot_longer(..., names_to="...", values_to = "...") %>%
      ggplot() +
      geom_bar(aes(x = ..., fill = did_survive)) +
      facet_wrap(~ ..., scales = "free")
    ```
    
    You should set the figure size appropriately using the `fig.width` and/or `fig.asp` options for the code chunk.
    
    Using your graphs, explain how each of these categorical variables is related to surviving (or not surviving) the Titanic. Do these results make sense given what you know about the Titanic's sinking? (You can read more about the sinking here: https://en.wikipedia.org/wiki/Sinking_of_the_RMS_Titanic)
    
    Which variables do you think might be most useful for predicting survival, and why?
    
    Once you have finished this exercise, commit your answers.
    
4. Sometimes variables are inter-related. We can investigate how one categorical variable affects the distribution of another categorical variable using a mosaic plot from the `ggmosaic` library.

    You should already have installed the `ggmosaic` library - if not, go up to the top of this instruction fiile and follow the installation instructions there.
    
    Then copy and paste the following code into your answer file:
    
    ```r
    train_df %>%
      ggplot() +
      geom_mosaic(mapping = aes(x = product(Sex, Pclass), fill = Sex)) + 
      facet_grid(. ~ did_survive, scales="free") +
      labs(x = "Passenger class", y = "Gender", title = "Mosaic plot of who survived the Titanic")
    ```
    
    The areas of each "tile" in the mosaic plot correspond the the count of observations in that combination of categories.
   
    Based on the mosaic plot, how does the interaction of gender and passenger class seem to affect survival? Are there similar patterns in the proportion of each gender who survived in each class?
    
    Once you have finished this exercise, commit your answers.
    
5.  Unfortunately, the `Age` column contains a large amount of missing data. The predictive models we wish to use cannot be trained with missing data. Therefpre, we either need to ignore any rows with missing data (not an option because there is also missing data in our test set), or we need to fill in the missing data with best guesses (a process called "imputation").
    
    i. First let's calculate the amount of missing data in the age column.
    
      Fill in the ellipses in this code. `count` should equal the number of rows (there is a function for this that you learned in the Data Wrangling module - *do not* just replace the ellipses with the actual number). `fraction_missing` should calculate the fraction of rows missing in the `Age` column:
        
      ```r
      train_df %>%
        summarize(
          count = ...,
          missing = sum(is.na(Age)),
          fraction_missing = ...
        )
      ```
        
      As you can see from the code above, the `is.na(...)` function is the correct way to check if a value equals NA (i.e. is missing), and will return TRUE or FALSE correspondingly. You should use this function to check for missing data, not a boolean expression like `Age == NA`, which will not work.

    ii. Next we will impute (estimate) the missing ages. To to this, we are going to `mutate` a new column, `age_imputed` using an `if_else` function.
      
      We are simply going to replace the missing ages with the median of the non-missing ages. This is will obviously lead to a large amount of error in our imputed values, but it has the advantage of being simple to implement.
      
      Copy and paste this code:
      
      ```r
      train_imputed <- train_df %>%
        mutate(
          age_imputed = if_else(
            condition = is.na(Age),
            true = median(Age, na.rm = TRUE),
            false = Age
          )
        )
      ```
        
      You will be using the if_else function again in this assignment, so take a moment to see how it works:
        
      * The first parameter, condition, is an expression that must evaluate to TRUE or FALSE for every row. Is this case we use is.na(Age) to check whether the Age column is missing. 
      * Then we have to supply values that will be inserted in the new column, depending on whether the expression is true (i.e. missing data in this example, in which case we use the median) or false (i.e. an age already existed for this passenger, which we just recycle).
      
      Note that we also save this result as a new dataframe, `train_imputed`.
    
    iii. Recalculate if there is now any missing data by rerunning your code from part (i) of this question on the `age_imputed` column in the new `train_imputed` dataframe (you should find that there is no missing data in the new column).
    
    Once you have finished this exercise, commit your answers.

6. 
    i. Create a first *logistic regression* model using the `glm` function using the `train_imputed` dataframe with the `Survived` column as your target value (i.e. response variable), and `age_imputed` as the only feature (i.e. explanatory variable).
    
      Don't forget to include the `family` parameter with an appropriate argument.
    
      Save this model as a new variable: `model_1`
    
    ii. Now, let's calculate our model's predictions on the training data (`train_imputed`).
    
      There will be two steps to this. First we will calculate the predicted probabilities (between 0 and 1) using the `add_predictions` function with the `type = "response"` argument. These predictions will be stored in a column called `pred`. Second, you will round this to a predicted outcome of either 0 or 1, depending on whether the `pred` column is greater or less than 0.5. You will do this second step using the `mutate` and `if_else` functions, and save the outcomes in a new column called `outcome`.
      
      Store the output dataframe with the two new columns (`pred` and `outcome`) in a variable called `model_1_preds`.
      
    
    iii. Finally let's calculate the accuracy of our model on the training dataset. We will calculate the accuracy as the number of passengers that we correctly predicted, divided by the total number of passengers.
    
      To do this, we will fill out the collowing code template:
      
      ```r
      model_1_preds %>%
        mutate(
          correct = if_else(
            condition = ...,
            true = ...,
            false = ...
          )
        ) %>%
        summarize(
          total_correct = ...,
          accuracy = ...
        )
      ```
        
      In the `mutate` function, you are creating a new column, `correct`. The `correct` column should compare the `Survived` and `outcome` columns. If they contain the same values, then you should put a 1 in the `correct` column. Otherwise, you should put a 0  in the `correct` column.
        
      Then in the `summarize` function, you are calculating the `total_correct` (which you can do by adding up the 1's in the `correct` column) and the accuracy, which is `total_correct` divided by the total number of rows.
        
      What is the accuracy of your model? Does this seem good or bad?
    
    Once you have finished this exercise, commit your answers.

7. The accuracy calculated on the training data will often appear to be unusually high, because we have created the model explicitly to predict this data.

    Therefore, we will use k-fold cross-validation to measure our model's performance on data that is has not seen. We will do this using the `cv.glm` function from the `boot` package. 
    
    Copy and paste the following code chunk into your answer file and run it:
    
    ```{r}
    logistic_cv1 <- cv.glm(train_imputed, model_1, cost, K=5)
    ```
    
    > How does this function work?
    >
    > * The first argument is the training dataset.
    >
    > * The second argument is the model which we already fitted with the `glm` function.
    >
    > * The third argument is a function to calculate the validation error. In this case we are using a function called `cost` that calculates *1 - accuracy* (i.e. the inaccuracy, or the fraction of incorrectly predicted rows). If you are interested, the function is defined in the set-up chunk.
    >
    > * The fourth argument, K, is the number of ways that the dataset will divided up for cross-validation.
    
    We are saving the cross valication output in a variable called `logistic_cv1`, which you notice in RStudio is a list object. One of the items in the list is `delta`, which contains the overall cross-validation error score (i.e. the average of each of the k validations).
    
    Report this in your answer file by adding this line of code:
    
    ```r
    logistic_cv1$delta
    ```
    
    The first of the two numbers is the one we care about, the cross-validation error (the second number is an adjusted value that we can ignore).
    
    Once you have finished this exercise, commit your answers.

8. i. Train a second, multivariate logistic regression model, using the `age_imputed`, `SibSp`, `Pclass`, and `Sex` variables as predictor variables.

      Run cross-validation on this model to calculate its error, which you should report.
    
    ii. Now, let's train a third logistic regression model with interaction between some of the variables.
    
      In exercise 4, we saw that there seemed to be some interaction between the effect of gender and class on survival. Let's also see if age interacts with these variables (you might remember that women and children were evacuated first from the Titanic)
    
      Use the same predictor variables as the part (i), but now treat `age_imputed`, `Pclass`, and `Sex` as interacting variables (i.e. use a `*` between these three variables rather than a `+`). You should add `SibSp` in as a fourth feature with a `+`.
    
      Run cross-validation on this model and report its error.
      
    iii. Which of your three models has the most accurate validation error? Is this what you would expect? (The predictive power of a model usually increases with its complexity, up to a point.)
    
    Once you have finished this exercise, commit your answers.



## Bonus exercise (optional, but worth 1 bonus point if completed)

9. Up to this point, we have not actually made any predictions on a test set.

    This Titanic data was downloaded from [Kaggle.com](https://www.kaggle.com/c/titanic/overview), a website for data science competitions. Kaggle has already divided the data into training and test sets for us. The training data was in the `train.csv` file which we loaded in Exercise 1. The test data is in a file called `test.csv`, which contains all the same columns as the training set except for the  `Survived` column.
    
    In other words, Kaggle does not tell us which of the passengers in the test set actually survived the Titanic, so we cannot calculate the generalization error ourselves. To measure the generalization error on our test dataset, we need to make predictions and then upload them to the Kaggle website, which will grade your submission and enter it into the competition leaderboard.
    
    As you will need to create an account on Kaggle, this is left as a bonus exercise, but is worth 1 bonus point if you complete it. Here are the steps you will need to complete.
    
    In your answer file (you must push your code for this to GitHub to get the bonus point):
    
    * Read in the `test.csv` file, using similar code to that you wrote in Exercise 1. Make sure to save the dataset as a new variable, such as `test_df`.

    * Create a `test_imputed` dataframe with an `age_imputed` column, by adapting your code from Exercise 5.
    
    * Add `pred` and `outcome` columns using your best model (the one with the lowest cross-validation error). You should not create a new model, just reuse the best of the 3 that you trained on the training data during the assignment.
    
    * Using the `write_csv` function, save just the `PassengerID` and `outcome` columns to a new csv file. You will need to rename the `outcome` column as "Survived" before you save it as a csv (as this is what Kaggle expects your predictions column to be called).
    
    * Download this new csv file from RStudio, and then upload it to the Kaggle Titanic competition (https://www.kaggle.com/c/titanic/overview), and take a screenshot of your position on the leaderboard after your submission is scored.
    
    To get credit for this bonus question, you must make sure to (a) commit and push your code to GitHub, and (b) submit the screenshot of your position on the leaderboard to the separate bonus point assignment on Blackboard.

## Submitting

To submit the main assignment (this is required whether or not you do the bonus exercise), follow the two steps below.

1.  Save, commit, and push your completed RMarkdown file so that everything is synchronized to GitHub.
    If you do this right, then you will be able to view your completed file on the GitHub website.

2.  Knit your RMarkdown document to PDF format, export (download) the PDF file from RStudio Server, and then upload it to *Assignment 10* posting on Blackboard.


## Cheatsheets

You are encouraged to review and keep the following cheatsheets handy while working on this homework:

*   [Data transformation cheatsheet][data-transformation-cheatsheet]

*   [Data import cheatsheet][data-import-cheatsheet]

*   [ggplot2 cheatsheet][ggplot2-cheatsheet]

*   [RStudio cheatsheet][rstudio-cheatsheet]

*   [RMarkdown cheatsheet][rmarkdown-cheatsheet]

*   [RMarkdown reference][rmarkdown-reference]

[ggplot2-cheatsheet]:             https://github.com/rstudio/cheatsheets/raw/master/data-visualization-2.1.pdf
[rstudio-cheatsheet]:             https://github.com/rstudio/cheatsheets/raw/master/rstudio-ide.pdf
[rmarkdown-reference]:            https://www.rstudio.com/wp-content/uploads/2015/03/rmarkdown-reference.pdf
[rmarkdown-cheatsheet]:           https://github.com/rstudio/cheatsheets/raw/master/rmarkdown-2.0.pdf
[data-import-cheatsheet]:         https://github.com/rstudio/cheatsheets/raw/master/data-import.pdf
[data-transformation-cheatsheet]: https://github.com/rstudio/cheatsheets/raw/master/data-transformation.pdf
# Titanic-Survival-Prediction
