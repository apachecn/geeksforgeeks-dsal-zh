# 在链接列表

> 原文：[https://www.geeksforgeeks.org/find-the-balanced-node-in-a-linked-list/](https://www.geeksforgeeks.org/find-the-balanced-node-in-a-linked-list/)

中找到平衡的节点

给定一个链表，任务是在链表中找到平衡节点。 平衡节点是这样一个节点，其左侧所有节点的总和等于右侧所有节点的总和，如果找不到这样的节点，则打印`-1`。

**示例**：

> **输入**：1-> 2-> 7-> 10-> 1-> 6-> 3->空
> **输出**：10
> 10 左侧的节点总和是 1 + 2 + 7 = 10
> 并且，10 右侧的是 1 + 6 + 3 = 10
> 
> **输入**：1-> 5-> 5-> 10-> -3->空
> **输出**：-1

**方法**：

*   首先，找到所有节点值的总和。

*   现在，一次遍历链表，同时遍历所有先前节点的值之和，并通过从总和中减去当前节点值和先前节点的值之和来找到其余节点的和。

*   比较两个总和，如果它们相等，则当前节点为所需节点，否则打印-1。

下面是上述方法的实现：

```

# Python3 implementation of the approach 
import sys 
import math 

# Structure of a node of linked list  
class Node: 
    def __init__(self, data): 
        self.next = None
        self.data = data 

# Push the new node to front of the linked list 
def push(head, data): 

    # Return new node as head if head is empty 
    if not head: 
        return Node(data) 
    temp = Node(data) 
    temp.next = head 
    head = temp 
    return head 

# Function to find the balanced node 
def findBalancedNode(head): 
    tsum = 0
    curr_node = head 

    # Traverse through all node  
    # to find the total sum 
    while curr_node: 
        tsum+= curr_node.data 
        curr_node = curr_node.next

    # Set current_sum and remaining sum to zero  
    current_sum, remaining_sum = 0, 0
    curr_node = head 

    # Traversing the list to check balanced node 
    while(curr_node): 
        remaining_sum = tsum-(current_sum + curr_node.data) 

        # If sum of the nodes on the left and the current node  
        # is equal to the sum of the nodes on the right 
        if current_sum == remaining_sum: 
            return curr_node.data 
        current_sum+= curr_node.data 
        curr_node = curr_node.next

    return -1

# Driver code 
if __name__=='__main__': 
    head = None
    head = push(head, 3) 
    head = push(head, 6) 
    head = push(head, 1) 
    head = push(head, 10) 
    head = push(head, 7) 
    head = push(head, 2) 
    head = push(head, 1) 

    print(findBalancedNode(head)) 

```

**Output:**

```
10

```

**时间复杂度**：`O(n)`



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。