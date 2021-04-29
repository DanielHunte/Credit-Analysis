# Report of Credit-Analysis

## Goal
Build a classification model to determine whether or not a loan applicant will receive a loan given some data about the loan and some objective data about an individual

## Implementation
Try many different model building algorithms and variants of such algorithms, and select the algorithm that produced the model that had the best accuracy (in short – we will be comparing accuracies)

## Relevant files:
- [database.csv](./database.csv): contains our data
- [data-joining.py](./data-joining.py): used to produce database.csv
- [model-selection.ipynb](./model-selection.ipynb): used to produce database.csv

## Collecting the Dataset
- the original dataset is sourced from [kaggle](https://www.kaggle.com/kapoorshivam/credit-analysis)
- due to the large amount of data in the dataset, the original dataset is split into the following two files: current_app.csv and previous_app.csv
- considering we need to test our data quickly, we decided to keep every 5th row from each of these datasets, and to join only those rows
- after joining every 5th row, we decided to keep 50,000 examples (before cleaning), considering we are preferring testing speed over maximum accuracy in our case
- such data collection was performed using a script that leverages python3's sqlite3 library
- data processing is done entirely as part of our jupyter notebook – we left as much work as possible to be done in pandas

## Implementation of Testing our models
- clean data
    - transform our target dimension into a binary number (simplifying from multiple values to a single value)
    - for each dimension that has multiple possible string values, we will create a dimension using one-hot encoding
- create a class that represents a test
    - each test contains a training algorithm and arguments to run the training algorithm
    - the class contains a run function that performs k-fold cross validation to obtain a model with high accuracy relative to all models in the k-fold validation, then stores those values in the class
    - the class is therefore a cache where one can run and get results, or where one can get results in constant time if the test has already been ran
- create a list of instances of those tests and run them and produce a numpy array that contains all test results

## Details we Looked for
- SVM
    - for rbf and for linear kernelrs, we did not have many options beside changing the cost coefficient, C, which is used as a regularization scalar
    - for the polynomial kernel, we tried combinations of degree and C
- Logistic Regression
    - for both ridge and lasso regression, we tried different regularization values
    - for lasso regression, we plotted the coefficients of the best model we found to see which parameters were irrelevant
- Neural Network
    - We tried using the algorithms we learned in class –Stochastic GD and Logistic Activation- however we quickly learned that they'd immediately become oversaturated (this is not to say what we learned in class is unusable, what we learned will naturally lead us to derive the optimizations that others made to improve neural networks)
    - We ran combinations of structures and regularization terms, and found that the hidden layer structure (4,3) with a high ∆ with relu activation worked best
    - After learning this, we used these arguments to compare different initial weights, and we achieved accuracy in the high 0.60s

## Issues we Dealt With
- With our original data, every prediction we made was entirely composed of one class – the models said yes to everything; we solved this by:
    - undersampling the yes' so there was an equal amount of yes' and nos
    - picking new dimensions
    - performing k-fold cross validation
- The first Neural Networks we tried had much larger training accuracies than test accuracies – the classic sign of an overfit; we solved this by introducing regularization and trying different ∆ values


## Running This Notebook
### Steps
```
python3 -m venv ./venv
source venv/bin/activate
pip install -r requirements.txt

# open this notebook in a Jupyter processor
```
### Links
- download [python3.9.4](https://www.python.org/downloads/release/python-394/)
- download [VSCode and its Jupyter processing extension](https://marketplace.visualstudio.com/items?itemName=ms-toolsai.jupyter)