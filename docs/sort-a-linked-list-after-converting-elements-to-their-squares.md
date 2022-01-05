# 将元素转换成方块后对链表进行排序

> 原文:[https://www . geeksforgeeks . org/sort-a-将元素转换为它们的方块后的链表/](https://www.geeksforgeeks.org/sort-a-linked-list-after-converting-elements-to-their-squares/)

给定一个非递减的[链表](https://www.geeksforgeeks.org/data-structures/linked-list/)。任务是在不使用任何额外的**空间的情况下，**将链表的元素排列成**排序的**顺序。****

****示例**:**

> ****输入**:1->2->3->4->5
> **输出**:1->4->9->16->25**
> 
> ****输入**:(-2)->(-1)->0->1->2
> **输出**:0->1->1->4->4**

****对于数组:**在本文中讨论了如何对数组进行同样的操作–[在将元素转换为正方形后对数组进行排序](https://www.geeksforgeeks.org/sort-array-converting-elements-squares/)**

****逼近**:任务可以通过**将**给定的列表从转换点(负向正)划分为两个不同的链表来解决，一个只包含负元素的链表表示“ **l1** ，另一个包含正元素的链表表示“ **l2** ”。将列表 **l1** 和[的所有元素进行平方，将其反转](https://www.geeksforgeeks.org/reverse-a-linked-list/)，同时将列表 **l2、**现在[的所有元素进行平方，合并两个排序列表](https://www.geeksforgeeks.org/merge-two-sorted-linked-lists/)得到结果列表。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

struct Node {
    int data;
    Node* next;
    Node(int data)
    {
        this->data = data;
        this->next = NULL;
    }
};

// Utility function to make linked list
Node* makeList(int n, int arr[])
{
    Node* h = NULL;
    Node* root;
    for (int i = 0; i < n; i++) {
        int data = arr[i];

        Node* node = new Node(data);

        if (h == NULL) {
            h = node;
            root = h;
        }
        else {
            root->next = node;
            root = node;
        }
    }
    return h;
}

// Utitlity function to print list
void print_list(Node* head)
{
    while (head != NULL) {
        cout << head->data << " ";
        head = head->next;
    }
    cout << "\n";
}

// Function to reverse the linked list
Node* reverse(Node* head)
{
    // Initialize current, previous and
    // next pointers
    Node* current = head;
    Node *prev = NULL, *next = NULL;

    while (current != NULL) {
        // Store next
        next = current->next;

        // Reverse current node's pointer
        current->next = prev;

        // Move pointers one position ahead.
        prev = current;
        current = next;
    }
    head = prev;
    return head;
}

// This function will find the point of transition
// where elements switch from negative to positive
// and return that point
Node* findBreakPoint(Node* head)
{
    if (head == NULL) {
        return NULL;
    }

    Node *prev = NULL, *curr = head;

    while (curr != NULL) {
        prev = curr;
        curr = curr->next;

        if (curr != NULL) {
            // If prev element is negative and
            // current element is positive
            if ((prev->data) < 0
                and (curr->data) >= 0) {

                return prev;
            }
        }
    }

    // Checking if list contains
    // only negative elements
    curr = head;
    while (curr->next) {
        if (curr->data < 0) {
            curr = curr->next;
            continue;
        }
        else {
            // Contains positve elements
            return NULL;
        }
    }

    // Contains only negative element
    // so returning the last element of the list
    return curr;
}

// Utility function to merge two sorted lists
struct Node* mergeUtil(struct Node* h1,
                       struct Node* h2)
{
    // If only one node in first list
    // simply point its head to second list
    if (!h1->next) {
        h1->next = h2;
        return h1;
    }

    // Initialize current and next pointers of
    // both lists
    struct Node *curr1 = h1, *next1 = h1->next;
    struct Node *curr2 = h2, *next2 = h2->next;

    while (next1 && curr2) {
        // If curr2 lies in between
        // curr1 and next1
        // then do curr1->curr2->next1
        if ((curr2->data) >= (curr1->data)
            && (curr2->data) <= (next1->data)) {
            next2 = curr2->next;
            curr1->next = curr2;
            curr2->next = next1;

            // Let curr1 and curr2 to point
            // their immediate next pointers
            curr1 = curr2;
            curr2 = next2;
        }
        else {
            // If more nodes in first list
            if (next1->next) {
                next1 = next1->next;
                curr1 = curr1->next;
            }

            // Else point the last
            // node of first list
            // to the remaining
            // nodes of second list
            else {
                next1->next = curr2;
                return h1;
            }
        }
    }
    return h1;
}

// Merges two given lists in-place.
// This function mainly compares
// head nodes and calls mergeUtil()
struct Node* merge(struct Node* h1,
                   struct Node* h2)
{
    if (!h1)
        return h2;
    if (!h2)
        return h1;

    // Start with the linked list
    // whose head data is the least
    if (h1->data < h2->data)
        return mergeUtil(h1, h2);
    else
        return mergeUtil(h2, h1);
}

// Function to return resultant squared list
Node* squaresList(Node* head)
{
    if (head == NULL)
        return NULL;

    Node* mid = findBreakPoint(head);

    Node* temp = head;
    while (temp != NULL) {
        temp->data *= temp->data;
        temp = temp->next;
    }

    // List contains only positive elements
    if (mid == NULL) {
        return head;
    }

    // List contains both positive
    // and negative elements
    Node* h1 = head;
    Node* h2 = mid->next;

    // Breaking the list where negative
    // switches to positive
    mid->next = NULL;

    // Reversing the list
    h1 = reverse(h1);

    // Merging the two lists
    Node* ans = merge(h1, h2);

    return ans;
}

// Driver Program
int main()
{

    int n = 7;
    int arr1[] = { 1, 2, 3, 4, 5 };
    Node* head = makeList(sizeof(arr1)
                              / sizeof(int),
                          arr1);

    n = 6;
    int arr2[] = { -2, -1, 0, 1, 2 };
    head = makeList(sizeof(arr2)
                        / sizeof(int),
                    arr2);

    int arr3[] = { -5, -4, -3, -2, -1 };
    head = makeList(sizeof(arr3)
                        / sizeof(int),
                    arr3);
    print_list(squaresList(head));
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
import java.util.*;

class GFG{

static class Node {
    int data;
    Node next;
    Node(int data)
    {
        this.data = data;
        this.next = null;
    }
    public Node() {
        // TODO Auto-generated constructor stub
    }
};

// Utility function to make linked list
static Node makeList(int n, int arr[])
{
    Node h = null;
    Node root = new Node();
    for (int i = 0; i < n; i++) {
        int data = arr[i];

        Node node = new Node(data);

        if (h == null) {
            h = node;
            root = h;
        }
        else {
            root.next = node;
            root = node;
        }
    }
    return h;
}

// Utitlity function to print list
static void print_list(Node head)
{
    while (head != null) {
        System.out.print(head.data+ " ");
        head = head.next;
    }
    System.out.print("\n");
}

// Function to reverse the linked list
static Node reverse(Node head)
{
    // Initialize current, previous and
    // next pointers
    Node current = head;
    Node prev = null, next = null;

    while (current != null) {
        // Store next
        next = current.next;

        // Reverse current node's pointer
        current.next = prev;

        // Move pointers one position ahead.
        prev = current;
        current = next;
    }
    head = prev;
    return head;
}

// This function will find the point of transition
// where elements switch from negative to positive
// and return that point
static Node findBreakPoint(Node head)
{
    if (head == null) {
        return null;
    }

    Node prev = null, curr = head;

    while (curr != null) {
        prev = curr;
        curr = curr.next;

        if (curr != null) {
            // If prev element is negative and
            // current element is positive
            if ((prev.data) < 0
                && (curr.data) >= 0) {

                return prev;
            }
        }
    }

    // Checking if list contains
    // only negative elements
    curr = head;
    while (curr.next!=null) {
        if (curr.data < 0) {
            curr = curr.next;
            continue;
        }
        else {
            // Contains positve elements
            return null;
        }
    }

    // Contains only negative element
    // so returning the last element of the list
    return curr;
}

// Utility function to merge two sorted lists
static Node mergeUtil(Node h1,
                       Node h2)
{
    // If only one node in first list
    // simply point its head to second list
    if (h1.next!=null) {
        h1.next = h2;
        return h1;
    }

    // Initialize current and next pointers of
    // both lists
    Node curr1 = h1, next1 = h1.next;
    Node curr2 = h2, next2 = h2.next;

    while (next1!=null && curr2!=null) {
        // If curr2 lies in between
        // curr1 and next1
        // then do curr1.curr2.next1
        if ((curr2.data) >= (curr1.data)
            && (curr2.data) <= (next1.data)) {
            next2 = curr2.next;
            curr1.next = curr2;
            curr2.next = next1;

            // Let curr1 and curr2 to point
            // their immediate next pointers
            curr1 = curr2;
            curr2 = next2;
        }
        else {
            // If more nodes in first list
            if (next1.next!=null) {
                next1 = next1.next;
                curr1 = curr1.next;
            }

            // Else point the last
            // node of first list
            // to the remaining
            // nodes of second list
            else {
                next1.next = curr2;
                return h1;
            }
        }
    }
    return h1;
}

// Merges two given lists in-place.
// This function mainly compares
// head nodes and calls mergeUtil()
static Node merge(Node h1,
                   Node h2)
{
    if (h1==null)
        return h2;
    if (h2==null)
        return h1;

    // Start with the linked list
    // whose head data is the least
    if (h1.data < h2.data)
        return mergeUtil(h1, h2);
    else
        return mergeUtil(h2, h1);
}

// Function to return resultant squared list
static Node squaresList(Node head)
{
    if (head == null)
        return null;

    Node mid = findBreakPoint(head);

    Node temp = head;
    while (temp != null) {
        temp.data *= temp.data;
        temp = temp.next;
    }

    // List contains only positive elements
    if (mid == null) {
        return head;
    }

    // List contains both positive
    // and negative elements
    Node h1 = head;
    Node h2 = mid.next;

    // Breaking the list where negative
    // switches to positive
    mid.next = null;

    // Reversing the list
    h1 = reverse(h1);

    // Merging the two lists
    Node ans = merge(h1, h2);

    return ans;
}

// Driver Program
public static void main(String[] args)
{

    int n = 7;
    int arr1[] = { 1, 2, 3, 4, 5 };
    Node head = makeList(arr1.length,
                          arr1);

    n = 6;
    int arr2[] = { -2, -1, 0, 1, 2 };
    head = makeList(arr2.length,
                    arr2);

    int arr3[] = { -5, -4, -3, -2, -1 };
    head = makeList(arr3.length,
                    arr3);
    print_list(squaresList(head));
}
}

// This code is contributed by 29AjayKumar
```

## **java 描述语言**

```
<script>

       // JavaScript Program to implement
       // the above approach
       class Node {

           constructor(data) {
               this.data = data;
               this.next = null;
           }
       }

       // Utility function to make linked list
       function makeList(n, arr) {
           let h = null;
           let root;
           for (let i = 0; i < n; i++) {
               let data = arr[i];

               let node = new Node(data);

               if (h == null) {
                   h = node;
                   root = h;
               }
               else {
                   root.next = node;
                   root = node;
               }
           }
           return h;
       }

       // Utitlity function to print list
       function print_list(head) {
           while (head != null) {
               document.write(head.data + " ")
               head = head.next;
           }
           document.write("<br>")
       }

       // Function to reverse the linked list
       function reverse(head)
       {

           // Initialize current, previous and
           // next pointers
           let current = head;
           let prev = null, next = null;

           while (current != null) {
               // Store next
               next = current.next;

               // Reverse current node's pointer
               current.next = prev;

               // Move pointers one position ahead.
               prev = current;
               current = next;
           }
           head = prev;
           return head;
       }

       // This function will find the point of transition
       // where elements switch from negative to positive
       // and return that point
       function findBreakPoint(head) {
           if (head == null) {
               return null;
           }

           let prev = null, curr = head;

           while (curr != null) {
               prev = curr;
               curr = curr.next;

               if (curr != null) {
                   // If prev element is negative and
                   // current element is positive
                   if ((prev.data) < 0
                       && (curr.data) >= 0) {

                       return prev;
                   }
               }
           }

           // Checking if list contains
           // only negative elements
           curr = head;
           while (curr.next) {
               if (curr.data < 0) {
                   curr = curr.next;
                   continue;
               }
               else {
                   // Contains positve elements
                   return null;
               }
           }

           // Contains only negative element
           // so returning the last element of the list
           return curr;
       }

       // Utility function to merge two sorted lists
       function mergeUtil(h1,
           h2) {
           // If only one node in first list
           // simply point its head to second list
           if (!h1.next) {
               h1.next = h2;
               return h1;
           }

           // Initialize current and next pointers of
           // both lists
           let curr1 = h1, next1 = h1.next;
           let curr2 = h2, next2 = h2.next;

           while (next1 && curr2) {
               // If curr2 lies in between
               // curr1 and next1
               // then do curr1.curr2.next1
               if ((curr2.data) >= (curr1.data)
                   && (curr2.data) <= (next1.data)) {
                   next2 = curr2.next;
                   curr1.next = curr2;
                   curr2.next = next1;

                   // Let curr1 and curr2 to point
                   // their immediate next pointers
                   curr1 = curr2;
                   curr2 = next2;
               }
               else {
                   // If more nodes in first list
                   if (next1.next) {
                       next1 = next1.next;
                       curr1 = curr1.next;
                   }

                   // Else point the last
                   // node of first list
                   // to the remaining
                   // nodes of second list
                   else {
                       next1.next = curr2;
                       return h1;
                   }
               }
           }
           return h1;
       }

       // Merges two given lists in-place.
       // This function mainly compares
       // head nodes and calls mergeUtil()
       function merge(h1,
           h2) {
           if (!h1)
               return h2;
           if (!h2)
               return h1;

           // Start with the linked list
           // whose head data is the least
           if (h1.data < h2.data)
               return mergeUtil(h1, h2);
           else
               return mergeUtil(h2, h1);
       }

       // Function to return resultant squared list
       function squaresList(head) {
           if (head == null)
               return null;

           let mid = findBreakPoint(head);

           let temp = head;
           while (temp != null) {
               temp.data *= temp.data;
               temp = temp.next;
           }

           // List contains only positive elements
           if (mid == null) {
               return head;
           }

           // List contains both positive
           // and negative elements
           let h1 = head;
           let h2 = mid.next;

           // Breaking the list where negative
           // switches to positive
           mid.next = null;

           // Reversing the list
           h1 = reverse(h1);

           // Merging the two lists
           let ans = merge(h1, h2);

           return ans;
       }

       // Driver Program

       let n = 7;
       let arr1 = [1, 2, 3, 4, 5];
       let head = makeList(arr1.length, arr1);

       n = 6;
       let arr2 = [-2, -1, 0, 1, 2];
       head = makeList(arr2.length,
           arr2);

       let arr3 = [-5, -4, -3, -2, -1];
       head = makeList(arr3.length,
           arr3);
       print_list(squaresList(head));

   // This code is contributed by Potta Lokesh
   </script>
```

## **C#**

```
// C# program for the above approach
using System;

public class GFG{

class Node {
    public int data;
    public Node next;
    public Node(int data)
    {
        this.data = data;
        this.next = null;
    }
    public Node() {
        // TODO Auto-generated constructor stub
    }
};

// Utility function to make linked list
static Node makeList(int n, int []arr)
{
    Node h = null;
    Node root = new Node();
    for (int i = 0; i < n; i++) {
        int data = arr[i];

        Node node = new Node(data);

        if (h == null) {
            h = node;
            root = h;
        }
        else {
            root.next = node;
            root = node;
        }
    }
    return h;
}

// Utitlity function to print list
static void print_list(Node head)
{
    while (head != null) {
        Console.Write(head.data+ " ");
        head = head.next;
    }
    Console.Write("\n");
}

// Function to reverse the linked list
static Node reverse(Node head)
{
    // Initialize current, previous and
    // next pointers
    Node current = head;
    Node prev = null, next = null;

    while (current != null) {
        // Store next
        next = current.next;

        // Reverse current node's pointer
        current.next = prev;

        // Move pointers one position ahead.
        prev = current;
        current = next;
    }
    head = prev;
    return head;
}

// This function will find the point of transition
// where elements switch from negative to positive
// and return that point
static Node findBreakPoint(Node head)
{
    if (head == null) {
        return null;
    }

    Node prev = null, curr = head;

    while (curr != null) {
        prev = curr;
        curr = curr.next;

        if (curr != null) {
            // If prev element is negative and
            // current element is positive
            if ((prev.data) < 0
                && (curr.data) >= 0) {

                return prev;
            }
        }
    }

    // Checking if list contains
    // only negative elements
    curr = head;
    while (curr.next!=null) {
        if (curr.data < 0) {
            curr = curr.next;
            continue;
        }
        else {
            // Contains positve elements
            return null;
        }
    }

    // Contains only negative element
    // so returning the last element of the list
    return curr;
}

// Utility function to merge two sorted lists
static Node mergeUtil(Node h1,
                       Node h2)
{
    // If only one node in first list
    // simply point its head to second list
    if (h1.next!=null) {
        h1.next = h2;
        return h1;
    }

    // Initialize current and next pointers of
    // both lists
    Node curr1 = h1, next1 = h1.next;
    Node curr2 = h2, next2 = h2.next;

    while (next1!=null && curr2!=null) {
        // If curr2 lies in between
        // curr1 and next1
        // then do curr1.curr2.next1
        if ((curr2.data) >= (curr1.data)
            && (curr2.data) <= (next1.data)) {
            next2 = curr2.next;
            curr1.next = curr2;
            curr2.next = next1;

            // Let curr1 and curr2 to point
            // their immediate next pointers
            curr1 = curr2;
            curr2 = next2;
        }
        else {
            // If more nodes in first list
            if (next1.next!=null) {
                next1 = next1.next;
                curr1 = curr1.next;
            }

            // Else point the last
            // node of first list
            // to the remaining
            // nodes of second list
            else {
                next1.next = curr2;
                return h1;
            }
        }
    }
    return h1;
}

// Merges two given lists in-place.
// This function mainly compares
// head nodes and calls mergeUtil()
static Node merge(Node h1,
                   Node h2)
{
    if (h1==null)
        return h2;
    if (h2==null)
        return h1;

    // Start with the linked list
    // whose head data is the least
    if (h1.data < h2.data)
        return mergeUtil(h1, h2);
    else
        return mergeUtil(h2, h1);
}

// Function to return resultant squared list
static Node squaresList(Node head)
{
    if (head == null)
        return null;

    Node mid = findBreakPoint(head);

    Node temp = head;
    while (temp != null) {
        temp.data *= temp.data;
        temp = temp.next;
    }

    // List contains only positive elements
    if (mid == null) {
        return head;
    }

    // List contains both positive
    // and negative elements
    Node h1 = head;
    Node h2 = mid.next;

    // Breaking the list where negative
    // switches to positive
    mid.next = null;

    // Reversing the list
    h1 = reverse(h1);

    // Merging the two lists
    Node ans = merge(h1, h2);

    return ans;
}

// Driver Program
public static void Main(String[] args)
{

    int n = 7;
    int []arr1 = { 1, 2, 3, 4, 5 };
    Node head = makeList(arr1.Length,
                          arr1);

    n = 6;
    int []arr2 = { -2, -1, 0, 1, 2 };
    head = makeList(arr2.Length,
                    arr2);

    int []arr3 = { -5, -4, -3, -2, -1 };
    head = makeList(arr3.Length,
                    arr3);
    print_list(squaresList(head));
}
}

// This code is contributed by 29AjayKumar
```

****Output**

```
1 4 9 16 25 
```** 

*****时间复杂度*** : O(N)，N 为节点数
***辅助空间*** : O(1)**