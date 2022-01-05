# 循环链表中下一个较大的元素

> 原文:[https://www . geeksforgeeks . org/next-大元循环链表/](https://www.geeksforgeeks.org/next-greater-element-in-a-circular-linked-list/)

给定一个[循环单链表](https://www.geeksforgeeks.org/circular-singly-linked-list-insertion/)，任务是为[链表](https://www.geeksforgeeks.org/data-structures/linked-list/)中的每个节点打印[下一个更大的元素](https://www.geeksforgeeks.org/next-greater-element/)。如果任何节点没有下一个更大的元素，则打印该节点的**-1”**。

**示例:**

> **输入:**head = 1→5→2→10→0→(head)
> **输出:** 5 10 10 -1 1
> **解释:**
> 每个节点的下一个较大元素是:
> 
> 1.  节点 1:下一个更大的元素是 5。
> 2.  节点 5:下一个更大的元素是 10。
> 3.  节点 2:下一个更大的元素是 10。
> 4.  节点 10:不存在下一个更大的元素。因此打印“-1”。
> 5.  节点 0:不存在下一个更大的元素。因此打印“-1”。
> 
> **输入:**head = 1→5→12→10→0 →( head)
> **输出:** 5 12 -1 12 1

**方法:**给定的问题可以通过[向右迭代循环链表](https://www.geeksforgeeks.org/circular-linked-list-set-2-traversal/)直到相同的元素再次出现，然后打印为每个节点找到的下一个更大的元素来解决。按照以下步骤解决问题:

*   初始化一个节点变量，说 **res** 为 [NULL](https://www.geeksforgeeks.org/null-pointer-exception-in-java/) 来存储代表下一个更大元素的链表头节点。
*   另外，初始化一个节点变量，将**临时列表**设为[空](https://www.geeksforgeeks.org/interesting-facts-about-null-in-java/)到[遍历代表下一个更大元素的链表](https://www.geeksforgeeks.org/how-to-iterate-linkedlist-in-java/)。
*   [迭代循环链表](https://www.geeksforgeeks.org/circular-linked-list-set-2-traversal/)并执行以下步骤:
    *   初始化一个节点，说 **curr** 存储对循环链表**当前节点**的引用。
    *   初始化一个变量，比如说 **Val** 为 **-1** 来存储**当前节点**的下一个较大元素的值。
    *   执行以下步骤，直到**电流**不等于循环链表**当前节点**的参考:
        *   如果当前节点**电流**的值大于循环链表的**当前节点**的值，则将**电流数据**的值赋给**值**和[脱离循环](https://www.geeksforgeeks.org/break-statement-in-java/)。
        *   将 **curr** 节点的值更新为 **curr = curr.next** 。
    *   如果节点 **res** 为**空**，则创建一个值为 **Val** 的新节点，并将其分配给 **res** ，然后将 **res** 的值分配给 **tempList** 。
    *   否则，创建一个值为 **Val** 的新节点，并将其分配给 **tempList.next** ，然后将节点 **tempList** 更新为 **tempList = tempList.next.**
*   完成以上步骤后，打印链表 **res** 的元素作为答案。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Node structure of the circular
// Linked list
struct Node
{
    int data;
    Node *next;

    // Constructor
    Node(int d)
    {
        data = d;
        next = NULL;
    }
};

// Function to print the elements
// of a Linked list
void print(Node *head)
{
    Node *temp = head;

    // Iterate the linked list
    while (temp != NULL)
    {

        // Print the data
        cout << temp->data << " ";
        temp = temp->next;
    }
}

// Function to find the next
// greater element for each node
void NextGreaterElement(Node *head)
{

    // Stores the head of circular
    // Linked list
    Node *H = head;

    // Stores the head of the
    // resulting linked list
    Node *res = NULL;

    // Stores the temporary head of
    // the resulting Linked list
    Node *tempList = NULL;

    // Iterate until head
    // is not equal to H
    do
    {

        // Used to iterate over the
        // circular Linked List
        Node *curr = head;

        // Stores if there exist
        // any next Greater element
        int Val = -1;

        // Iterate until head is
        // not equal to curr
        do
        {

            // If the current node
            // is smaller
            if (head->data < curr->data)
            {

                // Update the value
                // of Val
                Val = curr->data;
                break;
            }

            // Update curr
            curr = curr->next;

        } while (curr != head);

        // If res is Null
        if (res == NULL)
        {

            // Create new Node with
            // value curr->data
            res = new Node(Val);

            // Assign address of
            // res to tempList
            tempList = res;
        }
        else
        {

            // Update tempList
            tempList->next = new Node(Val);

            // Assign address of the
            // next node to tempList
            tempList = tempList->next;
        }

        // Update the value of
        // head node
        head = head->next;
    } while (head != H);

    // Print the resulting
    // Linked list
    print(res);
}

// Driver code
int main()
{
    Node *head = new Node(1);
    head->next = new Node(5);
    head->next->next = new Node(12);
    head->next->next->next = new Node(10);

    head->next->next->next->next = new Node(0);
    head->next->next->next->next->next = head;

    NextGreaterElement(head);

    return 0;
}

// This code is contributed by mohit kumar 29
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;
import java.util.*;

class GFG {
    static Node head;

    // Node structure of the circular
    // Linked list
    static class Node {
        int data;
        Node next;

        // Constructor
        public Node(int data)
        {
            this.data = data;
            this.next = null;
        }
    }

    // Function to print the elements
    // of a Linked list
    static void print(Node head)
    {
        Node temp = head;

        // Iterate the linked list
        while (temp != null) {

            // Print the data
            System.out.print(
                temp.data + " ");
            temp = temp.next;
        }
    }

    // Function to find the next
    // greater element for each node
    static void NextGreaterElement(Node head)
    {
        // Stores the head of circular
        // Linked list
        Node H = head;

        // Stores the head of the
        // resulting linked list
        Node res = null;

        // Stores the temporary head of
        // the resulting Linked list
        Node tempList = null;

        // Iterate until head
        // is not equal to H
        do {

            // Used to iterate over the
            // circular Linked List
            Node curr = head;

            // Stores if there exist
            // any next Greater element
            int Val = -1;

            // Iterate until head is
            // not equal to curr
            do {

                // If the current node
                // is smaller
                if (head.data < curr.data) {

                    // Update the value
                    // of Val
                    Val = curr.data;
                    break;
                }

                // Update curr
                curr = curr.next;

            } while (curr != head);

            // If res is Null
            if (res == null) {

                // Create new Node with
                // value curr.data
                res = new Node(Val);

                // Assign address of
                // res to tempList
                tempList = res;
            }
            else {

                // Update tempList
                tempList.next = new Node(Val);

                // Assign address of the
                // next node to tempList
                tempList = tempList.next;
            }

            // Update the value of
            // head node
            head = head.next;
        } while (head != H);

        // Print the resulting
        // Linked list
        print(res);
    }

    // Driver Code
    public static void main(String[] args)
    {
        head = new Node(1);
        head.next = new Node(5);
        head.next.next = new Node(12);
        head.next.next.next = new Node(10);

        head.next.next.next.next = new Node(0);
        head.next.next.next.next.next = head;

        NextGreaterElement(head);
    }
}
```

## C#

```
// C# program for the above approach
using System;

// Node structure of the circular
// Linked list
class Node
{
    public int data;
    public Node next;

    // Constructor
    public Node(int data)
    {
        this.data = data;
        this.next = null;
    }
}

class GFG{

static Node head;

// Function to print the elements
// of a Linked list
static void print(Node head)
{
    Node temp = head;

    // Iterate the linked list
    while (temp != null)
    {

        // Print the data
        Console.Write(temp.data + " ");
        temp = temp.next;
    }
}

// Function to find the next
// greater element for each node
static void NextGreaterElement(Node head)
{

    // Stores the head of circular
    // Linked list
    Node H = head;

    // Stores the head of the
    // resulting linked list
    Node res = null;

    // Stores the temporary head of
    // the resulting Linked list
    Node tempList = null;

    // Iterate until head
    // is not equal to H
    do{

        // Used to iterate over the
        // circular Linked List
        Node curr = head;

        // Stores if there exist
        // any next Greater element
        int Val = -1;

        // Iterate until head is
        // not equal to curr
        do{

            // If the current node
            // is smaller
            if (head.data < curr.data)
            {

                // Update the value
                // of Val
                Val = curr.data;
                break;
            }

            // Update curr
            curr = curr.next;

        } while (curr != head);

        // If res is Null
        if (res == null)
        {

            // Create new Node with
            // value curr.data
            res = new Node(Val);

            // Assign address of
            // res to tempList
            tempList = res;
        }
        else
        {

            // Update tempList
            tempList.next = new Node(Val);

            // Assign address of the
            // next node to tempList
            tempList = tempList.next;
        }

        // Update the value of
        // head node
        head = head.next;
    } while (head != H);

    // Print the resulting
    // Linked list
    print(res);
}

// Driver Code
static public void Main()
{
    head = new Node(1);
    head.next = new Node(5);
    head.next.next = new Node(12);
    head.next.next.next = new Node(10);

    head.next.next.next.next = new Node(0);
    head.next.next.next.next.next = head;

    NextGreaterElement(head);
}
}

// This code is contributed by unknown2108
```

## java 描述语言

```
<script>
// Javascript program for the above approach

let head;

// Node structure of the circular
    // Linked list
class Node
{
// Constructor
    constructor(data)
    {
        this.data = data;
        this.next = null;
    }
}

// Function to print the elements
    // of a Linked list
function print(head)
{
    let temp = head;

        // Iterate the linked list
        while (temp != null) {

            // Print the data
            document.write(
                temp.data + " ");
            temp = temp.next;
        }
}

// Function to find the next
    // greater element for each node
function NextGreaterElement(head)
{
    // Stores the head of circular
        // Linked list
        let H = head;

        // Stores the head of the
        // resulting linked list
        let res = null;

        // Stores the temporary head of
        // the resulting Linked list
        let tempList = null;

        // Iterate until head
        // is not equal to H
        do {

            // Used to iterate over the
            // circular Linked List
            let curr = head;

            // Stores if there exist
            // any next Greater element
            let Val = -1;

            // Iterate until head is
            // not equal to curr
            do {

                // If the current node
                // is smaller
                if (head.data < curr.data) {

                    // Update the value
                    // of Val
                    Val = curr.data;
                    break;
                }

                // Update curr
                curr = curr.next;

            } while (curr != head);

            // If res is Null
            if (res == null) {

                // Create new Node with
                // value curr.data
                res = new Node(Val);

                // Assign address of
                // res to tempList
                tempList = res;
            }
            else {

                // Update tempList
                tempList.next = new Node(Val);

                // Assign address of the
                // next node to tempList
                tempList = tempList.next;
            }

            // Update the value of
            // head node
            head = head.next;
        } while (head != H);

        // Print the resulting
        // Linked list
        print(res);
}

// Driver Code
head = new Node(1);
head.next = new Node(5);
head.next.next = new Node(12);
head.next.next.next = new Node(10);

head.next.next.next.next = new Node(0);
head.next.next.next.next.next = head;

NextGreaterElement(head);

// This code is contributed by unknown2108
</script>
```

**Output:** 

```
5 12 -1 12 1
```

***时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(N)*