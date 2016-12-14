

## List

1. 问题

```python
sampleList = [1,2,3,4,5,6,7,8]
#sampleList.insert(2,1)
#print(sampleList.count(1))
for a in sampleList:
    print (a)
    if a == 4:
        sampleList.reverse()
        print(sampleList)
```
上面代码输出结果如下

```python
1
2
3
4
[8, 7, 6, 5, 4, 3, 2, 1]
4
[1, 2, 3, 4, 5, 6, 7, 8]
6
7
8
```

可以发现for循环一个list表时，它本质上还是有个i变量，从0开始一直加到最开始的list表的长度(这个长度每次会重新获取一次），如下例子中，如果每次循环都向list中添加元素，那么应该一直遍历下去，但结果并不是

```python
sampleList = [1,2,3,4,5,6,7,8]
#sampleList.insert(2,1)
#print(sampleList.count(1))
for a in sampleList:
    print (a)
    if a==1:
        sampleList.append(12)

for a in range(0,len(sampleList)):
    print (a)
    if a==1:
        sampleList.append(12)
```

python2.x 中,range返回的是一个列表
python3.x中,range返回的是一个迭代值
类似for n in range(1,10):之类的可以照常使用
如果要在3.x中产生1-10的列表,可以list(range(1,10))

2. list的方法
.append(value) - appends element to end of the list
.count('x') - counts the number of occurrences of 'x' in the list
.index('x') - returns the index of 'x' in the list  若不含有x则报错
.insert('y','x') - inserts 'x' at location 'y' 
.pop() - returns last element then removes it from the list
.remove('x') - finds and removes first 'x' from list 无返回值
.reverse() - reverses the elements in the list
.sort() - sorts the list alphabetically in ascending order, or numerical in ascending order