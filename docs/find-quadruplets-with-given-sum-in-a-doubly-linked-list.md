# 在双向链表中找到给定和的四胞胎

> 原文:[https://www . geeksforgeeks . org/find-带双链表给定和的四胞胎/](https://www.geeksforgeeks.org/find-quadruplets-with-given-sum-in-a-doubly-linked-list/)

给定一个排序的[双链表](https://www.geeksforgeeks.org/doubly-linked-list/)和一个整数 **X** ，任务是打印双链表中总和为 **X** 的所有四胞胎。

***例:***

> ***输入:** LL: -3 ↔ 1 ↔ 2 ↔ 3 ↔ 5 ↔ 6，X = 7*
> ***输出:***
> *-3 2 3 5*
> *-3 3 1 6*
> ***解释:**具有和 7( = X)的四胞胎是:{-3，2，3，5}，{-3，1，6}。*
> 
> *输入**-2↑1↑0↑1↑2、x = 0
> *的输出****

****方法:**给定的问题可以使用本文[中讨论的思路](https://www.geeksforgeeks.org/find-four-numbers-with-sum-equal-to-given-sum/)使用 [4 指针技术](https://www.geeksforgeeks.org/find-four-elements-that-sum-to-a-given-value-two-pointer-approach/)来解决。按照以下步骤解决问题:**

*   **初始化四个变量，先说**作为双链表的开始即；**第一个=头**，**第二个**到第一个指针的下一个，**第三个**到第二个指针的下一个，以及**第四个**到存储排序的双链表中所有 4 个元素的双链表的最后一个节点。****
*   ****[迭代一个循环](https://www.geeksforgeeks.org/loops-in-c-and-cpp/)，直到**第一个**节点和**第四个**节点不为**空**，并且它们不相等，这两个节点不交叉，执行以下步骤:

    *   将**第二个**指针初始化到下一个第一个**。**
    *   **[迭代一个循环](https://www.geeksforgeeks.org/loops-in-c-and-cpp/)直到**第二个**和**第四个**节点不是 **NULL** ，它们不相等也不交叉。

        *   初始化一个变量，将**求和**为**(X –(第一个→数据+第二个→数据))**，将**第三个**指针指向**第二个**指针的下一个，取另一个 **temp** 指针初始化为**最后一个节点**，即指针**第四个**。
        *   [迭代一个循环](https://www.geeksforgeeks.org/loops-in-c-and-cpp/)而**温度**和**第三个**不是**空**，它们不相等也不交叉
            *   如果**和**的值为**三次→数据+温度→数据**，则打印四倍并将**三次指针**增加到当前**三次指针**的下一个，将**温度**增加到当前温度的前一个。
            *   如果**和**的值小于**三分之一→数据+温度→数据**，则增加**三分之一**指针，即**三分之一=三分之一→下一个**。
            *   否则，递减**温度**指针，即**温度=温度→前一个**。
        *   将第二个**指针移动到下一个指针。**** 
    *   **将第一个**指针移动到下一个指针。******** 

****下面是上述方法的实现:****

## ****C++****

```
**// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Structure of node of a doubly
// linked list
struct Node {
    int data;
    struct Node *next, *prev;
};

// Function to insert a new node at
// the beginning of the doubly linked
// list
void insert(struct Node** head, int data)
{
    // Allocate the node
    struct Node* temp = new Node();

    // Fill in the data value
    temp->data = data;
    temp->next = temp->prev = NULL;

    if ((*head) == NULL)
        (*head) = temp;
    else {
        temp->next = *head;
        (*head)->prev = temp;
        (*head) = temp;
    }
}

// Function to print the quadruples
// having sum equal to x
void PrintFourSum(struct Node* head, int x)
{
    // First pointer to the head node
    struct Node* first = head;

    // Pointer to point to the second
    // node for the required sum
    struct Node* second;

    // Pointer to point to the third
    // node for the required sum
    struct Node* third;

    // Fourth points to the last node
    struct Node* fourth = head;

    // Update the fourth pointer to
    // the end of the DLL
    while (fourth->next != NULL) {
        fourth = fourth->next;
    }

    // Node to point to the fourth node
    // of the required sum
    struct Node* temp;

    while (first != NULL
           && fourth != NULL
           && first != fourth
           && fourth->next != first) {

        // Point the second node to the
        // second element of quadruple
        second = first->next;

        while (second != NULL
               && fourth != NULL
               && second != fourth
               && fourth->next != second) {

            int reqsum = x - (first->data
                              + second->data);

            // Points to the 3rd element
            // of quadruple
            third = second->next;

            // Points to the tail of the DLL
            temp = fourth;

            while (third != NULL && temp != NULL
                   && third != temp
                   && temp->next != third) {

                // Store the current sum
                int twosum = third->data
                             + temp->data;

                // If the sum is equal,
                // then print quadruple
                if (twosum == reqsum) {

                    cout << "(" << first->data
                         << ", "
                         << second->data
                         << ", "
                         << third->data
                         << ", "
                         << temp->data
                         << ")\n";

                    third = third->next;
                    temp = temp->prev;
                }

                // If twosum is less than
                // the reqsum then move the
                // third pointer to the next
                else if (twosum < reqsum) {
                    third = third->next;
                }

                // Otherwise move the fourth
                // pointer to the previous
                // of the fourth pointer
                else {
                    temp = temp->prev;
                }
            }

            // Move to the next of
            // the second pointer
            second = second->next;
        }

        // Move to the next of
        // the first pointer
        first = first->next;
    }
}

// Driver Code
int main()
{
    struct Node* head = NULL;
    insert(&head, 2);
    insert(&head, 1);
    insert(&head, 0);
    insert(&head, 0);
    insert(&head, -1);
    insert(&head, -2);
    int X = 0;
    PrintFourSum(head, X);

    return 0;
}**
```

## ****Java 语言(一种计算机语言，尤用于创建网站)****

```
**// Java program for the above approach

class GFG {

    // structure of node of
    // doubly linked list
    static class Node {
        int data;
        Node next, prev;
    };

    // A utility function to insert
    // a new node at the beginning
    // of the doubly linked list
    static Node insert(Node head, int data)
    {

        // Allocate the node
        Node temp = new Node();

        // Fill in the data value
        temp.data = data;
        temp.next = temp.prev = null;
        if (head == null)
            (head) = temp;
        else {
            temp.next = head;
            (head).prev = temp;
            (head) = temp;
        }
        return temp;
    }

    // Function to print the quadruples
    // having sum equal to x
    static void PrintFourSum(Node head, int x)
    {

        // First pointer to the head node
        Node first = head;

        // Pointer to point to the second
        // node for the required sum
        Node second = head;

        // Pointer to point to the third
        // node for the required sum
        Node third = head;

        // Fourth points to the last node
        Node fourth = head;

        // Update the fourth pointer to
        // the end of the DLL
        while (fourth.next != null) {
            fourth = fourth.next;
        }

        // Node to point to the fourth node
        // of the required sum
        Node temp;
        while (first != null && fourth != null
               && first != fourth && fourth.next != first) {

            // Point the second node to the
            // second element of quadruple
            second = first.next;

            while (second != null && fourth != null
                   && second != fourth
                   && fourth.next != second) {

                int reqsum = x - (first.data + second.data);

                // Points to the 3rd element
                // of quadruple
                third = second.next;

                // Points to the tail of the DLL
                temp = fourth;

                while (third != null && temp != null
                       && third != temp
                       && temp.next != third) {

                    // Store the current sum
                    int twosum = third.data + temp.data;

                    // If the sum is equal,
                    // then print quadruple
                    if (twosum == reqsum) {

                        System.out.println(
                            "(" + first.data + ", "
                            + second.data + ", "
                            + third.data + ", " + temp.data
                            + ")");

                        third = third.next;
                        temp = temp.prev;
                    }

                    // If twosum is less than
                    // the reqsum then move the
                    // third pointer to the next
                    else if (twosum < reqsum) {
                        third = third.next;
                    }

                    // Otherwise move the fourth
                    // pointer to the previous
                    // of the fourth pointer
                    else {
                        temp = temp.prev;
                    }
                }

                // Move to the next of
                // the second pointer
                second = second.next;
            }

            // Move to the next of
            // the first pointer
            first = first.next;
        }
    }

    // Driver Code
    public static void main(String args[])
    {

        Node head = null;
        head = insert(head, 2);
        head = insert(head, 1);
        head = insert(head, 0);
        head = insert(head, 0);
        head = insert(head, -1);
        head = insert(head, -2);
        int x = 0;

        PrintFourSum(head, x);
    }
}

// This code is contributed
// by kirtishsurangalikar**
```

## ****蟒蛇 3****

```
**# Python3 program for the above approach

# Structure of node of a doubly
# linked list
class Node:

    def __init__(self, d):

        self.data = d
        self.left = None
        self.right = None

# Function to insert a new node at
# the beginning of the doubly linked
# list
def insert(head, data):

    # Allocate the node
    temp = Node(data)

    # Fill in the data value
    temp.data = data
    temp.next = temp.prev = None

    if (head == None):
        head = temp
    else:
        temp.next = head
        head.prev = temp
        head = temp

    return head

# Function to print the quadruples
# having sum equal to x
def PrintFourSum(head, x):

    # First pointer to the head node
    first = head

    # Pointer to point to the second
    # node for the required sum
    second = None

    # Pointer to point to the third
    # node for the required sum
    third = None

    # Fourth points to the last node
    fourth = head

    # Update the fourth pointer to
    # the end of the DLL
    while (fourth.next != None):
        fourth = fourth.next

    # Node to point to the fourth node
    # of the required sum
    temp = None

    while (first != None and
          fourth != None and
           first != fourth and
     fourth.next != first):

        # Point the second node to the
        # second element of quadruple
        second = first.next

        while (second != None and
               fourth != None and
               second != fourth and
          fourth.next != second):

            reqsum = x - (first.data +
                         second.data)

            # Points to the 3rd element
            # of quadruple
            third = second.next

            # Points to the tail of the DLL
            temp = fourth

            while (third != None and temp != None and
                   third != temp and temp.next != third):

                # Store the current sum
                twosum = third.data + temp.data

                # If the sum is equal,
                # then print quadruple
                if (twosum == reqsum):

                    print("(" + str(first.data) +
                         ", " + str(second.data) +
                         ", " + str(third.data) +
                         ", " + str(temp.data) + ")")
                    third = third.next
                    temp = temp.prev

                # If twosum is less than
                # the reqsum then move the
                # third pointer to the next
                elif (twosum < reqsum):
                    third = third.next

                # Otherwise move the fourth
                # pointer to the previous
                # of the fourth pointer
                else:
                    temp = temp.prev

            # Move to the next of
            # the second pointer
            second = second.next

        # Move to the next of
        # the first pointer
        first = first.next

# Driver Code
if __name__ == '__main__':

    head = None
    head = insert(head, 2)
    head = insert(head, 1)
    head = insert(head, 0)
    head = insert(head, 0)
    head = insert(head, -1)
    head = insert(head, -2)
    X = 0

    PrintFourSum(head, X)

# This code is contributed by mohit kumar 29**
```

## ****C#****

```
**// C# program for the above approach
using System;

public class GFG {

    // structure of node of
    // doubly linked list
public    class Node {
    public    int data;
    public    Node next, prev;
    };

    // A utility function to insert
    // a new node at the beginning
    // of the doubly linked list
    static Node insert(Node head, int data) {

        // Allocate the node
        Node temp = new Node();

        // Fill in the data value
        temp.data = data;
        temp.next = temp.prev = null;
        if (head == null)
            (head) = temp;
        else {
            temp.next = head;
            (head).prev = temp;
            (head) = temp;
        }
        return temp;
    }

    // Function to print the quadruples
    // having sum equal to x
    static void PrintFourSum(Node head, int x) {

        // First pointer to the head node
        Node first = head;

        // Pointer to point to the second
        // node for the required sum
        Node second = head;

        // Pointer to point to the third
        // node for the required sum
        Node third = head;

        // Fourth points to the last node
        Node fourth = head;

        // Update the fourth pointer to
        // the end of the DLL
        while (fourth.next != null) {
            fourth = fourth.next;
        }

        // Node to point to the fourth node
        // of the required sum
        Node temp;
        while (first != null && fourth != null && first != fourth && fourth.next != first) {

            // Point the second node to the
            // second element of quadruple
            second = first.next;

            while (second != null && fourth != null && second != fourth && fourth.next != second) {

                int reqsum = x - (first.data + second.data);

                // Points to the 3rd element
                // of quadruple
                third = second.next;

                // Points to the tail of the DLL
                temp = fourth;

                while (third != null && temp != null && third != temp && temp.next != third) {

                    // Store the current sum
                    int twosum = third.data + temp.data;

                    // If the sum is equal,
                    // then print quadruple
                    if (twosum == reqsum) {

                        Console.WriteLine(
                                "(" + first.data + ", " + second.data + ", " + third.data + ", " + temp.data + ")");

                        third = third.next;
                        temp = temp.prev;
                    }

                    // If twosum is less than
                    // the reqsum then move the
                    // third pointer to the next
                    else if (twosum < reqsum) {
                        third = third.next;
                    }

                    // Otherwise move the fourth
                    // pointer to the previous
                    // of the fourth pointer
                    else {
                        temp = temp.prev;
                    }
                }

                // Move to the next of
                // the second pointer
                second = second.next;
            }

            // Move to the next of
            // the first pointer
            first = first.next;
        }
    }

    // Driver Code
    public static void Main(String []args) {

        Node head = null;
        head = insert(head, 2);
        head = insert(head, 1);
        head = insert(head, 0);
        head = insert(head, 0);
        head = insert(head, -1);
        head = insert(head, -2);
        int x = 0;

        PrintFourSum(head, x);
    }
}

// This code is contributed by gauravrajput1**
```

## ****java 描述语言****

```
**<script>

// Javascript program for the above approach

// Structure of node of a doubly
// linked list
class Node {

    constructor()
    {
        this.data = 0;
        this.next = null;
        this.prev = null;
    }
};

// Function to insert a new node at
// the beginning of the doubly linked
// list
function insert(head, data)
{
    // Allocate the node
    var temp = new Node();

    // Fill in the data value
    temp.data = data;
    temp.next = temp.prev = null;

    if ((head) == null)
        (head) = temp;
    else {
        temp.next = head;
        (head).prev = temp;
        (head) = temp;
    }
    return head;
}

// Function to print the quadruples
// having sum equal to x
function PrintFourSum(head, x)
{
    // First pointer to the head node
    var first = head;

    // Pointer to point to the second
    // node for the required sum
    var second;

    // Pointer to point to the third
    // node for the required sum
    var third;

    // Fourth points to the last node
    var fourth = head;

    // Update the fourth pointer to
    // the end of the DLL
    while (fourth.next != null) {
        fourth = fourth.next;
    }

    // Node to point to the fourth node
    // of the required sum
    var temp;

    while (first != null
           && fourth != null
           && first != fourth
           && fourth.next != first) {

        // Point the second node to the
        // second element of quadruple
        second = first.next;

        while (second != null
               && fourth != null
               && second != fourth
               && fourth.next != second) {

            var reqsum = x - (first.data
                              + second.data);

            // Points to the 3rd element
            // of quadruple
            third = second.next;

            // Points to the tail of the DLL
            temp = fourth;

            while (third != null && temp != null
                   && third != temp
                   && temp.next != third) {

                // Store the current sum
                var twosum = third.data
                             + temp.data;

                // If the sum is equal,
                // then print quadruple
                if (twosum == reqsum) {

                    document.write( "(" + first.data
                         + ", "
                         + second.data
                         + ", "
                         + third.data
                         + ", "
                         + temp.data
                         + ")<br>");

                    third = third.next;
                    temp = temp.prev;
                }

                // If twosum is less than
                // the reqsum then move the
                // third pointer to the next
                else if (twosum < reqsum) {
                    third = third.next;
                }

                // Otherwise move the fourth
                // pointer to the previous
                // of the fourth pointer
                else {
                    temp = temp.prev;
                }
            }

            // Move to the next of
            // the second pointer
            second = second.next;
        }

        // Move to the next of
        // the first pointer
        first = first.next;
    }
}

// Driver Code
var head = null;
head = insert(head, 2);
head = insert(head, 1);
head = insert(head, 0);
head = insert(head, 0);
head = insert(head, -1);
head = insert(head, -2);
var X = 0;
PrintFourSum(head, X);

// This code is contributed by rrrtnx.
</script>**
```

******Output**

```
(-2, -1, 1, 2)
(-2, 0, 0, 2)
(-1, 0, 0, 1)
```**** 

*******时间复杂度:**O(N<sup>3</sup>)*
***辅助空间:** O(1)*****