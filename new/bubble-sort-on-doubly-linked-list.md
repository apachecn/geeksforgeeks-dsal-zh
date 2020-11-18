# 气泡在双链表

上排序

使用[冒泡排序](http://www.geeksforgeeks.org/bubble-sort/)对给定的双向链表进行排序。
示例：

```
Input :  5  4  3  2  1
Output : 1  2  3  4  5

Input : 2  1  3  5  4
Output :1  2  3  4  5

```

#### 说明

像在冒泡排序中一样，这里我们还要检查两个相邻节点的元素是否按升序排列，如果不是，则交换该元素。 我们这样做直到每个元素都达到其原始位置。

在第一遍中，最大元素获得其原始位置，在第二遍中，第二大元素获得其原始位置，而在第三遍中，第三大元素获得其原始位置，依此类推。
最后整个列表被排序。

注意：如果列表已经排序，则只能进行一次通过。

## C++

```cpp

// CPP program to sort a doubly linked list using 
// bubble sort 
#include <iostream> 
using namespace std; 

// structure of a node 
struct Node { 
    int data; 
    Node* prev; 
    Node* next; 
}; 

/* Function to insert a node at the beginning of a linked list */
void insertAtTheBegin(struct Node **start_ref, int data) 
{ 
    struct Node *ptr1 = new Node; 
    ptr1->data = data; 
    ptr1->next = *start_ref; 
    if (*start_ref != NULL) 
       (*start_ref)->prev = ptr1; 
    *start_ref = ptr1; 
} 

/* Function to print nodes in a given linked list */
void printList(struct Node *start) 
{ 
    struct Node *temp = start; 
    cout << endl; 
    while (temp!=NULL) 
    { 
        cout << temp->data << " "; 
        temp = temp->next; 
    } 
} 

/* Bubble sort the given linked list */
void bubbleSort(struct Node *start) 
{ 
    int swapped, i; 
    struct Node *ptr1; 
    struct Node *lptr = NULL; 

    /* Checking for empty list */
    if (start == NULL) 
        return; 

    do
    { 
        swapped = 0; 
        ptr1 = start; 

        while (ptr1->next != lptr) 
        { 
            if (ptr1->data > ptr1->next->data) 
            {  
                swap(ptr1->data, ptr1->next->data); 
                swapped = 1; 
            } 
            ptr1 = ptr1->next; 
        } 
        lptr = ptr1; 
    } 
    while (swapped); 
} 

int main() 
{ 
    int arr[] = {12, 56, 2, 11, 1, 90}; 
    int list_size, i; 

    /* start with empty linked list */
    struct Node *start = NULL; 

    /* Create linked list from the array arr[]. 
      Created linked list will be 1->11->2->56->12 */
    for (i = 0; i< 6; i++) 
        insertAtTheBegin(&start, arr[i]); 

    /* print list before sorting */
    printf("\n Linked list before sorting "); 
    printList(start); 

    /* sort the linked list */
    bubbleSort(start); 

    /* print list after sorting */
    printf("\n Linked list after sorting "); 
    printList(start); 

    return 0; 
} 

```

## Java

```java

// Java program to sort a doubly linked list using  
// bubble sort  
class GFG 
{ 

// structure of a node  
static class Node 
{  
    int data;  
    Node prev;  
    Node next;  
};  

// Function to insert a node at the beginning of a linked list  
static Node insertAtTheBegin( Node start_ref, int data)  
{  
    Node ptr1 = new Node();  
    ptr1.data = data;  
    ptr1.next = start_ref;  
    if (start_ref != null)  
    (start_ref).prev = ptr1;  
    start_ref = ptr1; 
    return start_ref; 
}  

// Function to print nodes in a given linked list  
static void printList( Node start)  
{  
    Node temp = start;  
    System.out.println();  
    while (temp != null)  
    {  
        System.out.print( temp.data + " ");  
        temp = temp.next;  
    }  
}  

// Bubble sort the given linked list  
static Node bubbleSort( Node start)  
{  
    int swapped, i;  
    Node ptr1;  
    Node lptr = null;  

    // Checking for empty list  
    if (start == null)  
        return null;  

    do
    {  
        swapped = 0;  
        ptr1 = start;  

        while (ptr1.next != lptr)  
        {  
            if (ptr1.data > ptr1.next.data)  
            {  
                int t = ptr1.data; 
                ptr1.data = ptr1.next.data; 
                ptr1.next.data = t; 
                swapped = 1;  
            }  
            ptr1 = ptr1.next;  
        }  
        lptr = ptr1;  
    }  
    while (swapped != 0);  
        return start; 
}  

// Driver code 
public static void main(String args[]) 
{  
    int arr[] = {12, 56, 2, 11, 1, 90};  
    int list_size, i;  

    // start with empty linked list  
    Node start = null;  

    // Create linked list from the array arr[].  
    //Created linked list will be 1->11->2->56->12  
    for (i = 0; i < 6; i++)  
        start=insertAtTheBegin(start, arr[i]);  

    // print list before sorting  
    System.out.printf("\n Linked list before sorting ");  
    printList(start);  

    // sort the linked list  
    start = bubbleSort(start);  

    // print list after sorting  
    System.out.printf("\n Linked list after sorting ");  
    printList(start);  
}  
}  

// This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# program to sort a doubly linked list using  
// bubble sort  
using System; 

class GFG 
{ 

// structure of a node  
public class Node 
{  
    public int data;  
    public Node prev;  
    public Node next;  
};  

// Function to insert a node at the beginning of a linked list  
static Node insertAtTheBegin( Node start_ref, int data)  
{  
    Node ptr1 = new Node();  
    ptr1.data = data;  
    ptr1.next = start_ref;  
    if (start_ref != null)  
    (start_ref).prev = ptr1;  
    start_ref = ptr1; 
    return start_ref; 
}  

// Function to print nodes in a given linked list  
static void printList( Node start)  
{  
    Node temp = start;  
    Console.WriteLine();  
    while (temp != null)  
    {  
        Console.Write( temp.data + " ");  
        temp = temp.next;  
    }  
}  

// Bubble sort the given linked list  
static Node bubbleSort( Node start)  
{  
    int swapped;  
    Node ptr1;  
    Node lptr = null;  

    // Checking for empty list  
    if (start == null)  
        return null;  

    do
    {  
        swapped = 0;  
        ptr1 = start;  

        while (ptr1.next != lptr)  
        {  
            if (ptr1.data > ptr1.next.data)  
            {  
                int t = ptr1.data; 
                ptr1.data = ptr1.next.data; 
                ptr1.next.data = t; 
                swapped = 1;  
            }  
            ptr1 = ptr1.next;  
        }  
        lptr = ptr1;  
    }  
    while (swapped != 0);  
        return start; 
}  

// Driver code 
public static void Main(String []args) 
{  
    int []arr = {12, 56, 2, 11, 1, 90};  
    int i;  

    // start with empty linked list  
    Node start = null;  

    // Create linked list from the array arr[].  
    //Created linked list will be 1->11->2->56->12  
    for (i = 0; i < 6; i++)  
        start=insertAtTheBegin(start, arr[i]);  

    // print list before sorting  
    Console.Write("\n Linked list before sorting ");  
    printList(start);  

    // sort the linked list  
    start = bubbleSort(start);  

    // print list after sorting  
    Console.Write("\n Linked list after sorting ");  
    printList(start);  
}  
}  

// This code contributed by Rajput-Ji 

```

**Output:**

```
Linked list before sorting 
90 1 11 2 56 12 
 Linked list after sorting 
1 2 11 12 56 90

```



* * *

* * *

如果您喜欢GeeksforGeeks并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至tribution@geeksforgeeks.org。 查看您的文章出现在GeeksforGeeks主页上，并帮助其他Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。