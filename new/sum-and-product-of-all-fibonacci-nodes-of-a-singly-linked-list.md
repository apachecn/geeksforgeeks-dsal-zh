# 单链接列表

的所有斐波那契节点的总和与乘积

给定一个包含 **N 个**节点的[单链列表](https://www.geeksforgeeks.org/data-structures/linked-list/singly-linked-list/)，任务是从列表中找到其数据值为斐波那契数的所有节点的和与积。

**示例：**

> **输入：** LL = 15-> 16-> 8-> 6-> 13
> **输出：**总和= 21，乘积= 104
> **说明：**
> 该列表包含 2 个斐波那契数据值 8 和 13。
> 因此：
> 总和= 8 + 13 = 21
> 乘积= 8 * 13 = 104
> 
> **输入：** LL = 5-> 3-> 4-> 2-> 9
> **输出：**总和= 10，乘积= 30
> **说明：**
> 该列表包含 3 个斐波那契数据值 5、3 和 2。
> 因此：
> 总和= 5 + 3 + 2 = 10
> 乘积= 5 * 3 * 2 = 30

**方法：**的想法是使用[哈希](http://www.geeksforgeeks.org/hashing-data-structure/)来预先计算并存储[斐波那契数](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)，然后检查节点是否在 O（1）时间中包含斐波那契值 。

1.  遍历整个[链接列表](http://www.geeksforgeeks.org/data-structures/linked-list/)，并获得列表中的最大值。
2.  现在，为了检查斐波那契数，建立一个[哈希表](https://www.geeksforgeeks.org/hashing-set-1-introduction/)，其中包含所有小于或等于链接列表中最大值的斐波那契数。
3.  最后，一个接一个地遍历链表中的节点，并检查该节点是否包含斐波那契数作为其数据值。 求出斐波那契节点的数据之和与乘积。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation to find the sum and
// product of all of the Fibonacci nodes
// in a singly linked list

#include <bits/stdc++.h>

using namespace std;

// Node of the singly linked list
struct Node {
    int data;
    Node* next;
};

// Function to insert a node
// at the beginning
// of the singly Linked List
void push(Node** head_ref, int new_data)
{
    // Allocate new node
    Node* new_node
        = (Node*)malloc(
            sizeof(struct Node));

    // Insert the data
    new_node->data = new_data;

    // Link the old list
    // to the new node
    new_node->next = (*head_ref);

    // Move the head to
    // point the new node
    (*head_ref) = new_node;
}

// Function that returns
// the largest element
// from the linked list.
int largestElement(
    struct Node* head_ref)
{
    // Declare a max variable
    // and initialize with INT_MIN
    int max = INT_MIN;

    Node* head = head_ref;

    // Check loop while
    // head not equal to NULL
    while (head != NULL) {

        // If max is less then head->data
        // then assign value of head->data
        // to max otherwise
        // node points to next node.
        if (max < head->data)
            max = head->data;

        head = head->next;
    }
    return max;
}

// Function to create a hash table
// to check Fibonacci numbers
void createHash(set<int>& hash,
                int maxElement)
{
    // Inserting the first
    // two numbers in the hash
    int prev = 0, curr = 1;
    hash.insert(prev);
    hash.insert(curr);

    // Loop to add Fibonacci numbers upto
    // the maximum element present in the
    // linked list
    while (curr <= maxElement) {
        int temp = curr + prev;
        hash.insert(temp);
        prev = curr;
        curr = temp;
    }
}

// Function to find
// the required sum and product
void sumAndProduct(Node* head_ref)
{
    // Find the largest node value
    // in Singly Linked List
    int maxEle
        = largestElement(head_ref);

    // Creating a set containing
    // all the fibonacci numbers
    // upto the maximum data value
    // in the Singly Linked List
    set<int> hash;
    createHash(hash, maxEle);

    int prod = 1;
    int sum = 0;

    Node* ptr = head_ref;

    // Traverse the linked list
    while (ptr != NULL) {

        // If current node is fibonacci
        if (hash.find(ptr->data)
            != hash.end()) {

            // Find the sum and the product
            prod *= ptr->data;
            sum += ptr->data;
        }

        ptr = ptr->next;
    }

    cout << "Sum = " << sum << endl;
    cout << "Product = " << prod;
}

// Driver code
int main()
{

    Node* head = NULL;

    // Create the linked list
    // 15 -> 16 -> 8 -> 6 -> 13
    push(&head, 13);
    push(&head, 6);
    push(&head, 8);
    push(&head, 16);
    push(&head, 15);

    sumAndProduct(head);

    return 0;
}

```

## Java

```java

// Java implementation to find the sum and
// product of all of the Fibonacci nodes
// in a singly linked list
import java.util.*;

class GFG{

// Node of the singly linked list
static class Node {
    int data;
    Node next;
};

// Function to insert a node
// at the beginning
// of the singly Linked List
static Node push(Node head_ref, int new_data)
{
    // Allocate new node
    Node new_node = new Node();

    // Insert the data
    new_node.data = new_data;

    // Link the old list
    // to the new node
    new_node.next = head_ref;

    // Move the head to
    // point the new node
    head_ref = new_node;
    return head_ref;
}

// Function that returns
// the largest element
// from the linked list.
static int largestElement(
    Node head_ref)
{
    // Declare a max variable
    // and initialize with Integer.MIN_VALUE
    int max = Integer.MIN_VALUE;

    Node head = head_ref;

    // Check loop while
    // head not equal to null
    while (head != null) {

        // If max is less then head.data
        // then assign value of head.data
        // to max otherwise
        // node points to next node.
        if (max < head.data)
            max = head.data;

        head = head.next;
    }
    return max;
}

// Function to create a hash table
// to check Fibonacci numbers
static void createHash(HashSet<Integer> hash,
                int maxElement)
{
    // Inserting the first
    // two numbers in the hash
    int prev = 0, curr = 1;
    hash.add(prev);
    hash.add(curr);

    // Loop to add Fibonacci numbers upto
    // the maximum element present in the
    // linked list
    while (curr <= maxElement) {
        int temp = curr + prev;
        hash.add(temp);
        prev = curr;
        curr = temp;
    }
}

// Function to find
// the required sum and product
static void sumAndProduct(Node head_ref)
{
    // Find the largest node value
    // in Singly Linked List
    int maxEle
        = largestElement(head_ref);

    // Creating a set containing
    // all the fibonacci numbers
    // upto the maximum data value
    // in the Singly Linked List
    HashSet<Integer> hash = new HashSet<Integer>();
    createHash(hash, maxEle);

    int prod = 1;
    int sum = 0;

    Node ptr = head_ref;

    // Traverse the linked list
    while (ptr != null) {

        // If current node is fibonacci
        if (hash.contains(ptr.data)) {

            // Find the sum and the product
            prod *= ptr.data;
            sum += ptr.data;
        }

        ptr = ptr.next;
    }

    System.out.print("Sum = " +  sum +"\n");
    System.out.print("Product = " +  prod);
}

// Driver code
public static void main(String[] args)
{

    Node head = null;

    // Create the linked list
    // 15.16.8.6.13
    head = push(head, 13);
    head = push(head, 6);
    head = push(head, 8);
    head = push(head, 16);
    head = push(head, 15);

    sumAndProduct(head);
}
}

// This code is contributed by Rajput-Ji

```

## Python3

```py

# Python3 implementation to find the sum and
# product of all of the Fibonacci nodes
# in a singly linked list
import sys

# Node of the singly linked list
class Node():

    def __init__(self, data):

        self.data = data
        self.next = None

# Function to insert a node
# at the beginning of the 
# singly Linked List
def push(head_ref, new_data):

    # Allocate new node
    new_node = Node(new_data)

    # Link the old list
    # to the new node
    new_node.next = head_ref

    # Move the head to
    # point the new node
    head_ref = new_node

    return head_ref

# Function that returns
# the largest element
# from the linked list.
def largestElement(head_ref):

    # Declare a max variable
    # and initialize with INT_MIN
    max = -sys.maxsize

    head = head_ref

    # Check loop while
    # head not equal to NULL
    while (head != None):

        # If max is less then head->data
        # then assign value of head->data
        # to max otherwise
        # node points to next node.
        if (max < head.data):
            max = head.data

        head = head.next

    return max

# Function to create a hash table
# to check Fibonacci numbers
def createHash(hash, maxElement):

    # Inserting the first
    # two numbers in the hash
    prev = 0
    curr = 1

    hash.add(prev)
    hash.add(curr)

    # Loop to add Fibonacci numbers upto
    # the maximum element present in the
    # linked list
    while (curr <= maxElement):
        temp = curr + prev
        hash.add(temp)
        prev = curr
        curr = temp

    return hash

# Function to find the 
# required sum and product
def sumAndProduct(head_ref):

    # Find the largest node value
    # in Singly Linked List
    maxEle = largestElement(head_ref)

    # Creating a set containing
    # all the fibonacci numbers
    # upto the maximum data value
    # in the Singly Linked List
    hash = set()

    hash = createHash(hash, maxEle)

    prod = 1
    sum = 0

    ptr = head_ref

    # Traverse the linked list
    while (ptr != None):

        # If current node is fibonacci
        if ptr.data in hash:

            # Find the sum and the product
            prod *= ptr.data
            sum += ptr.data

        ptr = ptr.next

    print("Sum =", sum)
    print("Product =", prod)

# Driver code
if __name__=="__main__":

    head = None;

    # Create the linked list
    # 15 -> 16 -> 8 -> 6 -> 13
    head = push(head, 13)
    head = push(head, 6)
    head = push(head, 8)
    head = push(head, 16)
    head = push(head, 15)

    sumAndProduct(head)

# This code is contributed by rutvik_56

```

## C#

```cs

// C# implementation to find the sum and
// product of all of the Fibonacci nodes
// in a singly linked list
using System;
using System.Collections.Generic;

class GFG{

// Node of the singly linked list
class Node {
    public int data;
    public Node next;
};

// Function to insert a node
// at the beginning
// of the singly Linked List
static Node push(Node head_ref, int new_data)
{
    // Allocate new node
    Node new_node = new Node();

    // Insert the data
    new_node.data = new_data;

    // Link the old list
    // to the new node
    new_node.next = head_ref;

    // Move the head to
    // point the new node
    head_ref = new_node;
    return head_ref;
}

// Function that returns
// the largest element
// from the linked list.
static int largestElement(
    Node head_ref)
{
    // Declare a max variable
    // and initialize with int.MinValue
    int max = int.MinValue;

    Node head = head_ref;

    // Check loop while
    // head not equal to null
    while (head != null) {

        // If max is less then head.data
        // then assign value of head.data
        // to max otherwise
        // node points to next node.
        if (max < head.data)
            max = head.data;

        head = head.next;
    }
    return max;
}

// Function to create a hash table
// to check Fibonacci numbers
static void createHash(HashSet<int> hash,
                int maxElement)
{
    // Inserting the first
    // two numbers in the hash
    int prev = 0, curr = 1;
    hash.Add(prev);
    hash.Add(curr);

    // Loop to add Fibonacci numbers upto
    // the maximum element present in the
    // linked list
    while (curr <= maxElement) {
        int temp = curr + prev;
        hash.Add(temp);
        prev = curr;
        curr = temp;
    }
}

// Function to find
// the required sum and product
static void sumAndProduct(Node head_ref)
{
    // Find the largest node value
    // in Singly Linked List
    int maxEle
        = largestElement(head_ref);

    // Creating a set containing
    // all the fibonacci numbers
    // upto the maximum data value
    // in the Singly Linked List
    HashSet<int> hash = new HashSet<int>();
    createHash(hash, maxEle);

    int prod = 1;
    int sum = 0;

    Node ptr = head_ref;

    // Traverse the linked list
    while (ptr != null) {

        // If current node is fibonacci
        if (hash.Contains(ptr.data)) {

            // Find the sum and the product
            prod *= ptr.data;
            sum += ptr.data;
        }

        ptr = ptr.next;
    }

    Console.Write("Sum = " +  sum +"\n");
    Console.Write("Product = " +  prod);
}

// Driver code
public static void Main(String[] args)
{

    Node head = null;

    // Create the linked list
    // 15.16.8.6.13
    head = push(head, 13);
    head = push(head, 6);
    head = push(head, 8);
    head = push(head, 16);
    head = push(head, 15);

    sumAndProduct(head);
}
}

// This code is contributed by Princi Singh

```

**Output:** 

```
Sum = 21
Product = 104

```

***时间复杂度：** O（N）*，其中 N 是链​​表中节点的数量。



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。