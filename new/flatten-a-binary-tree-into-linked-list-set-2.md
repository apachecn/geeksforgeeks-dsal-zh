# 将二叉树展平为链接列表| 第 2 组

给定一个二叉树，将其展平为一个链表。 展平后，每个节点的左侧应指向 NULL，右侧应按级别顺序包含下一个节点。

**范例**：

```
Input: 
          1
        /   \
       2     5
      / \     \
     3   4     6

Output:
    1
     \
      2
       \
        3
         \
          4
           \
            5
             \
              6

Input:
        1
       / \
      3   4
         /
        2
         \
          5
Output:
     1
      \
       3
        \
         4
          \
           2
            \ 
             5

```

**方法**：在先前的 [](https://www.geeksforgeeks.org/flatten-a-binary-tree-into-linked-list/) 中已经讨论了使用递归的方法。 这种方法暗示了使用堆栈对二叉树进行预遍历。 在此遍历中，每次将右子项推入堆栈时，都会使右子项等于左子项，并使左子项等于 NULL。 如果节点的右子节点变为 NULL，则会弹出堆栈，而右子节点将从堆栈中弹出。 重复上述步骤，直到堆栈的大小为零或根为 NULL。

下面是上述方法的实现：

## C++

```cpp

// C++ program to flatten the linked  
// list using stack | set-2  
#include <iostream> 
#include <stack> 
using namespace std; 

struct Node { 
    int key; 
    Node *left, *right; 
}; 

/* utility that allocates a new Node  
   with the given key  */
Node* newNode(int key) 
{ 
    Node* node = new Node; 
    node->key = key; 
    node->left = node->right = NULL; 
    return (node); 
} 

// To find the inorder traversal 
void inorder(struct Node* root) 
{ 
    // base condition 
    if (root == NULL) 
        return; 
    inorder(root->left); 
    cout << root->key << " "; 
    inorder(root->right); 
} 

// Function to convert binary tree into 
// linked list by altering the right node 
// and making left node point to NULL 
Node* solution(Node* A) 
{ 

    // Declare a stack 
    stack<Node*> st; 
    Node* ans = A; 

    // Iterate till the stack is not empty 
    // and till root is Null 
    while (A != NULL || st.size() != 0) { 

        // Check for NULL 
        if (A->right != NULL) { 
            st.push(A->right); 
        } 

        // Make the Right Left and 
        // left NULL 
        A->right = A->left; 
        A->left = NULL; 

        // Check for NULL 
        if (A->right == NULL && st.size() != 0) { 
            A->right = st.top(); 
            st.pop(); 
        } 

        // Iterate 
        A = A->right; 
    } 
    return ans; 
} 

// Driver Code 
int main() 
{ 
    /*    1 
        /   \ 
       2     5 
      / \     \ 
     3   4     6 */

    // Build the tree 
    Node* root = newNode(1); 
    root->left = newNode(2); 
    root->right = newNode(5); 
    root->left->left = newNode(3); 
    root->left->right = newNode(4); 
    root->right->right = newNode(6); 

    // Call the function to 
    // flatten the tree 
    root = solution(root); 

    cout << "The Inorder traversal after "
            "flattening binary tree "; 

    // call the function to print 
    // inorder after flatenning 
    inorder(root); 
    return 0; 

    return 0; 
} 

```

## Java

```java

// Java program to flatten the linked  
// list using stack | set-2  
import java.util.Stack; 

class GFG  
{ 

static class Node 
{ 
    int key; 
    Node left, right; 
} 

/* utility that allocates a new Node  
with the given key */
static Node newNode(int key) 
{ 
    Node node = new Node(); 
    node.key = key; 
    node.left = node.right = null; 
    return (node); 
} 

// To find the inorder traversal 
static void inorder(Node root) 
{ 
    // base condition 
    if (root == null) 
        return; 
    inorder(root.left); 
    System.out.print(root.key + " "); 
    inorder(root.right); 
} 

// Function to convert binary tree into 
// linked list by altering the right node 
// and making left node point to null 
static Node solution(Node A) 
{ 

    // Declare a stack 
    Stack<Node> st = new Stack<>(); 
    Node ans = A; 

    // Iterate till the stack is not empty 
    // and till root is Null 
    while (A != null || st.size() != 0)  
    { 

        // Check for null 
        if (A.right != null)  
        { 
            st.push(A.right); 
        } 

        // Make the Right Left and 
        // left null 
        A.right = A.left; 
        A.left = null; 

        // Check for null 
        if (A.right == null && st.size() != 0) 
        { 
            A.right = st.peek(); 
            st.pop(); 
        } 

        // Iterate 
        A = A.right; 
    } 
    return ans; 
} 

// Driver Code 
public static void main(String[] args)  
{ 
    /* 1 
        / \ 
    2     5 
    / \     \ 
    3 4     6 */

    // Build the tree 
    Node root = newNode(1); 
    root.left = newNode(2); 
    root.right = newNode(5); 
    root.left.left = newNode(3); 
    root.left.right = newNode(4); 
    root.right.right = newNode(6); 

    // Call the function to 
    // flatten the tree 
    root = solution(root); 

    System.out.print("The Inorder traversal after "
            +"flattening binary tree "); 

    // call the function to print 
    // inorder after flatenning 
    inorder(root); 
} 
} 

// This code has been contributed by 29AjayKumar 

```

## C#

```cs

// C# program to flatten the linked  
// list using stack | set-2  
using System; 
using System.Collections.Generic; 

class GFG  
{ 
    public class Node 
    { 
        public int key; 
        public Node left, right; 
    } 

    /* utility that allocates a new Node  
    with the given key */
    static Node newNode(int key) 
    { 
        Node node = new Node(); 
        node.key = key; 
        node.left = node.right = null; 
        return (node); 
    } 

    // To find the inorder traversal 
    static void inorder(Node root) 
    { 
        // base condition 
        if (root == null) 
            return; 
        inorder(root.left); 
        Console.Write(root.key + " "); 
        inorder(root.right); 
    } 

    // Function to convert binary tree into 
    // linked list by altering the right node 
    // and making left node point to null 
    static Node solution(Node A) 
    { 

        // Declare a stack 
        Stack<Node> st = new Stack<Node>(); 
        Node ans = A; 

        // Iterate till the stack is not empty 
        // and till root is Null 
        while (A != null || st.Count != 0)  
        { 

            // Check for null 
            if (A.right != null)  
            { 
                st.Push(A.right); 
            } 

            // Make the Right Left and 
            // left null 
            A.right = A.left; 
            A.left = null; 

            // Check for null 
            if (A.right == null && st.Count != 0) 
            { 
                A.right = st.Peek(); 
                st.Pop(); 
            } 

            // Iterate 
            A = A.right; 
        } 
        return ans; 
    } 

    // Driver Code 
    public static void Main(String[] args)  
    { 
        /* 1 
          / \ 
         2     5 
        / \     \ 
        3 4     6 */

        // Build the tree 
        Node root = newNode(1); 
        root.left = newNode(2); 
        root.right = newNode(5); 
        root.left.left = newNode(3); 
        root.left.right = newNode(4); 
        root.right.right = newNode(6); 

        // Call the function to 
        // flatten the tree 
        root = solution(root); 

        Console.Write("The Inorder traversal after "
                +"flattening binary tree "); 

        // call the function to print 
        // inorder after flatenning 
        inorder(root); 
    } 
} 

// This code contributed by Rajput-Ji 

```

**Output:**

```
The Inorder traversal after flattening binary tree 1 2 3 4 5 6

```

**时间复杂度**：`O(n)`

**辅助空间**：O（Log N）



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。