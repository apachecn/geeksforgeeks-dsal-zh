# 添加两个由链表表示的数字| 设置 1

给定两个列表代表的两个数字，编写一个返回和列表的函数。 总和列表是两个输入数字相加的列表表示形式。

**范例**：

> **输入：**
> List1：5- > 6- > 3 //代表数字 365
> List2：8- > 4- > 2 //代表数字 248
> **输出：**
> 结果列表：3- > 1- > 6 //代表数字 613
> **说明：** 365 + 248 = 613
> **输入：**
> List1：7- > 5- > 9- > 4- > 6 //代表数字 64957
> List2：8- > 4 //代表数字 48
> **输出：**
> 结果列表：5- > 0- > 0- > 5- > 6 //代表数字 65005
> **说明：** 64957 + 48 = 65005

**方法**：遍历两个列表和两个列表的一个接一个拾取节点并添加值。 如果总和大于 10，则使进位为 1 并减少总和。 如果一个列表的元素多于另一个列表，则将该列表的剩余值视为 0。

**步骤为：**

1.  从头到尾遍历两个链接列表

2.  将两个数字分别从各自的链接列表中添加。

3.  如果列表之一已到达末尾，则将 0 用作其数字。

4.  继续进行直到两个列表都结束。

5.  如果两个数字的总和大于 9，则将进位设置为 1，将当前数字设置为 *sum％10*

下面是此方法的实现。

## C++

```cpp

// C++ program to add two numbers
// represented by linked list
#include <bits/stdc++.h>
using namespace std;

/* Linked list node */
class Node {
public:
    int data;
    Node* next;
};

/* Function to create a 
new node with given data */
Node* newNode(int data)
{
    Node* new_node = new Node();
    new_node->data = data;
    new_node->next = NULL;
    return new_node;
}

/* Function to insert a node at the
beginning of the Singly Linked List */
void push(Node** head_ref, int new_data)
{
    /* allocate node */
    Node* new_node = newNode(new_data);

    /* link the old list off the new node */
    new_node->next = (*head_ref);

    /* move the head to point to the new node */
    (*head_ref) = new_node;
}

/* Adds contents of two linked lists and 
return the head node of resultant list */
Node* addTwoLists(Node* first, Node* second)
{

    // res is head node of the resultant list
    Node* res = NULL;
    Node *temp, *prev = NULL;
    int carry = 0, sum;

    // while both lists exist
    while (first != NULL
           || second != NULL) {
        // Calculate value of next
        // digit in resultant list.
        // The next digit is sum of
        // following things
        // (i) Carry
        // (ii) Next digit of first
        // list (if there is a next digit)
        // (ii) Next digit of second
        // list (if there is a next digit)
        sum = carry + (first ? first->data : 0)
              + (second ? second->data : 0);

        // update carry for next calulation
        carry = (sum >= 10) ? 1 : 0;

        // update sum if it is greater than 10
        sum = sum % 10;

        // Create a new node with sum as data
        temp = newNode(sum);

        // if this is the first node then
        // set it as head of the resultant list
        if (res == NULL)
            res = temp;

        // If this is not the first
        // node then connect it to the rest.
        else
            prev->next = temp;

        // Set prev for next insertion
        prev = temp;

        // Move first and second
        // pointers to next nodes
        if (first)
            first = first->next;
        if (second)
            second = second->next;
    }

    if (carry > 0)
        temp->next = newNode(carry);

    // return head of the resultant list
    return res;
}

// A utility function to print a linked list
void printList(Node* node)
{
    while (node != NULL) {
        cout << node->data << " ";
        node = node->next;
    }
    cout << endl;
}

/* Driver code */
int main(void)
{
    Node* res = NULL;
    Node* first = NULL;
    Node* second = NULL;

    // create first list 7->5->9->4->6
    push(&first, 6);
    push(&first, 4);
    push(&first, 9);
    push(&first, 5);
    push(&first, 7);
    printf("First List is ");
    printList(first);

    // create second list 8->4
    push(&second, 4);
    push(&second, 8);
    cout << "Second List is ";
    printList(second);

    // Add the two lists and see result
    res = addTwoLists(first, second);
    cout << "Resultant list is ";
    printList(res);

    return 0;
}

// This code is contributed by rathbhupendra

```

## C

```c

#include <stdio.h>
#include <stdlib.h>

/* Linked list node */
struct Node {
    int data;
    struct Node* next;
};

/* Function to create a new node with given data */
struct Node* newNode(int data)
{
    struct Node* new_node
        = (struct Node*)malloc(sizeof(struct Node));
    new_node->data = data;
    new_node->next = NULL;
    return new_node;
}

/* Function to insert a node
at the beginning of the Singly Linked List */
void push(struct Node** head_ref, int new_data)
{
    /* allocate node */
    struct Node* new_node = newNode(new_data);

    /* link the old list off the new node */
    new_node->next = (*head_ref);

    /* move the head to point to the new node */
    (*head_ref) = new_node;
}

/* Adds contents of two linked
 lists and return the head node
 of resultant list */
struct Node* addTwoLists(struct Node* first,
                         struct Node* second)
{

    // res is head node of the resultant list
    struct Node* res = NULL;
    struct Node *temp, *prev = NULL;
    int carry = 0, sum;

    // while both lists exist
    while (first != NULL || second != NULL) {
        // Calculate value of next
        // digit in resultant list.
        // The next digit is sum
        // of following things
        // (i)  Carry
        // (ii) Next digit of first
        // list (if there is a next digit)
        // (ii) Next digit of second
        // list (if there is a next digit)
        sum = carry + (first ? first->data : 0)
              + (second ? second->data : 0);

        // Update carry for next calulation
        carry = (sum >= 10) ? 1 : 0;

        // Update sum if it is greater than 10
        sum = sum % 10;

        // Create a new node with sum as data
        temp = newNode(sum);

        // if this is the first node then
        // set it as head of the resultant list
        if (res == NULL)
            res = temp;
        // If this is not the first node
        // then connect it to the rest.
        else
            prev->next = temp;

        // Set prev for next insertion
        prev = temp;

        // Move first and second
        // pointers to next nodes
        if (first)
            first = first->next;
        if (second)
            second = second->next;
    }

    if (carry > 0)
        temp->next = newNode(carry);

    // return head of the resultant list
    return res;
}

// A utility function to print a linked list
void printList(struct Node* node)
{
    while (node != NULL) {
        printf("%d ", node->data);
        node = node->next;
    }
    printf("\n");
}

/* Driver code */
int main(void)
{
    struct Node* res = NULL;
    struct Node* first = NULL;
    struct Node* second = NULL;

    // create first list 7->5->9->4->6
    push(&first, 6);
    push(&first, 4);
    push(&first, 9);
    push(&first, 5);
    push(&first, 7);
    printf("First List is ");
    printList(first);

    // create second list 8->4
    push(&second, 4);
    push(&second, 8);
    printf("Second List is ");
    printList(second);

    // Add the two lists and see result
    res = addTwoLists(first, second);
    printf("Resultant list is ");
    printList(res);

    return 0;
}

```

## Java

```java

// Java program to add two numbers
// represented by linked list

class LinkedList {

    static Node head1, head2;

    static class Node {

        int data;
        Node next;

        Node(int d)
        {
            data = d;
            next = null;
        }
    }

    /* Adds contents of two linked
lists and return the head node
of resultant list */
    Node addTwoLists(Node first, Node second)
    {
        // res is head node of the resultant list
        Node res = null;
        Node prev = null;
        Node temp = null;
        int carry = 0, sum;

        // while both lists exist
        while (first != null || second != null) {
            // Calculate value of next
            // digit in resultant list.
            // The next digit is sum
            // of following things
            // (i)  Carry
            // (ii) Next digit of first
            // list (if there is a next digit)
            // (ii) Next digit of second
            // list (if there is a next digit)
            sum = carry + (first != null ? first.data : 0)
                  + (second != null ? second.data : 0);

            // update carry for next calulation
            carry = (sum >= 10) ? 1 : 0;

            // update sum if it is greater than 10
            sum = sum % 10;

            // Create a new node with sum as data
            temp = new Node(sum);

            // if this is the first node then set
            // it as head of the resultant list
            if (res == null) {
                res = temp;
            }

            // If this is not the first
            // node then connect it to the rest.
            else {
                prev.next = temp;
            }

            // Set prev for next insertion
            prev = temp;

            // Move first and second pointers
            // to next nodes
            if (first != null) {
                first = first.next;
            }
            if (second != null) {
                second = second.next;
            }
        }

        if (carry > 0) {
            temp.next = new Node(carry);
        }

        // return head of the resultant list
        return res;
    }
    /* Utility function to print a linked list */

    void printList(Node head)
    {
        while (head != null) {
            System.out.print(head.data + " ");
            head = head.next;
        }
        System.out.println("");
    }

    // Driver Code
    public static void main(String[] args)
    {
        LinkedList list = new LinkedList();

        // creating first list
        list.head1 = new Node(7);
        list.head1.next = new Node(5);
        list.head1.next.next = new Node(9);
        list.head1.next.next.next = new Node(4);
        list.head1.next.next.next.next = new Node(6);
        System.out.print("First List is ");
        list.printList(head1);

        // creating seconnd list
        list.head2 = new Node(8);
        list.head2.next = new Node(4);
        System.out.print("Second List is ");
        list.printList(head2);

        // add the two lists and see the result
        Node rs = list.addTwoLists(head1, head2);
        System.out.print("Resultant List is ");
        list.printList(rs);
    }
}

// this code has been contributed by Mayank Jaiswal

```

## 蟒蛇

```

# Python program to add two numbers represented by linked list

# Node class

class Node:

    # Constructor to initialize the node object
    def __init__(self, data):
        self.data = data
        self.next = None

class LinkedList:

    # Function to initialize head
    def __init__(self):
        self.head = None

    # Function to insert a new node at the beginning
    def push(self, new_data):
        new_node = Node(new_data)
        new_node.next = self.head
        self.head = new_node

    # Add contents of two linked lists and return the head
    # node of resultant list
    def addTwoLists(self, first, second):
        prev = None
        temp = None
        carry = 0

        # While both list exists
        while(first is not None or second is not None):

            # Calculate the value of next digit in
            # resultant list
            # The next digit is sum of following things
            # (i) Carry
            # (ii) Next digit of first list (if ther is a
            # next digit)
            # (iii) Next digit of second list ( if there
            # is a next digit)
            fdata = 0 if first is None else first.data
            sdata = 0 if second is None else second.data
            Sum = carry + fdata + sdata

            # update carry for next calculation
            carry = 1 if Sum >= 10 else 0

            # update sum if it is greater than 10
            Sum = Sum if Sum < 10 else Sum % 10

            # Create a new node with sum as data
            temp = Node(Sum)

            # if this is the first node then set it as head
            # of resultant list
            if self.head is None:
                self.head = temp
            else:
                prev.next = temp

            # Set prev for next insertion
            prev = temp

            # Move first and second pointers to next nodes
            if first is not None:
                first = first.next
            if second is not None:
                second = second.next

        if carry > 0:
            temp.next = Node(carry)

    # Utility function to print the linked LinkedList
    def printList(self):
        temp = self.head
        while(temp):
            print temp.data,
            temp = temp.next

# Driver code
first = LinkedList()
second = LinkedList()

# Create first list
first.push(6)
first.push(4)
first.push(9)
first.push(5)
first.push(7)
print "First List is ",
first.printList()

# Create second list
second.push(4)
second.push(8)
print "\nSecond List is ",
second.printList()

# Add the two lists and see result
res = LinkedList()
res.addTwoLists(first.head, second.head)
print "\nResultant list is ",
res.printList()

# This code is contributed by Nikhil Kumar Singh(nickzuck_007)

```

## C#

```cs

// C# program to add two numbers
// represented by linked list
using System;

public class LinkedList {

    Node head1, head2;

    public class Node {
        public int data;
        public Node next;

        public Node(int d)
        {
            data = d;
            next = null;
        }
    }

    /* Adds contents of two linked lists
    and return the head node of resultant list */
    Node addTwoLists(Node first, Node second)
    {
        // res is head node of the resultant list
        Node res = null;
        Node prev = null;
        Node temp = null;
        int carry = 0, sum;

        // while both lists exist
        while (first != null || second != null) {
            // Calculate value of next digit in resultant
            // list. The next digit is sum of following
            // things (i) Carry (ii) Next digit of first
            // list (if there is a next digit) (ii) Next
            // digit of second list (if there is a next
            // digit)
            sum = carry + (first != null ? first.data : 0)
                  + (second != null ? second.data : 0);

            // update carry for next calulation
            carry = (sum >= 10) ? 1 : 0;

            // update sum if it is greater than 10
            sum = sum % 10;

            // Create a new node with sum as data
            temp = new Node(sum);

            // if this is the first node then set it as head
            // of the resultant list
            if (res == null) {
                res = temp;
            }

            // If this is not the first
            // node then connect it to the rest.
            else {
                prev.next = temp;
            }

            // Set prev for next insertion
            prev = temp;

            // Move first and second pointers to next nodes
            if (first != null) {
                first = first.next;
            }
            if (second != null) {
                second = second.next;
            }
        }

        if (carry > 0) {
            temp.next = new Node(carry);
        }

        // return head of the resultant list
        return res;
    }
    /* Utility function to print a linked list */

    void printList(Node head)
    {
        while (head != null) {
            Console.Write(head.data + " ");
            head = head.next;
        }
        Console.WriteLine("");
    }

    // Driver code
    public static void Main(String[] args)
    {
        LinkedList list = new LinkedList();

        // creating first list
        list.head1 = new Node(7);
        list.head1.next = new Node(5);
        list.head1.next.next = new Node(9);
        list.head1.next.next.next = new Node(4);
        list.head1.next.next.next.next = new Node(6);
        Console.Write("First List is ");
        list.printList(list.head1);

        // creating seconnd list
        list.head2 = new Node(8);
        list.head2.next = new Node(4);
        Console.Write("Second List is ");
        list.printList(list.head2);

        // add the two lists and see the result
        Node rs = list.addTwoLists(list.head1, list.head2);
        Console.Write("Resultant List is ");
        list.printList(rs);
    }
}

// This code contributed by Rajput-Ji

```

**Output**

```
First List is 7 5 9 4 6 
Second List is 8 4 
Resultant list is 5 0 0 5 6 

```

**复杂度分析：**

*   **时间复杂度：** O（m + n），其中 m 和 n 分别是第一列表和第二列表中的节点数。

    列表仅需要遍历一次。

*   **空间复杂度：** O（m + n）。

    需要一个临时链表来存储输出编号

https://www.youtube.com/watch?v=LLPuC5kWD8U 

相关文章：[添加两个由链表表示的数字| 设置 2](https://www.geeksforgeeks.org/sum-of-two-linked-lists/)

如果您发现上述代码/算法有误，请写评论，或者找到其他解决相同问题的方法。

