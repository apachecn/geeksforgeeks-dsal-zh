# 克隆堆栈而没有多余的空间

在给定源堆栈的情况下，将源堆栈的内容复制到目标堆栈，并保持相同的顺序，而无需使用额外的空间。

**示例：**

```
Input : Source:- |3|
                 |2|
                 |1|

Output : Destination:- |3|
                       |2|
                       |1|

Input : Source:- |a|
                 |b|
                 |c|

Output : Destination:- |a|
                       |b|
                       |c|

```

**方法：**为了解决此问题而不使用额外的空间，我们首先反转源堆栈，然后**逐一弹出**源堆栈的顶部元素，然后**推入**将其放入目标堆栈。 我们按照以下步骤反转源堆栈：

1.  将变量**计数**初始化为0。
2.  从源堆栈中弹出顶部元素，并将其存储在变量 **topVal** 中。
3.  现在从源堆栈中弹出元素，并将其推入目标堆栈，直到源堆栈的长度等于 **count** 为止。
4.  将 **topVal** 推入源堆栈，然后弹出目标堆栈中的所有元素，并将其推入源堆栈。
5.  增加**计数**的值。
6.  如果**计数**不等于源堆栈的长度– 1，则从步骤2开始重复该过程。

下面是上述方法的实现：

```

# Python3 program to copy the contents from source stack 
# into destination stack without using extra space 

# Define a class for Stack 
class Stack(object): 

    def __init__(self): 
        self.stack = [] 

    def push(self, value): 
        self.stack.append(value) 

    def pop(self): 
        return self.stack.pop() 

    def length(self): 
        return len(self.stack) 

    def display(self): 
        for i in range(len(self.stack)-1, -1, -1): 
            print(self.stack[i]) 

        print() 

source = Stack()     # Source Stack 
dest = Stack()         # Destination Stack 

source.push(1) 
source.push(2) 
source.push(3) 

print("Source Stack:") 
source.display() 

count = 0

# Reverse the order of the values in source stack 
while count != source.length() - 1: 

    topVal = source.pop() 
    while count != source.length(): 
        dest.push(source.pop()) 

    source.push(topVal) 
    while dest.length() != 0: 
        source.push(dest.pop()) 

    count += 1

# Pop the values from source and push into destination stack 
while source.length() != 0: 
    dest.push(source.pop()) 

print("Destination Stack:") 
dest.display() 

```

**输出：**

```
Source Stack:
3
2
1

Destination Stack:
3
2
1

```

**时间复杂度：** ![O(n^2)](img/598be626cedc018633480e0f69670fd8.png "Rendered by QuickLaTeX.com")

**高效方法：**更好的方法是将堆栈表示为链表。 以与反转链表相同的方式反转源堆栈，**逐一弹出**源堆栈的顶部元素，然后**将其推入**到目标堆栈。

下面是上述方法的实现：

```

# Python3 program to copy the contents from source stack 
# into destination stack without using extra space  
# in linear time using Linked List 

class StackNode(object): 

    def __init__(self, data): 
        self.data = data 
        self.next = None

# Class for Stack to represent it as Linked list 
class Stack(object): 

    def __init__(self): 
        self.top = None

    def push(self, value): 

        newVal = StackNode(value) 

        if self.top == None: 
            self.top = newVal 

        else: 
            newVal.next = self.top 
            self.top = newVal  

    def pop(self): 

        val = self.top.data 
        self.top = self.top.next
        return val 

    def display(self): 

        current = self.top 
        while current != None: 
            print(current.data) 
            current = current.next

        print() 

    def reverse(self): 

        current, temp, prev = self.top, None, None

        while current != None: 
            temp = current.next
            current.next = prev 
            prev = current 
            current = temp 

        self.top = prev 

    def isEmpty(self): 
        return self.top == None

source = Stack()        # Source Stack 
dest = Stack()          # Destination Stack 

source.push(1) 
source.push(2) 
source.push(3) 

print("Source Stack:") 
source.display() 

source.reverse() 

# Pop the values from source and push into destination stack 
while source.isEmpty() != True: 
    dest.push(source.pop()) 

print("Destination Stack:") 
dest.display() 

```

**输出：**

```
Source Stack:
3
2
1

Destination Stack:
3
2
1

```

**时间复杂度：** ![O(n)](img/d5229a9c6f59029cbbb0f53974c9a9de.png "Rendered by QuickLaTeX.com")

注意读者！ 现在不要停止学习。 通过 [**DSA自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的DSA概念，并为行业做好准备。

* * *

* * *

如果您喜欢GeeksforGeeks并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至tribution@geeksforgeeks.org。 查看您的文章出现在GeeksforGeeks主页上，并帮助其他Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。