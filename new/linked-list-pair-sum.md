# 链表对总和

> 原文：[https://www.geeksforgeeks.org/linked-list-pair-sum/](https://www.geeksforgeeks.org/linked-list-pair-sum/)

给定一个链表和一个数字，请检查它们是否存在两个数字之和等于给定数字的数字。 如果存在两个数字，请打印它们。 如果有多个答案，请打印其中的任何一个。

**示例**：

```
Input : 1 -> 2 -> 3 -> 4 -> 5 -> NULL 
        sum = 3
Output : Pair is (1, 2)

Input : 10 -> 12 -> 31 -> 42 -> 53 -> NULL 
        sum = 15
Output : NO PAIR EXIST

```

**方法（蛮力）**

反复检查它们是否存在一对

## C++

```cpp

// CPP code to find the pair with given sum 
#include <bits/stdc++.h> 
using namespace std; 

/* Link list node */
struct Node { 
    int data; 
    struct Node* next; 
}; 

/* Given a reference (pointer to pointer) 
    to the head of a list and an int, 
    push a new node on the front  
    of the list. */
void push(struct Node** head_ref, int new_data) 
{ 
    /* allocate node */
    struct Node* new_node =  
          (struct Node*)malloc(sizeof(struct Node)); 

    /* put in the data */
    new_node->data = new_data; 

    /* link the old list off the new node */
    new_node->next = (*head_ref); 

    /* move the head to point to the new node */
    (*head_ref) = new_node; 
} 

/* Takes head pointer of the linked list and sum*/
int check_pair_sum(struct Node* head, int sum) 
{ 
    struct Node* p = head, *q; 
    while (p != NULL) { 

        q = p->next; 
        while (q != NULL) { 

           // check if both sum is equal to 
           // given sum 
           if ((p->data) + (q->data) == sum) { 
               cout << p->data << " " << q->data; 
               return true; 
           }      
           q = q->next;           
        } 

        p = p->next; 
    } 

    return 0; 
} 

/* Driver program to test above function */
int main() 
{ 
    /* Start with the empty list */
    struct Node* head = NULL; 

    /* Use push() to construct linked list*/
    push(&head, 1); 
    push(&head, 4); 
    push(&head, 1); 
    push(&head, 12); 
    push(&head, 1); 
    push(&head, 18); 
    push(&head, 47); 
    push(&head, 16); 
    push(&head, 12); 
    push(&head, 14); 

    /* function to print the result*/
    bool res = check_pair_sum(head, 26); 
    if (res == false) 
        cout << "NO PAIR EXIST"; 

    return 0; 
} 

```

## Java

```java

// Java code to find the pair with given sum 
import java.util.*; 

class GFG 
{ 

/* Link list node */
static class Node  
{ 
    int data; 
    Node next; 
}; 
static Node head; 

/* Given a reference (pointer to pointer) 
    to the head of a list and an int, 
    push a new node on the front  
    of the list. */
// Inserting node at the beginning 
static Node push(Node head_ref, int new_data) 
{ 
    /* allocate node */
    Node new_node = new Node(); 

    /* put in the data */
    new_node.data = new_data; 

    /* link the old list to the new node */
    new_node.next = head_ref; 

    /* move the head to point to the new node */
    head_ref = new_node; 
    return head=head_ref; 
} 

/* Takes head pointer of the linked list and sum*/
static boolean check_pair_sum(Node head, int sum) 
{ 
    Node p = head, q; 
    while (p != null) 
    { 
        q = p.next; 
        while (q != null)  
        { 

            // check if both sum is equal to 
            // given sum 
            if ((p.data) + (q.data) == sum)  
            { 
                System.out.print(p.data + " " + 
                                 q.data); 
                return true; 
            }      
            q = q.next;          
        } 
        p = p.next; 
    } 
    return false; 
} 

// Driver Code 
public static void main(String[] args) 
{ 
    /* Start with the empty list */
    head = null; 

    /* Use push() to conlinked list*/
    push(head, 1); 
    push(head, 4); 
    push(head, 1); 
    push(head, 12); 
    push(head, 1); 
    push(head, 18); 
    push(head, 47); 
    push(head, 16); 
    push(head, 12); 
    push(head, 14); 

    /* function to print the result*/
    boolean res = check_pair_sum(head, 26); 
    if (res == false) 
        System.out.print("NO PAIR EXIST"); 
} 
} 

// This code is contributed by 29AjayKumar 

```

## Python3

```py

# Python3 program for finding the pair with given sum 

> 原文：[https://www.geeksforgeeks.org/linked-list-pair-sum/](https://www.geeksforgeeks.org/linked-list-pair-sum/)
import math 
import sys 

# Link list node # 

> 原文：[https://www.geeksforgeeks.org/linked-list-pair-sum/](https://www.geeksforgeeks.org/linked-list-pair-sum/)
class Node: 
    def __init__(self,data): 
        self.data=data 
        self.next=None
# Given a reference (pointer to pointer) to the head  

> 原文：[https://www.geeksforgeeks.org/linked-list-pair-sum/](https://www.geeksforgeeks.org/linked-list-pair-sum/)
# of a list and an int, push a new node on the front  

> 原文：[https://www.geeksforgeeks.org/linked-list-pair-sum/](https://www.geeksforgeeks.org/linked-list-pair-sum/)
# of the list. 

> 原文：[https://www.geeksforgeeks.org/linked-list-pair-sum/](https://www.geeksforgeeks.org/linked-list-pair-sum/)

def push(head,data): 
    if head == None: 
        return Node(data) 

    # allocate node 
    temp = Node(data) 

    # link the old list off the new node  
    temp.next = head 

    # move the head to point to the new node  
    head = temp 
    return head 

# Takes head pointer of the linked list and sum 

> 原文：[https://www.geeksforgeeks.org/linked-list-pair-sum/](https://www.geeksforgeeks.org/linked-list-pair-sum/)
def check_pair_sum(head,_sum_): 
    p = head 
    q = None
    while(p): 
        q = p.next
        while(q): 
            if p.data+q.data ==_sum_: 
                print("{} {}".format(p.data,q.data)) 
                return True
            q = q.next
        p = p.next
    return False

# Driver program to test above function 

> 原文：[https://www.geeksforgeeks.org/linked-list-pair-sum/](https://www.geeksforgeeks.org/linked-list-pair-sum/)
if __name__=='__main__': 

    # Start with the empty list 
    head = None

    # Use push() to construct linked list  
    head = push(head,1) 
    head = push(head,4) 
    head = push(head,1) 
    head = push(head,12) 
    head = push(head,1) 
    head = push(head,18) 
    head = push(head,47) 
    head = push(head,16) 
    head = push(head,12) 
    head = push(head,14) 

    # function to print the result 
    res = check_pair_sum(head,26) 
    if (res == False): 
        print("NO PAIR EXIST") 

# This code is contributed by Vikash Kumar 37 

> 原文：[https://www.geeksforgeeks.org/linked-list-pair-sum/](https://www.geeksforgeeks.org/linked-list-pair-sum/)

```

## C#

```cs

// C# code to find the pair with given sum 
using System; 

class GFG 
{ 

/* Link list node */
public class Node  
{ 
    public int data; 
    public Node next; 
}; 
static Node head; 

/* Given a reference (pointer to pointer) 
    to the head of a list and an int, 
    push a new node on the front  
    of the list. */

// Inserting node at the beginning 
static Node push(Node head_ref, int new_data) 
{ 
    /* allocate node */
    Node new_node = new Node(); 

    /* put in the data */
    new_node.data = new_data; 

    /* link the old list to the new node */
    new_node.next = head_ref; 

    /* move the head to point to the new node */
    head_ref = new_node; 
    return head=head_ref; 
} 

/* Takes head pointer of the linked list and sum*/
static Boolean check_pair_sum(Node head, int sum) 
{ 
    Node p = head, q; 
    while (p != null) 
    { 
        q = p.next; 
        while (q != null)  
        { 

            // check if both sum is equal to 
            // given sum 
            if ((p.data) + (q.data) == sum)  
            { 
                Console.Write(p.data + " " + 
                              q.data); 
                return true; 
            }      
            q = q.next;          
        } 
        p = p.next; 
    } 
    return false; 
} 

// Driver Code 
public static void Main(String[] args) 
{ 
    /* Start with the empty list */
    head = null; 

    /* Use push() to conlinked list*/
    push(head, 1); 
    push(head, 4); 
    push(head, 1); 
    push(head, 12); 
    push(head, 1); 
    push(head, 18); 
    push(head, 47); 
    push(head, 16); 
    push(head, 12); 
    push(head, 14); 

    /* function to print the result*/
    Boolean res = check_pair_sum(head, 26); 
    if (res == false) 
        Console.Write("NO PAIR EXIST"); 
} 
} 

// This code is contributed by Rajput-Ji 

```

**Output:**

```
14 12

```

时间复杂度：O（n * n）

**方法 2（使用散列）**

1.取一个散列表并将所有元素标记为零

2.迭代地将散列表中存在于链表

中的所有元素标记为 1。 。迭代查找链表的 sum-current 元素是否存在于哈希表中

## C++

```cpp

// CPP program to for finding the pair with given sum 
#include <bits/stdc++.h> 
#define MAX 100000 
using namespace std; 

/* Link list node */
struct Node { 
    int data; 
    struct Node* next; 
}; 

/* Given a reference (pointer to pointer) to the head 
    of a list and an int, push a new node on the front 
    of the list. */
void push(struct Node** head_ref, int new_data) 
{ 
    /* allocate node */
    struct Node* new_node =  
            (struct Node*)malloc(sizeof(struct Node)); 

    /* put in the data */
    new_node->data = new_data; 

    /* link the old list off the new node */
    new_node->next = (*head_ref); 

    /* move the head to point to the new node */
    (*head_ref) = new_node; 
} 

/* Takes head pointer of the linked list and sum*/
bool check_pair_sum(struct Node* head, int sum) 
{ 
    unordered_set<int> s; 

    struct Node* p = head; 
    while (p != NULL) { 
        int curr = p->data; 
        if (s.find(sum - curr) != s.end()) 
        { 
           cout << curr << " " << sum - curr; 
           return true; 
        } 
        s.insert(p->data); 
        p = p->next; 
    } 

    return false; 
} 

/* Driver program to test above function*/
int main() 
{ 
    /* Start with the empty list */
    struct Node* head = NULL; 

    /* Use push() to construct linked list */
    push(&head, 1); 
    push(&head, 4); 
    push(&head, 1); 
    push(&head, 12); 
    push(&head, 1); 
    push(&head, 18); 
    push(&head, 47); 
    push(&head, 16); 
    push(&head, 12); 
    push(&head, 14); 

    /* function to print the result*/
    bool res = check_pair_sum(head, 26); 
    if (res == false) 
        cout << "NO PAIR EXIST"; 

    return 0; 
} 

```

## Java

```java

// Java program for finding  
// the pair with given sum 
import java.util.*; 
class GFG  
{  
static int MAX = 100000; 

/* Link list node */
static class Node  
{ 
    int data; 
    Node next; 
}; 

static Node head; 

/* Given a reference (pointer to pointer)  
to the head of a list and an int,  
push a new node on the front of the list. */
static void push(Node head_ref, int new_data) 
{ 
    /* allocate node */
    Node new_node = new Node(); 

    /* put in the data */
    new_node.data = new_data; 

    /* link the old list off the new node */
    new_node.next = head_ref; 

    /* move the head to point to the new node */
    head_ref = new_node; 
    head = head_ref; 
} 

/* Takes head pointer of the linked list and sum*/
static boolean check_pair_sum(Node head, int sum) 
{ 
    HashSet<Integer> s = new HashSet<Integer>(); 

    Node p = head; 
    while (p != null) 
    { 
        int curr = p.data; 
        if (s.contains(sum - curr)) 
        { 
            System.out.print(curr + " " + 
                            (sum - curr)); 
            return true; 
        } 
        s.add(p.data); 
        p = p.next; 
    } 

    return false; 
} 

// Driver Code 
public static void main(String[] args)  
{ 

    /* Start with the empty list */
    head = null; 

    /* Use push() to conlinked list */
    push(head, 1); 
    push(head, 4); 
    push(head, 1); 
    push(head, 12); 
    push(head, 1); 
    push(head, 18); 
    push(head, 47); 
    push(head, 16); 
    push(head, 12); 
    push(head, 14); 

    /* function to print the result*/
    boolean res = check_pair_sum(head, 26); 
    if (res == false) 
        System.out.print("NO PAIR EXIST"); 
} 
} 

// This code is contributed by PrinciRaj1992  

```

## C#

```cs

// C# program for finding  
// the pair with given sum 
using System; 
using System.Collections.Generic; 

class GFG  
{  
static int MAX = 100000; 

/* Link list node */
public class Node  
{ 
    public int data; 
    public Node next; 
}; 

static Node head; 

/* Given a reference (pointer to pointer)  
to the head of a list and an int,  
push a new node on the front of the list. */
static void push(Node head_ref, int new_data) 
{ 
    /* allocate node */
    Node new_node = new Node(); 

    /* put in the data */
    new_node.data = new_data; 

    /* link the old list off the new node */
    new_node.next = head_ref; 

    /* move the head to point to the new node */
    head_ref = new_node; 
    head = head_ref; 
} 

/* Takes head pointer of the linked list and sum*/
static Boolean check_pair_sum(Node head, int sum) 
{ 
    HashSet<int> s = new HashSet<int>(); 

    Node p = head; 
    while (p != null) 
    { 
        int curr = p.data; 
        if (s.Contains(sum - curr)) 
        { 
            Console.Write(curr + " " + 
                         (sum - curr)); 
            return true; 
        } 
        s.Add(p.data); 
        p = p.next; 
    } 
    return false; 
} 

// Driver Code 
public static void Main(String[] args)  
{ 

    /* Start with the empty list */
    head = null; 

    /* Use push() to conlinked list */
    push(head, 1); 
    push(head, 4); 
    push(head, 1); 
    push(head, 12); 
    push(head, 1); 
    push(head, 18); 
    push(head, 47); 
    push(head, 16); 
    push(head, 12); 
    push(head, 14); 

    /* function to print the result*/
    Boolean res = check_pair_sum(head, 26); 
    if (res == false) 
        Console.Write("NO PAIR EXIST"); 
} 
} 

// This code is contributed by Princi Singh 

```

**Output:**

```
14 12

```

时间复杂度：O（n）

辅助空间：O（n）



* * *

* * *



