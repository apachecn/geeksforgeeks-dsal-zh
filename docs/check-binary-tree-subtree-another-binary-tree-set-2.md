# 检查一棵二叉树是否是另一棵二叉树的子树|集合 2

> 原文:[https://www . geesforgeks . org/check-二叉树-子树-另一个-二叉树-set-2/](https://www.geeksforgeeks.org/check-binary-tree-subtree-another-binary-tree-set-2/)

给定两个二叉树，检查第一个树是否是第二个树的子树。树 T 的子树是由 T 中的一个节点及其在 T 中的所有后代组成的树 S。
根节点对应的子树是整棵树；对应于任何其他节点的子树称为适当的子树。
例如，在以下情况下，Tree1 是 Tree2 的子树。

```
        Tree1
          x 
        /    \
      a       b
       \
        c

        Tree2
              z
            /   \
          x      e
        /    \     \
      a       b      k
       \
        c

```

对于这个问题，我们已经讨论了[一个 O(n)<sup>2</sup>的解决方案。在这篇文章中，讨论了一个 O(n)的解决方案。这个想法是基于这样一个事实，即](https://www.geeksforgeeks.org/check-if-a-binary-tree-is-subtree-of-another-binary-tree/)[序和前序/后序唯一地标识了一个二叉树](https://www.geeksforgeeks.org/if-you-are-given-two-traversal-sequences-can-you-construct-the-binary-tree/)。树 S 是 T 的一个子树，如果 S 的有序和前序遍历分别是 T 的有序和前序遍历的子串。
以下是详细步骤。
**1** )查找 T 的有序和预有序遍历，将它们存储在两个辅助数组 inT[]和 preT[]中。
**2** )找到 S 的有序和预有序遍历，将它们存储在两个辅助数组 inS[]和 preS[]中。
**3** )如果 inS[]是 inT[]的子数组，preS[]是 preT[]的子数组，那么 S 就是 t 的子树，否则不是。
在上面的算法中，我们也可以用后序遍历来代替前序。
让我们考虑一下上面的例子

```
Inorder and Preorder traversals of the big tree are.
inT[]   =  {a, c, x, b, z, e, k}
preT[]  =  {z, x, a, c, b, e, k}

Inorder and Preorder traversals of small tree are
inS[]  = {a, c, x, b}
preS[] = {x, a, c, b}

We can easily figure out that inS[] is a subarray of
inT[] and preS[] is a subarray of preT[]. 

```

编辑

```
The above algorithm doesn't work for cases where a tree is present
in another tree, but not as a subtree. Consider the following example.

        Tree1
          x 
        /    \
      a       b
     /        
    c         

        Tree2
          x 
        /    \
      a       b
     /         \
    c            d

Inorder and Preorder traversals of the big tree or Tree2 are.

Inorder and Preorder traversals of small tree or Tree1 are

The Tree2 is not a subtree of Tree1, but inS[] and preS[] are
subarrays of inT[] and preT[] respectively.

```

只要我们在有序和前序遍历中遇到空值，就可以通过添加一个特殊字符来扩展上述算法来处理这种情况。感谢 Shivam Goel 建议本次延期。
以下是上述算法的实现。

## C++

```
#include <cstring>
#include <iostream>
using namespace std;
#define MAX 100

// Structure of a tree node
struct Node {
    char key;
    struct Node *left, *right;
};

// A utility function to create a new BST node
Node* newNode(char item)
{
    Node* temp = new Node;
    temp->key = item;
    temp->left = temp->right = NULL;
    return temp;
}

// A utility function to store inorder traversal of tree rooted
// with root in an array arr[]. Note that i is passed as reference
void storeInorder(Node* root, char arr[], int& i)
{
    if (root == NULL) {
        arr[i++] = '{content}apos;;
        return;
    }
    storeInorder(root->left, arr, i);
    arr[i++] = root->key;
    storeInorder(root->right, arr, i);
}

// A utility function to store preorder traversal of tree rooted
// with root in an array arr[]. Note that i is passed as reference
void storePreOrder(Node* root, char arr[], int& i)
{
    if (root == NULL) {
        arr[i++] = '{content}apos;;
        return;
    }
    arr[i++] = root->key;
    storePreOrder(root->left, arr, i);
    storePreOrder(root->right, arr, i);
}

/* This function returns true if S is a subtree of T, otherwise false */
bool isSubtree(Node* T, Node* S)
{
    /* base cases */
    if (S == NULL)
        return true;
    if (T == NULL)
        return false;

    // Store Inorder traversals of T and S in inT[0..m-1]
    // and inS[0..n-1] respectively
    int m = 0, n = 0;
    char inT[MAX], inS[MAX];
    storeInorder(T, inT, m);
    storeInorder(S, inS, n);
    inT[m] = '\0', inS[n] = '\0';

    // If inS[] is not a substring of inT[], return false
    if (strstr(inT, inS) == NULL)
        return false;

    // Store Preorder traversals of T and S in preT[0..m-1]
    // and preS[0..n-1] respectively
    m = 0, n = 0;
    char preT[MAX], preS[MAX];
    storePreOrder(T, preT, m);
    storePreOrder(S, preS, n);
    preT[m] = '\0', preS[n] = '\0';

    // If preS[] is not a substring of preT[], return false
    // Else return true
    return (strstr(preT, preS) != NULL);
}

// Driver program to test above function
int main()
{
    Node* T = newNode('a');
    T->left = newNode('b');
    T->right = newNode('d');
    T->left->left = newNode('c');
    T->right->right = newNode('e');

    Node* S = newNode('a');
    S->left = newNode('b');
    S->left->left = newNode('c');
    S->right = newNode('d');

    if (isSubtree(T, S))
        cout << "Yes: S is a subtree of T";
    else
        cout << "No: S is NOT a subtree of T";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if binary tree
// is subtree of another binary tree
class Node {

    char data;
    Node left, right;

    Node(char item)
    {
        data = item;
        left = right = null;
    }
}

class Passing {

    int i;
    int m = 0;
    int n = 0;
}

class BinaryTree {

    static Node root;
    Passing p = new Passing();

    String strstr(String haystack, String needle)
    {
        if (haystack == null || needle == null) {
            return null;
        }
        int hLength = haystack.length();
        int nLength = needle.length();
        if (hLength < nLength) {
            return null;
        }
        if (nLength == 0) {
            return haystack;
        }
        for (int i = 0; i <= hLength - nLength; i++) {
            if (haystack.charAt(i) == needle.charAt(0)) {
                int j = 0;
                for (; j < nLength; j++) {
                    if (haystack.charAt(i + j) != needle.charAt(j)) {
                        break;
                    }
                }
                if (j == nLength) {
                    return haystack.substring(i);
                }
            }
        }
        return null;
    }

    // A utility function to store inorder traversal of tree rooted
    // with root in an array arr[]. Note that i is passed as reference
    void storeInorder(Node node, char arr[], Passing i)
    {
        if (node == null) {
            arr[i.i++] = '{content}apos;;
            return;
        }
        storeInorder(node.left, arr, i);
        arr[i.i++] = node.data;
        storeInorder(node.right, arr, i);
    }

    // A utility function to store preorder traversal of tree rooted
    // with root in an array arr[]. Note that i is passed as reference
    void storePreOrder(Node node, char arr[], Passing i)
    {
        if (node == null) {
            arr[i.i++] = '{content}apos;;
            return;
        }
        arr[i.i++] = node.data;
        storePreOrder(node.left, arr, i);
        storePreOrder(node.right, arr, i);
    }

    /* This function returns true if S is a subtree of T, otherwise false */
    boolean isSubtree(Node T, Node S)
    {
        /* base cases */
        if (S == null) {
            return true;
        }
        if (T == null) {
            return false;
        }

        // Store Inorder traversals of T and S in inT[0..m-1]
        // and inS[0..n-1] respectively
        char inT[] = new char[100];
        String op1 = String.valueOf(inT);
        char inS[] = new char[100];
        String op2 = String.valueOf(inS);
        storeInorder(T, inT, p);
        storeInorder(S, inS, p);
        inT[p.m] = '\0';
        inS[p.m] = '\0';

        // If inS[] is not a substring of preS[], return false
        if (strstr(op1, op2) != null) {
            return false;
        }

        // Store Preorder traversals of T and S in inT[0..m-1]
        // and inS[0..n-1] respectively
        p.m = 0;
        p.n = 0;
        char preT[] = new char[100];
        char preS[] = new char[100];
        String op3 = String.valueOf(preT);
        String op4 = String.valueOf(preS);
        storePreOrder(T, preT, p);
        storePreOrder(S, preS, p);
        preT[p.m] = '\0';
        preS[p.n] = '\0';

        // If inS[] is not a substring of preS[], return false
        // Else return true
        return (strstr(op3, op4) != null);
    }

    // Driver program to test above functions
    public static void main(String args[])
    {
        BinaryTree tree = new BinaryTree();
        Node T = new Node('a');
        T.left = new Node('b');
        T.right = new Node('d');
        T.left.left = new Node('c');
        T.right.right = new Node('e');

        Node S = new Node('a');
        S.left = new Node('b');
        S.right = new Node('d');
        S.left.left = new Node('c');

        if (tree.isSubtree(T, S)) {
            System.out.println("Yes, S is a subtree of T");
        }
        else {
            System.out.println("No, S is not a subtree of T");
        }
    }
}

// This code is contributed by Mayank Jaiswal
```

## C#

```
// C# program to check if binary tree is
// subtree of another binary tree
using System;

public class Node {

    public char data;
    public Node left, right;

    public Node(char item)
    {
        data = item;
        left = right = null;
    }
}

public class Passing {

    public int i;
    public int m = 0;
    public int n = 0;
}

public class BinaryTree {

    static Node root;
    Passing p = new Passing();

    String strstr(String haystack, String needle)
    {
        if (haystack == null || needle == null) {
            return null;
        }
        int hLength = haystack.Length;
        int nLength = needle.Length;
        if (hLength < nLength) {
            return null;
        }
        if (nLength == 0) {
            return haystack;
        }
        for (int i = 0; i <= hLength - nLength; i++) {
            if (haystack[i] == needle[0]) {
                int j = 0;
                for (; j < nLength; j++) {
                    if (haystack[i + j] != needle[j]) {
                        break;
                    }
                }
                if (j == nLength) {
                    return haystack.Substring(i);
                }
            }
        }
        return null;
    }

    // A utility function to store inorder
    // traversal of tree rooted with root in
    // an array arr[]. Note that i is passed as reference
    void storeInorder(Node node, char[] arr, Passing i)
    {
        if (node == null) {
            arr[i.i++] = '{content}apos;;
            return;
        }
        storeInorder(node.left, arr, i);
        arr[i.i++] = node.data;
        storeInorder(node.right, arr, i);
    }

    // A utility function to store preorder
    // traversal of tree rooted with root in
    // an array arr[]. Note that i is passed as reference
    void storePreOrder(Node node, char[] arr, Passing i)
    {
        if (node == null) {
            arr[i.i++] = '{content}apos;;
            return;
        }
        arr[i.i++] = node.data;
        storePreOrder(node.left, arr, i);
        storePreOrder(node.right, arr, i);
    }

    /* This function returns true if S
    is a subtree of T, otherwise false */
    bool isSubtree(Node T, Node S)
    {
        /* base cases */
        if (S == null) {
            return true;
        }
        if (T == null) {
            return false;
        }

        // Store Inorder traversals of T and S in inT[0..m-1]
        // and inS[0..n-1] respectively
        char[] inT = new char[100];
        String op1 = String.Join("", inT);
        char[] inS = new char[100];
        String op2 = String.Join("", inS);
        storeInorder(T, inT, p);
        storeInorder(S, inS, p);
        inT[p.m] = '\0';
        inS[p.m] = '\0';

        // If inS[] is not a substring of preS[], return false
        if (strstr(op1, op2) != null) {
            return false;
        }

        // Store Preorder traversals of T and S in inT[0..m-1]
        // and inS[0..n-1] respectively
        p.m = 0;
        p.n = 0;
        char[] preT = new char[100];
        char[] preS = new char[100];
        String op3 = String.Join("", preT);
        String op4 = String.Join("", preS);
        storePreOrder(T, preT, p);
        storePreOrder(S, preS, p);
        preT[p.m] = '\0';
        preS[p.n] = '\0';

        // If inS[] is not a substring of preS[], return false
        // Else return true
        return (strstr(op3, op4) != null);
    }

    // Driver program to test above functions
    public static void Main(String[] args)
    {
        BinaryTree tree = new BinaryTree();
        Node T = new Node('a');
        T.left = new Node('b');
        T.right = new Node('d');
        T.left.left = new Node('c');
        T.right.right = new Node('e');

        Node S = new Node('a');
        S.left = new Node('b');
        S.right = new Node('d');
        S.left.left = new Node('c');

        if (tree.isSubtree(T, S)) {
            Console.WriteLine("Yes, S is a subtree of T");
        }
        else {
            Console.WriteLine("No, S is not a subtree of T");
        }
    }
}

// This code contributed by Rajput-Ji
```

**输出:**

```
No: S is NOT a subtree of T

```

**时间复杂度:**二叉树的有序和前序遍历花费 O(n)个时间。功能[strtr()](http://www.cplusplus.com/reference/cstring/strstr/)也可以使用 [KMP 字符串匹配算法](https://www.geeksforgeeks.org/searching-for-patterns-set-2-kmp-algorithm/)在 O(n)时间内实现。
**辅助空间:** O(n)
感谢**阿什维尼辛格**提出此法。如果您发现任何不正确的地方，请写评论，或者您想分享更多关于上面讨论的主题的信息