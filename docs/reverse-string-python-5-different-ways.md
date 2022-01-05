# Python 中反串(5 种不同方式)

> 原文:[https://www . geesforgeks . org/reverse-string-python-5-differential-way/](https://www.geeksforgeeks.org/reverse-string-python-5-different-ways/)

Python 字符串库不像 list 这样的其他 python 容器那样支持内置的“ **reverse()** ”，因此知道其他方法来反转字符串会很有用。本文讨论了实现这一目标的几种方法。

**Using loop**

```
# Python code to reverse a string 
# using loop

def reverse(s):
  str = ""
  for i in s:
    str = i + str
  return str

s = "Geeksforgeeks"

print ("The original string  is : ",end="")
print (s)

print ("The reversed string(using loops) is : ",end="")
print (reverse(s))
```

输出:

```
The original string  is : Geeksforgeeks
The reversed string(using loops) is : skeegrofskeeG

```

**说明:**在上面的代码中，我们调用了一个函数来反转一个字符串，这个函数迭代到每一个元素，并智能地**在开头**连接每个字符，从而得到反转后的字符串。

**Using recursion**

```
# Python code to reverse a string 
# using recursion

def reverse(s):
    if len(s) == 0:
        return s
    else:
        return reverse(s[1:]) + s[0]

s = "Geeksforgeeks"

print ("The original string  is : ",end="")
print (s)

print ("The reversed string(using recursion) is : ",end="")
print (reverse(s))
```

输出:

```
The original string  is : Geeksforgeeks
The reversed string(using recursion) is : skeegrofskeeG

```

**说明:**在上面的代码中，字符串作为参数传递给递归函数来反转字符串。在函数中，基本条件是如果字符串的长度等于 0，则返回该字符串。如果不等于 0，则递归调用 reverse 函数，对字符串中除第一个字符以外的部分进行切分，并将第一个字符连接到切分字符串的末尾。

**Using stack**

```
# Python code to reverse a string 
# using stack

# Function to create an empty stack. It 
# initializes size of stack as 0
def createStack():
    stack=[]
    return stack

# Function to determine the size of the stack
def size(stack):
    return len(stack)

# Stack is empty if the size is 0
def isEmpty(stack):
    if size(stack) == 0:
        return true

# Function to add an item to stack . It
# increases size by 1    
def push(stack,item):
    stack.append(item)

# Function to remove an item from stack. 
# It decreases size by 1
def pop(stack):
    if isEmpty(stack): return
    return stack.pop()

# A stack based function to reverse a string
def reverse(string):
    n = len(string)

    # Create a empty stack
    stack = createStack()

    # Push all characters of string to stack
    for i in range(0,n,1):
        push(stack,string[i])

    # Making the string empty since all
    # characters are saved in stack    
    string=""

    # Pop all characters of string and put
    # them back to string
    for i in range(0,n,1):
        string+=pop(stack)

    return string

# Driver code
s = "Geeksforgeeks"
print ("The original string  is : ",end="")
print (s)
print ("The reversed string(using stack) is : ",end="")
print (reverse(s))
```

输出:

```
The original string  is : Geeksforgeeks
The reversed string(using stack) is : skeegrofskeeG

```

**解释:**创建一个空栈。一个接一个的字符串被推入堆栈。
堆栈中的所有字符被逐个弹出，并放回字符串。

**Using extended slice syntax**

```
# Python code to reverse a string 
# using extended slice syntax

# Function to reverse a string
def reverse(string):
    string = string[::-1]
    return string

s = "Geeksforgeeks"

print ("The original string  is : ",end="")
print (s)

print ("The reversed string(using extended slice syntax) is : ",end="")
print (reverse(s))
```

输出:

```
The original string  is : Geeksforgeeks
The reversed string(using extended slice syntax) is : skeegrofskeeG

```

**说明:**扩展切片提出将“步长”字段设置为**【开始、停止、步长】**，不给出字段作为开始和停止分别表示默认为 0 和字符串长度，并且“ **-1** ”表示从结束开始并在开始停止，因此反转字符串。

**Using reversed**

```
# Python code to reverse a string 
# using reversed()

# Function to reverse a string
def reverse(string):
    string = "".join(reversed(string))
    return string

s = "Geeksforgeeks"

print ("The original string  is : ",end="")
print (s)

print ("The reversed string(using reversed) is : ",end="")
print (reverse(s))
```

输出:

```
The original string  is : Geeksforgeeks
The reversed string(using reversed) is : skeegrofskeeG

```

**解释:**reversed()返回给定字符串的 reversed 迭代器，然后使用 join()将它的元素连接为空字符串。形成逆序串。

本文由 [**【曼吉特·辛格】**](https://auth.geeksforgeeks.org/profile.php?user=manjeet_04) 供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[contribute.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。

如果你发现任何不正确的地方，或者你想分享更多关于上面讨论的话题的信息，请写评论。