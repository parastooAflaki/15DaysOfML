
What are Outliers ?
---
We will generally define outliers as samples that are exceptionally far from the mainstream of the data.

Outliers can have many causes, such as:

  * Measurement or input error.
  * Data corruption.
  * True outlier observation (e.g. Michael Jordan in basketball).

There is no precise way to define and identify outliers in general because of the specifics of each dataset. However we can use statistics to identify observationes which are unlikely but are not necessarily outlier. Then you must interpret these rare observationes and decide whether one of them is an outlier or not.

---

### The Interquartile Range Method

Not all data is normal or normal enough to treat it as being drawn from a Gaussian distribution.

A good statistic for summarizing a non-Gaussian distribution sample of data is the Interquartile Range, or IQR for short.

The IQR can be used to identify outliers by defining limits on the sample values that are a factor k of the IQR below the 25th percentile or above the 75th percentile. 

  * The common value for the factor k is the value 1.5.

  * A factor k of 3 or more can be used to identify values that are extreme outliers or “far outs” when described in the context of box and whisker plots.

---

### Automatic Outlier Detection
In machine learning, an approach to tackling the problem of outlier detection is one-class classification.

---

### LOF : Local outlier factor
A technique that attempts to harness the idea of nearest neighbors for outlier detection. Each example is assigned a scoring of how isolated or how likely it is to be outliers based on the size of its local neighborhood. 
