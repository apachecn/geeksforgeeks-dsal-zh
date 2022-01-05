# 用于从排序链表中删除重复项的 Python 程序

> 原文:[https://www . geesforgeks . org/python-program-for-remove-replications-from-sorted-link-list/](https://www.geeksforgeeks.org/python-program-for-removing-duplicates-from-a-sorted-linked-list/)

编写一个函数，接受按非递减顺序排序的列表，并从列表中删除任何重复的节点。该列表只能遍历一次。
例如，如果链接列表是 11->11->11->21->43->43->60，则 removeDuplicates()应该将列表转换为 11- > 21- > 43- > 60。

**算法:**
从头(或开始)节点遍历列表。遍历时，将每个节点与其下一个节点进行比较。如果下一个节点的数据与当前节点相同，则删除下一个节点。在删除节点之前，我们需要存储节点的下一个指针

**实现:**
removeDuplicates()之外的函数只是创建一个链表并测试 remove duplicates()。

## 蟒蛇 3

```
# Python3 program to remove duplicate
# nodes from a sorted linked list 

# Node class 
class Node: 

    # Constructor to initialize 
    # the node object 
    def __init__(self, data): 
        self.data = data 
        self.next = None

class LinkedList: 

    # Function to initialize head 
    def __init__(self): 
        self.head = None

    # Function to insert a new node 
    # at the beginning 
    def push(self, new_data): 
        new_node = Node(new_data) 
        new_node.next = self.head 
        self.head = new_node 

    # Given a reference to the head of a 
    # list and a key, delete the first 
    # occurrence of key in linked list 
    def deleteNode(self, key): 

        # Store head node 
        temp = self.head 

        # If head node itself holds the 
        # key to be deleted 
        if (temp is not None): 
            if (temp.data == key): 
                self.head = temp.next
                temp = None
                return

        # Search for the key to be deleted, 
        # keep track of the previous node as
        # we need to change 'prev.next' 
        while(temp is not None): 
            if temp.data == key: 
                break
            prev = temp 
            temp = temp.next

        # If key was not present in 
        # linked list 
        if(temp == None): 
            return

        # Unlink the node from linked list 
        prev.next = temp.next

        temp = None

    # Utility function to print the 
    # linked LinkedList 
    def printList(self): 
        temp = self.head 
        while(temp): 
            print(temp.data , end = ' ')
            temp = temp.next

    # This function removes duplicates 
    # from a sorted list         
    def removeDuplicates(self):
        temp = self.head
        if temp is None:
            return
        while temp.next is not None:
            if temp.data == temp.next.data:
                new = temp.next.next
                temp.next = None
                temp.next = new
            else:
                temp = temp.next
        return self.head

# Driver Code 
llist = LinkedList() 

llist.push(20) 
llist.push(13) 
llist.push(13)
llist.push(11)
llist.push(11)
llist.push(11)
print ("Created Linked List: ")
llist.printList() 
print()
print("Linked List after removing", 
      "duplicate elements:")
llist.removeDuplicates()
llist.printList() 
# This code is contributed by Dushyant Pathak.
```

**输出:**

```
Linked list before duplicate removal  11 11 11 13 13 20
Linked list after duplicate removal  11 13 20
```

**时间复杂度:** O(n)，其中 n 是给定链表中的节点数。

**递归方法:**

## 蟒蛇 3

```
# Python3 Program to remove duplicates
# from a sorted linked list 
import math

# Link list node 
class Node: 
    def __init__(self, data): 
        self.data = data 
        self.next = None

# The function removes duplicates 
# from a sorted list 
def removeDuplicates(head): 

    # Pointer to store the pointer 
    # of a node to be deleted to_free 

    # Do nothing if the list is empty 
    if (head == None): 
        return

    # Traverse the list till last node 
    if (head.next != None): 

        # Compare head node with next node 
        if (head.data == head.next.data): 

            # The sequence of steps is important. 
            # to_free pointer stores the next of head 
            # pointer which is to be deleted. 
            to_free = head.next
            head.next = head.next.next

            # free(to_free) 
            removeDuplicates(head) 

        # This is tricky: only advance if no deletion
        else: 
            removeDuplicates(head.next) 

    return head

# UTILITY FUNCTIONS 
# Function to insert a node at the 
# beginning of the linked list 
def push(head_ref, new_data): 

    # Allocate node 
    new_node = Node(new_data) 

    # Put in the data 
    new_node.data = new_data 

    # Link the old list off the 
    # new node 
    new_node.next = head_ref     

    # Move the head to point to the 
    # new node 
    head_ref = new_node
    return head_ref

# Function to print nodes in a given 
# linked list 
def printList(node): 
    while (node != None): 
        print(node.data, end = " ") 
        node = node.next

# Driver code
if __name__=='__main__': 

    # Start with the empty list 
    head = None

    # Let us create a sorted linked list
    # to test the functions 
    # Created linked list will be 
    # 11.11.11.13.13.20 
    head = push(head, 20) 
    head = push(head, 13) 
    head = push(head, 13) 
    head = push(head, 11) 
    head = push(head, 11) 
    head = push(head, 11)                                 

    print("Linked list before duplicate removal ",
           end = "") 
    printList(head) 

    # Remove duplicates from linked list 
    removeDuplicates(head) 

    print("Linked list after duplicate removal ",
           end = "") 
    printList(head)         

# This code is contributed by Srathore
```

**输出:**

```
Linked list before duplicate removal  11 11 11 13 13 20
Linked list after duplicate removal  11 13 20
```

**另一种方法:**创建一个指向每个元素第一次出现的指针和另一个将迭代到每个元素的指针 temp，当前一个指针的值不等于 temp 指针时，我们将前一个指针的指针设置为另一个节点的第一次出现。

下面是上述方法的实现:

## 蟒蛇 3

```
# Python3 program to remove duplicates 
# from a sorted linked list  
import math 

# Link list node  
class Node:  

    def __init__(self, data):        
        self.data = data  
        self.next = None

# The function removes duplicates  
# from the given linked list 
def removeDuplicates(head):  

    # Do nothing if the list consist of 
    # only one element or empty  
    if (head == None and 
        head.next == None):
        return

    # Consturct a pointer 
    # pointing towards head
    current = head

    # Initialise a while loop till the 
    # second last node of the linkedlist 
    while (current.next):

        # If the data of current and next
        # node is equal we will skip the
        # node between them
        if current.data == current.next.data:
            current.next = current.next.next

        # If the data of current and 
        # next node is different move
        # the pointer to the next node
        else:
            current = current.next

    return

# UTILITY FUNCTIONS  
# Function to insert a node at the  
# beginning of the linked list  
def push(head_ref, new_data):  

    # Allocate node  
    new_node = Node(new_data)  

    # Put in the data  
    new_node.data = new_data  

    # Link the old list off 
    # the new node  
    new_node.next = head_ref      

    # Move the head to point
    # to the new node  
    head_ref = new_node 

    return head_ref 

# Function to print nodes 
# in a given linked list  
def printList(node):  

    while (node != None):  
        print(node.data, end = " ")  
        node = node.next

# Driver code 
if __name__=='__main__':  

    head = None    
    head = push(head, 20)  
    head = push(head, 13)  
    head = push(head, 13)  
    head = push(head, 11)  
    head = push(head, 11)  
    head = push(head, 11)                                  

    print("List before removal of "  
          "duplicates ", end = "")  
    printList(head)  

    removeDuplicates(head)  

    print("List after removal of "  
          "elements ", end = "")            
    printList(head)          
# This code is contributed by MukulTomar
```

**输出:**

```
List before removal of duplicates
11 11 11 13 13 20 
List after removal of elements
11 13 20 
```

更多详情请参考[从排序链表](https://www.geeksforgeeks.org/remove-duplicates-from-a-sorted-linked-list/)中删除重复项的完整文章！