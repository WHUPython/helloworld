# Unit Test

在Python进阶之路上，有必要了解Python是如何进行代码测试。测试驱动开发是现代软件开发的方法之一，受到很多人的追捧。[参考阅读：TDD（测试驱动开发）是否已死？](<https://www.zhihu.com/question/37623307>)

由于不涉及非常复杂的代码，所有只需要了解最为常见的**单元测试**即可。

---

假设我们写了一个函数

```python
def bin_search(lst, target):
    i, j = 0, len(lst)-1
    while i <= j:
        mid = (i + j)//2
        if target == lst[mid]:
            return mid
        elif target < lst[mid]:
            j = mid - 1
        else:
            i = mid + 1
    return -1
```

这个函数如果是正确的话，那么会返回列表（数组）中target元素的下标值；如果列表不存在这个元素就返回-1。

---

如何测试这段代码呢？

我们可以写出下面的单元测试代码？

```python
import unittest
class TestBinarySearch(unittest.TestCase):

    def test_common(self):
        self.assertEqual(bin_search([0, 1, 2, 3], 1), 1)
        self.assertEqual(bin_search([0, 1, 5, 10], 0), 0)
        self.assertEqual(bin_search([0, 1, 5, 10], 8), -1)

if __name__ == '__main__':
    unittest.main() # 启动测试
```

Python的提供了单元测试类`unittest`。想要进行进行单元测试，我们需要从类`unittest.TestCase`派生出子类，然后在子类中定义以`test`开头的方法(`method`)，再在方法里完成各种测试。每一个测试，都可以视为对被测试对象的一个要求。`self.assertEqual(a, b)`是断言 `a b` 要相等。 

---

Python提供了很多断言方法

| Method                                                       | Checks that            | New in |
| ------------------------------------------------------------ | ---------------------- | ------ |
| [`assertEqual(a, b)`](https://docs.python.org/3.7/library/unittest.html#unittest.TestCase.assertEqual) | `a == b`               |        |
| [`assertNotEqual(a, b)`](https://docs.python.org/3.7/library/unittest.html#unittest.TestCase.assertNotEqual) | `a != b`               |        |
| [`assertTrue(x)`](https://docs.python.org/3.7/library/unittest.html#unittest.TestCase.assertTrue) | `bool(x) is True`      |        |
| [`assertFalse(x)`](https://docs.python.org/3.7/library/unittest.html#unittest.TestCase.assertFalse) | `bool(x) is False`     |        |
| [`assertIs(a, b)`](https://docs.python.org/3.7/library/unittest.html#unittest.TestCase.assertIs) | `a is b`               | 3.1    |
| [`assertIsNot(a, b)`](https://docs.python.org/3.7/library/unittest.html#unittest.TestCase.assertIsNot) | `a is not b`           | 3.1    |
| [`assertIsNone(x)`](https://docs.python.org/3.7/library/unittest.html#unittest.TestCase.assertIsNone) | `x is None`            | 3.1    |
| [`assertIsNotNone(x)`](https://docs.python.org/3.7/library/unittest.html#unittest.TestCase.assertIsNotNone) | `x is not None`        | 3.1    |
| [`assertIn(a, b)`](https://docs.python.org/3.7/library/unittest.html#unittest.TestCase.assertIn) | `a in b`               | 3.1    |
| [`assertNotIn(a, b)`](https://docs.python.org/3.7/library/unittest.html#unittest.TestCase.assertNotIn) | `a not in b`           | 3.1    |
| [`assertIsInstance(a, b)`](https://docs.python.org/3.7/library/unittest.html#unittest.TestCase.assertIsInstance) | `isinstance(a, b)`     | 3.2    |
| [`assertNotIsInstance(a, b)`](https://docs.python.org/3.7/library/unittest.html#unittest.TestCase.assertNotIsInstance) | `not isinstance(a, b)` | 3.2    |

通过这些断言方法，我们可以完成对待测试函数的测试。