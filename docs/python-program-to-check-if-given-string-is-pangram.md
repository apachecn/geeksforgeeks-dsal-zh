# Python 程序检查给定字符串是否为 pangram

> 原文:[https://www . geesforgeks . org/python-程序检查给定字符串是否为-pangram/](https://www.geeksforgeeks.org/python-program-to-check-if-given-string-is-pangram/)

给定一个字符串，编写一个 Python 程序来检查该字符串是否是 Pangram。单词是包含英语字母表中每个字母的句子。

**示例:**

```
Input : The quick brown fox jumps over the lazy dog
Output : Yes

Input : abcdefgxyz
Output : No

```

我们已经在本文中讨论了 pangram 检查的幼稚方法。现在，让我们讨论一下 Pythonic 方法来实现同样的目的。

**方法# 1:**python 天真
这个方法使用一个循环来检查字符串的每个字符是否属于字母表集合。

```
# Python3 program to
# Check if the string is pangram
import string

def ispangram(str):
    alphabet = "abcdefghijklmnopqrstuvwxyz"
    for char in alphabet:
        if char not in str.lower():
            return False

    return True

# Driver code
string = 'the quick brown fox jumps over the lazy dog'
if(ispangram(string) == True):
    print("Yes")
else:
    print("No")
```

**Output:**

```
Yes

```

**方法 2 :** 使用 Python Set
将给定的字符串转换为 Set，然后检查字母集是否大于或等于它。如果字符串集大于或等于，则打印“是”，否则打印“否”。

```
# Python3 program to
# Check if the string is pangram
import string

alphabet = set(string.ascii_lowercase)

def ispangram(string):
    return set(string.lower()) >= alphabet

# Driver code
string = "The quick brown fox jumps over the lazy dog"
if(ispangram(string) == True):
    print("Yes")
else:
    print("No")
```

**Output:**

```
Yes

```

**方法#3 :** 集合方法的替代方法
这是另一种使用 Python 集合来查找字符串是否为 Pangram 的方法。我们制作一组小写字母和给定的字符串。如果从字母表中减去一组给定的字符串，我们就知道该字符串是否是 pangram。

```
# Python3 program to
# Check if the string is pangram
import string

alphabet = set(string.ascii_lowercase)

def ispangram(str):
     return not set(alphabet) - set(str)

# Driver code
string = 'the quick brown fox jumps over the lazy dog'
if(ispangram(string) == True):
    print("Yes")
else:
    print("No")
```

**Output:**

```
Yes

```

**方法#4 :** ASCII 方法
检查字符串的每个字符是否在小写字母的 ASCII 范围内，即 96 到 122。

```
# Python3 program to
# Check if the string is pangram
import itertools
import string

alphabet = set(string.ascii_lowercase)

def ispangram(str):
     return sum(1 for i in set(str) if 96 < ord(i) <= 122) == 26

# Driver code
string = 'the quick brown fox jumps over the lazy dog'
if(ispangram(string) == True):
    print("Yes")
else:
    print("No")
```

**Output:**

```
Yes

```