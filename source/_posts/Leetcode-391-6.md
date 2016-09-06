---
title: Leetcode-6-391
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

n个轴对称矩形(其中n>0)，判断是否能围成一个矩形,不能有重叠且恰好围成一个矩形区域。每个矩形用左下顶点和右上顶点来表示，如矩形[1,1,2,3]，表示该矩形左下顶点坐标为（1,1），右下顶点坐标为（2,3）。

* **方法一**  顶点检查法，[参考地址](https://discuss.leetcode.com/topic/55923/o-n-solution-by-counting-corners-with-detailed-explaination/2)
* **方法二**  扫描线法，[参考地址](https://discuss.leetcode.com/topic/55944/o-n-log-n-sweep-line-solution)
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


```java
//定义一个扫描事件
public class Event implements Comparable<Event> {
	int time;
	int[] rect;

	public Event(int time, int[] rect) {
		this.time = time;
		this.rect = rect;
	}
	
	public int compareTo(Event that) {
		if (this.time != that.time) return this.time - that.time;
		else return this.rect[0] - that.rect[0];
	}
}

public boolean isRectangleCover(int[][] rectangles) {
	PriorityQueue<Event> pq = new PriorityQueue<Event> ();
        // border of y-intervals
	int[] border= {Integer.MAX_VALUE, Integer.MIN_VALUE};
	for (int[] rect : rectangles) {
		Event e1 = new Event(rect[0], rect);
		Event e2 = new Event(rect[2], rect);
		pq.add(e1);
		pq.add(e2);
		if (rect[1] < border[0]) border[0] = rect[1];
		if (rect[3] > border[1]) border[1] = rect[3];
	}
	TreeSet<int[]> set = new TreeSet<int[]> (new Comparator<int[]> () {
		@Override
                // if two y-intervals intersects, return 0
		public int compare (int[] rect1, int[] rect2) {
			if (rect1[3] <= rect2[1]) return -1;
			else if (rect2[3] <= rect1[1]) return 1;
			else return 0;
		}
	});
	int yRange = 0;
	while (!pq.isEmpty()) {
		int time = pq.peek().time;
		while (!pq.isEmpty() && pq.peek().time == time) {
			Event e = pq.poll();
			int[] rect = e.rect;
			if (time == rect[2]) {
				set.remove(rect);
				yRange -= rect[3] - rect[1];
			} else {
				if (!set.add(rect)) return false;
				yRange += rect[3] - rect[1];
			}
		}
                // check intervals' range
		if (!pq.isEmpty() && yRange != border[1] - border[0]) {
                        return false;
			//if (set.isEmpty()) return false;
			//if (yRange != border[1] - border[0]) return false;
		}
	}
	return true;
}
```

