# 链表

> 原文：[https://www.geeksforgeeks.org/sum-of-all-odd-frequency-nodes-of-the-linked-list/](https://www.geeksforgeeks.org/sum-of-all-odd-frequency-nodes-of-the-linked-list/)

中所有奇数频率节点的总和

给定一个链表，任务是从给定的链表中找到所有奇数频率节点的总和。

**示例**：

> **输入**：8-> 8-> 1-> 4-> 1-> 2-> 8->空
> **输出**：30
> freq（8）= 3
> freq（1）= 2
> freq（4）= 1
> freq（2）= 1
> 8、4 和 2 出现奇数次（8 * 3）+（4 * 1）+（2 * 1）= 30
> 
> **输入**：6-> 2-> 2-> 6-> 2-> 1->空
> **输出**：7

**方法**：此问题可以通过[散列](http://www.geeksforgeeks.org/hashing-data-structure/)解决，

1.  创建一个散列来存储节点的频率。

2.  遍历[链表](http://www.geeksforgeeks.org/data-structures/linked-list/)并更新哈希变量中节点的频率。

3.  现在，再次遍历链表，对出现奇数次的每个节点，将其值加到运行总和中。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation of above approach 
#include<bits/stdc++.h> 
using namespace std; 

// Node class 
struct Node 
{ 
    int data; 
    Node* next; 
    Node(int d) 
    { 
        data = d; 
        next = NULL; 
    }  
} ; 

// Function to push the new node  
// to head of the linked list 
Node* push(Node* head,int data) 
{ 
    // If head is null return new node as head 
    if (!head) 
        return new Node(data); 
    Node* temp =new Node(data); 
    temp->next = head; 
    head = temp; 
    return head; 
} 

// Function to find the sum of all odd  
// frequency nodes of the linked list 
int sumOfOddFreqEle(Node* head) 
{ 
    // Hash to store the frequencies of  
    // the nodes of the linked list 
    map<int,int> mp ; 
    Node* temp = head; 
    while(temp) 
    { 
        int d = temp->data; 
        mp[d]++; 
        temp = temp->next; 
    } 

    // Initialize total_sum as zero  
    int total_sum = 0; 

    // Traverse through the map to get the sum 
    for (auto i : mp)  
    {  

        // If it appears for odd number of  
        // times then add it to the sum 
        if (i.second % 2 == 1) 
            total_sum+=(i.second * i.first); 
    } 
    return total_sum; 
} 

// Driver code 
int main() 
{ 
    Node* head = NULL; 
    head = push(head, 8); 
    head = push(head, 2); 
    head = push(head, 1); 
    head = push(head, 4); 
    head = push(head, 1); 
    head = push(head, 8); 
    head = push(head, 8); 

    cout<<(sumOfOddFreqEle(head)); 

    return 0; 
} 

// This code is contributed by Arnab Kundu 

```

## Java

```java

// Java implementation of the approach 
import java.util.*; 
class GFG  
{ 

// Node class 
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

// Function to push the new node  
// to head of the linked list 
static Node push(Node head,int data) 
{ 
    // If head is null return new node as head 
    if (head == null) 
        return new Node(data); 
    Node temp = new Node(data); 
    temp.next = head; 
    head = temp; 
    return head; 
} 

// Function to find the sum of all odd  
// frequency nodes of the linked list 
static int sumOfOddFreqEle(Node head) 
{ 
    // Hash to store the frequencies of  
    // the nodes of the linked list 
    HashMap<Integer, Integer> mp =  
         new HashMap<Integer, Integer>(); 
    Node temp = head; 
    while(temp != null) 
    { 
        int d = temp.data; 
        if(mp.containsKey(d)) 
        { 
            mp.put(d, mp.get(d) + 1); 
        } 
        else
        { 
            mp.put(d, 1); 
        } 
        temp = temp.next; 
    } 

    // Initialize total_sum as zero  
    int total_sum = 0; 

    // Traverse through the map to get the sum 
    for (Map.Entry<Integer,  
                   Integer> i : mp.entrySet())  
    {  

        // If it appears for odd number of  
        // times then add it to the sum 
        if (i.getValue() % 2 == 1) 
            total_sum+=(i.getValue() * i.getKey()); 
    } 
    return total_sum; 
} 

// Driver code 
public static void main(String[] args) 
{ 
    Node head = null; 
    head = push(head, 8); 
    head = push(head, 2); 
    head = push(head, 1); 
    head = push(head, 4); 
    head = push(head, 1); 
    head = push(head, 8); 
    head = push(head, 8); 

    System.out.println((sumOfOddFreqEle(head))); 
} 
} 

// This code is contributed by Rajput-Ji 

```

## Python

```py

# Python implementation of the approach 

# Node class 
class Node: 
    def __init__(self, data): 
        self.data = data 
        self.next = None

# Function to push the new node  
# to head of the linked list 
def push(head, data): 

    # If head is null return new node as head 
    if not head: 
        return Node(data) 
    temp = Node(data) 
    temp.next = head 
    head = temp 
    return head 

# Function to find the sum of all odd  
# frequency nodes of the linked list 
def sumOfOddFreqEle(head): 

    # Hash to store the frequencies of  
    # the nodes of the linked list 
    mp ={} 
    temp = head 
    while(temp): 
        d = temp.data 
        if d in mp: 
            mp[d]= mp.get(d)+1
        else: 
            mp[d]= 1
        temp = temp.next

    # Initialize total_sum as zero  
    total_sum = 0

    # Traverse through the map to get the sum 
    for digit in mp: 

        # keep tracking the to 
        tms = mp.get(digit) 

        # If it appears for odd number of  
        # times then add it to the sum 
        if tms % 2 == 1: 
            total_sum+=(tms * digit) 
    return total_sum 

# Driver code 
if __name__=='__main__': 
    head = None
    head = push(head, 8) 
    head = push(head, 2) 
    head = push(head, 1) 
    head = push(head, 4) 
    head = push(head, 1) 
    head = push(head, 8) 
    head = push(head, 8) 

    print(sumOfOddFreqEle(head)) 

```

## C#

```cs

// C# implementation of the approach 
using System; 
using System.Collections.Generic; 

class GFG  
{ 

// Node class 
public class Node 
{ 
    public int data; 
    public Node next; 
    public Node(int d) 
    { 
        data = d; 
        next = null; 
    }  
}; 

// Function to push the new node  
// to head of the linked list 
static Node push(Node head,int data) 
{ 
    // If head is null,  
    // return new node as head 
    if (head == null) 
        return new Node(data); 
    Node temp = new Node(data); 
    temp.next = head; 
    head = temp; 
    return head; 
} 

// Function to find the sum of all odd  
// frequency nodes of the linked list 
static int sumOfOddFreqEle(Node head) 
{ 
    // Hash to store the frequencies of  
    // the nodes of the linked list 
    Dictionary<int,  
               int> mp = new Dictionary<int,  
                                        int>(); 
    Node temp = head; 
    while(temp != null) 
    { 
        int d = temp.data; 
        if(mp.ContainsKey(d)) 
        { 
            mp[d] = mp[d] + 1; 
        } 
        else
        { 
            mp.Add(d, 1); 
        } 
        temp = temp.next; 
    } 

    // Initialize total_sum as zero  
    int total_sum = 0; 

    // Traverse through the map to get the sum 
    foreach(KeyValuePair<int, int> i in mp) 
    {  

        // If it appears for odd number of  
        // times then add it to the sum 
        if (i.Value % 2 == 1) 
            total_sum += (i.Value * i.Key); 
    } 
    return total_sum; 
} 

// Driver code 
public static void Main(String[] args) 
{ 
    Node head = null; 
    head = push(head, 8); 
    head = push(head, 2); 
    head = push(head, 1); 
    head = push(head, 4); 
    head = push(head, 1); 
    head = push(head, 8); 
    head = push(head, 8); 

    Console.WriteLine((sumOfOddFreqEle(head))); 
} 
} 

// This code is contributed by Rajput-Ji 

```

**Output:**

```
30

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。