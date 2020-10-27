# 从后序和顺序构建二叉树

给定 Postorder 和 Inorder 遍历，构造树。
**示例：** [

```
Input: 
in[]   = {2, 1, 3}
post[] = {2, 3, 1}

Output: Root of below tree
      1
    /   \
   2     3 

Input: 
in[]   = {4, 8, 2, 5, 1, 6, 3, 7}
post[] = {8, 4, 5, 2, 6, 7, 3, 1} 

Output: Root of below tree
          1
       /     \
     2        3
   /    \   /   \
  4     5   6    7
    \
      8

```

我们已经从有序遍历和预遍历遍历讨论了树的[构造。 这个想法是相似的。
让我们看一下从 in [] = {4，8，2，5，1，6，6，3，7}和 post [] = {8，4，5，2，6，7 ，3，1}
**1）**我们首先找到 post []中的最后一个节点。 最后一个节点为“ 1”，我们知道此值为 root，因为 root 总是出现在后顺序遍历的末尾。
**2）**我们在 in []中搜索“ 1”以找到根的左右子树。 in []中“ 1”左侧的所有内容都在左侧子树中，右侧的所有内容都在右侧子树中。](https://www.geeksforgeeks.org/construct-tree-from-given-inorder-and-preorder-traversal/)

```
         1
       /    \
[4, 8, 2, 5]   [6, 3, 7] 

```

**3）**以下两个步骤重复以上过程。
…。 **b）**重复 in​​ [] = {6，3，7}和 post [] = {6，7，3}
……。使创建的树成为根的右子节点。
…。 **a）**重复 in​​ [] = {4，8，2，5}和 post [] = {8，4，5，2}。
……。使创建的树成为根的左子节点。
以下是上述想法的实现。 一个重要的观察结果是，每当创建新节点时，我们都会降低后序索引的索引，因此在左子树之前递归地调用右子树。

## C ++

```

/* C++ program to construct tree using inorder and 
   postorder traversals */
#include <bits/stdc++.h> 

using namespace std; 

/* A binary tree node has data, pointer to left 
   child and a pointer to right child */
struct Node { 
    int data; 
    Node *left, *right; 
}; 

// Utility function to create a new node 
Node* newNode(int data); 

/* Prototypes for utility functions */
int search(int arr[], int strt, int end, int value); 

/* Recursive function to construct binary of size n 
   from  Inorder traversal in[] and Postorder traversal 
   post[].  Initial values of inStrt and inEnd should 
   be 0 and n -1.  The function doesn't do any error 
   checking for cases where inorder and postorder 
   do not form a tree */
Node* buildUtil(int in[], int post[], int inStrt, 
                int inEnd, int* pIndex) 
{ 
    // Base case 
    if (inStrt > inEnd) 
        return NULL; 

    /* Pick current node from Postorder traversal using 
       postIndex and decrement postIndex */
    Node* node = newNode(post[*pIndex]); 
    (*pIndex)--; 

    /* If this node has no children then return */
    if (inStrt == inEnd) 
        return node; 

    /* Else find the index of this node in Inorder 
       traversal */
    int iIndex = search(in, inStrt, inEnd, node->data); 

    /* Using index in Inorder traversal, construct left and 
       right subtress */
    node->right = buildUtil(in, post, iIndex + 1, inEnd, pIndex); 
    node->left = buildUtil(in, post, inStrt, iIndex - 1, pIndex); 

    return node; 
} 

// This function mainly initializes index of root 
// and calls buildUtil() 
Node* buildTree(int in[], int post[], int n) 
{ 
    int pIndex = n - 1; 
    return buildUtil(in, post, 0, n - 1, &pIndex); 
} 

/* Function to find index of value in arr[start...end] 
   The function assumes that value is postsent in in[] */
int search(int arr[], int strt, int end, int value) 
{ 
    int i; 
    for (i = strt; i <= end; i++) { 
        if (arr[i] == value) 
            break; 
    } 
    return i; 
} 

/* Helper function that allocates a new node */
Node* newNode(int data) 
{ 
    Node* node = (Node*)malloc(sizeof(Node)); 
    node->data = data; 
    node->left = node->right = NULL; 
    return (node); 
} 

/* This funtcion is here just to test  */
void preOrder(Node* node) 
{ 
    if (node == NULL) 
        return; 
    printf("%d ", node->data); 
    preOrder(node->left); 
    preOrder(node->right); 
} 

// Driver code 
int main() 
{ 
    int in[] = { 4, 8, 2, 5, 1, 6, 3, 7 }; 
    int post[] = { 8, 4, 5, 2, 6, 7, 3, 1 }; 
    int n = sizeof(in) / sizeof(in[0]); 

    Node* root = buildTree(in, post, n); 

    cout << "Preorder of the constructed tree : \n"; 
    preOrder(root); 

    return 0; 
} 

```

## 爪哇

```

// Java program to construct a tree using inorder 
// and postorder traversals 

/* A binary tree node has data, pointer to left 
   child and a pointer to right child */
class Node { 
    int data; 
    Node left, right; 

    public Node(int data) 
    { 
        this.data = data; 
        left = right = null; 
    } 
} 

// Class Index created to implement pass by reference of Index 
class Index { 
    int index; 
} 

class BinaryTree { 
    /* Recursive function to construct binary of size n 
       from  Inorder traversal in[] and Postrder traversal 
       post[].  Initial values of inStrt and inEnd should 
       be 0 and n -1.  The function doesn't do any error 
       checking for cases where inorder and postorder 
       do not form a tree */
    Node buildUtil(int in[], int post[], int inStrt, 
                   int inEnd, Index pIndex) 
    { 
        // Base case 
        if (inStrt > inEnd) 
            return null; 

        /* Pick current node from Postrder traversal using 
           postIndex and decrement postIndex */
        Node node = new Node(post[pIndex.index]); 
        (pIndex.index)--; 

        /* If this node has no children then return */
        if (inStrt == inEnd) 
            return node; 

        /* Else find the index of this node in Inorder 
           traversal */
        int iIndex = search(in, inStrt, inEnd, node.data); 

        /* Using index in Inorder traversal, construct left and 
           right subtress */
        node.right = buildUtil(in, post, iIndex + 1, inEnd, pIndex); 
        node.left = buildUtil(in, post, inStrt, iIndex - 1, pIndex); 

        return node; 
    } 

    // This function mainly initializes index of root 
    // and calls buildUtil() 
    Node buildTree(int in[], int post[], int n) 
    { 
        Index pIndex = new Index(); 
        pIndex.index = n - 1; 
        return buildUtil(in, post, 0, n - 1, pIndex); 
    } 

    /* Function to find index of value in arr[start...end] 
       The function assumes that value is postsent in in[] */
    int search(int arr[], int strt, int end, int value) 
    { 
        int i; 
        for (i = strt; i <= end; i++) { 
            if (arr[i] == value) 
                break; 
        } 
        return i; 
    } 

    /* This funtcion is here just to test  */
    void preOrder(Node node) 
    { 
        if (node == null) 
            return; 
        System.out.print(node.data + " "); 
        preOrder(node.left); 
        preOrder(node.right); 
    } 

    public static void main(String[] args) 
    { 
        BinaryTree tree = new BinaryTree(); 
        int in[] = new int[] { 4, 8, 2, 5, 1, 6, 3, 7 }; 
        int post[] = new int[] { 8, 4, 5, 2, 6, 7, 3, 1 }; 
        int n = in.length; 
        Node root = tree.buildTree(in, post, n); 
        System.out.println("Preorder of the constructed tree : "); 
        tree.preOrder(root); 
    } 
} 

// This code has been contributed by Mayank Jaiswal(mayank_24) 

```

## Python3

```

# Python3 program to construct tree using  
# inorder and postorder traversals  

# Helper function that allocates  
# a new node  
class newNode: 
    def __init__(self, data): 
        self.data = data  
        self.left = self.right = None

# Recursive function to construct binary  
# of size n from Inorder traversal in[]  
# and Postorder traversal post[]. Initial  
# values of inStrt and inEnd should be  
# 0 and n -1\. The function doesn't do any  
# error checking for cases where inorder  
# and postorder do not form a tree  
def buildUtil(In, post, inStrt, inEnd, pIndex): 

    # Base case  
    if (inStrt > inEnd):  
        return None

    # Pick current node from Postorder traversal  
    # using postIndex and decrement postIndex  
    node = newNode(post[pIndex[0]])  
    pIndex[0] -= 1

    # If this node has no children  
    # then return  
    if (inStrt == inEnd):  
        return node  

    # Else find the index of this node  
    # in Inorder traversal  
    iIndex = search(In, inStrt, inEnd, node.data)  

    # Using index in Inorder traversal,  
    # construct left and right subtress  
    node.right = buildUtil(In, post, iIndex + 1,  
                                  inEnd, pIndex)  
    node.left = buildUtil(In, post, inStrt,  
                        iIndex - 1, pIndex)  

    return node 

# This function mainly initializes index  
# of root and calls buildUtil()  
def buildTree(In, post, n): 
    pIndex = [n - 1]  
    return buildUtil(In, post, 0, n - 1, pIndex) 

# Function to find index of value in  
# arr[start...end]. The function assumes  
# that value is postsent in in[]  
def search(arr, strt, end, value): 
    i = 0
    for i in range(strt, end + 1): 
        if (arr[i] == value):  
            break
    return i 

# This funtcion is here just to test  
def preOrder(node): 
    if node == None:  
        return
    print(node.data,end=" ") 
    preOrder(node.left)  
    preOrder(node.right) 

# Driver code  
if __name__ == '__main__': 
    In = [4, 8, 2, 5, 1, 6, 3, 7] 
    post = [8, 4, 5, 2, 6, 7, 3, 1]  
    n = len(In) 

    root = buildTree(In, post, n)  

    print("Preorder of the constructed tree :")  
    preOrder(root) 

# This code is contributed by PranchalK 

```

## C＃

```

// C# program to construct a tree using  
// inorder and postorder traversals  
using System; 

/* A binary tree node has data, pointer  
to left child and a pointer to right child */
public class Node 
{ 
    public int data; 
    public Node left, right; 

    public Node(int data) 
    { 
        this.data = data; 
        left = right = null; 
    } 
} 

// Class Index created to implement  
// pass by reference of Index  
public class Index 
{ 
    public int index; 
} 

class GFG 
{ 
/* Recursive function to construct binary  
of size n from Inorder traversal in[] and  
Postrder traversal post[]. Initial values  
of inStrt and inEnd should be 0 and n -1.  
The function doesn't do any error checking  
for cases where inorder and postorder do  
not form a tree */
public virtual Node buildUtil(int[] @in, int[] post,  
                              int inStrt, int inEnd,  
                              Index pIndex) 
{ 
    // Base case  
    if (inStrt > inEnd) 
    { 
        return null; 
    } 

    /* Pick current node from Postrder traversal  
    using postIndex and decrement postIndex */
    Node node = new Node(post[pIndex.index]); 
    (pIndex.index)--; 

    /* If this node has no children  
    then return */
    if (inStrt == inEnd) 
    { 
        return node; 
    } 

    /* Else find the index of this node  
    in Inorder traversal */
    int iIndex = search(@in, inStrt, inEnd, node.data); 

    /* Using index in Inorder traversal,  
    construct left and right subtress */
    node.right = buildUtil(@in, post, iIndex + 1, 
                                inEnd, pIndex); 
    node.left = buildUtil(@in, post, inStrt, 
                               iIndex - 1, pIndex); 

    return node; 
} 

// This function mainly initializes  
// index of root and calls buildUtil()  
public virtual Node buildTree(int[] @in, 
                              int[] post, int n) 
{ 
    Index pIndex = new Index(); 
    pIndex.index = n - 1; 
    return buildUtil(@in, post, 0, n - 1, pIndex); 
} 

/* Function to find index of value in  
arr[start...end]. The function assumes 
that value is postsent in in[] */
public virtual int search(int[] arr, int strt,  
                          int end, int value) 
{ 
    int i; 
    for (i = strt; i <= end; i++) 
    { 
        if (arr[i] == value) 
        { 
            break; 
        } 
    } 
    return i; 
} 

/* This funtcion is here just to test */
public virtual void preOrder(Node node) 
{ 
    if (node == null) 
    { 
        return; 
    } 
    Console.Write(node.data + " "); 
    preOrder(node.left); 
    preOrder(node.right); 
} 

// Driver Code 
public static void Main(string[] args) 
{ 
    GFG tree = new GFG(); 
    int[] @in = new int[] {4, 8, 2, 5, 1, 6, 3, 7}; 
    int[] post = new int[] {8, 4, 5, 2, 6, 7, 3, 1}; 
    int n = @in.Length; 
    Node root = tree.buildTree(@in, post, n); 
    Console.WriteLine("Preorder of the constructed tree : "); 
    tree.preOrder(root); 
} 
} 

// This code is contributed by Shrikant13 

```

**Output**

```
Preorder of the constructed tree : 
1 2 4 8 5 3 6 7 
```

**时间复杂度：** O（n <sup>2</sup> ）
**优化的方法：**我们可以使用哈希（C ++中的 unordered_map 或 Java 中的 HashMap）优化上述解决方案。 我们将有序遍历的索引存储在哈希表中。 这样就可以完成 O（1）次搜索。

## C ++

```

/* C++ program to construct tree using inorder and  
postorder traversals */
#include <bits/stdc++.h> 

using namespace std; 

/* A binary tree node has data, pointer to left  
child and a pointer to right child */
struct Node { 
    int data; 
    Node *left, *right; 
}; 

// Utility function to create a new node 
Node* newNode(int data); 

/* Recursive function to construct binary of size n  
from Inorder traversal in[] and Postorder traversal  
post[]. Initial values of inStrt and inEnd should  
be 0 and n -1\. The function doesn't do any error  
checking for cases where inorder and postorder  
do not form a tree */
Node* buildUtil(int in[], int post[], int inStrt, 
    int inEnd, int* pIndex, unordered_map<int, int>& mp) 
{ 
    // Base case 
    if (inStrt > inEnd) 
        return NULL; 

    /* Pick current node from Postorder traversal   
    using postIndex and decrement postIndex */
    int curr = post[*pIndex]; 
    Node* node = newNode(curr); 
    (*pIndex)--; 

    /* If this node has no children then return */
    if (inStrt == inEnd) 
        return node; 

    /* Else find the index of this node in Inorder  
    traversal */
    int iIndex = mp[curr]; 

    /* Using index in Inorder traversal, construct  
    left and right subtress */
    node->right = buildUtil(in, post, iIndex + 1, 
                            inEnd, pIndex, mp); 
    node->left = buildUtil(in, post, inStrt, 
                           iIndex - 1, pIndex, mp); 

    return node; 
} 

// This function mainly creates an unordered_map, then 
// calls buildTreeUtil() 
struct Node* buildTree(int in[], int post[], int len) 
{ 
    // Store indexes of all items so that we 
    // we can quickly find later 
    unordered_map<int, int> mp; 
    for (int i = 0; i < len; i++) 
        mp[in[i]] = i; 

    int index = len - 1; // Index in postorder 
    return buildUtil(in, post, 0, len - 1, 
                     &index, mp); 
} 

/* Helper function that allocates a new node */
Node* newNode(int data) 
{ 
    Node* node = (Node*)malloc(sizeof(Node)); 
    node->data = data; 
    node->left = node->right = NULL; 
    return (node); 
} 

/* This funtcion is here just to test */
void preOrder(Node* node) 
{ 
    if (node == NULL) 
        return; 
    printf("%d ", node->data); 
    preOrder(node->left); 
    preOrder(node->right); 
} 

// Driver code 
int main() 
{ 
    int in[] = { 4, 8, 2, 5, 1, 6, 3, 7 }; 
    int post[] = { 8, 4, 5, 2, 6, 7, 3, 1 }; 
    int n = sizeof(in) / sizeof(in[0]); 

    Node* root = buildTree(in, post, n); 

    cout << "Preorder of the constructed tree : \n"; 
    preOrder(root); 

    return 0; 
} 

```

**Output**

```
Preorder of the constructed tree : 
1 2 4 8 5 3 6 7 
```

**时间复杂度：** O（n）

**另一种方法**：

使用堆栈和设置而不使用递归。

以下是上述想法的实现：

## C ++

```

// CPP program for above approach 
#include <bits/stdc++.h>  
using namespace std;  

/* A binary tree node has data, pointer 
to left   child and a pointer to right  
child */
struct Node  
{  
  int data;  
  Node *left, *right;  
  Node(int x) 
  { 
    data = x; 
    left = right = NULL; 
  } 
}; 

/*Tree building function*/
Node *buildTree(int in[], int post[], int n)  
{ 

  // Create Stack of type Node* 
  stack<Node*> st; 

  // Create Set of type Node* 
  set<Node*> s; 

  // Initialise postIndex with n - 1 
  int postIndex = n - 1; 

  // Initialise root with NULL 
  Node* root = NULL; 

  for (int p = n - 1, i = n - 1; p>=0; )   
  {  

    // Initialise node with NULL 
    Node* node = NULL;  

    // Run do-while loop 
    do
    {  

      // Initialise node with 
      // new Node(post[p]);  
      node = new Node(post[p]);  

      // Check is root is  
      // equal to NULL 
      if (root == NULL)  
      {  
        root = node;  
      }  

      // If size of set  
      // is greater than 0 
      if (st.size() > 0)   
      {  

        // If st.top() is present in the 
        // set s 
        if (s.find(st.top()) != s.end())  
        {  
          s.erase(st.top());  
          st.top()->left = node;  
          st.pop();  
        }  
        else
        {  
          st.top()->right = node;  
        }  
      } 

      st.push(node);  

    } while (post[p--] != in[i] && p >=0);  

    node = NULL;  

    // If the stack is not empty and 
    // st.top()->data is equal to in[i] 
    while (st.size() > 0 && i>=0 &&   
           st.top()->data == in[i])   
    {  
      node = st.top();  

      // Pop elements from stack 
      st.pop();  
      i--;  
    }  

    // if node not equal to NULL 
    if (node != NULL)   
    {  
      s.insert(node);  
      st.push(node);  
    }  
  }  

  // Return root 
  return root; 

} 
/* for print preOrder Traversal */
void preOrder(Node* node)  
{  
  if (node == NULL)  
    return;  
  printf("%d ", node->data);  
  preOrder(node->left);  
  preOrder(node->right);  
} 

// Driver Code 
int main()  
{ 

  int in[] = { 4, 8, 2, 5, 1, 6, 3, 7 };  
  int post[] = { 8, 4, 5, 2, 6, 7, 3, 1 };  
  int n = sizeof(in) / sizeof(in[0]);  

  // Function Call 
  Node* root = buildTree(in, post, n);  

  cout << "Preorder of the constructed  
                                tree : \n";  

  // Function Call for preOrder 
  preOrder(root);  
  return 0; 
} 

```

**Output**

```
Preorder of the constructed tree : 
1 2 4 8 5 3 6 7 
```

本文由 **Rishi** 提供。 如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请发表评论。

注意读者！ 现在不要停止学习。 通过 [**DSA 自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的 DSA 概念，并为行业做好准备。