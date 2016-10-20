---
title: Leetcode-396-399
date: 2016-09-12 22:53:21
tags: [Leetcode,algorithm,BFS]
categories: 算法分析
---

[Leetcoode  Weekly Contest 4](https://leetcode.com/contest/detail/4)总共有四道题

# 题目389 Find the Difference
## 问题描述

Given an array of integers `A` and let `n` to be its length.

Assume Bk to be an array obtained by rotating the array `A` k positions clock-wise, we define a "rotation function" `F` on `A` as follow:

`F(k) = 0 * Bk[0] + 1 * Bk[1] + ... + (n-1) * Bk[n-1]`.

Calculate the maximum value of `F(0), F(1), ..., F(n-1)`.

Note:
n is guaranteed to be less than 105.

**Example:**

```
A = [4, 3, 2, 6]

F(0) = (0 * 4) + (1 * 3) + (2 * 2) + (3 * 6) = 0 + 3 + 4 + 18 = 25
F(1) = (0 * 6) + (1 * 4) + (2 * 3) + (3 * 2) = 0 + 4 + 6 + 6 = 16
F(2) = (0 * 2) + (1 * 6) + (2 * 4) + (3 * 3) = 0 + 6 + 8 + 9 = 23
F(3) = (0 * 3) + (1 * 2) + (2 * 6) + (3 * 4) = 0 + 2 + 12 + 12 = 26

So the maximum value of F(0), F(1), F(2), F(3) is F(3) = 26.
```

## 解题思路


* **方法一**  强行求每个F(n)的值，然后保留最大的，（超时）
* **方法二**  注意到如下规则：

```java
//Sum(A)为数组A元素的和，len为数组长度
F(0)=0*A[0]+1*A[1]+...+(n-1)*A[n-1]
F(1)=F(0)+Sum(A) - A[len -1]*len
...
F(n-1)=F(n-1)+Sum(A) - A[len-n+1]*len
```

## 代码

方法一

```java
//该方法超时，不能通过
public static int maxRotateFunction(int[] A) {
    int max = Integer.MIN_VALUE;//初始化为最小值
    int len = A.length;
    if(len<1)return 0;//如果为空返回0
    for(int i = 0;i<len;i++){
        int m = 0;
        for(int j=0;j<len;j++){
            int s = (len-i+j)%len;//倒置函数
            m = m + j * A[s];
        }
        if(m>max)max = m;
    }
    return max; 
}
```

方法二

```java
public int maxRotateFunction(int[] A) {
        int max = 0;
        int len = A.length;
        if(len<1)return 0;
        int count = 0;
        int s = 0;
        for(int i = 0;i<len;i++){
           count  = count + i*A[i];//计算F(0)
           s += A[i];//计算Sum(A)
        }
        max = count;
        for(int i = 1;i<len;i++){
            count = count + s - A[len-i]*len;//计算F(i)
            if(count > max)max = count;//就行比较或者用max=Math.max(max,count);
        }
        return max;
    }
```


# 题目397 Integer Replacement
## 问题描述

Given a positive integer n and you can do operations as follow:

1. If n is even, replace n with n/2.
2. If n is odd, you can replace n with either n + 1 or n - 1.

What is the minimum number of replacements needed for n to become 1?

**Example1:**

```
Input:
8

Output:
3

Explanation:
8 -> 4 -> 2 -> 1
```

**Example2:**

```
Input:
7

Output:
4

Explanation:
7 -> 8 -> 4 -> 2 -> 1
or
7 -> 6 -> 3 -> 2 -> 1
```
## 解题思路

题目看起来比较简单，就是求一个**正整数**转换成1，**最少**需要多少次变化，变化的过程是指：

1. 整数n为偶数则n=n/2
2. 整数n为奇数则n=(n+1)/2或者n=(n-1)/2

* **方法一**  用递归，不过要注意到java中int的范围是-2147483648到2147483647，若n=2147483647时只能做减法,而且还要和(n+1)/2进行比较;n=1时为递归中值条件，否则则取(n+1)/2和(n-1)/2所求得最小值
* **方法二**  也是用递归，但是用的是**BFS(广度优先搜索算法)**，用队列来保存每次转换的可能值，下次遍历队列，继续遍历队列，直至有一个值为1（表示递归结束，已经找到最小值）。

## 代码

方法一

```java
    public static int integerReplacement(int n) {
        if(n==1)return 0;
        //由于int不能超过2147483647，只能手动计算(2147483647 + 1)的变化值，然后进行比较取最小值
        else if(n==2147483647)
            return Math.min(1+integerReplacement(2147483647-1),2+integerReplacement((2147483646/2) + 1));
        else if((n&1)==0)
            return 1+integerReplacement(n/2);
        else{
            return 2 + Math.min(integerReplacement((n+1)/2),integerReplacement(n/2));
        }
    }
```

方法二

```java
 public int integerReplacement(int n) {
        assert n > 0;
        Queue<Long> queue = new LinkedList<>();//一定是long型的队列，不然要分类讨论
        //n进队
        queue.offer((long)n);
        return bfs(queue, 0);//初始化的队列只有一个值，level初始值0，因为n可能为1.
    }
    
    private int bfs(Queue<Long> oldqueue, int level) {
        Queue<Long> newqueue = new LinkedList<>();//新建一个队列用来保存
        while (!oldqueue.isEmpty()) {
            long n = oldqueue.poll();//出队
            if (n == 1) {
                return level;
            }
            //进队，到新的队列
            if (n % 2 == 0) {
                newqueue.offer(n / 2);
            } else {
                newqueue.offer(n + 1);
                newqueue.offer(n - 1);
            }
        }
        return bfs(newqueue, level + 1);//继续将新的队列递归
    }
```

