---
title: Leetcode-4
categories: 算法分析
date: 2016-08-28 23:00:32
tags: [Leetcode,algorithm]
---

[Leetcode](https://leetcode.com/problems/median-of-two-sorted-arrays/)上算法题四，求两个已排序数组的中位数。

## 问题描述

There are two sorted arrays nums1 and nums2 of size m and n respectively.

Find the median of the two sorted arrays. The overall run time complexity should be O(log (m+n)).

**Example 1:**
```
nums1 = [1, 3]
nums2 = [2]

The median is 2.0
```

**Example 2:**
```
nums1 = [1, 2]
nums2 = [3, 4]

The median is (2 + 3)/2 = 2.5
```

## 解题思路
* **方法一**  将两个数组合并为一个有序数组a，根据两个数组长度的总长度n分类讨论：
  * 偶数则取数组a下标为n/2-1和n/2的取均值为所求的中位数，**注意：数组为整数，应该除以2.0，转换为浮点数。**
  * 奇数则取数组a下标为(n+1)/2-1的值为所求的中位数。
* **方法二** 分开求(未完成)

## 算法效率
方法一的空间复杂度为O(m+n),时间复杂度就是遍历一遍A,B数组为O(m+n);<br>
方法二


## 代码

### 方法一

```java
public static double findMedianSortedArrays2(int[] nums1, int[] nums2) {
        int len = nums1.length + nums2.length;
        int[] a = new int[len];
        int i = 0, j = 0,k = 0;
        while (i<nums1.length&&j<nums2.length){
            if(nums1[i]<nums2[j]){
                a[k++]=nums1[i++];
            }else {
                a[k++]=nums2[j++];
            }
        }
        //下面的while 只会执行一个
        while (i<nums1.length) a[k++]=nums1[i++];
        while (j<nums2.length) a[k++]=nums2[j++];
        if(len%2==0)
            return (a[len/2-1]+a[len/2])/2.0;//注意：数组为整数，应该除以2.0
        else
            return a[(len+1)/2-1];
    }
```


### 方法二

```java
public static double findMedianSortedArrays(int[] nums1, int[] nums2) {
        int len = nums1.length + nums2.length;
        int count = 0, i = 0, j = 0;
        int flag = 0;//flag 为1时表示数组1进行了++操作，为2表示数组2进行了++操作
        if (len % 2 == 0) {
            int m, n;
            while (i < nums1.length && i < nums2.length) {
                if (count == len / 2) {
                    if (flag == 1) {//数组1中有一个中位数其序号为i,另一个中位数序号可能为i+1,j,j+1中的一个
                        if (nums1[i] <= nums2[j]) {//另一个中位数为j
                            return (nums1[i] + nums2[j]) / 2.0;
                        } else if (nums1[i + 1] > nums2[j + 1])

                    }
                }
            }
            return (nums1[i] + nums2[j]) / 2;
        } else {
        }
    }
```