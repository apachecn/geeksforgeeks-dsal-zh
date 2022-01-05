# 编写函数获取链表第 n 个节点的 Python 程序

> 原文:[https://www . geesforgeks . org/python-写程序-函数-获取-链表中的第 n 个节点/](https://www.geeksforgeeks.org/python-program-for-writing-a-function-to-get-nth-node-in-a-linked-list/)

编写一个 GetNth()函数，该函数接受一个链表和一个整数索引，并返回存储在该索引位置的节点中的数据值。

**示例:**

```
Input:  1->10->30->14,  index = 2
Output: 30  
The node at index 2 is 30
```

**算法:**

```
1\. Initialize count = 0
2\. Loop through the link list
     a. If count is equal to the passed index then return
        current node
     b. Increment count
     c. change current to point to next of the current.
```

**实施:**

## 计算机编程语言

```
# A complete working Python program to 
# find n'th node in a linked list

# Node class
class Node:
    # Function to initialize the node object
    def __init__(self, data):

        # Assign data
        self.data = data  

        # Initialize next as null
        self.next = None  

# Linked List class contains a Node object
class LinkedList:

    # Function to initialize head
    def __init__(self):
        self.head = None

    # This function is in LinkedList class. 
    # It inserts a new node at the beginning 
    # of Linked List.
    def push(self, new_data):

        # 1 & 2: Allocate the Node &
        #        Put in the data
        new_node = Node(new_data)

        # 3\. Make next of new Node as head
        new_node.next = self.head

        # 4\. Move the head to point to new Node
        self.head = new_node

    # Returns data at given index in linked list
    def getNth(self, index):

        # Initialise temp
        current = self.head  

        # Index of current node
        count = 0  

        # Loop while end of linked list 
        # is not reached
        while (current):
            if (count == index):
                return current.data
            count += 1
            current = current.next

        # If we get to this line, the caller was 
        # asking for a non-existent element so 
        # we assert fail
        assert(false)
        return 0

# Driver Code
if __name__ == '__main__':

    llist = LinkedList()

    # Use push() to construct list
    # 1->12->1->4->1
    llist.push(1)
    llist.push(4)
    llist.push(1)
    llist.push(12)
    llist.push(1)

    n = 3
    print("Element at index 3 is :", 
           llist.getNth(n))
```

**输出:**

```
Element at index 3 is 4
```

**时间复杂度:** O(n)

**方法 2-带递归:**
此方法由 [MY_DOOM](https://auth.geeksforgeeks.org/user/MY_DOOM) 贡献。

**算法:**

```
getnth(node,n)
1\. Initialize count = 0
2\. if count==n
     return node->data
3\. else
    return getnth(node->next,n-1)
```

**实施:**

## 蟒蛇 3

```
# Python3 program to find n'th node in
# linked list using recursion

class Node:
    def __init__(self, data):
        self.data = data
        self.next = None

class LinkedList:
    def __init__(self):
        self.head = None

    # Given a reference (pointer to pointer) to 
    # the head of a list and an int, push a new 
    # node on the front of the list.

    # Make new node and add
    # into LinkedList
    def push(self, new_data):                                
        new_node = Node(new_data)
        new_node.next = self.head
        self.head = new_node

    def getNth(self, llist, position):

        # Call recursive method
        llist.getNthNode(self.head, 
                         position, llist)

    # Recursive method to find Nth Node
    def getNthNode(self.head, 
                   position, llist):

        # Initialize count
        count = 0  
        if(head):

            # If count is equal to position,
            # it means we have found the position
            if count == position:  

                print(head.data)
            else:
                llist.getNthNode(head.next,
                                 position - 1, llist)
        else:  
            # If head doesn't exist we have
            # traversed the LinkedList
            print('Index Doesn\'t exist')

# Driver Code
if __name__ == "__main__":
    llist = LinkedList()
    llist.push(1)
    llist.push(4)
    llist.push(1)
    llist.push(12)
    llist.push(1)

    # llist.getNth(llist,int(input()))
    # Enter the node position here
    # First argument is instance of LinkedList

    print("Element at Index 3 is", end = " ")
    llist.getNth(llist, 3)
# This code is contributed by Yogesh Joshi
```

**输出:**

```
Element at index 3 is 4
```

**时间复杂度:** O(n)

详情请参考[写函数获取链表](https://www.geeksforgeeks.org/write-a-function-to-get-nth-node-in-a-linked-list/)中第 n 个节点的完整文章！