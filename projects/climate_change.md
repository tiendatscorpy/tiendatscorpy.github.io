# Climate Change Dashboard

Keyword: **Heroku, Flask, Plotly, Facebook Prophet, Python**

[Website](https://climate-change-c3250-2020.herokuapp.com/) - [Project Report (pdf)](../pdf/climate.pdf)

## Project Description

This is a capstone project for **Data Science Project (CS-C3250)** course @Aalto University. The goal of this project was to produce a website that portrays climate change data smoothly to interested viewers. By using data points from multiple different sources, the site undoubtedly shares the most accurate and up-to-date information we could find. In order to accurately portray the effects climate change has had on the planet, we chose to illustrate data of CO2 emissions rising (along with other gases), the ice caps melting, which results in sea levels rising, the rising of temperatures, as well as included calculations that show how volcanic activity, El Niño, and other factors, are not the primary cause for the rise of CO2 in the atmosphere - but rather it is the human activity that has been the driving force.

## System Design

The website was built with a goal in mind to keep the architecture simple and hit the ground running as fast as possible. The Dashboard is hosted on Heroku hosting environment, due to its simplicity in deployment. Flask is used as a web server, and Plotly is used for interactive visualization. 

<img src="../images/climate_infra.png?raw=true"/>

## Results and Findings

In this section, we describe our findings as well as model performance on the dataset. EDA section can be found in the project report. The data has 398 rows and 10 columns in total, which includes variables such as 'ds', 'y', 'amo', 'co2', 'NINO1+2', 'NINO3', 'NINO4', 'nao', 'vei', 'ssn'. The naming convention are explained in the previous Correlation part. Due to the limited availability and poor quality of the data, the period of time in consideration was sliced down to 1984 - 2017. The train-test split was such that the train dataset was from January 1984 to December 2009, and the test set was on January 2010 to February 2017. The number of rows on the training set and test set are 312 and 86 rows, whose percentage on the total amount of rows are 78% and 22%. 

