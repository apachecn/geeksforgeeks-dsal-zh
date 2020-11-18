# 计算一个乘积等于给定值x的双链表中的三胞胎

给定一个不同节点的排序双链表（没有两个节点具有相同的数据）和一个值x。 任务是对列表中的三元组进行计数，直到达到给定值x。

**示例：**

> **输入：**列表= 1- > 2- > 4- > 5- > 6- > 8- > 9，x = 8
> **输出：** 1
> 三元组是（1、2、4）
> 
> **输入：**列表= 1- > 2- > 4- > 5- > 6- > 8- > 9，x = 120
> **输出：** 1
> 三元组是（4，5，6）

**天真的方法：**使用三个嵌套循环生成所有三元组，并检查三元组乘积中的元素是否等于x。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation to count triplets 
// in a sorted doubly linked list 
// whose product is equal to a given value 'x' 
#include <bits/stdc++.h> 
using namespace std; 

// structure of node of doubly linked list 
struct Node { 
    int data; 
    struct Node *next, *prev; 
}; 

// function to count triplets in a sorted doubly linked list 
// whose product is equal to a given value 'x' 
int countTriplets(struct Node* head, int x) 
{ 
    struct Node *ptr1, *ptr2, *ptr3; 
    int count = 0; 

    // generate all possible triplets 
    for (ptr1 = head; ptr1 != NULL; ptr1 = ptr1->next) 
        for (ptr2 = ptr1->next; ptr2 != NULL; ptr2 = ptr2->next) 
            for (ptr3 = ptr2->next; ptr3 != NULL; ptr3 = ptr3->next) 

                // if elements in the current triplet product up to 'x' 
                if ((ptr1->data * ptr2->data * ptr3->data) == x) 

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

    int x = 8; 

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
import java.util.*; 

// Represents node of a doubly linked list  
class Node  
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
                    if ((ptr1.data * ptr2.data * ptr3.data) == x)  

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
    public static void main(String []args)  
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

        int x = 8;  
        System.out.println("count = " + countTriplets(head, x));  
    }  
} 

// This code is contributed by 29AjayKumar 

```

## Python3

```py

# Python3 implementation to count triplets 
# in a sorted doubly linked list 
# whose sum is equal to a given value 'x' 

# Represents node of a doubly linked list 
class Node: 
    data = None
    prev = None
    next_ = None

    def __init__(self, val): 
        self.data = val 
        self.prev = None
        self.next_ = None

# function to count triplets in 
# a sorted doubly linked list 
# whose sum is equal to a given value 'x' 
def countTriplets(head, x): 
    ptr1, ptr2, ptr3 = Node(0), Node(0), Node(0) 
    count = 0

    # generate all possible triplets 
    ptr1 = head 
    while ptr1 is not None: 
        ptr2 = ptr1.next_ 
        while ptr2 is not None: 
            ptr3 = ptr2.next_ 
            while ptr3 is not None: 

                # if elements in the current  
                # triplet sum up to 'x' 
                if ptr1.data * ptr2.data * ptr3.data == x: 

                    # increment count 
                    count += 1
                ptr3 = ptr3.next_ 
            ptr2 = ptr2.next_ 
        ptr1 = ptr1.next_ 

        # required count of triplets 
        return count 

# A utility function to insert a new node at the 
# beginning of doubly linked list 
def insert(head, val): 

    # allocate node 
    temp = Node(val) 
    if head is None: 
        head = temp 
    else: 
        temp.next_ = head 
        head.prev = temp 
        head = temp 

    return head 

# Driver Code 
if __name__ == "__main__": 

    # start with an empty doubly linked list 
    head = Node(0) 

    # insert values in sorted order 
    head = insert(head, 9) 
    head = insert(head, 8) 
    head = insert(head, 6) 
    head = insert(head, 5) 
    head = insert(head, 4) 
    head = insert(head, 2) 
    head = insert(head, 1) 

    x = 8
    print("count =", countTriplets(head, x)) 

# This code is contributed by 
# sanjeev2552 

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
                    if ((ptr1.data * ptr2.data * ptr3.data) == x)  

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

        int x = 8;  
        Console.WriteLine("count = " + countTriplets(head, x));  
    }  
}  

// This code is contributed by Arnab Kundu 

```

**Output:**

```
Count = 1

```

**时间复杂度：** O（n ^ 3）
**辅助空间：** O（1）

**方法2（散列）：**创建一个散列表，其中（键，值）元组表示为（节点数据，节点指针）元组。 遍历双向链表，并将每个节点的数据及其指针对（元组）存储在哈希表中。 现在，生成每个可能的节点对。 对于每对节点，计算p_product（两个节点中数据的乘积），然后检查哈希表中是否存在（x / p_product）。 如果存在，则还要验证该对中的两个节点是否与哈希表中与（x / p_product）关联的节点不同，并最终递增计数。 返回（计数/ 3），因为在上述过程中每个三​​元组被计数3次。

下面是上述方法的实现：

```

// C++ implementation to count triplets 
// in a sorted doubly linked list 
// whose product is equal to a given value 'x' 
#include <bits/stdc++.h> 
using namespace std; 

// structure of node of doubly linked list 
struct Node { 
    int data; 
    struct Node *next, *prev; 
}; 

// function to count triplets in a sorted doubly linked list 
// whose product is equal to a given value 'x' 
int countTriplets(struct Node* head, int x) 
{ 
    struct Node *ptr, *ptr1, *ptr2; 
    int count = 0; 

    // unordered_map 'um' implemented as hash table 
    unordered_map<int, Node*> um; 

    // insert the <node data, node pointer> tuple in 'um' 
    for (ptr = head; ptr != NULL; ptr = ptr->next) 
        um[ptr->data] = ptr; 

    // generate all possible pairs 
    for (ptr1 = head; ptr1 != NULL; ptr1 = ptr1->next) 
        for (ptr2 = ptr1->next; ptr2 != NULL; ptr2 = ptr2->next) { 

            // p_product = product of elements in the current pair 
            int p_product = (ptr1->data * ptr2->data); 

            // if 'x/p_product' is present in 'um' and 
            // either of the two nodes 
            // are not equal to the 'um[x/p_product]' node 
            if (um.find(x / p_product) != um.end() && um[x / p_product] != ptr1 
                && um[x / p_product] != ptr2) 

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

// Driver program to test above functions 
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

    int x = 8; 

    cout << "Count = "
         << countTriplets(head, x); 
    return 0; 
} 

```

**Output:**

```
Count = 1

```

**时间复杂度：** O（n ^ 2）
**辅助空间：** O（n）

**方法3（使用两个指针）：**从左到右遍历双向链表。 对于遍历期间的每个当前节点，最后两个指针为first =指向当前节点旁边的节点的指针和last =指向列表的最后一个节点的指针。 现在，计算列表中从第一个指针到最后一个指针对的对，直到值（x /当前节点的数据）为止（本文中描述的算法）。 将此计数添加到三元组的total_count中。 指向最后一个节点的指针只能在开始处找到一次。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation to count triplets 
// in a sorted doubly linked list 
// whose product is equal to a given value 'x' 
#include <bits/stdc++.h> 
using namespace std; 

// structure of node of doubly linked list 
struct Node { 
    int data; 
    struct Node *next, *prev; 
}; 

// function to count pairs whose product equal to given 'value' 
int countPairs(struct Node* first, struct Node* second, int value) 
{ 
    int count = 0; 

    // The loop terminates when either of two pointers 
    // become NULL, or they cross each other (second->next 
    // == first), or they become same (first == second) 
    while (first != NULL && second != NULL && first != second 
           && second->next != first) { 

        // pair found 
        if ((first->data * second->data) == value) { 

            // increment count 
            count++; 

            // move first in forward direction 
            first = first->next; 

            // move second in backward direction 
            second = second->prev; 
        } 

        // if product is greater than 'value' 
        // move second in backward direction 
        else if ((first->data * second->data) > value) 
            second = second->prev; 

        // else move first in forward direction 
        else
            first = first->next; 
    } 

    // required count of pairs 
    return count; 
} 

// function to count triplets in a sorted doubly linked list 
// whose product is equal to a given value 'x' 
int countTriplets(struct Node* head, int x) 
{ 
    // if list is empty 
    if (head == NULL) 
        return 0; 

    struct Node *current, *first, *last; 
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

        // count pairs with product(x / current->data) in the range 
        // first to last and add it to the 'count' of triplets 
        count += countPairs(first, last, x / current->data); 
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

    int x = 8; 

    cout << "Count = "
         << countTriplets(head, x); 
    return 0; 
} 

```

## Java

```java

// Java implementation to count triplets 
// in a sorted doubly linked list 
// whose product is equal to a given value 'x' 
import java.util.*; 

class GFG 
{ 

// structure of node of doubly linked list 
static class Node  
{ 
    int data; 
    Node next, prev; 
}; 

// function to count pairs whose product 
// equal to given 'value' 
static int countPairs(Node first, Node second, 
                      int value) 
{ 
    int count = 0; 

    // The loop terminates when either of two pointers 
    // become null, or they cross each other (second.next 
    // == first), or they become same (first == second) 
    while (first != null && second != null &&  
            first != second && second.next != first) 
    { 

        // pair found 
        if ((first.data * second.data) == value)  
        { 

            // increment count 
            count++; 

            // move first in forward direction 
            first = first.next; 

            // move second in backward direction 
            second = second.prev; 
        } 

        // if product is greater than 'value' 
        // move second in backward direction 
        else if ((first.data * second.data) > value) 
            second = second.prev; 

        // else move first in forward direction 
        else
            first = first.next; 
    } 

    // required count of pairs 
    return count; 
} 

// function to count triplets in  
// a sorted doubly linked list 
// whose product is equal to a given value 'x' 
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
    for (current = head; current != null;  
        current = current.next)  
    { 

        // for each current node 
        first = current.next; 

        // count pairs with product(x / current.data)  
        // in the range first to last and 
        // add it to the 'count' of triplets 
        count += countPairs(first, last, x / current.data); 
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
    else 
    { 
        temp.next = head; 
        (head).prev = temp; 
        (head) = temp; 
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

    int x = 8; 

    System.out.println( "Count = "+ countTriplets(head, x)); 
} 
} 

// This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# implementation to count triplets 
// in a sorted doubly linked list 
// whose product is equal to a given value 'x' 
using System; 

class GFG 
{ 

// structure of node of doubly linked list 
class Node  
{ 
    public int data; 
    public Node next, prev; 
}; 

// function to count pairs whose product 
// equal to given 'value' 
static int countPairs(Node first, Node second, 
                      int value) 
{ 
    int count = 0; 

    // The loop terminates when either of two pointers 
    // become null, or they cross each other (second.next 
    // == first), or they become same (first == second) 
    while (first != null && second != null &&  
            first != second && second.next != first) 
    { 

        // pair found 
        if ((first.data * second.data) == value)  
        { 

            // increment count 
            count++; 

            // move first in forward direction 
            first = first.next; 

            // move second in backward direction 
            second = second.prev; 
        } 

        // if product is greater than 'value' 
        // move second in backward direction 
        else if ((first.data * second.data) > value) 
            second = second.prev; 

        // else move first in forward direction 
        else
            first = first.next; 
    } 

    // required count of pairs 
    return count; 
} 

// function to count triplets in  
// a sorted doubly linked list 
// whose product is equal to a given value 'x' 
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
    for (current = head; current != null;  
        current = current.next)  
    { 

        // for each current node 
        first = current.next; 

        // count pairs with product(x / current.data)  
        // in the range first to last and 
        // add it to the 'count' of triplets 
        count += countPairs(first, last, x / current.data); 
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
    else
    { 
        temp.next = head; 
        (head).prev = temp; 
        (head) = temp; 
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

    int x = 8; 

    Console.WriteLine( "Count = "+ countTriplets(head, x)); 
} 
} 

// This code is contributed by Rajput-Ji 

```

**Output:**

```
Count = 1

```

**时间复杂度：** O（n ^ 2）
**辅助空间：** O（1）



* * *

* * *

如果您喜欢GeeksforGeeks并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至tribution@geeksforgeeks.org。 查看您的文章出现在GeeksforGeeks主页上，并帮助其他Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。