# instructions
## follow these instructions
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

