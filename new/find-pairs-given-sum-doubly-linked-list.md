# 在双向链表

> 原文：[https://www.geeksforgeeks.org/find-pairs-given-sum-doubly-linked-list/](https://www.geeksforgeeks.org/find-pairs-given-sum-doubly-linked-list/)

中查找具有给定总和的对

给定一个排序的正相异元素的双链表，任务是在双链表中查找对，它们的总和等于给定值 x，而不使用任何多余的空间？

**例如**：

```
Input : head : 1 <-> 2 <-> 4 <-> 5 <-> 6 <-> 8 <-> 9
        x = 7
Output: (6, 1), (5,2)

```

预期的时间复杂度为`O(n)`，辅助空间为`O(1)`。

解决此问题的一种简单方法**是，一个节点一个接一个地选取每个节点，并通过向前遍历在剩余列表中找到总和等于 x 的第二个元素。此问题的时间复杂度为 O（n ^ 2），n 是双向链表中节点的总数。**

针对此问题的**有效解决方案**与该文章的[相同。 这是算法：](https://www.geeksforgeeks.org/write-a-c-program-that-given-a-set-a-of-n-numbers-and-another-number-x-determines-whether-or-not-there-exist-two-elements-in-s-whose-sum-is-exactly-x/)

*   初始化两个指针变量以在排序后的双向链表中查找候选元素。首先，从双向链表的开头初始化**。 **first = head** ，然后用双向链表的最后一个节点初始化**，然后初始化**；即， **second = last_node** 。**

*   我们将**第一个**和**第二个**指针初始化为第一个和最后一个节点。 这里我们没有随机访问权限，因此要找到第二个指针，我们遍历列表以初始化第二个指针。

*   如果当前**首先**和**第二**的当前总和小于 x，则我们将**首先**向前移动。 如果**第一个**和**第二个**元素的当前总和大于 x，则我们将**第二个**向后移动。

*   循环终止条件也与数组不同。 当两个指针中的任何一个变为 NULL 或它们彼此交叉（第二个->下一个=第一个），或者它们变为相同（第一个==第二个）时，循环终止

## C++

```cpp

// C++ program to find a pair with given sum x. 
#include<bits/stdc++.h> 
using namespace std; 

// structure of node of doubly linked list 
struct Node 
{ 
    int data; 
    struct Node *next, *prev; 
}; 

// Function to find pair whose sum equal to given value x. 
void pairSum(struct Node *head, int x) 
{ 
    // Set two pointers, first to the beginning of DLL 
    // and second to the end of DLL. 
    struct Node *first = head; 
    struct Node *second = head; 
    while (second->next != NULL) 
         second = second->next; 

    // To track if we find a pair or not 
    bool found = false; 

    // The loop terminates when either of two pointers 
    // become NULL, or they cross each other (second->next 
    // == first), or they become same (first == second) 
    while (first != NULL && second != NULL && 
           first != second && second->next != first) 
    { 
         // pair found 
         if ((first->data + second->data) == x) 
         { 
              found = true; 
              cout << "(" << first->data<< ", "
                   << second->data << ")" << endl; 

              // move first in forward direction 
              first = first->next; 

              // move second in backward direction 
              second = second->prev; 
          } 
          else
          { 
              if ((first->data + second->data) < x) 
                 first = first->next; 
              else
                 second = second->prev; 
          } 
      } 

      // if pair is not present 
      if (found == false) 
           cout << "No pair found"; 
} 

// A utility function to insert a new node at the 
// beginning of doubly linked list 
void insert(struct Node **head, int data) 
{ 
    struct Node *temp = new Node; 
    temp->data = data; 
    temp->next = temp->prev = NULL; 
    if (!(*head)) 
        (*head) = temp; 
    else
    { 
        temp->next = *head; 
        (*head)->prev = temp; 
        (*head) = temp; 
    } 
} 

// Driver program 
int main() 
{ 
    struct Node *head = NULL; 
    insert(&head, 9); 
    insert(&head, 8); 
    insert(&head, 6); 
    insert(&head, 5); 
    insert(&head, 4); 
    insert(&head, 2); 
    insert(&head, 1); 
    int x = 7; 

    pairSum(head, x); 

    return 0; 
} 

```

## Java

```java

// Java program to find a 
// pair with given sum x. 
class GFG 
{ 

// structure of node of 
// doubly linked list 
static class Node 
{ 
    int data; 
    Node next, prev; 
}; 

// Function to find pair whose  
// sum equal to given value x. 
static void pairSum( Node head, int x) 
{ 
    // Set two pointers, first 
    // to the beginning of DLL 
    // and second to the end of DLL. 
    Node first = head; 
    Node second = head; 
    while (second.next != null) 
        second = second.next; 

    // To track if we find a pair or not 
    boolean found = false; 

    // The loop terminates when either  
    // of two pointers become null, or  
    // they cross each other (second.next 
    // == first), or they become same 
    // (first == second) 
    while (first != null && second != null && 
           first != second && second.next != first) 
    { 
        // pair found 
        if ((first.data + second.data) == x) 
        { 
            found = true; 
            System.out.println( "(" + first.data +  
                                ", "+ second.data + ")" ); 

            // move first in forward direction 
            first = first.next; 

            // move second in backward direction 
            second = second.prev; 
        } 
        else
        { 
            if ((first.data + second.data) < x) 
                first = first.next; 
            else
                second = second.prev; 
        } 
    } 

    // if pair is not present 
    if (found == false) 
        System.out.println("No pair found"); 
} 

// A utility function to insert  
// a new node at the beginning 
// of doubly linked list 
static Node insert(Node head, int data) 
{ 
    Node temp = new Node(); 
    temp.data = data; 
    temp.next = temp.prev = null; 
    if (head == null) 
        (head) = temp; 
    else
    { 
        temp.next = head; 
        (head).prev = temp; 
        (head) = temp; 
    } 
    return temp; 
} 

// Driver Code 
public static void main(String args[]) 
{ 
    Node head = null; 
    head = insert(head, 9); 
    head = insert(head, 8); 
    head = insert(head, 6); 
    head = insert(head, 5); 
    head = insert(head, 4); 
    head = insert(head, 2); 
    head = insert(head, 1); 
    int x = 7; 

    pairSum(head, x); 
} 
} 

// This code is contributed 
// by Arnab Kundu 

```

## C#

```cs

// C# program to find a  
// pair with given sum x. 
using System;  

class GFG  
{  

    // structure of node of  
    // doubly linked list  
    class Node  
    {  
        public int data;  
        public Node next, prev;  
    };  

    // Function to find pair whose  
    // sum equal to given value x.  
    static void pairSum( Node head, int x)  
    {  
        // Set two pointers, first  
        // to the beginning of DLL  
        // and second to the end of DLL.  
        Node first = head;  
        Node second = head;  
        while (second.next != null)  
            second = second.next;  

        // To track if we find a pair or not  
        bool found = false;  

        // The loop terminates when either  
        // of two pointers become null, or  
        // they cross each other (second.next  
        // == first), or they become same  
        // (first == second)  
        while (first != null && second != null &&  
            first != second && second.next != first)  
        {  
            // pair found  
            if ((first.data + second.data) == x)  
            {  
                found = true;  
                Console.WriteLine( "(" + first.data +  
                                    ", "+ second.data + ")" );  

                // move first in forward direction  
                first = first.next;  

                // move second in backward direction  
                second = second.prev;  
            }  
            else
            {  
                if ((first.data + second.data) < x)  
                    first = first.next;  
                else
                    second = second.prev;  
            }  
        }  

        // if pair is not present  
        if (found == false)  
            Console.WriteLine("No pair found");  
    }  

    // A utility function to insert  
    // a new node at the beginning  
    // of doubly linked list  
    static Node insert(Node head, int data)  
    {  
        Node temp = new Node();  
        temp.data = data;  
        temp.next = temp.prev = null;  
        if (head == null)  
            (head) = temp;  
        else
        {  
            temp.next = head;  
            (head).prev = temp;  
            (head) = temp;  
        }  
        return temp;  
    }  

    // Driver Code  
    public static void Main(String []args)  
    {  
        Node head = null;  
        head = insert(head, 9);  
        head = insert(head, 8);  
        head = insert(head, 6);  
        head = insert(head, 5);  
        head = insert(head, 4);  
        head = insert(head, 2);  
        head = insert(head, 1);  
        int x = 7;  

        pairSum(head, x);  
    }  
}  

// This code is contributed by 29AjayKumar 

```

**Output:**

```
(1,6) 
(2,5)

```

**时间复杂度**：`O(n)`

**辅助空间**：`O(1)`

如果未对链表进行排序，那么我们可以将列表作为第一步进行排序。 但是在那种情况下，整体时间复杂度将变为 O（n Log n）。 如果没有多余的空间，我们可以在这种情况下使用哈希。 基于哈希的解决方案与方法 2 [在此处](https://www.geeksforgeeks.org/write-a-c-program-that-given-a-set-a-of-n-numbers-and-another-number-x-determines-whether-or-not-there-exist-two-elements-in-s-whose-sum-is-exactly-x/)相同。

本文由 [**Shashank Mishra（Gullu）**](https://www.facebook.com/shashank.mishra.92167) 贡献。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论。

