# 用于从未排序的链表中删除重复项的 Python 程序

> 原文:[https://www . geesforgeks . org/python-program-for-remove-replications-from-unsorted-link-list/](https://www.geeksforgeeks.org/python-program-for-removing-duplicates-from-an-unsorted-linked-list/)

编写一个 removeDuplicates()函数，该函数获取一个列表并从列表中删除任何重复的节点。列表未排序。
例如，如果链接列表是 12->11->12->21->41->43->21，则 removeDuplicates()应该将列表转换为 12->11->21->41->43。

**方法 1(使用两个循环):**
这是使用两个循环的简单方法。外环用于逐个拾取元素，内环将拾取的元素与其余元素进行比较。
感谢 Gaurav Saxena 对编写这段代码的帮助。

## 蟒蛇 3

```
# Python3 program to remove duplicates
# from unsorted linked list
class Node():    
    def __init__(self, data):        
        self.data = data
        self.next = None

class LinkedList():    
    def __init__(self):

        # Head of list
        self.head = None

    def remove_duplicates(self):        
        ptr1 = None
        ptr2 = None
        dup = None
        ptr1 = self.head

        # Pick elements one by one
        while (ptr1 != None and 
               ptr1.next != None):

            ptr2 = ptr1

            # Compare the picked element with 
            # rest of the elements
            while (ptr2.next != None):

                # If duplicate then delete it
                if (ptr1.data == ptr2.next.data):

                    # Sequence of steps is important here
                    dup = ptr2.next
                    ptr2.next = ptr2.next.next
                else:
                    ptr2 = ptr2.next

            ptr1 = ptr1.next

    # Function to print nodes in a 
    # given linked list 
    def printList(self):
        temp = self.head

        while(temp != None):
            print(temp.data, end = " ")
            temp = temp.next

        print()

# Driver code
list = LinkedList()
list.head = Node(10)
list.head.next = Node(12)
list.head.next.next = Node(11)
list.head.next.next.next = Node(11)
list.head.next.next.next.next = Node(12)
list.head.next.next.next.next.next = Node(11)
list.head.next.next.next.next.next.next = Node(10)

print("Linked List before removing duplicates :")
list.printList()
list.remove_duplicates()
print()
print("Linked List after removing duplicates :")
list.printList()
# This code is contributed by maheshwaripiyush9
```

**输出:**

```
Linked list before removing duplicates:
10 12 11 11 12 11 10 
Linked list after removing duplicates:
10 12 11
```

**时间复杂度:** O(n^2)

**方法 2(使用排序):**
一般来说，合并排序是最适合高效排序链表的排序算法。
1)使用合并排序对元素进行排序。我们很快会写一篇关于排序链表的文章。O(nLogn)
2)使用[算法在线性时间内移除重复项，以移除排序链表中的重复项。O(n)](https://www.geeksforgeeks.org/remove-duplicates-from-a-sorted-linked-list/)
请注意，这种方法没有保留元素的原始顺序。
**时间复杂度:** O(nLogn)

**方法 3(使用哈希):**
我们从头到尾遍历链接列表。对于每一个新遇到的元素，我们检查它是否在哈希表中:如果是，我们删除它；否则我们把它放到散列表中。

## 蟒蛇 3

```
# Python3 program to remove duplicates 
# from unsorted linkedlist 
class Node:    
    def __init__(self, data):        
        self.data = data
        self.next = None

class LinkedList:    
    def __init__(self):        
        self.head = None

    # Function to print nodes in a  
    # given linked list 
    def printlist(self):        
        temp = self.head

        while (temp):
            print(temp.data, end = " ")
            temp = temp.next

    # Function to remove duplicates from a 
    # unsorted linked list 
    def removeDuplicates(self, head):

        # Base case of empty list or 
        # list with only one element
        if self.head is None or self.head.next is None:
            return head

        # Hash to store seen values 
        hash = set()  

        current = head
        hash.add(self.head.data)

        while current.next is not None:
            if current.next.data in hash:
                current.next = current.next.next
            else:
                hash.add(current.next.data)
                current = current.next

        return head

# Driver code 
if __name__ == "__main__":

    # Creating Empty list
    llist = LinkedList()
    llist.head = Node(10)
    second = Node(12)
    third = Node(11)
    fourth = Node(11)
    fifth = Node(12)
    sixth = Node(11)
    seventh = Node(10)

    # Connecting second and third
    llist.head.next = second
    second.next = third
    third.next = fourth
    fourth.next = fifth
    fifth.next = sixth
    sixth.next = seventh

    # Printing data
    print("Linked List before removing Duplicates.")
    llist.printlist()
    llist.removeDuplicates(llist.head)
    print("Linked List after removing duplicates.")
    llist.printlist()
# This code is contributed by rajataro0
```

**输出:**

```
Linked list before removing duplicates:
10 12 11 11 12 11 10 
Linked list after removing duplicates:
10 12 11
```

感谢 bearwang 提出这个方法。
**时间复杂度:**平均 O(n)(假设哈希表访问时间平均为 O(1))。

更多详细信息，请参考完整文章[从未排序的链表](https://www.geeksforgeeks.org/remove-duplicates-from-an-unsorted-linked-list/)中删除重复项！