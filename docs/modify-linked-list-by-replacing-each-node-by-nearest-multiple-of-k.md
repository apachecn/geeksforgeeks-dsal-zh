# 通过用 K 的最近倍数替换每个节点来修改链表

> 原文:[https://www . geesforgeks . org/modify-linked-list-by-replace-每个节点由 k 的最近倍数计算/](https://www.geeksforgeeks.org/modify-linked-list-by-replacing-each-node-by-nearest-multiple-of-k/)

给定一个由 **N** 个节点和一个整数 **K** 组成的[单链表](https://www.geeksforgeeks.org/data-structures/linked-list/singly-linked-list/) **L** ，任务是将给定链表的每个节点的值修改为其最接近的倍数 **K** ，不超过该节点的值。

**示例:**

> **输入:** LL: 1 - > 2 - > 3 - > 5，K = 2
> **输出:**0->2->2->4
> **解释:**
> 合成 LL 的值小于原始 LL 值，是 K 的倍数(= 2)。
> 
> **输入:**LL:13->14->26->29->40，K = 13
> **输出:**13->13->26->26->39

**方法:**给定的问题可以通过[遍历给定的链表](https://www.geeksforgeeks.org/recursive-insertion-and-traversal-linked-list/)来解决，对于遍历的每个节点，找到**节点值**除以 **K** 的地板值 **val** ，并将节点值更新为 **val*K** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <iostream>
using namespace std;

// Structure of node
struct node {
    int data;
    node* next;
};

// Function to replace the node N
// by the nearest multiple of K
node* EvalNearestMult(node* N, int K)
{
    node* temp = N;
    int t;

    // Traverse the Linked List
    while (N != NULL) {

        // If data is less than K
        if (N->data < K)
            N->data = 0;

        else {

            // If the data of current
            // node is same as K
            if (N->data == K)
                N->data = K;

            // Otherwise change the value
            else {
                N->data = (N->data / K) * K;
            }
        }

        // Move to the next node
        N = N->next;
    }

    // Return the updated LL
    return temp;
}

// Function to print the nodes of
// the Linked List
void printList(node* N)
{
    // Traverse the LL
    while (N != NULL) {

        // Print the node's data
        cout << N->data << "  ";
        N = N->next;
    }
}

// Driver Code
int main()
{
    // Given Linked List
    node* head = NULL;
    node* second = NULL;
    node* third = NULL;

    head = new node();
    second = new node();
    third = new node();

    head->data = 3;
    head->next = second;
    second->data = 4;
    second->next = third;
    third->data = 8;
    third->next = NULL;

    node* t = EvalNearestMult(head, 3);

    printList(t);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;

class GFG {

    // Structure of node
    static class node {
        int data;
        node next;

        node(int d)
        {
            data = d;
        }
    }

    // Function to replace the node N
    // by the nearest multiple of K
    static node EvalNearestMult(node N, int K)
    {
        node temp = N;
        int t;

        // Traverse the Linked List
        while (N != null) {

            // If data is less than K
            if (N.data < K)
                N.data = 0;

            else {

                // If the data of current
                // node is same as K
                if (N.data == K)
                    N.data = K;

                // Otherwise change the value
                else {
                    N.data = (N.data / K) * K;
                }
            }

            // Move to the next node
            N = N.next;
        }

        // Return the updated LL
        return temp;
    }

    // Function to print the nodes of
    // the Linked List
    static void printList(node N)
    {
        // Traverse the LL
        while (N != null) {

            // Print the node's data
            System.out.print(N.data + "  ");
            N = N.next;
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        // Given Linked List
        node head = new node(3);
        head.next = new node(5);
          head.next.next = new node(8);

        node t = EvalNearestMult(head, 3);

        printList(t);
    }
}

// This code is contributed by Dharanendra L V
```

## 蟒蛇 3

```
# Python program for the above approach

# Structure of Node
class Node:
    def __init__(self, data):
        self.data = data;
        self.next = None;

# Function to replace the Node N
# by the nearest multiple of K
def EvalNearestMult(N, K):
    temp = N;
    t;

    # Traverse the Linked List
    while (N != None):

        # If data is less than K
        if (N.data < K):
            N.data = 0;

        else:

            # If the data of current
            # Node is same as K
            if (N.data == K):
                N.data = K;

            # Otherwise change the value
            else:
                N.data = (N.data // K) * K;

        # Move to the next Node
        N = N.next;

    # Return the updated LL
    return temp;

# Function to print Nodes of
# the Linked List
def printList(N):

    # Traverse the LL
    while (N != None):

        # Print Node's data
        print(N.data , end="  ");
        N = N.next;

# Driver Code
if __name__ == '__main__':

    # Given Linked List
    head = Node(3);
    head.next = Node(5);
    head.next.next = Node(8);
    t = None;
    t = EvalNearestMult(head, 3);

    printList(t);

# This code is contributed by gauravrajput1
```

## C#

```
// C# program for the above approach
using System;

public class GFG
{

  // Structure of node
  public    class node {
    public    int data;
    public    node next;

    public    node(int d) {
      data = d;
    }
  }

  // Function to replace the node N
  // by the nearest multiple of K
  static node EvalNearestMult(node N, int K) {
    node temp = N;

    // Traverse the Linked List
    while (N != null) {

      // If data is less than K
      if (N.data < K)
        N.data = 0;

      else {

        // If the data of current
        // node is same as K
        if (N.data == K)
          N.data = K;

        // Otherwise change the value
        else {
          N.data = (N.data / K) * K;
        }
      }

      // Move to the next node
      N = N.next;
    }

    // Return the updated LL
    return temp;
  }

  // Function to print the nodes of
  // the Linked List
  static void printList(node N) {
    // Traverse the LL
    while (N != null) {

      // Print the node's data
      Console.Write(N.data + "  ");
      N = N.next;
    }
  }

  // Driver Code
  public static void Main(String[] args)
  {

    // Given Linked List
    node head = new node(3);
    head.next = new node(5);
    head.next.next = new node(8);

    node t = EvalNearestMult(head, 3);

    printList(t);
  }
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Structure of node
class node {

    constructor()
    {
        this.data = 0;
        this.next = null;
    }
};

// Function to replace the node N
// by the nearest multiple of K
function EvalNearestMult(N, K)
{
    var temp = N;
    var t;

    // Traverse the Linked List
    while (N != null) {

        // If data is less than K
        if (N.data < K)
            N.data = 0;

        else {

            // If the data of current
            // node is same as K
            if (N.data == K)
                N.data = K;

            // Otherwise change the value
            else {
                N.data = parseInt(N.data / K) * K;
            }
        }

        // Move to the next node
        N = N.next;
    }

    // Return the updated LL
    return temp;
}

// Function to print the nodes of
// the Linked List
function printList(N)
{
    // Traverse the LL
    while (N != null) {

        // Print the node's data
        document.write( N.data + "  ");
        N = N.next;
    }
}

// Driver Code
// Given Linked List
var head = null;
var second = null;
var third = null;
head = new node();
second = new node();
third = new node();
head.data = 3;
head.next = second;
second.data = 4;
second.next = third;
third.data = 8;
third.next = null;
var t = EvalNearestMult(head, 3);
printList(t);

// This code is contributed by rrrtnx.

</script>
```

**Output:** 

```
3  3  6
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)