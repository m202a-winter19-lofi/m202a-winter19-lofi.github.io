---
layout: page
title: "Design"
---


![LOFI](/assets/images/lofi_diag.png)

LOFI takes user inputs such as their mood, estimated using their heart rate variability, and their activity, estimated using a convolutional neural network, and recommends songs accordingly. The recommender algorithm implements an intuitive K-nearest neighbors algorithm to find songs "closest" to the user's mood and activity in the latent valence-arousal-tempo space detailed below, returning the top K recommendations to the user by running the algorithm on a compact song metadata database on an app. In total, the system makes up a closed feedback loop where song recommendations that change a user's mood can in turn change future recommendations.



# *Mood estimation*

## Representing mood in 2 dimensions: the valence-arousal space
<p>One of the first questions that naturally surfaced when thinking up this project was, "How can you possibly quantify something like mood?"</p>
<p>In 1992, a paper was published that introduced a 2-dimensional, continuous representation of emotion in the Journal of Experimental Psychology [1].
This came to be known as the valence-arousal model of emotion, where different regions of the space represent different types of emotions.</p>
![VA space](/assets/images/va_space.png)
<p>Valence, the horizontal axis, represents the positivity or negativity of an emotion. Arousal, the vertical axis, represents the energy of an emotion. 
For example, an emotion like happiness is characterized by high valence and high arousal, whereas anger is characterized by low valence and high arousal.
This representation of emotion is desirable for our application since it is easy to visualize and to work with. </p>

<p>In 2018, researchers at Deezer, a music streaming service, published a paper on music mood classification [2] and a dataset of songs embedded with their respective VA values [3].
By using a variety of techniques such as lyric semantic analysis, MFCC analysis (Mel frequency cepstral coefficients: what instruments and timbres were present) and crowdsourced tag analysis 
(mapping valence and arousal values to user tags of songs like "danceable" or "chill"), VA values for each song were algorithmically generated and standardized across the dataset.</p>

![Deezer dataset excerpt](/assets/images/deezer_dataset.png)



## Heart rate variability (HRV) and the VA space

<p>In 2009, Stickel et. al wrote about how they mapped readings of heart rate variability to the VA space [4]. ... 
Using this method, measurements of heart rate variability can then be mapped to the VA space. By using a Hexiwear to measure heart rate, 
measurements can be sent over BLE to a bridge device (in this case, an Android smartphone) to make measurements in change of heart rate 
variability over time. </p>



# *Activity recognition*

## Goals of activity recognition

<p>For this iteration of the project, the goal is to be able to distinguish between times when the user is active (i.e. jogging) or not active (i.e. studying or commuting). 
In the case of a user jogging, the system will aim to suggest music with a tempo matching their cadence.
Indeed, music recommended to the user depends on which of these two states they are in. In a more relaxed state, VA values of the song are weighted more heavily in 
selecting song recommendations. But in a jogging state, where running to a song with a matching tempo makes more of an impact on the user's experience, song tempos are 
weighed more heavily.</p>

<p>If time allows, and/or in future iterations of the project, more kinds of activities can be detected and songs can be suggested based on various other kinds of activities.
The way is open for the project to be extended.</p>

## Convolutional neural network (CNN) design and training





# Song recommendation

## K nearest neighbors for top recommendations 

x

## Bringing it together: recommending based on mood (VA) and activity (tempo)

x



# Implementation

## Translating everything to an app implementation 

x

## Optimization 

x