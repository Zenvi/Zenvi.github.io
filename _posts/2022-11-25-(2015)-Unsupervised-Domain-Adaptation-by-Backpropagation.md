---
layout: post
read_time: true
show_date: true
title: Zenvi's Notes on "Unsupervised Domain Adaptation by Backpropagation"
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

- Overall optimization problem:

[image]

[image]

- After gradient reverse layer, the optimization problem becomes:

[image]

## KEY RESULTS

1. Minimizing the label prediction loss contributes to learning discriminative features
2. Maximizing the domain classification loss contributes to learning domain-invariant features
3. Training the domain discriminator is closely related to the estimation of HΔH divergence