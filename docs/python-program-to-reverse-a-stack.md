# Python 程序反转一个栈

> 原文:[https://www . geesforgeks . org/python-程序到反向堆栈/](https://www.geeksforgeeks.org/python-program-to-reverse-a-stack/)

**栈**是一个基于后进先出概念的线性数据结构。后进先出代表后进先出。在堆栈中，可以在一端插入和删除，这一端称为堆栈的顶部。

在本文中，我们将看到如何使用 Python 反转堆栈。

**算法:**

*   定义堆栈的一些基本函数，如 push()，pop()，show()，empty()，用于基本操作，如分别追加堆栈中的一个项目，移除堆栈中的一个项目，显示堆栈，检查给定的堆栈是否为空。
*   定义两个递归函数 BottomInsertion()和 Reverse()..

**BottomInsertion()** :这个方法在栈底追加元素，BottomInsertion 接受两个值作为参数第一个是 stack，第二个是 elements，这是一个递归方法。

```
# insert element at the bottom of the stack
def BottomInsert(s, value):
    # if stack is empty then call push() method.
    if s.empty():  
        s.push(value)

    # if stack is not empty then execute else
    # block
    else:

        # remove the element and store it to
        # popped  
        popped = s.pop()

        # invoke it self and pass stack and value 
        # as an argument.
        BottomInsert(s, value)

        # append popped item in the bottom of the stack 
        s.push(popped)
```

**Reverse()** :方法是对栈的元素进行反转，这个方法接受栈作为参数 Reverse()也是一个 Recursive()函数。Reverse()是调用 BottomInsertion()方法来完成堆栈上的反向操作。

```
# Reverse()
def Reverse(s): 

    # check the stack is empty of not  
    if s.empty():

        # if empty then do nothing
        pass

    # if stack is not empty then 
    else:

        # pop element and stare it to popped
        popped = s.pop()

        # call it self ans pass stack as an argument
        Reverse(s)

        # call BottomInsert() method and pass stack
        # and popped element as an argument
        BottomInsert(s, popped)
```

下面是实现。

## 蟒蛇 3

```
# create class for stack
class Stack:

    # create empty list
    def __init__(self):
        self.Elements = []

    # push() for insert an element
    def push(self, value):
        self.Elements.append(value)

    # pop() for remove an element
    def pop(self):
        return self.Elements.pop()

    # empty() check the stack is empty of not
    def empty(self):
        return self.Elements == []

    # show() display stack
    def show(self):
        for value in reversed(self.Elements):
            print(value)

# Insert_Bottom() insert value at bottom
def BottomInsert(s, value):

    # check the stack is empty or not
    if s.empty():

        # if stack is empty then call
        # push() method.
        s.push(value)

    # if stack is not empty then execute
    # else block
    else:
        popped = s.pop()
        BottomInsert(s, value)
        s.push(popped)

# Reverse() reverse the stack
def Reverse(s):
    if s.empty():
        pass
    else:
        popped = s.pop()
        Reverse(s)
        BottomInsert(s, popped)

# create object of stack class
stk = Stack()

stk.push(1)
stk.push(2)
stk.push(3)
stk.push(4)
stk.push(5)

print("Original Stack")
stk.show()

print("\nStack after Reversing")
Reverse(stk)
stk.show()
```

**输出:**

```
Original Stack
5
4
3
2
1

Stack after Reversing
1
2
3
4
5
```