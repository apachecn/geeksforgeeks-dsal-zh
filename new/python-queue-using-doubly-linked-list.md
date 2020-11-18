# Python | 使用双链表

> 原文：[https://www.geeksforgeeks.org/python-queue-using-doubly-linked-list/](https://www.geeksforgeeks.org/python-queue-using-doubly-linked-list/)

进行排队

队列是使用先进先出原则（FIFO）插入和删除的对象的集合。 插入是在队列的后部（后部）完成的，并且可以从队列中的第一个（前部）位置访问和删除元素。

### 队列操作：

```
1\. enqueue()     : Adds element to the back of Queue.
2\. dequeue()     : Removes and returns the first element from the queue.
3\. first()       : Returns the first element of the queue without removing it.
4\. size()        : returns the number of elements in the Queue.
5\. isEmpty()     : Return True if Queue is Empty else return False.
6\. printqueue()  : Print all elements of the Queue.

```

### 以下是在 Python 中使用 Doubly LinkedList 实现上述 Queue 操作的方法：

```

# A complete working Python program to demonstrate all  
# Queue operations using doubly linked list  

# Node class  
class Node: 

# Function to initialise the node object 
    def __init__(self, data): 
        self.data = data # Assign data 
        self.next = None # Initialize next as null 
        self.prev = None # Initialize prev as null 

# Queue class contains a Node object 
class Queue: 

    # Function to initialize head  
    def __init__(self): 
        self.head = None
        self.last=None

# Function to add an element data in the Queue 
    def enqueue(self, data): 
        if self.last is None: 
            self.head =Node(data) 
            self.last =self.head 
        else: 
            self.last.next = Node(data) 
            self.last.next.prev=self.last 
            self.last = self.last.next

# Function to remove first element and return the element from the queue  
    def dequeue(self): 

        if self.head is None: 
            return None
        else: 
            temp= self.head.data 
            self.head = self.head.next
            self.head.prev=None
            return temp 

# Function to return top element in the queue  
    def first(self): 

        return self.head.data 

# Function to return the size of the queue 
    def size(self): 

        temp=self.head 
        count=0
        while temp is not None: 
            count=count+1
            temp=temp.next
        return count 

# Function to check if the queue is empty or not       
    def isEmpty(self): 

        if self.head is None: 
            return True
        else: 
            return False

# Function to print the stack  
    def printqueue(self): 

        print("queue elements are:") 
        temp=self.head 
        while temp is not None: 
            print(temp.data,end="->") 
            temp=temp.next

# Code execution starts here           
if __name__=='__main__':  

# Start with the empty queue 
  queue = Queue() 

  print("Queue operations using doubly linked list") 

# Insert 4 at the end. So queue becomes 4->None   
  queue.enqueue(4) 

# Insert 5 at the end. So queue becomes 4->5None   
  queue.enqueue(5) 

# Insert 6 at the end. So queue becomes 4->5->6->None   
  queue.enqueue(6) 

# Insert 7 at the end. So queue becomes 4->5->6->7->None   
  queue.enqueue(7) 

# Print the queue  
  queue.printqueue() 

# Print the first element  
  print("\nfirst element is ",queue.first()) 

# Print the queue size  
  print("Size of the queue is ",queue.size()) 

# remove the first element  
  queue.dequeue() 

# remove the first element  
  queue.dequeue() 

# first two elements are removed 
# Print the queue  
  print("After applying dequeue() two times") 
  queue.printqueue() 

# Print True if queue is empty else False  
  print("\nqueue is empty:",queue.isEmpty()) 

```

**Output:**

```
Queue operations using doubly linked list
queue elements are:
4->5->6->7->
first element is  4
Size of the queue is  4
After applying dequeue() two times
queue elements are:
6->7->
queue is empty: False

```

注意怪胎！ 通过 [**Python 编程基础**](https://practice.geeksforgeeks.org/courses/Python-Foundation?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=GFG_Article_Bottom_Python_Foundation) 课程加强基础，并学习基础知识。

首先，您的面试准备将通过 [**Python DS**](https://practice.geeksforgeeks.org/courses/Data-Structures-With-Python?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=GFG_Article_Bottom_Python_DS) 课程增强您的数据结构概念。

* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。