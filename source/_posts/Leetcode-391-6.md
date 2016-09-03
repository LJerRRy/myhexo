---
title: Leetcode-389-390
date: 2016-09-04 00:12:01
tags: [Leetcode,algorithm]
categories: 算法分析
---

[Leetcoode](https://leetcode.com/problemset/algorithms/)上的第6题与第391题

# 题目6 ZigZag Conversion
## 问题描述

The string "PAYPALISHIRING" is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)

```
P   A   H   N
A P L S I I G
Y   I   R
```

And then read line by line: "PAHNAPLSIIGYIR"
Write the code that will take a string and make this conversion given a number of rows:
`string convert(string text, int nRows);`
convert("PAYPALISHIRING", 3) should return "PAHNAPLSIIGYIR".

## 解题思路

其实刚刚看到这个题目时，看了很久都不知道题目意思，然后去wiki了[Zigzag](https://en.wikipedia.org/wiki/Zigzag)的意思，指锯齿状，而且锯齿的角度是平行的且每隔一条线之间的两条行平行。简而言之就是多个`W`连接起来。
例如：
![](img/leetcode6.png)

```java
String s="123456789";
convert(s,3);
//输出的字符串应该为159246837
```

* **方法一** 用一个字符串数组来保存要输出每行的字符串，最后将字符串数组依次输出。
* **方法二** 寻找每行之间的规律，可以发现第一行和最后一行字符之间数组下标值相差（numRows-1）\*2，而其他行除了下标相差（numRows-1)\*2之外还有一个数，即该数是前一个数加上（numRows-1-i）\*2，这里i为行数（从0开始）。

## 代码

方法一

```java
略
```

方法二

```java
public String convert(String s, int numRows) {
        int len = s.length();
        if(numRows<=1||len==0)return s;//只有一行，或者字符串为空时直接返回s
        String res = "";//要输出的字符串
        for(int i = 0;i<numRows;i++)
        {
            for(int j = i;j<len;j+=(numRows-1)*2){
                res = res + s.charAt(j);
                if(i>0&&i<len-1){//除了第一行和最后一行
                    int k = j + (numRows - i - 1)*2;//之间的数的下标
                    if(k<len){//小于字符串长度
                        res += s.charAt(k);
                    }
                }
            }
        }
        return res;
    }
```


# 题目391 Perfect Rectangle
## 问题描述

[题目链接](https://leetcode.com/contest/2/problems/perfect-rectangle/)

Given N axis-aligned rectangles where N > 0, determine if they all together form an exact cover of a rectangular region.

Each rectangle is represented as a bottom-left point and a top-right point. For example, a unit square is represented as [1,1,2,2]. (coordinate of bottom-left point is (1, 1) and top-right point is (2, 2)).

**Example1:**

```
rectangles = [
  [1,1,3,3],
  [3,1,4,2],
  [3,2,4,4],
  [1,3,2,4],
  [2,3,3,4]
]

Return true. All 5 rectangles together form an exact cover of a rectangular region.
```

**Example2:**

```
rectangles = [
  [1,1,2,3],
  [1,3,2,4],
  [3,1,4,2],
  [3,2,4,4]
]

Return false. Because there is a gap between the two rectangular regions.
```

## 解题思路



* **方法一**  用数组，两个数组，一个用来保存未被删除的。但是该方法容易内存超过限制，不能通过leetcode。
* **方法二** 根据题设要求的数字移除过程，可以发现每执行完一趟数字移除操作，列表中剩余相邻数字之间的差都会加倍。（参考别人的）

## 代码

方法一

```java
    public static int lastRemaining2(int n) {
        int[] a = new int [n];
        int[] b = new int [n];
        for(int i = 0;i<n;i++)
            a[i]=i+1;
        int k = n;
        while(k>1){
            int i =0,j=0;
            while(i<k-1){//正向删除
                b[j++]=a[i+1];//复制
                i+=2;
            }
            k=k/2;
            if(k!=1){
            for(j=k-1,i=0;j>=0;j-=2){//逆向删除
                b[j]=0;//直接将其改为0
            }}
            for(i=0,j=0;i<k;i++){
                if(b[i]!=0){
                    a[j++]=b[i];//复制
                }
            }
            k=k/2;
        }
        return a[0];
    }
```

方法二

参考了[书影](http://bookshadow.com/weblog/2016/08/28/leetcode-elimination-game/)

```java
public static int lastRemaining3(int n) {
    int a=1,p=1,cnt=0;
    while (n>1){
        n/=2;
        cnt++;//执行的cnt趟
        p*=2;//数字间的间隔
        if(cnt%2==1){
            a += p/2 + p*(n-1);
        }else {
            a -= p/2 + p*(n-1);
        }
    }
    return a;
}
```

