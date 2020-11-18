# 链表

中的多数元素

给定一个链表，找到多数元素。 如果一个元素出现**多数元素**，则它的出现次数大于或等于 **n / 2** 倍，其中 n 是链接列表中节点的总数。

**示例：**

```
Input  : 1->2->3->4->5->1->1->1->NULL
Output : 1
Explanation  1 occurs 4 times 
Input :10->23->11->9->54->NULL
Output :NO majority element

```

**方法 1（简单）**
从头开始运行两个循环，并迭代计算每个元素的频率。 打印其频率大于或等于 n / 2 的元素。 在这种方法中，时间复杂度将为 **O（n * n）**，其中 n 是链表中节点的数量。

## C++

```cpp

// C++ program to find majority element in  
// a linked list 
#include <bits/stdc++.h> 
using namespace std; 

/* Link list node */
struct Node { 
    int data; 
    struct Node* next; 
}; 

/* Function to get the nth node from the  
last of a linked list*/
int majority(struct Node* head) 
{ 
    struct Node* p = head; 

    int total_count = 0, max_count = 0, res = -1; 
    while (p != NULL) { 

        // Count all occurrences of p->data 
        int count = 1; 
        struct Node* q = p->next; 
        while (q != NULL) { 
            if (p->data == q->data)              
               count++;               
            q = q->next; 
        } 

        // Update max_count and res if count 
        // is more than max_count 
        if (count > max_count) 
        { 
            max_count = count; 
            res = p->data; 
        } 

        p = p->next; 
        total_count++; 
    } 

    if (max_count >= total_count/2) 
        return res; 

    // if we reach here it means no 
    // majority element is present. 
    // and we assume that all the 
    // element are positive 
    return -1; 
} 

void push(struct Node** head_ref, int new_data) 
{ 
    struct Node* new_node = 
       (struct Node*)malloc(sizeof(struct Node)); 
    new_node->data = new_data; 
    new_node->next = (*head_ref); 
    (*head_ref) = new_node; 
} 

/* Driver program to test above function*/
int main() 
{ 
    /* Start with the empty list */
    struct Node* head = NULL; 

    // create linked 
    push(&head, 1); 
    push(&head, 1); 
    push(&head, 1); 
    push(&head, 5); 
    push(&head, 4); 
    push(&head, 3); 
    push(&head, 2); 
    push(&head, 1); 

    int res = majority(head); 

    if (res != (-1)) 
        cout << "Majority element is " << res; 
    else
        cout << "No majority element"; 
    return 0; 
} 

```

## Java

```java

// Java program to find majority element in  
// a linked list 
import java.util.*; 

class GFG 
{ 
static Node head; 

/* Link list node */
static class Node  
{ 
    int data; 
    Node next; 
}; 

/* Function to get the nth node from  
the last of a linked list*/
static int majority(Node head) 
{ 
    Node p = head; 

    int total_count = 0,  
        max_count = 0, res = -1; 
    while (p != null)  
    { 

        // Count all occurrences of p->data 
        int count = 1; 
        Node q = p.next; 
        while (q != null) 
        { 
            if (p.data == q.data)              
                count++;              
            q = q.next; 
        } 

        // Update max_count and res if count 
        // is more than max_count 
        if (count > max_count) 
        { 
            max_count = count; 
            res = p.data; 
        } 

        p = p.next; 
        total_count++; 
    } 

    if (max_count >= total_count / 2) 
        return res; 

    // if we reach here it means no 
    // majority element is present. 
    // and we assume that all the 
    // element are positive 
    return -1; 
} 

static void push(Node head_ref,      
                 int new_data) 
{ 
    Node new_node = new Node(); 
    new_node.data = new_data; 
    new_node.next = head_ref; 
    head_ref = new_node; 
    head = head_ref; 
} 

// Driver Code 
public static void main(String[] args)  

{ 

    /* Start with the empty list */
    head = null; 

    // create linked 
    push(head, 1); 
    push(head, 1); 
    push(head, 1); 
    push(head, 5); 
    push(head, 4); 
    push(head, 3); 
    push(head, 2); 
    push(head, 1); 

    int res = majority(head); 

    if (res != (-1)) 
        System.out.println("Majority element is " + res); 
    else
        System.out.println("No majority element"); 
    } 
} 

// This code is contributed by Princi Singh 

```

## Python3

```py

# Python3 program to find majority element in  
# a linked list 
head = None

# Link list node  
class Node : 
    def __init__(self): 
        self.data = 0
        self.next = None

# Function to get the nth node from  
# the last of a linked list 
def majority(head): 
    p = head 

    total_count = 0
    max_count = 0
    res = -1
    while (p != None):  

        # Count all occurrences of p->data 
        count = 1
        q = p.next
        while (q != None): 

            if (p.data == q.data):              
                count = count + 1            
            q = q.next

        # Update max_count and res if count 
        # is more than max_count 
        if (count > max_count): 

            max_count = count 
            res = p.data 

        p = p.next
        total_count = total_count + 1

    if (max_count >= total_count / 2): 
        return res 

    # if we reach here it means no 
    # majority element is present. 
    # and we assume that all the 
    # element are positive 
    return -1

def push( head_ref, new_data): 
    global head 
    new_node = Node() 
    new_node.data = new_data 
    new_node.next = head_ref 
    head_ref = new_node 
    head = head_ref 

# Driver Code 

# Start with the empty list  
head = None

# create linked 
push(head, 1) 
push(head, 1) 
push(head, 1) 
push(head, 5) 
push(head, 4) 
push(head, 3) 
push(head, 2) 
push(head, 1) 

res = majority(head) 

if (res != (-1)): 
    print("Majority element is " , res) 
else: 
    print("No majority element") 

# This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# program to find majority element in  
// a linked list 
using System; 

class GFG 
{ 
    static Node head; 

    /* Link list node */
    public class Node  
    { 
        public int data; 
        public Node next; 
    }; 

    /* Function to get the nth node from  
    the last of a linked list*/
    static int majority(Node head) 
    { 
        Node p = head; 

        int total_count = 0,  
            max_count = 0, res = -1; 
        while (p != null)  
        { 

            // Count all occurrences of p->data 
            int count = 1; 
            Node q = p.next; 
            while (q != null) 
            { 
                if (p.data == q.data)              
                    count++;              
                q = q.next; 
            } 

            // Update max_count and res if count 
            // is more than max_count 
            if (count > max_count) 
            { 
                max_count = count; 
                res = p.data; 
            } 

            p = p.next; 
            total_count++; 
        } 

        if (max_count >= total_count / 2) 
            return res; 

        // if we reach here it means no 
        // majority element is present. 
        // and we assume that all the 
        // element are positive 
        return -1; 
    } 

    static void push(Node head_ref,      
                     int new_data) 
    { 
        Node new_node = new Node(); 
        new_node.data = new_data; 
        new_node.next = head_ref; 
        head_ref = new_node; 
        head = head_ref; 
    } 

// Driver Code 
public static void Main(String[] args)  
{ 

    /* Start with the empty list */
    head = null; 

    // create linked 
    push(head, 1); 
    push(head, 1); 
    push(head, 1); 
    push(head, 5); 
    push(head, 4); 
    push(head, 3); 
    push(head, 2); 
    push(head, 1); 

    int res = majority(head); 

    if (res != (-1)) 
        Console.WriteLine("Majority element is " + res); 
    else
        Console.WriteLine("No majority element"); 
    } 
} 

// This code is contributed by PrinciRaj1992  

```

Time Complexity O(n*n)

**方法 2** 使用哈希技术。 我们计算每个元素的频率，然后打印频率≥n / 2 的元素；

## C++

```cpp

// CPP program to find majority element 
// in the linked list using hashing 
#include <bits/stdc++.h> 
using namespace std; 

/* Link list node */
struct Node { 
    int data; 
    struct Node* next; 
}; 

/* Function to get the nth node from the last 
 of a linked list*/
int majority(struct Node* head) 
{ 
    struct Node* p = head; 

    // Storing elements and their frequencies 
    // in a hash table. 
    unordered_map<int, int> hash;  

    int total_count = 0; 
    while (p != NULL) { 

        // increase every element 
        // frequency by 1 
        hash[p->data]++; 

        p = p->next; 

        total_count++; 
    } 

    // Check if frequency of any element 
    // is more than or equal to total_count/2 
    for (auto x : hash) 
       if (x.second >= total_count/2) 
           return x.first; 

    // If we reach here means no majority element 
    // is present. We assume that all the element  
    // are positive 
    return -1; 
} 

void push(struct Node** head_ref, int new_data) 
{ 
    struct Node* new_node =  
       (struct Node*)malloc(sizeof(struct Node)); 
    new_node->data = new_data; 
    new_node->next = (*head_ref); 
    (*head_ref) = new_node; 
} 

// Driver program to test above function 
int main() 
{ 

    /* Start with the empty list */
    struct Node* head = NULL; 
    push(&head, 1); 
    push(&head, 1); 
    push(&head, 1); 
    push(&head, 5); 
    push(&head, 4); 
    push(&head, 3); 
    push(&head, 2); 
    push(&head, 1); 

    int res = majority(head); 

    if (res != (-1)) 
        cout << "majority element is " << res; 
    else
        cout << "NO majority elemenet"; 
    return 0; 
} 

```

## Java

```java

// JAVA program to find majority element 
// in the linked list using hashing 
import java.util.*; 

class GFG 
{ 

/* Link list node */
static class Node 
{ 
    int data; 
    Node next; 
}; 

/* Function to get the nth node from the last 
of a linked list*/
static int majority(Node head) 
{ 
    Node p = head; 

    // Storing elements and their frequencies 
    // in a hash table. 
    HashMap<Integer,Integer> hash = new HashMap<Integer,Integer>();  

    int total_count = 0; 
    while (p != null)  
    { 

        // increase every element 
        // frequency by 1 
        if(hash.containsKey(p.data)) 
            hash.put(p.data, hash.get(p.data) + 1); 
        else
            hash.put(p.data, 1); 

        p = p.next; 

        total_count++; 
    } 

    // Check if frequency of any element 
    // is more than or equal to total_count/2 
    for (Map.Entry<Integer,Integer> x : hash.entrySet())  
    if (x.getValue() >= total_count/2) 
        return x.getKey(); 

    // If we reach here means no majority element 
    // is present. We assume that all the element  
    // are positive 
    return -1; 
} 

static Node push(Node head_ref, int new_data) 
{ 
    Node new_node = new Node(); 
    new_node.data = new_data; 
    new_node.next = head_ref; 
    head_ref = new_node; 
    return head_ref; 
} 

// Driver code 
public static void main(String[] args) 
{ 

    /* Start with the empty list */
    Node head = null; 
    head = push(head, 1); 
    head = push(head, 1); 
    head = push(head, 1); 
    head = push(head, 5); 
    head = push(head, 4); 
    head = push(head, 3); 
    head = push(head, 2); 
    head = push(head, 1); 

    int res = majority(head); 

    if (res != (-1)) 
        System.out.print("majority element is " + res); 
    else
        System.out.print("NO majority elemenet"); 
} 
} 

// This code is contributed by Rajput-Ji 

```

## C#

```cs

// C# program to find majority element 
// in the linked list using hashing 
using System; 
using System.Collections.Generic; 
class GFG 
{ 

/* Link list node */
public class Node 
{ 
    public int data; 
    public Node next; 
}; 

/* Function to get the nth node 
from the last of a linked list*/
static int majority(Node head) 
{ 
    Node p = head; 

    // Storing elements and their frequencies 
    // in a hash table. 
    Dictionary<int,  
               int> hash = new Dictionary<int,  
                                          int>();  

    int total_count = 0; 
    while (p != null)  
    { 

        // increase every element 
        // frequency by 1 
        if(hash.ContainsKey(p.data)) 
            hash[p.data] = hash[p.data] + 1; 
        else
            hash.Add(p.data, 1); 

        p = p.next; 

        total_count++; 
    } 

    // Check if frequency of any element 
    // is more than or equal to total_count/2 
    foreach(KeyValuePair<int, int> x in hash) 
    if (x.Value >= total_count/2) 
        return x.Key; 

    // If we reach here means no majority element 
    // is present. We assume that all the element  
    // are positive 
    return -1; 
} 

static Node push(Node head_ref, int new_data) 
{ 
    Node new_node = new Node(); 
    new_node.data = new_data; 
    new_node.next = head_ref; 
    head_ref = new_node; 
    return head_ref; 
} 

// Driver code 
public static void Main(String[] args) 
{ 

    /* Start with the empty list */
    Node head = null; 
    head = push(head, 1); 
    head = push(head, 1); 
    head = push(head, 1); 
    head = push(head, 5); 
    head = push(head, 4); 
    head = push(head, 3); 
    head = push(head, 2); 
    head = push(head, 1); 

    int res = majority(head); 

    if (res != (-1)) 
        Console.Write("majority element is " + res); 
    else
        Console.Write("NO majority elemenet"); 
} 
} 

// This code is contributed by 29AjayKumar 

```

Time Complexity O(n)
**Output :**

```
majority element is 1

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。