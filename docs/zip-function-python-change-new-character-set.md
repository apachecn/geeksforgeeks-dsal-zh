# Python 中的 Zip 函数，改为新的字符集

> 原文:[https://www . geesforgeks . org/zip-function-python-change-new-character-set/](https://www.geeksforgeeks.org/zip-function-python-change-new-character-set/)

给定一个 26 个字母的字符集，它相当于英语字母表的字符集(即 ABCD……。xyz)并充当关系。我们还会得到几个句子，我们必须在给定的新字符集的帮助下翻译它们。

示例:

```
New character set : qwertyuiopasdfghjklzxcvbnm
Input : "utta"
Output : geek

Input : "egrt"
Output : code

```

对于这个问题我们已经有了解决方案，请参考[将字符串更改为新的字符集](https://www.geeksforgeeks.org/change-string-to-a-new-character-set/)链接。我们将使用 [Zip()](https://www.geeksforgeeks.org/using-iterations-in-python-effectively/) 方法和[字典](https://www.youtube.com/watch?v=z7z_e5-l2yE&t=31s)数据结构在 python 中解决这个问题。方法很简单，

1.  Create a dictionary data structure, and we will map the original English character set to the new given character set. **zip (new charset, origcharset)** has done it for us. It maps each character sequence of the original character set to each given character of the new character set, and returns a list of tuple pairs. Now we use **dict ()** to convert it into a dictionary.
2.  Now traverse the original string and convert it into a new string.

```
# Function to change string to a new character

def newString(charSet,input):

    # map original character set of english
    # onto new character set given
    origCharSet = 'abcdefghijklmnopqrstuvwxyz'
    mapChars = dict(zip(charSet,origCharSet))

    # iterate through original string and get
    #  characters of original character set
    changeChars = [mapChars[chr] for chr in input] 

    # join characters without space to get new string
    print (''.join(changeChars))

# Driver program
if __name__ == "__main__":
    charSet = 'qwertyuiopasdfghjklzxcvbnm'
    input = 'utta'
    newString(charSet,input)
```

输出:

```
geek

```