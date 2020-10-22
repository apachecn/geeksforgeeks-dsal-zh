# 从给定的二叉树构造祖先矩阵

> 原文： [https://www.geeksforgeeks.org/construct-ancestor-matrix-from-a-given-binary-tree/](https://www.geeksforgeeks.org/construct-ancestor-matrix-from-a-given-binary-tree/)

给定一个二叉树，其中所有值都从 **0** 到`n-1`。 构造祖先矩阵`mat[n][n]`。 祖先矩阵定义如下。

```
mat[i][j] = 1 if i is ancestor of j
mat[i][j] = 0, otherwise

```

**示例**：

```
Input: Root of below Binary Tree.
          0
        /   \
       1     2
Output: 0 1 1
        0 0 0 
        0 0 0 

Input: Root of below Binary Tree.
           5
        /    \
       1      2
      /  \    /
     0    4  3
Output: 0 0 0 0 0 0 
        1 0 0 0 1 0 
        0 0 0 1 0 0 
        0 0 0 0 0 0 
        0 0 0 0 0 0 
        1 1 1 1 1 0

```

**我们强烈建议您最小化浏览器，然后自己尝试。**

**方法 1**：

这个想法是遍历这棵树。 遍历时，请跟踪数组中的祖先。 当我们访问一个节点时，将其添加到祖先数组中，并考虑邻接矩阵中的相应行。 我们将其行中的所有祖先标记为 1。一旦处理完一个节点及其所有子节点，便从祖先数组中删除该节点。

以下是上述想法的实现。

## C++ 

```cpp

// C++ program to construct ancestor matrix for 
// given tree. 
#include<bits/stdc++.h> 
using namespace std; 
#define MAX 100 

/* A binary tree node */
struct Node 
{ 
    int data; 
    Node *left, *right; 
}; 

// Creating a global boolean matrix for simplicity 
bool mat[MAX][MAX]; 

// anc[] stores all ancestors of current node.  This 
// function fills ancestors for all nodes. 
// It also returns size of tree.  Size of tree is 
// used to print ancestor matrix. 
int ancestorMatrixRec(Node *root, vector<int> &anc) 
{ 
    /* base case */
    if (root == NULL) return 0;; 

    // Update all ancestors of current node 
    int data = root->data; 
    for (int i=0; i<anc.size(); i++) 
       mat[anc[i]][data] = true; 

    // Push data to list of ancestors 
    anc.push_back(data); 

    // Traverse left and right subtrees 
    int l = ancestorMatrixRec(root->left, anc); 
    int r = ancestorMatrixRec(root->right, anc); 

    // Remove data from list the list of ancestors 
    // as all descendants of it are processed now. 
    anc.pop_back(); 

    return l+r+1; 
} 

// This function mainly calls ancestorMatrixRec() 
void ancestorMatrix(Node *root) 
{ 
    // Create an empty ancestor array 
    vector<int> anc; 

    // Fill ancestor matrix and find size of 
    // tree. 
    int n = ancestorMatrixRec(root, anc); 

    // Print the filled values 
    for (int i=0; i<n; i++) 
    { 
        for (int j=0; j<n; j++) 
            cout << mat[i][j] << " "; 
        cout << endl; 
    } 
} 

/* Helper function to create a new node */
Node* newnode(int data) 
{ 
    Node* node = new Node; 
    node->data = data; 
    node->left = node->right = NULL; 
    return (node); 
} 

/* Driver program to test above functions*/
int main() 
{ 
    /* Construct the following binary tree 
                5 
              /   \ 
            1      2 
          /  \    / 
         0    4  3    */
    Node *root        = newnode(5); 
    root->left        = newnode(1); 
    root->right       = newnode(2); 
    root->left->left  = newnode(0); 
    root->left->right = newnode(4); 
    root->right->left = newnode(3); 

    ancestorMatrix(root); 

    return 0; 
} 

```

## Java

```java
// Java Program to construct ancestor matrix for a given tree 
import java.util.*; 
  
class GFG 
{ 
    // ancestorMatrix function to populate the matrix of 
    public static void ancestorMatrix(Node root ,  
                                    int matrix[][],int size) 
    { 
          
        // base case: 
        if (root==null) 
        return ; 
          
        // call recursively for a preorder {left} 
        ancestorMatrix(root.left, matrix, size); 
          
        // call recursively for preorder {right} 
        ancestorMatrix(root.right, matrix, size); 
          
        // here we will reach the root node automatically 
        // try solving on pen and paper 
          
        if (root.left != null) 
        { 
            // make the current node as parent of its children node 
            matrix[root.data][root.left.data] = 1; 
              
            // iterate through all the columns of children node  
            // all nodes which are children to 
            // children of root node will also  
            // be children of root node 
            for (int i = 0; i < size; i++) 
            { 
                // if children of root node is a parent  
                // of someone (i.e 1) then make that node  
                // as children of root also 
                if (matrix[root.left.data][i] == 1) 
                matrix[root.data][i] = 1; 
            } 
        } 
          
        // same procedure followed for right node as well  
        if (root.right != null) 
        { 
            matrix[root.data][root.right.data] = 1; 
              
            for (int i = 0; i < size; i++) 
            { 
                if (matrix[root.right.data][i]==1) 
                matrix[root.data][i] = 1; 
            } 
        } 
              
          
    } 
      
    // Driver program to test the program 
    public static void main(String[] args)  
    { 
          
        // construct the binary tree as follows 
        Node tree_root = new Node(5); 
        tree_root.left = new Node (1); 
        tree_root.right = new Node(2); 
        tree_root.left.left = new Node(0); 
        tree_root.left.right = new Node(4); 
        tree_root.right.left = new Node(3); 
          
        // size of matrix  
        int size = 6; 
        int matrix [][] = new int[size][size]; 
          
        ancestorMatrix(tree_root, matrix, size); 
          
        for (int i = 0; i < size; i++) 
        { 
            for (int j = 0; j < size; j++) 
            { 
                System.out.print(matrix[i][j]+" "); 
            } 
            System.out.println(); 
        } 
    } 
      
    // node class for tree node 
    static class Node  
    { 
        public int data ; 
        public Node left ,right; 
        public Node (int data) 
        { 
            this.data = data; 
            this.left = this.right = null; 
        } 
    } 
} 
  
// This code is contributed by Sparsh Singhal
```

## Python3

```py
# Python3 program to construct ancestor  
# matrix for given tree. 
  
class newnode: 
    def __init__(self, data): 
        self.data = data 
        self.left = self.right = None
          
# anc[] stores all ancestors of current node.  
# This function fills ancestors for all nodes.  
# It also returns size of tree. Size of tree   
# is used to print ancestor matrix.  
def ancestorMatrixRec(root, anc): 
    global mat, MAX
      
    # base case  
    if root == None: 
        return 0
  
    # Update all ancestors of current node  
    data = root.data 
    for i in range(len(anc)): 
        mat[anc[i]][data] = 1
  
    # Push data to list of ancestors  
    anc.append(data)  
  
    # Traverse left and right subtrees  
    l = ancestorMatrixRec(root.left, anc)  
    r = ancestorMatrixRec(root.right, anc)  
  
    # Remove data from list the list of ancestors  
    # as all descendants of it are processed now.  
    anc.pop(-1)  
  
    return l + r + 1
  
# This function mainly calls ancestorMatrixRec()  
def ancestorMatrix(root): 
      
    # Create an empty ancestor array  
    anc = [] 
  
    # Fill ancestor matrix and find  
    # size of tree.  
    n = ancestorMatrixRec(root, anc)  
  
    # Print the filled values 
    for i in range(n): 
        for j in range(n): 
            print(mat[i][j], end = " ")  
        print() 
  
# Driver Code 
MAX = 100
mat = [[0] * MAX for i in range(MAX)] 
  
# Construct the following binary tree  
#         5  
#         / \  
#     1     2  
#     / \ /  
#     0 4 3  
root = newnode(5)  
root.left = newnode(1)  
root.right = newnode(2)  
root.left.left = newnode(0)  
root.left.right = newnode(4)  
root.right.left = newnode(3)  
  
ancestorMatrix(root) 
  
# This code is contributed by PranchalK
```

## C#

```cs
// C# Program to construct ancestor matrix for a given tree  
using System; 
  
class GFG  
{ 
    // ancestorMatrix function to populate the matrix of  
    public static void ancestorMatrix(Node root, 
                        int [,]matrix, int size)  
    { 
  
        // base case:  
        if (root == null)  
        { 
            return; 
        } 
  
        // call recursively for a preorder {left}  
        ancestorMatrix(root.left, matrix, size); 
  
        // call recursively for preorder {right}  
        ancestorMatrix(root.right, matrix, size); 
  
        // here we will reach the root node automatically  
        // try solving on pen and paper  
        if (root.left != null) 
        { 
            // make the current node as parent of its children node  
            matrix[root.data,root.left.data] = 1; 
  
            // iterate through all the columns of children node  
            // all nodes which are children to  
            // children of root node will also  
            // be children of root node  
            for (int i = 0; i < size; i++)  
            { 
                // if children of root node is a parent  
                // of someone (i.e 1) then make that node  
                // as children of root also  
                if (matrix[root.left.data,i] == 1)  
                { 
                    matrix[root.data,i] = 1; 
                } 
            } 
        } 
  
        // same procedure followed for right node as well  
        if (root.right != null) 
        { 
            matrix[root.data,root.right.data] = 1; 
  
            for (int i = 0; i < size; i++)  
            { 
                if (matrix[root.right.data,i] == 1)  
                { 
                    matrix[root.data,i] = 1; 
                } 
            } 
        } 
  
    } 
  
    // Driver code 
    public static void Main(String[] args) 
    { 
  
        // construct the binary tree as follows  
        Node tree_root = new Node(5); 
        tree_root.left = new Node(1); 
        tree_root.right = new Node(2); 
        tree_root.left.left = new Node(0); 
        tree_root.left.right = new Node(4); 
        tree_root.right.left = new Node(3); 
  
        // size of matrix  
        int size = 6; 
        int [,]matrix = new int[size,size]; 
  
        ancestorMatrix(tree_root, matrix, size); 
  
        for (int i = 0; i < size; i++)  
        { 
            for (int j = 0; j < size; j++)  
            { 
                Console.Write(matrix[i,j] + " "); 
            } 
            Console.WriteLine(); 
        } 
    } 
  
    // node class for tree node  
    public class Node 
    { 
  
        public int data; 
        public Node left, right; 
  
        public Node(int data)  
        { 
            this.data = data; 
            this.left = this.right = null; 
        } 
    } 
}  
  
// This code is contributed by 29AjayKumar
```

输出：

```
0 0 0 0 0 0 
1 0 0 0 1 0 
0 0 0 1 0 0 
0 0 0 0 0 0 
0 0 0 0 0 0 
1 1 1 1 1 0
```

上述解决方案的时间复杂度为`O(n ^ 2)`。

方法二：

此方法不使用任何辅助空间将值存储在向量中。 创建给定大小的二维矩阵（例如`M`）。 现在的想法是遍历`PreOrder`中的树。 遍历时，请跟踪最后一个祖先。

当我们访问一个节点时，如果该节点为`NULL`返回，则分配`M[lastAncestorValue][currentNodeValue] = 1`。

通过此操作，我们有了`Matrix(M)`来跟踪最低祖先，现在通过将传递闭包应用于此`Matrix(M)`，我们可以获得所需的结果。

以下是上述想法的实现。

## C++

```cpp
// C++ program to construct ancestor matrix for  
// given tree.  
#include<bits/stdc++.h>  
using namespace std;  
#define size 6  
  
int M[size][size]={0}; 
  
/* A binary tree node */
struct Node  
{  
    int data;  
    Node *left, *right;  
};  
  
/* Helper function to create a new node */
Node* newnode(int data)  
{  
    Node* node = new Node;  
    node->data = data;  
    node->left = node->right = NULL;  
    return (node);  
}  
  
void printMatrix(){ 
        for(int i=0;i<size;i++){ 
            for(int j=0;j<size;j++) 
                cout<<M[i][j]<<" "; 
            cout<<endl; 
        }         
  
} 
//First PreOrder Traversal  
void MatrixUtil(Node *root,int index){ 
          
    if(root==NULL)return; 
      
        int preData=root->data; 
              
        //Since there is no ancestor for root node, 
        // so we doesn't assign it's value as 1             
        if(index==-1)index=root->data; 
        else  M[index][preData]=1;     
      
    MatrixUtil(root->left,preData); 
    MatrixUtil(root->right,preData); 
} 
  
void Matrix(Node *root){ 
    // Call Func MatrixUtil 
    MatrixUtil(root,-1); 
      
      
    //Applying Transitive Closure for the given Matrix 
    for(int i=0;i<size;i++){ 
        for (int j = 0;j< size; j++) { 
            for(int k=0;k<size;k++) 
                M[j][k]=M[j][k]||(M[j][i]&&M[i][k]); 
              
        } 
          
    } 
      
    //Printing Matrix 
    printMatrix(); 
  
      
} 
/* Driver program to test above functions*/
int main()  
{  
    Node *root     = newnode(5);  
    root->left     = newnode(1);  
    root->right     = newnode(2);  
    root->left->left = newnode(0);  
    root->left->right = newnode(4);  
    root->right->left = newnode(3);  
  
    Matrix(root);  
      
  
    return 0;  
}
```

输出：

```
0 0 0 0 0 0 
1 0 0 0 1 0 
0 0 0 1 0 0 
0 0 0 0 0 0 
0 0 0 0 0 0 
1 1 1 1 1 0
```

怎么做 - 从祖先矩阵构造树？

[从祖先矩阵构造树](https://www.geeksforgeeks.org/construct-tree-from-ancestor-matrix/)。