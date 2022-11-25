---
layout: post
read_time: true
show_date: true
title: 2015--"Unsupervised Domain Adaptation by Backpropagation"
date: 2022-11-25 13:32:20 +0800
description: "DANN: The first attempt to incorporate an adversarial training strategy into domain adaptation."
img: posts/20221125/DANN-Structure.png
tags: [Deep Learning, Domain Adaptation, Adversarial Discriminative]
author: Zenvi
toc: yes # leave empty or erase for no table of contents
mathjax: yes
---

Paper Link: [Unsupervised Domain Adaptation by Backpropagation (mlr.press)](http://proceedings.mlr.press/v37/ganin15.pdf)

## Overall Structure

<center><img src="./assets/img/posts/20221125/DANN-Structure.png"></center>

1. Feature Extractor: Maps the source or target images to a feature vector
   + Minimizes the source classification error
   + Maximizes the loss of the domain discriminator (by making the two feature distributions as similar as possible so that the domain discriminator cannot tell whether the input is a source feature vector or a target feature vector)
2. Label Predictor: Maps the source feature vector to a vector of class probabilities
   + Minimizes the source classification error
3. Domain Discriminator: Classifies whether the input feature vector is a source or target feature vector
   + Minimizes the loss of the domain discriminator
4. Gradient Reversal Layer: Ensures that the feature distributions over the two domains are made similar (as indistinguishable as possible for the domain discriminator), thus resulting in the domain-invariant features

## Overall optimization problem:

<center><img src="./assets/img/posts/20221125/loss function.png"></center>

<center><img src="./assets/img/posts/20221125/Optimization Objective.png"></center>

- After gradient reverse layer, the optimization problem becomes:

<center><img src="./assets/img/posts/20221125/loss function after GRL.png"></center>

## Key Results

1. Minimizing the label prediction loss contributes to learning discriminative features
2. Maximizing the domain classification loss contributes to learning domain-invariant features
3. Training the domain discriminator is closely related to the estimation of HΔH divergence