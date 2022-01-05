# Python 中前缀和数组使用累加函数

> 原文:[https://www . geesforgeks . org/prefix-sum-array-python-using-aggregate-function/](https://www.geeksforgeeks.org/prefix-sum-array-python-using-accumulate-function/)

给我们一个数组，求给定数组的[前缀和](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)。

示例:

```
Input : arr = [1, 2, 3]
Output : sum = [1, 3, 6]

Input : arr = [4, 6, 12]
Output : sum = [4, 10, 22]

```

**前缀和**是给定序列的部分和的序列。例如，序列{a，b，c，…}的累计和是 a，a+b，a+b+c，以此类推。我们可以使用**累加(可迭代)**方法在 python 中快速解决这个问题。

```
# function to find cumulative sum of array
from itertools import accumulate

def cumulativeSum(input):
      print ("Sum :", list(accumulate(input)))

# Driver program
if __name__ == "__main__":
    input = [4, 6, 12]
    cumulativeSum(input)
```

输出:

```
Sum = [4, 10, 22]

```