---
title: String to Integer (atoi)
date: 2016-09-11 13:15:24
tags: [Leetcode,algorithm]
categories: 算法分析
---

[Leetcoode](https://leetcode.com/problemset/algorithms/)上的第8题

# 题目8 String to Integer (atoi）
## 问题描述

Implement `atoi` to convert a string to an integer.

## 解题思路

把字符串转换成整型数。

1. 函数跳过前面的空格字符，然后从第一个字符开始只能为`+`，`-`或者`数字`,之后跟着一串数字。
2. 首先去掉字符串开始的空格字符，然后判断第一个字符是否为`+`,`-`或者`数字`，若不是则返回0；
3. 判断最后解析出来的数字是否溢出，上溢则返回`INT_MAX (2147483647)`,下溢则返回`INT_MIN (-2147483648)`
4. 一定要用**double**来保存整数，不能用long，因为测试用例中比long还大的数。


## 代码

方法一

```java
public class Solution {
    //判断一个字符是否为数字
    public boolean isNum(char s){
        if(s>='0'&&s<='9'){
            return true;
        }else{
            return false;
        }
    }
    //我的方法有点乱。。
    public int myAtoi(String str) {
        double s = 0;
        int flag = 1;//用来保存+，-，若为-，flag=-1
        int size =0;//记录+-符号的个数
        int j;
        for(j=0;j<str.length();++j)if(str.charAt(j)!=' ')break;//去除空格
        if(j<str.length()&&str.charAt(j)!='-'&&str.charAt(j)!='+'&&!isNum(str.charAt(j)))return 0;//不满足条件2直接返回0
        for(int i = j;i<str.length();i++){
            char ch = str.charAt(i);
            if(ch=='-'||ch=='+'){
                size++;
                if(size>1){//符号的个数>1，跳出循环
                    break;
                }
                //判断符号后若不为数字或者该符号在字符串最后则返回0                
                if(i<str.length()-1&&!isNum(str.charAt(i+1))||i==str.length()-1) {
                    return 0;
                }
                flag = ch=='-'?-1:1;
            }
            else {
                if(isNum(ch)) {
                    s = s * 10 + ch - '0';
                }
                else{//整数解析完毕，跳出循环
                    break;
                }
            }
        }
        s = flag*s;
        if(s>Integer.MAX_VALUE)
            return Integer.MAX_VALUE;
        else if(s<Integer.MIN_VALUE)
            return Integer.MIN_VALUE;
        else
            return (int)s;
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


