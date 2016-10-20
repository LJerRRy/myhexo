---
title: Container With Most Water(Leetcode 11)
date: 2016-09-11 13:15:24
tags: [Leetcode,algorithm]
categories: 算法分析
---

[Leetcoode](https://leetcode.com/problemset/algorithms/)上的第11题

# 题目8 String to Integer (atoi）
## 问题描述

Given n non-negative integers `a1, a2, ..., an`, where each represents a point at coordinate (i, ai). n vertical lines are drawn such that the two endpoints of line i is at (i, ai) and (i, 0). Find two lines, which together with x-axis forms a container, such that the container contains the most water.<br>
Note: You may not slant the container.

## 解题思路

给定n个非负整数，这n个整数分别为`a1, a2, ..., an`,每个整数都对应一个坐标如`ai`对应坐标为(i,ai)，该坐标和点(i,0)形成的线段，从n条线段中找出两条使得形成的容器装水最多，容器不能倾斜。

**方法一**


## 代码

方法一

```java
//超时。。。
public class Solution {
    public int maxArea(int[] height) {
        int len = height.length;
        int max_water = 0;
        for(int j =0;j<len;j++){
            for(int i = j+1;i<len;i++){
                //取长度较小的边，类似木桶原理
                int h = height[i]>height[j]?height[j]:height[i];
                int w = (i-j)*h;
                if(max_water<w){
                    max_water = w;
                }
            }
        }
        return max_water;
    }
}
```

方法二

该方法参考的discuss上的。

```java
public class Solution {
    public int myAtoi(String str) {
        double result = 0;
        int POrN = 1;
        int count = 0;//用来去掉字符串开始时的空格
        char[] charArr = str.toCharArray();
        for(char c:charArr){
            count ++;
            if( c >='0' && c <='9' ){
                result *= 10;
                result += ( c - '0');
            }else if( c == '-' && count == 1){
                POrN = -1;
            }else if( c == '+' && count == 1){
                POrN =  1;
            }else if( c == ' ' && count == 1){
                //刚刚开始时count一定为1，若这时字符也恰好为空格，则count--，
                //下次判断又可以判断了
                count --;
            }else{
                break;
            }
            
        }
        if( result > Integer.MAX_VALUE ){
            if(POrN == 1)
                return Integer.MAX_VALUE;
            else
                return Integer.MIN_VALUE;
        }else{
            return (int)(result * POrN);
        }
    }
}
```


