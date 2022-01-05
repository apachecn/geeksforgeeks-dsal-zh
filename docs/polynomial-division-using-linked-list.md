# 使用链表进行多项式除法

> 原文:[https://www . geesforgeks . org/多项式除法-使用-链表/](https://www.geeksforgeeks.org/polynomial-division-using-linked-list/)

给定两个分别为[单链表](https://www.geeksforgeeks.org/data-structures/linked-list/singly-linked-list/)形式的多项式 **P1** 和 **P2** ，任务是打印单链表形式的商和余数表达式，通过将多项式 **P1** 除以 **P2** 得到。

***注:**假设多项式表示为 x 的**高次幂到 x** 的**低次幂(即 0)。***

**示例:**

> **输入:** P1 = 5 - > 4 - > 2，P2 = 5 - > 5
> **输出:**
> 商= 1 - > 0.2
> 余数= 3
> 
> **输入:** P1 = 3 - > 5 - > 2，P2 = 2 - > 1
> **输出:**
> 商= 1.5 - > 1.75
> 余数= 0.25

**方法:**按照以下步骤解决问题:

*   创建两个单链表，**商**和**余数**，其中每个节点将由 x 的幂系数和指向下一个节点的指针组成。
*   当**余数**的度数小于**除数**的度数时，执行以下操作:
    *   将**被除数**的前导项的幂减去**除数**的幂，存入**幂**。
    *   将**被除数**的前导项的系数除以**除数**，并存储在变量**系数**中。
    *   根据在**步骤 1** 和**步骤 2** 中形成的术语创建一个新节点 **N** ，并在**商**列表中插入 **N** 。
    *   用**除数**乘以 N，从得到的结果中减去**被除数**。
*   完成上述步骤后，打印**商**和**余数**列表。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Node structure containing power and
// coefficient of variable
struct Node {
    float coeff;
    int pow;
    struct Node* next;
};

// Function to create new node
void create_node(float x, int y,
                 struct Node** temp)
{
    struct Node *r, *z;
    z = *temp;

    // If temp is NULL
    if (z == NULL) {

        r = (struct Node*)malloc(
            sizeof(struct Node));

        // Update coefficient and
        // power in the LL z
        r->coeff = x;
        r->pow = y;
        *temp = r;
        r->next = (struct Node*)malloc(
            sizeof(struct Node));
        r = r->next;
        r->next = NULL;
    }

    // Otherwise
    else {
        r->coeff = x;
        r->pow = y;
        r->next = (struct Node*)malloc(
            sizeof(struct Node));
        r = r->next;
        r->next = NULL;
    }
}

// Function to create a LL that stores
// the value of the quotient while
// performing polynomial division
void store_quotient(float mul_c, int diff,
                    struct Node* quo)
{
    // Till quo is non-empty
    while (quo->next != NULL) {
        quo = quo->next;
    }

    // Update powers and coefficient
    quo->pow = diff;
    quo->coeff = mul_c;
    quo->next = (struct Node*)malloc(
        sizeof(struct Node));
    quo = quo->next;
    quo->next = NULL;
}

// Function to create a new polynomial
// whenever subtraction is performed
// in polynomial division
void formNewPoly(int diff, float mul_c,
                 struct Node* poly)
{
    // Till poly is not empty
    while (poly->next != NULL) {
        poly->pow += diff;
        poly->coeff *= mul_c;
        poly = poly->next;
    }
}

// Function to copy one polynomial
// into another linkedlist
void copyList(struct Node* r,
              struct Node** copy)
{
    // Copy the values of r in the
    // polynomial copy
    while (r != NULL) {

        struct Node* z
            = (struct Node*)malloc(
                sizeof(struct Node));

        // Store coefficient and power
        z->coeff = r->coeff;
        z->pow = r->pow;
        z->next = NULL;

        struct Node* dis = *copy;
        if (dis == NULL) {
            *copy = z;
        }
        else {
            while (dis->next != NULL) {
                dis = dis->next;
            }
            dis->next = z;
        }
        r = r->next;
    }
}

// Function to subtract two polynomial
void polySub(struct Node* poly1,
             struct Node* poly2,
             struct Node* poly)
{

    // Compute until poly1 and poly2 is empty
    while (poly1->next && poly2->next) {

        // If power of 1st polynomial
        // > 2nd, then store 1st as
        // it is and move its pointer
        if (poly1->pow > poly2->pow) {

            poly->pow = poly1->pow;
            poly->coeff = poly1->coeff;
            poly1 = poly1->next;
            poly->next
                = (struct Node*)malloc(
                    sizeof(struct Node));
            poly = poly->next;
            poly->next = NULL;
        }

        // If power of 2nd polynomial >
        // 1st then store 2nd as it is
        // and move its pointer
        else if (poly1->pow < poly2->pow) {

            poly->pow = poly2->pow;
            poly->coeff = -1 * poly2->coeff;
            poly2 = poly2->next;
            poly->next
                = (struct Node*)malloc(
                    sizeof(struct Node));
            poly = poly->next;
            poly->next = NULL;
        }

        // If power of both polynomial
        // is same then subtract their
        // coefficients
        else {

            if ((poly1->coeff
                 - poly2->coeff)
                != 0) {

                poly->pow = poly1->pow;
                poly->coeff = (poly1->coeff
                               - poly2->coeff);

                poly->next = (struct Node*)malloc(
                    sizeof(struct Node));
                poly = poly->next;
                poly->next = NULL;
            }

            // Update the pointers
            // poly1 and poly2
            poly1 = poly1->next;
            poly2 = poly2->next;
        }
    }

    // Add the remaining value of polynomials
    while (poly1->next || poly2->next) {

        // If poly1 exists
        if (poly1->next) {
            poly->pow = poly1->pow;
            poly->coeff = poly1->coeff;
            poly1 = poly1->next;
        }

        // If poly2 exists
        if (poly2->next) {
            poly->pow = poly2->pow;
            poly->coeff = -1 * poly2->coeff;
            poly2 = poly2->next;
        }

        // Add the new node to poly
        poly->next
            = (struct Node*)malloc(
                sizeof(struct Node));
        poly = poly->next;
        poly->next = NULL;
    }
}

// Function to display linked list
void show(struct Node* node)
{
    int count = 0;
    while (node->next != NULL
           && node->coeff != 0) {

        // If count is non-zero, then
        // print the postitive value
        if (count == 0)
            cout << node->coeff;

        // Otherwise
        else
            cout << abs(node->coeff);
        count++;

        // Print polynomial power
        if (node->pow != 0)
            cout << "x^" << node->pow;
        node = node->next;

        if (node->next != NULL)

            // If coeff of next term
            // > 0 then next sign will
            // be positive else negative
            if (node->coeff > 0)
                cout << " + ";
            else
                cout << " - ";
    }

    cout << "\n";
}

// Function to divide two polynomials
void divide_poly(struct Node* poly1,
                 struct Node* poly2)
{
    // Initialize Remainder and Quotient
    struct Node *rem = NULL, *quo = NULL;

    quo = (struct Node*)malloc(
        sizeof(struct Node));
    quo->next = NULL;

    struct Node *q = NULL, *r = NULL;

    // Copy poly1, i.e., dividend to q
    copyList(poly1, &q);

    // Copy poly, i.e., divisor to r
    copyList(poly2, &r);

    // Perform polynomial subtraction till
    // highest power of q > highest power of divisor
    while (q != NULL
           && (q->pow >= poly2->pow)) {

        // difference of power
        int diff = q->pow - poly2->pow;

        float mul_c = (q->coeff
                       / poly2->coeff);

        // Stores the quotient node
        store_quotient(mul_c, diff,
                       quo);

        struct Node* q2 = NULL;

        // Copy one LL in another LL
        copyList(r, &q2);

        // formNewPoly forms next value
        // of q after performing the
        // polynomial subtraction
        formNewPoly(diff, mul_c, q2);

        struct Node* store = NULL;
        store = (struct Node*)malloc(
            sizeof(struct Node));

        // Perform polynomial subtraction
        polySub(q, q2, store);

        // Now change value of q to the
        // subtracted value i.e., store
        q = store;
        free(q2);
    }

    // Print the quotient
    cout << "Quotient: ";
    show(quo);

    // Print the remainder
    cout << "Remainder: ";
    rem = q;
    show(rem);
}

// Driver Code
int main()
{
    struct Node* poly1 = NULL;
    struct Node *poly2 = NULL, *poly = NULL;

    // Create 1st Polynomial (Dividend):
    // 5x^2 + 4x^1 + 2
    create_node(5.0, 2, &poly1);
    create_node(4.0, 1, &poly1);
    create_node(2.0, 0, &poly1);

    // Create 2nd Polynomial (Divisor):
    // 5x^1 + 5
    create_node(5.0, 1, &poly2);
    create_node(5.0, 0, &poly2);

    // Function Call
    divide_poly(poly1, poly2);

    return 0;
}
```

**Output:** 

```
Quotient: 1x^1 - 0.2
Remainder: 3
```

***时间复杂度:** O(M + N)*
***辅助空间:** O(M + N)*