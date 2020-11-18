# 将给定的二叉树转换为双链表| 设置4

给定二叉树（BT），将其转换为就地双链表（DLL）。 节点中的左指针和右指针分别用作转换后的DLL中的上一个指针和下一个指针。 DLL中节点的顺序必须与给定二叉树的顺序相同。 有序遍历的第一个节点（BT中最左边的节点）必须是DLL的头节点。

[![TreeToList](img/1e6723c342ed8e5706a1c58b68241a4c.png)](https://media.geeksforgeeks.org/wp-content/cdn-uploads/TreeToList.png)

下面针对此问题讨论了三种不同的解决方案。
[将给定的二叉树转换为双链表| 设置1](https://www.geeksforgeeks.org/in-place-convert-a-given-binary-tree-to-doubly-linked-list/)
[将给定的二叉树转换为双链表| 设置2](https://www.geeksforgeeks.org/convert-a-given-binary-tree-to-doubly-linked-list-set-2/)
[将给定的二叉树转换为双链表| 套装3](https://www.geeksforgeeks.org/convert-given-binary-tree-doubly-linked-list-set-3/)

在以下实现中，我们以有序方式遍历树。 我们在当前链接列表的开头添加节点，并使用指向head指针的指针更新列表的开头。 由于我们在开始时插入，因此我们需要以相反的顺序处理叶子。 对于逆序，我们首先在左子树之前遍历右子树。 即执行反向有序遍历。

## C ++

```

// C++ program to convert a given Binary Tree to Doubly Linked List 
#include <bits/stdc++.h> 

// Structure for tree and linked list 
struct Node { 
    int data; 
    Node *left, *right; 
}; 

// Utility function for allocating node for Binary 
// Tree. 
Node* newNode(int data) 
{ 
    Node* node = new Node; 
    node->data = data; 
    node->left = node->right = NULL; 
    return node; 
} 

// A simple recursive function to convert a given 
// Binary tree to Doubly Linked List 
// root    --> Root of Binary Tree 
// head --> Pointer to head node of created doubly linked list 
void BToDLL(Node* root, Node*& head) 
{ 
    // Base cases 
    if (root == NULL) 
        return; 

    // Recursively convert right subtree 
    BToDLL(root->right, head); 

    // insert root into DLL 
    root->right = head; 

    // Change left pointer of previous head 
    if (head != NULL) 
        head->left = root; 

    // Change head of Doubly linked list 
    head = root; 

    // Recursively convert left subtree 
    BToDLL(root->left, head); 
} 

// Utility function for printing double linked list. 
void printList(Node* head) 
{ 
    printf("Extracted Double Linked list is:\n"); 
    while (head) { 
        printf("%d ", head->data); 
        head = head->right; 
    } 
} 

// Driver program to test above function 
int main() 
{ 
    /* Constructing below tree  
            5  
            / \  
            3     6  
        / \     \  
        1 4     8  
        / \     / \  
        0 2     7 9 */
    Node* root = newNode(5); 
    root->left = newNode(3); 
    root->right = newNode(6); 
    root->left->left = newNode(1); 
    root->left->right = newNode(4); 
    root->right->right = newNode(8); 
    root->left->left->left = newNode(0); 
    root->left->left->right = newNode(2); 
    root->right->right->left = newNode(7); 
    root->right->right->right = newNode(9); 

    Node* head = NULL; 
    BToDLL(root, head); 

    printList(head); 

    return 0; 
} 

```

## 爪哇

```

// Java program to convert a given Binary Tree to Doubly Linked List 

/* Structure for tree and Linked List */
class Node { 
    int data; 
    Node left, right; 

    public Node(int data) 
    { 
        this.data = data; 
        left = right = null; 
    } 
} 

class BinaryTree { 
    // root    --> Root of Binary Tree 
    Node root; 

    // head --> Pointer to head node of created doubly linked list 
    Node head; 

    // A simple recursive function to convert a given 
    // Binary tree to Doubly Linked List 
    void BToDLL(Node root) 
    { 
        // Base cases 
        if (root == null) 
            return; 

        // Recursively convert right subtree 
        BToDLL(root.right); 

        // insert root into DLL 
        root.right = head; 

        // Change left pointer of previous head 
        if (head != null) 
            head.left = root; 

        // Change head of Doubly linked list 
        head = root; 

        // Recursively convert left subtree 
        BToDLL(root.left); 
    } 

    // Utility function for printing double linked list. 
    void printList(Node head) 
    { 
        System.out.println("Extracted Double Linked List is : "); 
        while (head != null) { 
            System.out.print(head.data + " "); 
            head = head.right; 
        } 
    } 

    // Driver program to test the above functions 
    public static void main(String[] args) 
    { 
        /* Constructing below tree 
               5 
             /   \ 
            3     6 
           / \     \ 
          1   4     8 
         / \       / \ 
        0   2     7   9  */

        BinaryTree tree = new BinaryTree(); 
        tree.root = new Node(5); 
        tree.root.left = new Node(3); 
        tree.root.right = new Node(6); 
        tree.root.left.right = new Node(4); 
        tree.root.left.left = new Node(1); 
        tree.root.right.right = new Node(8); 
        tree.root.left.left.right = new Node(2); 
        tree.root.left.left.left = new Node(0); 
        tree.root.right.right.left = new Node(7); 
        tree.root.right.right.right = new Node(9); 

        tree.BToDLL(tree.root); 
        tree.printList(tree.head); 
    } 
} 

// This code has been contributed by Mayank Jaiswal(mayank_24) 

```

## Python3

```

# Python3 program to convert a given Binary Tree to Doubly Linked List  
class Node: 
    def __init__(self, data): 
        self.data = data 
        self.left = self.right = None

class BinaryTree: 
    # A simple recursive function to convert a given  
    # Binary tree to Doubly Linked List  
    # root    --> Root of Binary Tree  
    # head --> Pointer to head node of created doubly linked list  
    root, head = None, None

    def BToDll(self, root: Node): 
        if root is None: 
            return

        # Recursively convert right subtree 
        self.BToDll(root.right) 

        # Insert root into doubly linked list 
        root.right = self.head 

        # Change left pointer of previous head 
        if self.head is not None: 
            self.head.left = root 

        # Change head of doubly linked list 
        self.head = root 

        # Recursively convert left subtree 
        self.BToDll(root.left) 

    @staticmethod
    def print_list(head: Node): 
        print('Extracted Double Linked list is:') 
        while head is not None: 
            print(head.data, end = ' ') 
            head = head.right 

# Driver program to test above function  
if __name__ == '__main__': 

    """ 
    Constructing below tree 
            5 
        // \\ 
        3 6 
        // \\ \\ 
        1 4 8 
    // \\ // \\ 
    0 2 7 9 
    """
    tree = BinaryTree() 
    tree.root = Node(5) 
    tree.root.left = Node(3) 
    tree.root.right = Node(6) 
    tree.root.left.left = Node(1) 
    tree.root.left.right = Node(4) 
    tree.root.right.right = Node(8) 
    tree.root.left.left.left = Node(0) 
    tree.root.left.left.right = Node(2) 
    tree.root.right.right.left = Node(7) 
    tree.root.right.right.right = Node(9) 

    tree.BToDll(tree.root) 
    tree.print_list(tree.head) 

# This code is contributed by Rajat Srivastava 

```

## C＃

```

// C# program to convert a given Binary Tree to Doubly Linked List 
using System; 

/* Structure for tree and Linked List */
public class Node { 
    public int data; 
    public Node left, right; 

    public Node(int data) 
    { 
        this.data = data; 
        left = right = null; 
    } 
} 

class GFG { 
    // root    --> Root of Binary Tree 
    public Node root; 

    // head --> Pointer to head node of created doubly linked list 
    public Node head; 

    // A simple recursive function to convert a given 
    // Binary tree to Doubly Linked List 
    public virtual void BToDLL(Node root) 
    { 
        // Base cases 
        if (root == null) 
            return; 

        // Recursively convert right subtree 
        BToDLL(root.right); 

        // insert root into DLL 
        root.right = head; 

        // Change left pointer of previous head 
        if (head != null) 
            head.left = root; 

        // Change head of Doubly linked list 
        head = root; 

        // Recursively convert left subtree 
        BToDLL(root.left); 
    } 

    // Utility function for printing double linked list. 
    public virtual void printList(Node head) 
    { 
        Console.WriteLine("Extracted Double "
                          + "Linked List is : "); 
        while (head != null) { 
            Console.Write(head.data + " "); 
            head = head.right; 
        } 
    } 

    // Driver program to test above function 
    public static void Main(string[] args) 
    { 
        /* Constructing below tree  
            5  
            / \  
            3     6  
        / \     \  
        1 4     8  
        / \     / \  
        0 2     7 9 */

        GFG tree = new GFG(); 
        tree.root = new Node(5); 
        tree.root.left = new Node(3); 
        tree.root.right = new Node(6); 
        tree.root.left.right = new Node(4); 
        tree.root.left.left = new Node(1); 
        tree.root.right.right = new Node(8); 
        tree.root.left.left.right = new Node(2); 
        tree.root.left.left.left = new Node(0); 
        tree.root.right.right.left = new Node(7); 
        tree.root.right.right.right = new Node(9); 

        tree.BToDLL(tree.root); 
        tree.printList(tree.head); 
    } 
} 

// This code is contributed by Shrikant13 

```

**输出：**

```
Extracted Double Linked list is:
0 1 2 3 4 5 6 7 8 9
```

**时间复杂度：** O（n），因为该解决方案只遍历给定的二叉树。

本文由 **Aditya Goel** 提供。 如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论。

注意读者！ 现在不要停止学习。 通过 [**DSA自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的DSA概念，并为行业做好准备。