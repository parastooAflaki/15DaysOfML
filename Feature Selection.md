Feature Selection Methods
---
Feature selection is the process of reducing the number of input variables when developing a predictive model.
It's desirable to reduce the number of features for both reducing computational cost of model and improving its performance.

To summerize the content of this file, 
   * There are two main types of feature selection techniques: supervised and unsupervised, and 
        supervised methods may be divided into wrapper, filter and intrinsic.
   * Filter-based feature selection methods use statistical measures to score the correlation or dependence between input variables that
        can be filtered to choose the most relevant features.
   * Statistical measures for feature selection must be carefully chosen based on the data type of the input variable and the output or response variable.

An important distinction to be made in feature selection is that of supervised and unsupervised methods. When the outcome is ignored 
during the elimination of predictors, the technique is unsupervised. __Filter__ and __Wrapper__ methods however, are evaluated based on the performance
of the model on a hold out dataset.

* Filter Methods work based on the statistical relationship between each input feature and target.
* Wrapper Methods create multiple models with different subsets of features and select those features that result in best prformance
  according to a performance metric
  
 * Intrinsic Methods are built-in feature selection methods in some of the models, meaning that the model will only include 
    predictors that help maximize accuracy. In these cases, the model can pick and choose which representation of the data is best.
    
  ---
  
  * Note the difference between Feature Selection and Dimensionality Reduction :
   feature selection select features to keep or remove from the dataset,
   whereas dimensionality reduction create a projection of the data resulting in entirely new input features. As such, dimensionality reduction is an alternate to feature selection rather than a type of feature selection.

 ---
 ![image](https://user-images.githubusercontent.com/47450201/111804023-e9b7f400-88e4-11eb-8b78-ba3b6568a088.png)

  Statistics for Filter-Based Feature Selection Methods
 ---
  The choice of statistical measures is highly dependent upon the variable data types.
  Common input variable data types:
   
   * Numerical Variables
        * Integer Variables.
        * Floating Point Variables.
        
   * Categorical Variables.
        * Boolean Variables (dichotomous).
        * Ordinal Variables
        * Nominal Variables
---

* Numerical Input , Categorical Output: Classification Probelm
    * ANOVA correlation coefficient (linear)
    * Kendall’s rank coefficient (nonlinear)
* Categorical Input , Numerical Output : strange example of Regression Problem
    * you can use the same “Numerical Input, Categorical Output” methods, but in reverse.
* Categorical Input , Categorical Output: 

    * Chi-Squared test (contingency tables).
    * Mutual Information.
* Numerical Input , Numerical Output: Regression Probem

    * Pearson’s correlation coefficient (linear).
    * Spearman’s rank coefficient (nonlinear)
---
Some statistical measures assume properties of the variables, such as Pearson’s that assumes a Gaussian probability distribution to the observations and a linear relationship. You can transform the data to meet the expectations of the test and try the test regardless of the expectations and compare results.

---
* Scikit-learn privdes implementation of most useful statistical measures. for instance :
    * Pearson’s Correlation Coefficient: f_regression()
    * ANOVA: f_classif()
    * Chi-Squared: chi2()
    * Mutual Information: mutual_info_classif() and mutual_info_regression()
* Once you have calculated statistical measures for each input feature with the target, you can choose one of the below __Selection Methods__ provided by scikit-learn
  * Select the top k variables: SelectKBest
  * Select the top percentile variables: SelectPercentile


