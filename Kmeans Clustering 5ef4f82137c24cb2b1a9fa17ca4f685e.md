# Kmeans Clustering

- Dimentionality Reduction
- Clustring

    > Group similar instances together into clusters. a great tool for customer segmentaion, recommender systems , search engines, image segmentation and more

- Anamoly reduction

    > The objective is to learn what “normal” data looks like, and then use that to
    detect abnormal instances, such as defective items on a production line or a new trend in a time serie

- Density estimation

    > This is the task of estimating the probability density function (PDF) of the random process that generated the dataset. Density estimation is commonly used for anomaly detection: instances located in very low-density regions are likely to be anomalies. It is also useful for data analysis and visualization

These are some of the most common unsupervised tasks.

In this article we are going to get deep into the first one "Clustring".

Before get into unsupervised learning its important to note the difference between working with labled and unlabled datasets. Imagine we are going to gropu different flowers. Consider the figure below. In the left we have a labled dataset and in the right we have the same dataset without the lables. 

![Kmeans%20Clustering%205ef4f82137c24cb2b1a9fa17ca4f685e/Untitled.png](Kmeans%20Clustering%205ef4f82137c24cb2b1a9fa17ca4f685e/Untitled.png)

When your dataset is labled you can use common classification algorithms such as Logestic regression , SVM and Random Forrest Classifiers. but with the right dataset the story is different.

# Clustering

There is no universal definition of what a cluster is: it really depends on the context,
and different algorithms will capture different kinds of clusters. 

Some algorithms look for instances centered around a particular point, called a centroid. Others look for continuous regions of densely packed instances: these clusters can take on any
shape. Some algorithms are hierarchical, looking for clusters of clusters. And the list
goes on

Instead of assigning each instance to a single cluster, which is called hard clustering, it
can be useful to give each instance a score per cluster, which is called soft clustering.
The score can be the distance between the instance and the centroid;

## Kmeans

---

Useful for Dimensiotanlity reduction

```jsx
from sklearn.cluster import KMeans
k = 5
kmeans = KMeans(n_clusters=k)
y_pred = kmeans.fit_predict(X)

* kmeans.cluster_centers_
* kmeans.predict(X_new) 
* kmeans.transform(X_new)

//the KMeans class, the **transform()** method measures the distance from each instance to every centroid

kmeans = KMeans(n_clusters=5, init=good_init, n_init=1)
kmeans.inertia_
kmeans.score(X) --> Negative output because the "greater is better" rule.
```

The default algorithm that scikit learn uses is the 2003 version of it which accelerates by avoiding unnecessary distance calculations.

- kmeans is guranteed to converge but may not find the best solution.

    **n_init** : number of times to run the algorithm, each time with different random initializations

    **n_init ≠1** —> (default 10) avoid local optimum

- **inertia** : kmeans performance mteric

    The mean squared distance between each instance and its closest centroid

Computational Comlexity! 

The computational complexity of the algorithm is generally linear
with regard to the number of instances m, the number of clusters k,
and the number of dimensions n. 

However, this is only true when the data has a clustering structure. If it does not, then in the worstcase scenario the complexity can increase exponentially with the
number of instances. In

**K++ means**

- Choose first centroid C1 uninformly at random from the dataset
- Choose the next centroid base on the probabilty function so that the probablity of choosing a ppoint that is further from this centriod will be greater.
- Do the same untill you choose K centriods.

---

**Mini Batch Kmeans**

This speeds up the algorithm typically by a factor of three or four and makes it
possible to cluster huge datasets that do not fit in memory.

```jsx
from sklearn.cluster import MiniBatchKMeans
minibatch_kmeans = MiniBatchKMeans(n_clusters=5)
minibatch_kmeans.fit(X)
```

As the number of clusters increase, The Mini Batch Kmeans is faster compared to regualr Kmeans but its inertia gets slightly worse

Choosing K :

- elbow method: As we increase the K, the inertia gests lower and lower. For isntance if the right k is 5 you might see that when you increase k from 1 to 8, first it drops so quickly as we increase up to 4, then it decreases much slowely. The resulted curve shape is like an arm and the elbow can be the answer.
- Silhouette score: the mean shilhouette coefficient over all the instances.

    The silhouette coefficient can vary between –1 and +1.

    A coefficient close to +1 means that the instance is well inside its own cluster and far
    from other clusters, while a coefficient close to 0 means that it is close to a cluster
    boundary, and finally a coefficient close to –1 means that the instance may have been
    assigned to the wrong cluster.

    To compute the silhouette score, you can use Scikit-Learn’s silhouette_score()
    function, giving it all the instances in the dataset and the labels they were assigned:

    ```jsx
    >>> from sklearn.metrics import silhouette_score
    >>> silhouette_score(X, kmeans.labels_)
    0.655517642572828
    ```

    - Silhouette diagram

    Each diagram contains one knife shape per cluster. The shape’s height indicates the number of instances the cluster contains, and its width represents the sorted silhouette coefficients of the
    instances in the cluster (wider is better). 

    ![Kmeans%20Clustering%205ef4f82137c24cb2b1a9fa17ca4f685e/Untitled%201.png](Kmeans%20Clustering%205ef4f82137c24cb2b1a9fa17ca4f685e/Untitled%201.png)

    > This is because K-Means prefers clusters of similar sizes.

    ![Kmeans%20Clustering%205ef4f82137c24cb2b1a9fa17ca4f685e/Untitled%202.png](Kmeans%20Clustering%205ef4f82137c24cb2b1a9fa17ca4f685e/Untitled%202.png)

    ![Kmeans%20Clustering%205ef4f82137c24cb2b1a9fa17ca4f685e/Untitled%203.png](Kmeans%20Clustering%205ef4f82137c24cb2b1a9fa17ca4f685e/Untitled%203.png)

    Given the fact above , while using fewr than 8 clusters, although the red color is a falshy color compared to its surroundings, the kmeans algorithm fails to detect it.

Kmeans perform poorly when the clusters are different in size . densities or have nonspherical shapes. even having a low inertia the solution that algo finds might be terrible and other clustering models might perform better. For instance with ellistical clusters with different sizes, Gaussian mixture models work great.

Use Kmeans in Semi supervised Learning with lable propagation