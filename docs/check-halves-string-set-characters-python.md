# 检查字符串的两半在 Python 中是否有相同的字符集

> 原文:[https://www . geesforgeks . org/check-hales-string-set-characters-python/](https://www.geeksforgeeks.org/check-halves-string-set-characters-python/)

给定一个只有小写字符的字符串，任务是检查是否有可能从中间分割一个字符串，这将给出具有相同字符和每个字符相同频率的两半。如果给定字符串的长度为奇数，则忽略中间元素并检查其余部分。

示例:

```
Input : abbaab
Output : NO
The two halves contain the same characters
but their frequencies do not match so they
are NOT CORRECT

Input : abccab
Output : YES

```

此问题已有解决方案，请参考[检查字符串的两半是否有相同的字符集](https://www.geeksforgeeks.org/check-half-string-character-frequency-character/)链接。我们将使用 **[字典](https://www.youtube.com/watch?v=z7z_e5-l2yE&t=29s)** 比较来快速解决 Python 中的这个问题。

方法很简单:

1.  将字符串分成两部分，使用[计数器(迭代器)](https://www.geeksforgeeks.org/counters-in-python-set-1/)方法将两部分转换成字典，每个字典包含其字符作为键，频率作为值。
2.  现在比较一下这两本词典。在 python 中，我们可以使用 **==** 运算符来比较两个，它首先检查两个字典的键是否相同，然后检查每个键的值。如果一切都相等，那就意味着两本词典是一样的。

```
# Function to Check if both halves of 
# the string have same set of characters 
from collections import Counter 

def checkTwoHalves(input): 

    length = len(input) 

    # Break input string in two parts 
    if (length % 2 != 0): 
        first = input[0:length // 2] 
        second = input[(length // 2) + 1:] 
    else: 
        first = input[0:length // 2] 
        second = input[length // 2:] 

    # Convert both halves into dictionary and compare 
    if Counter(first) == Counter(second): 
        print ('YES')
    else: 
        print ('NO')

# Driver program 
if __name__ == "__main__": 
    input = 'abbaab'
    checkTwoHalves(input) 
```

**输出:**

```
NO

```