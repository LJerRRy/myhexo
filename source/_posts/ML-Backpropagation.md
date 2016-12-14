---
title: Backpropagation and  cost function for neural network
date: 2016-10-31 09:12:05
tags: [ML]
categories: 学习笔记
---

## Backpropagation 反向传播算法


## Multivariate Linear Regression

### Mutiple Features

### Gradient Descent for Multiple Variables

### Gradient Descent in Practice (Feature Scaling)

Make sure features are on a similar scale.

Get every Feature into approximately a -1 ≤ x<sub>i</sub> ≤ 1 range
将数据集（训练集）进行缩放，原因是直接使用原始的数据集进行梯度下降，迭代次数会非常多而且相当复杂。

**Mean normalization** Replace x<sub>i</sub> with x<sub>i</sub> - u<sub>i</sub> (average value) / s<sub>i</sub> (range) to make features have approximately zero mean (Do not apply to x<sub>0</sub> = 1)

### Gradient Descent in Practice (Learning Rate)

1. "Debugging": How to make sure gradient descent is working correctly

example automatic convergence test: Declare convergence if  J(θ) decrease by less than 10 <sup>-3</sup> in one iteration
Gradient descent not working : use smaller `α` 

`α` 很足够小，那么每次迭代后的梯度都会下降，但是收敛的速度很慢
`α` 太大了，不能够每次迭代梯度都能下降，可能造成不收敛（may not converge or slow converge)

2. How to choose learning rate `α` 

### Features and polynomial Regression(多项式回归)

That is, how to fit a polynomial, like a quadratic function, or a cubic function, to your data

## Computing Parameters Analytically

### Normal Equation(标准方程法)

Normal Equation: Method to solve for θ Analytically.
θ=(X<sup>T</sup>X)<sup>-1</sup>X<sup>T</sup>y

m training examples, n features
the disadvantages and advantages between Gradient Descent and Normal Equation
Gradient Descent                               Normal Equation
• Need to choose `α`                           • No need to choose `α`  
• Needs many iterations.                       • Don’t need to iterate.
• Works well even                              • Need to compute (X<sup>T</sup>X)<sup>-1</sup> 时间复杂度 O(n<sup>3</sup>)
when `n` is large.                             • Slow if `n` is very large (N>10000)
                            
### Normal Equation Noninvertibility

Normal Equation : θ=(X<sup>T</sup>X)<sup>-1</sup>X<sup>T</sup>y
what if X<sup>T</sup>X is non-invertible?(singular/degenerate)
1. Redundant features(linearly dependent). E.g. x<sub>1</sub>=size in feet <sup>2</sup> x2 = size in m<sup>2</sup>
2. Too many features(e.g.m≤n)
  ·  Delete some features, or use regularization
  
```
prinv(x'*x)*x'*y
pinv and inv
pinv函数可以伪逆(Return the pseudoinverse of X.)

```

## Octave Tutorial

```
format long/short
v = 1:0.1:2
v = 1:6
ones(1,3)
C = 2*ones(2,3)
v = rand(3,3) 随机随机矩阵
w = randn(1,1000)高斯随机矩阵
eye(4)单位矩阵
help rand
size(A)返回矩阵大小，size(A,1)返回矩阵的行数
who/whos
v = princeY(1:10)
load princeY.dat
save hello.mat v
save hello.txt v -ascii

A = [1 2;3 4;5 6]
A(3,2)
A(2,:)
A = [A,[100;101;102]]
A(:)

A*C
A.*C
abs(v)
log(v)
exp(v)
A'
max(a)
[val,ind]=max(a)
max(A)
magic(Number)

sum
prod
floor
ceil
max(A,[],1)
max(max(A))
sum(sum(A.*eye(9)))
flipud(eye(9))
```
## Word List

Feature Scaling: 特征缩放
Mean normalization：均值归一化
iteration： 迭代
converge：使收敛
Noninvertibility：不可逆性
round off your answer to two decimal ：保留两位小数
unvectorized/verctorized : 未向量化的/向量化的