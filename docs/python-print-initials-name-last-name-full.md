# Python |用全名打印名字的首字母

> 原文:[https://www . geesforgeks . org/python-print-首字母-姓名-姓氏-全名/](https://www.geeksforgeeks.org/python-print-initials-name-last-name-full/)

给定一个名字，打印名字的首字母(大写)和姓氏(大写的第一个字母)并用点分隔开。

**例:**

```
Input : geeks for geeks
Output : G.F.Geeks

Input : mohandas karamchand gandhi
Output : M.K.Gandhi 

```

一种天真的方法是迭代空格，并在除最后一个空格之外的每个空格后打印下一个字母。最后一个空格我们必须用简单的方法把最后一个空格后面的所有字符都去掉。

在内置函数中使用 **python，我们可以[将](https://www.geeksforgeeks.org/how-to-split-a-string-in-cc-python-and-java/)单词拆分成一个列表，然后遍历到第二个最后一个单词，并使用 Python 中的 [upper()](https://www.geeksforgeeks.org/isupper-islower-lower-upper-python-applications/) 函数打印大写的第一个字符，然后使用 Python 中的 [title()](https://www.geeksforgeeks.org/python-string-methods-set-1-find-rfind-startwith-endwith-islower-isupper-lower-upper-swapcase-title/) 函数添加最后一个单词，该函数会自动将第一个字母表转换为大写。**

```
# python program to print initials of a name 
def name(s):

    # split the string into a list 
    l = s.split()
    new = ""

    # traverse in the list 
    for i in range(len(l)-1):
        s = l[i]

        # adds the capital first character 
        new += (s[0].upper()+'.')

    # l[-1] gives last item of list l. We
    # use title to print first character in
    # capital.
    new += l[-1].title()

    return new 

# Driver code            
s ="mohandas karamchand gandhi" 
print(name(s))        
```

**输出:**

```
M.K.Gandhi

```