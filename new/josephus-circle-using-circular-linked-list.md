# Josephus Circle 使用循环链表

> 原文：[https://www.geeksforgeeks.org/josephus-circle-using-circular-linked-list/](https://www.geeksforgeeks.org/josephus-circle-using-circular-linked-list/)

n 人围成一圈等待执行。 计数从圆的某个点开始，然后沿固定的方向围绕圆进行。 在每个步骤中，将跳过一定数量的人员，然后执行下一个人员。 消灭在圈中进行（随着被处决者的撤离，圈越来越小），直到只有最后一个剩下的人被赋予了自由。 给定总人数 n 和人数 m，表示跳过 m-1 人，第 m 人被杀。 任务是选择初始圈子中的位置，以便您成为最后一个幸存者，从而生存下来。

**示例**：

```
Input : Length of circle : n = 4
        Count to choose next : m = 2
Output : 1

Input : n = 5
        m = 3
Output : 4

```

我们讨论了此问题的不同解决方案（此处 [](https://www.geeksforgeeks.org/josephus-problem-set-1-a-on-solution/) 和 [](https://www.geeksforgeeks.org/josephus-problem-using-bit-magic/) ）。 在这篇文章中，讨论了一个简单的基于[循环链表](https://www.geeksforgeeks.org/circular-linked-list/)的解决方案。

1）创建大小为 n 的循环链表。

2）遍历链表，并在第 m 个节点中逐个删除，直到剩下一个节点为止。

3）返回唯一左节点的值。

## C++

```cpp

// CPP program to find last man standing 
#include<bits/stdc++.h> 
using namespace std; 

/* structure for a node in circular 
   linked list */
struct Node 
{ 
    int data; 
    struct Node *next; 
}; 

// To create a new node of circular 
// linked list 
Node *newNode(int data) 
{ 
   Node *temp = new Node; 
   temp->next = temp; 
   temp->data = data; 
} 

/* Function to find the only person left 
   after one in every m-th node is killed 
   in a circle of n nodes */
void getJosephusPosition(int m, int n) 
{ 
    // Create a circular linked list of 
    // size N. 
    Node *head = newNode(1); 
    Node *prev = head; 
    for (int i = 2; i <= n; i++) 
    { 
        prev->next = newNode(i); 
        prev = prev->next; 
    } 
    prev->next = head; // Connect last 
                       // node to first 

    /* while only one node is left in the 
    linked list*/
    Node *ptr1 = head, *ptr2 = head; 
    while (ptr1->next != ptr1) 
    { 
        // Find m-th node 
        int count = 1; 
        while (count != m) 
        { 
            ptr2 = ptr1; 
            ptr1 = ptr1->next; 
            count++; 
        } 

        /* Remove the m-th node */
        ptr2->next = ptr1->next; 
        free(ptr1); 
        ptr1 = ptr2->next; 
    } 

    printf ("Last person left standing "
            "(Josephus Position) is %d\n ", 
            ptr1->data); 
} 

/* Driver program to test above functions */
int main() 
{ 
    int n = 14, m = 2; 
    getJosephusPosition(m, n); 
    return 0; 
} 

```

## Java

```java

// Java Code to find the last man Standing  
public class GFG { 

    // Node class to store data  
    static class Node 
    { 
        public int data ; 
        public Node next; 
        public Node( int data ) 
        { 
            this.data = data; 
        } 
    } 

    /* Function to find the only person left 
    after one in every m-th node is killed 
    in a circle of n nodes */
    static void getJosephusPosition(int m, int n) 
    { 
        // Create a circular linked list of 
        // size N. 
        Node head = new Node(1); 
        Node prev = head; 
        for(int i = 2; i <= n; i++) 
        { 
            prev.next = new Node(i); 
            prev = prev.next; 
        } 

        // Connect last node to first 
        prev.next = head; 

        /* while only one node is left in the 
        linked list*/
        Node ptr1 = head, ptr2 = head; 

        while(ptr1.next != ptr1) 
        { 

            // Find m-th node 
            int count = 1; 
            while(count != m) 
            { 
                ptr2 = ptr1; 
                ptr1 = ptr1.next; 
                count++; 
            } 

            /* Remove the m-th node */
            ptr2.next = ptr1.next; 
            ptr1 = ptr2.next; 
        } 
        System.out.println ("Last person left standing " + 
                 "(Josephus Position) is " + ptr1.data); 
    } 

    /* Driver program to test above functions */
    public static void main(String args[]) 
    { 
        int n = 14, m = 2; 
        getJosephusPosition(m, n); 
    } 
} 

```

## C#

```cs

// C# Code to find the last man Standing  
using System; 
public class GFG {  

    // Node class to store data  
    class Node  
    {  
        public int data ;  
        public Node next;  
        public Node( int data )  
        {  
            this.data = data;  
        }  
    }  

    /* Function to find the only person left  
    after one in every m-th node is killed  
    in a circle of n nodes */
    static void getJosephusPosition(int m, int n)  
    {  
        // Create a circular linked list of  
        // size N.  
        Node head = new Node(1);  
        Node prev = head;  
        for(int i = 2; i <= n; i++)  
        {  
            prev.next = new Node(i);  
            prev = prev.next;  
        }  

        // Connect last node to first  
        prev.next = head;  

        /* while only one node is left in the  
        linked list*/
        Node ptr1 = head, ptr2 = head;  

        while(ptr1.next != ptr1)  
        {  

            // Find m-th node  
            int count = 1;  
            while(count != m)  
            {  
                ptr2 = ptr1;  
                ptr1 = ptr1.next;  
                count++;  
            }  

            /* Remove the m-th node */
            ptr2.next = ptr1.next;  
            ptr1 = ptr2.next;  
        }  
        Console.WriteLine ("Last person left standing " +  
                "(Josephus Position) is " + ptr1.data);  
    }  

    /* Driver program to test above functions */
     static public void Main(String []args)  
    {  
        int n = 14, m = 2;  
        getJosephusPosition(m, n);  
    }  
}  
//contributed by Arnab Kundu 

```

**输出**：

```
Last person left standing (Josephus Position) is 13

```

**时间复杂度**：O（m * n）

本文由 **Raghav Sharma** 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论。

