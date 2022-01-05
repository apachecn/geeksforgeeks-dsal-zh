# Python |将字符列表转换成字符串

> 原文:[https://www . geesforgeks . org/python-convert-list-characters-string/](https://www.geeksforgeeks.org/python-convert-list-characters-string/)

给定一个字符列表，将所有字符合并成一个字符串。

示例:

```
Input : ['g', 'e', 'e', 'k', 's', 'f', 'o', 
             'r', 'g', 'e', 'e', 'k', 's']
Output : geeksforgeeks 

Input : ['p', 'r', 'o', 'g', 'r', 'a', 'm', 
                        'm', 'i', 'n', 'g']
Output : programming 

```

**方法 1:遍历列表**

在开头初始化一个空字符串。遍历字符列表，为每个索引在初始字符串中添加字符。完成遍历后，打印添加了每个字符的字符串。

```
# Python program to convert a list
# of character

def convert(s):

    # initialization of string to ""
    new = ""

    # traverse in the string 
    for x in s:
        new += x 

    # return string 
    return new

# driver code   
s = ['g', 'e', 'e', 'k', 's', 'f', 'o', 'r', 'g', 'e', 'e', 'k', 's']
print(convert(s))
```

**输出:**

```
geeksforgeeks

```

**方法二:使用 join()函数**

使用 python 中的 [join()](https://www.geeksforgeeks.org/python-string-methods-set-2-len-count-center-ljust-rjust-isalpha-isalnum-isspace-join/) 函数，可以连接列表中的所有字符。语法是:

```
str = ""
str1 = ( "geeks", "for", "geeks" )
str.join(str1) 
```

可以通过初始化 str= "来轻松地连接字符列表，以便其间没有空格。

```
# Python program to convert a list
# of character

def convert(s):

    # initialization of string to ""
    str1 = ""

    # using join function join the list s by 
    # separating words by str1
    return(str1.join(s))

# driver code   
s = ['g', 'e', 'e', 'k', 's', 'f', 'o', 'r', 'g', 'e', 'e', 'k', 's']
print(convert(s))
```

**输出:**

```
geeksforgeeks

```