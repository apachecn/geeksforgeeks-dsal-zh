# 在链接列表

> 原文：[https://www.geeksforgeeks.org/find-unique-elements-linked-list/](https://www.geeksforgeeks.org/find-unique-elements-linked-list/)

中查找唯一的元素

给定一个链表。 我们需要在链表中找到唯一元素，即链表中未重复的元素或频率为 1 的元素。如果列表中不存在此类元素，请打印“无唯一元素”。

**示例**：

```
Input : 1 -> 4 -> 4 -> 2 -> 3 -> 5 -> 3 -> 4 -> 5
Output :1 2 

Input :4 -> 5 -> 2 -> 5 -> 1 -> 4 -> 1 -> 2
Output :No Unique Elements

```

**方法 1（使用两个循环）**这是使用两个循环的简单方法。 外循环用于一一拾取元素，内循环将拾取的元素与其余元素进行比较。 如果 Element 不等于 Print 那个 Element 以外的其他元素。 时间复杂度：O（N * n）

**方法 2（排序）**：使用合并排序对元素进行排序。`O(n Log n)`。 现在以线性时间遍历列表，并检查当前元素是否不等于前一个元素，然后打印`O(n)`

请注意，此方法不会保留元素的原始顺序。

时间复杂度：`O(NlogN)`

**方法 3（哈希）**

我们使用哈希表的概念在这里，我们从头到尾遍历链接列表。 对于每个新遇到的元素，我们将其放在哈希表中，然后再次遍历列表并打印那些频率为 1 的元素。时间复杂度：`O(n)`

下面是此实现

## C++

```cpp

// C++ Program to Find the Unique elements in 
// linked lists 
#include <bits/stdc++.h> 
using namespace std; 

/* Linked list node */
struct Node { 
    int data; 
    struct Node* next; 
}; 

/* Function to insert a node at the beginning of  
   the linked list */
void push(struct Node** head_ref, int new_data) 
{ 
    struct Node* new_node = new Node; 
    new_node->data = new_data; 
    new_node->next = *head_ref; 
    *head_ref = new_node; 
} 

// function to Find the unique elements in linked lists 
void uniqueElements(struct Node* head) 
{ 
    // Initialize hash array that store the 
    // frequency of each element of list 
    unordered_map<int, int> hash; 

    for (Node *temp=head; temp!=NULL; temp=temp->next) 
        hash[temp->data]++; 

    int count = 0; 
    for (Node *temp=head; temp!=NULL; temp=temp->next) { 

        // Check whether the frequency of current  
        // element is 1 or not 
        if (hash[temp->data] == 1) { 
            cout << temp->data << " "; 
            count++; 
        } 
    } 

    // If No unique element in list 
    if (count == 0) 
        cout << " No Unique Elements "; 
} 

// Driver program to test above 
int main() 
{ 
    struct Node* head = NULL; 

    // creating linked list 
    push(&head, 5); 
    push(&head, 4); 
    push(&head, 3); 
    push(&head, 5); 
    push(&head, 3); 
    push(&head, 2); 
    push(&head, 4); 
    push(&head, 4); 
    push(&head, 1); 
    uniqueElements(head); 
    return 0; 
} 

```

## Java

```java

// Java Program to Find the Unique elements  
// in linked lists 
import java.util.*; 
class GFG  
{ 

/* Linked list node */
static class Node 
{ 
    int data; 
    Node next; 
}; 
static Node head; 

/* Function to insert a node at the 
beginning of the linked list */
static void push(Node head_ref, int new_data) 
{ 
    Node new_node = new Node(); 
    new_node.data = new_data; 
    new_node.next = head_ref; 
    head_ref = new_node; 
    head = head_ref; 
} 

// function to Find the unique elements 
// in linked lists 
static void uniqueElements(Node head) 
{ 
    // Initialize hash array that store the 
    // frequency of each element of list 
    HashMap<Integer,  
            Integer> hash = new HashMap<Integer,  
                                        Integer>(); 

    for (Node temp = head;  
              temp != null; temp = temp.next) 
    { 
        if(hash.containsKey(temp.data)) 
        { 
            hash.put(temp.data,  
            hash.get(temp.data) + 1); 
        } 
        else
        { 
            hash.put(temp.data, 1); 
        } 
    } 

    int count = 0; 
    for (Node temp = head;  
              temp != null; temp = temp.next)  
    { 

        // Check whether the frequency of current  
        // element is 1 or not 
        if (hash.get(temp.data) == 1)  
        { 
            System.out.print(temp.data + " "); 
            count++; 
        } 
    } 

    // If No unique element in list 
    if (count == 0) 
        System.out.print(" No Unique Elements "); 
} 

// Driver Code 
public static void main(String[] args) 
{ 
    head = null; 

    // creating linked list 
    push(head, 5); 
    push(head, 4); 
    push(head, 3); 
    push(head, 5); 
    push(head, 3); 
    push(head, 2); 
    push(head, 4); 
    push(head, 4); 
    push(head, 1); 
    uniqueElements(head); 
} 
}  

// This code is contributed by Rajput-Ji 

```

## Python3

```py

# Python3 Program to Find the Unique elements in  
# linked lists  
import sys 
import math 

# Linked list node  
class Node: 
    def __init__(self,data): 
        self.data = data 
        self.next = None

# Function to insert a node at the beginning of  
# the linked list  
def push(head,data): 
    if not head: 
        return Node(data) 
    temp = Node(data) 
    temp.next = head 
    head = temp 
    return head 

# function to Find the unique elements in linked lists  
def uniqueElements(head): 

    # Initialize hash array that store the  
    # frequency of each element of list 
    _map = {} 
    temp = head 
    while(temp): 
        d = temp.data 
        if d in _map: 
            _map[d]=_map.get(d)+1
        else: 
            _map[d] = 1
        temp = temp.next
    count = 0
    for i in _map: 

        # Check whether the frequency of current  
        # element is 1 or not  
        if _map.get(i) == 1: 
            count += 1
            print("{} ".format(i),end="") 

    # If No unique element in list  
    if count == 0: 
        print("No Unique Elements") 

# Driver program to test above 
if __name__=='__main__': 

    # creating linked list 
    head = None
    head = push(head,5) 
    head = push(head,4) 
    head = push(head,3) 
    head = push(head,5) 
    head = push(head,3) 
    head = push(head,2) 
    head = push(head,4) 
    head = push(head,4) 
    head = push(head,1) 
    uniqueElements(head) 

# This code is Contributed by Vikash Kumar 37 

```

## C#

```cs

// C# Program to Find the Unique elements  
// in linked lists 
using System; 
using System.Collections.Generic; 

class GFG  
{ 

/* Linked list node */
public class Node 
{ 
    public int data; 
    public Node next; 
}; 
static Node head; 

/* Function to insert a node at the 
beginning of the linked list */
static void push(Node head_ref,  
                 int new_data) 
{ 
    Node new_node = new Node(); 
    new_node.data = new_data; 
    new_node.next = head_ref; 
    head_ref = new_node; 
    head = head_ref; 
} 

// function to Find the unique elements 
// in linked lists 
static void uniqueElements(Node head) 
{ 

    // Initialize hash array that store the 
    // frequency of each element of list 
    Dictionary<int,  
               int> hash = new Dictionary<int,  
                                          int>(); 

    for (Node temp = head;  
              temp != null; temp = temp.next) 
    { 
        if(hash.ContainsKey(temp.data)) 
        { 
            hash[temp.data] = hash[temp.data] + 1; 
        } 
        else
        { 
            hash.Add(temp.data, 1); 
        } 
    } 

    int count = 0; 
    for (Node temp = head;  
              temp != null; temp = temp.next)  
    { 

        // Check whether the frequency of  
        // current element is 1 or not 
        if (hash[temp.data] == 1)  
        { 
            Console.Write(temp.data + " "); 
            count++; 
        } 
    } 

    // If No unique element in list 
    if (count == 0) 
        Console.Write(" No Unique Elements "); 
} 

// Driver Code 
public static void Main(String[] args) 
{ 
    head = null; 

    // creating linked list 
    push(head, 5); 
    push(head, 4); 
    push(head, 3); 
    push(head, 5); 
    push(head, 3); 
    push(head, 2); 
    push(head, 4); 
    push(head, 4); 
    push(head, 1); 
    uniqueElements(head); 
} 
} 

// This code is contributed by 29AjayKumar 

```

**Output:**

```
1 2

```

**时间复杂度**：`O(n)`

**辅助空间**：`O(n)`



* * *

* * *



