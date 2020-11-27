# 链表中其值等于其频率的节点数

> 原文：[https://www.geeksforgeeks.org/count-of-nodes-in-a-linkedlist-whose-value-is-equal-to-their-frequency/](https://www.geeksforgeeks.org/count-of-nodes-in-a-linkedlist-whose-value-is-equal-to-their-frequency/)

给定一个单链列表，任务是计算其数据值等于其频率的节点数。

**示例**：

> **输入**：`list = 2 -> 3 -> 3 -> 3 -> 4 -> 2`
>
> **输出**：2
>
> 元素 2 的频率为 2
>
> 元素 3 的频率为 3
>
> 元素 4 的频率为 1
>
> 因此，2 和 3 是具有与其值相同频率的元素
>
> **输入**：`list = 1 -> 2 -> 3 -> 4 -> 5 -> 6`
>
> **输出**：1

**方法**：

解决此问题的方法如下

*   遍历链表并使用映射存储数组每个元素的频率

*   遍历映射并计算其频率等于其值的元素的数量

下面是上述方法的实现：

## C++

```cpp

/* Link list node */
#include <bits/stdc++.h>
using namespace std;

class Node {
public:
    int data;
    Node* next;
};

// Function to add a node at the 
// beginning of List
void push(Node** head_ref, int data)  
{  
    /* allocate node */
    Node* new_node =new Node(); 

    /* put in the data */
    new_node->data = data;  

    // link the old list off the new
    // node
    new_node->next = (*head_ref);  

    // move the head to point to the
    // new node
    (*head_ref) = new_node;  
} 

// Counts the no. of occurences of a
// node in a linked list
int countValuesWithSameFreq(Node* start)
{
    map<int, int> mpp;
    Node* current = start;
    int count = 0;
    while (current != NULL) {
        mpp[current->data] += 1;
        current = current->next;
    }
    int ans = 0;
    for (auto x : mpp) {
        int value = x.first;
        int freq = x.second;

        // Check if value equls to frequency
        // and increment the count
        if (value == freq) {
            ans++;
        }
    }
    return ans;
}

// main program
int main()
{
    Node* head = NULL;
    push(&head, 3);
    push(&head, 4);
    push(&head, 3);
    push(&head, 2);
    push(&head, 2);
    push(&head, 3);

    cout << countValuesWithSameFreq(head);
    return 0;
}

```

## Java

```java

/* Link list node */
import java.util.*;

class GFG{

public static class Node
{
    int data;
    Node next;
};

// Function to add a node at the
// beginning of List
static Node push(Node head_ref, int data)
{

    // Allocate node 
    Node new_node = new Node();

    // Put in the data 
    new_node.data = data;

    // Link the old list off the new
    // node
    new_node.next = head_ref;

    // Move the head to point to the
    // new node
    head_ref = new_node;
    return head_ref;
}

// Counts the no. of occurences of a
// node in a linked list
static int countValuesWithSameFreq(Node start)
{
    HashMap<Integer, Integer> mpp = new HashMap<>();

    Node current = start;
    while (current != null)
    {
        if (mpp.containsKey(current.data)) 
        {
            mpp.put(current.data,
                     mpp.get(current.data) + 1);
        }
        else
        {
            mpp.put(current.data, 1);
        }
        current = current.next;
    }
    int ans = 0;
    for(Map.Entry<Integer, 
                  Integer> x : mpp.entrySet())
    {
        int value = x.getKey();
        int freq = x.getValue();

        // Check if value equls to frequency
        // and increment the count
        if (value == freq)
        {
            ans++;
        }
    }
    return ans;
}

// Driver code 
public static void main(String[] args)
{
    Node head = null;
    head = push(head, 3);
    head = push(head, 4);
    head = push(head, 3);
    head = push(head, 2);
    head = push(head, 2);
    head = push(head, 3);

    System.out.print(countValuesWithSameFreq(head));
}
}

// This code is contributed by amal kumar choubey

```

## C#

```cs

/* Link list node */
using System;
using System.Collections.Generic;

class GFG{

public class Node
{
    public int data;
    public Node next;
};

// Function to add a node at the
// beginning of List
static Node push(Node head_ref, int data)
{

    // Allocate node 
    Node new_node = new Node();

    // Put in the data 
    new_node.data = data;

    // Link the old list off the new
    // node
    new_node.next = head_ref;

    // Move the head to point to the
    // new node
    head_ref = new_node;
    return head_ref;
}

// Counts the no. of occurences of a
// node in a linked list
static int countValuesWithSameFreq(Node start)
{
    Dictionary<int, 
                 int> mpp = new Dictionary<int, 
                                           int>();

    Node current = start;
    while (current != null)
    {
        if (mpp.ContainsKey(current.data)) 
        {
            mpp[current.data] = mpp[current.data] + 1;
        }
        else
        {
            mpp.Add(current.data, 1);
        }
        current = current.next;
    }
    int ans = 0;

    foreach(KeyValuePair<int, int> x in mpp)
    {
        int value = x.Key;
        int freq = x.Value;

        // Check if value equls to frequency
        // and increment the count
        if (value == freq)
        {
            ans++;
        }
    }
    return ans;
}

// Driver code 
public static void Main(String[] args)
{
    Node head = null;
    head = push(head, 3);
    head = push(head, 4);
    head = push(head, 3);
    head = push(head, 2);
    head = push(head, 2);
    head = push(head, 3);

    Console.Write(countValuesWithSameFreq(head));
}
}

// This code is contributed by Rohit_ranjan

```

**输出**：

```
2

```

**复杂度分析**：

**时间复杂度**：对于大小为`n`的给定链表，我们对其进行一次迭代。 因此，此解决方案的时间复杂度为`O(n)`。

**空间复杂度**：对于大小为`n`的给定链表，我们使用了一个额外的 映射最多可以具有`n`个键值，因此此解决方案的空间复杂度为`O(n)`。



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。