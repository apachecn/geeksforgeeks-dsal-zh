# Python |检查给定字符串中是否存在子字符串

> 原文:[https://www . geesforgeks . org/python-check-substring-present-given-string/](https://www.geeksforgeeks.org/python-check-substring-present-given-string/)

给定两个字符串，检查 s2 中是否有 s1。

**示例:**

```
Input : s1 = geeks s2=geeks for geeks
Output : yes

Input : s1 = geek s2=geeks for geeks
Output : yes

```

我们可以迭代检查每个单词，但是 Python 为我们提供了一个内置函数 [find()](https://www.geeksforgeeks.org/python-string-methods-set-1-find-rfind-startwith-endwith-islower-isupper-lower-upper-swapcase-title/) ，它检查字符串中是否存在子字符串，这是在一行中完成的。
find()函数返回-1 如果没有找到，否则返回第一个出现的，所以使用这个函数这个问题可以解决。
**方法一:使用自定义函数。**

```
# function to check if small string is 
# there in big string
def check(string, sub_str):
    if (string.find(sub_str) == -1):
        print("NO")
    else:
        print("YES")

# driver code
string = "geeks for geeks"
sub_str ="geek"
check(string, sub_str)
```

**输出:**

```
YES          

```

**方法二:使用“count()”方法:-**

```
def check(s2, s1): 
    if (s2.count(s1)>0):     
        print("YES") 
    else: 
        print("NO") 

s2 = "A geek in need is a geek indeed"
s1 ="geek"
check(s2, s1) 
```

**输出:**

```
YES          

```

**方法 3:使用正则表达式**
正则表达式可以用来检查字符串是否包含指定的搜索模式。Python 有一个名为 **re** 的内置包，可以用来处理正则表达式。

```
# When you have imported the re module, you can start using regular expressions.
import re

# Take input from users
MyString1 =  "A geek in need is a geek indeed"
MyString2 ="geek"

# re.search() returns a Match object if there is a match anywhere in the string
if re.search( MyString2, MyString1 ):
    print("YES,string '{0}' is present in string '{1}' " .format(MyString2,MyString1))
else:
    print("NO,string '{0}' is not present in string {1} " .format(MyString2, MyString1) )
```

**输出:**

```
YES,string 'geek' is present in string 'A geek in need is a geek indeed' 
```