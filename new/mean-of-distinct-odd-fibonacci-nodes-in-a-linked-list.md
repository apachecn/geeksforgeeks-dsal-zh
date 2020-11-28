# 链表中不同的斐波那契奇数结点的平均值

> 原文：[https://www.geeksforgeeks.org/mean-of-distinct-odd-fibonacci-nodes-in-a-linked-list/](https://www.geeksforgeeks.org/mean-of-distinct-odd-fibonacci-nodes-in-a-linked-list/)

给定一个包含`N`个节点的[单链表](https://www.geeksforgeeks.org/data-structures/linked-list/singly-linked-list/)，任务是从该列表中找到其数据值为[奇数斐波那契数](https://www.geeksforgeeks.org/check-number-fibonacci-number/)的所有不同节点的[均值](https://www.geeksforgeeks.org/program-for-mean-and-median-of-an-unsorted-array/)。

**示例**：

> **输入**：`LL = 5 -> 21 -> 8 -> 12 -> 3 -> 13 -> 144 -> 6`
>
> **输出** 10.5
>
> **说明**：
>
> 链表中存在的斐波那契节点是`{5, 21, 8, 3, 13, 144}`
>
> 奇数斐波那契节点 列表是`{5, 21, 3, 13}`
>
> 奇数斐波那契结点数是 4
>
> 因此，奇数斐波那契结点值的平均值为`(5 + 21 + 3 + 13) / 4 = 10.5`
> 
> **输入**：`LL = 55 -> 3 -> 91 -> 89─> 76 -> 233 -> 34 -> 87 -> 5 -> 100`
>
> **输出**：77
>
> **说明**：
>
> 链表中存在的斐波纳契结点是`{55, 3, 89, 233, 34 , 5}`
>
> 链表中存在的奇数斐波那契节点是`{55, 3, 89, 233, 5}`
>
> 奇数斐波那契节点数是 5
>
> 因此，奇数斐波那契节点值为`(55 + 5 + 3 + 89 + 233) / 5 = 77`

**方法**：想法是使用[散列](https://www.geeksforgeeks.org/hashing-data-structure/)预先计算并存储所有[斐波那契数](https://www.geeksforgeeks.org/check-number-fibonacci-number/)，直到链表中的最大元素。

请按照以下步骤解决问题：](https://www.geeksforgeeks.org/find-smallest-largest-elements-singly-linked-list/)

1.  初始化两个变量，例如`cnt`和`sum`，分别存储奇数[斐波那契节点](https://www.geeksforgeeks.org/check-number-fibonacci-number/)的计数和所有奇数[斐波那契节点](https://www.geeksforgeeks.org/check-number-fibonacci-number/)的计数。

2.  [遍历单个链表](https://www.geeksforgeeks.org/linked-list-set-1-introduction/)并存储链表中[最大的元素](https://www.geeksforgeeks.org/find-smallest-largest-elements-singly-linked-list/)，例如`Max`。

3.  创建一个[集合](https://www.geeksforgeeks.org/set-in-cpp-stl/)，例如说`Hashmap`，以存储直到`Max`为止的所有斐波那契数。

4.  [遍历链表](https://www.geeksforgeeks.org/linked-list-set-1-introduction/)，并检查当前节点是否为[奇数](https://www.geeksforgeeks.org/check-whether-given-number-even-odd/)和[斐波那契数](https://www.geeksforgeeks.org/check-number-fibonacci-number/)。 如果发现是真的，则增加`cnt`的值，并将当前节点的数据值加到`sum`中，然后从`Hashmap`中删除该节点。

5.  最后，将`sum / cnt`的值打印为所需答案。

下面是上述方法的实现：

## C++

```cpp

// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Structure of a
// singly Linked List
struct Node {

    // Stores data value
    // of a Node
    int data;

    // Stores pointer 
    // to next Node
    Node* next;
};

// Function to insert a node at the
// beginning of the singly Linked List
void push(Node** head_ref, int new_data)
{

    // Create a new Node
    Node* new_node = new Node;

    // Insert the data into 
    // the Node
    new_node->data = new_data;

    // Insert pointer to
    // the next Node
    new_node->next = (*head_ref);

    // Update head_ref
    (*head_ref) = new_node;
}

// Function to find the largest
// element from the linked list
int largestElement(struct Node* head_ref)
{
    // Stores the largest element 
    // in the linked list
    int Max = INT_MIN;

    Node* head = head_ref;

    // Iterate over the linked list
    while (head != NULL) {

        // If max is less than
        // head->data
        if (Max < head->data) {

            // Update  max
            Max = head->data;
        }

        // Update head
        head = head->next;
    }
    return Max;
}

// Function to store all Fibonacci numbers 
// up to the largest element of the list
set<int> createHashMap(int Max)
{

    // Store all Fibonacci numbers
    // up to Max
    set<int> hashmap;

    // Stores first element of 
    // Fibonacci number
    int prev = 0;

    // Stores second element of
    // Fibonacci number
    int curr = 1;

    // Insert prev into hashmap
    hashmap.insert(prev);

    // Insert curr into hashmap
    hashmap.insert(curr);

    // Insert all elements of
    // Fibonacci numbers up to Max
    while (curr <= Max) {

        // Stores current fibonacci number
        int temp = curr + prev;

        // Insert temp into hashmap
        hashmap.insert(temp);

        // Update prev
        prev = curr;

        // Update curr
        curr = temp;
    }
    return hashmap;
}

// Function to find the mean
// of odd Fibonacci nodes
double meanofnodes(struct Node* head)
{
    // Stores the largest element 
    // in the linked list
    int Max = largestElement(head);

    // Stores all fibonacci numbers 
    // up to Max
    set<int> hashmap 
           = createHashMap(Max);

    // Stores current node
    // of linked list
    Node* curr = head;

    // Stores count of
    // odd Fibonacci nodes
    int cnt = 0;

    // Stores sum of all 
    // odd fibonacci nodes
    double sum = 0.0;

    // Traverse the linked list
    while (curr != NULL) {

        // if the data value of 
        // current node is an odd number
        if ((curr->data) & 1){

            // if data value of the node
            // is present in hashmap
            if (hashmap.count(curr->data)) {

                // Update cnt
                cnt++;

                // Update sum
                sum += curr->data;

                // Remove current fibonacci number
                // from hashmap so that duplicate
                // elements can't be counted
                hashmap.erase(curr->data);
            }

        }

        // Update curr
        curr = curr->next;
    }

    // Return the required mean
    return (sum / cnt);
}

// Driver Code
int main()
{   
    // Stores head node of
    // the linked list
    Node* head = NULL;

    // Insert all data values 
    // in the linked list
    push(&head, 5);
    push(&head, 21);
    push(&head, 8);
    push(&head, 12);
    push(&head, 3);
    push(&head, 13);
    push(&head, 144);
    push(&head, 6);

    cout<<meanofnodes(head);

    return 0;
}

```

## Java

```java

// Java program to implement
// the above approach
import java.util.*;
class GFG{

// Structure of a
// singly Linked List
static class Node 
{
  // Stores data value
  // of a Node
  int data;

  // Stores pointer 
  // to next Node
  Node next;
};

static Node head;

// Function to insert a 
// node at the beginning 
// of the singly Linked List
static Node push(Node head_ref, 
                 int new_data)
{
  // Create a new Node
  Node new_node = new Node();

  // Insert the data into 
  // the Node
  new_node.data = new_data;

  // Insert pointer to
  // the next Node
  new_node.next = head_ref;

  // Update head_ref
  head_ref = new_node;
  return head_ref;
}

// Function to find the largest
// element from the linked list
static int largestElement(Node head_ref)
{
  // Stores the largest element 
  // in the linked list
  int Max = Integer.MIN_VALUE;

  Node head = head_ref;

  // Iterate over the 
  // linked list
  while (head != null)
  {
    // If max is less than
    // head.data
    if (Max < head.data) 
    {
      // Update  max
      Max = head.data;
    }

    // Update head
    head = head.next;
  }
  return Max;
}

// Function to store all
// Fibonacci numbers up 
// to the largest element 
// of the list
static HashSet<Integer> 
       createHashMap(int Max)
{    
  // Store all Fibonacci
  // numbers up to Max
  HashSet<Integer> hashmap = 
          new HashSet<>();

  // Stores first element of 
  // Fibonacci number
  int prev = 0;

  // Stores second element of
  // Fibonacci number
  int curr = 1;

  // Insert prev into hashmap
  hashmap.add(prev);

  // Insert curr into hashmap
  hashmap.add(curr);

  // Insert all elements of
  // Fibonacci numbers up 
  // to Max
  while (curr <= Max) 
  {
    // Stores current fibonacci 
    // number
    int temp = curr + prev;

    // Insert temp into hashmap
    hashmap.add(temp);

    // Update prev
    prev = curr;

    // Update curr
    curr = temp;
  }
  return hashmap;
}

// Function to find the mean
// of odd Fibonacci nodes
static double meanofnodes()
{
  // Stores the largest element 
  // in the linked list
  int Max = largestElement(head);

  // Stores all fibonacci numbers 
  // up to Max
  HashSet<Integer> hashmap = 
          createHashMap(Max);

  // Stores current node
  // of linked list
  Node curr = head;

  // Stores count of
  // odd Fibonacci nodes
  int cnt = 0;

  // Stores sum of all 
  // odd fibonacci nodes
  double sum = 0.0;

  // Traverse the linked list
  while (curr != null) 
  {
    // if the data value of 
    // current node is an
    // odd number
    if ((curr.data) %2== 1)
    {
      // if data value of the node
      // is present in hashmap
      if (hashmap.contains(curr.data)) 
      {
        // Update cnt
        cnt++;

        // Update sum
        sum += curr.data;

        // Remove current fibonacci 
        // number from hashmap so that 
        // duplicate elements can't be 
        // counted
        hashmap.remove(curr.data);
      }

    }

    // Update curr
    curr = curr.next;
  }

  // Return the required mean
  return (sum / cnt);
}

// Driver Code
public static void main(String[] args)
{   
  // Stores head node of
  // the linked list
  head = null;

  // Insert all data values 
  // in the linked list
  head = push(head, 5);
  head = push(head, 21);
  head = push(head, 8);
  head = push(head, 12);
  head = push(head, 3);
  head = push(head, 13);
  head = push(head, 144);
  head = push(head, 6);

  System.out.print(meanofnodes());
}
}

// This code is contributed by 29AjayKumar

```

## C#

```cs

// C# program to implement
// the above approach
using System;
using System.Collections.Generic;

class GFG{

// Structure of a
// singly Linked List
public class Node 
{

  // Stores data value
  // of a Node
  public int data;

  // Stores pointer 
  // to next Node
  public Node next;
};

static Node head;

// Function to insert a 
// node at the beginning 
// of the singly Linked List
static Node push(Node head_ref, 
                 int new_data)
{

  // Create a new Node
  Node new_node = new Node();

  // Insert the data into 
  // the Node
  new_node.data = new_data;

  // Insert pointer to
  // the next Node
  new_node.next = head_ref;

  // Update head_ref
  head_ref = new_node;
  return head_ref;
}

// Function to find the largest
// element from the linked list
static int largestElement(Node head_ref)
{

  // Stores the largest element 
  // in the linked list
  int Max = int.MinValue;

  Node head = head_ref;

  // Iterate over the 
  // linked list
  while (head != null)
  {

    // If max is less than
    // head.data
    if (Max < head.data) 
    {

      // Update  max
      Max = head.data;
    }

    // Update head
    head = head.next;
  }
  return Max;
}

// Function to store all
// Fibonacci numbers up 
// to the largest element 
// of the list
static HashSet<int> createDictionary(int Max)
{   

  // Store all Fibonacci
  // numbers up to Max
  HashSet<int> hashmap = new HashSet<int>();

  // Stores first element of 
  // Fibonacci number
  int prev = 0;

  // Stores second element of
  // Fibonacci number
  int curr = 1;

  // Insert prev into hashmap
  hashmap.Add(prev);

  // Insert curr into hashmap
  hashmap.Add(curr);

  // Insert all elements of
  // Fibonacci numbers up 
  // to Max
  while (curr <= Max) 
  {

    // Stores current fibonacci 
    // number
    int temp = curr + prev;

    // Insert temp into hashmap
    hashmap.Add(temp);

    // Update prev
    prev = curr;

    // Update curr
    curr = temp;
  }
  return hashmap;
}

// Function to find the mean
// of odd Fibonacci nodes
static double meanofnodes()
{

  // Stores the largest element 
  // in the linked list
  int Max = largestElement(head);

  // Stores all fibonacci numbers 
  // up to Max
  HashSet<int> hashmap = createDictionary(Max);

  // Stores current node
  // of linked list
  Node curr = head;

  // Stores count of
  // odd Fibonacci nodes
  int cnt = 0;

  // Stores sum of all 
  // odd fibonacci nodes
  double sum = 0.0;

  // Traverse the linked list
  while (curr != null) 
  {

    // if the data value of 
    // current node is an
    // odd number
    if ((curr.data) % 2 == 1)
    {

      // if data value of the node
      // is present in hashmap
      if (hashmap.Contains(curr.data)) 
      {

        // Update cnt
        cnt++;

        // Update sum
        sum += curr.data;

        // Remove current fibonacci 
        // number from hashmap so that 
        // duplicate elements can't be 
        // counted
        hashmap.Remove(curr.data);
      }

    }

    // Update curr
    curr = curr.next;
  }

  // Return the required mean
  return (sum / cnt);
}

// Driver Code
public static void Main(String[] args)
{   

  // Stores head node of
  // the linked list
  head = null;

  // Insert all data values 
  // in the linked list
  head = push(head, 5);
  head = push(head, 21);
  head = push(head, 8);
  head = push(head, 12);
  head = push(head, 3);
  head = push(head, 13);
  head = push(head, 144);
  head = push(head, 6);

  Console.Write(meanofnodes());
}
}

// This code is contributed by Amit Katiyar

```

**输出**： 

```
10.5

```

**时间复杂度**：`O(n)`

**辅助空间**：`O(n)`



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。