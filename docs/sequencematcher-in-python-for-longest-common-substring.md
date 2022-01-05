# Python 中最长公共子串的序列匹配器

> 原文:[https://www . geeksforgeeks . org/sequence matcher-in-python-for-long-common-substring/](https://www.geeksforgeeks.org/sequencematcher-in-python-for-longest-common-substring/)

给定两个字符串“X”和“Y”，打印最长的公共子字符串。

示例:

```
Input :  X = "GeeksforGeeks", 
         Y = "GeeksQuiz"
Output : Geeks

Input : X = "zxabcdezy", 
        Y = "yzabcdezx"
Output : abcdez

```

这个问题我们已经有解决方案了请参考[打印最长的常用子串](https://www.geeksforgeeks.org/print-longest-common-substring/)链接。我们将使用 SequenceMatcher . find _ long _ match()方法在 python 中解决这个问题。

### sequence matcher . find _ long _ match(aLow，aHigh，bLow，bHigh)方法是如何工作的？

首先我们用两个输入字符串 str1 和 str2 初始化 **SequenceMatcher** 对象，**find _ long _ match(aLow，aHigh，bLow，bHigh)** 取 4 个参数 aLow，bLow 分别是第一个和第二个字符串的起始索引，aHigh，bHigh 分别是第一个和第二个字符串的长度。find _ longest _ match()返回命名元组(I，j，k)，使得 a[i:i+k]等于 b[j:j+k]，如果没有块匹配，则返回(aLow，bLow，0)。

```
# Function to find Longest Common Sub-string

from difflib import SequenceMatcher

def longestSubstring(str1,str2):

     # initialize SequenceMatcher object with 
     # input string
     seqMatch = SequenceMatcher(None,str1,str2)

     # find match of longest sub-string
     # output will be like Match(a=0, b=0, size=5)
     match = seqMatch.find_longest_match(0, len(str1), 0, len(str2))

     # print longest substring
     if (match.size!=0):
          print (str1[match.a: match.a + match.size]) 
     else:
          print ('No longest common sub-string found')

# Driver program
if __name__ == "__main__":
    str1 = 'GeeksforGeeks'
    str2 = 'GeeksQuiz'
    longestSubstring(str1,str2)
```

输出:

```
Geeks

```