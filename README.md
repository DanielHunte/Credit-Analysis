# Credit-Analysis

## Goal
build a classification model to determine whether or not a loan applicant will receive a loan given some data about the loan and some objective data about an individual

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


## Presenting
- a 6 minute live presentation will be given to the class

## Dataset
- the original dataset is sourced from [kaggle](https://www.kaggle.com/kapoorshivam/credit-analysis)
- due to the large amount of data in the dataset, the original dataset is split into the following two files: current_app.csv and previous_app.csv
- considering we need to test our data quickly, we decided to keep every 5th row from each of these datasets, and to join only those rows
- after joining every 5th row, we decided to keep 25,000 examples, considering we are preferring testing speed over maximum accuracy in our case
- such data collection was performed using a script that leverages python3's sqlite3 library
- data processing is done entirely as part of our jupyter notebook – we left as much work as possible to be done in pandas


## Approach
- train models using three standard supervised classification algorithms and analyze the results of the models built from each algorithm
- multiple augmentations of each algorithm will be analyzed, such as different feature transformations and such as different regularization techniques

## Implementation
- clean data
    - transform our target dimension into a binary number (simplifying from multiple values to a single value)
    - for each dimension that has multiple possible string values, we will create a dimension using one-hot encoding
- create a class that represents a test
    - each test contains a training algorithm and arguments to run the training algorithm
    - results of run will be presented as a single-row numpy array (that can be hstacked onto the other results)
- create a list of instances of those tests and run them and produce a numpy array that contains all test results