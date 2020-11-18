# 使用链表

> 原文：[https://www.geeksforgeeks.org/multiplication-of-two-polynomials-using-linked-list/](https://www.geeksforgeeks.org/multiplication-of-two-polynomials-using-linked-list/)

的两个多项式相乘

给定两个多项式形式的链表。 任务是找到两个多项式的乘法。

**示例**：

```
Input: Poly1: 3x^2 + 5x^1 + 6, Poly2: 6x^1 + 8
Output: 18x^3 + 54x^2 + 76x^1 + 48
On multiplying each element of 1st polynomial with 
elements of 2nd polynomial, we get
18x^3 + 24x^2 + 30x^2 + 40x^1 + 36x^1 + 48
On adding values with same power of x,
18x^3 + 54x^2 + 76x^1 + 48

Input: Poly1: 3x^3 + 6x^1 - 9, Poly2: 9x^3 - 8x^2 + 7x^1 + 2
Output: 27x^6 - 24x^5 + 75x^4 - 123x^3 + 114x^2 - 51x^1 - 18

```

![](img/f8a00d4931ebbd6b5a6bec564954f368.png)

**方法**：

1.  在这种方法中，我们将第二个多项式与第一个多项式的每个项相乘。

2.  将相乘的值存储在新的链表中。

3.  然后，我们将在所得多项式中相加具有相同功效的元素的系数。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation of the above approach
#include <bits/stdc++.h>
using namespace std;

// Node structure containing powerer
// and coefficient of variable
struct Node {
    int coeff, power;
    Node* next;
};

// Function add a new node at the end of list
Node* addnode(Node* start, int coeff, int power)
{
    // Create a new node
    Node* newnode = new Node;
    newnode->coeff = coeff;
    newnode->power = power;
    newnode->next = NULL;

    // If linked list is empty
    if (start == NULL)
        return newnode;

    // If linked list has nodes
    Node* ptr = start;
    while (ptr->next != NULL)
        ptr = ptr->next;
    ptr->next = newnode;

    return start;
}

// Functionn To Display The Linked list
void printList(struct Node* ptr)
{
    while (ptr->next != NULL) {
        cout << ptr->coeff << "x^" << ptr->power ;
       if( ptr->next!=NULL && ptr->next->coeff >=0)
          cout << "+";

        ptr = ptr->next;
    }
    cout << ptr->coeff << "\n";
}

// Function to add coefficients of
// two elements having same powerer
void removeDuplicates(Node* start)
{
    Node *ptr1, *ptr2, *dup;
    ptr1 = start;

    /* Pick elements one by one */
    while (ptr1 != NULL && ptr1->next != NULL) {
        ptr2 = ptr1;

        // Compare the picked element
        // with rest of the elements
        while (ptr2->next != NULL) {

            // If powerer of two elements are same
            if (ptr1->power == ptr2->next->power) {

                // Add their coefficients and put it in 1st element
                ptr1->coeff = ptr1->coeff + ptr2->next->coeff;
                dup = ptr2->next;
                ptr2->next = ptr2->next->next;

                // remove the 2nd element
                delete (dup);
            }
            else
                ptr2 = ptr2->next;
        }
        ptr1 = ptr1->next;
    }
}

// Function two Multiply two polynomial Numbers
Node* multiply(Node* poly1, Node* poly2,
               Node* poly3)
{

    // Create two pointer and store the
    // address of 1st and 2nd polynomials
    Node *ptr1, *ptr2;
    ptr1 = poly1;
    ptr2 = poly2;
    while (ptr1 != NULL) {
        while (ptr2 != NULL) {
            int coeff, power;

            // Multiply the coefficient of both
            // polynomials and store it in coeff
            coeff = ptr1->coeff * ptr2->coeff;

            // Add the powerer of both polynomials
            // and store it in power
            power = ptr1->power + ptr2->power;

            // Invoke addnode function to create
            // a newnode by passing three parameters
            poly3 = addnode(poly3, coeff, power);

            // move the pointer of 2nd polynomial
            // two get its next term
            ptr2 = ptr2->next;
        }

        // Move the 2nd pointer to the
        // starting point of 2nd polynomial
        ptr2 = poly2;

        // move the pointer of 1st polynomial
        ptr1 = ptr1->next;
    }

    // this function will be invoke to add
    // the coefficient of the elements
    // having same powerer from the resultant linked list
    removeDuplicates(poly3);
    return poly3;
}

// Driver Code
int main()
{

    Node *poly1 = NULL, *poly2 = NULL, *poly3 = NULL;

    // Creation of 1st Polynomial: 3x^2 + 5x^1 + 6
    poly1 = addnode(poly1, 3, 3);
    poly1 = addnode(poly1, 6, 1);
    poly1 = addnode(poly1, -9, 0);

    // Creation of 2nd polynomial: 6x^1 + 8
    poly2 = addnode(poly2, 9, 3);
    poly2 = addnode(poly2, -8, 2);
    poly2 = addnode(poly2, 7, 1);
    poly2 = addnode(poly2, 2, 0);

    // Displaying 1st polynomial
    cout << "1st Polynomial:- ";
    printList(poly1);

    // Displaying 2nd polynomial
    cout << "2nd Polynomial:- ";
    printList(poly2);

    // calling multiply function
    poly3 = multiply(poly1, poly2, poly3);

    // Displaying Resultant Polynomial
    cout << "Resultant Polynomial:- ";
    printList(poly3);

    return 0;
}

```

## Java

```java

// Java implementation of above approach 
import java.util.*;
class GFG
{

// Node structure containing powerer 
// and coefficient of variable 
static class Node { 
    int coeff, power; 
    Node next; 
}; 

// Function add a new node at the end of list 
static Node addnode(Node start, int coeff, int power) 
{ 
    // Create a new node 
    Node newnode = new Node(); 
    newnode.coeff = coeff; 
    newnode.power = power; 
    newnode.next = null; 

    // If linked list is empty 
    if (start == null) 
        return newnode; 

    // If linked list has nodes 
    Node ptr = start; 
    while (ptr.next != null) 
        ptr = ptr.next; 
    ptr.next = newnode; 

    return start; 
} 

// Functionn To Display The Linked list 
static void printList( Node ptr) 
{ 
    while (ptr.next != null) { 
        System.out.print( ptr.coeff + "x^" + ptr.power + " + "); 

        ptr = ptr.next; 
    } 
    System.out.print( ptr.coeff  +"\n"); 
} 

// Function to add coefficients of 
// two elements having same powerer 
static void removeDuplicates(Node start) 
{ 
    Node ptr1, ptr2, dup; 
    ptr1 = start; 

    /* Pick elements one by one */
    while (ptr1 != null && ptr1.next != null) { 
        ptr2 = ptr1; 

        // Compare the picked element 
        // with rest of the elements 
        while (ptr2.next != null) { 

            // If powerer of two elements are same 
            if (ptr1.power == ptr2.next.power) { 

                // Add their coefficients and put it in 1st element 
                ptr1.coeff = ptr1.coeff + ptr2.next.coeff; 
                dup = ptr2.next; 
                ptr2.next = ptr2.next.next; 

            } 
            else
                ptr2 = ptr2.next; 
        } 
        ptr1 = ptr1.next; 
    } 
} 

// Function two Multiply two polynomial Numbers 
static Node multiply(Node poly1, Node poly2, 
            Node poly3) 
{ 

    // Create two pointer and store the 
    // address of 1st and 2nd polynomials 
    Node ptr1, ptr2; 
    ptr1 = poly1; 
    ptr2 = poly2; 
    while (ptr1 != null) { 
        while (ptr2 != null) { 
            int coeff, power; 

            // Multiply the coefficient of both 
            // polynomials and store it in coeff 
            coeff = ptr1.coeff * ptr2.coeff; 

            // Add the powerer of both polynomials 
            // and store it in power 
            power = ptr1.power + ptr2.power; 

            // Invoke addnode function to create 
            // a newnode by passing three parameters 
            poly3 = addnode(poly3, coeff, power); 

            // move the pointer of 2nd polynomial 
            // two get its next term 
            ptr2 = ptr2.next; 
        } 

        // Move the 2nd pointer to the 
        // starting point of 2nd polynomial 
        ptr2 = poly2; 

        // move the pointer of 1st polynomial 
        ptr1 = ptr1.next; 
    } 

    // this function will be invoke to add 
    // the coefficient of the elements 
    // having same powerer from the resultant linked list 
    removeDuplicates(poly3); 
    return poly3; 
} 

// Driver Code 
public static void main(String args[]) 
{ 

    Node poly1 = null, poly2 = null, poly3 = null; 

    // Creation of 1st Polynomial: 3x^2 + 5x^1 + 6 
    poly1 = addnode(poly1, 3, 2); 
    poly1 = addnode(poly1, 5, 1); 
    poly1 = addnode(poly1, 6, 0); 

    // Creation of 2nd polynomial: 6x^1 + 8 
    poly2 = addnode(poly2, 6, 1); 
    poly2 = addnode(poly2, 8, 0); 

    // Displaying 1st polynomial 
    System.out.print("1st Polynomial:- "); 
    printList(poly1); 

    // Displaying 2nd polynomial 
    System.out.print("2nd Polynomial:- "); 
    printList(poly2); 

    // calling multiply function 
    poly3 = multiply(poly1, poly2, poly3); 

    // Displaying Resultant Polynomial 
    System.out.print( "Resultant Polynomial:- "); 
    printList(poly3); 

} 

}
// This code is contributed by Arnab Kundu

```

## C#

```cs

// C# implementation of above approach 
using System;

class GFG
{

// Node structure containing powerer 
// and coefficient of variable 
public class Node 
{ 
    public int coeff, power; 
    public Node next; 
}; 

// Function add a new node at the end of list 
static Node addnode(Node start, int coeff, int power) 
{ 
    // Create a new node 
    Node newnode = new Node(); 
    newnode.coeff = coeff; 
    newnode.power = power; 
    newnode.next = null; 

    // If linked list is empty 
    if (start == null) 
        return newnode; 

    // If linked list has nodes 
    Node ptr = start; 
    while (ptr.next != null) 
        ptr = ptr.next; 
    ptr.next = newnode; 

    return start; 
} 

// Functionn To Display The Linked list 
static void printList( Node ptr) 
{ 
    while (ptr.next != null) 
    { 
        Console.Write( ptr.coeff + "x^" + ptr.power + " + "); 

        ptr = ptr.next; 
    } 
    Console.Write( ptr.coeff +"\n"); 
} 

// Function to add coefficients of 
// two elements having same powerer 
static void removeDuplicates(Node start) 
{ 
    Node ptr1, ptr2, dup; 
    ptr1 = start; 

    /* Pick elements one by one */
    while (ptr1 != null && ptr1.next != null)
    { 
        ptr2 = ptr1; 

        // Compare the picked element 
        // with rest of the elements 
        while (ptr2.next != null) 
        { 

            // If powerer of two elements are same 
            if (ptr1.power == ptr2.next.power) 
            { 

                // Add their coefficients and put it in 1st element 
                ptr1.coeff = ptr1.coeff + ptr2.next.coeff; 
                dup = ptr2.next; 
                ptr2.next = ptr2.next.next; 

            } 
            else
                ptr2 = ptr2.next; 
        } 
        ptr1 = ptr1.next; 
    } 
} 

// Function two Multiply two polynomial Numbers 
static Node multiply(Node poly1, Node poly2, 
            Node poly3) 
{ 

    // Create two pointer and store the 
    // address of 1st and 2nd polynomials 
    Node ptr1, ptr2; 
    ptr1 = poly1; 
    ptr2 = poly2; 
    while (ptr1 != null)
    { 
        while (ptr2 != null) 
        { 
            int coeff, power; 

            // Multiply the coefficient of both 
            // polynomials and store it in coeff 
            coeff = ptr1.coeff * ptr2.coeff; 

            // Add the powerer of both polynomials 
            // and store it in power 
            power = ptr1.power + ptr2.power; 

            // Invoke addnode function to create 
            // a newnode by passing three parameters 
            poly3 = addnode(poly3, coeff, power); 

            // move the pointer of 2nd polynomial 
            // two get its next term 
            ptr2 = ptr2.next; 
        } 

        // Move the 2nd pointer to the 
        // starting point of 2nd polynomial 
        ptr2 = poly2; 

        // move the pointer of 1st polynomial 
        ptr1 = ptr1.next; 
    } 

    // this function will be invoke to add 
    // the coefficient of the elements 
    // having same powerer from the resultant linked list 
    removeDuplicates(poly3); 
    return poly3; 
} 

// Driver Code 
public static void Main(String []args) 
{ 

    Node poly1 = null, poly2 = null, poly3 = null; 

    // Creation of 1st Polynomial: 3x^2 + 5x^1 + 6 
    poly1 = addnode(poly1, 3, 2); 
    poly1 = addnode(poly1, 5, 1); 
    poly1 = addnode(poly1, 6, 0); 

    // Creation of 2nd polynomial: 6x^1 + 8 
    poly2 = addnode(poly2, 6, 1); 
    poly2 = addnode(poly2, 8, 0); 

    // Displaying 1st polynomial 
    Console.Write("1st Polynomial:- "); 
    printList(poly1); 

    // Displaying 2nd polynomial 
    Console.Write("2nd Polynomial:- "); 
    printList(poly2); 

    // calling multiply function 
    poly3 = multiply(poly1, poly2, poly3); 

    // Displaying Resultant Polynomial 
    Console.Write( "Resultant Polynomial:- "); 
    printList(poly3); 
} 
}

// This code has been contributed by 29AjayKumar

```

**Output**

```
1st Polynomial:- 3x^3+6x^1-9
2nd Polynomial:- 9x^3-8x^2+7x^1+2
Resultant Polynomial:- 27x^6-24x^5+75x^4-123x^3+114x^2-51x^1-18

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。