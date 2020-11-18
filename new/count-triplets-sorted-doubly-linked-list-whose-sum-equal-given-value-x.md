# 计数一个排序的双向链表中的三元组，其总数等于给定值x

给定一个不同节点的排序双链表（没有两个节点具有相同的数据），值 **x** 。 计算列表中的三元组，它们总计为给定值 **x** 。

例子：

![](img/2d05e5e01ed336aac98a3382928d97bf.png)

**方法1（朴素方法）：**
使用三个嵌套循环生成所有三元组，并检查三元组中的元素总和是否为 **x** 。

## C++

```cpp

// C++ implementation to count triplets in a sorted doubly linked list 
// whose sum is equal to a given value 'x' 
#include <bits/stdc++.h> 

using namespace std; 

// structure of node of doubly linked list 
struct Node { 
    int data; 
    struct Node* next, *prev; 
}; 

// function to count triplets in a sorted doubly linked list 
// whose sum is equal to a given value 'x' 
int countTriplets(struct Node* head, int x) 
{ 
    struct Node* ptr1, *ptr2, *ptr3; 
    int count = 0; 

    // generate all possible triplets 
    for (ptr1 = head; ptr1 != NULL; ptr1 = ptr1->next) 
        for (ptr2 = ptr1->next; ptr2 != NULL; ptr2 = ptr2->next) 
            for (ptr3 = ptr2->next; ptr3 != NULL; ptr3 = ptr3->next) 

                // if elements in the current triplet sum up to 'x' 
                if ((ptr1->data + ptr2->data + ptr3->data) == x) 

                    // increment count 
                    count++; 

    // required count of triplets 
    return count; 
} 

// A utility function to insert a new node at the 
// beginning of doubly linked list 
void insert(struct Node** head, int data) 
{ 
    // allocate node 
    struct Node* temp = new Node(); 

    // put in the data 
    temp->data = data; 
    temp->next = temp->prev = NULL; 

    if ((*head) == NULL) 
        (*head) = temp; 
    else { 
        temp->next = *head; 
        (*head)->prev = temp; 
        (*head) = temp; 
    } 
} 

// Driver program to test above 
int main() 
{ 
    // start with an empty doubly linked list 
    struct Node* head = NULL; 

    // insert values in sorted order 
    insert(&head, 9); 
    insert(&head, 8); 
    insert(&head, 6); 
    insert(&head, 5); 
    insert(&head, 4); 
    insert(&head, 2); 
    insert(&head, 1); 

    int x = 17; 

    cout << "Count = "
         << countTriplets(head, x); 
    return 0; 
} 

```

## Java

```java

// Java implementation to count triplets 
// in a sorted doubly linked list  
// whose sum is equal to a given value 'x'  
import java.io.*; 
import java.util.*; 

// Represents node of a doubly linked list 
class Node  
{ 
    int data; 
    Node prev, next; 
    Node(int val) 
    { 
        data = val;  
        prev = null; 
        next = null; 
    } 
} 

class GFG  
{ 

    // function to count triplets in  
    // a sorted doubly linked list  
    // whose sum is equal to a given value 'x'  
    static int countTriplets(Node head, int x) 
    { 
            Node ptr1, ptr2, ptr3; 
            int count = 0; 

            // generate all possible triplets  
            for (ptr1 = head; ptr1 != null; ptr1 = ptr1.next) 
                for (ptr2 = ptr1.next; ptr2 != null; ptr2 = ptr2.next) 
                    for (ptr3 = ptr2.next; ptr3 != null; ptr3 = ptr3.next) 

                        // if elements in the current triplet sum up to 'x'  
                        if ((ptr1.data + ptr2.data + ptr3.data) == x) 

                            // increment count 
                            count++; 

            // required count of triplets  
            return count; 
    } 

    // A utility function to insert a new node at the  
    // beginning of doubly linked list 
    static Node insert(Node head, int val) 
    { 
            // allocate node  
            Node temp = new Node(val); 

            if (head == null) 
                head = temp; 

            else 
            { 
                temp.next = head; 
                head.prev = temp; 
                head = temp; 
            } 

            return head; 
    } 

    // Driver code 
    public static void main(String args[]) 
    { 
            // start with an empty doubly linked list 
            Node head = null; 

            // insert values in sorted order 
            head = insert(head, 9); 
            head = insert(head, 8); 
            head = insert(head, 6); 
            head = insert(head, 5); 
            head = insert(head, 4); 
            head = insert(head, 2); 
            head = insert(head, 1); 

            int x = 17; 
            System.out.println("count = " + countTriplets(head, x)); 
    } 
} 

// This code is contributed by rachana soma  

```

## Python3

```py

# Python3 implementation to count triplets 
# in a sorted doubly linked list 
# whose sum is equal to a given value 'x' 

# structure of node of doubly linked list 
class Node:  
    def __init__(self): 
        self.data = None
        self.prev = None
        self.next = None

# function to count triplets in a sorted doubly linked list 
# whose sum is equal to a given value 'x' 
def countTriplets( head, x): 

    ptr1 = head 
    ptr2 = None
    ptr3 = None
    count = 0

    # generate all possible triplets 
    while (ptr1 != None ): 
        ptr2 = ptr1.next
        while ( ptr2 != None ): 
            ptr3 = ptr2.next
            while ( ptr3 != None ): 

                # if elements in the current triplet sum up to 'x' 
                if ((ptr1.data + ptr2.data + ptr3.data) == x): 

                    # increment count 
                    count = count + 1
                ptr3 = ptr3.next
            ptr2 = ptr2.next
        ptr1 = ptr1.next

    # required count of triplets 
    return count 

# A utility function to insert a new node at the 
# beginning of doubly linked list 
def insert(head, data): 

    # allocate node 
    temp = Node() 

    # put in the data 
    temp.data = data 
    temp.next = temp.prev = None

    if ((head) == None): 
        (head) = temp 
    else : 
        temp.next = head 
        (head).prev = temp 
        (head) = temp 
    return head 

# Driver code 

# start with an empty doubly linked list 
head = None

# insert values in sorted order 
head = insert(head, 9) 
head = insert(head, 8) 
head = insert(head, 6) 
head = insert(head, 5) 
head = insert(head, 4) 
head = insert(head, 2) 
head = insert(head, 1) 

x = 17

print( "Count = ", countTriplets(head, x)) 

# This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# implementation to count triplets  
// in a sorted doubly linked list  
// whose sum is equal to a given value 'x'  
using System;  

// Represents node of a doubly linked list  
public class Node  
{  
    public int data;  
    public Node prev, next;  
    public Node(int val)  
    {  
        data = val;  
        prev = null;  
        next = null;  
    }  
}  

class GFG  
{  

    // function to count triplets in  
    // a sorted doubly linked list  
    // whose sum is equal to a given value 'x'  
    static int countTriplets(Node head, int x)  
    {  
        Node ptr1, ptr2, ptr3;  
        int count = 0;  

        // generate all possible triplets  
        for (ptr1 = head; ptr1 != null; ptr1 = ptr1.next)  
            for (ptr2 = ptr1.next; ptr2 != null; ptr2 = ptr2.next)  
                for (ptr3 = ptr2.next; ptr3 != null; ptr3 = ptr3.next)  

                    // if elements in the current triplet sum up to 'x'  
                    if ((ptr1.data + ptr2.data + ptr3.data) == x)  

                        // increment count  
                        count++;  

        // required count of triplets  
        return count;  
    }  

    // A utility function to insert a new node at the  
    // beginning of doubly linked list  
    static Node insert(Node head, int val)  
    {  
        // allocate node  
        Node temp = new Node(val);  

        if (head == null)  
            head = temp;  

        else
        {  
            temp.next = head;  
            head.prev = temp;  
            head = temp;  
        }  

        return head;  
    }  

    // Driver code  
    public static void Main(String []args)  
    {  
            // start with an empty doubly linked list  
            Node head = null;  

            // insert values in sorted order  
            head = insert(head, 9);  
            head = insert(head, 8);  
            head = insert(head, 6);  
            head = insert(head, 5);  
            head = insert(head, 4);  
            head = insert(head, 2);  
            head = insert(head, 1);  

            int x = 17;  
            Console.WriteLine("count = " + countTriplets(head, x));  
    }  
}  

// This code is contributed by Arnab Kundu 

```

**输出：**

```
Count = 2

```

**时间复杂度：** O（n <sup>3</sup> ）
**辅助空间：** O（1）

**方法2（哈希）：**
创建一个哈希表，其中**（键，值）**元组表示为**（节点数据，节点指针）元组**。 遍历双向链表，并将每个节点的数据及其指针对（元组）存储在哈希表中。 现在，生成每个可能的节点对。 对于每对节点，计算 **p_sum** （两个节点中数据的总和），并检查哈希表中是否存在**（x-p_sum）**。 如果存在，则还要验证该对中的两个节点与与哈希表中的**（x-p_sum）**关联的节点不同，并最终使**计数**递增。 返回**（计数/ 3）**，因为在上述过程中每个三​​元组被计数了3次。

## C++

```cpp

// C++ implementation to count triplets in a sorted doubly linked list 
// whose sum is equal to a given value 'x' 
#include <bits/stdc++.h> 

using namespace std; 

// structure of node of doubly linked list 
struct Node { 
    int data; 
    struct Node* next, *prev; 
}; 

// function to count triplets in a sorted doubly linked list 
// whose sum is equal to a given value 'x' 
int countTriplets(struct Node* head, int x) 
{ 
    struct Node* ptr, *ptr1, *ptr2; 
    int count = 0; 

    // unordered_map 'um' implemented as hash table 
    unordered_map<int, Node*> um; 

    // insert the <node data, node pointer> tuple in 'um' 
    for (ptr = head; ptr != NULL; ptr = ptr->next) 
        um[ptr->data] = ptr; 

    // generate all possible pairs 
    for (ptr1 = head; ptr1 != NULL; ptr1 = ptr1->next) 
        for (ptr2 = ptr1->next; ptr2 != NULL; ptr2 = ptr2->next) { 

            // p_sum - sum of elements in the current pair 
            int p_sum = ptr1->data + ptr2->data; 

            // if 'x-p_sum' is present in 'um' and either of the two nodes 
            // are not equal to the 'um[x-p_sum]' node 
            if (um.find(x - p_sum) != um.end() && um[x - p_sum] != ptr1 
                && um[x - p_sum] != ptr2) 

                // increment count 
                count++; 
        } 

    // required count of triplets 
    // division by 3 as each triplet is counted 3 times 
    return (count / 3); 
} 

// A utility function to insert a new node at the 
// beginning of doubly linked list 
void insert(struct Node** head, int data) 
{ 
    // allocate node 
    struct Node* temp = new Node(); 

    // put in the data 
    temp->data = data; 
    temp->next = temp->prev = NULL; 

    if ((*head) == NULL) 
        (*head) = temp; 
    else { 
        temp->next = *head; 
        (*head)->prev = temp; 
        (*head) = temp; 
    } 
} 

// Driver program to test above 
int main() 
{ 
    // start with an empty doubly linked list 
    struct Node* head = NULL; 

    // insert values in sorted order 
    insert(&head, 9); 
    insert(&head, 8); 
    insert(&head, 6); 
    insert(&head, 5); 
    insert(&head, 4); 
    insert(&head, 2); 
    insert(&head, 1); 

    int x = 17; 

    cout << "Count = "
         << countTriplets(head, x); 
    return 0; 
} 

```

## Java

```java

// Java implementation to count triplets in a sorted doubly linked list 
// whose sum is equal to a given value 'x' 
import java.util.*; 

class GFG{ 

// structure of node of doubly linked list 
static class Node { 
    int data; 
    Node next, prev; 
    Node(int val) 
    { 
        data = val;  
        prev = null; 
        next = null; 
    } 
}; 

// function to count triplets in a sorted doubly linked list 
// whose sum is equal to a given value 'x' 
static int countTriplets(Node head, int x) 
{ 
    Node ptr, ptr1, ptr2; 
    int count = 0; 

    // unordered_map 'um' implemented as hash table 
    HashMap<Integer,Node> um = new HashMap<Integer,Node>(); 

    // insert the <node data, node pointer> tuple in 'um' 
    for (ptr = head; ptr != null; ptr = ptr.next) 
        um.put(ptr.data, ptr); 

    // generate all possible pairs 
    for (ptr1 = head; ptr1 != null; ptr1 = ptr1.next) 
        for (ptr2 = ptr1.next; ptr2 != null; ptr2 = ptr2.next) { 

            // p_sum - sum of elements in the current pair 
            int p_sum = ptr1.data + ptr2.data; 

            // if 'x-p_sum' is present in 'um' and either of the two nodes 
            // are not equal to the 'um[x-p_sum]' node 
            if (um.containsKey(x - p_sum) && um.get(x - p_sum) != ptr1 
                && um.get(x - p_sum) != ptr2) 

                // increment count 
                count++; 
        } 

    // required count of triplets 
    // division by 3 as each triplet is counted 3 times 
    return (count / 3); 
} 

// A utility function to insert a new node at the 
// beginning of doubly linked list 
static Node insert(Node head, int val) 
{ 
        // allocate node  
        Node temp = new Node(val); 

        if (head == null) 
            head = temp; 

        else
        { 
            temp.next = head; 
            head.prev = temp; 
            head = temp; 
        } 

        return head; 
} 

// Driver program to test above 
public static void main(String[] args) 
{ 
    // start with an empty doubly linked list 
    Node head = null; 

    // insert values in sorted order 
    head = insert(head, 9); 
    head = insert(head, 8); 
    head = insert(head, 6); 
    head = insert(head, 5); 
    head = insert(head, 4); 
    head = insert(head, 2); 
    head = insert(head, 1); 

    int x = 17; 

    System.out.print("Count = "
         + countTriplets(head, x)); 
} 
} 

// This code is contributed by Rajput-Ji 

```

## C#

```cs

// C# implementation to count triplets in a sorted doubly linked list 
// whose sum is equal to a given value 'x' 
using System; 
using System.Collections.Generic; 

class GFG 
{ 

// structure of node of doubly linked list 
class Node { 
    public int data; 
    public Node next, prev; 
    public Node(int val) 
    { 
        data = val;  
        prev = null; 
        next = null; 
    } 
}; 

// function to count triplets in a sorted doubly linked list 
// whose sum is equal to a given value 'x' 
static int countTriplets(Node head, int x) 
{ 
    Node ptr, ptr1, ptr2; 
    int count = 0; 

    // unordered_map 'um' implemented as hash table 
    Dictionary<int,Node> um = new Dictionary<int,Node>(); 

    // insert the <node data, node pointer> tuple in 'um' 
    for (ptr = head; ptr != null; ptr = ptr.next) 
        if(um.ContainsKey(ptr.data)) 
            um[ptr.data] = ptr; 
        else
            um.Add(ptr.data, ptr); 

    // generate all possible pairs 
    for (ptr1 = head; ptr1 != null; ptr1 = ptr1.next) 
        for (ptr2 = ptr1.next; ptr2 != null; ptr2 = ptr2.next) 
        { 

            // p_sum - sum of elements in the current pair 
            int p_sum = ptr1.data + ptr2.data; 

            // if 'x-p_sum' is present in 'um' and either of the two nodes 
            // are not equal to the 'um[x-p_sum]' node 
            if (um.ContainsKey(x - p_sum) && um[x - p_sum] != ptr1 
                && um[x - p_sum] != ptr2) 

                // increment count 
                count++; 
        } 

    // required count of triplets 
    // division by 3 as each triplet is counted 3 times 
    return (count / 3); 
} 

// A utility function to insert a new node at the 
// beginning of doubly linked list 
static Node insert(Node head, int val) 
{ 
        // allocate node  
        Node temp = new Node(val); 

        if (head == null) 
            head = temp; 

        else
        { 
            temp.next = head; 
            head.prev = temp; 
            head = temp; 
        } 

        return head; 
} 

// Driver code 
public static void Main(String[] args) 
{ 
    // start with an empty doubly linked list 
    Node head = null; 

    // insert values in sorted order 
    head = insert(head, 9); 
    head = insert(head, 8); 
    head = insert(head, 6); 
    head = insert(head, 5); 
    head = insert(head, 4); 
    head = insert(head, 2); 
    head = insert(head, 1); 

    int x = 17; 

    Console.Write("Count = "
        + countTriplets(head, x)); 
} 
} 

// This code is contributed by PrinciRaj1992 

```

**输出：**

```
Count = 2

```

**时间复杂度：** O（n <sup>2</sup> ）
**辅助空间：** O（n）

**方法3高效方法（使用两个指针）：**
从左到右遍历双向链表。 对于遍历过程中的每个**当前**节点，最后插入两个指针**，第一个** =指向紧接**当前**节点的节点，最后**个指针** =指针 到列表的最后一个节点。 现在，计算列表中从**第一个**到**最后一个**指针的对，它们总计为值**（x –当前节点的数据）**（[中描述的算法](https://www.geeksforgeeks.org/find-pairs-given-sum-doubly-linked-list/) 帖子）。 将此计数添加到三元组的 **total_count** 中。 指向**最后一个**节点的指针只能在开始处找到一次。

## C++

```cpp

// C++ implementation to count triplets in a sorted doubly linked list 
// whose sum is equal to a given value 'x' 
#include <bits/stdc++.h> 

using namespace std; 

// structure of node of doubly linked list 
struct Node { 
    int data; 
    struct Node* next, *prev; 
}; 

// function to count pairs whose sum equal to given 'value' 
int countPairs(struct Node* first, struct Node* second, int value) 
{ 
    int count = 0; 

    // The loop terminates when either of two pointers 
    // become NULL, or they cross each other (second->next 
    // == first), or they become same (first == second) 
    while (first != NULL && second != NULL &&  
           first != second && second->next != first) { 

        // pair found 
        if ((first->data + second->data) == value) { 

            // increment count 
            count++; 

            // move first in forward direction 
            first = first->next; 

            // move second in backward direction 
            second = second->prev; 
        } 

        // if sum is greater than 'value' 
        // move second in backward direction 
        else if ((first->data + second->data) > value) 
            second = second->prev; 

        // else move first in forward direction 
        else
            first = first->next; 
    } 

    // required count of pairs 
    return count; 
} 

// function to count triplets in a sorted doubly linked list 
// whose sum is equal to a given value 'x' 
int countTriplets(struct Node* head, int x) 
{ 
    // if list is empty 
    if (head == NULL) 
        return 0; 

    struct Node* current, *first, *last; 
    int count = 0; 

    // get pointer to the last node of 
    // the doubly linked list 
    last = head; 
    while (last->next != NULL) 
        last = last->next; 

    // traversing the doubly linked list 
    for (current = head; current != NULL; current = current->next) { 

        // for each current node 
        first = current->next; 

        // count pairs with sum(x - current->data) in the range 
        // first to last and add it to the 'count' of triplets 
        count += countPairs(first, last, x - current->data); 
    } 

    // required count of triplets 
    return count; 
} 

// A utility function to insert a new node at the 
// beginning of doubly linked list 
void insert(struct Node** head, int data) 
{ 
    // allocate node 
    struct Node* temp = new Node(); 

    // put in the data 
    temp->data = data; 
    temp->next = temp->prev = NULL; 

    if ((*head) == NULL) 
        (*head) = temp; 
    else { 
        temp->next = *head; 
        (*head)->prev = temp; 
        (*head) = temp; 
    } 
} 

// Driver program to test above 
int main() 
{ 
    // start with an empty doubly linked list 
    struct Node* head = NULL; 

    // insert values in sorted order 
    insert(&head, 9); 
    insert(&head, 8); 
    insert(&head, 6); 
    insert(&head, 5); 
    insert(&head, 4); 
    insert(&head, 2); 
    insert(&head, 1); 

    int x = 17; 

    cout << "Count = "
         << countTriplets(head, x); 
    return 0; 
} 

```

## Java

```java

// Java implementation to count triplets in a sorted doubly linked list 
// whose sum is equal to a given value 'x' 
import java.util.*; 

class GFG{ 

// structure of node of doubly linked list 
static class Node { 
    int data; 
    Node next, prev; 
}; 

// function to count pairs whose sum equal to given 'value' 
static int countPairs(Node first, Node second, int value) 
{ 
    int count = 0; 

    // The loop terminates when either of two pointers 
    // become null, or they cross each other (second.next 
    // == first), or they become same (first == second) 
    while (first != null && second != null &&  
           first != second && second.next != first) { 

        // pair found 
        if ((first.data + second.data) == value) { 

            // increment count 
            count++; 

            // move first in forward direction 
            first = first.next; 

            // move second in backward direction 
            second = second.prev; 
        } 

        // if sum is greater than 'value' 
        // move second in backward direction 
        else if ((first.data + second.data) > value) 
            second = second.prev; 

        // else move first in forward direction 
        else
            first = first.next; 
    } 

    // required count of pairs 
    return count; 
} 

// function to count triplets in a sorted doubly linked list 
// whose sum is equal to a given value 'x' 
static int countTriplets(Node head, int x) 
{ 
    // if list is empty 
    if (head == null) 
        return 0; 

    Node current, first, last; 
    int count = 0; 

    // get pointer to the last node of 
    // the doubly linked list 
    last = head; 
    while (last.next != null) 
        last = last.next; 

    // traversing the doubly linked list 
    for (current = head; current != null; current = current.next) { 

        // for each current node 
        first = current.next; 

        // count pairs with sum(x - current.data) in the range 
        // first to last and add it to the 'count' of triplets 
        count += countPairs(first, last, x - current.data); 
    } 

    // required count of triplets 
    return count; 
} 

// A utility function to insert a new node at the 
// beginning of doubly linked list 
static Node insert(Node head, int data) 
{ 
    // allocate node 
    Node temp = new Node(); 

    // put in the data 
    temp.data = data; 
    temp.next = temp.prev = null; 

    if ((head) == null) 
        (head) = temp; 
    else { 
        temp.next = head; 
        (head).prev = temp; 
        (head) = temp; 
    } 
    return head; 
} 

// Driver program to test above 
public static void main(String[] args) 
{ 
    // start with an empty doubly linked list 
    Node head = null; 

    // insert values in sorted order 
    head = insert(head, 9); 
    head = insert(head, 8); 
    head = insert(head, 6); 
    head = insert(head, 5); 
    head = insert(head, 4); 
    head = insert(head, 2); 
    head = insert(head, 1); 

    int x = 17; 

    System.out.print("Count = "
         + countTriplets(head, x)); 
} 
} 

// This code is contributed by 29AjayKumar 

```

## C#

```cs

// C# implementation to count triplets  
// in a sorted doubly linked list 
// whose sum is equal to a given value 'x' 
using System; 

class GFG 
{ 

// structure of node of doubly linked list 
class Node  
{ 
    public int data; 
    public Node next, prev; 
}; 

// function to count pairs whose sum equal to given 'value' 
static int countPairs(Node first, Node second, int value) 
{ 
    int count = 0; 

    // The loop terminates when either of two pointers 
    // become null, or they cross each other (second.next 
    // == first), or they become same (first == second) 
    while (first != null && second != null &&  
        first != second && second.next != first) { 

        // pair found 
        if ((first.data + second.data) == value) { 

            // increment count 
            count++; 

            // move first in forward direction 
            first = first.next; 

            // move second in backward direction 
            second = second.prev; 
        } 

        // if sum is greater than 'value' 
        // move second in backward direction 
        else if ((first.data + second.data) > value) 
            second = second.prev; 

        // else move first in forward direction 
        else
            first = first.next; 
    } 

    // required count of pairs 
    return count; 
} 

// function to count triplets in a sorted doubly linked list 
// whose sum is equal to a given value 'x' 
static int countTriplets(Node head, int x) 
{ 
    // if list is empty 
    if (head == null) 
        return 0; 

    Node current, first, last; 
    int count = 0; 

    // get pointer to the last node of 
    // the doubly linked list 
    last = head; 
    while (last.next != null) 
        last = last.next; 

    // traversing the doubly linked list 
    for (current = head; current != null; current = current.next) { 

        // for each current node 
        first = current.next; 

        // count pairs with sum(x - current.data) in the range 
        // first to last and add it to the 'count' of triplets 
        count += countPairs(first, last, x - current.data); 
    } 

    // required count of triplets 
    return count; 
} 

// A utility function to insert a new node at the 
// beginning of doubly linked list 
static Node insert(Node head, int data) 
{ 
    // allocate node 
    Node temp = new Node(); 

    // put in the data 
    temp.data = data; 
    temp.next = temp.prev = null; 

    if ((head) == null) 
        (head) = temp; 
    else { 
        temp.next = head; 
        (head).prev = temp; 
        (head) = temp; 
    } 
    return head; 
} 

// Driver program to test above 
public static void Main(String[] args) 
{ 
    // start with an empty doubly linked list 
    Node head = null; 

    // insert values in sorted order 
    head = insert(head, 9); 
    head = insert(head, 8); 
    head = insert(head, 6); 
    head = insert(head, 5); 
    head = insert(head, 4); 
    head = insert(head, 2); 
    head = insert(head, 1); 

    int x = 17; 

    Console.Write("Count = "
        + countTriplets(head, x)); 
} 
} 

// This code is contributed by 29AjayKumar 

```

**输出：**

```
Count = 2

```

**时间复杂度：** O（n <sup>2</sup> ）
**辅助空间：** O（1）

本文由 **Ayush Jauhari** 提供。 如果您喜欢GeeksforGeeks并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至tribution@geeksforgeeks.org。 查看您的文章出现在GeeksforGeeks主页上，并帮助其他Geeks。

如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论。

