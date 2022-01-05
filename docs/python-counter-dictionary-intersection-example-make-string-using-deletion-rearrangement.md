# Python 计数器和字典交集示例(使用删除和重排制作字符串)

> 原文:[https://www . geesforgeks . org/python-counter-dictionary-交集-example-make-string-use-delete-重排/](https://www.geeksforgeeks.org/python-counter-dictionary-intersection-example-make-string-using-deletion-rearrangement/)

给定两个字符串，通过从第二个字符串中删除一些字符并重新排列剩余的字符，找出我们是否可以从第二个字符串中创建第一个字符串。

示例:

```
Input : s1 = ABHISHEKsinGH
      : s2 = gfhfBHkooIHnfndSHEKsiAnG
Output : Possible

Input : s1 = Hello
      : s2 = dnaKfhelddf
Output : Not Possible

Input : s1 = GeeksforGeeks
      : s2 = rteksfoGrdsskGeggehes
Output : Possible

```

对于这个问题我们已经有了解决方案，请参考[通过删除和重新排列字符](https://www.geeksforgeeks.org/make-string-another-deletion-rearrangement-characters/)链接从另一个字符串中创建一个字符串。我们将在 python 中快速解决这个问题。方法很简单，

1.  Use the [counter (iterative)](https://www.geeksforgeeks.org/counters-in-python-set-1/) method to convert two strings into dictionaries, each of which contains characters in the strings as keys and their frequencies as values.
2.  Now take the intersection of [and](https://www.geeksforgeeks.org/sets-in-python/) of the two dictionaries, and compare the result output with the dictionary of the first string. If the two dictionaries are equal, it means that **may** convert the string, otherwise, it is impossible.

```
# Python code to find if we can make first string
# from second by deleting some characters from 
# second and rearranging remaining characters.
from collections import Counter

def makeString(str1,str2):

    # convert both strings into dictionaries
    # output will be like str1="aabbcc", 
    # dict1={'a':2,'b':2,'c':2}
    # str2 = 'abbbcc', dict2={'a':1,'b':3,'c':2}
    dict1 = Counter(str1)
    dict2 = Counter(str2)

    # take intersection of two dictionries
    # output will be result = {'a':1,'b':2,'c':2}
    result = dict1 & dict2

    # compare resultant dictionary with first
    # dictionary comparison first compares keys
    # and then compares their corresponding values 
    return result == dict1

# Driver program
if __name__ == "__main__":
    str1 = 'ABHISHEKsinGH'
    str2 = 'gfhfBHkooIHnfndSHEKsiAnG'
    if (makeString(str1,str2)==True):
        print("Possible")
    else:
        print("Not Possible")
```

输出:

```
Possible

```