# instructions
## follow these instructions
<!-- Task 2 -->
# [ ] Task 2! 
# `Update: April 7, 2024`
### `N.B.` references are available in the end of this instruction file!
# `Required OPTIMIZATION ==> IMPORTANT!`
## `TODO:` 

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
    - most importantly the following : ```From scikit-learn: [‘cityblock’, ‘euclidean’, ‘l1’, ‘l2’, ‘manhattan’].``` [sklearn.metrics.pairwise_distances](https://scikit-learn.org/stable/modules/generated/sklearn.metrics.pairwise_distances.html)
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
<!-- Task 3 -->
# [ ] Task 3!
## writing your paper
# reference paper
there is my recent paper [^10] `very similar` which you can use as a springboard to start writing your paper, I uploaded a copy  ` Efficient spark-based framework for big geospatial data query processing and analysis` [^10]. Use it as a starting point. However, you need also to cite our other papers detailed below!
# `IMPortant` test with more than one data, add NYC taxi mobility data (for journal paper, you need tests on more than one data):
[available online](https://github.com/IsamAljawarneh/datasets/tree/master/data), `nyc1.zip`
- start writing your paper, either for conferences or journal. For journal, use the `applied sciences` template atatched in the `target-venue` folder titled `applsci-template.dot`. (minimum 10 pages)
- or even, consider one of the following two conference (IEEE template for those conferences is attached) (minimum 6 pages)
    - [MCNA - Spain](https://mcna-conference.org/2024/committee.php)
    - [IDSTA - Croatia](https://idsta-conference.org/2024/calls.php)
1.  [ ] Include (cite appropriately) all of the following papers! reference papers include:
    # Category A : for sampling desing and Approximate Query Processing (AQP)
    > Spatial-aware approximate big data stream processing [^2] and
    > Polygon Simplification for the Efficient Approximate Analytics of Georeferenced Big Data [^3]
    > QoS-aware approximate query processing for smart cities spatial data streams. [^4]
    > Spatially representative online Big Data sampling for smart cities. [^5]
    # Category B: for spatial join procesing
    > SpatialSSJP: QoS-Aware Adaptive Approximate Stream-Static Spatial Join Processor [^6]
    > Efficient Integration of Heterogeneous Mobility-Pollution Big Data for Joint Analytics at Scale with QoS Guarantees [^7]
    > Efficiently integrating mobility and environment data for climate change analytics.[^8]
    > Efficient QoS-aware spatial join processing for scalable NoSQL storage frameworks. [^9]
    # Category C: clustering DBSCAN
    > Efficient spark-based framework for big geospatial data query processing and analysis [^10]
 
    [^1]: Al Jawarneh, I. M., Foschini, L., & Corradi, A. (2023, November). Efficient Generation of Approximate Region-based Geo-maps from Big Geotagged Data. In 2023 IEEE 28th International Workshop on Computer Aided Modeling and Design of Communication Links and Networks (CAMAD) (pp. 93-98). IEEE.
    [^2]: Al Jawarneh, I. M., Bellavista, P., Foschini, L., & Montanari, R. (2019, December). Spatial-aware approximate big data stream processing. In 2019 IEEE global communications conference (GLOBECOM) (pp. 1-6). IEEE. [available online](https://www.researchgate.net/profile/Isam-Al-Jawarneh/publication/339562314_Spatial-Aware_Approximate_Big_Data_Stream_Processing/links/5ff45764299bf14088708888/Spatial-Aware-Approximate-Big-Data-Stream-Processing.pdf)
    [^3]: Al Jawarneh, I. M., Foschini, L., & Bellavista, P. (2023). Polygon Simplification for the Efficient Approximate Analytics of Georeferenced Big Data. Sensors, 23(19), 8178.[available online](https://www.mdpi.com/1424-8220/23/19/8178)
    [^4]: Al Jawarneh, I. M., Bellavista, P., Corradi, A., Foschini, L., & Montanari, R. (2021). QoS-aware approximate query processing for smart cities spatial data streams. Sensors, 21(12), 4160. [available online](https://www.mdpi.com/1424-8220/21/12/4160)
    [^5]: Al Jawarneh, I. M., Bellavista, P., Corradi, A., Foschini, L., & Montanari, R. (2020, September). Spatially representative online Big Data sampling for smart cities. In 2020 IEEE 25th International Workshop on Computer Aided Modeling and Design of Communication Links and Networks (CAMAD) (pp. 1-6). IEEE.[presentation available online](https://isamaljawarneh.github.io/talks/CAMAD20.pdf)
    [^6]: Al Jawarneh, I. M., Bellavista, P., Corradi, A., Foschini, L., & Montanari, R. (2023). SpatialSSJP: QoS-Aware Adaptive Approximate Stream-Static Spatial Join Processor. IEEE Transactions on Parallel and Distributed Systems. [available online](https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=10309986)
    [^7]: Al Jawarneh, I. M., Foschini, L., & Bellavista, P. (2023). Efficient Integration of Heterogeneous Mobility-Pollution Big Data for Joint Analytics at Scale with QoS Guarantees. Future Internet, 15(8), 263. [available online](https://www.mdpi.com/1999-5903/15/8/263)
    [^8]:Al Jawarneh, I. M., Bellavista, P., Corradi, A., Foschini, L., & Montanari, R. (2021, October). Efficiently integrating mobility and environment data for climate change analytics. In 2021 IEEE 26th International Workshop on Computer Aided Modeling and Design of Communication Links and Networks (CAMAD) (pp. 1-5). IEEE.[presentation available online](https://isamaljawarneh.github.io/talks/CAMAD21.pdf)
    [^9]:Al Jawarneh, I. M., Bellavista, P., Corradi, A., Foschini, L., & Montanari, R. (2020). Efficient QoS-aware spatial join processing for scalable NoSQL storage frameworks. IEEE Transactions on Network and Service Management, 18(2), 2437-2449.[available online](https://isamaljawarneh.github.io/pubs/TNSM3034150.pdf)
    [^10]: Aljawarneh, I. M., Bellavista, P., Corradi, A., Montanari, R., Foschini, L., & Zanotti, A. (2017, July). Efficient spark-based framework for big geospatial data query processing and analysis. In 2017 IEEE symposium on computers and communications (ISCC) (pp. 851-856). IEEE. [available online](https://www.academia.edu/download/55478212/08024633.pdf)
---------------------------

<!-- Task 1 -->
# [ ] Task 1! 
1. [X] run the example clustering code (DBSCAN)

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
