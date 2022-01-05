# 在链表中插入节点的 Python 程序

> 原文:[https://www . geesforgeks . org/python-用于在链表中插入节点的程序/](https://www.geeksforgeeks.org/python-program-for-inserting-a-node-in-a-linked-list/)

我们已经在[之前的帖子](https://www.geeksforgeeks.org/linked-list-set-1-introduction/)中引入了链表。我们还创建了一个简单的 3 节点链表，并讨论了链表遍历。
本文讨论的所有程序都考虑了链表的以下表示。

## 计算机编程语言

```
# Node class
class Node:

    # Function to initialize the 
    # node object
    def __init__(self, data):

        # Assign data
        self.data = data  

        # Initialize next as null
        self.next = None  

# Linked List class
class LinkedList:

    # Function to initialize the 
    # Linked List object
    def __init__(self): 
        self.head = None
```

在这篇文章中，讨论了在链表中插入一个新节点的方法。一个节点可以通过三种方式添加
**1)** 在链表的前面
**2)** 在给定的节点之后。
**3)** 在链表的末尾。

**在前面添加一个节点:(4 步流程)**
新节点总是添加在给定链表的头部之前。新添加的节点成为链表的新头。例如，如果给定的链接列表是 10- > 15- > 20- > 25，并且我们在前面添加了项目 5，则链接列表变成 5->10->15->20->25。让我们调用在列表前面添加的函数是 push()。push()必须接收指向头指针的指针，因为 push 必须更改头指针以指向新节点(参见[本](https://www.geeksforgeeks.org/how-to-write-functions-that-modify-the-head-pointer-of-a-linked-list/)

[![linkedlist_insert_at_start](img/0fcc552ce260975b170428e6877939dc.png)](https://media.geeksforgeeks.org/wp-content/cdn-uploads/gq/2013/03/Linkedlist_insert_at_start.png)

以下是在前端添加节点的 4 个步骤。

## 计算机编程语言

```
# This function is in LinkedList class
# Function to insert a new node at 
# the beginning
def push(self, new_data):

    # 1 & 2: Allocate the Node &
    #        Put in the data
    new_node = Node(new_data)

    # 3\. Make next of new Node as head
    new_node.next = self.head

    # 4\. Move the head to point to new Node 
    self.head = new_node
```

push()的时间复杂度是 O(1)，因为它做的功是恒定的。
**给定节点后添加节点:(5 步流程)**
给我们一个节点的指针，新节点插入给定节点后。

[![linkedlist_insert_middle](img/b6bf7ceee6de4eb0511ffb8bb649abfb.png)](https://media.geeksforgeeks.org/wp-content/cdn-uploads/gq/2013/03/Linkedlist_insert_middle.png) 

## 计算机编程语言

```
# This function is in LinkedList class. 
# Inserts a new node after the given 
# prev_node. This method is defined 
# inside LinkedList class shown above 
def insertAfter(self, prev_node, new_data): 

    # 1\. Check if the given prev_node exists 
    if prev_node is None: 
        print "The given previous node must in LinkedList."
        return

    # 2\. Create new node & 
    # 3\. Put in the data 
    new_node = Node(new_data) 

    # 4\. Make next of new Node as next of prev_node 
    new_node.next = prev_node.next

    # 5\. make next of prev_node as new_node 
    prev_node.next = new_node
```

insertAfter()的时间复杂度是 O(1)，因为它做的功是恒定的。

**在末尾添加节点:(6 步流程)**
新节点总是添加在给定链表的最后一个节点之后。例如，如果给定的链表是 5- > 10- > 15- > 20- > 25，并且我们在末尾添加了一个项目 30，那么链表就变成了 5->10->15->20->25->30。
由于链表通常由链表的头来表示，所以我们必须遍历链表直到结束，然后将倒数第二个节点更改为新节点。

[![linkedlist_insert_last](img/428a5c975bfca4a1c08bc29cf2a6e78a.png)](https://media.geeksforgeeks.org/wp-content/cdn-uploads/gq/2013/03/Linkedlist_insert_last.png)

下面是在末尾添加节点的 6 个步骤。

## 计算机编程语言

```
# This function is defined in Linked List 
# class appends a new node at the end.  
# This method is defined inside LinkedList 
# class shown above 
def append(self, new_data):

   # 1\. Create a new node
   # 2\. Put in the data
   # 3\. Set next as None
   new_node = Node(new_data)

   # 4\. If the Linked List is empty, then 
   #    make the new node as head
   if self.head is None:
        self.head = new_node
        return

   # 5\. Else traverse till the last node
   last = self.head
   while (last.next):
       last = last.next

   # 6\. Change the next of last node
   last.next =  new_node
```

追加的时间复杂度为 O(n)，其中 n 是链表中的节点数。因为从头到尾有一个循环，所以函数做 O(n)工作。
这个方法也可以通过保持一个额外的指针指向链表的尾部/

下面是一个完整的程序，使用上述所有方法来创建一个链表。

## 计算机编程语言

```
# A complete working Python program to demonstrate all
# insertion methods of linked list

# Node class
class Node:

    # Function to initialize the 
    # node object
    def __init__(self, data):

        # Assign data
        self.data = data  

        # Initialize next as null
        self.next = None  

# Linked List class contains a
# Node object
class LinkedList:

    # Function to initialize head
    def __init__(self):
        self.head = None

    # Functio to insert a new node at
    # the beginning
    def push(self, new_data):

        # 1 & 2: Allocate the Node &
        #        Put in the data
        new_node = Node(new_data)

        # 3\. Make next of new Node as head
        new_node.next = self.head

        # 4\. Move the head to point to new Node
        self.head = new_node

    # This function is in LinkedList class. 
    # Inserts a new node after the given
    # prev_node. This method is defined 
    # inside LinkedList class shown above 
    def insertAfter(self, prev_node, new_data):

        # 1\. Check if the given prev_node exists
        if prev_node is None:
            print "The given previous node must inLinkedList."
            return

        #  2\. Create new node &
        #     Put in the data
        new_node = Node(new_data)

        # 4\. Make next of new Node as next 
        #    of prev_node
        new_node.next = prev_node.next

        # 5\. make next of prev_node as new_node
        prev_node.next = new_node

    # This function is defined in Linked List class
    # Appends a new node at the end.  This method is
    # defined inside LinkedList class shown above */
    def append(self, new_data):

        # 1\. Create a new node
        # 2\. Put in the data
        # 3\. Set next as None
        new_node = Node(new_data)

        # 4\. If the Linked List is empty, then make the
        #    new node as head
        if self.head is None:
            self.head = new_node
            return

        # 5\. Else traverse till the last node
        last = self.head
        while (last.next):
            last = last.next

        # 6\. Change the next of last node
        last.next =  new_node

    # Utility function to print the 
    # linked list
    def printList(self):
        temp = self.head
        while (temp):
            print temp.data,
            temp = temp.next

# Code execution starts here
if __name__=='__main__':

    # Start with the empty list
    llist = LinkedList()

    # Insert 6.  So linked list 
    becomes 6->None
    llist.append(6)

    # Insert 7 at the beginning. So 
    # linked list becomes 7->6->None
    llist.push(7);

    # Insert 1 at the beginning. So 
    # linked list becomes 1->7->6->None
    llist.push(1);

    # Insert 4 at the end. So linked list 
    # becomes 1->7->6->4->None
    llist.append(4)

    # Insert 8, after 7\. So linked list 
    # becomes 1 -> 7-> 8-> 6-> 4-> None
    llist.insertAfter(llist.head.next, 8)

    print 'Created linked list is:',
    llist.printList()
# This code is contributed by Manikantan Narasimhan
```

**输出:**

```
 Created Linked list is:  1  7  8  6  4
```

详情请参考[链表|集合 2(插入节点)](https://www.geeksforgeeks.org/linked-list-set-2-inserting-a-node/)整篇文章！