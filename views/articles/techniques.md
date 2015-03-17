# Techniques
<hr>
### Introduction

Machine learning (ML) is a subfield of Computer Science originating from research into artificial intelligence. It explores the construction and study of algorithms that can learn from data. Such algorithms operate by building a model from example inputs and using that to make predictions or decisions, rather than following strictly static program instructions[^1].

Machine Learning plays an important role in MER as it is with ML that the computer predicts the emotions we feel depending on the music. There exist many techniques, which each have their own pros and cons. However as ML is a relatively new science they are not all very effective, and even the most effective techniques are not extremely reliable.

We have chosen to study three techniques of ML applied to MER:  Support Vector Regression (SVR), Support Vector Machine (SVM) and Neural Networks (NN). These techniques will span over MER by classification and by regression.

### Support Vector Regression ### {#SVR}

The SVR based music emotion recognition consists of three steps:

1. Extraction of music features such as the overall energy of the music, the rhythm and harmonics.
2. These features and their combination must then be mapped into emotion categories on a plane; this technique therefore quantifies emotions.
3. Find regression functions that will enable the mapping of the music to a category, i.e. placing it on the plane. When a piece is playing, the computer will retrieve the musical features, then use the regression functions that take these features as inputs, to output the emotion as coordinates (in the form of a vector) of the plane.

SVR was used in an experiment in 2009 supervised by Byeong-jun Han, Seungmin Rho, Roger B. and Dannenberg Eenjun Hwang[^2]. The plane they used was Thayer’s two-dimensional emotional plane which evaluates the valence (i.e. the mood) of an emotion on the x–axis and its arousal (i.e. the intensity) on the y–axis. Representing emotions with coordinates is called *[Regression](regression)*, which we will look at later on. They chose to extract seven music features such as scale, intensity, rhythm and harmonics and selected 165 various music pieces for their experiment.  

<figure markdown="1">
![Thayer's two-dimensional emotion plane](/assets/images/VADiagram.png)
<figcaption markdown="1">
  Figure 2.1: Thayer's two-dimensional emotion plane. Adapted from: Russell, J. A. (1980). A circumplex model of affect. Journal of Personality and Social Psychology, 39, 1161–1178.
</figcaption>
</figure>

These features were then used as input for the regression functions; both Cartesian and polar coordinates were used as outputs:

1. In case of Cartesian representation, the emotion of a song can be represented by (*a*, *v*), where *a* denoting arousal and *v* denoting valence and their ranges are *a* ∈ `[-1,1]` and *v* ∈ `[-1,1]`.
2. In case of polar representation assume that `Emotion`<sub>`c`</sub> and `Emotion`<sub>`p`</sub> represent an emotion in Cartesian and polar coordinate systems, respectively. We can calculate the distance and angle values of each emotion and transfer the coordinate system from Cartesian to polar using simple mathematical equations.
Why use both forms? Well they found out that for the emotions that were hard to differentiate, using Cartesian form gave misclassifications. For example, “Peaceful” and “Bored” were misclassified into the “Calm” on the AV plane. The results they had using polar coordinates were much more accurate as you can see with the following table:

<figure markdown="1">
Coordinate type           | Accuracy
--------------------------| -------------
Cartesian                 | 63.03%
Polar                     | 94.55%
<figcaption markdown="1">
Figure 2.2: Table comparing accuracy of SVR using Polar and Cartesian forms[^2]
</figcaption>
</figure>


They also compared the accuracy of SVR with classification ML techniques such as Gaussian Mixture Model (GMM) and Support Vector Machine to try and see which was more effective. These are the results they got:

<figure markdown="1">
Technique       | Coordinate type  | Accuracy
----------------| ---------------- | --------------
SVR             | Cartesian        | 63.03%
SVR             | Polar            | 94.55%
SVM             | Cartesian        | 32.73%
GMM             | Cartesian        | 91.52%
GMM             | Polar            | 92.73%
<figcaption markdown="1">
Figure 2.3: Table of different techniques used for experience and their accuracy[^2]
</figcaption>
</figure>

Misclassifications still occurred as we can see, partly due to the fact that some emotions are too hard to differentiate for a computer (even for us sometimes) such as sleepy, sad, anger, etc. It also is interesting to notice that in general, use of polar coordinates results in a better accuracy of emotion recognition (i.e. misclassifications are significantly reduced).

### Support Vector Machine ### {#SVM}

The job of a SVM is to create a separation boundary (not necessarily linear) in a feature space such that subsequent observations can be automatically classified into separate groups. For MER, these groups correspond to emotions. A good example of such a system is classifying emails into spam or non-spam. The seperation boundary is produced by an optimal separating hyperplane. Consider a `n` dimensional space. A separating hyperplane is essentially an affine `(n-1)` dimensional space that lives within the larger `n` dimensional space[^5].

<figure markdown="1">
![One- and two-dimensional hyperplanes](/assets/images/seperating_hyperplane.png)
<figcaption markdown="1">
  Figure 2.4: One- and two-dimensional hyperplanes[^5]
</figcaption>
</figure>

An *optimal* separating plane is the separating hyperplane that is farthest from any training observations also called Maximal Margin Hyperplane (MMH). To find an MMH, we first compute the perpendicular distance from each training observation `x`<sub>`i`</sub> for a given separating hyperplane. The smallest perpendicular distance to a training observation from the hyperplane is known as the margin. The MMH is the separating hyperplane where the margin is the largest. We can see on the figure below that the MMH is the mid-line of the widest "block" (i.e. margin) that we can insert between the two classes such that they are perfectly separated.

<figure markdown="1">
![ Maximal margin hyperplane with support vectors (A, B and C)](/assets/images/MMH.png)
<figcaption markdown="1">
  Figure 2.5: Maximal margin hyperplane with support vectors (A, B and C)[^5]
</figcaption>
</figure>

This is how a Soft Margin Classifier (SMC) works. A SMC allows some observations to be on the incorrect side of the margin or hyperplane. The following figures below demonstrate observations being on the wrong side of the margin and the wrong side of the hyperplane respectively.

<figure markdown="1">
![Observations on the wrong side of the margin and hyperplane, respectively](/assets/images/SVC.png)
<figcaption markdown="1">
  Figure 2.6: Observations on the wrong side of the margin and hyperplane, respectively[^5]
</figcaption>
</figure>

SVM is an extension of a SMC which allows non-linear decision boundaries. Consider the following figures below. In such a situation a purely linear SMC will be useless, simply because the data has no clear linear separation.

<figure markdown="1">
![No clear linear separation between classes and thus poor SVC performance](/assets/images/nonlinear.png)
<figcaption markdown="1">
  Figure 2.7: No clear linear separation between classes and thus poor SVC performance[^5]
</figcaption>
</figure>

SVM results from expanding the feature space through the use of special functions known as kernels[^5].

<figure markdown="1">
![A d-degree polynomial kernel and a radial kernel](/assets/images/SVM.png)
<figcaption markdown="1">
  Figure 2.8: A d-degree polynomial kernel and a radial kernel[^5]
</figcaption>
</figure>

An experiment to study SVM was lead by Cyril Laurier and Perfecto Herrera[^6]. They chose 133 music features such as energy band ratio, flatnessDB, beats per minute, etc. Five clusters, shown below, were selected (clusters/labels are another way to represent emotions: it's called *[Classification](classification)*). The hyperplanes were therefore 4-dimensional as a 5-dimensional plane was used (five clusters &rarr; 5-dimensional plane).

<figure markdown="1">
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
Figure 2.9: MIREX table of 5 clusters of emotions.[^6]
</figcaption>
</figure>

As you can see, the emotions in each cluster are deliberately vague for the SVM to cover as many emotions as possible.

The experience shows three main points :

1. Cluster 3 and 5 are the most predictable
2. There is a problem to predict Cluster 1 because it is close to Cluster 5 due to acoustic similarities. Both are energetic, loud and many of both use electric guitar. So the computer will have difficulties to evaluate the difference of the two Clusters.
3. There is a confusion between Cluster 2 and 4 because the emotions in these two Clusters sometimes overlap: fun (Cluster 2) and humorous (Cluster 4).

The results of the experience is summarised in the table below:

<figure markdown="1">
Truth/Predicted  | 1        | 2        | 3        | 4        | 5
---------------- | -------- | -------- | -------- | -------- | --------
Cluster 1        | **45.8** | 11.7     | 5.0      | 17.5     | 20.0
Cluster 2        | 10.8     | **50.0** | 11.7     | 27.5     | 0.0
Cluster 3        | 1.7      | 11.7     | **82.5** | 4.1      | 0.0
Cluster 4        | 10.0     | 31.7     | 4.2      | **53.3** | 0.8
Cluster 5        | 18.3     | 1.7      | 2.5      | 6.7      | **70.8**

<figcaption markdown="1">
  Figure 2.10: Confusion Matrix, horizontally the distribution of the prediction for a given Cluster[^6]
</figcaption>
</figure>

### Neural Network ### {#NN}

Neural Networks imitate the activity of our biological nervous system. It associates attributes and characteristics of data to emotions amongst other things. For example, certain colours are associated with certain emotions (brightly coloured paintings are usually associated with joy and happiness whereas dark-coloured paintings are associated with sadness, fear, etc.). The principle of this technique is illustrated with the image below. A certain number of inputs are used. These inputs are then analysed by the computer with “tools” that class the information given: the hidden layers. Each input now has a “weight” associated with the hidden layer. The hidden layers with the most weight have a greater activity level. The activity level of each layer then determines the output[^3]. Although neural networks have been applied extensively in domains such as object recognition, speech and text recognition, they have been relatively under-utilised in music cognition and music informatics.

<figure markdown="1">
![Neural Network schema](/assets/images/NeuralNetworkSchema.jpg)
<figcaption markdown="1">
  Figure 2.9: Neural Network schema[^3]
</figcaption>
</figure>

In MER application, the hidden layers correspond to music features. You also need a training set of data for the computer to work with (i.e. data that depending on the activity of the features outputs the corresponding emotion). It is also necessary to find a concrete way to represent emotions. Usually researchers will use coordinates with x-axis representing some general aspect of emotion and y-axis another aspect of emotion such as valence and arousal.
Just like your nervous system associates musical attributes to certain emotions (high energy music, fast rhythm&hellip; &rarr; agitated; slow rhythm, no energy, long sounds as opposed to short, brief sounds &rarr; sad&hellip;), the neural network does the same thing.

Naresh N. Vempala and Frank A. Russo led an experiment of MER using Neural Networks. They conducted a network that predicted the emotion for the entire piece of music. Twelve music experts were used to give the emotions they felt whilst listening to pieces. The data that was retrieved was then used as the "actual" emotion of the song even though emotions are subjective. Then thirteen music features were extracted used as inputs and hidden layers  and the ouputs were again AV coordinates (because it is an simple way to represent emotions) as shown on the image below. It is also important to note that the weight between input units and hidden layers and between hidden layers and outputs were set to random numbers close to 0.

<figure markdown="1">
![Neural Network schema](/assets/images/NN_explanation.png)
<figcaption markdown="1">
  Figure 2.10: Neural Network of the Experience[^4]
</figcaption>
</figure>

Inputs were passed through a &ldquo;sigmoidal& function, multiplied with the connection weights `W`<sub>`hi`</sub>, and summed at each hidden unit. Hidden unit values were obtained by passing the summed value at each hidden unit through a sigmoidal function. These values were multiplied with the connection weights `W`<sub>`oh`</sub>, summed at each output unit, and passed through a "sigmoidal" function to arrive at the final output value for each output unit. Network outputs were compared to desired outputs and the error was computed. The machine then computed the weight changes that had to be done. At the end, connection weights were updated with the sum of all stored weight changes.

This is the final result of the experiment:

<figure markdown="1">
![Neural Network schema](/assets/images/NNresult1.png)
<figcaption markdown="1">
  Figure 2.11: Result of experiment[^4]
</figcaption>
</figure>

We can see from the graph that overall, Neural Networks accurately predict emotions. However Stravinsky "actual" emotions and predicted emotions are quite far off. What could be done is to create a Neural Network for each music attribute and then use the ones that contribute the most to the AV prediction.

### Conclusion

There exists many ML techniques applied to MER. We have seen three: SVR, SVM, Neural Networks. Some other techniques worth mentioning are Gaussian Mixture Models, Decision Tree Learning, Clustering and K-Nearest Neighbours.  

<figure markdown="1">
#### Accuracy #### {#Fig210}
Technique       | Accuracy
----------------| --------------
SVR             | 78.8%
SVM             | 60.5%
GMM             | 92.1%
Neural Network  | 85.6%
KNN[^7]         | 38.9%
<figcaption markdown="1">
  Figure 2.10: Comparative Table of Various ML Techniques Applied in MER (Calculated from average of [^2], [^6], [^4], [^7])
</figcaption>
</figure>

From the table above, we can see that the researches and experiments on MER are promising because generally emotions are recognised by the computer. However all of these techniques have yet to be perfected and therefore need a lot of work.  

*[ML]: Machine Learning
*[MER]: Music Emotion Recognition
*[SVR]: Support Vector Regression
*[SVM]: Support Vector Machine
*[GMM]: Gaussian Mixture Model
*[AV]: Arousal Valence
*[MMH]: Maximal Margin Hyperplane
*[SMC]: Soft Margin Classifier

### References

[^1]: Wikipedia (2015) Machine Learning [Online] Available from: <a href="http://en.wikipedia.org/wiki/Machine_learning" TARGET="_blank">http://en.wikipedia.org/wiki/Machine_learning</a>  

[^2]: Byeong-jun Han, Seungmin Rho Roger and B. Dannenberg Eenjun Hwang (2009) SMERS: Music Emotion Recognition using Support Vector Recognition [Online] Available from:[ http://www.cs.cmu.edu/~rbd/pap&hellip;](http://www.cs.cmu.edu/~rbd/papers/emotion-ismir-09.pdf)

[^3]: Christos Stergiou and Dimitrios Siganos (-) Neural Networks [Online] Available from: [http://www.doc.ic.ac.uk/~nd/surprise_96/journal/vol4/cs11/repo&hellip;](http://www.doc.ic.ac.uk/~nd/surprise_96/journal/vol4/cs11/report.html#What%20is%20a%20Neural%20Network)

[^4]: Naresh N. Vempala and Frank A. Russo (2012) Predicting Emotion from Music Audio Features Using Neural Networks [Online] Available from: [http://www.cmmr2012.eecs.qmul.ac.uk/sites/cmmr2012.eec&hellip;](http://www.cmmr2012.eecs.qmul.ac.uk/sites/cmmr2012.eecs.qmul.ac.uk/files/pdf/papers/cmmr2012_submission_66.pdf)

[^5]: Michael Halls-Moore (2014) Predicting Support Vector Machines: A guide for beginners [Online] Available from: [http://www.quantstart.com/articles/Support-Vector-Mach&hellip;](http://www.quantstart.com/articles/Support-Vector-Machines-A-Guide-for-Beginners)

[^6]: Cyril Laurier and Perfecto Herrera (-) Audio Music Mood Classification
Using Support Vecotor Machine [Online] Available from: [http://www.mtg.upf.edu/files/publications/b6c06&hellip;](http://www.mtg.upf.edu/files/publications/b6c067-ISMIR-MIREX-2007-Laurier-Herrera.pdf)

[^7]: Ricardo Malheiro, Renato Panda, Paulo Gomes and Rui Pedro Paiva (2013) Music Emotion Recognition from Lyrics: A Comparative Study [Online] Available from: [http://www.academia.edu/8516120/Music_Emotion_Recogn&hellip;](http://www.academia.edu/8516120/Music_Emotion_Recognition_from_Lyrics_A_Comparative_Study._6th_International_Workshop_on_Machine_Learning_and_Music_MML13_._Praga)
