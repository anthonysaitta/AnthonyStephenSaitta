# RapidMiner_PersonalLoan
RapidMiner Decision Tree - Personal Loan Acceptance 
The XML and XLSX files both relate to the RapidMiner Personal Loan acceptance. 
The goal was to create a predictive machine model 
#Understanding the Data and Data Cleaning/Process 
  The Excel file contains 7 tabs named: 
    1) Description
    2) Data_Source
    3) Data_AllNumeric
    4) Correlation
    5) Data_BinominalMix
    6) Data_COMPLETELY_Binominal
    7) FINAL
1.	Data Preprocessing: Excel 
  a.	I examined the 5000 rows from the source file and looked for any data that did not logically fit into the business process.  
    i.	I deleted 52 rows because the number of years of experience Ire negative values. 
ii.	I made this decision because of the large volume of data and the fact that 52 rows represented only 1.04% of the data. 
  b.	Columns Ire added for education with binominal ansIrs, namely: UG Degree, G Degree, and AP Degree.  
i.	Personal loan was set to YES/NO for the purpose of making analysis in RapidMiner easier.  
  c.	The next step, after taking out obvious errors, was to look holistically at the data provided: 
  the ranges, comparison of numerical variables, and how to convert the 1/0 data into binominal or
  polynomial to make evaluation proper for our given data set. This led to the need for a control model (the source) and four others: 
    i.	all numeric data 
    ii.	mixture of numeric variables for the continuous variables and binominal for 1/0 options
    iii.	all binominal data (through use of binning)
    iv.	The final data choice (Using Tab 6 data, but standardized in RapidMiner) 
  d.	After these four conversions, I ran the data analysis through a correlation matrix in excel to find the 
  values with the highest correlation to the target variable.  
  e.  Tab 7, FINAL, was created as a combination: using Tab 5, but with binning/normalization done in RapidMiner.  
  After this step, the preprocessing portion of the project was set to begin.  
#2.	Feature Selection and Engineering in RapidMiner
  a.	With the data thoroughly cleaned and a modified version of the source created, the next step commenced with 
  the use of RapidMiner to test the data and see if our model predicted what customers would likely accept a personal loan.  
  b.	the decision tree process began with choosing the Cross-Validation package from RapidMiner.  
  Within the package Ire three functions: Decision Tree, Apply Model, and Performance. 
  The first iteration had the following parameters:  
  i. Decision Tree
    1.	Maximal Depth – 10 
    2.	Confidence - .1
    3.	Minimal Gain – 0.015
    4.	Apply Model 
    5.	Performance
#Results and Engineering of Variables 

#For the fourth model I used the optimization tools and deleted the outlier analysis function.  
The optimized parameters Are: 
Decision Tree.criterion	= gain_ratio
Decision Tree.confidence	= 0.1
Decision Tree.minimal_gain	= 0.01
Decision Tree.minimal_leaf_size	= 5
Decision Tree.maximal_depth	= 18

The confusion matrix was: 
accuracy: 97.76% +/- 0.83% (micro average: 97.76%)
precision: 94.12% +/- 5.13% (micro average: 93.82%) (positive class: Yes)
recall: 82.35% +/- 7.63% (micro average: 82.29%) (positive class: Yes)

And the decision tree: 
CCAvg > 3.956: Yes {No=0, Yes=7}
CCAvg ≤ 3.956
|   Mort > 5.002: Yes {No=2, Yes=11}
|   Mort ≤ 5.002
|   |   Income > 0.860
|   |   |   G Degree = No: No {No=557, Yes=67}
|   |   |   G Degree = Yes
|   |   |   |   Income > 0.925: Yes {No=0, Yes=298}
|   |   |   |   Income ≤ 0.925
|   |   |   |   |   Income > 0.882: Yes {No=6, Yes=8}
|   |   |   |   |   Income ≤ 0.882: No {No=11, Yes=5}
|   |   Income ≤ 0.860
|   |   |   CCAvg > 0.580
|   |   |   |   CD Account = No
|   |   |   |   |   Income > 0.405
|   |   |   |   |   |   G Degree = No: No {No=51, Yes=5}
|   |   |   |   |   |   G Degree = Yes
|   |   |   |   |   |   |   CCAvg > 1.524: Yes {No=0, Yes=6}
|   |   |   |   |   |   |   CCAvg ≤ 1.524
|   |   |   |   |   |   |   |   CCAvg > 1.438: No {No=6, Yes=1}
|   |   |   |   |   |   |   |   CCAvg ≤ 1.438: Yes {No=7, Yes=22}
|   |   |   |   |   Income ≤ 0.405
|   |   |   |   |   |   CCAvg > 1.152: No {No=49, Yes=0}
|   |   |   |   |   |   CCAvg ≤ 1.152
|   |   |   |   |   |   |   Securities Account = No
|   |   |   |   |   |   |   |   Income > 0.188
|   |   |   |   |   |   |   |   |   Mort > 0.470: No {No=7, Yes=0}
|   |   |   |   |   |   |   |   |   Mort ≤ 0.470
|   |   |   |   |   |   |   |   |   |   CCAvg > 0.637
|   |   |   |   |   |   |   |   |   |   |   Income > 0.210: No {No=9, Yes=3}
|   |   |   |   |   |   |   |   |   |   |   Income ≤ 0.210: Yes {No=0, Yes=7}
|   |   |   |   |   |   |   |   |   |   CCAvg ≤ 0.637: No {No=5, Yes=0}
|   |   |   |   |   |   |   |   Income ≤ 0.188: No {No=74, Yes=7}
|   |   |   |   |   |   |   Securities Account = Yes: No {No=13, Yes=0}
|   |   |   |   CD Account = Yes: Yes {No=6, Yes=20}
|   |   |   CCAvg ≤ 0.580
|   |   |   |   Income > 0.709
|   |   |   |   |   Family > 0.966
|   |   |   |   |   |   AP Degree = No: Yes {No=3, Yes=5}
|   |   |   |   |   |   AP Degree = Yes: No {No=11, Yes=2}
|   |   |   |   |   Family ≤ 0.966: No {No=63, Yes=6}
|   |   |   |   Income ≤ 0.709: No {No=3587, Yes=0}



