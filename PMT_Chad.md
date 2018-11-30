---
title: "Proxy Means Test - Chad"
author: "Bill Olander, RBD"
date: "November 30, 2018"
output: 
  html_document:
    keep_md: true
---



### Key Points

1. Explored "Proxy Means Testing", using assessment data to predict food security indicators using easily observable/verifiable household characteristics for targeting of households
2. This method, largely fails accurately predict the FCS and Food Expenditures and misclassifies a large number of the food insecure households   
3. It's unlikely that selecting additional variables will improve the predictive power.  While more complicated methods/models could be explored to improve predictive power, this would defeat the purpose of PMT - which is to provide and easily interpretable method for scoring/categorization of households.

## Methods

Following Proxy Means Tests methods here: https://olc.worldbank.org/sites/default/files/1.pdf , used recent household assessment data for Burkina Faso, Chad, Mali, Niger and Senegal to:

1. Create a multiple linear regression (model) to predict the FCS and Food Expenditures using variables which are easily observable/collectable by enumerators (i.e. type of roof, possession of animals, sex of the head of household)
2. Using the model, create a predicted FCS/Expenditure for each household 
3. Create FCS/Expenditure quintiles for predicted and actual FCS/Expenditure scores
4. To assess accuracy, calculate the inclusion and exclusion error of the poorest 


*linear regression model to predict FCS in Chad using easily observable/verifiable household characteristics*

```r
summary(modelChad2)
```

```
## 
## Call:
## lm(formula = FCS ~ departement + alphabetisation_CM + toilette + 
##     Houetot + Machettetot + Brouettetot, data = Chad_2018_EFSA)
## 
## Residuals:
##     Min      1Q  Median      3Q     Max 
## -40.634 -11.071  -0.571   9.397  51.566 
## 
## Coefficients:
##                    Estimate Std. Error t value Pr(>|t|)    
## (Intercept)         45.3484     2.1686  20.911  < 2e-16 ***
## departement          4.8386     1.0900   4.439 1.02e-05 ***
## alphabetisation_CM   3.0236     1.0415   2.903  0.00379 ** 
## toilette            -3.6227     0.6624  -5.469 5.90e-08 ***
## Houetot              9.2524     1.1287   8.198 8.55e-16 ***
## Machettetot          8.2931     1.1216   7.394 3.30e-13 ***
## Brouettetot          5.9693     1.9027   3.137  0.00176 ** 
## ---
## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
## 
## Residual standard error: 14.25 on 886 degrees of freedom
## Multiple R-squared:  0.3204,	Adjusted R-squared:  0.3158 
## F-statistic: 69.62 on 6 and 886 DF,  p-value: < 2.2e-16
```

##Results

The following table present Actual vs Predicted Food Consumption Quintile Groups for each Country 

####Chad FCS Quintiles (Actual in rows/predicted in columns)
*52% of the poorest quintile were correctly classified by the prediction*
<table class="table" style="margin-left: auto; margin-right: auto;">
 <thead>
  <tr>
   <th style="text-align:left;">   </th>
   <th style="text-align:right;"> Predicted FCS Quintile 1 </th>
   <th style="text-align:right;"> Predicted FCS Quintile 2 </th>
   <th style="text-align:right;"> Predicted FCS Quintile 3 </th>
   <th style="text-align:right;"> Predicted FCS Quintile 4 </th>
   <th style="text-align:right;"> Predicted FCS Quintile 5 </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;font-weight: bold;"> Actual FCS Quintile 1 </td>
   <td style="text-align:right;"> 93 </td>
   <td style="text-align:right;"> 46 </td>
   <td style="text-align:right;"> 24 </td>
   <td style="text-align:right;"> 14 </td>
   <td style="text-align:right;"> 2 </td>
  </tr>
  <tr>
   <td style="text-align:left;font-weight: bold;"> Actual FCS Quintile 2 </td>
   <td style="text-align:right;"> 47 </td>
   <td style="text-align:right;"> 49 </td>
   <td style="text-align:right;"> 47 </td>
   <td style="text-align:right;"> 21 </td>
   <td style="text-align:right;"> 15 </td>
  </tr>
  <tr>
   <td style="text-align:left;font-weight: bold;"> Actual FCS Quintile 3 </td>
   <td style="text-align:right;"> 31 </td>
   <td style="text-align:right;"> 33 </td>
   <td style="text-align:right;"> 43 </td>
   <td style="text-align:right;"> 37 </td>
   <td style="text-align:right;"> 34 </td>
  </tr>
  <tr>
   <td style="text-align:left;font-weight: bold;"> Actual FCS Quintile 4 </td>
   <td style="text-align:right;"> 6 </td>
   <td style="text-align:right;"> 33 </td>
   <td style="text-align:right;"> 43 </td>
   <td style="text-align:right;"> 57 </td>
   <td style="text-align:right;"> 40 </td>
  </tr>
  <tr>
   <td style="text-align:left;font-weight: bold;"> Actual FCS Quintile 5 </td>
   <td style="text-align:right;"> 2 </td>
   <td style="text-align:right;"> 18 </td>
   <td style="text-align:right;"> 21 </td>
   <td style="text-align:right;"> 50 </td>
   <td style="text-align:right;"> 87 </td>
  </tr>
</tbody>
<tfoot>
<tr><td style="padding: 0; border: 0;" colspan="100%"><span style="font-style: italic;">Note: </span></td></tr>
<tr><td style="padding: 0; border: 0;" colspan="100%">
<sup></sup> Here is a general comments of the table. </td></tr>
<tr><td style="padding: 0; border: 0;" colspan="100%">
<sup>1</sup> Footnote 1; </td></tr>
<tr><td style="padding: 0; border: 0;" colspan="100%">
<sup>2</sup> Footnote 2; </td></tr>
<tr><td style="padding: 0; border: 0;" colspan="100%">
<sup>a</sup> Footnote A; </td></tr>
<tr><td style="padding: 0; border: 0;" colspan="100%">
<sup>b</sup> Footnote B; </td></tr>
<tr><td style="padding: 0; border: 0;" colspan="100%">
<sup>*</sup> Footnote Symbol 1; </td></tr>
<tr><td style="padding: 0; border: 0;" colspan="100%">
<sup>†</sup> Footnote Symbol 2</td></tr>
</tfoot>
</table>

## Discussion

As observed in the assesment data for 6 countries, the PMT method fails to accurately  predict/classify a large percentage of households.

Criticism of the approach (http://www.developmentpathways.co.uk/blog/poxy-means-testing-official/, https://www.unicef.org/socialpolicy/files/targeting-poorest.pdf) is it often not understood by beneficiaries and seen as a lottery system. 

Investing in more complicating models and methods for prediction will only lessen the interpretability of methods.  


