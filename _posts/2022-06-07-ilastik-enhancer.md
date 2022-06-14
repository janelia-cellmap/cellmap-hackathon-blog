---
toc: false
layout: post
description: Dominik Kutra presents a demo on a recent enhancer in ilastik
categories: [ilastik,Random Forests,Open Science,Deep Learning,BioImage]
title: Ilastik Enhancer Demo
image: images/ilastik-logo.png
---
# From Shallow to Deep: Exploiting Feature-Based Classifiers for Domain Adaptation in Semantic Segmentation
Dominik Kutra ([@k-dominik](https://github.com/k-dominik)) from the [Kreshuk group at EMBL-Heidelberg](https://www.embl.org/groups/kreshuk/) shared a demo of the lastest from [ilastik](https://www.ilastik.org), recently published in Frontiers in Computer Science ([Matskevych et al., 2022](https://www.frontiersin.org/articles/10.3389/fcomp.2022.805166/full))

The method trains many different Random Forests on source from full labels, then trains an 'Enhancer' (U-Net) to improve the Random Forest predictions. 
1. Step 1: Train the Random Forest with ilastik (normal workflow)
2. Step 2 Apply the Enhancer for significant improvements

The Enhancer _only_ sees the Random Forest predictions. The model can be found in the [BioImage Model Zoo](https://bioimage.io/#/?tags=mitochondria&id=10.5281%2Fzenodo.6406756).

See more in this twitter thread announcing the method:
{% twitter https://twitter.com/ilastik_team/status/1501089028476706818?s=20&t=KyGJcQ6aSDrx1c0XHFEBVA %}
