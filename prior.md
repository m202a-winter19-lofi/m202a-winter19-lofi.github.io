---
layout: page
title: "Prior Work"
---

# *Effects of music on mood and exercise* 
<p>As research shows, music stimulates emotions and hence mood [15]. Since people tend to like music that sympathizes with them, people also seem 
to have a habit of choosing music based on the mood they are already feeling. This translates to that when people are feeling happy, sorrowful, or angry, 
they will generally want to listen to that type of music. By listening to music that sympathizes with one’s mood, people are able to process their emotion, 
even those held on a subconscious level.</p>

<p>Music evokes a “distraction effect” that increases comfort level when exercising [11]. A distraction effect is what keeps people from fully realizing 
their body’s exhaustion, hence allowing them to keep exercising. A research study from Sports Med Open found that playing music with tempo that matches one's 
cadence further enhances the “distraction effect” [10]. Cadence is the frequency of steps when running or walking. In their results, they showed that subjects 
had significant increase in adherence/motivation to exercise when listening to music with tempos that matched their cadence.</p>

# *Relationship between mood and music* 

<p>Researchers at Deezer worked on mood classification of music using hybrid techniques [1a]. The dataset they construct is an integral part of our project, as it 
gives context to the latent emotional space inhabited by music.</p>

<p>Hu et. al wrote about lyric text mining in music mood classification [2a], citing a "ceiling" to the mood classification that could be done just with frequency 
analysis. They also discuss the difficulties of creating ground truth datasets and go through considerable efforts to create their own. They distinguish between 
18 moods, much more granularity than in our project, and open us up to just how finely emotions can be discriminated when using text semantic analysis.</p>

<p>Laurier et. al also tackle the problem of mood classification of music through a multimodal approach [3a]. They compare classifications of songs using 
musical features and lyrics independently, then look into combining the two. In summary, they find that musical feature-based classification out-performs 
lyric-based classification, but combining the two modalities produces better results than any single approach.</p>

<p>Çano and Morisio split the VA space into the four quadrants that we base much of the project design on [4a]. They construct their own VA-embedded dataset 
based on song lyrics and achieve solid results of 74.25% classification accuracy (in the quadrant-based VA space partitioning).</p>

<p>Malheiro et. al incorporate new features to mood classification in songs. Namely, they introduce ideas of accounting for a slang dictionary (colloquial language 
that often won't appear in other dictionaries) and taking into account the structure of the song, interpreting lyrics differently depending on if they are perceived 
to be part of a song's verse or chorus. They were able to construct their own manually-annotated dataset of song lyrics labeled based on the VA model, and could 
achieve classification accuracy of 80.1% in quadrant-based VA classification.</p>



# *Emotion estimation from heart rate variability*

<p>Heart rate variability (HRV) is a generic term used to describe many measures of the heart, two of which are standard deviation of normal-normal R-R peaks (SDNN), 
absolute power in low frequency (LF), and absolute power in high frequency (HF). Many studies have tried to find the relation between mood and HRV. In these studies, 
valence and arousal are measures used to represent mood [13]. The Valence/Arousal plot is a model that was developed by Russel, and the formal name of it is 
Circumplex Model of Affect.</p>

<p>Research from National Chiao Tung University studied the correlation between music, heart rate variability, and mood [12]. They stated that SDNN can be used 
to estimate the valence axis, and LF/HF and can be used to estimate the arousal axis.  Just like how everyone has a different heart rate or blood pressure, 
everyone has their individual SDNN and LF/HF. So, it’s not enough to simply map their SDNN and LF/HF to a point of the Valence/Arousal plot. Instead, change 
of SDNN and gain of LF/HF can be used to estimate change of mood [14]. Kwansei Gakuin University studied the correlation between mood and heart rate variability 
indices during daily life, and observed that changes of HRV gave promising results for estimating change of mood.</p>

# *Activity recognition* 

<p>Rueda et. al published work on classifying human activities using a CNN and several different body-worn sensors [1x]. As used in this project, they use sliding 
windows over time-series data to train and test their CNN. They publish their architecture which involves a concatenation of all the body-worn sensor data which is 
incorporated into the final dense layer for classification. They use the popular Opportunity dataset among others to train their network and arrive at 
classification accuracies of over 92%.</p>

<p>Yang et. al publish results of their attempts at activity recognition with the Opportunity dataset [2x] (which has far more activity types than is investigated for our project) 
using various architectures including SVM (support vector machine), one-layer neural network, DBN (deep belief network), and CNN. They found CNN to perform the best, 
achieving accuracy of 96% when using temporal smoothing (using a low-pass filter to remove noise). </p>

<p>Whereas the previously mentioned papers worked with an array of body-worn sensors, Ronao and Cho focus on classification using a single smartphone [3x]. Although 
they use accelerometer and gyroscope data, they set a great precedent of work for this project to build on. Like our architecture, they use layers of convolution 
and pooling in repetition to extract features. They showed that SVM could perform about as well as a convolutional neural network.</p>

<p>The 2017 survey for activity recognition using deep learning by Wang et. al was instrumental in surveying the state of the art techniques used in this problem 
space [4x].</p>

<p>The paper by Kwapisz et. al that actually constructed the dataset used in the project was essential in understanding how the dataset was created and how to 
more finely interpret its features [5x] by, for example, displaying the orientation of the phone acceleration axes used when acquiring the data (shown in Design 
section of this report). Their best classification result is 91% using a multi-layer perceptron, which our model improves on soundly. </p>

<p>Before committing to a CNN-based architecture, RNNs were also investigated (recurrent neural networks). The paper on using deep RNNs for activity recognition by 
Murad and Pyun investigate this [6x]. By using unidirectional, bidirectional and LSTM RNNs they evaluate their effectiveness at solving the activity recognition 
problem. The models they propose actually end up outperforming comparable CNNs. Although, CNNs were still used for this project for their relative ease in 
interpretability, implementation and explainability. </p>

# *Systems that use mood to recommend music* 

<p>Rumiantcev published a thesis on an emotion-driven music recommendation system [1y]. While our project is real-time and constantly up to date with user mood, 
this thesis requires a user to answer explicit questions about their mood in a questionnaire before recommendations are given. </p> 

<p>Andjelkovic et. al introduce their system, Moodplay, as an interactive music recommendation system based on artists' mood similarity. They look into interesting 
extensions of the problems we address in our project, such as recommending music based on 
user mood that doesn't necessarily match the users' mood, but instead contrasts it. For example, a sad user may want happy music to help lift them up. 
They approach this by "pathing" from the current perceived emotional state to the target state. They also reinforce the benefits in health of music therapy, including 
positive effects on movement in patients who have suffered a stroke. </p>

