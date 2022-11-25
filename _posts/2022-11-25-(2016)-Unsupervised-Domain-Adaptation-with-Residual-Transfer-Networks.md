---
layout: post
read_time: true
show_date: true
title: 2016--"Unsupervised Domain Adaptation with Residual Transfer Networks"
date: 2022-11-25 15:29:00 +0800
img: posts/20221125/RTN-Structure.png
tags: [Deep Learning, Domain Adaptation, Statistical Matching]
author: Zenvi
toc: yes # leave empty or erase for no table of contents
mathjax: yes
---

Paper Link: [Unsupervised Domain Adaptation with Residual Transfer Networks (neurips.cc)](https://proceedings.neurips.cc/paper/2016/file/ac627ab1ccbdb62ec96e702f07f6425b-Paper.pdf)

Code Link: [https://github.com/thuml/transfer-caffe](https://github.com/thuml/transfer-caffe)

## The Authors Argue That:

- The source and target classifiers differ by a small residual function (A theory that is not testified)

## Overall Structure

<center><img src="./assets/img/posts/20221125/RTN-Structure.png"></center>

1. Use tensor product to fuse the high-level features
2. **Feature Adaptation**: Calculate the MMD based on the fused high-level features (They didn't use the Mk-MMD as proposed in DAN)
3. **Classifier Adaptation**: Use a residual block following the source classifier to approximate target classifier (In plain words: they concatenated a residual block after the source classifier, and add the outputs of the residual block and the target classifier up, the outcome will be fed to the cross entropy loss function, which can be seen as the source domain classification loss)
4. Entropy Minimization

## Overall Optimization Problem

<center><img src="./assets/img/posts/20221125/RTN-Loss.png"></center>

where:

<center><img src="./assets/img/posts/20221125/RTN-f_s.png"></center>

