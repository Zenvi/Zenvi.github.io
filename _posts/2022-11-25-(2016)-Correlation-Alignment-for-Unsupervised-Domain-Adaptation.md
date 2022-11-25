---
layout: post
read_time: true
show_date: true
title: 2016--"Correlation Alignment for Unsupervised Domain Adaptation"
date: 2022-11-25 15:58:00 +0800
img: posts/20221125/CORAL-Structure.png
tags: [Deep Learning, Domain Adaptation, Statistical Matching]
author: Zenvi
toc: yes # leave empty or erase for no table of contents
mathjax: yes
---

Paper Link: [https://arxiv.org/pdf/1612.01939.pdf](https://arxiv.org/pdf/1612.01939.pdf)

Code Link: [https://github.com/VisionLearningGroup/CORAL](https://github.com/VisionLearningGroup/CORAL)

## What Had the Authors Proposed

1. CORrelation ALignment (CORAL): minimizes domain shift by aligning the second-order statistics of source and target distributions
2. A solution that applies a linear transformation to source features to align them with target features before classifier training
3. How to apply CORAL to classifier weights
4. How to apply CORAL to deep neural networks

## The Steps of the Linear Transformation

<center><img src="./assets/img/posts/20221125/CORAL-LinearT.png"></center>

1. Normalize the source and target features to zero mean and unit variance
2. Remove the feature correlations of the source domain, which can be seen as the procedure of "de-coloring" the source feature
3. Add the correlation of the target domain to the source features, which can be seen as "re-coloring" the source feature to a target-feature-style

+ Notes: the process of deriving the linear transformation solution requires a high level mathematical skill. The derivation is also where I learn a lot from the paper. You can also review the process whenever necessary as practice

## Deep CORAL

<center><img src="./assets/img/posts/20221125/CORAL-Structure.png"></center>

<center>$L_{CORAL}=\frac {1}{4d^2}|| C_s-C_t||_F^2$</center>

Where the covariance matrices of the source and target data are given by:

<center>$ C_s=\frac {1}{n_s-1}(D_S^T D_S - \frac {1}{n_s}(\mathbb 1^T D_S)^T (\mathbb 1^T D_S))$</center>

<center>$C_t=\frac {1}{n_t-1}(D_T^T D_T - \frac {1}{n_t}(\mathbb 1^T D_T)^T (\mathbb 1^T D_T))$</center>

## What Can I Improve:

- The calculation of CORAL is not complex. Plus, CORAL is only aligning the second moment statistics of the source and target distribution, which I think is far away from aligning two distributions. Especially after so many years of development, monster-order moment alignment is already in the literature, CORAL shows little advantage over the current approaches.
- But CORAL is computationally efficient, anytime your work requires reducing computational load, you can consider CORAL.