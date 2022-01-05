# 检查 Python 中的平衡括号

> 原文:[https://www . geesforgeks . org/检查平衡-python 括号/](https://www.geeksforgeeks.org/check-for-balanced-parentheses-in-python/)

给定一个表达式字符串，编写一个 python 程序来查找给定字符串是否有平衡括号。

**示例:**

```
Input : {[]{()}}
Output : Balanced

Input : [{}{}(]
Output : Unbalanced

```

**方法#1 :** 使用堆栈

检查平衡括号的一种方法是使用堆栈。每次遇到开括号时，将它推入堆栈，遇到闭括号时，将其与堆栈顶部匹配并弹出。如果堆栈末尾为空，则返回“平衡”，否则返回“不平衡”。

```
# Python3 code to Check for 
# balanced parentheses in an expression
open_list = ["[","{","("]
close_list = ["]","}",")"]

# Function to check parentheses
def check(myStr):
    stack = []
    for i in myStr:
        if i in open_list:
            stack.append(i)
        elif i in close_list:
            pos = close_list.index(i)
            if ((len(stack) > 0) and
                (open_list[pos] == stack[len(stack)-1])):
                stack.pop()
            else:
                return "Unbalanced"
    if len(stack) == 0:
        return "Balanced"
    else:
        return "Unbalanced"

# Driver code
string = "{[]{()}}"
print(string,"-", check(string))

string = "[{}{})(]"
print(string,"-", check(string))

string = "((()"
print(string,"-",check(string))
```

**Output:**

```
{[]{()}} - Balanced
[{}{})(] - Unbalanced
((() - Unbalanced

```

**接近#2 :** 使用队列

首先将左括号映射到相应的右括号。使用“I”迭代给定的表达式，如果“I”是开括号，则在队列中追加，如果“I”是闭括号，则检查队列是空的还是“I”是队列的顶部元素，如果是，则返回“不平衡”，否则返回“平衡”。

```
# Python3 code to Check for 
# balanced parentheses in an expression
def check(expression):

    open_tup = tuple('({[')
    close_tup = tuple(')}]')
    map = dict(zip(open_tup, close_tup))
    queue = []

    for i in expression:
        if i in open_tup:
            queue.append(map[i])
        elif i in close_tup:
            if not queue or i != queue.pop():
                return "Unbalanced"
    if not queue:
        return "Balanced"
    else:
        return "Unbalanced"

# Driver code
string = "{[]{()}}"
print(string, "-", check(string))

string = "((()"
print(string,"-",check(string))
```

**Output:**

```
{[]{()}} - Balanced
((() - Unbalanced

```

**方法#3 :** 基于淘汰的
在每次迭代中，最里面的括号被淘汰(替换为空字符串)。如果我们以一个空字符串结束，我们的初始字符串是平衡的；否则，不会。

```
# Python3 code to Check for 
# balanced parentheses in an expression
def check(my_string):
    brackets = ['()', '{}', '[]']
    while any(x in my_string for x in brackets):
        for br in brackets:
            my_string = my_string.replace(br, '')
    return not my_string

# Driver code
string = "{[]{()}}"
print(string, "-", "Balanced" 
      if check(string) else "Unbalanced")
```

**Output:**

```
{[]{()}} - Balanced

```