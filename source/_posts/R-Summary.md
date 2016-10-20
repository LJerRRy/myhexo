---
title: R Learnning
date: 2016-10-20 22:48:19
tags: R
categories: 学习笔记
---

## R语言学习

Everything in R is an **object**; Every object in R has a **class**;
一切皆对象，每个对象都有类；

### R基本语法

R语言也支持**table键**自动补全

#### 获取help

1. `> help.start() `开启帮助文档
2. `>help(solve)` 显示某命令的帮助信息，或者 ` >?solve`
3. 对于由特殊字符指定的功能，这些参数必须用单引号或双引号括起来，使之成为一个“字符串”,如`> help("[[")`
4. 与某个主题相关的例子通常可以用下面的命令得到
`> example(topic)`

#### 命令简介

1. R对大小写是敏感的；名称不能以数字开始；
2. 基本的命令由表达式或者赋值语句组成。如果一个表达式被作为一条命令给出，它将被求值、打印而表达式的值并不被保存。一个赋值语句同样对表达式求值之后把表达式的值传给一个变量，不过并不会自动的被打印出来；
3. 命令由分号(;)来分隔，或者另起新行；
4. 基本命令可以由花括号(f和g)合并为一组复合表达式；
5. 注释几乎可以被放在任何地方，只要是以井号( # )开始，到行末结束；
6. 如果一个命令在行末仍没有结束，R将会给出一个不同的提示符，默认的是‘+’。

#### 基本数据结构

"numeric" is a class corresponding to numeric vectors. The other vector basic classes are "logical", "integer", "complex", "character", "raw", "list" and "expression".

```R
#1. 逻辑 TRUE,FALSE 只能大写，false，true等都不是
v <- TRUE
print(class(v))
#输出
#[1] "logical" 

#2. 数字  12.3,5,999
v <- 23.5
print(class(v))
#输出
#[1] "numeric" 

#3. 整数  2L, 34L, 0L 
v <- 2L 
print(class(v))
#输出
#[1] "integer" 

#4. 复数  3 + 2i 
v <- 3 + 2i 
print(class(v))
#输出
#[1] "complex"

#5.字符 'a' , '"good", "TRUE", '23.4' 
v <- "Hello"
print(class(v))
#输出
#[1] "character"

#6.原始  "Hello" 将被存储为 48 65 6c 6c 6f 
v <- charToRaw("Hello")
print(class(v))
#输出
#[1] "raw"

```

因此，在R语言中的非常基本的数据类型是R-对象，如上图所示占据着不同类别的元素向量。请注意R语言中类的数量并不只限于上述的六种类型。 例如，我们可以使用许多原子向量以及创建一个数组，它的类将成为数组。 

#### 对象


1. 向量vector
当希望使用多个元素创建向量，应该使用`c()`函数，这意味着元素结合成一个向量。

```R
apple <- c('red','green',"yellow")
print(apple)
print(class(apple))
#输出
#[1] "red" "green"  "yellow"
#[1] "character"
```

2. 列表list
列表是R-对象，它里面可以包含多个不同类型的元素，如向量，函数，甚至是另一个列表。

```R
list1 <- list(c(2,5,3),21.3,sin)
print(list1)
#输出
#[[1]]
#[1] 2 5 3
#
#[[2]]
#[1] 21.3
#
#[[3]]
#function (x)  .Primitive("sin")
```

3. 矩阵
矩阵是一个二维矩形数据集。它可以使用一个向量输入到矩阵函数来创建。 

```R
M = matrix( c('a','a','b','c','b','a'), nrow=2,ncol=3,byrow = TRUE)
print(M)
#输出
#     [,1] [,2] [,3]
#[1,] "a"  "a"  "b" 
#[2,] "c"  "b"  "a"  
```

4. 数组
尽管矩阵限于两个维度，数组可以是任何数目的尺寸大小。数组函数使用它创建维度的所需数量的属性-dim。在下面的例子中，我们创建了两个元素数组，这是3×3矩阵。

```R
a <- array(c('green','yellow'),dim=c(3,3,2))
print(a)
```

5. 因子
因子是使用向量创建的R对象。它存储随同该向量作为标记元素的不同值的向量。 标签始终是字符，而不论它在输入向量的是数字或字符或布尔等。它们在统计建模有用。 
运用` factor()` 函数创建因子。nlevels 函数给出级别的计数。 

```R
# Create a vector.
apple_colors <- c('green','green','yellow','red','red','red','green')

# Create a factor object.
factor_apple <- factor(apple_colors)

# Print the factor.
print(factor_apple)
print(nlevels(factor_apple))
```

6. 数据帧
数据帧是表格数据对象。不像在数据帧的矩阵，每一列可以包含不同的数据的模型。第一列可以是数字，而第二列可能是字符和第三列可以是逻辑。它与向量列表的长度相等。 
数据帧所使用 `data.frame()`函数来创建。 

```R
# Create the data frame.
BMI <- 	data.frame(
			gender = c("Male", "Male","Female"), 
			height = c(152, 171.5, 165), 
			weight = c(81,93, 78),
			Age =c(42,38,26)
			)
print(BMI)
```

#### R语言变量与运算符

1. 变量命名规范
变量名由有字母，数字，**点**和下划线组成，数字不能开头，且若点开头，点`.`后不能跟一个数字

<p style="color:red;">.2invalid  2invalid  (非法命名)</p>

<p style="color:blue;">.v2alid  valid  (合法命名)</p>


2. 变量赋值

变量可以使用**向左(<-)**，**向右(->)**或者**等于**操作符来分配值。可以使用 print() 或 cat() 函数打印变量的值。cat() 函数将多个项目并成连续并打印输出。 

```R
#c()函数用来新建一个向量
# Assignment using equal operator.
var.1 = c(0,1,2,3)           

# Assignment using leftward operator.
var.2 <- c("learn","R")   

# Assignment using rightward operator.   
c(TRUE,1) -> var.3           

print(var.1)
cat ("var.1 is ", var.1 ,"\n")
cat ("var.2 is ", var.2 ,"\n")
cat ("var.3 is ", var.3 ,"\n")
#注意矢量c（TRUE，1）有逻辑和数值类的混合。因此，逻辑类强迫转换到数字类，如TRUE为1
```

3. 变量的数据类型 

在R，变量本身不需要声明成任何数据类型，但它得到分配给它的是 R-对象的数据类型。所以R被称为**动态类型的语言**，这意味着我们可以当在程序中使用它，并可再次并**改变相同变量的变量的数据类型**。
`class()`函数用来查询参数的数据类型

4. 查找变量

要知道目前在工作区中的可用变量，可以使用 `ls()`函数列出所有变量。另外，`ls()` 函数可以使用模式来匹配变量名称。 
在 ls() 函数可以使用模式匹配变量名。`print(ls(pattern="var"))`列出参数中包含var的参数名称。
以点(.) 开始的变量是隐藏的，它们可以使用 “all.names= TRUE” 参数给 `ls()`函数来列出。即`ls(all.name=TRUE)`

5. 删除变量

变量可以通过使用`rm()`函数来删除。下面我们删除变量`var.3`。然后再打印变量时出现异常错误。

```R
rm(var.3)
print(var.3)
```

当上面的代码执行时，它产生以下结果： 

```
[1] "var.3"
Error in print(var.3) : object 'var.3' not found
```
所有的变量可以通过使用`rm()`和 `ls()`函数来一起删除。 

```R
rm(list=ls())
print(ls())
```

6. 算术运算符

```R
#加法减法  两个向量相加、相减，下面给出加法的例子和结果 
v <- c( 2,5.5,6)
t <- c(8, 3, 4)
print(v+t)
#[1] 10.0  8.5  10.0

#乘法除法  两个向量乘、除，
v <- c( 2,5.5,6)
t <- c(8, 3, 4)
print(v/t)
#[1] 0.250000 1.833333 1.500000

#取余%% 得到第一矢量与第二个矢量余数 
v <- c( 2,5.5,6)
t <- c(8, 3, 4)
print(v%%t)
#[1] 2.0 2.5 2.0

#%/% 第一个向量与第二（商）相除的结果 ，保留整数（即整除）
v <- c( 2,5.5,6)
t <- c(8, 3, 4)
print(v%/%t)
#[1] 0 1 1

#^ 第一向量提升到第二向量的指数 
v <- c( 2,5.5,6)
t <- c(8, 3, 4)
print(v^t)
#[1]  256.000  166.375 1296.000
```

7. 关系运算符、逻辑运算符和其他运算符

1. 关系运算符`>,<,>=,<=,==,!=`
2. 逻辑运算符`& | !`第一向量的每个元素与所述第二向量的相应元素进行比较。比较的结果是一个布尔值。 
所有数值大于1则认为逻辑值为TRUE。**复数的逻辑值为TRUE**
逻辑运算符`&&`和`||`考虑矢量仅第一元素并给单个元素作为输出的向量。
3. 其他运算符

`:`冒号运算符。它创建顺序一系列数字的向量 

```R
v <- 2:8
print(v) 
#[1] 2 3 4 5 6 7 8 
```


`%in%` 这个操作符用于识别一个元素是否属于（在）一个向量。

```R
v1 <- 8
v2 <- 12
t <- 1:10
print(v1 %in% t) 
print(v2 %in% t) 
#[1] TRUE
#[1] FALSE 
``` 

`%*% `这个操作符是用来乘以它的转置矩阵。 

```R
#t()函数矩阵转置
M = matrix( c(2,6,5,1,10,4), nrow=2,ncol=3,byrow = TRUE)
t = M %*% t(M)
print(t) 
```


