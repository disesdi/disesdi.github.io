-------

[home](https://disesdi.github.io/) \| [resources](https://disesdi.github.io/resources.html) \| <a href="https://github.com/disesdi/" target="_blank" rel="noopener noreferrer">github</a> \| <a href="https://anglesofattack.io/about.html" target="_blank" rel="noopener noreferrer">about</a>

-------

# Detecting Cyberattacks In Industrial Control Systems: Ensemble Methods For Binary Classification Of Synchrophasor & Security Logs 

### By <a href="https://hypr.systems/about.html" target="_blank" rel="noopener noreferrer">Disesdi</a> | 21 October 2022

-------

Code available [here >>](https://github.com/disesdi/ics_ensemble/blob/main/ics_ensemble_1.ipynb)

-------



## Introduction

This project utilyzes Power System Attack Datasets produced by Mississippi State University and Oak Ridge National Laboratory (ORNL). The datasets contain security logs as well as electrical synchrophasor data.

 
The Dataset(s) README is available [here](http://www.ece.uah.edu/~thm0009/icsdatasets/PowerSystem_Dataset_README.pdf):<sup>[1]</sup>

* http://www.ece.uah.edu/~thm0009/icsdatasets/PowerSystem_Dataset_README.pdf


Links to download these & other Industrial Control System (ICS) cyberattack datasets [here](https://sites.google.com/a/uah.edu/tommy-morris-uah/ics-data-sets?authuser=1):<sup>[2]</sup>

* https://sites.google.com/a/uah.edu/tommy-morris-uah/ics-data-sets?authuser=1


## Background

Synchrophasors / Phasor Measurement Units (PMUs) use a common time source to synchronize measurements of electrical waves in an power grid.<sup>[3]</sup> 

These measurements sometimes present anomalous events, which may constitute cyberattacks.

Cyberattacks on power grids can take the form of data injections that mimic fault events, causing power to be erroneously shut down by sensors in the system.<sup>[4]</sup>

In the diagram below, G1 and G2 are power generators. R1 through R4 are Intelligent Electronic Devices (IEDs) that can switch the breakers on or off. 


![ics_ensemble_1](https://user-images.githubusercontent.com/110150470/197652921-2f98b627-4d1c-4f43-95d5-f3d286b825cd.png)

*[Image source](http://www.ece.uah.edu/~thm0009/icsdatasets/PowerSystem_Dataset_README.pdf) <sup>[1]</sup>*


The IEDs/breakers have no internal validation to detect whether fault events are valid or faked. Breakers can be shut off based on false data injections, resulting in malicious interruption of power.

Differentiating between real fault events and data injection attacks is thus vital to maintaining power grid operation.

The system from which these measurements were taken contains 4 PMUs measuring 29 features, which results in a total of 116 PMU measurement columns.

The dataset additionally contains [Snort](https://www.snort.org/) <sup>[5]</sup>  and simulated control panel logs.


## Methods

### Preprocessing

The dataset contains 2 target classes for binary classification, representing natural and attack scenarios. Where appropriate for the model, categorical data have been transformed to numerical values.


The full dataset contains 78,377 rows of data. Rows containing values that were either very large or very small (`np.inf`, `-np.inf`) were dropped, resulting in a final 72,073 rows of data.


### Model Training

**Non-ensemble Method: Gaussian Naive Bayes**

For comparison, a non-ensemble model--[Gaussian Naive Bayes (GNB)](https://scikit-learn.org/stable/modules/naive_bayes.html?highlight=gaussian+naive+bayes)--was trained on the data first.

Gaussian Naive Bayes prediction accuracy was **31.17%**.

**Ensemble Methods**

Models from five ensemble algorithm groups were trained. These included bagging, random forests, gradiant boosted decision trees, extreme gradient boosting (XGBoost), and histogram-based boosting.

The bagging method utilyzed a K-Neighbors classifier, while the remaining four models employed some form of decision tree-based classification.


* **Bagging methods** are "*a class of algorithms which build several instances of a black-box estimator on random subsets of the original training set and then aggregate their individual predictions.*"<sup>[6]</sup> Bagging is an effective method to boost base model performance (without changing the underlying algorithm),<sup>[7]</sup> as well as reducing overfit tendencies.


* **Random Forests** is an algorithm based on randomized decision trees. It utilyzes a *perturb-and-combine* system specially designed for trees,<sup>[8]</sup> introducing randomness into the construction of each classifier.<sup>[9]</sup> The average of all classifiers is used to make predictions.


* **Gradient Tree Boosting** or **Gradient Boosted Decision Trees (GBDT)** is an ensemble method using multiple trees sequentially, each "learning" from the mistakes of previous trees. <sup>[10]</sup>  GBDT algorithms implement *shrinkage*, a regularization strategy that scales the contribution of each learner by some constant.<sup>[11]</sup> Overfit in `sklearn` GBDT can be moderated by scaling gradient descent step length using the `learning_rate` hyper-parameter. Because this parameter interacts closely with the number of learners that are fit, care should be taken when setting the number of estimators (trees).<sup>[12]</sup>


* [**XGBoost**](https://github.com/dmlc/xgboost) is an open-source implementation of GBDT algorithm.<sup>[13][14]</sup> 


* **Histogram-based gradient boosting** implementation in `sklearn` is similar to XGBoost and [LightGBM](https://papers.nips.cc/paper/2017/hash/6449f44a102fde848669bdd9eb6b76fa-Abstract.html), and can be orders of magnitude faster than classical gradient boosting algorithms, when the number of samples is large.<sup>[15][16]</sup>



## Results

The winning model in terms of accuracy is Random Forests. Random Forests dramatically outperformed other methods, at **93.1%**.


Prediction accuracy for XGBoost was **83.01%**.


Bagging with K-Neighbors as estimator made predictions with **81.96%** accuracy.
 

The highest performing Gradient Boost model had the highest number of estimators, underscoring the effectiveness of ensemble methods on this dataset. This model also had the highest max tree depth. These results are in line with the high-dimensional nature of the data.

In fact, although a higher number of estimators tends to result in better results with GBDT, leaving the number of estimators unchanged at 400 while increasing maximum tree depth to 4 resulted in a seven point jump in accuracy, from 78.4% to 85.6%.

The increased tree depth came with training time increases, however. Resource usage was unscalable with predetermined computing constraints, so a faster histogram-based gradient boosting technique was applied. Prediction accuracy leveled off for this model at 92.19% after 4,000 iterations; a slight gain over 92.01% after 2,000 iterations. Based on these results, it is unlikely that additional training will result in dramatic accuracy improvement. 

*Part 2 of this project explores outlier handling for anomaly detection.*

*Code available [here >>](https://github.com/disesdi/ics_ensemble/blob/main/ics_ensemble_1.ipynb)*

-------


## [*Contact me >>*](https://hypr.systems/about.html)


-------

## References


1. Power System Attack Datasets - Mississippi State University and Oak Ridge National Laboratory - 4/15/2014, 15 April 2014, http://www.ece.uah.edu/~thm0009/icsdatasets/PowerSystem_Dataset_README.pdf. Accessed 21 October 2022.


2. “Tommy Morris - Industrial Control System (ICS) Cyber Attack Datasets.” Google Sites, https://sites.google.com/a/uah.edu/tommy-morris-uah/ics-data-sets?authuser=1. Accessed 21 October 2022.


3. Knapp, Eric D. and Raj Samani. “Applied Cyber Security and the Smart Grid: Implementing Security Controls into the Modern Power Infrastructure.” (2013).


4. Unsal, Derya, Taha Selim Ustun, S. M. Suhail Hussain and Ahmet Onen. “Enhancing Cybersecurity in Smart Grids: False Data Injection and Its Mitigation.” Energies 14 (2021): 2657.


5. Snort - Network Intrusion Detection & Prevention System, https://www.snort.org/. Accessed 21 October 2022.


6. “1.11. Ensemble methods — scikit-learn 1.1.2 documentation: Bagging meta-estimator.” Scikit-learn, https://scikit-learn.org/stable/modules/ensemble.html?highlight=bagging#bagging-meta-estimator. Accessed 21 October 2022.


7. L. Breiman, “Bagging predictors”, Machine Learning, 24(2), 123-140, 1996.


8. Ensemble methods — scikit-learn 1.1.2 documentation: Forests of randomized trees.” Scikit-learn, https://scikit-learn.org/stable/modules/ensemble.html?highlight=random+forests#forests-of-randomized-trees“1.11. Accessed 21 October 2022.



9. Breiman, “Random Forests”, Machine Learning, 45(1), 5-32, 2001.


10. “1.11. Ensemble methods — scikit-learn 1.1.2 documentation: Gradient Boosting.” Scikit-learn, https://scikit-learn.org/stable/modules/ensemble.html#gradient-boosting. Accessed 21 October 2022.


11. Friedman, J.H. (2001). Greedy function approximation: A gradient boosting machine. Annals of Statistics, 29, 1189-1232.


12. “1.11. Ensemble methods — scikit-learn 1.1.2 documentation: Gradient Boosting--Shrinkage.” Scikit-learn, https://scikit-learn.org/stable/modules/ensemble.html#gradient-boosting-shrinkage. Accessed 21 October 2022.


13. Tianqi Chen and Carlos Guestrin. XGBoost: A Scalable Tree Boosting System. In 22nd SIGKDD Conference on Knowledge Discovery and Data Mining, 2016


14. “Scalable, Portable and Distributed Gradient Boosting (GBDT, GBRT or GBM) Library, for Python, R, Java, Scala, C++ and more. Runs on single machine, Hadoop, Spark, Dask, Flink and DataFlow.” GitHub, https://github.com/dmlc/xgboost. Accessed 21 October 2022.


15. “1.11. Ensemble methods — scikit-learn 1.1.2 documentation: Histogram Based Gradient Boosting.” Scikit-learn, https://scikit-learn.org/stable/modules/ensemble.html#histogram-based-gradient-boosting. Accessed 21 October 2022


16. Ke et. al. “LightGBM: A Highly Efficient Gradient Boosting Decision Tree”

-------

[home](https://disesdi.github.io/) \| [resources](https://disesdi.github.io/resources.html) \| <a href="https://github.com/disesdi/" target="_blank" rel="noopener noreferrer">github</a> \| <a href="https://anglesofattack.io/about.html" target="_blank" rel="noopener noreferrer">about</a>
