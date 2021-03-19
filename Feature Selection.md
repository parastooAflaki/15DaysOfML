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

