# 使用映射

> 原文：[https://www.geeksforgeeks.org/adding-two-polynomials-using-linked-list-using-map/](https://www.geeksforgeeks.org/adding-two-polynomials-using-linked-list-using-map/)

使用链接列表添加两个多项式

给定两个由链表表示的多项式。 编写函数以执行其代数和。

**示例**：

> **输入**：
>
> 第一个数字：`5x ^ 2 + 4x ^ 1 + 2x ^ 0`
>
> 第二个数字：`5x ^ 1 + 5x ^ 0`
>
> **输出**：`5x ^ 2 + 9x ^ 1 + 7x ^ 0`

**方法**：该实现使用[映射](http://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)数据结构，以便将具有相同幂值的所有系数加在一起并保存在映射内的键值对中。

下面是上述方法的实现：

```

// C++ program for addition of two polynomials 
// represented as linked lists 
#include <bits/stdc++.h> 
using namespace std; 

// Structure of Node used 
struct Node { 

    // Coefficient of the polynomial 
    int coeff; 

    // Power of the polynomial 
    int pow; 
    Node* next; 
}; 

// Function to create new node 
void create_node(int x, int y, 
                 struct Node** temp) 
{ 
    struct Node *r, *z; 
    z = *temp; 
    if (z == NULL) { 
        r = (struct Node*) 
            malloc(sizeof(struct Node)); 
        r->coeff = x; 
        r->pow = y; 
        *temp = r; 
        r->next = (struct Node*) 
            malloc(sizeof(struct Node)); 
        r = r->next; 
        r->next = NULL; 
    } 
    else { 
        r->coeff = x; 
        r->pow = y; 
        r->next = (struct Node*) 
            malloc(sizeof(struct Node)); 
        r = r->next; 
        r->next = NULL; 
    } 
} 

// Display Linked list 
void show(struct Node* node) 
{ 
    if (node == NULL) 
        return; 
    while (node->next != NULL) { 
        printf("%dx^%d", node->coeff, node->pow); 
        node = node->next; 
        if (node->next != NULL) 
            printf(" + "); 
    } 
} 

/* Function to print the required sum of a  
polynomial p1 and p2 as specified in output */
void addPolynomial(Node* p1, Node* p2) 
{ 
    map<int, int> mp; 
    Node* temp1 = p1; 
    Node* temp2 = p2; 
    while (temp1 != NULL) { 

        // Add coefficients of same power value 
        // map contains (powervalue, coeff) pair 
        mp[temp1->pow] += temp1->coeff; 
        temp1 = temp1->next; 
    } 
    while (temp2 != NULL) { 
        mp[temp2->pow] += temp2->coeff; 
        temp2 = temp2->next; 
    } 

    // Started from the end because higher power should 
    // come first and there should be "+" symbol in between 
    // so iterate up to second element and print last out of 
    // the loop. 

    for (auto it = (mp.rbegin()); it != prev(mp.rend()); ++it) 
        cout << it->second << "x^" << it->first << " + "; 
    cout << mp.begin()->second << "x^" << mp.begin()->first; 
} 

// Driver function 
int main() 
{ 
    struct Node *poly1 = NULL, *poly2 = NULL, *poly = NULL; 

    // Create first list of 5x^2 + 4x^1 + 2x^0 
    create_node(5, 2, &poly1); 
    create_node(4, 1, &poly1); 
    create_node(2, 0, &poly1); 

    // Create second list of 5x^1 + 5x^0 
    create_node(5, 1, &poly2); 
    create_node(5, 0, &poly2); 

    printf("1st Number: "); 
    show(poly1); 

    printf("\n2nd Number: "); 
    show(poly2); 

    poly = (struct Node*)malloc(sizeof(struct Node)); 

    printf("\nAdded polynomial: "); 

    // Function add two polynomial numbers 
    addPolynomial(poly1, poly2); 

    return 0; 
} 

```

**Output:**

```
1st Number: 5x^2 + 4x^1 + 2x^0
2nd Number: 5x^1 + 5x^0
Added polynomial: 5x^2 + 9x^1 + 7x^0

```

**时间复杂度**：`O((m + n)log(m + n))`，其中`m`和`n`分别是第一和第二个列表中的节点数，我们正在使用映射将系数额外`log(m + n)`因子被添加。



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。