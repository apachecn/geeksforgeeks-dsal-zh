# 在 Python Pangram 检查中使用 Set()

> 原文:[https://www . geesforgeks . org/using-set-python-pang ram-checking/](https://www.geeksforgeeks.org/using-set-python-pangram-checking/)

给定一个字符串，检查它是否是 Pangram。单词是包含英语字母表中每个字母的句子。小写和大写被认为是相同的。

示例:

```
Input : str = 'The quick brown fox jumps over 
               the lazy dog'
Output : Yes
// Contains all the characters from ‘a’ to ‘z’

Input : str='The quick brown fox jumps over the dog'
Output : No
// Doesn’t contains all the characters from ‘a’
// to ‘z’, as ‘l’, ‘z’, ‘y’ are missing

```

此问题已有解决方案请参考[盘查](https://www.geeksforgeeks.org/pangram-checking/)链接。我们将使用 [Set()](https://www.geeksforgeeks.org/sets-in-python/) 数据结构和 [List()理解](https://www.geeksforgeeks.org/python-list-comprehension-and-slicing/)在 Python 中解决这个问题。方法很简单，

1.  Use **lower ()** method of string data type in python to convert complete sentences into lowercase.
2.  Now pass this sentence into **set (str)** , so that we can get a list of all unique characters in a given string.
3.  Now separate out the list of all letters (a-z). If the list length is 26, all characters exist, and the sentence is **pangram** , otherwise it does not exist.

```
# function to check pangram

def pangram(input):

    # convert input string into lower case
    input = input.lower()

    # convert input string into Set() so that we will
    # list of all unique characters present in sentence
    input = set(input)

    # separate out all alphabets
    # ord(ch) returns ascii value of character
    alpha = [ ch for ch in input if ord(ch) in range(ord('a'), ord('z')+1)]

    if len(alpha) == 26:
        return 'true'
    else:
        return 'false'

# Driver program
if __name__ == "__main__":
    input = 'The quick brown fox jumps over the lazy dog'
    print (pangram(input))
```

输出:

```
true

```