---
layout: page
title: "Results"
---

# *CNN performance*

### 6-activity CNN performance on test data 

<p align="center"><img src="/assets/images/results_cnn_confusion.PNG"></p>
<p align="center"><img src="/assets/images/results_cnn_loss.PNG"></p>
<p>The sensor dataset was split into a 50-25-25 training-validation-test split. The testing accuracy achieved was 99.84%, which is an improvement
over the best results of the paper that the dataset was created for [#], which had a 91.7% classification accuracy using a multilayer perceptron. 
Test samples were 3 second windows (60 samples) with no overlap of each of the 3 axes of accelerometer time series data. The test samples were 
randomly chosen across all activity types and all subjects, maximizing generalization performance of the network.
Choosing a window size of 3 seconds and no overlap as hyperparameters along with the architecture choice made for a well-performing network, in theory.
This could be owed to how relatively low-level features can be enough to distinguish between different activities, as discussed in the Design section.
What mattered more was how the network would perform when implemented on a smartphone.</p>

### 4-activity CNN performance on smartphone 

<p align="center"><img src="/assets/images/results_real_life_classification.PNG"></p>

<p>The network was implemented on the smartphone using the TensorFlow Lite library, as discussed more in Design. The reason for using a 4-activity 
network instead of the 6-activity one is also explained in Design.
Each of the 3 tests consisted of each activity for 1 minute while the phone was in their front leg pocket. 
Since 3-second windows are taken as input to the network, there are 20 samples each minute and therefore each activity has 20 trials per test. A phone 
screen recording app [#] was used to record the classifications and review them.</p>

<p>From the summary of classification accuracy at the bottom, even when implemented on the smartphone the network performs well. The activities walking and jogging 
have the highest classification accuracy as they are robust to different kinds of gaits and strides thanks to training over several test subjects. Interestingly, 
standing, one of the stationary activities, has the worst classification accuracy. This is due to the classification of standing being rather sensitive: one has to stand 
quite still, and upright to consistently be classified as standing. Leaning on a wall or even slight shifts in weight from one foot to the other can trigger misclassifications.
Training can be augmented by introducing new standing samples complete with small variances included through leaning on surfaces and shifting weight around, or with 
feet re-positioning to make the network more robust.</p>

<p align="center"><img src="/assets/images/results_real_life_activity_level.PNG"></p>

<p>The above experiment is meant to examine the network's performance in distinguishing between non-active activities (sitting, standing) and active activities (walking, jogging) 
so that the app may distinguish between operation modes: if the user is non-active, recommend songs based on mood only; otherwise, recommend songs based on stride rate as well. 
Each test is made up of 1 minute of classifications, so as before, 20 classifications per test. However, each of the tests were conducted back-to-back in a continuous 3-minute 
stretch. In the first minute (first test), at the 45 second mark the sitting user stood up and the walking user started to jog. 45 seconds later (30 seconds into test 2), 
the standing user sat down and the jogging user started to walk. This was repeated again 45 seconds later. These tests then capture classification performance during 
transition between activities as well. While the network was always able to correctly classify active activities, it had some trouble correctly classifying non-active 
activities. Almost all of these inaccuracies (i.e. walking or jogging predicted when the user was sitting or standing) occurred during the transition period between sitting 
and standing: this change in gravity acting on the phone is sometimes understood as walking or jogging before "settling into" the transitioned-into activity within the next 3
classifications. While there is 
room for improvement in making transition detection more robust and prior work for it, for our project we find it sufficient to consider a user doing an active activity if their 
activity is classified as active for at least 3 consecutive classifications.</p>

# *Stride rate estimation*

...

# *Mood estimation*

...

@ *Song recommendation*

... 