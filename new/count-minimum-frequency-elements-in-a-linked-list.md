# 计算链表中的最小频率元素

> 原文：[https://www.geeksforgeeks.org/count-minimum-frequency-elements-in-a-linked-list/](https://www.geeksforgeeks.org/count-minimum-frequency-elements-in-a-linked-list/)

给定一个包含重复元素的链表。 任务是在给定的链表中查找所有最少出现的元素的数量。 这是矩阵中频率最小的所有此类元素的计数。

**示例**：

```
Input : 1-> 2-> 2-> 3
Output : 2
Explanation:
1 and 3 are elements occurs only one time.
So, count is 2.

Input : 10-> 20-> 20-> 10-> 30
Output : 1

```

**方法**：

*   遍历链表，并使用哈希表存储链表元素的频率，以使`map`的键为链表元素，值为链表中其频率。

*   然后遍历哈希表以找到最小频率。

*   最后，遍历哈希表以查找元素的频率，并检查其是否与上一步中获得的最小频率匹配，如果是，则添加此频率以进行计数。

下面是上述方法的实现：

## C++

```cpp

// C++ program to find count of minimum 
// frequqncy elements in Linked list 
#include <bits/stdc++.h> 
using namespace std; 

/* Link list node */
struct Node { 
    int key; 
    struct Node* next; 
}; 

/* Given a reference (pointer to pointer) to the head  
of a list and an int, push a new node on the front  
of the list. */
void push(struct Node** head_ref, int new_key) 
{ 
    struct Node* new_node = new Node; 
    new_node->key = new_key; 
    new_node->next = (*head_ref); 
    (*head_ref) = new_node; 
} 

// Function to count minimum frequency elements 
// in the linked list 
int countMinimum(struct Node* head) 
{ 
    // Store frequencies of all nodes. 
    unordered_map<int, int> mp; 
    struct Node* current = head; 
    while (current != NULL) { 
        int data = current->key; 
        mp[data]++; 
        current = current->next; 
    } 

    // Find min frequency 
    current = head; 
    int min_frequency = INT_MAX, countMin = 0; 
    for (auto it = mp.begin(); it != mp.end(); it++) { 
        if (it->second <= min_frequency) { 
            min_frequency = it->second; 
        } 
    } 

    // Find count of min frequency elements 
    for (auto it = mp.begin(); it != mp.end(); it++) { 
        if (it->second == min_frequency) { 
            countMin += (it->second); 
        } 
    } 

    return countMin; 
} 

/* Driver program to test count function*/
int main() 
{ 
    /* Start with the empty list */
    struct Node* head = NULL; 
    int x = 21; 

    /* Use push() to construct below list  
    10->10->11->30->10 */
    push(&head, 10); 
    push(&head, 30); 
    push(&head, 11); 
    push(&head, 10); 
    push(&head, 10); 

    cout << countMinimum(head) << endl; 
    return 0; 
} 

```

## Java

```java

// Java program to find count of minimum 
// frequqncy elements in Linked list 
import java.util.*; 

class GFG 
{ 

/* Link list node */
static class Node { 
    int key; 
    Node next; 
}; 

/* Given a reference (pointer to pointer) to the head  
of a list and an int, push a new node on the front  
of the list. */
static Node push(Node head_ref, int new_key) 
{ 
    Node new_node = new Node(); 
    new_node.key = new_key; 
    new_node.next = (head_ref); 
    (head_ref) = new_node; 
    return head_ref; 
} 

// Function to count minimum frequency elements 
// in the linked list 
static int countMinimum( Node head) 
{ 
    // Store frequencies of all nodes. 
    HashMap<Integer,Integer> mp = new HashMap<Integer,Integer>(); 
    Node current = head; 
    while (current != null) 
    { 
        int data = current.key; 
        mp.put(data, (mp.get(data) == null ? 1:mp.get(data) + 1)); 
        current = current.next; 
    } 

    // Find min frequency 
    current = head; 
    int min_frequency = Integer.MAX_VALUE, countMin = 0; 
    for (Map.Entry<Integer,Integer> it :mp.entrySet())  
    { 
        if (it.getValue() <= min_frequency) 
        { 
            min_frequency = it.getValue(); 
        } 
    } 

    // Find count of min frequency elements 
    for (Map.Entry<Integer,Integer> it :mp.entrySet())  
    { 
        if (it.getValue() == min_frequency) 
        { 
            countMin += (it.getValue()); 
        } 
    } 

    return countMin; 
} 

/* Driver code*/
public static void main(String args[]) 
{ 
    /* Start with the empty list */
    Node head = null; 
    int x = 21; 

    /* Use push() to construct below list  
    10.10.11.30.10 */
    head = push(head, 10); 
    head = push(head, 30); 
    head = push(head, 11); 
    head = push(head, 10); 
    head = push(head, 10); 

    System.out.println( countMinimum(head) ); 
} 
} 

// This code is contributed by andrew1234 

```

## Python3

```py

# Python3 program to find count of minimum  
# frequqncy elements in Linked list  
import sys 
import math 

# Link list node 
class Node: 
    def __init__(self,data): 
        self.data = data 
        self.next = None

# Given a reference (pointer to pointer) to the head  
# of a list and an int, push a new node on the front  
# of the list.  
def push(head,data): 
    if not head: 
        return Node(data) 
    temp = Node(data) 
    temp.next = head 
    head = temp 
    return head 

# Function to count minimum frequency elements  
# in the linked list  
def countMinimun(head): 

    # Store frequencies of all nodes.  
    freq = {} 
    temp = head 
    while(temp): 
        d = temp.data 
        if d in freq: 
            freq[d] = freq.get(d) + 1
        else: 
            freq[d] = 1
        temp = temp.next

    # Find min frequency 
    minimum_freq = sys.maxsize 
    for i in freq: 
        minimum_freq = min(minimum_freq, freq.get(i)) 

    # Find count of min frequency elements  
    countMin = 0
    for i in freq: 
        if freq.get(i) == minimum_freq: 
            countMin += 1
    return countMin 

# Driver program to test count function # 
if __name__=='__main__': 

    # Start with the empty list 
    head = None

    # Use push() to construct below list  
    #10->10->11->30->10  
    head = push(head,10) 
    head = push(head,30) 
    head = push(head,11) 
    head = push(head,10) 
    head = push(head,10) 

    print(countMinimun(head)) 

# This code is Contribute by Vikash Kumar 37 

```

## C#

```cs

// C# program to find count of minimum 
// frequqncy elements in Linked list 
using System; 
using System.Collections.Generic; 

class GFG 
{ 

/* Link list node */
public class Node { 
    public int key; 
    public Node next; 
}; 

/* Given a reference (pointer to pointer) to the head  
of a list and an int, push a new node on the front  
of the list. */
static Node push(Node head_ref, int new_key) 
{ 
    Node new_node = new Node(); 
    new_node.key = new_key; 
    new_node.next = (head_ref); 
    head_ref = new_node; 
    return head_ref; 
} 

// Function to count minimum frequency elements 
// in the linked list 
static int countMinimum( Node head) 
{ 
    // Store frequencies of all nodes. 
    IDictionary<int,int> mp = new Dictionary<int,int>(); 

    Node current = head; 
    while (current != null) 
    { 
        int data = current.key; 
        int val = 0; 
        mp[data] = (!mp.TryGetValue(data,out val)  ? 1:mp[data]+ 1); 
        current = current.next; 
    } 

    // Find min frequency 
    current = head; 
    int min_frequency = int.MaxValue, countMin = 0; 
    foreach (KeyValuePair<int, int> it in mp)  
    { 
        if (it.Value <= min_frequency) 
        { 
            min_frequency = it.Value; 
        } 
    } 

    // Find count of min frequency elements 
    foreach (KeyValuePair<int, int> it in mp)  
    { 
        if (it.Value == min_frequency) 
        { 
            countMin += (it.Value); 
        } 
    } 

    return countMin; 
} 

/* Driver code*/
public static void Main() 
{ 
    /* Start with the empty list */
    Node head = null; 
    int x = 21; 

    /* Use push() to construct below list  
    10.10.11.30.10 */
    head = push(head, 10); 
    head = push(head, 30); 
    head = push(head, 11); 
    head = push(head, 10); 
    head = push(head, 10); 

    Console.WriteLine( countMinimum(head) ); 
} 
} 

// This code is contributed by SoumikMondal 

```

**输出**：

```
2

```

**时间复杂度**：`O(n)`



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。