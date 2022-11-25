---
layout: post
read_time: true
show_date: true
title:  Unsupervised Domain Adaptation by Backpropagation
date:   2022-11-25 13:32:20 +0800
description: "DANN: The first attempt to incorporate an adversarial training strategy into domain adaptation."
img: posts\20221125\DANN-Structure.png
tags: [Deep Learning, Domain Adaptation: Adversarial Discriminative]
author: Zenvi
toc: yes # leave empty or erase for no table of contents
mathjax: yes
---

# (DANN) Unsupervised Domain Adaptation by Backpropagation

- Overall structure of the proposed model:

[image]

- Overall optimization problem:

[image]

[image]

- After gradient reverse layer, the optimization problem becomes:

[image]

## KEY RESULTS

1. Minimizing the label prediction loss contributes to learning discriminative features
2. Maximizing the domain classification loss contributes to learning domain-invariant features
3. Training the domain discriminator is closely related to the estimation of HΔH divergence