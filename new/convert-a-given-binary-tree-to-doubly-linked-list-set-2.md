# 将给定的二叉树转换为双链表| 设置2

给定二叉树（BT），将其转换为双链表（DLL）。 节点中的左指针和右指针分别用作转换后的DLL中的上一个指针和下一个指针。 DLL中节点的顺序必须与给定二叉树的顺序相同。 有序遍历的第一个节点（BT中最左边的节点）必须是DLL的头节点。

[![TreeToList](img/1e6723c342ed8e5706a1c58b68241a4c.png)](https://media.geeksforgeeks.org/wp-content/cdn-uploads/TreeToList.png)

在的[中讨论了此问题的解决方案。
在这篇文章中，讨论了另一个简单有效的解决方案。 这里讨论的解决方案有两个简单的步骤。](https://www.geeksforgeeks.org/in-place-convert-a-given-binary-tree-to-doubly-linked-list/)

**1）*固定左指针*：**在此步骤中，我们将左指针更改为指向DLL中的先前节点。 想法很简单，我们对树进行有序遍历。 在有序遍历中，我们跟踪先前访问的节点，并将左指针更改为先前的节点。 请参见以下实现中的 *fixPrevPtr（）*。

**2）*固定右指针*：**上面的内容非常直观和简单。 如何更改指向DLL中下一个节点的右指针？ 这个想法是使用在步骤1中固定的左指针。我们从二叉树（BT）的最右边的节点开始。 最右边的节点是DLL中的最后一个节点。 由于左指针已更改为指向DLL中的上一个节点，因此我们可以使用这些指针线性遍历整个DLL。 遍历将是从最后一个节点到第一个节点。 在遍历DLL时，我们跟踪先前访问的节点，并更改指向先前节点的右指针。 请参见以下实现中的 *fixNextPtr（）*。

## C ++

```

// A simple inorder traversal based  
// program to convert a Binary Tree to DLL  
#include <bits/stdc++.h> 
using namespace std; 

// A tree node  
class node  
{  
    public: 
    int data;  
    node *left, *right;  
};  

// A utility function to create 
// a new tree node  
node *newNode(int data)  
{  
    node *Node = new node(); 
    Node->data = data;  
    Node->left = Node->right = NULL;  
    return(Node);  
}  

// Standard Inorder traversal of tree  
void inorder(node *root)  
{  
    if (root != NULL)  
    {  
        inorder(root->left);  
        cout << "\t" << root->data;  
        inorder(root->right);  
    }  
}  

// Changes left pointers to work as  
// previous pointers in converted DLL  
// The function simply does inorder  
// traversal of Binary Tree and updates  
// left pointer using previously visited node  
void fixPrevPtr(node *root)  
{  
    static node *pre = NULL;  

    if (root != NULL)  
    {  
        fixPrevPtr(root->left);  
        root->left = pre;  
        pre = root;  
        fixPrevPtr(root->right);  
    }  
}  

// Changes right pointers to work  
// as next pointers in converted DLL  
node *fixNextPtr(node *root)  
{  
    node *prev = NULL;  

    // Find the right most node  
    // in BT or last node in DLL  
    while (root && root->right != NULL)  
        root = root->right;  

    // Start from the rightmost node,  
    // traverse back using left pointers.  
    // While traversing, change right pointer of nodes.  
    while (root && root->left != NULL)  
    {  
        prev = root;  
        root = root->left;  
        root->right = prev;  
    }  

    // The leftmost node is head  
    // of linked list, return it  
    return (root);  
}  

// The main function that converts  
// BST to DLL and returns head of DLL  
node *BTToDLL(node *root)  
{  
    // Set the previous pointer  
    fixPrevPtr(root);  

    // Set the next pointer and return head of DLL  
    return fixNextPtr(root);  
}  

// Traverses the DLL from left tor right  
void printList(node *root)  
{  
    while (root != NULL)  
    {  
        cout<<"\t"<<root->data;  
        root = root->right;  
    }  
}  

// Driver code  
int main(void)  
{  
    // Let us create the tree  
    // shown in above diagram  
    node *root = newNode(10);  
    root->left = newNode(12);  
    root->right = newNode(15);  
    root->left->left = newNode(25);  
    root->left->right = newNode(30);  
    root->right->left = newNode(36);  

    cout<<"\n\t\tInorder Tree Traversal\n\n";  
    inorder(root);  

    node *head = BTToDLL(root);  

    cout << "\n\n\t\tDLL Traversal\n\n";  
    printList(head);  
    return 0;  
} 

// This code is contributed by rathbhupendra 

```

## C

```

// A simple inorder traversal based program to convert a Binary Tree to DLL 
#include<stdio.h> 
#include<stdlib.h> 

// A tree node 
struct node 
{ 
    int data; 
    struct node *left, *right; 
}; 

// A utility function to create a new tree node 
struct node *newNode(int data) 
{ 
    struct node *node = (struct node *)malloc(sizeof(struct node)); 
    node->data = data; 
    node->left = node->right = NULL; 
    return(node); 
} 

// Standard Inorder traversal of tree 
void inorder(struct node *root) 
{ 
    if (root != NULL) 
    { 
        inorder(root->left); 
        printf("\t%d",root->data); 
        inorder(root->right); 
    } 
} 

// Changes left pointers to work as previous pointers in converted DLL 
// The function simply does inorder traversal of Binary Tree and updates 
// left pointer using previously visited node 
void fixPrevPtr(struct node *root) 
{ 
    static struct node *pre = NULL; 

    if (root != NULL) 
    { 
        fixPrevPtr(root->left); 
        root->left = pre; 
        pre = root; 
        fixPrevPtr(root->right); 
    } 
} 

// Changes right pointers to work as next pointers in converted DLL 
struct node *fixNextPtr(struct node *root) 
{ 
    struct node *prev = NULL; 

    // Find the right most node in BT or last node in DLL 
    while (root && root->right != NULL) 
        root = root->right; 

    // Start from the rightmost node, traverse back using left pointers. 
    // While traversing, change right pointer of nodes. 
    while (root && root->left != NULL) 
    { 
        prev = root; 
        root = root->left; 
        root->right = prev; 
    } 

    // The leftmost node is head of linked list, return it 
    return (root); 
} 

// The main function that converts BST to DLL and returns head of DLL 
struct node *BTToDLL(struct node *root) 
{ 
    // Set the previous pointer 
    fixPrevPtr(root); 

    // Set the next pointer and return head of DLL 
    return fixNextPtr(root); 
} 

// Traverses the DLL from left tor right 
void printList(struct node *root) 
{ 
    while (root != NULL) 
    { 
        printf("\t%d", root->data); 
        root = root->right; 
    } 
} 

// Driver program to test above functions 
int main(void) 
{ 
    // Let us create the tree shown in above diagram 
    struct node *root = newNode(10); 
    root->left        = newNode(12); 
    root->right       = newNode(15); 
    root->left->left  = newNode(25); 
    root->left->right = newNode(30); 
    root->right->left = newNode(36); 

    printf("\n\t\tInorder Tree Traversal\n\n"); 
    inorder(root); 

    struct node *head = BTToDLL(root); 

    printf("\n\n\t\tDLL Traversal\n\n"); 
    printList(head); 
    return 0; 
} 

```

## 爪哇

```

// Java program to convert BTT to DLL using 
// simple inorder traversal 

public class BinaryTreeToDLL  
{ 
    static class node  
    { 
        int data; 
        node left, right; 

        public node(int data)  
        { 
            this.data = data; 
        } 
    } 

    static node prev; 

    // Changes left pointers to work as previous  
    // pointers in converted DLL The function  
    // simply does inorder traversal of Binary  
    // Tree and updates left pointer using  
    // previously visited node 
    static void fixPrevptr(node root)  
    { 
        if (root == null) 
            return; 

        fixPrevptr(root.left); 
        root.left = prev; 
        prev = root; 
        fixPrevptr(root.right); 

    } 

    // Changes right pointers to work  
    // as next pointers in converted DLL 
    static node fixNextptr(node root)  
    {         
        // Find the right most node in  
        // BT or last node in DLL 
        while (root.right != null) 
            root = root.right; 

        // Start from the rightmost node, traverse  
        // back using left pointers. While traversing,  
        // change right pointer of nodes 
        while (root != null && root.left != null)  
        { 
            node left = root.left; 
            left.right = root; 
            root = root.left; 
        } 

        // The leftmost node is head of linked list, return it 
        return root; 
    } 

    static node BTTtoDLL(node root)  
    { 
        prev = null; 

        // Set the previous pointer 
        fixPrevptr(root); 

        // Set the next pointer and return head of DLL 
        return fixNextptr(root); 
    } 

    // Traverses the DLL from left tor right 
    static void printlist(node root)  
    { 
        while (root != null)  
        { 
            System.out.print(root.data + " "); 
            root = root.right; 
        } 
    } 

    // Standard Inorder traversal of tree 
    static void inorder(node root)  
    { 
        if (root == null) 
            return; 
        inorder(root.left); 
        System.out.print(root.data + " "); 
        inorder(root.right); 
    } 

    public static void main(String[] args)  
    { 
        // Let us create the tree shown in above diagram 
        node root = new node(10); 
        root.left = new node(12); 
        root.right = new node(15); 
        root.left.left = new node(25); 
        root.left.right = new node(30); 
        root.right.left = new node(36); 

        System.out.println("Inorder Tree Traversal"); 
        inorder(root); 

        node head = BTTtoDLL(root); 

        System.out.println("\nDLL Traversal"); 
        printlist(head); 
    } 
} 

// This code is contributed by Rishabh Mahrsee 

```

## 蟒蛇

```

# A simple inorder traversal based program to convert a  
# Binary Tree to DLL 

# A Binary Tree node 
class Node: 

    # Constructor to create a new tree node 
    def __init__(self, data): 
        self.data = data  
        self.left = None
        self.right = None

# Standard Inorder traversal of tree 
def inorder(root): 

    if root is not None: 
        inorder(root.left) 
        print "\t%d" %(root.data), 
        inorder(root.right) 

# Changes left pointers to work as previous pointers 
# in converted DLL 
# The function simply does inorder traversal of  
# Binary Tree and updates 
# left pointer using previously visited node 
def fixPrevPtr(root): 
    if root is not None: 
        fixPrevPtr(root.left) 
        root.left = fixPrevPtr.pre 
        fixPrevPtr.pre = root  
        fixPrevPtr(root.right) 

# Changes right pointers to work as nexr pointers in 
# converted DLL  
def fixNextPtr(root): 

    prev = None
    # Find the right most node in BT or last node in DLL 
    while(root and root.right != None): 
        root = root.right  

    # Start from the rightmost node, traverse back using 
    # left pointers 
    # While traversing, change right pointer of nodes  
    while(root and root.left != None): 
        prev = root  
        root = root.left  
        root.right = prev 

    # The leftmost node is head of linked list, return it 
    return root  

# The main function that converts BST to DLL and returns 
# head of DLL 
def BTToDLL(root): 

    # Set the previous pointer  
    fixPrevPtr(root) 

    # Set the next pointer and return head of DLL 
    return fixNextPtr(root) 

# Traversses the DLL from left to right  
def printList(root): 
    while(root != None): 
        print "\t%d" %(root.data), 
        root = root.right 

# Driver program to test above function 
root = Node(10) 
root.left = Node(12) 
root.right = Node(15) 
root.left.left = Node(25) 
root.left.right = Node(30) 
root.right.left = Node(36) 

print "\n\t\t Inorder Tree Traversal\n"
inorder(root) 

# Static variable pre for function fixPrevPtr 
fixPrevPtr.pre = None
head = BTToDLL(root) 

print "\n\n\t\tDLL Traversal\n"
printList(head) 

# This code is contributed by Nikhil Kumar Singh(nickzuck_007) 

```

## C＃

```

// C# program to convert BTT to DLL using  
// simple inorder traversal  
using System; 

class GFG 
{ 
public class node 
{ 
    public int data; 
    public node left, right; 

    public node(int data) 
    { 
        this.data = data; 
    } 
} 

public static node prev; 

// Changes left pointers to work as previous  
// pointers in converted DLL The function  
// simply does inorder traversal of Binary  
// Tree and updates left pointer using  
// previously visited node  
public static void fixPrevptr(node root) 
{ 
    if (root == null) 
    { 
        return; 
    } 

    fixPrevptr(root.left); 
    root.left = prev; 
    prev = root; 
    fixPrevptr(root.right); 

} 

// Changes right pointers to work  
// as next pointers in converted DLL  
public static node fixNextptr(node root) 
{ 
    // Find the right most node in  
    // BT or last node in DLL  
    while (root.right != null) 
    { 
        root = root.right; 
    } 

    // Start from the rightmost node, traverse  
    // back using left pointers. While traversing,  
    // change right pointer of nodes  
    while (root != null && root.left != null) 
    { 
        node left = root.left; 
        left.right = root; 
        root = root.left; 
    } 

    // The leftmost node is head of  
    // linked list, return it  
    return root; 
} 

public static node BTTtoDLL(node root) 
{ 
    prev = null; 

    // Set the previous pointer  
    fixPrevptr(root); 

    // Set the next pointer and  
    // return head of DLL  
    return fixNextptr(root); 
} 

// Traverses the DLL from left tor right  
public static void printlist(node root) 
{ 
    while (root != null) 
    { 
        Console.Write(root.data + " "); 
        root = root.right; 
    } 
} 

// Standard Inorder traversal of tree  
public static void inorder(node root) 
{ 
    if (root == null) 
    { 
        return; 
    } 
    inorder(root.left); 
    Console.Write(root.data + " "); 
    inorder(root.right); 
} 

public static void Main() 
{ 
    // Let us create the tree  
    // shown in above diagram  
    node root = new node(10); 
    root.left = new node(12); 
    root.right = new node(15); 
    root.left.left = new node(25); 
    root.left.right = new node(30); 
    root.right.left = new node(36); 

    Console.WriteLine("Inorder Tree Traversal"); 
    inorder(root); 

    node head = BTTtoDLL(root); 

    Console.WriteLine("\nDLL Traversal"); 
    printlist(head); 
} 
} 

// This code is contributed by Shrikant13 

```

**Output:**

```
                Inorder Tree Traversal

        25      12      30      10      36      15

                DLL Traversal

        25      12      30      10      36      15
```

时间复杂度：O（n），其中n是给定二叉树中的节点数。 该解决方案仅对所有二叉树节点进行两次遍历。

本文由 **Bala** 提供。 如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论

注意读者！ 现在不要停止学习。 通过 [**DSA自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的DSA概念，并为行业做好准备。