# 在链表中搜索元素的 Python 程序

> 原文:[https://www . geesforgeks . org/python-program-for-search-in-a-element-in-a-link-list/](https://www.geeksforgeeks.org/python-program-for-searching-an-element-in-a-linked-list/)

编写一个函数，在给定的单链表中搜索给定的键“x”。如果 x 出现在链表中，函数应该返回 true，否则返回 false。

```
bool search(Node *head, int x)
```

例如，如果要搜索的关键字是 15，链表是 14->21->11->30->10，那么函数应该返回 false。如果要搜索的关键字是 14，那么函数应该返回 true。
**迭代求解:**

```
1) Initialize a node pointer, current = head.
2) Do following while current is not NULL
    a) current->key is equal to the key being searched return true.
    b) current = current->next
3) Return false 
```

下面是上述算法的迭代实现，以搜索给定的关键字。

## 计算机编程语言

```
# Iterative Python program to search 
# an element in linked list

# Node class
class Node:

    # Function to initialise the 
    # node object
    def __init__(self, data):

        # Assign data
        self.data = data 

        # Initialize next as null
        self.next = None 

# Linked List class
class LinkedList:
    def __init__(self):

        # Initialize head as None
        self.head = None 

    # This function insert a new node at the
    # beginning of the linked list
    def push(self, new_data):

        # Create a new Node
        new_node = Node(new_data)

        # 3\. Make next of new Node as head
        new_node.next = self.head

        # 4\. Move the head to point to new Node
        self.head = new_node

    # This Function checks whether the value
    # x present in the linked list 
    def search(self, x):

        # Initialize current to head
        current = self.head

        # Loop till current not equal to None
        while current != None:
            if current.data == x:

                # Data found
                return True 

            current = current.next

        # Data Not found
        return False 

# Driver code
if __name__ == '__main__':

    # Start with the empty list
    llist = LinkedList()

    # Use push() to construct list
    # 14->21->11->30->10 
    llist.push(10);
    llist.push(30);
    llist.push(11);
    llist.push(21);
    llist.push(14);

    if llist.search(21):
        print("Yes")
    else:
        print("No")
# This code is contributed by Ravi Shankar
```

**输出:**

```
Yes
```

**递归解:**

```
bool search(head, x)
1) If head is NULL, return false.
2) If head's key is same as x, return true;
3) Else return search(head->next, x)
```

下面是上述算法的递归实现，用于搜索给定的关键字。

## 计算机编程语言

```
# Recursive Python program to 
# search an element in linked list

# Node class
class Node:

    # Function to initialize 
    # the node object
    def __init__(self, data):

        # Assign data
        self.data = data 

        # Initialize next as null
        self.next = None 

class LinkedList:

    def __init__(self):

        # Initialize head as None
        self.head = None 

    # This function insert a new node at 
    # the beginning of the linked list
    def push(self, new_data):

        # Create a new Node
        new_node = Node(new_data)

        # Make next of new Node as head
        new_node.next = self.head

        # Move the head to 
        # point to new Node
        self.head = new_node

    # Checks whether the value key 
    # is present in linked list 
    def search(self, li, key):

        # Base case
        if(not li):
            return False

        # If key is present in 
        # current node, return true
        if(li.data == key):
            return True

        # Recur for remaining list
        return self.search(li.next, key)

# Driver Code            
if __name__=='__main__':

    li = LinkedList()

    li.push(1)
    li.push(2)
    li.push(3)
    li.push(4)

    key = 4

    if li.search(li.head,key):
        print("Yes")
    else:
        print("No")
# This code is contributed by Manoj Sharma
```

**输出:**

```
Yes
```

更多细节请参考完整的文章[在链表中搜索元素(迭代和递归)](https://www.geeksforgeeks.org/search-an-element-in-a-linked-list-iterative-and-recursive/)！