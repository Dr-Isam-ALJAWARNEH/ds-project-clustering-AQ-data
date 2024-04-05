# instructions
## follow these instructions

[ ]

**NEW!** April 2, 2024

- TODO:
  - ```Simple Random Sampling (SRS)``` such as the one that is done here might be not sufficient!
  - Perform ```stratified-like sampling``` instead, similar to the one we've done in the class, on a granular level could be based on geohash (take equal fractions from each geohash independently) or on a coarser level based on neighborhood, borough, or any other offical city administrative division (take equal fractions from each administrative division independently),
  - Thereafter, you do all the other steps that follow, normalization, scaling, clustering, visualization, etc., and you compare the results between SRS and stratified-like geospatial sampling!

  You need to draw several x-y figures to capture those comparisons, in the x-axis is the sampling fraction: 20%, 40%, 60%, 80%, 90%,,,, and in the y-axis probably the silhouette (for both SRS and stratified-like sampling schemes) using for example column graphs or line graphs. See example figure in the comments below.
    - You have based your distance calculation by applying the stock version of DBSCAN in sickit-learn as-is, relying on using ```haversine``` as a distance metric to calculate haversine distances between coordinates (longitudes/latitudes pairs)
  > the attention that should be given in this case is that you did not capture any statistics regarding the distribution of the pm25 values (our target variable), you could for example capture the histograms of those values.
  Read more about possible values of ```pm2.5``` in this reference [PM2.5 particles in the air](https://www.epa.vic.gov.au/for-community/environmental-information/air-quality/pm25-particles-in-the-air). This means that you need to create a histogram showing the density of each bracket, your binning strategy should rely on the community definition of ranges of values. For example, binning example is the follwoing: Less than 25, 25–50, 50–100, 100–300, More than 300. Simialr to what appears in the following figure[in notebook].
  
    - Also, draw histograms showing the same binning and density of pm2.5 values in each neighborhood in your data. By the way, how many neighborhoods you have in your data?!
  > this is important as it will inform us about the fact wether nearby locations are having similar pm25 values. Why do we need to do this, because it is only in that case we consider those as a cluster, since they are geographiclly nearby, and also having simialr feature values (pm25 in this case). So what you need to do next is the following:
  - .. ```Extract and normalize several features```, similar to what has been done in the following tutorial, read specifically [Extending DBSCAN beyond just spatial coordinates](https://musa-550-fall-2020.github.io/slides/lecture-11A.html), thereafter ```Run DBSCAN to extract high-density clusters``` passing as an argument to the DBSCAN the new ```scaled features```, probably something like ```cores, labels = dbscan(features, eps=eps, min_samples=min_samples)``` . notice passing features (including pm25, longitude, latitude) instead of simply the coordinates.
  - having done this novel distance calculation (based on geometrical distance and pm25 values distance), calculate again the ```silhouette_score```, and check wether you obtain a higher accuracy (higher silhouette_score values) or not!

  > **N.B.** we are able to do this because of the definition of ```metric``` in DBSCAN which says **metric: The metric to use when calculating distance between instances in** a ```feature array``` so, it  a distance between several features is possible, given a ```feature array```, so put your scaled features in a feature array.

  - one importance configurable parameter in this case is the distance metric.
  > you can use instead 
    - most importantly the following : ```From scikit-learn: [‘cityblock’, ‘euclidean’, ‘l1’, ‘l2’, ‘manhattan’].```
    - and probably aome of the following ```From scipy.spatial.distance: [‘braycurtis’, ‘canberra’, ‘chebyshev’, ‘dice’, ‘hamming’, ‘jaccard’, ‘kulsinski’, ‘rogerstanimoto’, ‘russellrao’,, ‘sokalmichener’, ‘sokalsneath’, ```

  - then, having permutate this configurable parameter, capture the ```silhouette_score``` and compare, then draw an x-y figure such as the following [figure attached in notebook], (```you can do those graphs in MS excel after capturing the numbers```):
  - Provide a detailed explanation of the values you obtained for ```Silhouette Coefficient```
    - take some insights from [scikit-learn docs](https://scikit-learn.org/stable/modules/generated/sklearn.metrics.silhouette_score.html#sklearn.metrics.silhouette_score)
    - That is to say, >
    > "The best value is 1 and the worst value is -1. Values near 0 indicate overlapping clusters. Negative values generally indicate that a sample has been assigned to the wrong cluster, as a different cluster is more similar."
  - you need to do more analytics and Exploratory Spatio-Temporal Data Analytics (ESTDA,  read specifically [Extending DBSCAN beyond just spatial coordinates](https://musa-550-fall-2020.github.io/slides/lecture-11A.html), thereafter, for example ```Identify the 5 largest clusters``` , ```Get mean statistics for the top 5 largest clusters```, ```Visualize the top 5 largest clusters```, ```Visualizing one cluster at a time```.
- add other metrics from the [sklearn.metrics](https://scikit-learn.org/stable/modules/clustering.html#clustering-performance-evaluation), for example the following:
  > - ```Davies-Bouldin Index```, **Zero is the lowest possible score. Values closer to zero indicate a better partition.**
  for your experiment, we have obtained a number on par with 2.78!, which is very high! so probably your clustering scheme misses something! try different combinations of configurations (sampling scheme, distance methods, distance based on combination of features such as geographical long/lat and pm25 values), read my previous comments to get insights.
    - ```Calinski-Harabasz Index```. You have computed that already, but what is your explanation and reasoning of the results obtained!

-------------------------------------

1. [ ] run the example clustering code (DBSCAN)

2. [ ] read more about how DBSCAN works in scikit-learn
    > [DBSCAN scikit-learn](https://scikit-learn.org/stable/modules/generated/sklearn.cluster.DBSCAN.html)

3. [ ] you need to use ```Silhouette Coefficient ```for evaluation
    > ***"If the ground truth labels are not known, evaluation can only be performed using the model results itself. In that case, the Silhouette Coefficient comes in handy."***
    an example is here:
    [Demo of DBSCAN clustering algorithm](https://scikit-learn.org/stable/auto_examples/cluster/plot_dbscan.html#sphx-glr-auto-examples-cluster-plot-dbscan-py)

4. [ ] then you need to apply other algorithms such as [K-Means](https://scikit-learn.org/stable/modules/clustering.html#k-means),  [HDBSCAN](https://scikit-learn.org/stable/modules/clustering.html#hdbscan), and [OPTICS](https://scikit-learn.org/stable/modules/clustering.html#optics), then you need to compare the performance of those algorithms using several ```Clustering performance evaluation``` as below!
    ### Examples:
- [Demo of HDBSCAN clustering algorithm](https://scikit-learn.org/stable/auto_examples/cluster/plot_hdbscan.html#sphx-glr-auto-examples-cluster-plot-hdbscan-py)
- [Demo of OPTICS clustering algorithm](https://scikit-learn.org/stable/auto_examples/cluster/plot_optics.html#sphx-glr-auto-examples-cluster-plot-optics-py)
- [K-means Clustering](https://scikit-learn.org/stable/auto_examples/cluster/plot_cluster_iris.html#sphx-glr-auto-examples-cluster-plot-cluster-iris-py)
- 
5. [ ] Apply as much ```Clustering performance evaluation``` metircs as you can!
    > read more here:
        [Clustering performance evaluation](https://scikit-learn.org/stable/modules/clustering.html#clustering-performance-evaluation)

- bonus if you could apply [geosilhouettes](https://pysal.org/esda/notebooks/geosilhouettes.html)

------------------------------------




