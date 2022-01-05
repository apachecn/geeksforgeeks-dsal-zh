# 根据 Python 中输入字符串中出现的字符生成两个输出字符串

> 原文:[https://www . geeksforgeeks . org/generate-two-output-strings-only-on-occurrence-character-input-string-python/](https://www.geeksforgeeks.org/generate-two-output-strings-depending-upon-occurrence-character-input-string-python/)

给定一个输入字符串 str[]，生成两个输出字符串。其中一个由在输入字符串中只出现一次的字符组成，第二个由多次出现的字符组成。输出字符串必须排序。

示例:

```
Input : str = "geeksforgeeks"
Output : String with characters occurring once:
"for".
String with characters occurring multiple times:
"egks"

Input : str = "geekspractice"
Output : String with characters occurring once:
"agikprst"
String with characters occurring multiple times:
"ce"

```

对于这个问题我们已经有了解决方案，请参考[根据输入字符串](https://www.geeksforgeeks.org/generate-two-output-strings-depending-upon-occurrence-character-input-string/)链接中出现的字符生成两个输出字符串。我们可以使用[计数器(可迭代)](https://www.geeksforgeeks.org/counters-in-python-set-1/)方法在 python 中快速解决这个问题。方法很简单，

1.  使用**计数器()**方法将字符串转换为以字符为键、以频率为值的字典。
2.  现在分离出频率为 1 和频率大于 1 的字符列表。
3.  对两个列表中的字符进行排序以获得输出字符串。

```
# Function Generate two output strings depending upon 
# occurrence of character in input string

from collections import Counter

def generateStrings(input):

     # convert string into dictionary
     # having characters as keys and frequency as value
     freqDict = Counter(input)

     # separate out characters having frequency 1 and more than 1
     freq1 = [ key for (key,count) in freqDict.items() if count==1]
     freqMore1 = [ key for (key,count) in freqDict.items() if count>1]

     # sort lists and concatenate characters
     # with out space to print resultant strings
     freq1.sort()
     freqMore1.sort()

     # print output strings
     print ('String with characters occurring once:')
     print (''.join(freq1))
     print ('String with characters occurring multiple times:')
     print (''.join(freqMore1))

# Driver program
if __name__ == "__main__":
    input = "geeksforgeeks"
    generateStrings(input)
```

输出:

```
String with characters occurring once:
for
String with characters occurring multiple times:
egks

```