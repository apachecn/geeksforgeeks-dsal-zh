# Python 中使用给定字符的可能单词

> 原文:[https://www . geesforgeks . org/可能-单词-使用给定字符-python/](https://www.geeksforgeeks.org/possible-words-using-given-characters-python/)

给定字典和字符数组，使用数组中的字符打印所有可能的有效单词。
**注意:**不允许重复字符。
示例:

```
Input : Dict = ["go","bat","me","eat","goal","boy", "run"]
        arr = ['e','o','b', 'a','m','g', 'l']
Output : go, me, goal. 

```

此问题已有解决方案，请参考[使用数组字符](https://www.geeksforgeeks.org/print-valid-words-possible-using-characters-array/)链接打印所有可能的有效单词。我们将使用[字典数据结构](https://www.youtube.com/watch?v=z7z_e5-l2yE&t=28s)在 python 中非常快速地解决这个问题。方法很简单:

1.  使用**集合**模块的[计数器(输入)](https://www.geeksforgeeks.org/counters-in-python-set-1/)方法，逐个遍历给定字符串列表，并将其转换为字典。
2.  检查任何字符串的所有键是否都在给定的字符集内，这意味着这个单词是可以创建的。

```
# Function to print words which can be created
# using given set of characters

def charCount(word):
    dict = {}
    for i in word:
        dict[i] = dict.get(i, 0) + 1
    return dict

def possible_words(lwords, charSet):
    for word in lwords:
        flag = 1
        chars = charCount(word)
        for key in chars:
            if key not in charSet:
                flag = 0
            else:
                if charSet.count(key) != chars[key]:
                    flag = 0
        if flag == 1:
            print(word)

if __name__ == "__main__":
    input = ['goo', 'bat', 'me', 'eat', 'goal', 'boy', 'run']
    charSet = ['e', 'o', 'b', 'a', 'm', 'g', 'l']
    possible_words(input, charSet)
```

输出:

```
go 
me
goal

```