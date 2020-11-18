# 使用合并排序的两个链接列表的差异

给定两个链表，任务是创建一个链表来存储链表1与链表2的差异，即链表1中的元素而不是链表2中的元素。

**示例：**

> **输入：**
> 列表1：10-> 15-> 4-> 20，
> 列表2：8-> 4-> 2-> 10
> **输出：** 15-> 20
> **说明：**
> 在给定的链表中，元素15和20在列表1中，但在列表1中不存在。 清单2。
> 
> **输入：**
> 列表1：2-> 4-> 8-> 10，
> 列表2：8-> 10
> **输出：** 2-> 4
> **说明：**
> 在给定的链表1中，元素2和4在列表1中存在，但在列表2中不存在。

**方法：**

*   使用合并排序对两个链表进行排序。
*   线性扫描两个排序的列表以在p1和p2上使用两个指针来获得差异，并比较链接列表中节点的数据，并在以下三种情况下执行以下操作–
    1.  如果 **p1.data == p2.data** ，则p1.data不能在差异列表中，因此将指针p1和p2向前移动。
    2.  如果 **p1.data > p2.data** 则p1.data可能存在于其他节点的列表2中，因此将指针p2向前移动。
    3.  如果 **p1.data > p2.data** 那么，p1.data现在不能出现在列表2中，因此将p1的数据添加到差异列表中并将指针p1向前移动。
*   如果到达列表2的末尾，请将列表1的所有其余元素插入差异列表。

下面是上述方法的实现。

## 蟒蛇

```

# Python implementation to create 
# a difference Linked List of  
# two Linked Lists 

# Node of the Linked List 
class Node: 
    def __init__(self, data): 
        self.data = data 
        self.next = None

# Linked List 
class linked_list: 
    def __init__(self): 
        self.head = None

    # Function to insert a node 
    # at the end of Linked List 
    def append(self, data): 
        temp = Node(data) 
        if self.head == None: 
            self.head = temp 
        else: 
            p = self.head 
            while p.next != None: 
                p = p.next
            p.next = temp 

    # Function to find the middle 
    # node of the Linked List  
    def get_mid(self, head): 
        if head == None: 
            return head 
        slow = fast = head 
        while fast.next != None \ 
           and fast.next.next != None: 
            slow = slow.next
            fast = fast.next.next
        return slow 

    # Recursive method to merge the 
    # two half after sorting  
    def merge(self, l, r): 
        if l == None:return r 
        if r == None:return l 

        if l.data<= r.data: 
            result = l 
            result.next = \ 
                self.merge(l.next, r) 
        else: 
            result = r 
            result.next = \ 
                self.merge(l, r.next) 
        return result 

    # Recusive method to divide the  
    # list into two half until 1 node left 
    def merge_sort(self, head): 
        if head == None or head.next == None: 
            return head 
        mid = self.get_mid(head) 
        next_to_mid = mid.next
        mid.next = None
        left = self.merge_sort(head) 
        right = self.merge_sort(next_to_mid) 
        sorted_merge = self.merge(left, right) 
        return sorted_merge 

    # Function to print the list elements 
    def display(self): 
        p = self.head 
        while p != None: 
            print(p.data, end =' ') 
            p = p.next
        print() 

# Function to get the difference list 
def get_difference(p1, p2): 
    difference_list = linked_list() 
    # Scan the lists  
    while p1 != None and p2 != None: 

        # Condition to check if the  
        # Data of the both pointer are  
        # same then move ahead 
        if p2.data == p1.data: 
            p1 = p1.next
            p2 = p2.next

        # Condition to check if the  
        # Data of the first pointer is  
        # greater than second then  
        # move second pointer ahead 
        elif p2.data<p1.data: 
            p2 = p2.next

        # Condition when first pointer 
        # data is greater than the  
        # second pointer then append 
        # into the difference list and move 
        else: 
            difference_list.append(p1.data) 
            p1 = p1.next

    # If end of list2 is reached,  
    # there may be some nodes in  
    # List 1 left to be scanned,  
    # they all will be inserted  
    # in the difference list 
    if p2 == None: 
        while p1: 
            difference_list.append(p1.data) 
            p1 = p1.next

    return difference_list 

# Driver Code 
if __name__ == '__main__': 
    # Linked List 1 
    list1 = linked_list() 
    list1.append(2) 
    list1.append(6) 
    list1.append(8) 
    list1.append(1) 

    # Linked List 2 
    list2 = linked_list() 
    list2.append(4) 
    list2.append(1) 
    list2.append(9) 

    # Sort both the linkedlists 
    list1.head = list1.merge_sort( 
                   list1.head 
                 ) 
    list2.head = list2.merge_sort( 
                   list2.head 
                 ) 

    # Get difference list 
    result = get_difference( 
               list1.head, list2.head 
             ) 
    if result.head: 
        result.display() 

    # if difference list is empty, 
    # then lists are equal 
    else: 
        print('Lists are equal') 

```

**Output:**

```
2 6 8

```

**时间复杂度：** O（M Log M + N Log N）。



* * *

* * *

如果您喜欢GeeksforGeeks并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至tribution@geeksforgeeks.org。 查看您的文章出现在GeeksforGeeks主页上，并帮助其他Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。