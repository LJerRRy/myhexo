---
title: Leetcode-392-394(共四道)
date: 2016-09-07 01:17:21
tags: [Leetcode,algorithm]
categories: 算法分析
---

[Leetcoode](https://leetcode.com/problemset/algorithms/)上的第392题与第394题

# 题目392 Is Subsequence
## 问题描述

Given a string s and a string t, check if s is subsequence of t.

You may assume that there is only lower case English letters in both s and t. t is potentially a very long (length ~= 500,000) string, and s is a short string (<=100).

A subsequence of a string is a new string which is formed from the original string by deleting some (can be none) of the characters without disturbing the relative positions of the remaining characters. (ie, "ace" is a subsequence of `"abcde"` while `"aec"` is not).

**Example1:**

s = `"abc"`, t = `"ahbgdc"`

Return `true`.

**Example2**

s=`"axc"`,t=`"ahbgdc"`

Return `false`.


## 解题思路

题目大意：给定两个字符串s，t，检查s是否是t的子串。其中s和t都只包含小写字符，t是非常大的字符串（长度大约有50万长），s是一个比较短的字符串长度小于等于100。子串是指该字符串由原来的字符串删除一些字符但不改变字符的相对位置。



* **方法一** 两个for循环遍历一遍。（刚刚开始，我在想int是不是不能50万，后来想到java中int为32位，肯定可以达到50w；
* **方法二** 参考了discuss上的，只需要一个for循环。

## 代码

方法一

```java
public boolean isSubsequence(String s, String t) {
        int ls=s.length();
        int lt=t.length();
        if(ls==0)return true;//空串肯定为t的子串
        int i,m=0;//m标识该从t中哪开始遍历
        for(i=0;i<ls;i++){
            char a = s.charAt(i);
            for(int j=m;j<lt;j++){
                if(a==t.charAt(j)){
                    m = j+1;//下次遍历从j+1开始
                    break;
                }
                m = j + 1;//记录当前遍历到哪了
            }
            if(m>=lt&&i<ls-1)return false;
        }
        return true;
    }
```

方法二

```java
 public boolean isSubsequence(String s, String t) 
    {
        if(t.length() < s.length()) return false;
        int prev = 0;//相当于方法一中的m
        for(int i = 0; i < s.length();i++)
        {
            char tempChar = s.charAt(i);
            prev = t.indexOf(tempChar,prev);//在t中查找tempChar字符，运用indexOf方法，相当于方法一中第二个for循环
            if(prev == -1) return false;
            prev++;
        }
        
        return true;
    }
```


# 题目391 Perfect Rectangle
## 问题描述

[题目链接](https://leetcode.com/contest/2/problems/perfect-rectangle/)

A character in UTF8 can be from 1 to 4 bytes long, subjected to the following rules:

    1. For 1-byte character, the first bit is a 0, followed by its unicode code.
    2. For n-bytes character, the first n-bits are all one's, the n+1 bit is 0, followed by n-1 bytes with most significant 2 bits being 10.
This is how the UTF-8 encoding would work:

```
 Char. number range  |        UTF-8 octet sequence
      (hexadecimal)    |              (binary)
   --------------------+---------------------------------------------
   0000 0000-0000 007F | 0xxxxxxx
   0000 0080-0000 07FF | 110xxxxx 10xxxxxx
   0000 0800-0000 FFFF | 1110xxxx 10xxxxxx 10xxxxxx
   0001 0000-0010 FFFF | 11110xxx 10xxxxxx 10xxxxxx 10xxxxxx
```

Given an array of integers representing the data, return whether it is a valid utf-8 encoding.

**Note:**
The input is an array of integers. Only **the least significant 8 bits** of each integer is used to store the data. This means each integer represents only 1 byte of data.

**Example1:**

```
data = [197, 130, 1], which represents the octet sequence: 11000101 10000010 00000001.

Return true.
It is a valid utf-8 encoding for a 2-bytes character followed by a 1-byte character.
```

**Example2:**

```
data = [235, 140, 4], which represented the octet sequence: 11101011 10001100 00000100.

Return false.
The first 3 bits are all one's and the 4th bit is 0 means it is a 3-bytes character.
The next byte is a continuation byte which starts with 10 and that's correct.
But the second continuation byte does not start with 10, so it is invalid.
```

## 解题思路

题目大意：一个UTF-8编码的字符长度可能为1byte到4byte长，主要取决于以下规则：
1. 对于1byte字符，他的第一位是0，紧接着的是其的Unicode编码
2. 对于n-bytes字符，前n-bits全是1，而n+1位为0，紧跟着的是n-1个字节其前两位为10开始的

给定一个int数组，数组中每个整数都至少是8位来存储数据，这意味着一个整数仅仅代表一个字节的数据

* **方法一** 首先获取第一个整数判断其前几位是1，然后再判断后面几个是否为10（二进制）开始的。参考discuss的

## 代码

方法一

```java
    public int getLen(int s){
        int mask = 0x80;//mask 二进制为10000000
        if((s&mask)==0)return 0;//进行与操作，判断第一位是否为0
        mask>>=1;//mask 现在为 1000000 ，进行右移操作
        if((s&mask)==0)return -1;//第二位为0的话肯定不是utf-8
        int len = 1;
        mask>>=1;
        while((mask!=0)&&(s&mask)==mask){//判断前几位1的个数
            mask>>=1;
            len++;
        }
        return len==7?-1:len;//排除11111111，
    }
    public boolean validUtf8(int[] data) {
       if(data.length==0&&data ==null)return false;
        int  i =0;
        while(i<data.length){
            int s = getLen(data[i]);
            if(s<0||(i+s)>=data.length)return false;
            while (s>0){
                if(data[++i]>>6!=2)return false;
                s--;
            }
            if(s>0)return false;
            i++;//如果数组中还有数要继续判断其是否为utf-8
        }
        return true;
    }
```
