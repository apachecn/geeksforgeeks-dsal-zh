# Python程序使用一次遍历来查找链接列表的中间

给定一个单链表，找到链表的中间。 给定一个单链表，找到链表的中间。 例如，如果给定的链表为1-> 2-> 3-> 4-> 5，则输出应为3。

**方法1：**
遍历整个链表并计算编号。 节点。 现在再次遍历列表，直到count / 2并返回count / 2处的节点。

**方法2：**
使用两个指针遍历链表。 将一个指针移动一个，另一个指针移动两个。 当快速指针到达末尾时，慢速指针将到达链表的中间。

```

# Python 3 program to find the middle of a   
# given linked list  

# Node class  
class Node:  

    # Function to initialise the node object  
    def __init__(self, data):  
        self.data = data  
        self.next = None 

class LinkedList: 

    def __init__(self): 
        self.head = None

    def push(self, new_data): 
        new_node = Node(new_data) 
        new_node.next = self.head 
        self.head = new_node 

    # Function to get the middle of  
    # the linked list 
    def printMiddle(self): 
        slow_ptr = self.head 
        fast_ptr = self.head 

        if self.head is not None: 
            while (fast_ptr is not None and fast_ptr.next is not None): 
                fast_ptr = fast_ptr.next.next
                slow_ptr = slow_ptr.next
            print("The middle element is: ", slow_ptr.data) 

# Driver code 
list1 = LinkedList() 
list1.push(5) 
list1.push(4) 
list1.push(2) 
list1.push(3) 
list1.push(1) 
list1.printMiddle() 

```

**Output:**

```
The middle element is:  2

```

**方法3：**
初始化临时变量为head
初始化计数为零
循环执行，直到head变为Null（即列表的末尾），并在count为时增加临时节点 仅奇数，以这种方式temp将遍历到元素的中部，并且head将遍历所有链表。 打印温度数据。

```

# Python 3 program to find the middle of a   
# given linked list  

class Node: 
    def __init__(self, value): 
        self.data = value 
        self.next = None

class LinkedList: 

    def __init__(self): 
        self.head = None

    # create Node and and make linked list 
    def push(self, new_data): 
        new_node = Node(new_data) 
        new_node.next = self.head 
        self.head = new_node 

    def printMiddle(self): 
        temp = self.head  
        count = 0

        while self.head: 

            # only update when count is odd 
            if (count & 1):  
                temp = temp.next
            self.head = self.head.next

            # increment count in each iteration  
            count += 1 

        print(temp.data)      

# Driver code 
llist = LinkedList()  
llist.push(1) 
llist.push(20)  
llist.push(100)  
llist.push(15)  
llist.push(35) 
llist.printMiddle() 
# code has been contributed by - Yogesh Joshi 

```

**Output:**

```
100

```

注意读者！ 现在不要停止学习。 通过 [**DSA自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的DSA概念，并为行业做好准备。

* * *

* * *

如果您喜欢GeeksforGeeks并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至tribution@geeksforgeeks.org。 查看您的文章出现在GeeksforGeeks主页上，并帮助其他Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。