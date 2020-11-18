# 从 3D 矩阵

构造链接列表

给定大小为 **X * Y * Z** 的 3D 矩阵 **mat [] [] []** 。 任务是将该矩阵转换为完全连接的循环链表。 每个节点将具有 6 个指针，即：**左，右，上，下，前，后。**

**范例：** [

> **输入：** X = 2，Y = 2，Z = 2
> 垫[0] [0] [0] = 10 垫[0] [0] [1] = 11
> 垫 [0] [1] [0] = 12 垫[0] [1] [1] = 13
> 垫[1] [0] [0] = 14 垫[1] [0] [1] = 15
> 垫[1] [1] [0] = 16 垫[1] [1] [1] = 17
> 
> ![](img/578e567552c3d485c811575835a42ce6.png)
> 
> **输出：**
> 元素前背面左右上下
> 10 14 14 11 11 12 12
> 11 15 15 10 10 13 13
> 12 16 16 13 13 10 10
> 13 17 17 12 12 11 11
> 14 10 10 15 15 16 16
> 15 11 11 14 14 17 17
> 16 12 12 17 17 14 14
> 17 13 13 16 16 15 15
> **解释：**
> 对于值为[10]的 mat [0] [0] [0]：
> 其后指针指向值为 14 的单元格 mat [1] [0] [0]。
> 它前面没有任何元素。 为了保持循环顺序，前指针指向值为 12 的单元格 mat [1] [0] [0]。
> 其右指针指向值为 11 的单元格 mat [0] [0] [1] 。
> 它的左侧没有任何元素。 为了维持循环顺序，左指针指向值为 11 的单元格 mat [0] [0] [1]。
> 其底部指针指向值为 12 的单元格 mat [0] [1] [0] 。
> 它上面没有任何元素。 为了保持循环顺序，顶部指针指向值为 12 的单元格 mat [0] [1] [0]。
> 这样，每个单元格的所有指针都连接到它们各自的单元格。
> 
> **输入：** X = 1，Y = 3，Z = 2
> mat [0] [0] [0] = 1 mat [0] [0] [1] = 2 mat [0] [0] [0] = 3
> mat [0] [1] [0] = 4 mat [0] [1] [1] = 5 Mat [0] [0] [0] = 6
> **输出：**
> 元素前背面左右上下
> 1 4 4 3 2 1 1
> 2 5 5 1 3 2 2
> 3 6 6 2 1 3 3
> 4 1 1 6 5 4 4
> 5 2 2 4 6 5 5
> 6 3 3 5 4 6 6

**方法：**

*   对于矩阵的每个单元，创建一个由 6 个指针组成的节点，例如**上，下，左，右，后和前**。

*   将所有节点的**指针向下链接**。 对于给定的单元格，如果在其下方不存在任何单元格，则将其向下指针指向该行的最顶部单元格以保持循环顺序。

*   在所有节点的指针上链接**。 对于给定的单元格，如果在其上方不存在任何单元格，则将其向上指针指向该行的最底部单元格以保持循环顺序。**

*   链接所有节点的**右**指针。 对于给定的单元格，如果右侧不存在任何单元格，则将其右指针指向行的最左侧单元格以保持循环顺序。

*   链接所有节点的**左**指针。 对于给定的单元格，如果左侧不存在任何单元格，则将其左指针指向该行的最右侧单元格以保持循环顺序。

*   链接所有节点的**前**指针。 对于给定的单元格，如果在其前面不存在任何单元格，则将其前指针指向该行的最后一个单元格以保持循环顺序。

*   链接所有节点的**返回**指针。 对于给定的单元格，如果后面没有单元格，则将其向后指针指向该行的最前面的单元格以保持循环顺序。

*   因此，以循环方式链接所有指针。 遍历如此形成的整个链表，并针对链表的每个节点，使用其 6 个指针打印其指向的所有值。

下面是上述方法的实现：

## CPP

```

// C++ code for the above program 

#include <bits/stdc++.h> 
using namespace std; 

// Node structure of the 
// 3D-linked list 
class ThreeDLinkedListNode { 
public: 
    int val; 
    ThreeDLinkedListNode* front; 
    ThreeDLinkedListNode* back; 
    ThreeDLinkedListNode* up; 
    ThreeDLinkedListNode* right; 
    ThreeDLinkedListNode* down; 
    ThreeDLinkedListNode* left; 

    ThreeDLinkedListNode( 
        int x, 
        ThreeDLinkedListNode* f = NULL, 
        ThreeDLinkedListNode* b = NULL, 
        ThreeDLinkedListNode* u = NULL, 
        ThreeDLinkedListNode* r = NULL, 
        ThreeDLinkedListNode* d = NULL, 
        ThreeDLinkedListNode* l = NULL) 
    { 
        // initialization of 3D 
        // linkedlist Node 
        val = x; 
        front = f; 
        back = b; 
        up = u; 
        right = r; 
        down = d; 
        left = l; 
    } 

    vector<int> extractNeighbors() 
    { 
        // extracting all front, 
        // back, up, down, left, 
        // right neighbours of 
        // the node 
        vector<int> neighbour; 

        // front back left right up down 
        neighbour.push_back(front->val); 
        neighbour.push_back(back->val); 
        neighbour.push_back(left->val); 
        neighbour.push_back(right->val); 
        neighbour.push_back(up->val); 
        neighbour.push_back(down->val); 
        return neighbour; 
    } 
}; 

class Solution { 
public: 
    void setDown( 
        vector<vector<vector<int> > > a, 
        int layer, int row, int column, 
        ThreeDLinkedListNode* node) 
    { 
        // setting the down pointers 
        // of all nodes in a 
        // 3D linked list 
        bool flag = false; 
        ThreeDLinkedListNode* head = node; 

        // loop to traverse the layers 
        for (int i = 0; 
             i < layer; i++) { 

            ThreeDLinkedListNode* 
                start_layer_head 
                = node; 

            // Loop to traverse the 
            // columns of each layer 
            for (int j = 0; 
                 j < column; j++) { 

                ThreeDLinkedListNode* 
                    start 
                    = node; 

                // Loop to traverse 
                // each row 
                for (int k = 0; 
                     k < row; k++) { 

                    // Check if its the 
                    // last cell of the 
                    // current row 
                    if (k == row - 1) 
                        node->down = start; 
                    else
                        node->down 
                            = new ThreeDLinkedListNode( 
                                a[i][k + 1][j]); 

                    node = node->down; 
                } 

                // Check if it is the last 
                // element of the current 
                // column 
                if (j == column - 1) { 

                    node->right = start_layer_head; 

                    // Check if it it is the 
                    // last element of the 
                    // current layer 
                    if (i < layer - 1) { 

                        start_layer_head->back 
                            = new ThreeDLinkedListNode( 
                                a[i + 1][0][0]); 

                        node = start_layer_head->back; 
                    } 
                    else { 

                        start_layer_head->back = head; 
                        node = start_layer_head->back; 
                    } 
                } 
                else { 

                    node->right 
                        = new ThreeDLinkedListNode( 
                            a[i][0][j + 1]); 
                    node = node->right; 
                } 
            } 
        } 
    } 

    void setUp( 
        vector<vector<vector<int> > > a, 
        int layer, int row, int column, 
        ThreeDLinkedListNode* node) 
    { 

        // setting the up pointers of all 
        // nodes in a 3d linked list 
        ThreeDLinkedListNode* head = node; 

        // loop to traverse the layers 
        for (int i = 0; 
             i < layer; i++) { 

            ThreeDLinkedListNode* 
                start_layer_head 
                = node; 

            // Loop to traverse the 
            // columns 
            for (int j = 0; 
                 j < column; j++) { 

                ThreeDLinkedListNode* 
                    start 
                    = node; 

                // Loop to traverse 
                // the rows 
                for (int k = 0; 
                     k < row; k++) { 

                    node->down->up = node; 
                    node = node->down; 
                } 

                // Check if it is the 
                // last element of 
                // the column 
                if (j == column - 1) { 

                    node 
                        = start_layer_head->back; 
                } 
                else { 
                    node = node->right; 
                } 
            } 
        } 
    } 

    void setRight( 
        vector<vector<vector<int> > > a, 
        int layer, int row, int column, 
        ThreeDLinkedListNode* node) 
    { 
        // setting the Right pointers of 
        // all nodes in a 3d linked list 
        ThreeDLinkedListNode* head = node; 

        // loop to traverse the layers 
        for (int i = 0; 
             i < layer; i++) { 

            ThreeDLinkedListNode* 
                start_layer_head 
                = node; 

            // loop to traverse the 
            // columns 
            for (int j = 0; 
                 j < column; j++) { 

                ThreeDLinkedListNode* 
                    start 
                    = node; 

                // loop to traverse 
                // the rows 
                for (int k = 0; 
                     k < row; k++) { 

                    node->down->right 
                        = node->right->down; 
                    node = node->down; 
                } 

                // Check if it is the 
                // last element of the 
                // column 
                if (j == column - 1) { 
                    node 
                        = start_layer_head->back; 
                } 
                else { 
                    node = node->right; 
                } 
            } 
        } 
    } 

    void setLeft( 
        vector<vector<vector<int> > > a, 
        int layer, int row, int column, 
        ThreeDLinkedListNode* node) 
    { 

        // setting the Left pointers of 
        // all nodes in a 3d linked list 
        ThreeDLinkedListNode* head = node; 

        // loop to traverse the layers 
        for (int i = 0; 
             i < layer; i++) { 

            ThreeDLinkedListNode* 
                start_layer_head 
                = node; 

            // loop to traverse the 
            // columns 
            for (int j = 0; 
                 j < column; j++) { 

                ThreeDLinkedListNode* 
                    start 
                    = node; 

                // loop to traverse 
                // the rows` 
                for (int k = 0; 
                     k < row; k++) { 

                    node->right->left = node; 
                    node = node->down; 
                } 

                // Check if it is the 
                // last element of the 
                // column 
                if (j == column - 1) { 
                    node 
                        = start_layer_head->back; 
                } 
                else { 
                    node = node->right; 
                } 
            } 
        } 
    } 

    void setBack( 
        vector<vector<vector<int> > > a, 
        int layer, int row, int column, 
        ThreeDLinkedListNode* node) 
    { 

        // setting the Back pointers of 
        // all nodes in a 3d linked list 
        ThreeDLinkedListNode* head = node; 

        // loop to traverse the layers 
        for (int i = 0; 
             i < layer; i++) { 

            ThreeDLinkedListNode* 
                start_layer_head 
                = node; 

            // loop to traverse the 
            // columns 
            for (int j = 0; 
                 j < column; j++) { 

                ThreeDLinkedListNode* 
                    start 
                    = node; 

                // loop to traverse 
                // the rows 
                for (int k = 0; 
                     k < row; k++) { 

                    node->down->back 
                        = node->back->down; 
                    node = node->down; 
                } 

                // Check if it is the 
                // last element of the 
                // column 
                if (j == column - 1) { 
                    node = start_layer_head->back; 
                } 
                else { 
                    node = node->right; 
                    node->back = start->back->right; 
                } 
            } 
        } 
    } 

    void setFront( 
        vector<vector<vector<int> > > a, 
        int layer, int row, int column, 
        ThreeDLinkedListNode* node) 
    { 

        // setting the Front pointers of 
        // all nodes in a 3d linked list 
        ThreeDLinkedListNode* head = node; 

        // loop to traverse the layers 
        for (int i = 0; 
             i < layer; i++) { 

            ThreeDLinkedListNode* 
                start_layer_head 
                = node; 

            // loop to traverse the 
            // columns 
            for (int j = 0; 
                 j < column; j++) { 

                ThreeDLinkedListNode* 
                    start 
                    = node; 

                // loop to traverse 
                // the rows 
                for (int k = 0; 
                     k < row; k++) { 

                    node->back->front = node; 
                    node = node->down; 
                } 

                // Check if it is the 
                // last element of the 
                // column 
                if (j == column - 1) { 
                    node = start_layer_head->back; 
                } 
                else { 
                    node = node->right; 
                    node->back = start->back->right; 
                } 
            } 
        } 
    } 

    ThreeDLinkedListNode* 
    ThreeDimensionalMatrixToLinkedList( 
        vector<vector<vector<int> > > a, 
        int layer, int row, int column) 
    { 
        ThreeDLinkedListNode* head 
            = new ThreeDLinkedListNode( 
                a[0][0][0]); 

        ThreeDLinkedListNode* temp = head; 

        // setting down pointers 
        // of all the nodes 
        setDown(a, layer, 
                row, column, temp); 

        // setting up pointers 
        // of all the nodes 
        setUp(a, layer, 
              row, column, temp); 

        // setting right pointers 
        // of all the nodes 
        setRight(a, layer, 
                 row, column, temp); 

        // setting left pointers 
        // of all the nodes 
        setLeft(a, layer, 
                row, column, temp); 

        // setting back pointers 
        // of all the nodes 
        setBack(a, layer, 
                row, column, temp); 

        // setting front pointers 
        // of all the nodes 
        setFront(a, layer, 
                 row, column, temp); 

        return head; 
    } 
}; 

void print_2d_matrix( 
    vector<vector<vector<int> > > mat, 
    ThreeDLinkedListNode* head, 
    int rows, int cols, int layer) 
{ 

    ThreeDLinkedListNode* rest; 

    // loop to traverse 
    // the rows 
    for (int i = 0; 
         i < rows; ++i) { 

        rest = head->down; 

        // loop to traverse 
        // the columns 
        for (int j = 0; 
             j < cols; ++j) { 

            cout << mat[layer][i][j] 
                 << "\t"; 
            vector<int> neighbors 
                = head->extractNeighbors(); 
            for (auto ne : neighbors) 
                cout << ne << "\t"; 

            cout << "\n"; 
            head = head->right; 
        } 
        head = rest; 
    } 
} 

void printOutput( 
    vector<vector<vector<int> > > mat, 
    ThreeDLinkedListNode* head, 
    int layer, int row, int column) 
{ 

    ThreeDLinkedListNode* rest; 

    // loop to traverse the layers 
    for (int i = 0; 
         i < layer; i++) { 

        rest = head->back; 
        print_2d_matrix(mat, head, 
                        row, column, i); 
        head = rest; 
    } 
} 

// Driver Code 
int main() 
{ 
    // Initialise the count 
    // of layers, columns and 
    // rows 
    int layer = 3; 
    int row = 3; 
    int column = 3; 

    vector<vector<vector<int> > > 
    mat(layer, 
        vector<vector<int> >( 
            row, vector<int>(column))); 

    mat = { { { 1, 2, 3 }, 
              { 4, 5, 6 }, 
              { 7, 8, 9 } }, 
            { { 10, 11, 12 }, 
              { 13, 14, 15 }, 
              { 16, 17, 18 } }, 
            { { 19, 20, 21 }, 
              { 22, 23, 24 }, 
              { 25, 26, 27 } } }; 

    // Function Call to form 
    // the linked list for the 
    // given 3D matrix 
    ThreeDLinkedListNode* 
        head 
        = Solution() 
              .ThreeDimensionalMatrixToLinkedList( 
                  mat, layer, row, column); 

    cout << "element\t"
         << "front\tback\t"
         << "left\tright\t"
         << "up\tdown\n"; 

    // Function to print the 
    // linked list elements 
    // and thevalues pointed 
    // by corresponding pointers 
    printOutput(mat, head, 
                layer, row, column); 
    return 0; 
} 

```

**Output:**

```
element    front    back    left    right    up    down
1    19    10    3    2    7    4    
2    20    11    1    3    8    5    
3    21    12    2    1    9    6    
4    22    13    6    5    1    7    
5    23    14    4    6    2    8    
6    24    15    5    4    3    9    
7    25    16    9    8    4    1    
8    26    17    7    9    5    2    
9    27    18    8    7    6    3    
10    1    19    12    11    16    13    
11    2    20    10    12    17    14    
12    3    21    11    10    18    15    
13    4    22    15    14    10    16    
14    5    23    13    15    11    17    
15    6    24    14    13    12    18    
16    7    25    18    17    13    10    
17    8    26    16    18    14    11    
18    9    27    17    16    15    12    
19    10    1    21    20    25    22    
20    11    2    19    21    26    23    
21    12    3    20    19    27    24    
22    13    4    24    23    19    25    
23    14    5    22    24    20    26    
24    15    6    23    22    21    27    
25    16    7    27    26    22    19    
26    17    8    25    27    23    20    
27    18    9    26    25    24    21

```

***时间复杂度：** O（X * Y * Z），其中 X，Y，Z 是 3D 矩阵的尺寸。*

***辅助空间：** O（X * Y * Z），其中 X，Y，Z 是 3D 矩阵的尺寸。*



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。