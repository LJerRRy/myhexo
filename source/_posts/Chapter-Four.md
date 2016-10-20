---
title: Chapter Two and One
date: 2016-09-28 12:11:05
tags: [sort,algorithm]
categories: 算法导论
---

算法导论（Introduction to Algorithm）

### 最短路径和旅行商问题

相似之处：都是寻求最短的路线
不同之处：最短路线问题是从若干条可选线路中选择一条线路使之在两个点之间达到交通路径最短，不需要经过所有的点；旅行商人问题中如果把仓库看做是图中的一个
点的话，首先要满足遍历所有的点，然后在所有满足的线路中选择最短的线路，其复杂程度要高于最短路径。

### 插入排序

插入算法的设计使用的是增量（incremental）方法：在排好子数组A[1..j-1]后，将元素A[j]插入，形成排好序的子数组A[1..j]。伪代码如下，伪代码中**数组是从1开始的**。

```
INSERTION-SORT(A)
1 for j = 2 to length[A]
2   key = A[j]
3   //Insert A[j] into the sorted sequence A[1..j-1]
4   i = j-1
5   while i > 0 and A[i] > key
6       A[i+1]=A[i]
7       i = i − 1
8   A[i+1]=key
```

插入排序的java算法如下

```java
public class InsertSort{
    public void inserSort(int[] a){
        int len = a.length;
        for(int j=1;j<len;j++){
            int key = a[j];
            int i = j-1;
            while(i>=0&&a[i]>key){
                a[i+1]=a[i];
                i--;
            }
            a[i+1]=key;
        }
    }
    public static void main(String[] args) {
        InsertSort is = new InsertSort();
        int num=100;
        int[] a = new int[num];
        for(int i=0;i<num;i++)
            a[i]= (int) (Math.random()*num);//Math.random()随机产生[0,1]的双精度浮点数
        is.inserSort(a);
        for(int i =0;i<num;i++)
            System.out.print(a[i]+" ");
    }
}
```

### 循环不变式

循环不变式(Loop Invariant)是证明算法正确性的一个重要工具。对于循环不变式，必须证明它的三个性质：<br>
**初始化(Initialization)**：它在循环的第一轮迭代开始之前，应该是正确的。 <br>
**保持(Maintenance)**：如果在循环的某一次迭代开始之前它是正确的，那么，在下一次迭代开始之前，它也是正确的。
**终止(Termination)**：当循环结束时，不变式给了我们一个有用的性质，它有助于表明算法是正确的。 <br>

运用循环不变式对插入排序算法的正确性进行证明：
**初始化**：j=2，子数组 A[1..j-1]只包含一个元素 A[1],显然它是已排序的。
**保持**： 若A[1..j-1]是已排序的， 则按照大小确定了插入元素 A[j]位置之后的数组A[1..j]显然也是已排序的。
**终止**：当 j=n+1 时，退出循环，此时已排序的数组是由 A[1],A[2],A[3]…A[n]组成的A[1..n]，此即原始数组 A。

### 分治法

**分治法（divide-and-conquer）**:有很多算法在结构上是递归的：为了解决一个给定的问题，算法要一次戒多次地递归调用其自身来解决相关的问题。这些算法通常采用分治策略：将原问题划分成 n 个规模较小而结构不原问题相似的子问题；递归地解决这些子问题，然后再合并其结果，就得到原问题的解。

分治模式在每一层递归上都有三个步骤：
**分解（Divide）**：将原问题分解成一系列子问题；
**解决（Conquer）**：递归地解各子问题。若子问题足够小，则直接求解；
**合并（Combine）**：将子问题的结果合并成原问题的解。

### 归并排序

归并排序是基于分治法。
**分解**：将 n 个元素分成各含 n/2 个元素的子序列；
**解决**：用合并排序法对两个子序列递归地排序；
**合并**：合并两个已排序的子序列以得到排序结果。
归并排序伪代码如下：

```
MERGE(A,p,q,r)
1 n1 = q − p + 1
2 n2 = r − q
3 create arrays L[1..n1 + 1] and R[1..n2 + 1]
4 for i = 1 to n1
5   L[i]=A[p+i-1]
6 for j=1 to n2
7   R[j]=A[q+j]
8 L[n1 + 1]= ∞
9 R[n2 + 1]= ∞
10 i = 1
11 j = 1
12 for k =p to r
13  if L[i]≤R[j]
14      A[k]=L[i]
15      i = i + 1
16  else A[k]=R[j]
17      j = j + 1
MERGE-SORT(A,p,r)
1 if p<r
2   q= (p+r)/2
3   MERGE-SORT(A,p,r)
4   MERGE-SORT(A,q+1,r)
5   MERGE-SORT(A,p,q,r)
```

java代码如下：

```java
public class Merge {
    //归并算法
    private void merge(int[] a,int p,int q,int r){
        int []m = new int[q-p+1];
        int []n = new int[r-q];
        for(int i=0,j=p;j<=q;i++,j++)
            m[i]=a[j];
        for(int i=0,j=q+1;j<=r;i++,j++)
            n[i]=a[j];
        int i=0,j=0,k=0;
        while(i<m.length&&j<n.length){
            if(m[i]>n[j])a[p++]=n[j++];
            else a[p++]=m[i++];
        }
        while(i<m.length)a[p++]=m[i++];
        while(j<n.length)a[p++]=n[j++];
    }
    //递归进行归并排序
    public void merge_sort(int[]a,int p,int r){
        if(p<r){
            int q=(p+r)/2;
            merge_sort(a,p,q);
            merge_sort(a,q+1,r);
            merge(a,p,q,r);
        }
    }

    public static void main(String[] args) {
        Merge merge = new Merge();
        int num=100;
        int[] a = new int[num];
        for(int i=0;i<num;i++)
            a[i]= (int) (Math.random()*num);//Math.random()随机产生[0,1]的双精度浮点数
        merge.merge_sort(a,0,num-1);
        for(int i =0;i<num;i++)
            System.out.print(a[i]+" ");
    }
}
```