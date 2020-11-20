# 使用循环链表相加两个多项式

> 原文：[https://www.geeksforgeeks.org/adding-two-polynomials-using-circular-linked-list/](https://www.geeksforgeeks.org/adding-two-polynomials-using-circular-linked-list/)



给出[循环链表](https://www.geeksforgeeks.org/circular-linked-list/)表示的两个多项式，任务是[通过添加同一变量的幂的系数来将这两个多项式](https://www.geeksforgeeks.org/adding-two-polynomials-using-linked-list/)相加。

**注意**：在给定的多项式中，包含`x`的更高幂的项将首先出现。

**示例**：

> **输入**：
>
> 第一个数字：`5x ^ 2 * y ^ 1 + 4x ^ 1 * y ^ 2 + 3x ^ 1 * y ^ 1 + 2x ^ 1`
>
> 第二个数字：`3x ^ 1 * y ^ 2 + 4x ^ 1`
>
> **输出**：
>
> `5x ^ 2 * y ^ 1 + 7x ^ 1 * y ^ 2 + 3x ^ 1 * y ^ 1 + 6x ^ 1`
>
> **说明**：
>
> 第一个数字`x ^ 2 * y ^ 1`的系数是 5，第二个数字是 0。 因此，`x ^ 2 * Y ^ 1`的总和为 5。
>
> 第一个数字`x ^ 1 * y ^ 2`的系数在第二个数字中为 4 和 3。 因此，`x ^ 1 * Y ^ 2`的系数之和为 7。
>
> 第一个数字`x ^ 1 * y ^ 1`的系数为 3，第二个数字为 0。 因此，`x ^ 1 * Y ^ 1`的系数之和为 2。
>
> 第一个数字`x ^ 1 * Y ^ 0`的系数为 2，第二个数字为 4。 因此，`x ^ 1 * Y ^ 0`的系数之和为 6。
> 
> **输入**：
>
> 第一个数字：`3x ^ 3 * y ^ 2 + 2x ^ 2 + 5x ^ 1 * y ^ 1 + 9y ^ 1 + 2`
>
> 第二个数字：`4x ^ 3 * y ^ 3 + 2x ^ 3 * y ^ 2 + 1y ^ 2 + 3`
>
> **输出**：
>
> `4x ^ 3 * y ^ 3 + 5x ^ 3 * y ^ 2 + 2x ^ 2 + 5x ^ 1 * y ^ 1 + 1y ^ 2 + 9y ^ 1 + 5`

**方法**：请按照以下步骤解决问题：

1.  创建[两个循环链表](https://www.geeksforgeeks.org/circular-linked-list/)，其中每个节点将由系数，`x`的功效，`y`的功效以及指向下一个节点的指针组成。

2.  遍历两个多项式并检查以下条件：

    *   如果第一多项式的`x`的幂大于第二多项式的`x`的幂，则将第一多项式的节点存储在所得多项式中，并增加多项式`1`的计数器。

    *   如果第一个多项式的`x`的幂小于第二个多项式的`x`的幂，则将第二个多项式的节点存储在所得多项式中，并增加多项式`2`的计数器 。

    *   如果第一个多项式的`x`的幂等于第二个多项式的`x`的幂，并且`y`的幂大于第二个多项式的`y`的幂。 然后，将第一个多项式的节点存储在结果多项式中，并增加多项式`1`的计数器。

    *   如果第一个多项式的`x`的幂等于第二个多项式的`x`的幂，并且第二个多项式的`y`的幂等于第一个多项式的`y`的幂，然后，将两个多项式的系数之和存储在结果多项式中，并同时增加多项式`1`和多项式`2`的计数。

3.  如果在第一多项式或第二多项式中还有要遍历的节点，则将其附加到结果多项式中。

4.  最后，打印结果多项式。

下面是上述方法的实现：

## C++

```cpp

// C++ program to implement 
// the above approach 

#include <bits/stdc++.h> 
using namespace std; 

// Structure of a node 
// in a circular linked list 
struct Node { 

    // Stores coefficient 
    // of a node 
    int coeff; 

    // Stores power of' 
    // variable x of a node 
    int powx; 

    // Stores power of 
    // variable y of a node 
    int powy; 

    // Stores pointer  
    // to next node 
    struct Node* next; 
}; 

// Function to dynamically create a node 
void create_node(int c, int p1, int p2,  
                        struct Node** temp) 
{ 

    // Stores new node 
    struct Node *r; 

    // Stores temp node 
    struct Node *z  
              = *temp; 

    // Dyanamically create a new node 
    r = (struct Node*)malloc( 
                  sizeof(struct Node)); 

    // Update coefficient 
    // of r               
    r->coeff = c; 

    // Update power of  
    // variable x in r 
    r->powx = p1; 

    // Update power of  
    // variable y in r 
    r->powy = p2; 

    // If z is null 
    if (z == NULL) { 

        // Update temp node 
        (*temp) = r; 

        // Update next pointer 
        // of temp node 
        (*temp)->next = (*temp); 
    } 
    else { 

        // Update next pointer 
        // of z 
        r->next = z->next; 

        // Update next pointer 
        // of z 
        z->next = r; 

        // Update temp Node 
        (*temp) = r; 
    } 
} 

// Function to add polynomial of two list 
void add_poly(struct Node* poly1,  
    struct Node* poly2, struct Node** temp) 
{ 

    // Stores head node of polynomial1 
    struct Node *start1 = poly1; 

    // Stores head node of polynomial1 
    struct Node *start2 = poly2; 

    // Update poly1 
    poly1 = poly1->next; 

    // Update poly2 
    poly2 = poly2->next; 

    // Traverse both circular linked list 
    while ((poly1 != start1 && 
                     poly2 != start2)) { 

        // Stores new node                  
        struct Node* r; 

        // Stores temp node 
        struct Node* z  
                 = *temp; 

        // Dynamically create a new node          
        r = (struct Node*)malloc( 
                    sizeof(struct Node)); 

        // Update coefficient of r             
        r->coeff = 0; 

        // If power of x of poly1 is 
        // greater than power of x of poly2 
        if (poly1->powx > poly2->powx) { 

            // Update coefficient of r 
            r->coeff = poly1->coeff; 

            // Update of power of x in r 
            r->powx = poly1->powx; 

            // Update of power of y in r 
            r->powy = poly1->powy; 

            // Update poly1 
            poly1 = poly1->next; 
        } 

        // If power of x of 1st polynomial is 
        // less than power of x of 2nd poly 
        else if (poly1->powx < poly2->powx) { 

            // Update coefficient OF r 
            r->coeff = poly2->coeff; 

            // Update power of x in r 
            r->powx = poly2->powx; 

            // Update power of y in r 
            r->powy = poly2->powy; 

            // Update ploy2 
            poly2 = poly2->next; 
        } 

        // If power of x of 1st polynomial is 
        //  equal to power of x of 2nd poly 
        else { 

            // Power of y of 1st polynomial is 
            // greater than power of y of poly2 
            if (poly1->powy > poly2->powy) { 

                // Update coefficient of r 
                r->coeff = poly1->coeff; 

                // Update power of x in r 
                r->powx = poly1->powx; 

                // Update power of y in r 
                r->powy = poly1->powy; 

                // Update poly1 
                poly1 = poly1->next; 
            } 

            // If power of y of poly1 is  
            // less than power of y of ploy2 
            else if (poly1->powy <  
                            poly2->powy) { 

                // Update coefficient of r 
                r->coeff = poly2->coeff; 

                // Update power of x in r 
                r->powx = poly2->powx; 

                // Update power of y in r 
                r->powy = poly2->powy; 

                // Update poly2 
                poly2 = poly2->next; 
            } 

            // If power of y of 1st poly is 
            // equal to power of y of ploy2 
            else { 

                // Update coefficient of r 
                r->coeff = poly2->coeff  
                         + poly1->coeff; 

                // Update power of x in r          
                r->powx = poly1->powx; 

                // Update power of y in r  
                r->powy = poly1->powy; 

                // Update poly1 
                poly1 = poly1->next; 

                // Update poly2 
                poly2 = poly2->next; 
            } 
        } 

        // If z is null 
        if (z == NULL) { 

            // Update temp 
            (*temp) = r; 

            // Update next pointer 
            // of temp 
            (*temp)->next = (*temp); 
        } 
        else { 

            // Update next pointer 
            // of r 
            r->next = z->next; 

            // Update next pointer  
            // of z 
            z->next = r; 

            // Update temp 
            (*temp) = r; 
        } 
    } 

    // If there are nodes left to be   
    // traversed in poly1 or poly2 then 
    // append them in resultant polynomial . 
    while (poly1 != start1 || 
                    poly2 != start2) { 

        // If poly1 is not empty                 
        if (poly1 != start1) { 

            // Stores new node 
            struct Node *r; 

            // Stores temp node 
            struct Node *z = *temp; 

            // Create new node 
            r = (struct Node*)malloc( 
                        sizeof(struct Node)); 

            // Update coefficient or r 
            r->coeff = poly1->coeff; 

            // Update power of x in r 
            r->powx = poly1->powx; 

            // Update power of y in r 
            r->powy = poly1->powy; 

            // Update poly1 
            poly1 = poly1->next; 

            // If z is null 
            if (z == NULL) { 

                // Update temp 
                (*temp) = r; 

                // Update pointer  
                // to next node 
                (*temp)->next = (*temp); 
            } 
            else { 

                // Update next pointer 
                // of r 
                r->next = z->next; 

                // Update next pointer of z 
                z->next = r; 

                // Update temp 
                (*temp) = r; 
            } 
        } 

        // If poly2 is not empty 
        if (poly2 != start2) { 

            // Stores new node 
            struct Node *r; 

            // Stores temp node 
            struct Node *z = *temp; 

            // Create new node 
            r = (struct Node*)malloc( 
                     sizeof(struct Node)); 

            // Update coefficient of z          
            z->coeff = poly2->coeff; 

            // Update power of x in z 
            z->powx = poly2->powx; 

            // Update power of y in z 
            z->powy = poly2->powy; 

            // Update poly2 
            poly2 = poly2->next; 

            // If z is null 
            if (z == NULL) { 

                // Update temp 
                (*temp) = r; 

                // Update next pointer 
                // of temp 
                (*temp)->next = (*temp); 
            } 
            else { 

                // Update next pointer 
                // of r 
                r->next = z->next; 

                // Update next pointer  
                // of z 
                z->next = r; 

                // Update temp 
                (*temp) = r; 
            } 
        } 
    } 

    // Stores new node 
    struct Node *r; 

    // Stores temp node 
    struct Node *z = *temp; 

    // Create new node 
    r = (struct Node*)malloc( 
         sizeof(struct Node)); 

    // Update coefficient of r      
    r->coeff = 0; 

    // If power of x of start1 greater than 
    // power of x of start2 
    if (start1->powx > start2->powx) { 

        // Update coefficient of r 
        r->coeff = start1->coeff; 

        // Update power of x in r 
        r->powx = start1->powx; 

        // Update power of y in r 
        r->powy = start1->powy; 
    } 

    // If power of x of start1 less than 
    // power of x of start2 
    else if (start1->powx < start2->powx) { 

        // Update coefficient of r 
        r->coeff = start2->coeff; 

        // Update power of x in r 
        r->powx = start2->powx; 

        // Update power of y in r 
        r->powy = start2->powy; 
    } 

    // If power of x of start1 equal to 
    // power of x of start2 
    else { 

        // If power of y of start1 greater than 
        // power of y of start2 
        if (start1->powy > start2->powy) { 

            // Update coefficient of r 
            r->coeff = start1->coeff; 

            // Update power of x in r 
            r->powx = start1->powx; 

            // Update power of y in r 
            r->powy = start1->powy; 
        } 

        // If power of y of start1 less than 
        // power of y of start2 
        else if (start1->powy <  
                           start2->powy) { 

            // Update coefficient of r 
            r->coeff = start2->coeff; 

            // Update power of x in r 
            r->powx = start2->powx; 

            // Update power of y in r 
            r->powy = poly2->powy; 
        } 

        // If power of y of start1 equal to 
        // power of y of start2 
        else { 

            // Update coefficient of r 
            r->coeff = start2->coeff  
                        + start1->coeff; 

            // Update power of x in r 
            r->powx = start1->powx; 

            // Update power of y in r 
            r->powy = start1->powy; 
        } 
    } 

    // If z is null 
    if (z == NULL) { 

        // Update temp 
        (*temp) = r; 

        // Update next pointer  
        // of temp 
        (*temp)->next = (*temp); 
    } 
    else { 

        // Update next pointer of r 
        r->next = z->next; 

        // Update next pointer of z 
        z->next = r; 

        // Update temp 
        (*temp) = r; 
    } 
} 

// Display the circular linked list 
void display(struct Node* node) 
{ 

    // Stores head node of list 
    struct Node* start = node; 

    // Update node 
    node = node->next; 

    // Traverse the list 
    while (node != start && 
            node->coeff != 0) { 

        // Print coefficient of 
        // current node         
        cout << node->coeff; 

        // If power of variable x 
        // is not zero 
        if (node->powx != 0) 
            cout << "x^" << node->powx; 

        // If power of variable x 
        // and y is not zero      
        if(node->powx != 0 && 
                 node->powy != 0)  
            cout<<" * ";   

        // If power of variable y 
        // is not zero     
        if (node->powy != 0) 
            cout << "y^" << node->powy; 

        // Add next term of  
        // the polynomial     
        if (node != start && 
          node->next->coeff != 0) { 
            cout << " + "; 
        } 

        // Update node 
        node = node->next; 
    } 

    // Print coefficient of 
    // current node  
    cout << node->coeff; 

    // If power of variable x 
    // is not zero 
    if (node->powx != 0) 
        cout << "x^" << node->powx; 

    // If power of variable y 
    // is not zero     
    if (node->powy != 0) 
        cout << "y^" << node->powy; 
    cout << "\n\n"; 
} 

// Driver Code 
int main() 
{ 

    // Stores node of  
    // first polynomial 
    struct Node *poly1 = NULL; 

    // Stores node of  
    // second polynomial 
    struct Node *poly2 = NULL; 

    // Stores node of resultant  
    // polynomial 
    struct Node *store = NULL; 

    // Create first polynomial 
    create_node(5, 2, 1, &poly1); 
    create_node(4, 1, 2, &poly1); 
    create_node(3, 1, 1, &poly1); 
    create_node(2, 1, 0, &poly1); 
    create_node(3, 0, 1, &poly1); 
    create_node(2, 0, 0, &poly1); 

    // Create second polynomial 
    create_node(3, 1, 2, &poly2); 
    create_node(4, 1, 0, &poly2); 
    create_node(2, 0, 1, &poly2); 
    create_node(6, 0, 0, &poly2); 

    // Function call to add 
    // two polynomial 
    add_poly(poly1, poly2, &store); 

    // Display polynomial 1 
    cout << "Polynomial 1"
         << "\n"; 
    display(poly1); 

    // Display polynomial 2 
    cout << "Polynomail 2"
         << "\n"; 
    display(poly2); 

    // Display final addition of 2-variable polynomial 
    cout << "Polynomial after addition"
         << "\n"; 
    display(store); 

    return 0; 
} 

```

**Output:**

```
Polynomial 1
5x^2 * y^1 + 4x^1 * y^2 + 3x^1 * y^1 + 2x^1 + 3y^1 + 2

Polynomail 2
3x^1 * y^2 + 4x^1 + 2y^1 + 6

Polynomial after addition
5x^2 * y^1 + 7x^1 * y^2 + 3x^1 * y^1 + 6x^1 + 5y^1 + 8

```

**时间复杂度**：`O(M + N)`，其中`M`和`N`分别是第一列表和第二列表中的节点数。

**辅助空间**：`O(M + N)`



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。