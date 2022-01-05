# Python 代码，用于在单次遍历中将空格移动到字符串前面

> 原文:[https://www . geesforgeks . org/python-code-move-spaces-front-string-single-traversation/](https://www.geeksforgeeks.org/python-code-move-spaces-front-string-single-traversal/)

给定一个包含单词和空格的字符串，编写一个程序，通过遍历字符串一次，将所有空格移到字符串的前面。

示例:

```
Input  : str = "geeks for geeks"
Output : ste = "  geeksforgeeks"

Input  : str = "move these spaces to beginning"
Output : str = "    movethesespacestobeginning"
There were four space characters in input,
all of them should be shifted in front. 

```

该问题已有解决方案，请参考[单次遍历](https://www.geeksforgeeks.org/move-spaces-front-string-single-traversal/)链接时将空格移到字符串前面。
我们将使用[列表理解](https://www.geeksforgeeks.org/python-list-comprehension-and-slicing/)在 Python 中快速解决这个问题。
**接近**:

1.  遍历输入字符串，并使用列表理解创建一个没有任何空格字符的字符串。
2.  现在要知道原始字符串中有多少个空格字符，只需计算原始字符串和新字符串的长度之差。
3.  现在创建另一个字符串，并在开头添加空格字符。

```
# Function to move spaces to front of string 
# in single traversal in Python 

def moveSpaces(input): 

    # Traverse string to create string without spaces 
    noSpaces = [ch for ch in input if ch!=' '] 

    # calculate number of spaces 
    space= len(input) - len(noSpaces) 

    # create result string with spaces 
    result = ' '*space 

    # concatenate spaces with string having no spaces 
    result = '"'+result + ''.join(noSpaces)+'"'
    print (result) 

# Driver program 
if __name__ == "__main__": 
    input = 'geeks for geeks'
    moveSpaces(input) 
```

输出:

```
"  geeksforgeeks"

```