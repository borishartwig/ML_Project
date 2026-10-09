# Machine Learning Project – Personality Types

*Boris Hartwig*  

## Abstract  
   
This project takes a Kaggle dataset from the so called **Big Five Personality Test** 

## Data Cleaning
   
The Dataset contains 19,719 rows and 22 columns. Very little data is missing:
  
In the column **gender** 24 entries are missing; therefore we shall discard these for their small number.

In the column **hand**, 100 entries are missing; therefore we shall discard these for their small number.

In the age column, there appear birth years and some seemingly random large numbers. 
From Kaggle  info, we know that the dataset was created in 2008. We substract the year from the age entry. This leaves us with exactly 10 ages over 110 (assumed maximum age of a person), which we also discard.
 
The answers to the questions shall always be between 1 and 5, but there are a few scattered zeroes.
We discard these records as well and keep the remaining 19,599 records.  
