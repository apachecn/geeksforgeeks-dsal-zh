# 在二叉树中计数对，其总和等于给定值 x

给定一个包含 **n** 个不同数字和值 **x** 的二叉树。 问题在于在给定的二叉树中对它们的总和等于给定值 **x** 的对进行计数。

**示例：**

```
Input : 
        5      
       / \      
      3   7      
     / \ / \  
    2  4 6  8   

        x = 10

Output : 3
The pairs are (3, 7), (2, 8) and (4, 6).

```

**1）天真的方法：**通过任何一种树遍历方法逐一获取二叉树的每个节点。 将节点 **temp** ，树的**根**和值 **x** 传递给另一个函数，例如 **findPair（）**。 在功能中，借助**根**指针再次遍历树。 将这些节点与 **temp** 逐一求和，并检查 sum == x。 如果是这样，则递增**计数**。 计算计数=计数/ 2，因为通过上述方法已对一对进行了两次计数。

## C++

```cpp

// C++ implementation to count pairs in a binary tree 
// whose sum is equal to given value x 
#include <bits/stdc++.h> 
using namespace std; 

// structure of a node of a binary tree 
struct Node { 
    int data; 
    Node *left, *right; 
}; 

// function to create and return a node 
// of a binary tree 
Node* getNode(int data) 
{ 
    // allocate space for the node 
    Node* new_node = (Node*)malloc(sizeof(Node)); 

    // put in the data 
    new_node->data = data; 
    new_node->left = new_node->right = NULL; 
} 

// returns true if a pair exists with given sum 'x' 
bool findPair(Node* root, Node* temp, int x) 
{ 
    // base case 
    if (!root) 
        return false; 

    // pair exists 
    if (root != temp && ((root->data + temp->data) == x)) 
        return true; 

    // find pair in left and right subtress 
    if (findPair(root->left, temp, x) || findPair(root->right, temp, x)) 
        return true; 

    // pair does not exists with given sum 'x' 
    return false; 
} 

// function to count pairs in a binary tree 
// whose sum is equal to given value x 
void countPairs(Node* root, Node* curr, int x, int& count) 
{ 
    // if tree is empty 
    if (!curr) 
        return; 

    // check whether pair exists for current node 'curr' 
    // in the binary tree that sum up to 'x' 
    if (findPair(root, curr, x)) 
        count++; 

    // recursively count pairs in left subtree 
    countPairs(root, curr->left, x, count); 

    // recursively count pairs in right subtree 
    countPairs(root, curr->right, x, count); 
} 

// Driver program to test above 
int main() 
{ 
    // formation of binary tree 
    Node* root = getNode(5); /*        5      */
    root->left = getNode(3); /*       / \      */
    root->right = getNode(7); /*    3   7      */
    root->left->left = getNode(2); /*   / \ / \   */
    root->left->right = getNode(4); /*   2 4 6 8   */
    root->right->left = getNode(6); 
    root->right->right = getNode(8); 

    int x = 10; 
    int count = 0; 

    countPairs(root, root, x, count); 
    count = count / 2; 

    cout << "Count = " << count; 

    return 0; 
} 

```

## Java

```java

// Java implementation to count pairs in a binary tree 
// whose sum is equal to given value x 
import java.util.*; 

class GFG 
{ 

// structure of a node of a binary tree 
static class Node  
{ 
    int data; 
    Node left, right; 
}; 
static int count; 

// function to create and return a node 
// of a binary tree 
static Node getNode(int data) 
{ 
    // allocate space for the node 
    Node new_node = new Node(); 

    // put in the data 
    new_node.data = data; 
    new_node.left = new_node.right = null; 
    return new_node; 
} 

// returns true if a pair exists with given sum 'x' 
static boolean findPair(Node root, Node temp, int x) 
{ 
    // base case 
    if (root==null) 
        return false; 

    // pair exists 
    if (root != temp && ((root.data + temp.data) == x)) 
        return true; 

    // find pair in left and right subtress 
    if (findPair(root.left, temp, x) ||  
           findPair(root.right, temp, x)) 
        return true; 

    // pair does not exists with given sum 'x' 
    return false; 
} 

// function to count pairs in a binary tree 
// whose sum is equal to given value x 
static void countPairs(Node root, Node curr, int x) 
{ 
    // if tree is empty 
    if (curr == null) 
        return; 

    // check whether pair exists for current node 'curr' 
    // in the binary tree that sum up to 'x' 
    if (findPair(root, curr, x)) 
        count++; 

    // recursively count pairs in left subtree 
    countPairs(root, curr.left, x); 

    // recursively count pairs in right subtree 
    countPairs(root, curr.right, x); 
} 

// Driver code 
public static void main(String[] args) 
{ 
    // formation of binary tree 
    Node root = getNode(5); /*     5     */
    root.left = getNode(3); /*     / \     */
    root.right = getNode(7); /* 3 7     */
    root.left.left = getNode(2); /* / \ / \ */
    root.left.right = getNode(4); /* 2 4 6 8 */
    root.right.left = getNode(6); 
    root.right.right = getNode(8); 

    int x = 10; 
    count = 0; 

    countPairs(root, root, x); 
    count = count / 2; 

    System.out.print("Count = " + count); 
} 
} 

// This code is contributed by PrinciRaj1992 

```

## Python3

```py

# Python3 implementation to count pairs in a binary tree 
# whose sum is equal to given value x 

# structure of a node of a binary tree 
class getNode(object): 
    def __init__(self, value): 
        self.data = value 
        self.left = None
        self.right = None

# returns True if a pair exists with given sum 'x' 
def findPair(root, temp, x): 
    # base case 
    if root == None: 
        return False

    # pair exists 
    if (root != temp and ((root.data + temp.data) == x)): 
        return True

    # find pair in left and right subtress 
    if (findPair(root.left, temp, x) or findPair(root.right, temp, x)): 
        return True

    # pair does not exists with given sum 'x' 
    return False

# function to count pairs in a binary tree 
# whose sum is equal to given value x 
def countPairs(root, curr, x): 
    global count 

    # if tree is empty 
    if curr == None: 
        return

    # check whether pair exists for current node 'curr' 
    # in the binary tree that sum up to 'x' 
    if (findPair(root, curr, x)): 
        count += 1

    # recursively count pairs in left subtree 
    countPairs(root, curr.left, x) 

    # recursively count pairs in right subtree 
    countPairs(root, curr.right, x) 

# Driver program to test above 
# formation of binary tree 
root = getNode(5)     
root.left = getNode(3)  
root.right = getNode(7)  
root.left.left = getNode(2)  
root.left.right = getNode(4) 
root.right.left = getNode(6) 
root.right.right = getNode(8) 
x = 10
count = 0

countPairs(root, root, x) 
count = count // 2

print("Count =", count) 

# This code is contributed by shubhamsingh10 

```

## C#

```cs

// C# implementation to count pairs in a binary tree 
// whose sum is equal to given value x 
using System; 

class GFG 
{ 

// structure of a node of a binary tree 
class Node  
{ 
    public int data; 
    public Node left, right; 
}; 
static int count; 

// function to create and return a node 
// of a binary tree 
static Node getNode(int data) 
{ 
    // allocate space for the node 
    Node new_node = new Node(); 

    // put in the data 
    new_node.data = data; 
    new_node.left = new_node.right = null; 
    return new_node; 
} 

// returns true if a pair exists with given sum 'x' 
static bool findPair(Node root, Node temp, int x) 
{ 
    // base case 
    if (root == null) 
        return false; 

    // pair exists 
    if (root != temp && ((root.data + temp.data) == x)) 
        return true; 

    // find pair in left and right subtress 
    if (findPair(root.left, temp, x) ||  
        findPair(root.right, temp, x)) 
        return true; 

    // pair does not exists with given sum 'x' 
    return false; 
} 

// function to count pairs in a binary tree 
// whose sum is equal to given value x 
static void countPairs(Node root, Node curr, int x) 
{ 
    // if tree is empty 
    if (curr == null) 
        return; 

    // check whether pair exists for current node 'curr' 
    // in the binary tree that sum up to 'x' 
    if (findPair(root, curr, x)) 
        count++; 

    // recursively count pairs in left subtree 
    countPairs(root, curr.left, x); 

    // recursively count pairs in right subtree 
    countPairs(root, curr.right, x); 
} 

// Driver code 
public static void Main(String[] args) 
{ 
    // formation of binary tree 
    Node root = getNode(5); /*     5     */
    root.left = getNode(3); /*     / \     */
    root.right = getNode(7); /* 3 7     */
    root.left.left = getNode(2); /* / \ / \ */
    root.left.right = getNode(4); /* 2 4 6 8 */
    root.right.left = getNode(6); 
    root.right.right = getNode(8); 

    int x = 10; 
    count = 0; 

    countPairs(root, root, x); 
    count = count / 2; 

    Console.Write("Count = " + count); 
} 
} 

// This code is contributed by Rajput-Ji 

```

**输出：**

```
Count = 3

```

时间复杂度：O（n ^ 2）。

**2）高效方法：**以下是步骤：

1.  将给定的二叉树转换为双向链表。 请参阅此帖子的[。](https://www.geeksforgeeks.org/convert-a-given-binary-tree-to-doubly-linked-list-set-4/)
2.  对在步骤 1 中获得的双向链表进行排序。请参阅此帖子中的[。](https://www.geeksforgeeks.org/merge-sort-for-doubly-linked-list/)
3.  计数对以加倍等于“ x”的双链排序。 请参阅此帖子的[。](https://www.geeksforgeeks.org/find-pairs-given-sum-doubly-linked-list/)
4.  显示在步骤 4 中获得的计数。

## C++

```cpp

// C++ implementation to count pairs in a binary tree 
// whose sum is equal to given value x 
#include <bits/stdc++.h> 
using namespace std; 

// structure of a node of a binary tree 
struct Node { 
    int data; 
    Node *left, *right; 
}; 

// function to create and return a node 
// of a binary tree 
Node* getNode(int data) 
{ 
    // allocate space for the node 
    Node* new_node = (Node*)malloc(sizeof(Node)); 

    // put in the data 
    new_node->data = data; 
    new_node->left = new_node->right = NULL; 
} 

// A simple recursive function to convert a given 
// Binary tree to Doubly Linked List 
// root     --> Root of Binary Tree 
// head_ref --> Pointer to head node of created 
// doubly linked list 
void BToDLL(Node* root, Node** head_ref) 
{ 
    // Base cases 
    if (root == NULL) 
        return; 

    // Recursively convert right subtree 
    BToDLL(root->right, head_ref); 

    // insert root into DLL 
    root->right = *head_ref; 

    // Change left pointer of previous head 
    if (*head_ref != NULL) 
        (*head_ref)->left = root; 

    // Change head of Doubly linked list 
    *head_ref = root; 

    // Recursively convert left subtree 
    BToDLL(root->left, head_ref); 
} 

// Split a doubly linked list (DLL) into 2 DLLs of 
// half sizes 
Node* split(Node* head) 
{ 
    Node *fast = head, *slow = head; 
    while (fast->right && fast->right->right) { 
        fast = fast->right->right; 
        slow = slow->right; 
    } 
    Node* temp = slow->right; 
    slow->right = NULL; 
    return temp; 
} 

// Function to merge two sorted doubly linked lists 
Node* merge(Node* first, Node* second) 
{ 
    // If first linked list is empty 
    if (!first) 
        return second; 

    // If second linked list is empty 
    if (!second) 
        return first; 

    // Pick the smaller value 
    if (first->data < second->data) { 
        first->right = merge(first->right, second); 
        first->right->left = first; 
        first->left = NULL; 
        return first; 
    } 
    else { 
        second->right = merge(first, second->right); 
        second->right->left = second; 
        second->left = NULL; 
        return second; 
    } 
} 

// Function to do merge sort 
Node* mergeSort(Node* head) 
{ 
    if (!head || !head->right) 
        return head; 
    Node* second = split(head); 

    // Recur for left and right halves 
    head = mergeSort(head); 
    second = mergeSort(second); 

    // Merge the two sorted halves 
    return merge(head, second); 
} 

// Function to count pairs in a sorted doubly linked list 
// whose sum equal to given value x 
int pairSum(Node* head, int x) 
{ 
    // Set two pointers, first to the beginning of DLL 
    // and second to the end of DLL. 
    Node* first = head; 
    Node* second = head; 
    while (second->right != NULL) 
        second = second->right; 

    int count = 0; 

    // The loop terminates when either of two pointers 
    // become NULL, or they cross each other (second->right 
    // == first), or they become same (first == second) 
    while (first != NULL && second != NULL && first != second && second->right != first) { 
        // pair found 
        if ((first->data + second->data) == x) { 
            count++; 

            // move first in forward direction 
            first = first->right; 

            // move second in backward direction 
            second = second->left; 
        } 
        else { 
            if ((first->data + second->data) < x) 
                first = first->right; 
            else
                second = second->left; 
        } 
    } 

    return count; 
} 

// function to count pairs in a binary tree 
// whose sum is equal to given value x 
int countPairs(Node* root, int x) 
{ 
    Node* head = NULL; 
    int count = 0; 

    // Convert binary tree to 
    // doubly linked list 
    BToDLL(root, &head); 

    // sort DLL 
    head = mergeSort(head); 

    // count pairs 
    return pairSum(head, x); 
} 

// Driver program to test above 
int main() 
{ 
    // formation of binary tree 
    Node* root = getNode(5); /*        5      */
    root->left = getNode(3); /*       / \      */
    root->right = getNode(7); /*    3   7      */
    root->left->left = getNode(2); /*   / \ / \   */
    root->left->right = getNode(4); /*   2 4 6 8   */
    root->right->left = getNode(6); 
    root->right->right = getNode(8); 

    int x = 10; 

    cout << "Count = "
         << countPairs(root, x); 

    return 0; 
} 

```

## Java

```java

// Java implementation to count pairs  
// in a binary tree whose sum is equal to 
// given value x 
class GFG  
{ 

    // structure of a node of a binary tree 
    static class Node  
    { 
        int data; 
        Node left, right; 
    }; 

    static Node head_ref; 

    // function to create and return a node 
    // of a binary tree 
    static Node getNode(int data)  
    { 
        // allocate space for the node 
        Node new_node = new Node(); 

        // put in the data 
        new_node.data = data; 
        new_node.left = new_node.right = null; 
        return new_node; 
    } 

    // A simple recursive function to convert  
    // a given Binary tree to Doubly Linked List 
    // root -. Root of Binary Tree 
    // head_ref -. Pointer to head node of created 
    // doubly linked list 
    static void BToDLL(Node root)  
    { 
        // Base cases 
        if (root == null) 
            return; 

        // Recursively convert right subtree 
        BToDLL(root.right); 

        // insert root into DLL 
        root.right = head_ref; 

        // Change left pointer of previous head 
        if (head_ref != null) 
            head_ref.left = root; 

        // Change head of Doubly linked list 
        head_ref = root; 

        // Recursively convert left subtree 
        BToDLL(root.left); 
    } 

    // Split a doubly linked list (DLL)  
    // into 2 DLLs of half sizes 
    static Node split(Node head) 
    { 
        Node fast = head, slow = head; 
        while (fast.right != null &&  
               fast.right.right != null)  
        { 
            fast = fast.right.right; 
            slow = slow.right; 
        } 
        Node temp = slow.right; 
        slow.right = null; 
        return temp; 
    } 

    // Function to merge two sorted  
    // doubly linked lists 
    static Node merge(Node first, Node second) 
    { 
        // If first linked list is empty 
        if (first == null) 
            return second; 

        // If second linked list is empty 
        if (second == null) 
            return first; 

        // Pick the smaller value 
        if (first.data < second.data)  
        { 
            first.right = merge(first.right, 
                                second); 
            first.right.left = first; 
            first.left = null; 
            return first; 
        }  
        else
        { 
            second.right = merge(first,  
                                 second.right); 
            second.right.left = second; 
            second.left = null; 
            return second; 
        } 
    } 

    // Function to do merge sort 
    static Node mergeSort(Node head) 
    { 
        if (head == null || head.right == null) 
            return head; 
        Node second = split(head); 

        // Recur for left and right halves 
        head = mergeSort(head); 
        second = mergeSort(second); 

        // Merge the two sorted halves 
        return merge(head, second); 
    } 

    // Function to count pairs in a sorted  
    // doubly linked list whose sum equal  
    // to given value x 
    static int pairSum(Node head, int x) 
    { 
        // Set two pointers, first to the beginning  
        // of DLL and second to the end of DLL. 
        Node first = head; 
        Node second = head; 
        while (second.right != null) 
            second = second.right; 

        int count = 0; 

        // The loop terminates when either of two pointers 
        // become null, or they cross each other (second.right 
        // == first), or they become same (first == second) 
        while (first != null && second != null && 
               first != second && second.right != first) 
        { 
            // pair found 
            if ((first.data + second.data) == x) 
            { 
                count++; 

                // move first in forward direction 
                first = first.right; 

                // move second in backward direction 
                second = second.left; 
            }  
            else
            { 
                if ((first.data + second.data) < x) 
                    first = first.right; 
                else
                    second = second.left; 
            } 
        } 
        return count; 
    } 

    // function to count pairs in a binary tree 
    // whose sum is equal to given value x 
    static int countPairs(Node root, int x)  
    { 
        head_ref = null; 

        // Convert binary tree to 
        // doubly linked list 
        BToDLL(root); 

        // sort DLL 
        head_ref = mergeSort(head_ref); 

        // count pairs 
        return pairSum(head_ref, x); 
    } 

    // Driver Code 
    public static void main(String[] args)  
    { 
        // formation of binary tree 
        Node root = getNode(5); /* 5 */
        root.left = getNode(3); /* / \ */
        root.right = getNode(7); /* 3 7 */
        root.left.left = getNode(2); /* / \ / \ */
        root.left.right = getNode(4); /* 2 4 6 8 */
        root.right.left = getNode(6); 
        root.right.right = getNode(8); 

        int x = 10; 

        System.out.print("Count = " +  
                countPairs(root, x)); 
    } 
} 

// This code is contributed by Rajput-Ji 

```

## C#

```cs

// C# implementation to count pairs  
// in a binary tree whose sum is  
// equal to the given value x 
using System; 

class GFG  
{ 

    // structure of a node of a binary tree 
    class Node  
    { 
        public int data; 
        public Node left, right; 
    }; 

    static Node head_ref; 

    // function to create and return a node 
    // of a binary tree 
    static Node getNode(int data)  
    { 
        // allocate space for the node 
        Node new_node = new Node(); 

        // put in the data 
        new_node.data = data; 
        new_node.left = new_node.right = null; 
        return new_node; 
    } 

    // A simple recursive function to convert  
    // a given Binary tree to Doubly Linked List 
    // root -. Root of Binary Tree 
    // head_ref -. Pointer to head node of  
    // created doubly linked list 
    static void BToDLL(Node root)  
    { 
        // Base cases 
        if (root == null) 
            return; 

        // Recursively convert right subtree 
        BToDLL(root.right); 

        // insert root into DLL 
        root.right = head_ref; 

        // Change left pointer of previous head 
        if (head_ref != null) 
            head_ref.left = root; 

        // Change head of Doubly linked list 
        head_ref = root; 

        // Recursively convert left subtree 
        BToDLL(root.left); 
    } 

    // Split a doubly linked list (DLL)  
    // into 2 DLLs of half sizes 
    static Node split(Node head) 
    { 
        Node fast = head, slow = head; 
        while (fast.right != null &&  
               fast.right.right != null)  
        { 
            fast = fast.right.right; 
            slow = slow.right; 
        } 
        Node temp = slow.right; 
        slow.right = null; 
        return temp; 
    } 

    // Function to merge two sorted  
    // doubly linked lists 
    static Node merge(Node first, 
                      Node second) 
    { 
        // If first linked list is empty 
        if (first == null) 
            return second; 

        // If second linked list is empty 
        if (second == null) 
            return first; 

        // Pick the smaller value 
        if (first.data < second.data)  
        { 
            first.right = merge(first.right, 
                                second); 
            first.right.left = first; 
            first.left = null; 
            return first; 
        }  
        else
        { 
            second.right = merge(first,  
                                 second.right); 
            second.right.left = second; 
            second.left = null; 
            return second; 
        } 
    } 

    // Function to do merge sort 
    static Node mergeSort(Node head) 
    { 
        if (head == null || head.right == null) 
            return head; 
        Node second = split(head); 

        // Recur for left and right halves 
        head = mergeSort(head); 
        second = mergeSort(second); 

        // Merge the two sorted halves 
        return merge(head, second); 
    } 

    // Function to count pairs in a sorted  
    // doubly linked list whose sum equal  
    // to given value x 
    static int pairSum(Node head, int x) 
    { 
        // Set two pointers, first to the beginning  
        // of DLL and second to the end of DLL. 
        Node first = head; 
        Node second = head; 
        while (second.right != null) 
            second = second.right; 

        int count = 0; 

        // The loop terminates when either of  
        // two pointers become null, or they  
        // cross each other (second.right == first), 
        // or they become same (first == second) 
        while (first != null && second != null && 
               first != second && second.right != first) 
        { 
            // pair found 
            if ((first.data + second.data) == x) 
            { 
                count++; 

                // move first in forward direction 
                first = first.right; 

                // move second in backward direction 
                second = second.left; 
            }  
            else
            { 
                if ((first.data + second.data) < x) 
                    first = first.right; 
                else
                    second = second.left; 
            } 
        } 
        return count; 
    } 

    // function to count pairs in a binary tree 
    // whose sum is equal to given value x 
    static int countPairs(Node root, int x)  
    { 
        head_ref = null; 

        // Convert binary tree to 
        // doubly linked list 
        BToDLL(root); 

        // sort DLL 
        head_ref = mergeSort(head_ref); 

        // count pairs 
        return pairSum(head_ref, x); 
    } 

    // Driver Code 
    public static void Main(String[] args)  
    { 
        // formation of binary tree 
        Node root = getNode(5);         /* 5 */
        root.left = getNode(3);         /* / \ */
        root.right = getNode(7);     /* 3 7 */
        root.left.left = getNode(2); /* / \ / \ */
        root.left.right = getNode(4); /* 2 4 6 8 */
        root.right.left = getNode(6); 
        root.right.right = getNode(8); 

        int x = 10; 

        Console.Write("Count = " +  
                countPairs(root, x)); 
    } 
} 

// This code is contributed by Rajput-Ji 

```

**输出：**

```
Count = 3

```

时间复杂度：O（nLog n）。

**3）另一种有效的方法–无需转换为 DLL 和排序：**以下是步骤：

1.  以任何顺序（前/后/中）遍历树。
2.  创建一个空哈希，并继续在当前节点的值和 X 之间添加差异。
3.  在每个节点上，检查其值是否在哈希中，如果是，则将计数增加 1，并且请勿在哈希中将该节点的值与 X 的差相加，以避免重复计算单个对。

```

# Python program to Count pairs  
# in a binary tree whose sum is  
# equal to a given value x 

# Node class to represent a 
# node in the binary tree  
# with value, left and right attributes 
class Node(object): 
    def __init__(self, value, left = None, right = None): 
        self.value = value 
        self.left = left 
        self.right = right 

# To store count of pairs 
count = 0

# To store difference between  
# current node's value and x, 
# acts a lookup for counting pairs 
hash_t = set() 

# The input, we need to count  
# pairs whose sum is equal to x 
x = 10

# Function to count number of pairs 
# Does a pre-order traversal of the tree 
def count_pairs_w_sum(root): 
    # global count 
    if root: 
        if root.value in hash_t: 
            count += 1
        else: 
            hash_t.add(x-root.value) 

        count_pairs_w_sum(root.left) 
        count_pairs_w_sum(root.right) 

# Entry point / Driver - Create a  
# binary tree and call the function  
# to get the count 
if __name__ == '__main__': 
    root = Node(5) 

    root.left = Node(3) 
    root.right = Node(7) 

    root.left.left = Node(2) 
    root.left.right = Node(4) 

    root.right.left = Node(6) 
    root.right.right = Node(8) 

    count_pairs_w_sum(root) 

    print count 

```

输出：

```
Count = 3

```

时间复杂度：O（n）
空间复杂度：O（n）



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。