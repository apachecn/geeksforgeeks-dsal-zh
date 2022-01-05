# 使用双向链表的多项式偏导数

> 原文:[https://www . geesforgeks . org/多项式的偏导数使用双链表/](https://www.geeksforgeeks.org/partial-derivative-of-a-polynomial-using-doubly-linked-list/)

给定一个由[双链表](https://www.geeksforgeeks.org/doubly-linked-list/)表示的 2 变量[多项式](https://en.wikipedia.org/wiki/Polynomial)，任务是找到存储在双链表中的多项式的[偏导数](https://en.wikipedia.org/wiki/Partial_derivative)。

**示例:**

> **输入:** P(x，y)= 2(x^3 y^4)+3(x^5 y^7)+1(x^2 y^6)
> **输出:**
> 偏导数 w.r.t. x:6(x^2 y^4)+15(x^4 y^7)+2(x^1 y^6)
> 偏导数 w . r . t . y:24(x^2 y^3)+105(x^4 y^6)+12(x 1y 5)
> 偏导数 w . r . t . x 和 y:144(x 1y 2)+2520(x 3y 5)+60(x 0y 4)
> 
> **输入:** P(x，y)= 3(x^2 y^1)+4(x^2 y^3)+2(x^4 y^7)
> **输出:**
> 偏导数 w.r.t. x:6(x^1 y^1)+8(x^1 y^3)+8(x^3 y^7)
> 偏导数 w . r . t . y:6(x^1 y^0)+24(x^1 y^2)+56(x 3y 6)
> 偏导数 w . r . t . x 和 y:48(x 0y 1)+1008(x 2y 5)

**方法:**按照以下步骤解决这个问题:

*   声明一个[类](https://www.geeksforgeeks.org/c-classes-and-objects/)或[结构](https://www.geeksforgeeks.org/structures-in-cpp/)来存储一个节点的内容，即**数据**代表系数，**幂 1** 代表 **x** 上升到的幂，**幂 2** 代表 **y** 上升到的幂，以及指向其下一个和**上一个**节点的指针。
*   声明计算关于 **x** 的导数、关于 **y** 的导数以及关于 **x** 和 **y** 的导数的函数。
*   计算并打印得到的导数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Structure of a node
struct node {
    node* link1 = NULL;
    node* link2 = NULL;
    int data = 0;
    int pow1 = 0;
    int pow2 = 0;
};

// Function to generate Doubly Linked
// List from given parameters
void input_equation(node*& head, int d,
                    int p1, int p2)
{
    node* temp = head;

    // If list is empty
    if (head == NULL) {

        // Create new node
        node* ptr = new node();
        ptr->data = d;
        ptr->pow1 = p1;
        ptr->pow2 = p2;

        // Set it as the head
        // of the linked list
        head = ptr;
    }

    // If list is not empty
    else {

        // Temporarily store
        // address of the head node
        temp = head;

        // Traverse the linked list
        while (temp->link2 != NULL) {

            // Link to next node
            temp = temp->link2;
        }

        // Create new node
        node* ptr = new node();
        ptr->data = d;
        ptr->pow1 = p1;
        ptr->pow2 = p2;

        // Connect the nodes
        ptr->link1 = temp;
        temp->link2 = ptr;
    }
}

// Function to calculate partial
// derivative w.r.t. X
void derivation_with_x(node*& head)
{
    cout << "Partial derivatives"
         << " w.r.t. x: ";

    node* temp = head;

    // Traverse the Linked List
    while (temp != NULL) {

        if (temp->pow1 != 0) {
            temp->data = (temp->data)
                         * (temp->pow1);
            temp->pow1 = temp->pow1 - 1;
        }
        else {
            temp->data = 0;
            temp->pow1 = 0;
            temp->pow2 = 0;
        }

        temp = temp->link2;
    }

    temp = head;

    cout << " " << temp->data
         << "(x^" << temp->pow1
         << " y^" << temp->pow2
         << ")";
    temp = temp->link2;

    while (temp != NULL) {
        cout << " + "
             << temp->data << "(x^"
             << temp->pow1 << " y^"
             << temp->pow2 << ")";
        temp = temp->link2;
    }

    cout << "\n";
}

// Function to calculate partial
// derivative w.r.t. Y
void derivation_with_y(node*& head)
{
    cout << "Partial derivatives"
         << " w.r.t. y: ";

    node* temp = head;

    // Traverse the Linked List
    while (temp != NULL) {

        if (temp->pow2 != 0) {
            temp->data = (temp->data)
                         * (temp->pow2);
            temp->pow2 = temp->pow2 - 1;
        }
        else {
            temp->data = 0;
            temp->pow1 = 0;
            temp->pow2 = 0;
        }

        temp = temp->link2;
    }

    temp = head;
    cout << " "
         << temp->data
         << "(x^" << temp->pow1
         << " y^"
         << temp->pow2 << ")";
    temp = temp->link2;

    while (temp != NULL) {
        cout << " + "
             << temp->data << "(x^"
             << temp->pow1 << " y^"
             << temp->pow2 << ")";
        temp = temp->link2;
    }
    cout << "\n";
}

// Function to calculate partial
// derivative w.r.t. XY
void derivation_with_x_y(node*& head)
{
    cout << "Partial derivatives"
         << " w.r.t. x and y: ";

    node* temp = head;

    // Derivative with respect to
    // the first variable
    while (temp != NULL) {
        if (temp->pow1 != 0) {

            temp->data = (temp->data)
                         * (temp->pow1);
            temp->pow1 = temp->pow1 - 1;
        }

        else {
            temp->data = 0;
            temp->pow1 = 0;
            temp->pow2 = 0;
        }

        temp = temp->link2;
    }
    temp = head;

    // Derivative with respect to
    // the second variable
    while (temp != NULL) {

        if (temp->pow2 != 0) {
            temp->data = (temp->data)
                         * (temp->pow2);
            temp->pow2 = temp->pow2 - 1;
        }

        else {
            temp->data = 0;
            temp->pow1 = 0;
            temp->pow2 = 0;
        }

        temp = temp->link2;
    }

    temp = head;
    cout << " "
         << temp->data << "(x^"
         << temp->pow1 << " y^"
         << temp->pow2 << ")";

    temp = temp->link2;

    // Print the list after the
    // calculating the derivative
    while (temp != NULL) {

        cout << " + "
             << temp->data << "(x^"
             << temp->pow1 << " y^"
             << temp->pow2 << ")";
        temp = temp->link2;
    }
    cout << "\n";
}

// Driver Code
int main()
{
    node* head1 = NULL;

    // Creating doubly-linked list
    input_equation(head1, 2, 3, 4);
    input_equation(head1, 3, 5, 7);
    input_equation(head1, 1, 2, 6);

    // Function Call
    derivation_with_x(head1);
    derivation_with_y(head1);
    derivation_with_x_y(head1);

    return 0;
}
```

**Output:** 

```
Partial derivatives w.r.t. x:  6(x^2 y^4) + 15(x^4 y^7) + 2(x^1 y^6)
Partial derivatives w.r.t. y:  24(x^2 y^3) + 105(x^4 y^6) + 12(x^1 y^5)
Partial derivatives w.r.t. x and y:  144(x^1 y^2) + 2520(x^3 y^5) + 60(x^0 y^4)
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)