# Udacity capstone project: predicting the EBIDTA of Brazil's largest companies

## Libraries

The code presented in this repository was written in Python 3. To work, it requires the following Python packages: `Pandas`, `Numpy`, `Math`, `Seaborn`, `Plotly`, `Matplotlib`, `Sklearn` and `Statsmodels`.

## Introduction, project motivation and data
Every year (for 48 years now), the Brazilian fortnightly magazine Exame, that specializes in business and technology and is published by Editora Abril, releases a study called ["Melhores e Maiores" (Best and Largest)](https://mm.exame.com/). It is a ranking of Brazil's 500 largest companies, based on their net profits. In its website, Exame makes available the ranking of the 500 largest companies for the 2015-2019 period, and extensive data on their level of revenues, profits, and financial health. This is a selection of the data that is available in the data set:

- Rank                                         
- Sector                                       
- Net sales in US$ million                         
- Net sales percentage growth                      
- Legal net income US$ million                
- Adjusted profit US$million                 
- Sales profitability percentage
- Net working capital in US$ million             
- General indebtedness percentage
- Long term indebtedness percentage
- No. of employees                                  
- Wages and charges US$million               
- Ebitda in US$ million                     
- Equity control                               

As will be seen in the EDA, several indicators available for the set of Brazil's 500 largest companies in the 2015-2019 period - such as "Sales profitability in %", "Adjusted profit in US* million" and "EBITDA in US* million" - appear to reflect a crisis scenario.  In this context, the objective of this project is to analyse whether the data available in Exame's ranking on Brazil's top 500 companies for the 2015-2019 scenario can indeed be interpreted as markers of a crisis and what are its main drivers. The questions that I attempt to answer are:

**- Is it possible to predict the EBITDA in US$ million (Earnings Before Interest, Taxes, Depreciation, and Amortization), which is a measure of profitability, of Brazilian's largest companies? Can the prediction be used as an indicator of economic crisis?**

**- What are the drivers of EBITDA and, hence, most important endogenous determinants of the companies' crisis?**

**- In a high indebtedness scenario, are companies that have a larger degree of maneuvre for investments, as measured by the Net working capital in US$ million, more profitable** 

**- Are there differences in profitability between private Brazilian companies, foreign controlled ones, and State-Owned Enterprises?**              

To answer these questions, I will perform an EDA and employ Machine Learning models to predict the "EBITDA in US$ million" and its drivers, which are measured by the parameters of the model.  

## File Descriptions
- [capstone_notebook.ipynb](https://github.com/ebelingbarros/udacity_capstone_project/blob/main/capstone_notebook.ipynb): The code contained in this Jupyter notebook cleans and prepares the data, carries out the EDA analysis and generates the Machine Learning regression model. 
- data: The folder contains the [exame500.csv](https://github.com/ebelingbarros/udacity_capstone_project/blob/main/data/exame500.csv) csv file, in which the data for the project is stored.

## Methodology
### 1. Data cleaning and preprocessing
I opted to perform the data cleaning before the EDA, as the data in the original set was in Portuguese. This step consisted in translating columns, column values and dropping some columns where the number of NANs was larger than 1000. 

### 2. Exploratory Data Analysis

The EDA Analysis permits some crucial conclusions. As can be seen in the graph below, for the vast majority of data points the Adjusted net income in US$ million has been small. It is also noteworthy that there are more companies with a negative one than a slightly smaller than average one, which reflects the fact that the period in consideration has been of economic crisis. Another possible conclusion is that Brazilian companies from Exame's ranking are generally small in terms of Adjusted Net Income in US$ million.

<p align="center">
  <img width="80%" height="100%" src="https://github.com/ebelingbarros/udacity_capstone_project/blob/main/figure1.png"> 
</p> 

As suggested by the Graph below, the fact that the EBITDA in US$ million has been low or negative for most companies reflects that this is a period of crisis. Again, this also might be interpreted of a marker of the companies' small relative size.

<p align="center">
  <img width="80%" height="100%" src="https://github.com/ebelingbarros/udacity_capstone_project/blob/main/figure2.png"> 
</p> 

The following graph conveys that although this is a period of crisis, **it is also one of recovery**. While the indicator "Net sales in US million" is strongly suggestive of a crisis scenario in the two first years of the dataset, the recovery of the "EBITDA in US million" towards the end of the period indeed suggests a recovery.

<p align="center">
  <img width="80%" height="100%" src="https://github.com/ebelingbarros/udacity_capstone_project/blob/main/figure4.png"> 
</p> 

Similar conclusions are reached by the following graph. While the oscillations in the indicator "Net sales perc growth" and the increase in "General Indebment" suggest a crisis, the rise in "Sales profitability perc" suggests a recovery.

<p align="center">
  <img width="80%" height="100%" src="https://github.com/ebelingbarros/udacity_capstone_project/blob/main/figure5.png"> 
</p> 

This graph tells us that the most profitable companies in terms of its EBITDA are either private Brazilian or foreign. As expected, SEOs have a lower EBITDA but may also have huge Net sales in US$ million.

<p align="center">
  <img width="80%" height="100%" src="https://github.com/ebelingbarros/udacity_capstone_project/blob/main/figure3.png"> 
</p> 

### 3. Building the model

While one question could be answered with the EDA ( Are there differences in profitability between private Brazilian companies, foreign controlled ones, and State-Owned Enterprises), the most important part of this project is the creation a Machine Learning model capable of predicting the "EBITDA in US$ million" and also in establishing its main determinants. Because of the conclusions obtained in the EDA, a preliminary step before creating the Machine Learning model is to estimate OLS estimations for the dependent variable and the chosen independent variables, 'Net working capital in US* million', 'Net sales US* million', 'Sales profitability (perc.)", 'Employees', 'Long term indebtedness (perc.)' considering subsets of the dataframe according to the companies' equity control (Private Brazilian, Foreign and SEOs). It is found that although the results are diverging, the aggregate dataframe has the best parameters and results. 

For running the model four of Sklearn's estimators are recruited: Linear Regression, Random Forest, SGDR and Bayesian. 

### 4. Model Evaluation

With the suprising exception of the Random Forest regressor, the results are solid, with the "EBITDA in US$ million" being estimated in the US$191-280 million range. Another surprising result is that the indicator "Net working capital in US* million" has been found to have a negative relationship with the dependent variable "EBITDA in US* million".

<p align="center">
  <img width="80%" height="100%" src="https://github.com/ebelingbarros/udacity_capstone_project/blob/main/results_synthesis.png"> 
</p> 

To have a more nuanced picture of the data, I decide to run the models once more for every individual year for the Linear regression case. While it is possible to estimate  the EBITDA for the period as a whole, it gets more complicated for the individual years' estimation. For the estimation technique for individual years - performed with linear regression - relative result robustness as measured by the R2 and the RMSE is only reached in 2015, 2017, and 2018. This makes drawing conclusions more difficult, as the proposed model might be unsuitable. Nonetheless, it is interesting to notice that the predicted mean EBITDA grew from 2015 to 2017, signalling the beginning of a possible recovery.

<p align="center">
  <img width="80%" height="100%" src="https://github.com/ebelingbarros/udacity_capstone_project/blob/main/results_2.png"> 
</p> 

## Conclusions and next steps

This project has developed ML regression models capable of predicting the likely EBITDA in US$ million of top 500 Brazilian companies. The model also estimated the drivers of profitability as measured by the EBITDA in US$ million. It was seen that the Net working capital in US$ million, which is a precondition to carry out investment, is negatively correlated with the EBITDA. This suggests that companies that have a larger degree of maneuvre to invest do not necessarily are more profitable. Before that, in the EDA part, it was also seen that private Brazilian companies and foreign controlled ones tend to be more profitable that SEOs. 

A possible next step is to gather investments data from these Brazilian companies' websites to answer the question if companies that invest more are profitable or not. It should be noted that this step would require lots of time because data mining tools are difficult to apply to the universe of top 500 Brazilian companies due to the absence of data for some companies and the fact that the data is very scattered. 
 
As a last word, I would like to state that this project scope was quiet unambitious in terms of the proposed business question. My objective here was less to develop an advanced framework to understand the behavior of top Brazilian companies than to train some of the things that have been learned in the course, chiefly the practice of utilizing functions in the development of ML models. 

The entire Medium post regarding these conclusions can be read [here](https://ebelingbarros.medium.com/predicting-the-ebidta-of-brazils-500-largest-companies-c2e70bc58cab). 


