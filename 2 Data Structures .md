# Data Structure

* 高效地组织数据
* 创建二维数组

## 数据组织

铭记“程序模型是客观世界的”会对某个具体的客观事物选择合适的表示方式大有裨益。这想想或许是非常直接的，但实际上却需要大量的考量才能达到目的。

刚开始的时候，你也许会为应用选择合适的模型绞尽脑汁，但这个过程会帮助你成为一个更好的程序猿。当然，你也可以遵从前人指导，但我不推荐这样。解决编程难题是必经之路。在你编程做决定的时候，会对你的程序有一个更加全面的理解。

在你的Python之路上，你会适应日益复杂的数据结构。目前，我们创建的结构有`list`和`dict`，他们都是不可改变的(immutable)，不可改变的还有数字(numbers)和字符串(strings)。当然，你也可以在你自己的数据结构中使用list, tuples, dicts或其他复杂数据结构。

在对象中数据结构也是相当重要的。通过一个`class`语句定义一类对象的行为。class语句定义了类实例的行为--`method` ，用户可以调用它们来产生某种行为。Each instance has its own namespace though, which makes it appear like a data structure with behaviors common to all members of its class.    

### Handling Multi-Dimensional Arrays in Python    

Python中，我们一般通过从创建类来执行任务。索引(indexing)是利用`__getitem__`方法完成的。

__整数(integer)和切片`int slice`__是可以用做下标索引的**唯二**类型(type)。一般不直接和slice对象进行接触，而是通过冒号分割的多下标方式进行访问(for which 冒号也被称为切片符号)。

```python
>>> class GI:
... def __getitem__(self, *args, **kw):
    ... print("Args:", args)
    ... print("Kws: ", kw)
...
>>> gi = GI()
>>> gi[0]
Args: (0,)
Kws: {}
>>> gi[0:1]
Args: (slice(0, 1, None),)
Kws: {}
>>> gi[0:10:-2]
Args: (slice(0, 10, -2),)
Kws: {}
>>> gi[1, 2, 3]
Args: ((1, 2, 3),)
Kws: {}
>>> gi[1:2:3, 4:5:6]
Args: ((slice(1, 2, 3), slice(4, 5, 6)),)
Kws: {}
>>> gi[1, 2:3, 4:5:6]
Args: ((1, slice(2, 3, None), slice(4, 5, 6)),)
Kws: {}
>>> gi[(1, 2:3, 4:5:6)]
File "<console>", line 1
gi[(1, 2:3, 4:5:6)]
^
SyntaxError: invalid syntax
>>> (1, 2:3, 4:5:6)
File "<console>", line 1
(1, 2:3, 4:5:6)
^
SyntaxError: invalid syntax
>>>
```

切片只能是下标表达式(subscripting expressions)参数元组（tuple）的最上层元素（即元组的元素），对元组加引号或者在下标表达式的括号外面使用类似的元组都会报错。

解释器把 整数直接传递给`__getitem__()`，但是对由冒号分割的整数，会先创建一个切片对象（slice object），再把切片对象传递给`__getitem__()`方法。上面的代码展示了可以用多个切片对象作为下标，`__getitem__()`方法会收到一个切片对象的元组。

小结一下，上面的要点如下

```python
obj[M] == obj.__getitem__(M)
当M为整数或者切片时，上面等式都成立。
```

```python
obj[M:N] == obj.__getitem__(slice(M, N, None)) 
and
obj[M:N:S] == obj.__getitem__(slice(M, N, S))
```

方括号下标访问都会被代理到`__getitem__`、 `__setitem__`方法上去，这就给了我们很大的想象空间：我们可以在类的这两个方法上恣意妄为。

```python
class array:
    def __init__(self, M, N):
        self._data = [0] * M * N
        self._rows = M
        self._cols = N
    def __getitem__(self, key):
        """retrieve elements from self._data"""
        pass
   	def __setitem__(self, key, value):
        """Set value to place key in self._data"""
        pass
   	def __delitem__(self, key):
        """Amos: delete an item from self._data"""
```



# 课后练习Quiz

## Data Structures - Quiz 1

Which data types can be used to index a sequence?

int and slice

**Grading Criteria:** Student should show a more sophisticated understanding of indexing.

What is the best-known third-party package for numerical programming in Python?

Numpy.

**Grading Criteria:** Student shows developing awareness of the Python ecosystem and its third-party libraries, especially where intensive numeric computing is concerned.

Which method of o is called when evaluating o[i] (o and i should be part of the answer)?

__getitem__()

**Grading Criteria:** Student should show increased understanding of how syntax triggers special named methods.