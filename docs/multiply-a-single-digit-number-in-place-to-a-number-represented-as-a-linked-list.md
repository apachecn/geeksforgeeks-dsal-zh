# 将一个位数乘以一个表示为链表的数字

> 原文:[https://www . geesforgeks . org/将一个一位数的数字乘以一个表示为链表的数字/](https://www.geeksforgeeks.org/multiply-a-single-digit-number-in-place-to-a-number-represented-as-a-linked-list/)

给定一个由 **N** 节点组成的[链表](https://www.geeksforgeeks.org/data-structures/linked-list/) ，其中每个节点代表一个数字的位数和一个单位数 **M** ，任务是将链表乘以 **M** 并打印结果链表。

**示例:**

> **输入:**链表:1 → 2 → 7 → 3 → NULL，M = 3
> **输出:** 3 → 8 → 1 → 9 → NULL
> **说明:**给定的链表代表数字 1273。1273 乘以 3 = 1273*3 = 3819。因此，得到的链表是
> 3 → 8 → 1 → 9 →空
> 
> **输入:**链表:9 → 9 → 9 → NULL，M = 2
> **输出:** 1 → 9 → 9 → 8 → NULL
> **说明:**给定的链表代表数字 999。999 乘以 2 = 999*2 = 1998。因此，得到的链表是
> 1 → 9 → 9 → 8 →空

**方法:**既然允许我们反向 LL，最多给它增加 1 个额外节点，那么解决这个问题的思路就是先[反向链表](https://www.geeksforgeeks.org/reverse-a-linked-list/)。然后，[遍历链表](https://www.geeksforgeeks.org/linked-list-set-1-introduction/)并开始乘法 **M** ，每个节点添加生成的进位并在每个乘法步骤后更新进位。再次[反转修改后的链表](https://www.geeksforgeeks.org/reverse-a-linked-list/)并打印结果列表。

下面是上述方法的实现:

## C++14

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Node of a Linked List
class Node {
public:
    int data;
    Node* next;
};

// Function to create a new
// node with given data
Node* newNode(int data)
{
    // Initialize new node
    Node* new_node = new Node;

    // Set the data field of the node
    new_node->data = data;
    new_node->next = NULL;

    // Return the new node
    return new_node;
}

// Function to reverse the linked list
Node* reverse(Node* head)
{
    Node* prev = NULL;
    Node* current = head;
    Node* next;

    // Traverse until curr!=null
    while (current != NULL) {
        next = current->next;
        current->next = prev;
        prev = current;
        current = next;
    }

    // Return the head of the
    // reversed linked list
    return prev;
}

// Utility function to multiply a single digit
// to a linked list
Node* multiplyHelp(Node* head, int M)
{
    // Store the head of list
    Node* res = head;

    // Stores the address of previous node
    Node* prev = NULL;

    // Initially set carry as 0 and product as 1
    int carry = 0, product = 1;

    while (head != NULL) {

        // Multiply M with each digit
        product = head->data * M;

        // Add carry to product if carry exist
        product += carry;

        // Update carry for next calculation
        carry = product / 10;

        // Update the value of each nodes
        head->data = product % 10;

        // Move head and temp pointers to next nodes
        prev = head;
        head = head->next;
    }

    // If some carry is still there,
    // add a new node to list
    if (carry > 0)
        prev->next = newNode(carry);

    // Return head of the resultant list
    return res;
}

// Function to multiply a single digit
// to a linked list
Node* multiply(Node* head, int M)
{
    // Reverse linked list
    head = reverse(head);

    // Multiply M from left to right of reversed list
    head = multiplyHelp(head, M);

    // Reverse the modified list and return its head
    return reverse(head);
}

// Function to print the linked list
void printList(Node* node)
{
    while (node != NULL) {
        cout << node->data;
        node = node->next;
    }
}

// Driver Code
int main()
{
    // Given Input list: 1->2->7->3
    Node* head = newNode(1);
    head->next = newNode(2);
    head->next->next = newNode(7);
    head->next->next->next = newNode(3);
    int M = 3;

    // Function Call
    head = multiply(head, M);

    // Print resultant list
    printList(head);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG {

  // Node of a Linked List
  static class Node {
    int data;
    Node next;
  };

  // Function to create a new
  // node with given data
  static Node newNode(int data)
  {

    // Initialize new node
    Node new_node = new Node();

    // Set the data field of the node
    new_node.data = data;
    new_node.next = null;

    // Return the new node
    return new_node;
  }

  // Function to reverse the linked list
  static Node reverse(Node head) {
    Node prev = null;
    Node current = head;
    Node next;

    // Traverse until curr!=null
    while (current != null) {
      next = current.next;
      current.next = prev;
      prev = current;
      current = next;
    }

    // Return the head of the
    // reversed linked list
    return prev;
  }

  // Utility function to multiply a single digit
  // to a linked list
  static Node multiplyHelp(Node head, int M) {
    // Store the head of list
    Node res = head;

    // Stores the address of previous node
    Node prev = null;

    // Initially set carry as 0 and product as 1
    int carry = 0, product = 1;

    while (head != null) {

      // Multiply M with each digit
      product = head.data * M;

      // Add carry to product if carry exist
      product += carry;

      // Update carry for next calculation
      carry = product / 10;

      // Update the value of each nodes
      head.data = product % 10;

      // Move head and temp pointers to next nodes
      prev = head;
      head = head.next;
    }

    // If some carry is still there,
    // add a new node to list
    if (carry > 0)
      prev.next = newNode(carry);

    // Return head of the resultant list
    return res;
  }

  // Function to multiply a single digit
  // to a linked list
  static Node multiply(Node head, int M)
  {

    // Reverse linked list
    head = reverse(head);

    // Multiply M from left to right of reversed list
    head = multiplyHelp(head, M);

    // Reverse the modified list and return its head
    return reverse(head);
  }

  // Function to print the linked list
  static void printList(Node node) {
    while (node != null) {
      System.out.print(node.data);
      node = node.next;
    }
  }

  // Driver Code
  public static void main(String[] args)
  {

    // Given Input list: 1.2.7.3
    Node head = newNode(1);
    head.next = newNode(2);
    head.next.next = newNode(7);
    head.next.next.next = newNode(3);
    int M = 3;

    // Function Call
    head = multiply(head, M);

    // Print resultant list
    printList(head);

  }
}

// This code contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python program for the above approach

# Node of a Linked List
class Node:
    def __init__(self, data):
        self.data = data;
        self.next = None;

# Function to create a new
# Node with given data
def newNode(data):

    # Initialize new Node
    new_Node = Node(data);

    # Return the new Node
    return new_Node;

# Function to reverse the linked list
def reverse(head):
    prev = None;
    current = head;
    next = None;

    # Traverse until curr!=None
    while (current != None):
        next = current.next;
        current.next = prev;
        prev = current;
        current = next;

    # Return the head of the
    # reversed linked list
    return prev;

# Utility function to multiply a single digit
# to a linked list
def multiplyHelp(head, M):
    # Store the head of list
    res = head;

    # Stores the address of previous Node
    prev = None;

    # Initially set carry as 0 and product as 1
    carry = 0;
    product = 1;

    while (head != None):

        # Multiply M with each digit
        product = head.data * M;

        # Add carry to product if carry exist
        product += carry;

        # Update carry for next calculation
        carry = product // 10;

        # Update the value of each Nodes
        head.data = product % 10;

        # Move head and temp pointers to next Nodes
        prev = head;
        head = head.next;

    # If some carry is still there,
    # add a new Node to list
    if (carry > 0):
        prev.next = newNode(carry);

    # Return head of the resultant list
    return res;

# Function to multiply a single digit
# to a linked list
def multiply(head, M):

    # Reverse linked list
    head = reverse(head);

    # Multiply M from left to right of reversed list
    head = multiplyHelp(head, M);

    # Reverse the modified list and return its head
    return reverse(head);

# Function to prthe linked list
def printList(node):
    while (node != None):
        print(node.data,end="");
        node = node.next;

# Driver Code
if __name__ == '__main__':

    # Given Input list: 1.2.7.3
    head = newNode(1);
    head.next = newNode(2);
    head.next.next = newNode(7);
    head.next.next.next = newNode(3);
    M = 3;

    # Function Call
    head = multiply(head, M);

    # Prresultant list
    printList(head);

# This code is contributed by gauravrajput1
```

## C#

```
// C# program for the above approach
using System;

public class GFG {

  // Node of a Linked List
  class Node {
    public int data;
    public Node next;
  };

  // Function to create a new
  // node with given data
  static Node newNode(int data)
  {

    // Initialize new node
    Node new_node = new Node();

    // Set the data field of the node
    new_node.data = data;
    new_node.next = null;

    // Return the new node
    return new_node;
  }

  // Function to reverse the linked list
  static Node reverse(Node head) {
    Node prev = null;
    Node current = head;
    Node next;

    // Traverse until curr!=null
    while (current != null) {
      next = current.next;
      current.next = prev;
      prev = current;
      current = next;
    }

    // Return the head of the
    // reversed linked list
    return prev;
  }

  // Utility function to multiply a single digit
  // to a linked list
  static Node multiplyHelp(Node head, int M) {
    // Store the head of list
    Node res = head;

    // Stores the address of previous node
    Node prev = null;

    // Initially set carry as 0 and product as 1
    int carry = 0, product = 1;

    while (head != null) {

      // Multiply M with each digit
      product = head.data * M;

      // Add carry to product if carry exist
      product += carry;

      // Update carry for next calculation
      carry = product / 10;

      // Update the value of each nodes
      head.data = product % 10;

      // Move head and temp pointers to next nodes
      prev = head;
      head = head.next;
    }

    // If some carry is still there,
    // add a new node to list
    if (carry > 0)
      prev.next = newNode(carry);

    // Return head of the resultant list
    return res;
  }

  // Function to multiply a single digit
  // to a linked list
  static Node multiply(Node head, int M)
  {

    // Reverse linked list
    head = reverse(head);

    // Multiply M from left to right of reversed list
    head = multiplyHelp(head, M);

    // Reverse the modified list and return its head
    return reverse(head);
  }

  // Function to print the linked list
  static void printList(Node node) {
    while (node != null) {
      Console.Write(node.data);
      node = node.next;
    }
  }

  // Driver Code
  public static void Main(String[] args)
  {

    // Given Input list: 1.2.7.3
    Node head = newNode(1);
    head.next = newNode(2);
    head.next.next = newNode(7);
    head.next.next.next = newNode(3);
    int M = 3;

    // Function Call
    head = multiply(head, M);

    // Print resultant list
    printList(head);

  }
}

// This code contributed by Princi Singh
```

## java 描述语言

```
<script>
// javascript program for the above approach

 // Node of a Linked List
class Node {
    constructor() {
        this.data = 0;
        this.next = null;
    }
}

  // Function to create a new
  // node with given data
  function newNode(data)
  {

    // Initialize new node
     var new_node = new Node();

    // Set the data field of the node
    new_node.data = data;
    new_node.next = null;

    // Return the new node
    return new_node;
  }

  // Function to reverse the linked list
  function reverse(head) {
    var prev = null;
    var current = head;
    var next;

    // Traverse until curr!=null
    while (current != null) {
      next = current.next;
      current.next = prev;
      prev = current;
      current = next;
    }

    // Return the head of the
    // reversed linked list
    return prev;
  }

  // Utility function to multiply a single digit
  // to a linked list
  function multiplyHelp(head , M) {
    // Store the head of list
    var res = head;

    // Stores the address of previous node
    var prev = null;

    // Initially set carry as 0 and product as 1
    var carry = 0, product = 1;

    while (head != null) {

      // Multiply M with each digit
      product = head.data * M;

      // Add carry to product if carry exist
      product += carry;

      // Update carry for next calculation
      carry = parseInt(product / 10);

      // Update the value of each nodes
      head.data = product % 10;

      // Move head and temp pointers to next nodes
      prev = head;
      head = head.next;
    }

    // If some carry is still there,
    // add a new node to list
    if (carry > 0)
      prev.next = newNode(carry);

    // Return head of the resultant list
    return res;
  }

  // Function to multiply a single digit
  // to a linked list
  function multiply(head , M)
  {

    // Reverse linked list
    head = reverse(head);

    // Multiply M from left to right of reversed list
    head = multiplyHelp(head, M);

    // Reverse the modified list and return its head
    return reverse(head);
  }

  // Function to print the linked list
  function printList(node) {
    while (node != null) {
      document.write(node.data);
      node = node.next;
    }
  }

  // Driver Code

    // Given Input list: 1.2.7.3
    var head = newNode(1);
    head.next = newNode(2);
    head.next.next = newNode(7);
    head.next.next.next = newNode(3);
    var M = 3;

    // Function Call
    head = multiply(head, M);

    // Print resultant list
    printList(head);

// This code is contributed by gauravrajput1
</script>
```

**Output**

```
3819
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)