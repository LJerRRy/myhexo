---
title: Palindrome Number
date: 2016-10-25 00:16:23
tags: [Leetcode,algorithm]
categories: 算法分析
---

[Leetcoode](https://leetcode.com/problemset/algorithms/)上的第406题

# 题目406 Queue Reconstruction by Height
## 问题描述

Suppose you have a random list of people standing in a queue. Each person is described by a pair of integers `(h, k)`, where h is the height of the person and `k` is the number of people in front of this person who have a height greater than or equal to `h`. Write an algorithm to reconstruct the queue.

Example

```
Input:
[[7,0], [4,4], [7,1], [5,0], [6,1], [5,2]]

Output:
[[5,0], [7,0], [5,2], [6,1], [4,4], [7,1]]
```

## 解题思路

刚刚看到题目时候是想按照身高进行从大到小排序，如果第一个数相同则第二个数小的要大（即要在前面）。
例如排序后序列为`[[7,0], [7,1], [6,1], [5,0], [5,2], [4,4]] `
然后从已排序好的数组people数组第一个元素开始，放入到数组result中，放入的位置就是离result开始位置偏移了元素第二个数字后的位置。如下： 
1. 
people: [7,0] 
插入到离开始位置偏移了0个距离的位置。 
result: [[7,0]] 
2. 
people: [7,1] 
插入到离开始位置偏移了1个距离的位置，即插入到[7,0]的后面。 
result: [[7,0], [7,1]] 
3. 
people: [6,1] 
插入到离开始位置偏移了1个距离的位置，即插入到[7,0]的后面。 
result: [[7,0], [6,1], [7,1]] 
4. 
people: [5,0] 
插入到离开始位置偏移了0个距离的位置，即插入到[7,0]的前面。 
result: [[5,0], [7,0], [6,1], [7,1]] 
5. 
people: [5,2] 
插入到离开始位置偏移了2个距离的位置，即插入到[7,0]的后面。 
result: [[5,0], [7,0], [5,2], [6,1], [7,1]] 
5. 
people: [4,4] 
插入到离开始位置偏移了4个距离的位置，即插入到[6,1]的后面。 
result: [[5,0], [7,0], [5,2], [6,1], [4,4], [7,1]]

java代码如下

```java
public class Solution {
    //注意这里用二维数组来表示键值对，即该数组有n行，2列，一定是两列，否则返回people
    public int[][] reconstructQueue(int[][] people) {
        if (people == null || people.length <= 1) {
            return people;
        }
        //将数组排序
        Arrays.sort(people, new Comparator<int[]>() {
            @Override
            public int compare(int[] o1, int[] o2) {
                //相等情况下比较第二个数的大小，第二个数小的大
                return o1[0] == o2[0] ? o1[1] - o2[1] : o1[0] - o2[0];
            }
        });
        int n = people.length;
        int[][] ret = new int[n][];
        //从已排序的第一个元素开始，
        for (int i = 0; i < n; i++) {
            for (int j = 0, ahead = 0; j < n; j++) {
                //ahead是偏移量
                if (ahead < people[i][1]) {
                    ahead += (ret[j] == null || ret[j][0] >= people[i][0]) ? 1 : 0;
                } else if (ret[j] == null) {
                    ret[j] = people[i];
                    break;
                }
            }
        }
        return ret;
    }
}
```
