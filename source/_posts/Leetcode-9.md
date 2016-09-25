---
title: Palindrome Number
date: 2016-09-20 00:12:12
tags: [Leetcode,algorithm]
categories: 算法分析
---

[Leetcoode](https://leetcode.com/problemset/algorithms/)上的第8题

# 题目9 SPalindrome Number
## 问题描述

Determine whether an integer is a palindrome. Do this without extra space.

## 解题思路

求一个整数是否为回文数字。

1. 0~9肯定是回文数字，负数也不是（开始以为负数也要判断其是否为回文）。
2. 将整数从最低位开始向最高位进行比较，不需要转换为字符串。

## 代码

方法一

```java
public class Solution {
    public boolean isPalindrome(int x) {
        if(x<10&&x>=0)return true;//0~9
        if(x<0)return false;//负数
        int y = x;
        int m = 1;
        int c = 0;//c来存储整数的位数
        while(y/10!=0){//计算整数x有几位
            y/=10;
            m*=10;
            c++;
        }
        c++;
        y=x;//x,y，分别代表从高位和从低位开始
        while(true){
            int t = x/m;//高位的值
            int p = y%10;//低位的值
            if(t!=p)return false;//若不相等则肯定不为回文
            if(c==0||c==1)return true;//若c=0或者c=1代表以及比较完毕，肯定为回文。
            x=x%m;//去掉高位值
            m=m/10;
            y=y/10;//去掉低位
            c=c-2;//位数减2
        }
    }
}
```

方法二

该方法参考的discuss上的。

```java
/**
*1. 将整数x分为两部分，前半部分保存在x，后半部分逆序后保存在v中，
*2. 其中x>v，即若x的位数为奇数时，x则比v多一位。若x>v，x=x/10
*3. 然后再判断x是否和v相等
*4. 这个方法效率z高
*/
public class Solution {
    static int v;
    public static boolean isPalindrome(int x) {
        //optimizations
        if(x<0) return false;
        if(x<10) return true;
        if(x%10==0) return false;
        if(x<100&&x%11==0) return true;
        if(x<1000&&((x/100)*10+x%10)%11==0) return true;

        //actual logic
        v=x%10;
        x=x/10;
        while(x-v>0)
        {
                v=v*10+x%10;
                x/=10;
        }
        if(v>x){v/=10;}
        return v==x?true:false;
    }
}
```


