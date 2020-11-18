# 链接列表到平衡BST

给定一个单链列表，其中的数据成员按升序排序。 构造一个[平衡二进制搜索树](https://www.geeksforgeeks.org/how-to-determine-if-a-binary-tree-is-balanced/)，该树的数据成员与给定的链接列表相同。
 **范例：**

```
Input:  Linked List 1->2->3
Output: A Balanced BST 
     2   
   /  \  
  1    3 

Input: Linked List 1->2->3->4->5->6->7
Output: A Balanced BST
        4
      /   \
     2     6
   /  \   / \
  1   3  5   7  

Input: Linked List 1->2->3->4
Output: A Balanced BST
      3   
    /  \  
   2    4 
 / 
1

Input:  Linked List 1->2->3->4->5->6
Output: A Balanced BST
      4   
    /   \  
   2     6 
 /  \   / 
1   3  5   

```

**方法1（简单）**
下面是一个简单的算法，在该算法中，我们首先找到列表的中间节点，并将其设为要构建的树的根。

```
1) Get the Middle of the linked list and make it root.
2) Recursively do same for the left half and right half.
       a) Get the middle of the left half and make it left child of the root
          created in step 1.
       b) Get the middle of right half and make it the right child of the
          root created in step 1.

```

时间复杂度：O（nLogn）其中n是链表中的节点数。

**方法2（棘手）**
方法1从根到叶构造树。 在这种方法中，我们从叶到根进行构建。 想法是按照与在“链表”中出现的顺序相同的顺序在BST中插入节点，以便可以以O（n）时间复杂度构造树。 我们首先计算给定链接列表中的节点数。 让计数为n。 在计数节点之后，我们取左n / 2个节点并递归构造左子树。 构造左子树后，我们为root分配内存，并将左子树与root链接。 最后，我们递归构造正确的子树并将其与根链接。
在构造BST时，我们还不断将列表头指针移到next位置，以便在每个递归调用中都有适当的指针。

下面是方法2的实现。突出显示了创建Balanced BST的主要代码。

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ implementation of above approach``#include <bits/stdc++.h>``using` `namespace` `std;``/* Link list node */``class` `LNode ``{ ` `public` `:` `int` `data; ` `LNode* next; ``}; ``/* A Binary Tree node */``class` `TNode ``{ ` `public` `:` `int` `data; ` `TNode* left; ` `TNode* right; ``}; ``TNode* newNode(` `int` `data); ``int` `countLNodes(LNode *head); ``TNode* sortedListToBSTRecur(LNode **head_ref,` `int` `n); ``/* This function counts the number of` [HTG35 1]`nodes in Linked List and then calls ``sortedListToBSTRecur() to construct BST */``TNode* sortedListToBST(LNode *head) ``{ ` `/*Count the number of nodes in Linked List */` `int` `n = countLNodes(head); ` `/* Construct BST */` `return` `sortedListToBSTRecur(&head, n); ``} ``/* The main function that constructs ``balanced BST and returns root of it. ``head_ref --> Pointer to pointer to ``head node of linked list n --> No.``of nodes in Linked List */``TNode* sortedListToBSTRecur(LNode **head_ref,` `int` `n) ``{ ` `/* Base Case */` `if` `(n <= 0) ` `return` `NULL; ` `/* Recursively construct the left subtree */` `TNode *left = sortedListToBSTRecur(head_ref, n/2); ` `/* Allocate memory for root, and ` `link the above constructed left ` `subtree with root */` `TNode *root = newNode((*head_ref)->data); ` `root->left = left; ` `/* Change head pointer of Linked List` `for parent recursive calls */` `*head_ref = (*head_ref)->next; ` `/* Recursively construct the right ` ] `subtree and link it with root ` `The number of nodes in right subtree` `is total nodes - nodes in ` `left subtree - 1 (for root) which is n-n/2-1*/` `root->right = sortedListToBSTRecur(head_ref, n - n / 2 - 1); ` `return` `root; ``} ``/* UTILITY FUNCTIONS */``/* A utility function that returns ``count of nodes in a given Linked List */`]`int` `countLNodes(LNode *head) ``{ ` `int` `count = 0; `[HTG1 35] `LNode *temp = head; ` `while` `(temp) ` `{ ` `temp = temp->next; ` `count++; ` `} ` `return` `count; ``} ` [`/* Function to insert a node ``at the beginging of the linked list */``void` `push(LNode** head_ref,` `int` `new_data) ``{ ` `/* allocate node */` `LNode* new_node =` `new` `LNode();` `/* put in the data */` `new_node->data = new_data; ` `/* link the old list off the new node */` `new_node->next = (*head_ref); ` ] `/* move the head to point to the new node */` `(*head_ref) = new_node; ``} `[H`/* Function to print nodes in a given linked list */``void` `printList(LNode *node) ``{ ` `while` `(node!=NULL) ` `{ ` `cout << node->data <<` `" "` `; ` `node = node->next; ` `} ``} ``/* Helper function that allocates a new node with the ``given data and NULL left and right pointers. */``TNode* newNode(` `int` `data) ``{ ` `TNode* node =` `new` `TNode();` `node->data = data; ` `node->left = NULL; ` `node->right = NULL; ` `return` `node; ``} ``/* A utility function to ``print preorder traversal of BST */``void` `preOrder(TNode* node) ``{ ` `if` `(node == NULL) ` `return` `; ` `cout<<node->data<<` `" "` `; ` `preOrder(node->left); ` `preOrder(node->right); ``} ``/* Driver code*/``int` `main() ``{ ` `/* Start with the empty list */` `LNode* head = NULL; ` `/* Let us create a sorted linked list to test the functions ` `Created linked list will be 1->2->3->4->5->6->7 */` `push(&head, 7); `]  `push(&head, 6); ` `push(&head, 5); ` `push(&head, 4); ` `push(&head, 3); ` `push(&head, 2); `​​ `push(&head, 1); ` `cout<<` `"Given Linked List "` `; ` `printList(head); ` `/* Convert List to BST */` `TNode *root = sortedListToBST(head); ` `cout<<` `"\nPreOrder Traversal of constructed BST "` `; ` `preOrder(root); ` [ `return` `0; ``} ``// This code is contributed by rathbhupendra` |

*chevron_right**filter_none*