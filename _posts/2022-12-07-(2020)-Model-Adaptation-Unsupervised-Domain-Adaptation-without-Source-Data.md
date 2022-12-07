---
layout: post
read_time: true
show_date: true
title: 2020--"Model Adaptation：Unsupervised Domain Adaptation without Source Data"
date: 2022-12-07 15:24:00 +0800
img: posts/20221207/ModelAdaptation-Structure.png
tags: [Deep Learning, Domain Adaptation, SFDA]
author: Zenvi
toc: yes # leave empty or erase for no table of contents
mathjax: yes
---

Paper Link: [Model Adaptation: Unsupervised Domain Adaptation Without Source Data (thecvf.com)](https://openaccess.thecvf.com/content_CVPR_2020/papers/Li_Model_Adaptation_Unsupervised_Domain_Adaptation_Without_Source_Data_CVPR_2020_paper.pdf)

## Key Elements

<center><img src="./assets/img/posts/20221207/ModelAdaptation-Structure.png"></center>

1. Target Generation:

    +  Collaborative Class Conditional GAN (3CGAN)

        +  Domain Discriminator D:

           <center>$ \max_{\theta_D} \mathbb E_{x_t \sim  D_t } [log D(x_t)] + \mathbb E_{y,z}[log(1-D(G(y,z)))]$</center>

           Which is try to tell whether its inputs are original target samples or generated target sample

        +  Generator G:

           <center>$l_{adv}(G)=\mathbb E_{y,z}[logD(1-G(y,z))]$</center>

           <center>$\min_{\theta_G}l_{adv}+\lambda_sl_{sem}$</center>

           Which is trying to confuse the Domain Discriminator D

           And minimize the cross-entropy loss

        +  Fixed Predictor C (Pretrained on source domain):

           <center>$l_{sem}(G)=\mathbb E_{y,z}[-ylog_{p_{\theta_C}}(G(y,z))]$</center>

           Which is there to check whether the generated samples are identical to its original labels

2. Model Adaptation:

   + This time we don't fix the pretrained predictor C anymore

   + The final optimization objective:

     <center>$\min_{\theta_C} \lambda_gl_{gen} + \lambda_w l_{wReg} + \lambda_{clu} l_{cluReg} ​$</center>

   + Basic generation loss (which is the cross entropy loss for the generated target-like samples)

     <center>$l_{gen}=\mathbb E_{y,z}[-ylog_{p_{\theta_C}}(x_g)]$</center>

   + Weight Regularization (which is trying to make the newly trained classifier not too different from the original predictor C)

     <center>$l_{wReg} =||\theta_C - \theta_{C_s}||^2$</center>

   + Clustering-based Regularization (Entropy Minimization + KL Divergence between the distribution of target samples and the distribution of perturbated target samples, the KL Divergence is trying to make the prediction model locally smooth for each unlabeled target sample)

     <center>$l_{cluReg} =\mathbb E_{x_t \sim D_t} [-p_{\theta_C}(x_t) log_{p_{\theta_C}}] + [KL(p_{\theta_C} (x_t) || p_{\theta_C} (x_t + \tilde r))]$</center>