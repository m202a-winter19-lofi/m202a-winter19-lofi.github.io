---
layout: page
title: "Overview"
---
Welcome! Below is a quick overview of some essentials of the project. To begin the report proper, start by checking out the <a href="{{ '/abstract' | prepend: site.baseurl | prepend: site.url }}">abstract</a>.


# Download

## Source code

* <a href="https://github.com/m202a-winter19-lofi/lofi">Android Studio project</a>
* <a href="https://github.com/m202a-winter19-lofi/lofi/tree/master/app/src/main/assets">"VAT" dataset of songs embedded with valence, arousal, tempo</a>
* <a href="https://github.com/m202a-winter19-lofi/lofi/blob/master/app/src/main/assets/activity_recognizer_4.tflite">TensorFlow Lite model of CNN used</a>
* <a href="https://github.com/jcr179/misc/blob/master/dataset_creation.ipynb">Dataset creation Jupyter notebook</a>
* <a href="https://github.com/jcr179/misc/blob/master/CNN_6.ipynb">CNN training and exporting Jupyter notebook</a>
* <a href="https://github.com/m202a-winter19-lofi/lofi/blob/master/app/build/outputs/apk/debug/app-debug.apk">App APK</a> (Min API level is 21 = 5.0, Lollipop)
* Hexiwear code (PPG data to SDNN and LF/HF + Bluetooth transmission)
* PPG signal processing code 
* <a href="https://github.com/m202a-winter19-lofi/raspberry_pi_zero_w">Code on the Raspberry Pi Zero W</a> (includes installed packages list)




# Timeline 

## Week 1
* Broadly searched for project ideas 

## Week 2 
* Narrowed interests to neural networks, biomedical 

## Week 3
* Established broad idea of project and applications 
* Background research on effects of music on mood 
* Looked into prior work of music mood classification

## Week 4
* Made project goals concrete, established timeline and deadlines 
* Research of emotion representation systems, activity recognition methods 
* Surveyed options for different components of project toolchain 
* Explored Hexiwear capabilities of heart rate sensing and BLE communication

## Week 5
* Researched different song databases
* Found Deezer dataset of valence/arousal-embedded songs 
* Found Million Songs dataset of songs with several high-level features 
* Merged datasets to create valence/arousal/tempo dataset of 3,514 songs for recommendation

## Week 6
* Found WISDM activity prediction dataset 
* Wrote functions for preprocessing and windowing sensor data 
* Trained 1D convolutional neural network over different hyperparameters, architectures
* Exported best model (test accuracy of 99.7%, 50-25-25 train-validation-test split) as .h5

## Week 7
* Worked on extracting heart rate data and pedometer data from Hexiwear 
* Began writing Android app 
* Converted .h5 file of network model to .tflite to be able to use TensorFlow Lite 
* Implemented CNN on Android app using live accelerometer data 

## Week 8 
* Stored storage-optimized dataset on app for lookup and song recommendation
* Various cleanup and helper function writing for app 
* Implemented manual valence/arousal/tempo entry returning top K song recommendations
* Began working on this project website 

## Week 9
* Implemented various versions of SDNN and LF/HF measurement algorithms for VA estimation 
* Evaluated activity recognition and stride rate estimation deployed on smartphone 
* Evaluated SDNN and LF/HF measurement with a test subject 
* Fleshed out app features and UI
* Uploaded source code to project site 

## Week 10
* Implemented Raspberry Pi Zero W 
* Tested and evaluated entire system 
* Created demo video  

# About the authors

### Juan Carlo Rebanal (UID 005227239)

Juan is a Masters student in Electrical and Computer Engineering at UCLA. He is most interested in deep learning applications, and also enjoys working with machine learning. 
Juan trained and implemented the convolutional neural network featured in this project for activity recognition with classification accuracy of 99.87%. He also surveyed, 
preprocessed and worked with the datasets used in the project. Juan also developed the Android app that implements the project, and implemented the Raspberry Pi Zero W 
in the project system. While waiting for models to train, Juan likes to create and discover music, play fighting games like Street Fighter 3: 3rd Strike, learn languages, and to 
exercise. 

### Jeannie Hur (UID 504955572)

Jeannie is an Electrical Engineering undergraduate at UCLA. She designed the signal processing of the photoplethysmography signal (PPG) measured with the Hexiwear 
and implemented the code to calculate heart rate variability. She handled most of the coding of the Hexiwear. When she’s not debugging the Hexiwear, she enjoys 
trying interesting food from Trader Joe’s and occasionally walking in parks.

### What does LOFI mean? 

LoFi stands for Logical Fitness. We refer to using a logical system to recommend music to improve physical and mental fitness. Though at its core, the project name was 
inspired by those lo-fi hip-hop playlists that have popped up across YouTube in the last few years, often making up various "study/chill/sleep" playlists. So we wanted to fit in the 
tongue-in-cheek reference too. (: