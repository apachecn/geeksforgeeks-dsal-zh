# 布伦特循环检测算法

给定一个链表，请检查链表是否具有循环。 下图显示了带有循环的链表。

[![](img/de522899e01a1322ab2808eeff1ad73e.png "Linked List Loop")](https://media.geeksforgeeks.org/wp-content/cdn-uploads/2009/04/Linked-List-Loop.gif)

我们已经讨论了 [Floyd的算法来检测链表中的周期。](https://www.geeksforgeeks.org/detect-loop-in-a-linked-list/)

**布伦特的周期检测算法**与 [floyd的算法](https://www.geeksforgeeks.org/detect-loop-in-a-linked-list/)类似，因为它也使用了两种指针技术。 但是他们的方法有所不同。 在这里，我们使一个指针静止直到每次迭代，然后以两个的乘方将其传送到另一个指针**。 循环的开始由两个满足的**的最小功率确定。 通过减少调用次数，可以改善Floyd算法的常数因子。

1.  以2的幂数移动快速指针（或second_pointer），直到找到循环。 每次通电后，我们将慢速指针（或first_pointer）重置为第二个指针的先前值。 每次通电后，将长度重置为0。
2.  循环测试的条件是first_pointer和second_pointer变为相同。 如果second_pointer变为NULL，则不存在循环。
3.  当我们脱离循环时，我们就有循环的长度。
4.  我们将first_pointer重置为head，将second_pointer重置为head + length位置的节点。
5.  现在，我们将两个指针一一移动以找到循环的起点。

**与弗洛伊德（Floyd）算法的比较：**
1）在第一个循环检测循环本身中找到循环的长度。 不需要额外的工作。
2）我们在每次迭代中只移动第二个，避免移动第一个（如果移动到下一个节点涉及评估函数，这可能会很昂贵）。

## C ++

```

// CPP program to implement Brent's cycle  
// detection algorithm to detect cycle in 
// a linked list. 
#include <stdio.h> 
#include <stdlib.h> 

/* Link list node */
struct Node { 
    int data; 
    struct Node* next; 
}; 

/* This function detects loop in the list 
If loop was there in the list then it returns, 
the first node of loop otherwise returns NULL */
struct Node* detectCycle(struct Node* head) 
{ 
    // if head is null then no loop 
    if (head == NULL)  
        return NULL;     

    struct Node* first_pointer = head; 
    struct Node* second_pointer = head->next; 
    int power = 1; 
    int length = 1; 

    // This loop runs till we find the loop. 
    // If there is no loop then second_pointer 
    // ends at NULL . 
    while (second_pointer != NULL &&  
           second_pointer != first_pointer) { 

        // condition after which we will 
        // update the power and length as 
        // smallest power of two gives the 
        // start of cycle. 
        if (length == power) { 

            // updating the power. 
            power *= 2; 

            // updating the length 
            length = 0; 

            first_pointer = second_pointer; 
        } 

        second_pointer = second_pointer->next; 
        ++length; 
    } 

    // if it is null then no loop 
    if (second_pointer == NULL)  
        return NULL;     

    // Otherwise length stores actual length  
    // of loop. 
    // If needed, we can also print length of 
    // loop. 
    // printf("Length of loop is %d\n", length); 

    // Now set first_pointer to the beginning 
    // and second_pointer to beginning plus 
    // cycle length which is length. 
    first_pointer = second_pointer = head; 
    while (length > 0) { 
        second_pointer = second_pointer->next; 
        --length; 
    } 

    // Now move both pointers at same speed so 
    // that they meet at the beginning of loop. 
    while (second_pointer != first_pointer) { 
        second_pointer = second_pointer->next; 
        first_pointer = first_pointer->next; 
    } 

    // If needed, we can also print length of 
    // loop. 
    // printf("Length of loop is %d", length); 

    return first_pointer; 
} 

struct Node* newNode(int key) 
{ 
    struct Node* temp =  
      (struct Node*)malloc(sizeof(struct Node)); 
    temp->data = key; 
    temp->next = NULL; 
    return temp; 
} 

// Driver program to test above function 
int main() 
{ 
    struct Node* head = newNode(50); 
    head->next = newNode(20); 
    head->next->next = newNode(15); 
    head->next->next->next = newNode(4); 
    head->next->next->next->next = newNode(10); 

    // Create a loop for testing  
    head->next->next->next->next->next =  
                              head->next->next; 

    Node *res = detectCycle(head); 
    if (res == NULL) 
        printf("No loop"); 
    else
        printf("Loop is present at %d", res->data); 
    return 0; 
} 

```

## Python3

```

# Python program to implement 
# Brent's cycle detection 
# algorithm to detect cycle 
# in a linked list. 

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

    # Function to insert a new Node 
    #  at the beginning 
    def push(self, new_data): 
        new_node = Node(new_data) 
        new_node.next = self.head 
        self.head = new_node 

    # Utility function to prit 
    # the linked LinkedList 
    def printList(self): 
        temp = self.head 
        while(temp): 
            print (temp.data,end=" ") 
            temp = temp.next

    def detectCycle(self): 
         # if head is null 
         # then no loop 
         temp=self.head 

         if not (temp): 
             return False
         first_p=temp 
         second_p=temp.next
         power = 1
         length = 1

         # This loop runs till we 
         # find the loop. If there 
         # is no loop then second 
         # pointer ends at NULL  
         while (second_p and second_p!= first_p): 

             # condition after which  
             # we will update the power 
             # and length as smallest 
             # power of two gives 
             # the start of cycle. 
           if (length == power): 

            # updating the power. 
                power *= 2

            # updating the length 
                length = 0

                first_p = second_p 

           second_p = second_p.next
           length=length+1
         # if it is null then no loop 
         if not (second_p) : 
             return    

    # Otherwise length stores 
    # actual length of loop. 
    # If needed, we can also 
    # print length of loop. 
    # print("Length of loop is ") 
    # print (length) 

    # Now set first_pointer 
    # to the beginning and 
    # second_pointer to 
    # beginning plus cycle 
    # length which is length. 
         first_p = second_p = self.head 
         while (length > 0): 
             second_p = second_p.next
             length=length-1

            # Now move both pointers 
            # at same speed so that 
            # they meet at the 
            # beginning of loop. 
         while (second_p!= first_p) : 
               second_p = second_p.next
               first_p = first_p.next

         return first_p 

# Driver program for testing 
llist = LinkedList() 
llist.push(50) 
llist.push(20) 
llist.push(15) 
llist.push(4) 
llist.push(10) 

# Create a loop for testing 
llist.head.next.next.next.next.next = llist.head.next.next; 
res=llist.detectCycle() 
if( res.data): 
    print ("loop found at ",end=' ') 
    print (res.data) 
else : 
    print ("No Loop ") 

# This code is contributed by Gitanjali 

```

Output:

```
Loop is present at 15

```

***时间复杂度：*** O（m + n），其中 **m** 是序列的最小索引，即周期的开始， **n [** 是循环的长度。
***辅助空间：*** – **O（1）**辅助空间

**参考文献：**
[https://en.wikipedia.org/wiki/Cycle_detection#Brent’s_algorithm](https://en.wikipedia.org/wiki/Cycle_detection#Brent's_algorithm)
[github](https://github.com/alxli/Algorithm-Anthology/blob/master/Section-1-Elementary-Algorithms/1.4.2%20Cycle%20Detection%20(Brent's).cpp)

注意读者！ 现在不要停止学习。 通过 [**DSA自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的DSA概念，并为行业做好准备。

* * *

* * *

如果您喜欢GeeksforGeeks并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至tribution@geeksforgeeks.org。 查看您的文章出现在GeeksforGeeks主页上，并帮助其他Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。