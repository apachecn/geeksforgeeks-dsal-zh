# 用下一个随机指针集克隆链表的 Python 程序 2

> 原文:[https://www . geesforgeks . org/python-program-for-clone-a-link-list-with-next-and-random-pointer-set-2/](https://www.geeksforgeeks.org/python-program-for-cloning-a-linked-list-with-next-and-random-pointer-set-2/)

我们已经讨论了克隆链表的两种不同方法。在[这篇](https://www.geeksforgeeks.org/a-linked-list-with-next-and-arbit-pointer/)的帖子中，讨论了一个更简单的克隆链表的方法。

想法是使用哈希。下面是算法。

1.  遍历原始链表，根据数据进行复制。
2.  制作一个键值对与原始链表节点和复制链表节点的哈希映射。
3.  再次遍历原始链表，并使用哈希映射调整克隆链表节点的下一个随机引用。

下面是上述方法的实现。

## 蟒蛇 3

```
# Python3 program to clone a linked list 
# with random pointers 
class Node: 
    def __init__(self, data):

        # Node Data
        self.data = data 

        # Node Next
        self.next = None 

        # Node Random
        self.random = None 

# Dictionary
class MyDictionary(dict): 

    # __init__ function
    def __init__(self):

        super().__init__()
        self = dict()

        # Function to add key:value
        def add(self, key, value):

        # Adding Values to dictionary
        self[key] = value 

# Linked list class 
class LinkedList:

    # Linked list constructor
    def __init__(self, node):
        self.head = node

    # Method to print the list.
    def __repr__(self):

        temp = self.head
        while temp is not None:
            random = temp.random
            random_data = (random.data if 
                           random is not None else -1)

            data = temp.data
            print(f"Data-{data}, 
                  Random data: {random_data}")
            temp = temp.next

        return ""

    # Push method to put data always at 
    # the head in the linked list.
    def push(self, data):

        node = Node(data)
        node.next = self.head
        self.head = node

    # Actual clone method which returns head
    # reference of cloned linked list.
    def clone(self):

        # Initialize two references, one 
        # with original list's head.
        original = self.head
        clone = None

        # Initialize two references, one 
        # with original list's head.
        mp = MyDictionary()

        # Traverse the original list and 
        # make a copy of that
        # in the clone linked list
        while original is not None:
            clone = Node(original.data)
            mp.add(original, clone)
            original = original.next

        # Adjusting the original 
        # list reference again.
        original = self.head

        # Traversal of original list again
        # to adjust the next and random 
        # references of clone list using hash map.
        while original is not None:
            clone = mp.get(original)
            clone.next = mp.get(original.next)
            clone.random = mp.get(original.random)
            original = original.next

        # Return the head reference of the clone list.
        return LinkedList(self.head)

# Driver code

# Pushing data in the linked list.
l = LinkedList(Node(5))
l.push(4)
l.push(3)
l.push(2)
l.push(1)

# Setting up random references.
l.head.random = l.head.next.next
l.head.next.random = 
l.head.next.next.next
l.head.next.next.random = 
l.head.next.next.next.next
l.head.next.next.next.random = 
(l.head.next.next.next.next.next)
l.head.next.next.next.next.random = 
l.head.next

# Making a clone of the 
# original linked list.
clone = l.clone()

# Print the original and cloned
# linked list.s
print("Original linked list")
print(l)
print("Cloned linked list")
print(clone)
# This code is contributed by ashwinathappan
```

**输出:**

```
Original linked list
Data = 1, Random data = 3
Data = 2, Random data = 4
Data = 3, Random data = 5
Data = 4, Random data = -1
Data = 5, Random data = 2

Cloned linked list
Data = 1, Random data = 3
Data = 2, Random data = 4
Data = 3, Random data = 5
Data = 4, Random data = -1
Data = 5, Random data = 2
```

**时间复杂度:**O(n)
T3】辅助空间: O(n)
详情请参考[上的完整文章用 next 和随机指针克隆链表| Set 2](https://www.geeksforgeeks.org/clone-linked-list-next-arbit-pointer-set-2/) ！