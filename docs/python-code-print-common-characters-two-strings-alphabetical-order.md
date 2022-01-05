# Python 代码按字母顺序打印两个字符串的常用字符

> 原文:[https://www . geesforgeks . org/python-code-print-common-characters-two-strings-字母顺序/](https://www.geeksforgeeks.org/python-code-print-common-characters-two-strings-alphabetical-order/)

给定两个字符串，按字典顺序打印所有常用字符。如果没有常用字母，打印-1。所有字母都是小写的。

示例:

```
Input : 
string1 : geeks
string2 : forgeeks
Output : eegks
Explanation: The letters that are common between 
the two strings are e(2 times), k(1 time) and 
s(1 time).
Hence the lexicographical output is "eegks"

Input : 
string1 : hhhhhello
string2 : gfghhmh
Output : hhh

```

此问题已有解决方案请参考[按字母顺序打印两个字符串的常用字符](https://www.geeksforgeeks.org/print-common-characters-two-strings-alphabetical-order-2/)链接。我们将使用[交集](https://www.geeksforgeeks.org/sets-in-python/)属性和[集合在 python 中解决这个问题。计数器()](https://www.geeksforgeeks.org/counters-in-python-set-1/)模块。方法很简单，

1.  使用**计数器(str)** 方法将两个字符串转换为字典数据类型，该方法将字符串的字符作为键，将它们的频率作为值。
2.  现在使用**交集(a & b )** 属性找到两个字符串之间的公共元素。
3.  结果也将是一个计数器字典，以公共元素作为键，以它们的公共频率作为值。
4.  使用计数器字典的**元素()**方法，通过键的频率次数来扩展键列表。
5.  对列表进行排序，并连接输出列表中的每个字符，没有空格来打印结果字符串。

```
# Function to print common characters of two Strings 
# in alphabetical order 
from collections import Counter 

def common(str1,str2): 

    # convert both strings into counter dictionary 
    dict1 = Counter(str1) 
    dict2 = Counter(str2) 

    # take intersection of these dictionaries 
    commonDict = dict1 & dict2 

    if len(commonDict) == 0: 
        print (-1)
        return

    # get a list of common elements 
    commonChars = list(commonDict.elements()) 

    # sort list in ascending order to print resultant 
    # string on alphabetical order 
    commonChars = sorted(commonChars) 

    # join characters without space to produce 
    # resultant string 
    print (''.join(commonChars)) 

# Driver program 
if __name__ == "__main__": 
    str1 = 'geeks'
    str2 = 'forgeeks'
    common(str1, str2) 
```

输出:

```
eegks

```