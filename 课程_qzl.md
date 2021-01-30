# 基本数据结构

---

## bool逻辑

1. 被定义为'假'的常量：`None` And `False`。（`False`的底层是一个**类似宏定义**的常量，**一般作为数字处理**，`None`一般针对**返回空**或者对象的处理）
2. 任何数值类型的零：`0`,`0.0`,`0j`
3. 空的序列和多项集：`''`,`()`,`[]`,`range(0)`

---

## bool运算

和C语言相同，不再赘述。
主要运算：`or`, `and`, `not`（`or`和`and`属于一种**短路运算**）
注意这里的`not`和C语言中的`!`是一样的，但是`python`中没有`!`的用法

---

## 比较
|运算|含义|
|:-|:-|
|<|严格小于|
|<= |小于或等于|
|>|严格大于|
|>=|大于或等于|
|==|等于|
|!= |不等于|
|`is`|对象标识|
|`is not`|否定对象标识|
注意一下字符串比较大小的时候是按位依次比较，其实就是比较第一个不相等的元素，和字符串的长度无关。比如："aaaaaa" < "acss"。

---

# 分支语句
`Python`和其他语言一样可以使用`if/else/elif`关键字判断条件实现程序分支。

---

## 循环语句

### While语句

```python
numbers = [12,37,5,42,8,3]
even = []
odd = []
while len(numbers) > 0:
    number = numbers.pop() #取出List元素
    if(number % 2 == 0):
        even.append(number) #List中加入元素
    else:
        odd.append(number)
```
最后的结果：
$odd = [3,5,37]$  
$even = [ 8,42,12]$

---

### For语句
Python中的for语句非常灵活，可以遍历任何序列(包括列表，字符串，元组等)。

```python
for i in range(8):
    print(i) # 0,1,2,3,4,5,6,7          

for i in range(0,10,2):
    print(i) # 0,2,4,6,8

for i in range(1,4):
    print(i) # 1,2,3
```
关于直男表白的代码的迭代可以这样写：、
```python
for i in range(0,len(message),2):
    ......
```
**注意：**
range 不返回列表！返回的是一个迭代器
$type(range) = range$
如果需要用`range`得到一个列表，可以类型转换`a = list(range(0,6,2))`或者`a = [x for x in range(0,6,2)]`

---

### break,continue,else
`break`用于跳出循环，`continue`用于忽略当此循环剩下的语句直接进行下次循环。Python中也有`else`语句，在执行完整个循环后 会执行`else`的内容，如果`break`跳出，则不会执行。
```python
for n in range(2,10):
    for x in range(2,n):
        if n % x == 0:
            print(n,'equals',x,'*',n // x)
            break
    else: #如果上述循环终止，那就不会执行这个else语句
        print(n," is a prime number")
```

---

### Pass语句
`pass`什么都不做，但是如果按`Ctrl + c`会跳出循环或者程序，经常用来占位。先留着一个空的位置以后再实现具体作用。

---

## 函数
`Python`中用`def`来定义函数。
```python
def calc(a,b):
    c = a + b
    return c
```
如果不写函数的返回值，系统自动返回`None`

---

### 函数实现递归
```cpp
def Fibonaci(n):
    if n == 0 :
        return 0
    elif n == 1:
        return 1
    else:
        return Fibonaci(n - 1) + Fibonaci(n - 2)
```
但是注意递归的**空间时间消耗会很大**。

---

这是另外的一种写法：
```python
def fib_loop(n):
    a,b = 0,1
    while a < n:
        print(a,end = ' ')
        a,b = b,a + b 
    print()

n = (int)(input())
fib_loop(n)

```

---

## 参数默认值
`Python`中的函数**可以设定参数的默认值**，具有默认值的参数在函数调用时可以不传值。没有默认值的参数为函数的**必选参数**，拥有默认值的参数为函数的**可选参数**。
```python
def countdown(start,end = 0):
    while start > end:
        start -= 1
        print(start)

if __name__ == "__main__":
    # countdown()
    countdown(100)
    countdown(start =  5)
```

---

## 任意个数个参数
`Python`中在定义函数时，可以通过在参数前面加上`*`来表示任意个数的参数。

```python
def concat(*args,sep = ' '): #这里的sep是分隔符哦~
    print(type(args)) #元组
    return sep.join(args) #字符串拼接

print(concat('abc','def','123'))
```

---

## Lambda匿名函数
Python中可以使用lambda关键字来创建一个匿名函数，属于**语法糖**
```python
pairs = [(1,'one'),(2,'two'),(3,'thre'),(4,'four')]
pairs.sort(key = lambda p : p[0])
print(pairs)
```
同义写法：
```python
def cmd(p):
    return p[0]

pairs = [(1,'one'),(2,'two'),(3,'thre'),(4,'four')]
pairs.sort(key = cmd)
print(pairs)
```
# 数据结构进阶

---
## 列表进阶操作

列表的基本操作： **增加**，**更新**，**查找**和其他。

### 增加内容

|操作|返回值|
|:-|:-|
|`L *= n`|序列重放n次并存入原序列|
|`L.append(x)`|将x追加到序列尾部|
|`L.extend(t)`or `L += t`|将列表L后面追加t输出的所有项|
|`L.insert(i,x)`|在列表的索引处i插入元素x|

**注意：** 
- 这里一定要区分`L.append(x)`和`L.extend(t)`的区别,给出一个代码解释：
```python
L = [1,2,3]

L.append([4,5])

print(L) #L = [1,2,3,[4,5]]

L = [1,2,3]

L.extend([4,5])

print(L) #L = [1,2,3,4,5]s
```
注意这两个写法的输出,`append`相当于把其中的参数当作一个量对待，而不管其中的参数是`list`还是其他。

- 对于`inset()`函数，他的效率并不高。

- `extend(t)`中的对象不一定是`list`，可以是其他**可迭代**的对象

### 更新内容

|操作|返回值|
|:-|:-|
|`L[start:end] = t`|将`start:end`的部分替换成`t`|
|`L[start:end:step] = t`|按步长`step`替换`start : end`为`t`|
|`L.sort(key = None,reverse = False)`|对列表L进行排序，可以通过key来确定顺序的键值，默认升序|
|`L.reverse()`|反转列表中的元素的顺序|

**注意：** 
- 第一步操作中的替换，`t`的长度可以不为$end - start + 1$
- 第二步中的操作，`t`的长度需要和列表所取的元素数量一致。（取决于`step`的大小）
- `L.sort()` **不返回任何值！！** 修改的内容是列表本身，这和`append()`和`extend()`及`insert()`函数一致
- `t`仍然是可迭代对象。

### 查找内容

|操作|返回值|
|:-|:-|
|`x in L`|`True/False`|
|`x not in L`|`True/False`|
|`min(L)`|返回`L`中的**最小值**|
|`max(L)`|返回`L`中的**最大值**|
|`L.index(x[,start[,end]])`|返回`x`在`L`中**第一次出现的下标**，可查找指定范围为`[start,end)`|
|`L.count(x)`|返回`x`在`L`中出现的次数|

**Question:**
`index()`函数加入范围的用法？

### 其他操作

|操作|返回值|
|:-|:-|
|`L.copy()`或`L[:]`|返回一个和L完全相同的列表（**注意这里有返回值！**）|
|`L * n`|列表重复n次（**同样带有返回值**）|
|`L.pop(i)`|删除索引为`i`的元素并返回，无参时返回最后一个元素|
|`L.remove(x)`|删除第一个**值为x**的元素（**注意这里不是下标了！**）|
|`L.clear()`|**删除**列表的所有元素|
|`del L[start : end]`|删除对应部分的元素|
|`del L[start : end : step]`|删除相应部分，**有步长**|
|`del L`|删除列表（**是直接把L删除掉，恢复到未定义状态**）|


## 元组
---
### 元组概念

元组是一个不可变序列，同样可以用多种方式构建元组。
- 使用一对`()`来表示空元组：`a = (),`
- 使用一个后缀的逗号来表示单元组`a,`或`(a,)`
- 使用逗号分割多个项：`a,b,c`或`(a,b,c)`
- 使用内置的`tuple()`函数，接受一个**可迭代的对象**

### 元组操作

在上述的列表的操作中，元组**不能进行包括反转、删除部分元素在内的，会改变他本身的操作** ，其他的查找方法和切片是允许的。同时，元组支持`b = a[:]`但是不能写成`b = a.copy()`
**元组的删除只能是删除整个元组。**

可以看出，**列表和元组的操作有相同之处并且操作大概类似**，但是**元组可以支持`Hash()`函数**， 得到一个哈希值，但是列表不可以。
`a = hash(t)`
返回一个**整形哈希值。**
**注意： 可变序列不能作为字典key,不变序列可以**

### `Range`

`range`也属于不可变的序列，做大的作用就是用来进行`for`循环，好处是占用空间小。

**注意：和列表不同，它并不分配实际空间，而是生成一个可迭代的`range`对象**  

## 集合

---
集合中无序地保存不重复的元素，也就是集合中的元素是唯一的，经常用来**去重**

- `set()`用来创造空集合

### 集合的操作
|操作|返回值|
|:-|:-|
|`x in s`|x存在于集合s中|
|`x not in s`|x不存在于s中|
|`len(s)`|集合元素个数|
|`s.isdisjoint(t)`|s,t是否有交集，交集为空返回`True`|
|`union(*others)`或`set | others`|并集|
|`intersection(*others)`或`set & others`|交集|
|`difference(*others)`或`set - others`|差集|
|`symmetric_difference(*others)`或`set ^ others`|对称差集|
## 字典
---
本质上字典是一种映射。**一种可哈希的值映射到任意值**。
`Example :`
```python
a = {'one' : 1,'two' : 2,'three' : 3} #使用最多
b = dict(zip(['one','two','three'],[1,2,3]))
c = dict([('two',2),('one',1),('three',3)])
d = dict({'three' : 3,'two' : 2,'one' : 1})
```
**注意** 

- 第一种构建方式我们使用最多
- 第二种的`zip`操作是将两个**等长**的序列（**可以是元组也可以是列表**）合并成字典
- 也可以把列表转换成字典，但是要求**列表里的元素必须是元组**！ 

### 字典的操作

|操作|返回值|
|:-|:-|:-|:-|:-|:-|
|`len(d)`|**键值对**的数目|
|`d[key]`|获得键值`key`对应的值`value`|
|`d.get(key[,default])`|获得某个`key`的值，如果不存在返回`None`|
|`d.pop(key[,default])`|获取某个`key`的值并从字典中删除，如果不存在返回`None`|
|`d.popitem()`|默认返回**最后一对**进入字典的值（默认元组）|
|`d.keys()`|返回一个可迭代的对象，包含所有的`key`|
|`d.items()`|返回一个可迭代的对象`view`，包含所有的`(key,value)`|
|`d.values()`|返回一个可迭代的`view`，包括所有的`value`|
**注意:** 后三个操作基本和**循环**结合使用.

### 对于序列的进阶操作技巧
**E1:**
```python
student = [201900 + x for x in range(0,10)]

for index,value in enumerate(student) :
    print(index,value)
```
其中的`enumerate`函数是一个**枚举函数**
这里再解释一下`student`列表构建的方法,其实就是`lambda`函数的一种简写,可以让列表的构建更加简洁直接.
```python
student = list(map(lambda x : x + 201900,range(10)))
```
其实就是这个东西.

**E2:**
```python
import random

student = list(map(lambda x : x + 201900,range(10)))

for index,value in enumerate(student) :
    print(index,value)

scores = [random.randint(60,100) for x in range(10)]

for score , name in zip(scores,student):
    print(name,score)

```
这其中我们也可以同时循环两个序列,需要用`zip`函数连接

**E3:**
```python
checkin = [201900,201900,201901,201903]

unique_checkin = list(set(checkin))

all_student = list(map(lambda x : x + 201900,range(10)))

miss_student = set(all_student) - set(checkin) 

print(miss_student)
```
这就是集合的进阶用法，我们可以用来进行查重求差集.注意差集的写法!

**E4:** 
```python
import random

student = list(map(lambda x : x + 201900,range(10)))

scores = [random.randint(60,100) for x in range(10)]

transport = dict(zip(student,scores))

ranking = sorted(transport.items(),key = lambda x : x[1],reverse = True)

print(ranking)

print(type(ranking))

rank = dict(ranking)

print(rank)

print(type(rank))
```

**注意:** 第一个`ranking`属于列表类型,所以需要最后做一下转换,变成字典型的`rank`

# 输入输出

---
## 输入函数`input()`

函数原型：`input(promot)`

```python
name = input()

# name = input('Please input your name:') 带有交互

print(name)
```

## 输出函数`print`
```python
name = input()

age = input()

print(name,age)
```
使用输出函数可以**指定程序输出。**
```python
f = open('log.txt','w')

name = input()

age = input()

print(name,age,file = f,sep = '\n')

f.close()
```
这样程序的输出**不会显示在终端**

## 字符串格式化进阶

### `fstring`

`fstring`又称为格式化字符串字面值，特点是简单易用，在字符串的前面加一个`f`或者`F`即可。

```python
name = 'anjing'

age = 20

print(F'My teacher is {name},his age is {age}')
```
可以看到使用`fstring`后我们的的`name`和`age`的值就被自动算出来啦。
PS:如果不加这个`f`，你将会看到这样子的输出：
`My teacher is {name},his age is {age}`~~QAQ~~

### `format()`方法

字符串对象提供了`s.format()`方法来实现对输出内容的格式化。
```python
name = 'anjing'

age = 20

print(f'My teacher is {name},his age is {age}')

print('My teacher is {0},he is {1} years old'.format(name,age))

print('My teacher is {},he is {} years old'.format(name,age))

print('My teacher is {a},he is {b} years old'.format(a = name,b = age))
```
### 格式化迷你语言

详情请见：
[python 官方文档](https://docs.python.org/zh-cn/3/library/string.html#formatspec)