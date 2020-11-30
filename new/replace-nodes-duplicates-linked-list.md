# 用链表

> 原文：[https://www.geeksforgeeks.org/replace-nodes-duplicates-linked-list/](https://www.geeksforgeeks.org/replace-nodes-duplicates-linked-list/)

中的重复项替换节点

给定一个链表，其中包含一些从 1 到`n`的随机整数，并且有很多重复项。 用值`n + 1`，`n + 2`，`n + 3`等替换链表中存在的每个重复元素（以给定链表中的从左到右开始）。

**示例**：

```
Input : 1 3 1 4 4 2 1
Output : 1 3 5 4 6 2 7
Replace 2nd occurrence of 1 with 5 i.e. (4+1)
        2nd occurrence of 4 with 6 i.e. (4+2)
        3rd occurrence of 1 with 7 i.e. (4+3)

Input : 1 1 1 4 3 2 2
Output : 1 5 6 4 3 2 7

```

**方法**：

1.  遍历链表，在映射中存储链表中每个数字的频率，并找到链表中存在的最大整数，即`maxNum`。

2.  现在，再次遍历链表，如果任意数字的频率大于 1，则在第一次出现时将其值设置为 -1。

3.  这样做的原因是，在下一次出现此数字时，我们将找到它的值 -1，这意味着此数字之前已发生，请使用`maxNum + 1`更改其数据并递增`maxNum`。

下面是想法的实现。

## C++

```cpp

// C++ Program to replace duplicates  
// in an unsorted linked list 
#include <bits/stdc++.h> 
using namespace std; 

/* A linked list node */
struct Node { 
    int data; 
    struct Node* next; 
}; 

// Utility function to create a new Node 
struct Node* newNode(int data) 
{ 
    Node* temp = new Node; 
    temp->data = data; 
    temp->next = NULL; 
    return temp; 
} 

// Function to replace duplicates from a  
// linked list 
void replaceDuplicates(struct Node* head) 
{ 
    // map to store the frequency of numbers 
    unordered_map<int, int> mymap; 

    Node* temp = head; 

    // variable to store the maximum number 
    // in linked list 
    int maxNum = 0; 

    // traverse the linked list to store  
    // the frequency of every number and  
    // find the maximum integer 
    while (temp) { 
        mymap[temp->data]++; 
        if (maxNum < temp->data) 
            maxNum = temp->data; 
        temp = temp->next; 
    } 

    // Traverse again the linked list 
    while (head) { 

        // Mark the node with frequency more 
        // than 1 so that we can change the 
        // 2nd occurrence of that number 
        if (mymap[head->data] > 1) 
            mymap[head->data] = -1; 

        // -1 means number has occurred  
        // before change its value 
        else if (mymap[head->data] == -1) 
            head->data = ++maxNum; 

        head = head->next; 
    } 
} 

/* Function to print nodes in a given 
linked list */
void printList(struct Node* node) 
{ 
    while (node != NULL) { 
        printf("%d ", node->data); 
        node = node->next; 
    } 
    cout << endl; 
} 

/* Driver program to test above function */
int main() 
{ 
    /* The constructed linked list is: 
    1->3->1->4->4->2->1*/
    struct Node* head = newNode(1); 
    head->next = newNode(3); 
    head->next->next = newNode(1); 
    head->next->next->next = newNode(4); 
    head->next->next->next->next =  
                                newNode(4); 
    head->next->next->next->next-> 
                         next = newNode(2); 
    head->next->next->next->next-> 
                   next->next = newNode(1); 

    cout << "Linked list before replacing"
         << " duplicates\n"; 
    printList(head); 

    replaceDuplicates(head); 

    cout << "Linked list after replacing"
         << " duplicates\n"; 
    printList(head); 

    return 0; 
} 

```

## Java

```java

// Java implementation of the approach  
import java.util.*; 

class GFG 
{ 

// Representation of node  
static class Node  
{  
    int data;  
    Node next;  
    Node(int d) 
    { 
        data = d; 
        next = null; 
    } 
};  

// Function to insert a node at the beginning  
static Node insert(Node head, int item)  
{  
    Node temp = new Node(0);  
    temp.data = item;  
    temp.next = head;  
    head = temp; 
    return head; 
}  

// Function to replace duplicates from a  
// linked list  
static void replaceDuplicates( Node head)  
{  
    // map to store the frequency of numbers  
    Map<Integer, Integer> mymap = new HashMap<>();  

    Node temp = head;  

    // variable to store the maximum number  
    // in linked list  
    int maxNum = 0;  

    // traverse the linked list to store  
    // the frequency of every number and  
    // find the maximum integer  
    while (temp != null)  
    {  
        mymap.put(temp.data,(mymap.get(temp.data) ==  
                    null?0:mymap.get(temp.data))+1);  
        if (maxNum < temp.data)  
            maxNum = temp.data;  
        temp = temp.next;  
    }  

    // Traverse again the linked list  
    while (head != null) 
    {  

        // Mark the node with frequency more  
        // than 1 so that we can change the  
        // 2nd occurrence of that number  
        if (mymap.get(head.data) > 1)  
            mymap.put(head.data, -1);  

        // -1 means number has occurred  
        // before change its value  
        else if (mymap.get(head.data) == -1)  
            head.data = ++maxNum;  

        head = head.next;  
    }  
}  

// Function to print nodes in a given  
//linked list / 
static void printList( Node node)  
{  
    while (node != null) 
    {  
        System.out.printf("%d ", node.data);  
        node = node.next;  
    } System.out.println(); 
}  

// Driver code  
public static void main(String args[]) 
{  
    // The constructed linked list is:  
    // 1->3->1->4->4->2->1/ 
    Node head = new Node(1);  
    head.next = new Node(3);  
    head.next.next = new Node(1);  
    head.next.next.next = new Node(4);  
    head.next.next.next.next = new Node(4);  
    head.next.next.next.next.  
                        next = new Node(2);  
    head.next.next.next.next.  
                next.next = new Node(1);  

    System.out.println( "Linked list before replacing"
        + " duplicates\n");  
    printList(head);  

    replaceDuplicates(head);  

    System.out.println("Linked list after replacing"
        + " duplicates\n");  
    printList(head);  
} 
}  

// This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# implementation of the approach  
using System; 
using System.Collections.Generic; 

class GFG 
{ 

// Representation of node  
class Node  
{  
    public int data;  
    public Node next;  
    public Node(int d) 
    { 
        data = d; 
        next = null; 
    } 
};  

// Function to insert a node at the beginning  
static Node insert(Node head, int item)  
{  
    Node temp = new Node(0);  
    temp.data = item;  
    temp.next = head;  
    head = temp; 
    return head; 
}  

// Function to replace duplicates from a  
// linked list  
static void replaceDuplicates( Node head)  
{  
    // map to store the frequency of numbers  
    Dictionary<int,  
               int> mymap = new Dictionary<int,  
                                           int>(); 

    Node temp = head;  

    // variable to store the maximum number  
    // in linked list  
    int maxNum = 0;  

    // traverse the linked list to store  
    // the frequency of every number and  
    // find the maximum integer  
    while (temp != null)  
    {  
        if(mymap.ContainsKey(temp.data)) 
            mymap[temp.data] = mymap[temp.data] + 1; 
        else
            mymap.Add(temp.data, 1); 

        if (maxNum < temp.data)  
            maxNum = temp.data;  
        temp = temp.next;  
    }  

    // Traverse again the linked list  
    while (head != null) 
    {  

        // Mark the node with frequency more  
        // than 1 so that we can change the  
        // 2nd occurrence of that number  
        if (mymap[head.data] > 1)  
            mymap[head.data] = -1;  

        // -1 means number has occurred  
        // before change its value  
        else if (mymap[head.data] == -1)  
            head.data = ++maxNum;  

        head = head.next;  
    }  
}  

// Function to print nodes in a given  
// linked list 
static void printList( Node node)  
{  
    while (node != null) 
    {  
        Console.Write("{0} ", node.data);  
        node = node.next;  
    }  
}  

// Driver code  
public static void Main(String []args) 
{  

    // The constructed linked list is:  
    // 1->3->1->4->4->2->1/ 
    Node head = new Node(1);  
    head.next = new Node(3);  
    head.next.next = new Node(1);  
    head.next.next.next = new Node(4);  
    head.next.next.next.next = new Node(4);  
    head.next.next.next.next.next = new Node(2);  
    head.next.next.next.next.next.next = new Node(1);  

    Console.WriteLine("Linked list before" +  
                      " replacing duplicates");  
    printList(head);  

    replaceDuplicates(head);  

    Console.WriteLine("\nLinked list after" +  
                      " replacing duplicates");  
    printList(head);  
} 
} 

// This code is contributed by 29AjayKumar 

```

**输出**：

```
Linked list before replacing duplicates
1 3 1 4 4 2 1 
Linked list after replacing duplicates
1 3 5 4 6 2 7 

```

本文由 [**Chhavi**](https://auth.geeksforgeeks.org/profile.php?user=chhavi saini 1&list=practice) 贡献。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论。

