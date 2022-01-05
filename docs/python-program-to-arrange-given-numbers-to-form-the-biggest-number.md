# 排列给定数字形成最大数字的 Python 程序

> 原文:[https://www . geesforgeks . org/python-程序-排列-给定数字-形成最大数字/](https://www.geeksforgeeks.org/python-program-to-arrange-given-numbers-to-form-the-biggest-number/)

给定一组数字，以产生最大值的方式排列它们。例如，如果给定的数字是{54，546，548，60}，则排列 6054854654 给出最大值。如果给定的数字是{1，34，3，98，9，76，45，4}，那么排列 998764543431 给出最大值。

我们想到的一个**简单的解决方法**就是把所有的数字按照降序排序，但是单纯的排序是行不通的。例如，548 大于 60，但在输出中 60 在 548 之前。作为第二个例子，98 大于 9，但是在输出中 9 在 98 之前。

那我们该怎么做呢？想法是使用任何基于[比较的排序](https://www.geeksforgeeks.org/analysis-of-different-sorting-techniques/)算法。
在使用的排序算法中，不使用默认的比较，而是编写一个比较函数 **myCompare()** 并用它来排序数字。

给定两个数字 **X** 和 **Y** ，那么 **myCompare()** 应该如何决定先放哪个数字——我们比较两个数字 XY (Y 附加在 X 的末尾)和 YX (X 附加在 Y 的末尾)。如果 **XY** 比较大，那么输出中 X 应该在 Y 之前，否则 Y 应该在之前。例如，让 X 和 Y 分别为 542 和 60。为了比较 X 和 Y，我们比较了 54260 和 60542。因为 60542 大于 54260，所以我们把 Y 放在第一位。

下面是上述方法的实现。
为了保持代码简单，数字被视为字符串，使用向量代替普通数组。

下面是上述方法的实现:

## 蟒蛇 3

```
# Python3 Program to get the maximum
# possible integer from given array
# of integers...

# Custom comparator to sort according
# to the ab, ba as mentioned in description
def comparator(a, b):
    ab = str(a) + str(b)
    ba = str(b) + str(a)
    return ((int(ba) & gt
             int(ab)) -
            (int(ba) & lt
             int(ab)))

def myCompare(mycmp):

    # Convert a cmp= function into a 
    # key= function
    class K(object):
        def __init__(self, obj, *args):
            self.obj = obj

        def __lt__(self, other):
            return mycmp(self.obj, other.obj) & 
                   lt 0

        def __gt__(self, other):
            return mycmp(self.obj, other.obj) & 
                   gt 0

        def __eq__(self, other):
            return mycmp(self.obj, other.obj) == 0

        def __le__(self, other):
            return mycmp(self.obj, other.obj) & 
                   lt = 0

        def __ge__(self, other):
            return mycmp(self.obj, other.obj) & 
                   gt = 0

        def __ne__(self, other):
            return mycmp(self.obj, other.obj) != 0
    return K

# Driver code
if __name__ == "__main__":
    a = [54, 546, 548, 60]
    sorted_array = sorted(a, key = 
                   myCompare(comparator))
    number = "".join([str(i) for i in sorted_array])
    print(number)

# This code is Contributed by SaurabhTewary
```

**输出:**

```
6054854654
```

**时间复杂度:**O(nlogn)**排序**被认为运行时间复杂度为 O(nlogn)，for 循环在 O(n)时间内运行。
**辅助空间:** O(1)。

**另一种方法:**(使用[迭代工具](https://www.geeksforgeeks.org/itertools-combinations-module-python-print-possible-combinations/)

使用 Python 的内置库，itertools 库可以用来执行这个任务。

## 蟒蛇 3

```
# Python3 implementation this is to 
# use itertools. permutations as 
# coded below:

from itertools import permutations
def largest(l):
    lst = []
    for i in permutations(l, len(l)):

        # Provides all permutations of the 
        # list values, store them in list to 
        # find max
        lst.append("".join(map(str,i))) 
    return max(lst)

print(largest([54, 546, 548, 60])) 
# This code is contributed by Raman Monga
```

**输出:**

```
6054854654
```

**时间复杂度:**O(nlogn)
T3】辅助空间: O(1)。

更多详情请参考[整篇文章排列给定数字形成最大数字|集合 1](https://www.geeksforgeeks.org/given-an-array-of-numbers-arrange-the-numbers-to-form-the-biggest-number/) ！