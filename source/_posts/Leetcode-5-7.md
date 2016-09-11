---
title: Leetcode-6-391
date: 2016-09-11 13:15:24
tags: [Leetcode,algorithm]
categories: 算法分析
---

[Leetcoode](https://leetcode.com/problemset/algorithms/)上的第5题与第7题

# 题目5 Longest Palindromic Substring
## 问题描述

Given a string S, find the longest palindromic substring in S. You may assume that the maximum length of S is 1000, and there exists one unique longest palindromic substring.

## 解题思路

给定一个字符串求最长的回文子字符串。方法一和二参考discuss


* **方法一** 用两个指针从可能回文的字符串地方向两边进行判断。如一个奇数长度字符串两个指针从中间开始分别进行比较，而偶数时则是至少中间两个字符串相同（也可能是四个八个等等）。
* **方法二** 基于动态规划，dp(i,j)代表字符串s(i to j)是回文字符串，则dp(i,j)=true，否则dp(i,j)=false。
1. 那么一般情况下dp\[i][j]=dp\[i+1]\[j=1]&&s[i]==s\[j]
2. 或者当j-i<3时，dp\[i][j]=(j-i<3)&&s[i]==s\[j]
## 代码

方法一

```java
public String longestPalindrome(String s) {
        if(s==null|s.isEmpty())return "";
        int max = 0;
        int a = 0, b = 0;//保存最长的字符串数组下标
        for(int i = 0;i<s.length();i++){
            int beg = i,end = i;
            while(end+1<s.length()&&s.charAt(beg)==s.charAt(end+1)){//判断可能为回文字符串的中间
                end++;
            }
            while(end+1<s.length()&&beg-1>=0&&s.charAt(end+1)==s.charAt(beg-1)){//向中间向两边两边开始遍历
                beg--;
                end++;
            }
            if(end - beg + 1>max){//判断该回文字符串是不是最大的字符串
                a=beg;
                b=end;
                max = end - beg + 1;
            }
        }
        return s.substring(a,b+1);
    }
```

方法二

```java
public String longestPalindrome(String s) {
  int n = s.length();
  String res = null;
    
  boolean[][] dp = new boolean[n][n];
    
  for (int i = n - 1; i >= 0; i--) {
    for (int j = i; j < n; j++) {
      dp[i][j] = s.charAt(i) == s.charAt(j) && (j - i < 3 || dp[i + 1][j - 1]);//求得dp的值
            
      if (dp[i][j] && (res == null || j - i + 1 > res.length())) {//dp值为true则该字符串为回文字符串
        res = s.substring(i, j + 1);
      }
    }
  }
    
  return res;
}
```


# 题目7 Reverse Integer
## 问题描述

[题目链接](https://leetcode.com/problems/reverse-integer/)

Reverse digits of an integer.

**Example1:** `x = 123, return 321`

**Example2:** `x = 123, return 321`

## 解题思路

求一个正数(int)的反向数。要注意到**反向之后可能会越界**，java的int类型是32位(-2147483648到2147483648)，例如1010101019的反向数就会越界。其次是**负数取余的值还是负数**。


## 代码

方法一

```java
public int reverse(int x) {
    if(x==0)return 0;
    int y = x;
    long res = 0;//这里用long来求反向数
    while(y!=0){
        res = res*10 + y%10;//负数对正数取余负号保留
        y/=10;
    }
    if(res>Integer.MAX_VALUE||res<Integer.MIN_VALUE){//判断是否越界，越界则反向数为0
        res = 0;
    }
    return (int) res;
}
```