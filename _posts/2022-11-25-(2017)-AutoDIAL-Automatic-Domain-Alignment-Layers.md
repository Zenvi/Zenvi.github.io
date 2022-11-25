---
layout: post
read_time: true
show_date: true
title: 2017--"AutoDIAL: Automatic Domain Alignment Layers"
date: 2022-11-25 20:17:00 +0800
img: posts/20221125/AutoDIAL-Structure.png
tags: [Deep Learning, Domain Adaptation, Statistical Matching]
author: Zenvi
toc: yes # leave empty or erase for no table of contents
mathjax: yes
---



Paper Link: [AutoDIAL: Automatic DomaIn Alignment Layers (thecvf.com)](https://openaccess.thecvf.com/content_ICCV_2017/papers/Carlucci_AutoDIAL_Automatic_DomaIn_ICCV_2017_paper.pdf)

Supplementary Material: [Carlucci_AutoDIAL_Automatic_DomaIn_ICCV_2017_supplemental.pdf (thecvf.com)](https://openaccess.thecvf.com/content_ICCV_2017/supplemental/Carlucci_AutoDIAL_Automatic_DomaIn_ICCV_2017_supplemental.pdf)

Code Link: [https://github.com/ducksoup/autodial](https://github.com/ducksoup/autodial)

## Key Elements:

<center><img src="./assets/img/posts/20221125/AutoDIAL-Structure.png"></center>

- Softmax loss on source samples
- Entropy minimizaiton on target samples
- DA-layers to adapt the features

## DA Layer:

- The DA layer used for source data and the DA layer used for target data is probably going to be different, because there is a large probability that the distributions of source and target are different.

- Every DA layer will have an $\alpha$ parameter, used for determining how deeply the DA layer will adapt to its input data.

- DA layer specifics:

  1. Let's first construct two new distributions:

     <center>$q_\alpha^{st} = \alpha q^s + (1 - \alpha) q^t$</center>

     <center>$q_\alpha^{ts} = \alpha q^t + (1 - \alpha) q^s$</center>

     where: $\alpha \in [0.5,1]$

     We can se $q_\alpha^{st}​$ as the source distribution being contaminated by the target distribution and vice versa.

  2. And according to the calculation process of BN layer, we can directly write out the output expression for DA layer:

     <center>$DA(x_s ; \alpha) = \frac {x_s - \mu_{st,\alpha}} {\sqrt {\epsilon + \sigma^2_{st,\alpha}}}$</center>

     <center>$DA(x_t ; \alpha) = \frac {x_t - \mu_{ts,\alpha}} {\sqrt {\epsilon + \sigma^2_{ts,\alpha}}}$</center>

  3. $\alpha$ will be learned during training process. It directly depends how deeply the adaptation level of the DA layer currently is. 

     $\alpha=0.5$ means no adaptation at all. In other words, current DA layer makes the same transformation for data from source and target domains.

     $\alpha=1$ means deeply adaptation

## My Comments:

1. $q^{st}_\alpha$ and $q^{ts}_\alpha$ is definitely unmeasurable, because source and target distributions are unmeasurable. So how did the authors calculate $\mu$ and $\sigma$ for the two mixed distributions?
2. I'm having trouble with understanding the training process in the original paper.
3. Can I try incorporate DA Layer or AdaBN into DAN? With some statistical improvement.