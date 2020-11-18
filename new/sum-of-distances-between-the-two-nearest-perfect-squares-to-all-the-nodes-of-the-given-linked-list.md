# 两个最接近的完美平方到给定链表

的所有节点之间的距离总和

给定一个链表，任务是为给定链表的所有节点找到两个最接近的完美平方之间的距离之和。

**示例：**

> **输入：** 3-> 15-> 7-> NULL
> **输出：** 15
> 对于3：最接近的左侧完美平方为1，最接近 右4即4-1 = 3
> 对于15：16 – 9 = 7
> 对于7：9 – 4 = 5
> 3 + 7 + 5 = 15
> 
> **输入：** 1-> 5-> 10-> 78-> 23->空
> **输出：** 38

**方法：**初始化 **sum = 0** ，对于每个节点，如果当前节点的值本身是一个理想平方，则左，右最接近的理想平方将成为该值本身，而距离为 0.否则，找到左和右最接近的完美正方形，说 **leftPS** 和 **rightPS** ，然后更新 **sum = sum +（+ rightPS – leftPS）**。

下面是上述方法的实现：

```

# Python3 implementation of the approach 
import sys 
import math 

# Structure for a node 
class Node: 
    def __init__(self, data): 
        self.data = data 
        self.next = None

# Function to find the total distance sum 
def distanceSum(head): 

    # If head is null 
    if not head: 
        return

    # To store the required sum 
    tsum = 0
    temp = head 

    # Traversing through all the nodes one by one 
    while(temp): 
        sq_root = math.sqrt(temp.data) 

    # If current node is not a perfect square  
    # then find left perfect square and  
    # right perfect square 
        if sq_root<temp.data: 
            left_ps = math.floor(sq_root)**2
            right_ps = math.ceil(sq_root)**2
            tsum+=(right_ps - left_ps) 

        # Get to the next node 
        temp = temp.next
    return tsum 

# Driver code 
if __name__=='__main__': 
    head = Node(3) 
    head.next = Node(15) 
    head.next.next = Node(7) 
    head.next.next.next = Node(40) 
    head.next.next.next.next = Node(42) 

    result = distanceSum(head) 
    print("{}".format(result)) 

```

**Output:**

```
41

```

**时间复杂度：** O（n）

注意读者！ 现在不要停止学习。 通过 [**DSA自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的DSA概念，并为行业做好准备。

* * *

* * *

如果您喜欢GeeksforGeeks并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至tribution@geeksforgeeks.org。 查看您的文章出现在GeeksforGeeks主页上，并帮助其他Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。