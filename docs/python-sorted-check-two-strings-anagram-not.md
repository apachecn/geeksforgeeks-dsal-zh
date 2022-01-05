# Python 程序检查两个字符串是否是字谜

> 原文:[https://www . geesforgeks . org/python-sorted-check-two-strings-anagram-not/](https://www.geeksforgeeks.org/python-sorted-check-two-strings-anagram-not/)

**提问:**

给定两个字符串 s1 和 s2，检查这两个字符串是否是彼此的[字谜](https://www.geeksforgeeks.org/check-whether-two-strings-are-anagram-of-each-other/)。
例子:

```
Input : s1 = "listen"
        s2 = "silent"
Output : The strings are anagrams.

Input : s1 = "dad"
        s2 = "bad"
Output : The strings aren't anagrams.
```

### **解决方案:**

### **方法#1:使用排序()功能**

Python 提供了一个内置函数 [sorted()](https://www.geeksforgeeks.org/sorted-function-python/) ，该函数不修改原始字符串，而是返回排序后的字符串。
下面是上述方法的 Python 实现:

## 计算机编程语言

```
# function to check if two strings are
# anagram or not
def check(s1, s2):

    # the sorted strings are checked
    if(sorted(s1)== sorted(s2)):
        print("The strings are anagrams.")
    else:
        print("The strings aren't anagrams.")        

# driver code 
s1 ="listen"
s2 ="silent"
check(s1, s2)
```

**Output**

```
The strings are anagrams.
```

### 方法 2:使用 Counter()函数

*   使用计数器()计算第一个字符串和第二个字符串的所有频率
*   如果它们相等，则打印字谜

## 蟒蛇 3

```
# Python3 program for the above approach
from collections import Counter

# function to check if two strings are
# anagram or not
def check(s1, s2):

    # implementing counter function
    if(Counter(s1) == Counter(s2)):
        print("The strings are anagrams.")
    else:
        print("The strings aren't anagrams.")

# driver code
s1 = "listen"
s2 = "silent"
check(s1, s2)
```

**Output**

```
The strings are anagrams.
```

### **方法 3:使用 set()功能**

*   检查两个字符串的长度是否相同
*   验证两个字符串是否具有相同的元素
*   为了统一，请将元素转换为较低的()
*   也可以用于字符串中的整数

## 蟒蛇 3

```
'''\
Python3 program for implementation of checking string is anagram or not
using set function.
'''

def check(s1, s2):

    # Asserting length of string
    assert len(s1) == len(s2), 'The strings are not of same length'

    # Implementation of set function
    if set(s1.lower()) == set(s2.lower()):
      print("The strings are anagrams.")
    else:
      print("The strings aren't anagrams.")

    # one liner for above implementation
    # print('The strings are anagrams.') if set(s1.lower()) == set(s2.lower()) else print('The strings aren\'t anagrams.')

#Driver code
if __name__ == '__main__':
    word1, word2 = 'listen', 'silent'
    check(word1, word2)
```

**Output**

```
The strings are anagrams.
```