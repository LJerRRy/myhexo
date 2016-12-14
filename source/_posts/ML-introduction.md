---
title: Introduction of Machine Learning
date: 2016-10-26 12:11:05
tags: [ML]
categories: 学习笔记
---

机器学习是一门研究在非特定编程条件下让计算机采取行动的学科。最近二十年，机器学习为我们带来了自动驾驶汽车、实用的语音识别、高效的网络搜索，让我们对人类基因的解读能力大大提高。当今机器学习技术已经非常普遍，您很可能在毫无察觉情况下每天使用几十次。许多研究者还认为机器学习是人工智能（AI）取得进展的最有效途径。在本课程中，您将学习最高效的机器学习技术，了解如何使用这些技术，并自己动手实践这些技术。更重要的是，您将不仅将学习理论知识，还将学习如何实践，如何快速使用强大的技术来解决新问题。最后，您将了解在硅谷企业如何在机器学习和AI领域进行创新。 本课程将广泛介绍机器学习、数据挖掘和统计模式识别。相关主题包括：(i) 监督式学习（参数和非参数算法、支持向量机、核函数和神经网络）。(ii) 无监督学习（集群、降维、推荐系统和深度学习）。(iii) 机器学习实例（偏见/方差理论；机器学习和AI领域的创新）。课程将引用很多案例和应用，您还需要学习如何在不同领域应用学习算法，例如智能机器人（感知和控制）、文本理解（网络搜索和垃圾邮件过滤）、计算机视觉、医学信息学、音频、数据库挖掘等领域。

A computer program is said to learn from experience E with respect to some task T and some performance measure P, if its performance on T, as measured by P, improves with experience E.

*careful abut the meanning of E P T*

Example

```
Classifying emails as spam or not spam.---> T
Watching you label emails as spam or not spam. --->E 
The number (or fraction) of emails correctly classified as spam/not spam. ---->P
```

## supervised learning（有监督的学习）  

the term supervised learning refers to the fact that we gave the algorithm a data set in which the "right answers" were given. 
### regression problem    

To define with a bit more terminology this is also called a regression problem and by regression problem I mean we're trying to predict a **continuous** value output.

### classification problem  

The term classification refers to the fact that here we're trying to predict a **discrete** value output: zero or one, malignant or benign. 
example:  Given email labeled as spam/not spam, learn a spam filter(垃圾邮件的分类)

```
a quadratic function or a seconde-order polynomial一个二次函数或者一个二次多项式
a breast cancer as malignant or benign 恶性/良性
clump thickness 
uniformity of cell size/shape
```

(a) Regression - Given a picture of Male/Female, we have to predict his/her age on the basis of the given picture.
(b) Classification - Given a patient with a tumor/diabetes, we have to predict whether the tumor is malignant or benign.


## unsupervised learning（无监督的学习）or clustering（聚类）

Unsupervised learning allows us to approach problems with little or no idea what our results should look like. We can derive structure from data where we don't necessarily know the effect of the variables.

examples

1. google news
2. understanding genomics(**clustering**). Take a collection of 1,000,000 different genes, and find a way to automatically group these genes into groups that are somehow similar or related by different variables, such as lifespan, location, roles, and so on.
3. Cocktail(鸡尾酒) party problem algorithm(**Non-clustering**). The "Cocktail Party Algorithm", allows you to find structure in a chaotic environment. (i.e. identifying individual voices and music from a mesh of sounds at a cocktail party).
Octave(similar to Matlab)
`[W,s,v] = svd((repmat(sum(x.*x,1),size(x,1),1).*x)*x');`

4. The market segmentation example 
5.  Astronomical data analysis


## Linear regression with one variable

Training Set-->Learning Algorithm --> hypothesis(假设)

Linear regression with one variable == univariate linear regression

**cost function** == squared errror cause function
**Gradient Descent**(梯度下降) can coverge to a local minimum, even with the learning rate `α` **fixed**. As we approach a local minimum, gradient descent will automatically take smaller steps. So, no need to decrease `α` over time.(the result is a local optimus)
If `α` is too small,'gradient descent can be slow.If `α` is too large, gradient descent can overshoot the minimum. It may fail to converge, or even diverge.
**Batch Gradient Descent**  batch : Each step of gradient descent uses all the training examples.

## Linear Algebra Review

**Matrix** : Rectangular array of numbers
Dimension of matrix: number of rows x(by) number of columns

**Vector** : An n x 1 matrix.  --> n-dimensional vector

**Indentity Matrix** 

**Inverse Matrix**

**Transpose Matrix**


## WordList


1. a quadratic function or a seconde-order polynomial一个二次函数或者一个二次多项式
2. a breast cancer as malignant or benign 恶性/良性
3. clump thickness 肿瘤块的浓度
4. uniformity of cell size/shape
5. fraction of emails correctly classified as spam / not spam.
6. You have a large **inventory** of identical items
7. **Cocktail** party problem
8. Machine learning is the field of study that gives computers the ability to learn without being **explicitly**programmed.
9. contour plots/figures
10. the derivative term
11. caculus
12. convex function == bowl-shaped
13. scalar multiplication == real number multiplication
