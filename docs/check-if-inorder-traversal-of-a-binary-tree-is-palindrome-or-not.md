# 检查二叉树的中序遍历是否是回文

> 原文：[https://www.geeksforgeeks.org/check-if-inorder-traversal-of-a-binary-tree-is-palindrome-or-not/](https://www.geeksforgeeks.org/check-if-inorder-traversal-of-a-binary-tree-is-palindrome-or-not/)

给定[二叉树](https://www.geeksforgeeks.org/binary-tree-data-structure/)和任务，以检查其[中序序列](https://www.geeksforgeeks.org/tree-traversals-inorder-preorder-and-postorder/)是否是回文。

**示例**：

> **输入**：
>
> ![](img/38794aac18f0127ecf2abcd9bdda2a98.png)
>
> **输出**：`True`
>
> **说明**：
>
> 树的顺序为`"bbaaabb"`，这是回文字符串。
> 
> **输入**：
>
> ![](img/787020686d40d89902c5e489a8572ccb.png)
>
> **输出**：`False`
>
> **说明**：
>
> 树的顺序为`"bbdaabb"`，这不是回文字符串。

**方法**：

要解决此问题，请参考以下步骤：

*   [将给定的二叉树转换为双链表](https://www.geeksforgeeks.org/in-place-convert-a-given-binary-tree-to-doubly-linked-list/)。

*   这将问题归约到[检查字符的双链表是否是回文](https://www.geeksforgeeks.org/check-doubly-linked-list-characters-palindrome-not/)。

下面是上述方法的实现：

## C++

```cpp

// C++ Program to check if 
// the Inorder sequence of a 
// Binary Tree is a palindrome 

#include <bits/stdc++.h> 
using namespace std; 

// Define node of tree 
struct node { 
    char val; 
    node* left; 
    node* right; 
}; 

// Function to create the node 
node* newnode(char i) 
{ 
    node* temp = NULL; 
    temp = new node(); 
    temp->val = i; 
    temp->left = NULL; 
    temp->right = NULL; 
    return temp; 
} 

// Function to convert the tree 
// to the double linked list 
node* conv_tree(node* root, 
                node* shoot) 
{ 
    if (root->left != NULL) 
        shoot = conv_tree(root->left, 
                          shoot); 

    root->left = shoot; 

    if (shoot != NULL) 
        shoot->right = root; 

    shoot = root; 

    if (root->right != NULL) 
        shoot = conv_tree(root->right, 
                          shoot); 

    return shoot; 
} 

// Function for checking linked 
// list is palindrom or not 
int checkPalin(node* root) 
{ 
    node* voot = root; 

    // Count the nodes 
    // form the back 
    int j = 0; 

    // Set the pointer at the 
    // very first node of the 
    // linklist and count the 
    // length of the linklist 
    while (voot->left != NULL) { 
        j = j + 1; 
        voot = voot->left; 
    } 
    int i = 0; 

    while (i < j) { 
        // Check if the value matches 
        if (voot->val != root->val) 
            return 0; 

        else { 
            i = i + 1; 
            j = j - 1; 
            voot = voot->right; 
            root = root->left; 
        } 
    } 

    return 1; 
} 

// Driver Program 
int main() 
{ 
    node* root = newnode('b'); 
    root->left = newnode('b'); 
    root->right = newnode('a'); 
    root->left->right = newnode('b'); 
    root->left->left = newnode('a'); 

    node* shoot = conv_tree(root, NULL); 

    if (checkPalin(shoot)) 
        cout << "True" << endl; 
    else
        cout << "False" << endl; 
} 

```

## Java

```java

// Java Program to check if 
// the Inorder sequence of a 
// Binary Tree is a palindrome 
import java.util.*; 
class GFG{ 

// Define node of tree 
static class node 
{ 
    char val; 
    node left; 
    node right; 
}; 

// Function to create the node 
static node newnode(char i) 
{ 
    node temp = null; 
    temp = new node(); 
    temp.val = i; 
    temp.left = null; 
    temp.right = null; 
    return temp; 
} 

// Function to convert the tree 
// to the double linked list 
static node conv_tree(node root, 
                      node shoot) 
{ 
    if (root.left != null) 
        shoot = conv_tree(root.left, 
                          shoot); 

    root.left = shoot; 

    if (shoot != null) 
        shoot.right = root; 

    shoot = root; 

    if (root.right != null) 
        shoot = conv_tree(root.right, 
                          shoot); 

    return shoot; 
} 

// Function for checking linked 
// list is palindrom or not 
static int checkPalin(node root) 
{ 
    node voot = root; 

    // Count the nodes 
    // form the back 
    int j = 0; 

    // Set the pointer at the 
    // very first node of the 
    // linklist and count the 
    // length of the linklist 
    while (voot.left != null) 
    { 
        j = j + 1; 
        voot = voot.left; 
    } 
    int i = 0; 

    while (i < j)  
    { 
        // Check if the value matches 
        if (voot.val != root.val) 
            return 0; 

        else 
        { 
            i = i + 1; 
            j = j - 1; 
            voot = voot.right; 
            root = root.left; 
        } 
    } 
    return 1; 
} 

// Driver Code 
public static void main(String[] args) 
{ 
    node root = newnode('b'); 
    root.left = newnode('b'); 
    root.right = newnode('a'); 
    root.left.right = newnode('b'); 
    root.left.left = newnode('a'); 

    node shoot = conv_tree(root, null); 

    if (checkPalin(shoot) == 1) 
        System.out.print("True" + "\n"); 
    else
        System.out.print("False" + "\n"); 
} 
} 

// This code is contributed by 29AjayKumar 

```

## Python3

```py

# Python3 program to check if 
# the Inorder sequence of a 
# Binary Tree is a palindrome 

# Define node of tree 
class Node:  
    def __init__(self,val):  

        self.val = val  
        self.left = None
        self.right = None

# Function to create the node 
def newnode(i): 

    #temp = None; 
    temp = Node(i); 
    temp.val = i; 
    temp.left = None; 
    temp.right = None; 
    return temp; 

# Function to convert the tree 
# to the double linked list 
def conv_tree(root, shoot): 

    if (root.left != None): 
        shoot = conv_tree(root.left, shoot); 

    root.left = shoot; 

    if (shoot != None): 
        shoot.right = root; 

    shoot = root; 

    if (root.right != None): 
        shoot = conv_tree(root.right, shoot); 

    return shoot; 

# Function for checking linked 
# list is palindrom or not 
def checkPalin(root): 

    voot = root; 

    # Count the nodes 
    # form the back 
    j = 0; 

    # Set the pointer at the 
    # very first node of the 
    # linklist and count the 
    # length of the linklist 
    while (voot.left != None):  
        j = j + 1; 
        voot = voot.left; 

    i = 0; 

    while (i < j): 

        # Check if the value matches 
        if (voot.val != root.val): 
            return 0; 
        else: 
            i = i + 1; 
            j = j - 1; 
            voot = voot.right; 
            root = root.left; 

    return 1; 

# Driver code 
if __name__=='__main__':  

    root = newnode('b'); 
    root.left = newnode('b'); 
    root.right = newnode('a'); 
    root.left.right = newnode('b'); 
    root.left.left = newnode('a'); 

    shoot = conv_tree(root, None); 

    if (checkPalin(shoot)): 
        print("True"); 
    else: 
        print("False"); 

# This code is contributed by AbhiThakur 

```

## C#

```cs

// C# program to check if the inorder   
// sequence of a Binary Tree is a  
// palindrome 
using System; 

class GFG{ 

// Define node of tree 
class node 
{ 
    public char val; 
    public node left; 
    public node right; 
}; 

// Function to create the node 
static node newnode(char i) 
{ 
    node temp = null; 
    temp = new node(); 
    temp.val = i; 
    temp.left = null; 
    temp.right = null; 

    return temp; 
} 

// Function to convert the tree 
// to the double linked list 
static node conv_tree(node root, 
                      node shoot) 
{ 
    if (root.left != null) 
        shoot = conv_tree(root.left, 
                          shoot); 

    root.left = shoot; 

    if (shoot != null) 
        shoot.right = root; 

    shoot = root; 

    if (root.right != null) 
        shoot = conv_tree(root.right, 
                          shoot); 

    return shoot; 
} 

// Function for checking linked 
// list is palindrom or not 
static int checkPalin(node root) 
{ 
    node voot = root; 

    // Count the nodes 
    // form the back 
    int j = 0; 

    // Set the pointer at the 
    // very first node of the 
    // linklist and count the 
    // length of the linklist 
    while (voot.left != null) 
    { 
        j = j + 1; 
        voot = voot.left; 
    } 
    int i = 0; 

    while (i < j)  
    { 

        // Check if the value matches 
        if (voot.val != root.val) 
            return 0; 
        else
        { 
            i = i + 1; 
            j = j - 1; 
            voot = voot.right; 
            root = root.left; 
        } 
    } 
    return 1; 
} 

// Driver Code 
public static void Main(String[] args) 
{ 
    node root = newnode('b'); 
    root.left = newnode('b'); 
    root.right = newnode('a'); 
    root.left.right = newnode('b'); 
    root.left.left = newnode('a'); 

    node shoot = conv_tree(root, null); 

    if (checkPalin(shoot) == 1) 
        Console.Write("True" + "\n"); 
    else
        Console.Write("False" + "\n"); 
} 
} 

// This code is contributed by 29AjayKumar 

```

**输出**：

```
True

```

***时间复杂度**：`O(n)`

**辅助空间**：`O(1)`*



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。