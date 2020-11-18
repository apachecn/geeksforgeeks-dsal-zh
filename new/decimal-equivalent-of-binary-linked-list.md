# 二进制链表

的十进制等效项

给定一个0和1的单链表，可以找到其十进制等效项。

```
   Input  : 0->0->0->1->1->0->0->1->0
   Output : 50   

   Input  : 1->0->0
   Output : 4

```

空链表的十进制值视为0。

将结果初始化为0。遍历链接列表，并为每个节点将结果乘以2，然后将节点的数据添加到其中。

## C ++

```

// C++ Program to find decimal value of  
// binary linked list  
#include <bits/stdc++.h> 
using namespace std; 

/* Link list Node */
class Node  
{  
    public: 
    bool data;  
    Node* next;  
};  

/* Returns decimal value of binary linked list */
int decimalValue(Node *head)  
{  
    // Initialized result  
    int res = 0;  

    // Traverse linked list  
    while (head != NULL)  
    {  
        // Multiply result by 2 and add  
        // head's data  
        res = (res << 1) + head->data;  

        // Move next  
        head = head->next;  
    }  
    return res;  
}  

// Utility function to create a new node.  
Node *newNode(bool data)  
{  
    Node *temp = new Node;  
    temp->data = data;  
    temp->next = NULL;  
    return temp;  
}  

/* Driver program to test above function*/
int main()  
{  
    /* Start with the empty list */
    Node* head = newNode(1);  
    head->next = newNode(0);  
    head->next->next = newNode(1);  
    head->next->next->next = newNode(1);  

    cout << "Decimal value is "
        << decimalValue(head);  

    return 0;  
}  

// This is code is contributed by rathbhupendra 

```

## C

```

// C Program to find decimal value of 
// binary linked list 
#include<iostream> 
using namespace std; 

/* Link list Node */
struct Node 
{ 
    bool data; 
    struct Node* next; 
}; 

/* Returns decimal value of binary linked list */
int decimalValue(struct Node *head) 
{ 
    // Initialized result 
    int  res = 0; 

    // Traverse linked list 
    while (head != NULL) 
    { 
        // Multiply result by 2 and add 
        // head's data 
        res = (res  << 1) + head->data; 

        // Move next 
        head = head->next; 
    } 
    return res; 
} 

// Utility function to create a new node. 
Node *newNode(bool data) 
{ 
    struct Node *temp = new Node; 
    temp->data = data; 
    temp->next = NULL; 
    return temp; 
} 

/* Driver program to test above function*/
int main() 
{ 
    /* Start with the empty list */
    struct Node* head = newNode(1); 
    head->next = newNode(0); 
    head->next->next = newNode(1); 
    head->next->next->next = newNode(1); 

    cout << "Decimal value is "
         << decimalValue(head); 

    return 0; 
} 

```

## 爪哇

```

// Java Program to find decimal value of  
// binary linked list  
class GFG 
{ 

// Link list Node / 
static class Node  
{  
    boolean data;  
    Node next;  
};  

// Returns decimal value of binary linked list / 
static int decimalValue( Node head)  
{  
    // Initialized result  
    int res = 0;  

    // Traverse linked list  
    while (head != null)  
    {  
        // Multiply result by 2 and add  
        // head's data  
        res = (res << 1) + (head.data?1:0);  

        // Move next  
        head = head.next;  
    }  
    return res;  
}  

// Utility function to create a new node.  
static Node newNode(int data)  
{  
    Node temp = new Node();  
    temp.data = (data==1? true:false);  
    temp.next = null;  
    return temp;  
}  

// Driver code/ 
public static void main(String args[]) 
{  
    // Start with the empty list / 
    Node head = newNode(1);  
    head.next = newNode(0);  
    head.next.next = newNode(1);  
    head.next.next.next = newNode(1);  

    System.out.print( "Decimal value is "+decimalValue(head));  
} 
} 

// This code is contributed by Arnab Kundu 

```

## Python3

```

# Python3 program to find decimal value  
# of binary linked list 

# Node Class 
class Node: 

    # Function to initialise the  
    # node object 
    def __init__(self, data): 

        # Assign data 
        self.data = data  

        # Initialize next as null 
        self.next = None 

# Linked List class contains  
# a Node object 
class LinkedList: 

    # Function to initialize head 
    def __init__(self): 

        self.head = None

    # Returns decimal value of binary 
    # linked list 
    def decimalValue(self, head): 

        # Initialized result 
        res = 0

        # Traverse linked list 
        while head: 

            # Multiply result by 2 and  
            # add head's data  
            res = (res << 1) + head.data 

            # Move Next 
            head = head.next

        return res 

# Driver code 
if __name__ == '__main__': 

    #Start with the empty list  
    llist = LinkedList() 

    llist.head = Node(1) 
    llist.head.next = Node(0) 
    llist.head.next.next = Node(1) 
    llist.head.next.next.next = Node(1) 

    print("Decimal Value is {}".format( 
           llist.decimalValue(llist.head))) 

# This code is contributed by Mohit Jangra 

```

## C＃

```

// C# Program to find decimal value of  
// binary linked list  
using System; 

class GFG 
{ 

// Link list Node / 
public class Node  
{  
    public Boolean data;  
    public Node next;  
};  

// Returns decimal value of binary linked list 
static int decimalValue( Node head)  
{  
    // Initialized result  
    int res = 0;  

    // Traverse linked list  
    while (head != null)  
    {  
        // Multiply result by 2 and add  
        // head's data  
        res = (res << 1) + (head.data ? 1 : 0);  

        // Move next  
        head = head.next;  
    }  
    return res;  
}  

// Utility function to create a new node.  
static Node newNode(int data)  
{  
    Node temp = new Node();  
    temp.data = (data == 1 ? true : false);  
    temp.next = null;  
    return temp;  
}  

// Driver cod 
public static void Main(String []args) 
{  
    // Start with the empty list  
    Node head = newNode(1);  
    head.next = newNode(0);  
    head.next.next = newNode(1);  
    head.next.next.next = newNode(1);  

    Console.WriteLine("Decimal value is " +  
                       decimalValue(head));  
} 
} 

// This code is contributed by Rajput-Ji 

```

**输出：**

```
Decimal value is 11

```

本文由 **Shivam Gupta** 提供。 如果您喜欢GeeksforGeeks并希望做出贡献，那么您也可以写一篇文章，然后将您的文章邮寄到contribution@geeksforgeeks.org。 查看您的文章出现在GeeksforGeeks主页上，并帮助其他Geeks。
如果发现任何不正确的内容，或者想分享有关上述主题的更多信息，请发表评论。

注意读者！ 现在不要停止学习。 通过 [**DSA自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的DSA概念，并为行业做好准备。