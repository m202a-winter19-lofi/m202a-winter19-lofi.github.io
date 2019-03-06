---
layout: page
title: "Design"
---


![LOFI](/assets/images/lofi_diag_new.png)

LOFI takes user inputs such as their mood, estimated using their heart rate variability, and their activity, estimated using a convolutional neural network, and recommends songs accordingly. The recommender algorithm implements an intuitive K-nearest neighbors algorithm to find songs "closest" to the user's mood and activity in the latent valence-arousal-tempo space detailed below, returning the top K recommendations to the user by running the algorithm on a compact song metadata database on an app. In total, the system makes up a closed feedback loop where song recommendations that change a user's mood can in turn change future recommendations.



# **Mood estimation**

### Representing mood in 2 dimensions: the valence-arousal space
<p>One of the first questions that naturally surfaced when thinking up this project was, "How can you possibly quantify something like mood?"</p>
<p>In 1992, a paper was published that introduced a 2-dimensional, continuous representation of emotion in the Journal of Experimental Psychology [1].
This came to be known as the valence-arousal model of emotion, where different regions of the space represent different types of emotions.</p>

<p align="center"><img src="/assets/images/va_space.png"></p>

<p>Valence, the horizontal axis, represents the positivity or negativity of an emotion. Arousal, the vertical axis, represents the energy of an emotion. 
For example, an emotion like happiness is characterized by high valence and high arousal, whereas anger is characterized by low valence and high arousal.
This representation of emotion is desirable for our application since it is easy to visualize and to work with. </p>

<p>In 2018, researchers at Deezer, a music streaming service, published a paper on music mood classification [2] and a dataset of songs embedded with their respective VA values [3].
By using a variety of techniques such as lyric semantic analysis, MFCC analysis (Mel frequency cepstral coefficients: what instruments and timbres were present) and crowdsourced tag analysis 
(mapping valence and arousal values to user tags of songs like "danceable" or "chill"), VA values for each song were algorithmically generated and standardized across the dataset.</p>

![Deezer dataset excerpt](/assets/images/deezer_dataset.PNG)

<p align="center"><img src="/assets/images/deezer_va.PNG"></p>

<p>By dividing the valence-arousal space into 4 quadrants as per the paper on MoodyLyrics by Çano and Morisio [4], the distribution of the Deezer dataset's distinction 
between 4 key "bins" of mood can be distinguished. Each data point plotted represents the valence and arousal value of a given song. Happy (yellow) songs are positive and high energy. 
Relaxed (green) songs are positive and low energy. Their respective complements are: sad (blue) songs that are negative with low energy, and angry (red) songs that are negative with high energy.</p>

### Heart rate variability (HRV) and the VA space

<p>In 2009, Stickel et. al wrote about how they mapped readings of heart rate variability to the VA space [5]. ... 
Using this method, measurements of heart rate variability can then be mapped to the VA space. By using a Hexiwear to measure heart rate, 
measurements can be sent over BLE to a bridge device (in this case, an Android smartphone) to make measurements in change of heart rate 
variability over time. </p>



# **Activity recognition**

### Goals of activity recognition

<p>For this iteration of the project, the goal is to be able to distinguish between times when the user is active (i.e. jogging) or not active (i.e. studying or commuting). 
In the case of a user jogging, the system will aim to suggest music with a tempo matching their cadence.
Indeed, music recommended to the user depends on which of these two states they are in. In a more relaxed state, VA values of the song are weighted more heavily in 
selecting song recommendations. But in a jogging state, where running to a song with a matching tempo makes more of an impact on the user's experience, song tempos are 
weighed more heavily.</p>

<p>To build on the aforementioned Deezer dataset with this in mind, we used the Million Songs dataset (MSD) [6] to lift the VA representation of songs to the 3rd dimension: tempo. 
Since the Deezer dataset was made from songs in the MSD, one of the dataset's fields was the MSD track ID. Using this field, songs in the Deezer set could be looked up in the MSD, where 
those songs have a variety of high-level feature information, one of such features being tempo. By appending this new column to the Deezer dataset, we can arrive at a 3D visualization of what 
we can now call VAT space (valence, arousal, tempo).</p>

<p align="center"><img src="/assets/images/deezer_vat.PNG"></p>

<p>If time allows, and/or in future iterations of the project, more kinds of activities can be detected and songs can be suggested based on various other kinds of activities.
The way is open for the project to be extended. Other features can be extracted from the MSD to add further dimensions to this latent space, or we could implement our own 
feature extraction algorithms to find features of interest.</p>

### Convolutional neural network (CNN) design and training

<p>In order to infer what kind of activity a user is doing, convolutional neural networks (CNNs) were employed. 
Activity classification is most often done with CNNs or recurrent neural networks (RNNs). One of the main strengths of 
RNNs is their ability to use past information to make better inferences. This can shine in applications involving aperiodic
time series data (such as in EEG data of subjects interacting with their environment). However, in the concise set of activities 
we wish to classify, the activities are either periodic (walking) or static (sitting). In such a case, taking windows of data 
(i.e., a number of samples of sensor data over a given time) can serve to be excellent predictors of the actual activity if the network 
was trained on such windows. Therefore, in an effort to keep the network model as simple (conceptually and in terms of number of parameters)
as possible, a 1-dimensional CNN was chosen for the project.</p>

<p>The dataset used to train the CNN was the Activity Prediction dataset from WISDM at Fordham University [5]. The dataset contains 
samples of 3D accelerometer data of a smartphone in the front leg pocket of several subjects, which matches the conditions that the project 
assumes most users would be in when using LOFI. 
The activities that the dataset consists of are:</p>
* Sitting
* Standing
* Walking (on a flat surface)
* Walking upstairs 
* Walking downstairs 
* Jogging 

<p>The dataset was relatively evenly distributed across users (a good variety of different gaits and movement patterns across body types was acquired)
and most of the activity samples were of either walking or jogging.</p>

![samples over users](/assets/images/cnn_dist_users.PNG)

<p align="center"><img src="/assets/images/cnn_dist_activities.PNG"></p>

<p>All of the data was sampled at 20 Hz. We normalized the acceleration values x during preprocessing across all samples according to equation (2).</p>

<p align="center"><img src="/assets/images/eq2.PNG" alt="normalization equation"></p>

Here, *x* tilde is the normalized data, *µ* is the expected value of *x*, and *σ* is the standard deviation of *x*.

<p>Before normalization, an accelerometer reading 
of magnitude 1 was equal to 1G, or 9.8 m/s squared. By optimizing over different window lengths and amounts 
of window overlap, we arrived at using a 3 second window with no overlap for training (60 samples per input to the network), validation, and testing of the data.
Below are plots of a single window of different activities, preceded by a figure showing how the different smartphone acceleration axes were positioned relative to 
subjects' bodies during data collection [6].</p>

<p align="center"><img src="/assets/images/sensor_orientation.PNG"></p>

![jogging](/assets/images/jogging.PNG)

![walking](/assets/images/walking.PNG)

![sitting](/assets/images/sitting.PNG)

![standing](/assets/images/standing.PNG)

![upstairs](/assets/images/upstairs.PNG)

![downstairs](/assets/images/downstairs.PNG)

<p>As expected, more vigorous activities like jogging have greater change in acceleration over time than a stationary activity like sitting.
Other activities have observable, distinct features to set them apart from other types of activities (e.g. standing can be distinguished from sitting 
based on which axis feels gravity and walking up/downstairs have distinct "humps" in accelerometer readings).</p>

<p>The CNN architecture used is based off [7] and was visualized using Netron [8].</p>

<p align="center"><img src ="/assets/images/cnn_architecture.png" alt="architecture" height="650"></p>

<p>The convolution layers include a rectified linear unit (ReLU) at their output as their non-linear activation function.
This popular choice of activation function is fast to compute and empirically performs well. The convolution filter size used was 
4, and the number of filters in the first pair of convolution layers was 100, and in the second pair there were 160 filters used. Consecutive convolution layers 
allow for higher-level features in the sensor data to be discovered before being passed into the max pooling layer. These layers 
reduce intermediate tensor size while retaining the most critical information, all without adding extra training parameters. The 
dropout layer approximates bagging (bootstrap aggregating), a method of ensembling intended to improve generalization of the model. 
A dropout rate of 0.5 was used (half of the neurons would be "on"). Lastly, the output of the dropout layer is fed to a fully 
connected affine layer whose output is then fed to a softmax function to convert the scores into classification probabilities. The class (activity type) whose
probability was the maximum among these was the activity the sample is to be classified as.</p>

<p>The "adam" optimizer was used since it has been found to often give strong empirical results and it utilizes both running means of momentum and 
past gradient history. A batch size of 400 samples was used in training the network over 10 epochs.</p>

# **Song recommendation**

### K nearest neighbors for top recommendations 

<p>To take advantage of the VA space representation of the song dataset and HRV, we exploit the fact that listening 
to music with the same mood as a user is feeling has been shown to help the user feel better [9]. The top K songs are recommended to a user 
based on the Euclidean distance (norm 2) between a user's estimated mood in VA space and the K songs with the least distance to that mood. 
The K-nearest neighbors (KNN) algorithm is used to find these recommended songs.</p>





### Bringing it together: recommending based on mood (VA) and activity (tempo)

<p>However, the desired minimum distance is a function of the 
user's activity - we want to recommend songs completely based on mood if a user is not active, but we want to factor in tempo if the user is active (and 
include some valence/arousal biases to avoid playing sad music during a workout). So, the top K recommendations are ultimately found by solving the 
following optimization problem for the smallest K distances:</p>

<p align="center"><img src="/assets/images/modified_knn.PNG"></p>

We wish to minimize the Euclidean distance of these quantities over all songs in the dataset *i* and return the K smallest distances and their respective songs.
*v*, *a*, and *t* represent valence, arousal and tempo values, respectively. *α*, *β*, and *γ* are weights applied to their respective terms used for fine tuning 
recommendations. The subscript *i* refers to the values of one of the songs in the dataset. 
The subscript *x* refers to the values of a user's mood (a user's cadence when referring to tempo in *t* sub x). *θ* represents an indicator variable whose 
value can either be 1 or 0; *θ* = 1 if the user is active (jogging), else *θ* = 0. The subscript *θ* in the last term of the equation are the biases applied to 
the valence and arousal value regardless of user mood or song: if the user is jogging, we want to bias the valence and arousal of suggested songs such that 
songs that are too sad or relaxed are not suggested (an active workout would benefit from a higher-energy, positive playlist). 



# Implementation

### Translating everything to an app implementation 

x

### Optimization 

<p>Because the majority of the computing takes place on the smartphone, 