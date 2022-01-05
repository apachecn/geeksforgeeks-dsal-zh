# 使用链表从给定的稀疏矩阵生成矩阵，并重建稀疏矩阵

> 原文:[https://www . geeksforgeeks . org/从给定稀疏矩阵生成矩阵-使用链表并重建稀疏矩阵/](https://www.geeksforgeeks.org/generate-matrix-from-given-sparse-matrix-using-linked-list-and-reconstruct-the-sparse-matrix/)

给定维度为 **N*M** 的[稀疏矩阵](https://www.geeksforgeeks.org/sparse-matrix-representation/) **mat[][]** ，任务是使用[链表](https://www.geeksforgeeks.org/data-structures/linked-list/)构建和表示原始矩阵，并重构给定的[稀疏矩阵](https://www.geeksforgeeks.org/sparse-matrix-representation/)。

**示例:**

> **输入:** mat[][] = {{0，1，0，0，0，0}，{0，1，0，0，0，0}，{0，0，2，0，0，4}，{0，3，0，0，5，0，0，0 } }
> T3】输出:T5】链表表示法:(4，2，5) → (3，4，4) → (3，1，3) → (2，2，2) → (1，1，1)
> 
> **输入:** mat[][] = {{0，0，0，4，0}，{0，1，0，0，0}}
> **输出:**
> 链表表示法:(1，1，1) → (0，3，4) → NULL
> 原始矩阵:
> {{0，0，0，4，0}，
> {0，1，0，0，0}}

**方法:**给定的问题可以通过存储**行索引**、**列索引**、其**值**以及链表节点中所有非零元素的下一个指针来解决。按照以下步骤解决问题:

*   对于使用链表构造稀疏矩阵的[，T2 遍历矩阵](https://www.geeksforgeeks.org/sparse-table/)，对于每个非零元素创建一个新节点，[将这个新创建的节点插入到列表](https://www.geeksforgeeks.org/linked-list-set-2-inserting-a-node/)的开头。
*   重建时，创建一个辅助的 2D 维数数组 **N*M** ，所有条目为 **0** ，然后[遍历链表](https://www.geeksforgeeks.org/linked-list-set-1-introduction/)并更新这个新创建数组中的所有非零元素。

下面是上述方法的实现:

## C

```
// C program for the above approach

#include <stdio.h>
#include <stdlib.h>

// Store the size of sparse matrix
#define R 5
#define C 5

// Linked list node
typedef struct SNode {
    int data;
    int Col;
    int Row;
    struct SNode* next;
} SparseNode;

// Store the head pointer of the linked
// list and the size of the matrix
typedef struct MNode {
    int Matrix[2];
    SparseNode* SNPTR;
} MatrixNode;

// Function to initialize the head of
// the linked list
MatrixNode* ConstructMNhead(
    MatrixNode* MNhead, SparseNode* SNhead)
{

    MNhead = (MatrixNode*)malloc(sizeof(MNhead));

    // Update the number of rows and
    // columns and update head pointer
    MNhead->Matrix[0] = R;
    MNhead->Matrix[1] = C;
    MNhead->SNPTR = SNhead;

    return MNhead;
}

// Function to create a new node
SparseNode* CreateList(int Row, int Col,
                       int data)
{

    // Create a new node
    SparseNode* New
        = (SparseNode*)malloc(sizeof(SparseNode));

    // Update the value and the row
    // and column index and set the
    // next pointer to NULL
    New->data = data;
    New->Col = Col;
    New->Row = Row;
    New->next = NULL;

    return New;
}

// Function to insert a node at the
// beginning of the  linked list
MatrixNode* AddInList(
    MatrixNode* MNhead, int Row,
    int Col, int data)
{
    MatrixNode* Mptr = MNhead;

    // Create a new node
    SparseNode* New = CreateList(
        Row, Col, data);

    // If the head is NULL, point it
    // to the newly created node
    if (Mptr->SNPTR == NULL) {
        Mptr->SNPTR = New;
        return MNhead;
    }

    // Insert this node at beginning
    New->next = Mptr->SNPTR;

    // Update the head pointer
    Mptr->SNPTR = New;

    return MNhead;
}

// Function to construct the sparse
// matrix using linked list
MatrixNode* ConstructSparseMatrix(
    MatrixNode* MNhead, int Matrix[R][C],
    SparseNode* SNhead)
{
    int i, j;
    MatrixNode* Mptr = MNhead;

    // If the head pointer is NULL
    if (MNhead == NULL) {
        MNhead = ConstructMNhead(
            MNhead, SNhead);
    }

    Mptr = MNhead;

    // Traverse the matrix, row-wise
    for (i = 0;
         i < Mptr->Matrix[0]; i++) {
        for (j = 0;
             j < Mptr->Matrix[1]; j++) {

            // For all non-zero values,
            // push them in linked list
            if (Matrix[i][j])
                MNhead = AddInList(
                    MNhead, i, j,
                    Matrix[i][j]);
        }
    }

    return MNhead;
}

// Function to reconstruct the sparse
// matrix using linked list
void ReConstructArray(MatrixNode* MNhead)
{
    int i, j;
    SparseNode* Sptr = MNhead->SNPTR;

    // Create a 2D array
    int** OriginalMatrix

        = (int**)malloc(sizeof(int*)
                        * MNhead->Matrix[0]);

    for (i = 0;
         i < MNhead->Matrix[0]; i++) {
        OriginalMatrix[i]
            = (int*)malloc(sizeof(int)
                           * MNhead->Matrix[1]);
    }

    // Initialize all the elements
    // in the original matrix as 0
    for (i = 0;
         i < MNhead->Matrix[0]; i++) {

        for (j = 0;
             j < MNhead->Matrix[1]; j++) {
            OriginalMatrix[i][j] = 0;
        }
    }

    // Print the linked list
    printf("Linked list represe"
           "ntation:\n");

    // Iterate while sptr pointer is not NULL
    while (Sptr != NULL) {

        // Update the element in the
        // original matrix and print
        // the current node
        OriginalMatrix[Sptr->Row][Sptr->Col]
            = Sptr->data;

        printf("(%d, %d, %d)->",
               Sptr->Row, Sptr->Col,
               OriginalMatrix[Sptr->Row][Sptr->Col]);

        // Move to the next node
        Sptr = Sptr->next;
    }
    printf("NULL\n");

    // Print the reconstructed matrix
    printf("Original Matrix Re"
           "-Construction:\n");

    for (i = 0; i < R; i++) {
        for (j = 0; j < C; j++) {
            printf("%d, ", OriginalMatrix[i][j]);
        }
        printf("\n");
    }
}

// Create a head of the linked list
MatrixNode* MNhead = NULL;
SparseNode* SNhead = NULL;

// Driver Code
int main()
{
    int Matrix[R][C] = { { 0, 1, 0, 0, 0 },
                         { 0, 1, 0, 0, 0 },
                         { 0, 0, 2, 0, 0 },
                         { 0, 3, 0, 0, 4 },
                         { 0, 0, 5, 0, 0 } };
    int** OriginalMatrix;

    // Sparse matrix Construction
    MNhead = ConstructSparseMatrix(
        MNhead, Matrix, SNhead);

    // Sparse matrix Re-Construction
    ReConstructArray(MNhead);

    return 0;
}
```

**Output**

```
Linked list representation:
(4, 2, 5)->(3, 4, 4)->(3, 1, 3)->(2, 2, 2)->(1, 1, 1)->(0, 1, 1)->NULL
Original Matrix Re-Construction:
0, 1, 0, 0, 0, 
0, 1, 0, 0, 0, 
0, 0, 2, 0, 0, 
0, 3, 0, 0, 4, 
0, 0, 5, 0, 0, 

```

***时间复杂度:** O(N*M)*
***辅助空间:** O(N*M)*