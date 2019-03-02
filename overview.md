---
layout: page
title: "Overview"
---
Welcome! Below is a quick overview of some essentials of the project. To begin the report proper, start by checking out the <a href="{{ '/abstract' | prepend: site.baseurl | prepend: site.url }}">abstract</a>.


# Download

## Source code

* Android Studio project file 
* "VAT" dataset of songs embedded with valence, arousal, tempo 
* Dataset creation Jupyter notebook 
* CNN training and exporting Jupyter notebook 
* App APK




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
* ?

## Week 10
* ?




# About the authors

## Juan Carlo Rebanal (005227239)

Plays Street Fighter 3

## Jeannie Hur (???)

Eats dried lemons

# What does LOFI mean? 

Glad you asked...