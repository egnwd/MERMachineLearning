# Classification
<hr>
### Introduction
#### What is a classification problem?

A classification problem is one in which the data is to be given some discrete label(s) describing their nature in relation to a given situation. In the context of Music Emotion Recognition (MER) this involves giving a piece of music a label or a set of labels which describe which emotion(s) the music is trying to evoke, e.g. confident, cheerful, aggressive. See [Fig. 3.1](#Fig31) for the MIREX table of 5 clusters of emotional labels.[^7] It is important to note that what the Machine Learning Algorithms want to retrieve is the emotion which the piece of music is trying to evoke, rather than the perceived emotion, as listeners may respond to different pieces of music in different way, e.g. a person may be pleased to hear melancholic music if this is the tone of music they enjoy.[^1]

Ground truth is the term given to a label which a certain piece of data actually has. the aim of classification techniques is to suggest a high probability (or in a perfect world 'certainty') of the data having this ground truth label. Note that many ground truths can exist for a given data piece.

<figure markdown="1">
#### Cluster Table #### {#Fig31}

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
#### Different types of classification

In general, if a problem is labeled as a classification problem, it means that all elements in the data set should fall into one of two opposing categories, e.g. in the scenario of determining whether it is day or night in a photograph, each photo should be classified as 'day' or 'not day'.[^8] This is clearly not the case for MER as there are many emotional labels for a piece of music to fall under. In this article, four different forms of classification will be discussed which involve a large set of candidate labels:
##### Single-Label
The single-label technique acknowledges the possibility of data belonging to many labels. However, once the algorithm finds labels which it believes the data belongs to, a single label is chosen based on some criterion, e.g. which label has the highest calculated probability for this data piece[^4]. The training set of data in this type of classification are associated with one label each.[^2]

##### Multi-Class
Multi-class classification involves creating a label which is the combination of two or more labels in the given set. It is like considering each member of the power set of labels as a possible fit for data, e.g. the set of all possible labels for the colour of a car include, but is not limited to: white; black; grey; blue; {white + black}; {black + blue + grey}[^4].

##### Multi-Label
With multi-label classification, the output for the learning algorithm has such a form that it is possible to see if the data is thought to belong to each set. One way of doing this is by outputting a binary vector (sequence of 0s &amp; 1s) which act as flags to indicate whether each label fits.[^4] There are two types of classification problems: Problem Transformation Methods (PTMs) and Algorithm Adaptation Methods (AAMs). PTMs convert multi-label problems into one or more single-label problems, for which established and efficient algorithms already exist. AAMs take a more direct approach in which it takes a known machine learning (ML) algorithm and enhances it to cope with many labels.[^3]  

##### Fuzzy Label
The purposes of the previous forms mentioned are to output a definite value for whether data should be given a label or not. A fuzzy label, however, provides the probabilities of the data belonging to each category. The result from running a fuzzy classification algorithm can be thought of as similar to the binary vectors produced in multi-label classification, however the components can be any real number in the interval `[0,1]`. The non-discrete nature of a fuzzy label can be thought of as the stepping stone to continuous techniques of representing the emotion evoked by a piece of music like regression.[^9]

### Why classification is difficult

Classification is, in essence, pattern recognition - &ldquo;the act of taking in raw data and making an action based on the "category" of the pattern&rdquo;.[^5] Although humans clearly have this skill, we often struggle with defining rules for the classification of a particular set of data because it comes so naturally to us. Because of this, machine learning is very useful in classification as the rules created are data based, therefore more likely to be accurate in determining the nature of the data.[^11] The training set of data does however need to be labelled by a human before a machine can come up with a suitable model for classifying (known as supervised learning); otherwise it will just be trying to partition groups of data with common attributes (unsuprevised learning) which may not result in emotion related connections.[^12]

### Machine learning models

#### Support Vector Machines
Support Vector Machines take training data (a.k.a. observations) and represent them as a pair; the first part of the pair is a vector, and the second is the ground truth. The vectors for each observation have n dimensions and are plotted in a set space also of `n` dimensions (`R`<sup>`n`</sup>) where `n` is the number of elements / features used to compare the observations. Using one of the observations as the origin, hyperplanes are created to shatter the points (divide the points into two groups, data points which exist in the class and those which don't). If the data are not falling into the correct partition of the space, a vector of weighting coefficients is adjusted and applied to the the vectors to shift the data round in order to fit into the partition which matches their ground truth.[^13]

<figure markdown="1">
![Examples of data shattering in 2 dimensions](/assets/images/dataShattering.png) {#Fig32}
<figcaption markdown="1">
Figure 3.2: Examples of data shattering in 2 dimensions.[^13]
</figcaption>
</figure>

Many hyperplanes can exist which shatter the data points correctly, SVMs choose the hyperplane which maximises the distance to the closest points in order to generate the most general model. The vectors closest to the hyper plane are known as the support vectors.[^14] It is important to use a more general model as it is more resilient against subtle changes in test data and in real life applications.

<figure markdown="1">
![Demonstration of strongest hyperplane](/assets/images/manyHyperPlanes.png) {#Fig33}
<figcaption markdown="1">
  Figure 3.3: Demonstration of strongest Hyperplane.[^14]
</figcaption>
</figure>

One particular study into the use of SVMs for MER carried out by Chiang et al. used 35 features such as rhythm, dynamics and pitch to determine a model which fits pieces of music into four categories: happy, sad, peaceful and tensional. Once the relevant features had been extracted and selected, the intensity (arousal level) of the piece is classified as low or high using one SVM node, then the mood (valance level) of the piece is determined to decide which of the categories it belongs to. A flowchart for this system can be seen in [Fig 3.4](#Fig34). As we can see, SVMs can be used in traditional binary classification problems and part of PTMs for multi-label classification.[^15] Multi-class problems can also be approached with SVMs; however, since the number of classes will be large and sparse in the context of MER, it is not really used.[^4]

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
#### Fuzzy k-Nearest Neighbour Classifiers (FKNN) #### {#FKNN}
In regular k-Nearest Neighbour algorithms, the input data is predicted to exist in the category which it's k-Nearest Neighbours belong to. The *fuzzy* introduces the notion of likelihood in belonging to this category, and all categories.  To find the fuzzy membership `μ`<!-- mu --> to a particular class of an input data, you take `(Σ(μ`<sub>`i`</sub> `/` `x`<sub>`i`</sub><sup>`2`</sup> `)) / (Σx`<sub>`i`</sub><sup>`-2`</sup>`) : 1 <= i <= k; x`<sub>`i`</sub> is the distance from input data to data point `i`.

For the machine to create a model, it must first learn the values of the training set. These values are fuzzy vectors, of which, each component is calculated from the mean of the f<sup>th</sup> feature in each class. The machine learning part of this is when the error is calculated for each test data point and removes the weakest features are removed in order until the output vector accuracy converges. <!-- restructure this part #remove remove -->

In a study carried out by Yang et al., each piece in the training set were split into segments. When labeling the segments, if the classifications were not a<!--?--> majority, the segment was withdrawn from the training data. This particular study found an accuracy of 70.88%[^10]


### Conclusion

As you can see from the case studied above, Machine Learning is clearly far more effective in determining if a piece of music expresses a certain emotion than just flipping a coin. The problem of classification is greatly decreased by using ML techniques on large data sets. Humans would do a better job classifying a short list of songs; however, there is a greater efficiency introduced when a mathematical model is applied to the data.

As shown by the techniques above, there are different techniques to deal with the different forms of classification problems. [Fig. 3.5](#Fig35) shows the advantages and disadvantages of using each of the four previously mentioned forms of classification in the context of MER.


<figure markdown="1">
#### Classification Form Comparison #### {#Fig35}

Form         | Advantages  | Disadvantages
------------ | ----------- | --------------
Single-label | It is clear to see what the primary emotion of the piece is                  | All other emotions the music evoke are lost in the result
Multi-class  | No emotional information is lost in the label given                          | The possible set of labels grows exponentially with the number of classes. Also the labels are often sparse
Multi-label  | The membership to each class is easily read and understood                   | A lot of computational power is required for this as the membership to each class must be calculated
Fuzzy-label  | The likelihood of membership to classes can make sorting by relevance easier | The result may be less clear to read when working out if each piece belongs to a certain class

<figcaption markdown="1">
Figure 3.5: Comparison table for the different forms of classification in the context of MER.
</figcaption>
</figure>

Some may argue that, since certain emotions are so similar to each other and yet still distinct, the best way to express them is through some sort of continuous scale like the one you will see in the Regression article of this website. Though this may simplify a mathematical model, it is easier for a human who is stating or requesting the emotion of a piece of music to understand a clear label than than it is to understand a 3.6 on a certain emotion based axis. This is why classification is very effective in MER.


### References
[^1]: Yang, Y., Lin, Y., Su, Y. and Chen, H. (2008). A Regression Approach to Music Emotion Recognition. IEEE Transactions on Audio, Speech, and Language Processing, [online] 16(2), pp.448-457. Available at: http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.331.1655&rep=rep1&type=pdf [Accessed 12 Feb. 2015].
[^2]: Trohidis, K., Tsoumakas, G., Kalliris, G. and Vlahavas, I. (2011). Multi-label classification of music by emotion. EURASIP Journal on Audio, Speech, and Music Processing, [online] 2011(1), p.4. Available at: http://ismir2008.ismir.net/papers/ISMIR2008_275.pdf [Accessed 13 Feb. 2015].
[^3]: Tsoumakas, G. and Katakis, I. (2007). Multi-Label Classification. International Journal of Data Warehousing and Mining, [online] 3(3), pp.1-13. Available at: http://books.google.co.uk/books?hl=en&lr=&id=1bpEifVEi2MC&oi=fnd&pg=PA64&dq=Multi-label+classification:An+overview&ots=WyD83kziKF&sig=P6VHFTT9RycLgfpCDrK0vq5o4hM#v=onepage&q=single-label%20&f=false [Accessed 15 Feb. 2015].
[^4]: Boutell, M. (2004). Learning multi-label scene classification*1. Pattern Recognition. [online] Available at: https://www.rose-hulman.edu/~boutell/publications/boutell04PRmultilabel.pdf [Accessed 3 Mar. 2015].
[^5]: Duda, R., Hart, P. and Stork, D. (2001). Pattern classification. 2nd ed. New York: Wiley.
[^6]: <!-- not used -->(SVM use for text recognition) https://dl.acm.org/citation.cfm?id=944790.944793&coll=DL&dl=ACM&CFID=485866018&CFTOKEN=79343228
[^7]: X., Downie, J., Laurier, C., Bay, M. and Ehmann, A. (2008). The 2007 MIREX audio mood classification task: Lessons learned. Proceedings of the International Conference on Music Information Retrieval. [online] Available at : http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.182.2004&rep=rep1&type=pdf [Accessed 5 Mar. 2015].
[^8]: Ng,A.. 2012. Classification (8 min). [online]. [Accessed 25 Feb. 2015]. Available from: https://class.coursera.org/ml-005/lecture/33
[^9]: Barthet, M., Fazekas, G. and Sandler, M. (2013). Music emotion recognition: from content-to context-based models. From Sounds to Music and Emotions. [online] Available at: https://books.google.co.uk/books?id=zWG5BQAAQBAJ&pg=PA243&dq=fuzzy+label+classification&hl=en&sa=X&ei=9dn2VIDsGIG3UeHngIgL&ved=0CC4Q6AEwAA#v=onepage&q=fuzzy%20label%20classification&f=false [Accessed 5 Mar. 2015].
[^10]: Yang, Y., Liu, C. and Chen, H. (2006). Music emotion classification. Proceedings of the 14th annual ACM international conference on Multimedia - MULTIMEDIA '06. [online] Available at: http://dl.acm.org/citation.cfm?id=1180665 [Accessed 12 Feb. 2015].
[^11]: Schapire, R. (n.d.). Machine Learning Algorithms for Classification..
[^12]: Ng,A.. 2012. Supervised Learning (12 min). [online]. [Accessed 25 Feb. 2015]. Available from: https://class.coursera.org/ml-005/lecture/3
[^13]: Burges, C. J. (1998). A tutorial on support vector machines for pattern recognition. Data mining and knowledge discovery. [online] 2(2), 121-167. Available from: http://research.microsoft.com/pubs/67119/svmtutorial.pdf [Accessed 26 Feb. 2015].
[^14]: opencv dev team, (2015). Introduction to Support Vector Machines — OpenCV 2.4.11.0 documentation. [online] Docs.opencv.org. Available at: http://docs.opencv.org/doc/tutorials/ml/introduction_to_svm/introduction_to_svm.html [Accessed 17 Mar. 2015].
[^15]: Chiang, W., Wang, J. and Hsu, Y. (2014). A Music Emotion Recognition Algorithm with Hierarchical SVM Based Classifiers. 2014 International Symposium on Computer, Consumer and Control. [online] Available at: http://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=6846115 [Accessed 28 Feb. 2015].
