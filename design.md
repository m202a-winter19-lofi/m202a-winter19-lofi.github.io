---
layout: page
title: "Design"
---

# Overview



![LOFI diagram]("{{ '/assets/images/lofi_diag.png' | prepend: site.baseurl | prepend: site.url }}")

LOFI takes user inputs such as their mood, estimated using their heart rate variability, and their activity, estimated using a convolutional neural network, along with user preferences for certain music and recommends songs accordingly. The recommender algorithm implements an intuitive K-nearest neighbors algorithm to find songs "closest" to the user's mood and activity in the latent valence-arousal-tempo space detailed below, returning the top K recommendations to the user by running the algorithm on a compact song metadata database on an app. In total, the system makes up a closed feedback loop where song recommendations that change a user's mood can in turn change future recommendations.



# Mood estimation

## Representing mood in 2 dimensions: the valence-arousal space



## Heart rate variability (HRV) and the VA space 

x



# Activity recognition

## Training a model 

x

## Convolutional neural network (CNN) design

x



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