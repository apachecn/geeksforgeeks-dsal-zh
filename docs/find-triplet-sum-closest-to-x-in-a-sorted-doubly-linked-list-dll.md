# 在排序的双向链表中找到最接近 X 的三元组和

> 原文:[https://www . geesforgeks . org/find-triple-sum-最接近 x-in-a-sorted-double-link-list-dll/](https://www.geeksforgeeks.org/find-triplet-sum-closest-to-x-in-a-sorted-doubly-linked-list-dll/)

给定一个排序后的 **N** 节点的[双链表](https://www.geeksforgeeks.org/doubly-linked-list/)和一个整数 **X** ，任务是找出列表中最接近 **X** 的三个节点的和。

**示例:**

> ***输入:** DLL: -8 ↔ 2 ↔ 3 ↔ 4 ↔ 5，X = 1*
> ***输出:** 1*
> ***解释:**所需的三个整数{-8，4，5}的和为 1 且最接近 1。*
> 
> ***输入:** DLL: 1 ↔ 2 ↔ 3 ↔ 4，X = 3*
> ***输出:** 6*
> ***解释:**所需的三个整数是{1，2，3}，其和为 6，最接近 X = 3。*

**天真法**:解决给定问题最简单的方法是[使用三个](https://www.geeksforgeeks.org/print-all-triplets-with-given-sum/)[嵌套循环](https://www.geeksforgeeks.org/nested-loops-in-c-with-examples-2/)生成所有可能的三元组，然后选择和最接近 **X** 的三元组，并打印三元组的和。

***时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(1)*

**高效进场:**为了优化上述进场，思路是使用 [3 指针技术](https://www.geeksforgeeks.org/find-a-triplet-in-an-array-whose-sum-is-closest-to-a-given-number/)。按照以下步骤解决此问题:

*   初始化 4 个变量，**第一个**和**第二个**指向双链表的头节点，即**第一个=头**、**第二个** = **头**，以及**尾**和**第三个**都初始化到双链表的最后一个节点[。](https://www.geeksforgeeks.org/nth-node-from-the-end-of-a-linked-list/)
*   初始化一个变量 **diff** ，初始化为 [**INT_MAX** ，](https://www.geeksforgeeks.org/int_max-int_min-cc-applications/)，存储最接近 **X** 的和。
*   [当**第一个**节点不是**空**时迭代，并执行以下步骤:](https://www.geeksforgeeks.org/loops-in-c-and-cpp/)
    *   初始化**秒**到**第一个**的下一个，即**秒=第一个→下一个**、**第三个** **=** **尾**(双链表的最后一个节点)。
    *   [迭代而](https://www.geeksforgeeks.org/loops-in-c-and-cpp/) **第二**和**第三**不是**空****第三**不等于第二**。

        *   初始化一个变量，说**将**求和为**(第一个→数据+第二个→数据+第三个→数据)**。
        *   如果**X–sum**的绝对值小于**X****–****diff**的[绝对值](https://www.geeksforgeeks.org/abs-labs-llabs-functions-cc/)，则将 **diff** 的值更新为 **sum。**
        *   如果**和**小于 **X** ，则增加**秒**指针，即**秒=秒→下一个**。
        *   否则，递减**第三个**，即**第三个=第三个→上一个。**** 
    *   **将第一个指针移动到下一个指针，即 **first = first→next** 。**
*   **完成以上步骤后，打印 **diff** 的值作为结果。**

**下面是上述方法的实现:**

## **C++**

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Doubly linked list node
struct Node {
    int data;
    struct Node *next, *prev;
};

// Function to insert a new node at
// the beginning of doubly linked
// list
void insert(struct Node** head, int data)
{
    // Allocate node
    struct Node* temp = new Node();

    // Fill the data value in it
    temp->data = data;
    temp->next = temp->prev = NULL;

    // If head is NULL change
    // head to temp
    if ((*head) == NULL) {
        (*head) = temp;
    }

    // Insert the node before head
    else {
        temp->next = *head;
        (*head)->prev = temp;
        (*head) = temp;
    }
}

// Function to find sum of triplet
// closest to X
void closestTripletSum(struct Node* head, int X)
{
    // Points to the first node
    // of the triplet
    struct Node* first = head;

    // Points to the second node
    // of the triplet
    struct Node* second = head->next;

    // Stores the last node of
    // doubly linked list
    struct Node* tail = head;

    // Traverse till end of the list
    while (tail->next != NULL) {
        tail = tail->next;
    }

    // Stores the sum closest to X
    int diff = INT_MAX;

    // Points to the third node
    // of the triplet
    struct Node* third = tail;

    // Iterate till the end of the list
    while (first != NULL) {
        second = first->next;
        third = tail;

        while (second != NULL && third != NULL
               && third != second) {
            int sum = (first->data + second->data
                       + third->data);

            // Check if the current sum
            // is closest to X
            if (abs(X - sum) < abs(X - diff)) {

                // Update the value of diff
                diff = sum;
            }

            // Check if sum is less than X
            if (sum < X) {

                // Increment the second
                // pointer
                second = second->next;
            }
            else {

                // Decrement the third
                // pointer
                third = third->prev;
            }
        }

        // Move the first pointer
        // ahead
        first = first->next;
    }

    // Print the closest sum
    cout << diff;
}

// Driver Code
int main()
{
    // Given Input
    struct Node* head = NULL;
    insert(&head, 4);
    insert(&head, 3);
    insert(&head, 2);
    insert(&head, 1);
    int X = 3;

    // Function Call
    closestTripletSum(head, X);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java program for the above approach
class GFG {

    // Doubly linked list node
    static class Node {
        int data;
        Node next, prev;
    };
    static Node head;

    // Function to insert a new node at
    // the beginning of doubly linked
    // list
    static void insert(int data)
    {

        // Allocate node
        Node temp = new Node();

        // Fill the data value in it
        temp.data = data;
        temp.next = temp.prev = null;

        // If head is null change
        // head to temp
        if ((head) == null) {
            (head) = temp;
        }

        // Insert the node before head
        else {
            temp.next = head;
            (head).prev = temp;
            (head) = temp;
        }
    }

    // Function to find sum of triplet
    // closest to X
    static void closestTripletSum(int X)
    {
        // Points to the first node
        // of the triplet
        Node first = head;

        // Points to the second node
        // of the triplet
        Node second = head.next;

        // Stores the last node of
        // doubly linked list
        Node tail = head;

        // Traverse till end of the list
        while (tail.next != null) {
            tail = tail.next;
        }

        // Stores the sum closest to X
        int diff = Integer.MAX_VALUE;

        // Points to the third node
        // of the triplet
        Node third = tail;

        // Iterate till the end of the list
        while (first != null) {
            second = first.next;
            third = tail;

            while (second != null && third != null
                   && third != second) {
                int sum = (first.data + second.data
                           + third.data);

                // Check if the current sum
                // is closest to X
                if (Math.abs(X - sum)
                    < Math.abs(X - diff)) {

                    // Update the value of diff
                    diff = sum;
                }

                // Check if sum is less than X
                if (sum < X) {

                    // Increment the second
                    // pointer
                    second = second.next;
                }
                else {

                    // Decrement the third
                    // pointer
                    third = third.prev;
                }
            }

            // Move the first pointer
            // ahead
            first = first.next;
        }

        // Print the closest sum
        System.out.print(diff);
    }

    // Driver Code
    public static void main(String[] args)
    {

        // Given Input
        head = null;
        insert(4);
        insert(3);
        insert(2);
        insert(1);
        int X = 3;

        // Function Call
        closestTripletSum(X);
    }
}

// This code is contributed by umadevi9616
```

## **C#**

```
// C# program for the above approach
using System;
using System.Collections.Generic;
public class GFG {

    // Doubly linked list node
public    class Node {
    public    int data;
    public    Node next, prev;
    };

    static Node head;

    // Function to insert a new node at
    // the beginning of doubly linked
    // list
    static void insert(int data) {

        // Allocate node
        Node temp = new Node();

        // Fill the data value in it
        temp.data = data;
        temp.next = temp.prev = null;

        // If head is null change
        // head to temp
        if ((head) == null) {
            (head) = temp;
        }

        // Insert the node before head
        else {
            temp.next = head;
            (head).prev = temp;
            (head) = temp;
        }
    }

    // Function to find sum of triplet
    // closest to X
    static void closestTripletSum(int X) {
        // Points to the first node
        // of the triplet
        Node first = head;

        // Points to the second node
        // of the triplet
        Node second = head.next;

        // Stores the last node of
        // doubly linked list
        Node tail = head;

        // Traverse till end of the list
        while (tail.next != null) {
            tail = tail.next;
        }

        // Stores the sum closest to X
        int diff = int.MaxValue;

        // Points to the third node
        // of the triplet
        Node third = tail;

        // Iterate till the end of the list
        while (first != null) {
            second = first.next;
            third = tail;

            while (second != null && third != null && third != second) {
                int sum = (first.data + second.data + third.data);

                // Check if the current sum
                // is closest to X
                if (Math.Abs(X - sum) < Math.Abs(X - diff)) {

                    // Update the value of diff
                    diff = sum;
                }

                // Check if sum is less than X
                if (sum < X) {

                    // Increment the second
                    // pointer
                    second = second.next;
                } else {

                    // Decrement the third
                    // pointer
                    third = third.prev;
                }
            }

            // Move the first pointer
            // ahead
            first = first.next;
        }

        // Print the closest sum
        Console.Write(diff);
    }

    // Driver Code
    public static void Main(String[] args) {

        // Given Input
        head = null;
        insert(4);
        insert(3);
        insert(2);
        insert(1);
        int X = 3;

        // Function Call
        closestTripletSum(X);
    }
}

// This code is contributed by umadevi9616
```

## **java 描述语言**

```
<script>
// javascript program for the above approach    // Doubly linked list node
class Node {
    constructor(val = 0) {
        this.data = val;
        this.prev = null;
        this.next = null;
    }
}
    var head;

    // Function to insert a new node at
    // the beginning of doubly linked
    // list
    function insert(data) {

        // Allocate node
            var temp = new Node();

        // Fill the data value in it
        temp.data = data;
        temp.next = temp.prev = null;

        // If head is null change
        // head to temp
        if ((head) == null) {
            (head) = temp;
        }

        // Insert the node before head
        else {
            temp.next = head;
            (head).prev = temp;
            (head) = temp;
        }
    }

    // Function to find sum of triplet
    // closest to X
    function closestTripletSum(X)
    {

        // Points to the first node
        // of the triplet
        var first = head;

        // Points to the second node
        // of the triplet
        var second = head.next;

        // Stores the last node of
        // doubly linked list
        var tail = head;

        // Traverse till end of the list
        while (tail.next != null) {
            tail = tail.next;
        }

        // Stores the sum closest to X
        var diff = Number.MAX_VALUE;

        // Points to the third node
        // of the triplet
        var third = tail;

        // Iterate till the end of the list
        while (first != null) {
            second = first.next;
            third = tail;

            while (second != null && third != null && third != second) {
                var sum = (first.data + second.data + third.data);

                // Check if the current sum
                // is closest to X
                if (Math.abs(X - sum) < Math.abs(X - diff)) {

                    // Update the value of diff
                    diff = sum;
                }

                // Check if sum is less than X
                if (sum < X) {

                    // Increment the second
                    // pointer
                    second = second.next;
                } else {

                    // Decrement the third
                    // pointer
                    third = third.prev;
                }
            }

            // Move the first pointer
            // ahead
            first = first.next;
        }

        // Print the closest sum
        document.write(diff);
    }

    // Driver Code

        // Given Input
        head = null;
        insert(4);
        insert(3);
        insert(2);
        insert(1);
        var X = 3;

        // Function Call
        closestTripletSum(X);

// This code is contributed by umadevi9616
</script>
```

****Output**

```
6
```** 

*****时间复杂度:**O(N<sup>2</sup>)*
***辅助空间:** O(1)***