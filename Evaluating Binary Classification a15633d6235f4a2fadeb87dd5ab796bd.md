# Evaluating Binary Classification

## Precision , Recall

```jsx
from sklearn.model_selection import cross_val_predict

from sklearn.metrics import confusion_matrix

from sklearn.metrics import precision_recall_curve
from sklearn.metrics import roc_curve

from sklearn.metrics import roc_auc_score
from sklearn.metrics import precision_score, recall_score
from sklearn.metrics import f1_score
f1_score(y_train_5, y_train_pred) , recall_score(y_train_5, y_train_pred)

```

> A trivial way to have perfect precision is to make one single positive prediction and ensure it is correct

![Evaluating%20Binary%20Classification%20a15633d6235f4a2fadeb87dd5ab796bd/Untitled.png](Evaluating%20Binary%20Classification%20a15633d6235f4a2fadeb87dd5ab796bd/Untitled.png)

The F1 score is the harmonic mean of precision and recall (Equation 3-3). Whereas the regular mean
treats all values equally, the harmonic mean gives much more weight to low values.

> The classifier will only get a high F1 score if both recall and precision are high.

instead of using .predict we can call .descision_function and then set a threshold manually like below :

```python
y_scores = sgd_clf.decision_function([some_digit])
// output : array([2412.53175101])
threshold = 8000
y_some_digit_pred = (y_scores > threshold)
// raising the threshold decreases recall.
```

### **How do you decide which threshold to use?**

First, use the **cross_val_predict()** function to get the scores of all instances in the training set, but this time specify that you want to return decision scores instead of predictions:

```jsx
y_scores = cross_val_predict(sgd_clf, X_train, y_train_5, cv=3,
method="decision_function")

precisions, recalls, thresholds = precision_recall_curve(y_train_5, y_scores)

plt.plot(thresholds, precisions[:-1], "b--", label="Precision")
plt.plot(thresholds, recalls[:-1], "g-", label="Recall")
plt.show()
```

- Precision may sometimes go down when you raise the threshold (although in general it will go up)
- Recall can only go down when the threshold is increased, which explains why its curve looks smooth.

Take a look at pr curve nad You will probably want to select a precision/recall trade-off just before that drop.

```jsx
threshold_90_precision = thresholds[np.argmax(precisions >= 0.90)]

y_train_pred_90 = (y_scores >= threshold_90_precision)
```

## ROC curve

The receiver operating characteristic (ROC) curve is another common tool used with
binary classifiers. 

The ROC curve plots the true positive rate (another name for recall) against the false positive rate (FPR).

> FPR = 1 - specificity (TNR)

```java
y_scores = sgd_clf.decision_function([some_digit])

fpr, tpr, thresholds = roc_curve(y_train_5, y_scores)

plt.plot(fpr, tpr, linewidth=2, label=label)
plt.plot([0, 1], [0, 1], 'k--') //purely Random classifier 

plt.show()
```

Once again there is a **trade-off**: the higher the recall (TPR), the more false positives
(FPR) the classifier produces.

### AUC (area under the curve )

A perfect classifier will have a ROC AUC equal to 1, whereas a purely random classifier will
have a ROC AUC equal to 0.5.

```jsx
roc_auc_score(y_train_5, y_scores)
```

![Evaluating%20Binary%20Classification%20a15633d6235f4a2fadeb87dd5ab796bd/Untitled%201.png](Evaluating%20Binary%20Classification%20a15633d6235f4a2fadeb87dd5ab796bd/Untitled%201.png)

![Evaluating%20Binary%20Classification%20a15633d6235f4a2fadeb87dd5ab796bd/Untitled%202.png](Evaluating%20Binary%20Classification%20a15633d6235f4a2fadeb87dd5ab796bd/Untitled%202.png)

Random Forest Classifier class does not have a decision_function() method. Instead, it has  predict_proba() method.

### **predict_proba()**

Between predict_proba and descision_function, Scikit-Learn classifiers generally have one or the other, or both. The predict_proba() method returns an array containing a row per instance and a column per class, each containing the probability that the given instance belongs to the given class (e.g., 70% chance that the image represents a 5):

```java
from sklearn.ensemble import RandomForestClassifier

forest_clf = RandomForestClassifier(random_state=42)

y_probas_forest = cross_val_predict(forest_clf, X_train, y_train_5, cv=3,
method="predict_proba")

y_scores_forest = y_probas_forest[:, 1] // score = proba of positive class
fpr_forest, tpr_forest, thresholds_forest = roc_curve(y_train_5,y_scores_forest)
```

## PR vs ROC curve

As a rule of thumb, you should prefer the PR curve whenever

the positive class is rare        or          when you care more about the false positives than
the false negatives. Otherwise, use the ROC curve.