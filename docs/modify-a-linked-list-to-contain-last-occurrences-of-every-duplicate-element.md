# 修改链表以包含每个重复元素的最后一次出现

> 原文:[https://www . geeksforgeeks . org/modify-a-link-list-to-contain-last-occurs-of-ever-replicate-element/](https://www.geeksforgeeks.org/modify-a-linked-list-to-contain-last-occurrences-of-every-duplicate-element/)

给定由可能包含重复元素的 **N** 节点组成的未排序的[单链表](https://www.geeksforgeeks.org/data-structures/linked-list/singly-linked-list/)，任务是从[链表](https://www.geeksforgeeks.org/data-structures/linked-list/)中移除除最后一次出现的重复元素之外的所有元素。

**示例:**

> **输入:**1->2->7->3->2->5->1
> T3】输出:7->3->2->5->1
> T6】解释:
> 给定链表:1->2->7->3->2->
> 
> **输入:**1->2->3->4->5
> **输出:**1->2->3->4->5

**方法:**按照以下步骤解决问题:

*   初始化一个**伪**节点，使其成为下一个指向**头**。
*   [反转给定的链表。](https://www.geeksforgeeks.org/reverse-a-linked-list/)
*   初始化一个[无序集](https://www.geeksforgeeks.org/unordered_set-in-cpp-stl/)，比如**访问过，**存储已经访问过的节点。
*   初始化两个节点，说 **currnode，**指向**哑**节点， **nextnode，**存储**当前**节点的 **next** 节点。
*   [遍历链表](https://www.geeksforgeeks.org/how-to-iterate-linkedlist-in-java/)，检查**当前**节点的**下一个**节点的数据是否已经被访问过。
*   如果已经访问过，请执行以下步骤:
    *   初始化一个新节点，比如说**复制**，来存储**下一个节点**，在这种情况下是一个复制节点。
    *   使**当前的** **下一个**指向**下一个节点**的**下一个**。
*   否则:
    *   将**下一个节点**的数据插入到**访问的**集合中。
    *   使 **nextnode** 成为 **currentnode** 。
*   最后，反转修改后的链表并返回。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Node class
class Node {
public:
    int data;
    Node* next;

    Node(int x)
    {
        this->data = x;
        this->next = NULL;
    }
};

// Function to reverse a Linked List
Node* reverseList(Node* head)
{
    Node *prev = NULL, *nextNode = NULL;
    while (head != NULL) {

        // Point to next node
        // of the current node
        nextNode = head->next;

        // Point next of current
        // to the previous node
        head->next = prev;

        prev = head;

        head = nextNode;
    }
    return prev;
}

// Function to modify a linked list
// such that it contains only the
// last occurrence of duplicate elements
Node* Remove_Dup_Keep_Last_Occurence(
    Node* head)
{
    // Make a dummy node
    Node* dummy = new Node(-1);
    dummy->next = head;

    // Reverse the given Linked List
    dummy->next = reverseList(dummy->next);

    // Stores duplicate elements
    unordered_set<int> visited;

    Node *currNode = dummy, *nextNode;

    // Iterate over the list
    while (currNode != NULL
           && currNode->next != NULL) {

        nextNode = currNode->next;

        // Check if data of the next node of the
        // current node is already visited or not
        if (visited.count(nextNode->data) != 0) {

            // Stores the duplicate pointer
            Node* duplicate = nextNode;
            currNode->next = nextNode->next;

            // Erase memory of duplicate pointer
            delete duplicate;
        }
        else {

            // Mark as visited to data of nextNode
            visited.insert(nextNode->data);

            // Go for the next node
            currNode = nextNode;
        }
    }

    // Reverse the modified linked list
    dummy->next = reverseList(dummy->next);

    return dummy->next;
}

// Function to print a Linked List
void print_Linked_List(Node* head)
{
    Node* curr = head;
    while (curr != NULL) {
        cout << curr->data << ' ';
        curr = curr->next;
    }
}

// Driver Code
int main()
{

    // Given Input
    Node* head = new Node(3);
    head->next = new Node(2);
    head->next->next = new Node(3);
    head->next->next->next = new Node(1);
    head->next->next->next->next = new Node(5);
    head->next->next->next->next->next = new Node(1);
    head->next->next->next->next->next->next = new Node(6);

    head = Remove_Dup_Keep_Last_Occurence(head);

    // Function Call
    print_Linked_List(head);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG
{

// Node class
static class Node {
    int data;
    Node next;

    Node(int x)
    {
        this.data = x;
        this.next = null;
    }
};

// Function to reverse a Linked List
static Node reverseList(Node head)
{
    Node prev = null, nextNode = null;
    while (head != null) {

        // Point to next node
        // of the current node
        nextNode = head.next;

        // Point next of current
        // to the previous node
        head.next = prev;

        prev = head;

        head = nextNode;
    }
    return prev;
}

// Function to modify a linked list
// such that it contains only the
// last occurrence of duplicate elements
static Node Remove_Dup_Keep_Last_Occurence(
    Node head)
{
    // Make a dummy node
    Node dummy = new Node(-1);
    dummy.next = head;

    // Reverse the given Linked List
    dummy.next = reverseList(dummy.next);

    // Stores duplicate elements
    HashSet<Integer> visited = new HashSet<Integer>();

    Node currNode = dummy;
    Node nextNode;

    // Iterate over the list
    while (currNode != null
           && currNode.next != null) {

        nextNode = currNode.next;

        // Check if data of the next node of the
        // current node is already visited or not
        if (visited.contains(nextNode.data)) {

            // Stores the duplicate pointer
            Node duplicate = nextNode;
            currNode.next = nextNode.next;

            // Erase memory of duplicate pointer
            duplicate=null;
        }
        else {

            // Mark as visited to data of nextNode
            visited.add(nextNode.data);

            // Go for the next node
            currNode = nextNode;
        }
    }

    // Reverse the modified linked list
    dummy.next = reverseList(dummy.next);

    return dummy.next;
}

// Function to print a Linked List
static void print_Linked_List(Node head)
{
    Node curr = head;
    while (curr != null) {
        System.out.print(curr.data +" ");
        curr = curr.next;
    }
}

// Driver Code
public static void main(String[] args)
{

    // Given Input
    Node head = new Node(3);
    head.next = new Node(2);
    head.next.next = new Node(3);
    head.next.next.next = new Node(1);
    head.next.next.next.next = new Node(5);
    head.next.next.next.next.next = new Node(1);
    head.next.next.next.next.next.next = new Node(6);

    head = Remove_Dup_Keep_Last_Occurence(head);

    // Function Call
    print_Linked_List(head);

}
}

// This code is contributed by shikhasingrajput
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

public class GFG {

    // Node class
public    class Node {
    public    int data;
    public    Node next;

    public    Node(int x) {
            this.data = x;
            this.next = null;
        }
    };

    // Function to reverse a Linked List
    static Node reverseList(Node head) {
        Node prev = null, nextNode = null;
        while (head != null) {

            // Point to next node
            // of the current node
            nextNode = head.next;

            // Point next of current
            // to the previous node
            head.next = prev;

            prev = head;

            head = nextNode;
        }
        return prev;
    }

    // Function to modify a linked list
    // such that it contains only the
    // last occurrence of duplicate elements
    static Node Remove_Dup_Keep_Last_Occurence(Node head)
    {

        // Make a dummy node
        Node dummy = new Node(-1);
        dummy.next = head;

        // Reverse the given Linked List
        dummy.next = reverseList(dummy.next);

        // Stores duplicate elements
        HashSet<int> visited = new HashSet<int>();

        Node currNode = dummy;
        Node nextNode;

        // Iterate over the list
        while (currNode != null && currNode.next != null) {

            nextNode = currNode.next;

            // Check if data of the next node of the
            // current node is already visited or not
            if (visited.Contains(nextNode.data)) {

                // Stores the duplicate pointer
                Node duplicate = nextNode;
                currNode.next = nextNode.next;

                // Erase memory of duplicate pointer
                duplicate = null;
            } else {

                // Mark as visited to data of nextNode
                visited.Add(nextNode.data);

                // Go for the next node
                currNode = nextNode;
            }
        }

        // Reverse the modified linked list
        dummy.next = reverseList(dummy.next);

        return dummy.next;
    }

    // Function to print a Linked List
    static void print_Linked_List(Node head) {
        Node curr = head;
        while (curr != null) {
            Console.Write(curr.data + " ");
            curr = curr.next;
        }
    }

    // Driver Code
    public static void Main(String[] args) {

        // Given Input
        Node head = new Node(3);
        head.next = new Node(2);
        head.next.next = new Node(3);
        head.next.next.next = new Node(1);
        head.next.next.next.next = new Node(5);
        head.next.next.next.next.next = new Node(1);
        head.next.next.next.next.next.next = new Node(6);

        head = Remove_Dup_Keep_Last_Occurence(head);

        // Function Call
        print_Linked_List(head);

    }
}

// This code is contributed by umadevi9616
```

## java 描述语言

```
<script>
// javascript program for the above approach

    // Node class
class Node {
    constructor(val) {
        this.data = val;
        this.next = null;
    }
}

    // Function to reverse a Linked List
    function reverseList(head) {
    var prev = null, nextNode = null;
        while (head != null) {

            // Point to next node
            // of the current node
            nextNode = head.next;

            // Point next of current
            // to the previous node
            head.next = prev;

            prev = head;

            head = nextNode;
        }
        return prev;
    }

    // Function to modify a linked list
    // such that it contains only the
    // last occurrence of duplicate elements
    function Remove_Dup_Keep_Last_Occurence(head)
    {

        // Make a dummy node
        var dummy = new Node(-1);
        dummy.next = head;

        // Reverse the given Linked List
        dummy.next = reverseList(dummy.next);

        // Stores duplicate elements
        var visited = new Set();

        var currNode = dummy;
        var nextNode;

        // Iterate over the list
        while (currNode != null && currNode.next != null) {

            nextNode = currNode.next;

            // Check if data of the next node of the
            // current node is already visited or not
            if (visited.has(nextNode.data)) {

                // Stores the duplicate pointer
                var duplicate = nextNode;
                currNode.next = nextNode.next;

                // Erase memory of duplicate pointer
                duplicate = null;
            } else {

                // Mark as visited to data of nextNode
                visited.add(nextNode.data);

                // Go for the next node
                currNode = nextNode;
            }
        }

        // Reverse the modified linked list
        dummy.next = reverseList(dummy.next);

        return dummy.next;
    }

    // Function to print a Linked List
    function print_Linked_List(head) {
var curr = head;
        while (curr != null) {
            document.write(curr.data + " ");
            curr = curr.next;
        }
    }

    // Driver Code

        // Given Input
var head = new Node(3);
        head.next = new Node(2);
        head.next.next = new Node(3);
        head.next.next.next = new Node(1);
        head.next.next.next.next = new Node(5);
        head.next.next.next.next.next = new Node(1);
        head.next.next.next.next.next.next = new Node(6);

        head = Remove_Dup_Keep_Last_Occurence(head);

        // Function Call
        print_Linked_List(head);

// This code contributed by umadevi9616
</script>
```

**Output:** 

```
2 3 5 1 6
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)