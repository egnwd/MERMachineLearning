# Classification

  "Without music, life would be a mistake" Friedrich Nietzsche, German philosopher.[^2]

## Introduction
### What is a classification problem?

A classification problem is one in which the data is to be given some discrete label(s) describing their nature in relation to a given situation. In the context of Music Emotion Recognition (MER) this involves giving a piece of music a label or a set of labels in describing which emotion(s) the music is trying to evoke, e.g. confident, cheerful, aggressive. See [Fig. 3.1](#Fig31) for the MIREX table of 5 clusters of emotional labels.[^7] It is important to note that what the Machine Learning Algorithms want to retrieve the emotion which the piece of music is trying to evoke, rather than the perceived emotion, as listeners may respond to different pieces of music in different way, e.g. a person may be pleased to hear melancholic music if this is the tone of music they enjoy.[^1] A ground truth is the term given to a label which a certain piece of data actually has. the aim of classification techniques is to suggest a high probability (or in a perfect world 'certainty') of the data having this ground truth label. Note that many ground truths can exist for a given data piece.

<figure markdown="1">
### Cluster Table ### {#Fig31}

Cluster 1  | Cluster 2  | Cluster 3   | Cluster 4 | Cluster 5
---------- | ---------- | ----------- | --------- | ----------
Rowdy      | Amiable    | Literate    | Witty     | Volatile
Rousing    | Sweet      | Wistful     | Humorous  | Fiery
Confident  | Fun        | Bittersweet | Whimsical | Visceral
Boisterous | Rollicking | Autumnal    | Wry       | Aggressive
Passionate | Cheerful   | Brooding    | Campy     | Tense/Anxious
           |            | Poignant    | Quirky    | Intense
           |            |             | Silly     |

<figcaption markdown="1">
Figure 3.1: MIREX table of 5 clusters of emotions.[^7]
</figcaption>
</figure>
### Different types of classification

In general, if a problem is labeled as a classification problem, it means that all elements in the data set should fall into one of two opposing categories, e.g. in the scenario of determining whether it is day or night in a photograph, each photo should be classified as 'day' or 'not day'.[^8] This is clearly not the case for MER as there are so many emotional label for a piece of music to fall under. In this article, four different forms of classification will be discussed which involve a large set of candidate labels:
#### Single-Label
The single-label technique acknowledges the possibility of data belonging to many labels. However, once the algorithm finds labels which it believes the data belongs to, a single label is chosen based on some criterion, e.g. which label has highest calculated probability for this data piece[^4]. The training set of data in this type of classification are associated with one label each.[^2]
#### Multi-Class
Multi-class classification involves creating a label which is the combination of two or more labels in the given set. It is like considering each member of the power set of labels as a possible fit for data, e.g. the set of all possible labels for the colour of a car include: white; black; grey; blue; {white + black}; {black + blue + grey}.[^4]
#### Multi-Label
With multi-label classification, the output for the learning algorithm has such a form that it is possible to see if the data is thought to belong to each set. One way of doing this is by outputting a binary vector (sequence of 0s &amp; 1s) which act as flags to indicate if each label fits.[^4] There are two types of classification problems: Problem Transformation Methods (PTMs) and Algorithm Adaptation Methods (AAMs). PTMs convert multi-label problem into one or more single-label problems, for which established and efficient algorithms already exist. AAMs take a more direct approach in which it takes a known ML algorithm and enhances it to cope with many labels.[^3]  
#### Fuzzy Label
The purpose of the previous the forms mentioned are to output a definite value for whether data should be given a label or not. A fuzzy label, however, provides the probabilities of the data belonging to each category. The result from running a fuzzy classification algorithm can be thought of as like the binary vector produced in multi-label classification, however the components can be any real number in the interval [0,1]. The non-discrete nature of a fuzzy label can be thought of as the stepping stone to continuous techniques of representing the emotion evoked by a piece of music like regression.[^9]

## Why classification is difficult

Classification is in essence pattern recognition <!-- quote --> 'the act of taking in raw data and making an action based on the "category" of the pattern'.[^5] Although humans clearly have this skill, we often struggle with defining rules for the classification of a particular set of data because it comes so naturally to us. Because of this, machine learning is very useful in classification as rules created are data based and so are more likely to be accurate in determining the nature of the data.[^11] The training set of data does however need to be labeled by a human before a machine can come up with a suitable model for classifying (known as supervised learning); otherwise it will just be trying to partition groups of data with common attributes (unsuprevised learning) which may not result in emotion related connections.[^12]

## Machine learning models

#### Support Vector Machines
Support Vector Machines take training data (a.k.a. observations) and represent them as a pair; the first part of the pair is a vector, and the second is the ground truth. The vectors for each observation have n dimensions and are plot in a set space also of n dimensions (*R*<sup>n</sup>) where n is the number of elements/ features used to compare the observations. Using one of the observations as the origin, a hyper-planes are created to shatter the points (divide the points into two groups, data points which exist in the class and those which don't). If the data are not falling into the correct partition of the space, a vector of weighting coefficients is adjusted and applied to the the vectors to shift the data round in order to fit into the partition which matches their ground truth.[^13]

<figure markdown="1">
![Examples of data shattering in 2 dimensions](/assets/images/dataShattering.png) {#Fig32}
<figcaption markdown="1">
Figure 3.2: Examples of data shattering in 2 dimensions.[^13]
</figcaption>
</figure>

Many hyper-planes can exist which shatter the data points correctly, SVMs choose the hyper-plane which maximises the distance to the closest points in order to generate the most general model. The vectors closest to the hyper plane are known as the support vectors.[^14] It is important to use a more general model as it is more resilient against subtle changes in test data and in real life applications.

<figure markdown="1">
![Demonstration of strongest Hyper-plane](/assets/images/manyHyperPlanes.png) {#Fig33}
<figcaption markdown="1">
  Figure 3.3: Demonstration of strongest Hyper-plane.[^14]
</figcaption>
</figure>

One particular study into the use of SVMs for MER carried out by Chiang et. al. used 35 features such as rhythm, dynamics and pitch to determine a model to fit pieces of music into four categories: happy, sad, peaceful and tensional. Once the relevant features had been extracted and selected, the intensity (arousal level) of the piece is classified as low or high using one SVM node, then the mood (valance level) of the piece is determined to decide which of the categories it belongs to. Flowchart for this system can be seen in [Fig 3.4](#Fig34). As we can see, SVMs can be used in traditional binary classification problems and part of PTMs for multi-label classification.[^15]

<figure markdown="1">
![Flowchart of SVM usage in study by Chiang et. al.](/assets/images/ClassificationExampleFlowChart.png) {#Fig34}
<figcaption markdown="1">
  Figure 3.4: Flowchart of SVM usage in study by Chiang et. al.[^15]
</figcaption>
</figure>

This study managed to achieve average accuracies of 86.94% in one data set and 92.33% in another.[^15]

 <!-- - Decision trees -->
 <!-- - Boosting -->
 <!-- - neural networks -->
#### Fuzzy k-Nearest Neighbour Classifiers (FKNN)
In regular k-Nearest Neighbour algorithms, the input data is predicted to exist in the category which it's k nearest neighbours belong to. The 'fuzzy' introduces the notion of likelihood in belonging to this category, and all categories.  To find the fuzzy membership &#956;<!-- mu --> to a particular class of an input data, <br>you take &#931;<!-- capital sigma -->(&#956;<sub>i</sub> / (distance from input data to data point i)<sup>2</sup> ) : 1 <= i <= k, <br>and divide by &#931; distances<sup>-2</sup>.

For the machine to create a model, it must first learn the values of the training set. These values are fuzzy vectors, of which, each component is calculated from the mean of the f<sup>th</sup> feature in each class. The machine learning part of this is when the error is calculated for each test data point and removes the weakest features are removed in order until the output vector accuracy converges.

In a study carried out by Yang et. al., each piece in the training set were split into segments. When labeling the segments, if the classifications were not majority, the segment was withdrawn from the training data. This particular study found an accuracy of 70.88%[^10]

 <!-- - Naive Bayes -->
 <!-- - bagging -->
 <!-- - random forests -->

<!--
#### Non-textual features
 - Table1 comparison of Multi(class vs Label)
 - Animation1 (think about one)
 - Table2 emotional adjectives
-->

### References
<!-- DONT FORGET TO COPY OVER REFERENCES -->
