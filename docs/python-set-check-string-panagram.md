# Python 设置检查字符串是否为 panagram

> 原文:[https://www . geesforgeks . org/python-set-check-string-pana gram/](https://www.geeksforgeeks.org/python-set-check-string-panagram/)

给定一个字符串，检查给定的字符串是否是 pangram。
示例:

```
Input : The quick brown fox jumps over the lazy dog
Output : The string is a pangram

Input : geeks for geeks
Output : The string is not pangram
```

一个正常的方法是使用频率表，检查是否所有元素都存在。但是使用**导入 ascii _ 小写作为 asc_lower** 我们导入集合中所有较低的字符和另一个集合中字符串的所有字符。在该函数中，形成了两组-一组用于所有小写字母，另一组用于字符串中的字母。这两个集合被相减，如果它是一个空集合，那么这个字符串就是一个 pangram。
下面是上述方法的 Python 实现:

## 计算机编程语言

```
# import from string all ascii_lowercase and asc_lower
from string import ascii_lowercase as asc_lower

# function to check if all elements are present or not
def check(s):
    return set(asc_lower) - set(s.lower()) == set([])

# driver code
string ="The quick brown fox jumps over the lazy dog"
if(check(string)== True):
    print("The string is a pangram")
else:
    print("The string isn't a pangram")
```

输出:

```
The string is a pangram
```