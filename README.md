# Udacity capstone project: predicting the EBIDTA of Brazil's largest companies

## Libraries

The code presented in this repository was written in Python 3. To work, it requires the following Python packages:

- Pandas
- Numpy
- Math 
- Seaborn
- Plotly
- Matplotlib
- Sklearn
- Statsmodels

## Introduction and project motivation
Every year (for 48 years now), the Brazilian fortnightly magazine Exame, that specializes in business and technology and is published by Editora Abril, releases a study called ["Melhores e Maiores" (Best and Largest)](https://mm.exame.com/), with a ranking of Brazil's 500 largest companies, based on their net profits. 

In the latter it was established that several indicators available for the set of Brazil's 500 largest companies in the 2015-2019 period - such as "Sales profitability in %", "Adjusted profit in US* million" and "EBITDA in US* million" - reflect a crisis scenario. 

## File Descriptions
- Capstone Notebook.ipynb: The code contained in this Jupyter notebook cleans and prepares the data, carries out the EDA analysis and generates the Machine Learning regression model. 
- data: The folder contains the exame500.csv, in which the data for the project is stored.

## Methodology
### 1. Data cleaning and preprocessing
I opted to perform the data cleaning before the EDA, as the data in the original set was in Portuguese. This step consisted in translating columns, column values and dropping some columns where the number of NANs was larger than 1000.

### 2. Exploratory Data Analysis

The EDA Analysis permits some crucial conclusions. As can be seen in the graph below, for the vast majority of data points the Adjusted net income in US$ million has been small. It is also noteworthy that there are more companies with a negative one than a slightly smaller than average one, which reflects the fact that the period in consideration has been of economic crisis.

<p align="center">
  <img width="80%" height="100%" src="https://github.com/ebelingbarros/udacity_capstone_project/blob/main/figure1.png"> 
</p> 

The indicator EBITDA (Earnings Before Interest, Taxes, Depreciation, and Amortization) is a measure of a company's profitability. As suggested by the Graph below, the fact that it has been low or negative for most companies reflects that this is a period of crisis.

<p align="center">
  <img width="80%" height="100%" src="https://github.com/ebelingbarros/udacity_capstone_project/blob/main/figure2.png"> 
</p> 

This graph tells us that the most profitable companies in terms of its EBITDA are either private Brazilian or foreign. As expected, SEOs have a lower EBITDA but may also have huge Net sales in US$ million.

<p align="center">
  <img width="80%" height="100%" src="https://github.com/ebelingbarros/udacity_capstone_project/blob/main/figure3.png"> 
</p> 

### 3. Building the model

The main goal of this project is to create a Machine Learning model capable of predicting the "EBITDA in US* million" and also in establishing its main determinants. Because of the conclusions obtained in the EDA, a preliminary step before creating the Machine Learning model is to estimate OLS estimations for the dependent variable and the chosen independent variables, 'Net working capital in US* million', 'Net sales US* million', 'Sales profitability (perc.)", 'Employees', 'Long term indebtedness (perc.)' considering subsets of the dataframe according to the companies' equity control (Private Brazilian, Foreign and SEOs). It is found that although the results are diverging, the aggregate dataframe has the best parameters and results. 

For running the model four of Sklearn's estimators are recruited: Linear Regression, Random Forest, SGDR and Bayesian. 

### 4. Model Evaluation

With the suprising exception of the Random Forest regressor, the results are solid, with the "EBITDA in US* million" being estimated in the 189- range. Another surprising result is that the indicator "Net working capital in US* million" has been found to have a negative relationship with the dependent variable "EBITDA in US* million".


## Conclusion



## Next steps








