# 已排序DLL到平衡BST的就地转换

给定一个双向链接列表，该列表具有按升序排序的数据成员。 构造一个[平衡二进制搜索树](https://www.geeksforgeeks.org/how-to-determine-if-a-binary-tree-is-balanced/)，该树的数据成员与给定的双链表相同。 该树必须就地构建（不应为树转换分配新节点）

**示例：**

```
Input:  Doubly Linked List 1  2  3
Output: A Balanced BST 
     2   
   /  \  
  1    3 

Input: Doubly Linked List 1  2 3  4 5  6  7
Output: A Balanced BST
        4
      /   \
     2     6
   /  \   / \
  1   3  4   7  

Input: Doubly Linked List 1  2  3  4
Output: A Balanced BST
      3   
    /  \  
   2    4 
 / 
1

Input:  Doubly Linked List 1  2  3  4  5  6
Output: A Balanced BST
      4   
    /   \  
   2     6 
 /  \   / 
1   3  5   

```

双链表转换非常类似于[这个单链表问题](https://www.geeksforgeeks.org/sorted-linked-list-to-balanced-bst/)，并且方法1与[先前文章](https://www.geeksforgeeks.org/sorted-linked-list-to-balanced-bst/)的方法1完全相同。 方法2也几乎相同。 方法2的唯一区别是，我们没有重复为BST分配新节点，而是重用了相同的DLL节点。 我们将上一个指针用作左侧，将下一个指针用作右侧。

**方法1（简单）**
下面是一个简单的算法，我们首先找到列表的中间节点，并将其设为要构建的树的根。

```
1) Get the Middle of the linked list and make it root.
2) Recursively do same for left half and right half.
       a) Get the middle of left half and make it left child of the root
          created in step 1.
       b) Get the middle of right half and make it right child of the
          root created in step 1.

```

时间复杂度：O（nLogn）其中n是链表中的节点数。

**方法2（棘手）**
方法1构造了从根到叶的树。 在这种方法中，我们从叶到根进行构建。 想法是按照与出现在“双向链接列表”中的顺序相同的顺序在BST中插入节点，以便可以以O（n）时间复杂度构造树。 我们首先计算给定链接列表中的节点数。 让计数为n。 在计数节点之后，我们取左n / 2个节点并递归构造左子树。 构造左子树后，我们将中间节点分配给根，并将左子树与根链接。 最后，我们递归构造正确的子树并将其与根链接。
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

| `#include <bits/stdc++.h>``using` `namespace` `std;``/* A Doubly Linked List node that``will also be used as a tree node */``class` `Node ``{ ` `public` `:` `int` `data; ` `// For tree, next pointer can be` `// used as right subtree pointer ` `Node* next; ` `// For tree, prev pointer can be` `// used as left subtree pointer ` `Node* prev; ``}; ``// A utility function to count nodes in a Linked List ``int` `countNodes(Node *head); ``Node* sortedListToBSTRecur(Node **head_ref,` `int` `n); ``/* This function counts the number of ``nodes in Linked List and then calls ``sortedListToBSTRecur() to construct BST */``Node* sortedListToBST(Node *head) `[HT G339] `{ ` `/*Count the number of nodes in Linked List */` `int` `n = countNodes(head); ` `/* Construct BST */` `return` `sortedListToBSTRecur(&head, n); ``} ``/* The main function that constructs ``balanced BST and returns root of it. ``head_ref --> Pointer to pointer to``head node of Doubly linked list ``n --> No. of nodes in the Doubly Linked List */``Node* sortedListToBSTRecur(Node **head_ref,` `int` `n) ``{ ` `/* Base Case */` `if` `(n <= 0) ` `return` `NULL; ` `/* Recursively construct the left subtree */` `Node *left = sortedListToBSTRecur(head_ref, n/2); ` `/* head_ref now refers to middle node,` ] `make middle node as root of BST*/` `Node *root = *head_ref; ` `// Set pointer to left subtree `[H TG90] `root->prev = left; ` `/* Change head pointer of Linked List` `for parent recursive calls */` `*head_ref = (*head_ref)->next; ` `/* Recursively construct the right ` `subtree and link it with root ` `The number of nodes in right subtree`]  `is total nodes - nodes in ` `left subtree - 1 (for root) */` `root->next = sortedListToBSTRecur(head_ref, n-n/2-1); ` `return` `root; ``} ``/* UTILITY FUNCTIONS */``/* A utility function that returns ``count of nodes in a given Linked List */``int` `countNodes(Node *head) ``{ ` `int` `count = 0; ` `Node *temp = head; ` `while` `(temp) ` `{ ` `temp = temp->next; ` `count++; ` `} ` `return` `count; ``} ``/* Function to insert a node at ``the beginging of the Doubly Linked List */``void` `push(Node** head_ref,` `int` `new_data) ``{ ` `/* allocate node */` `Node* new_node =` `new` `Node();` `/* put in the data */` `new_node->data = new_data; ` `/* since we are adding at the beginning, ` `prev is always NULL */` ] `new_node->prev = NULL; ` [ `/* link the old list off the new node */` `new_node->next = (*head_ref); ` `/* change prev of head node to new node */` `if` `((*head_ref) != NULL) ` `(*head_ref)->prev = new_node ; `[HTG4 95]  `/* move the head to point to the new node */` `(*head_ref) = new_node; ``} `的`/* Function to print nodes in a given linked list */``void` `printList(Node *node) ``{ ` `while` `(node!=NULL) ` `{ ` `cout<<node->data<<` `" "` `; ` `node = node->next; ` `} `[`} ``/* A utility function to print``preorder traversal of BST */``void` `preOrder(Node* node) ``{ ` `if` `(node == NULL) ` `return` `; ` `cout<<node->data<<` `" "` `; ` `preOrder(node->prev); ` `preOrder(node->next); ``} `[HT G229]`/* Driver code*/``int` `main() ``{ ` `/* Start with the empty list */` `Node* head = NULL; ` `/* Let us create a sorted linked list to test the functions ` `Created linked list will be 7->6->5->4->3->2->1 */` `push(&head, 7); ` `push(&head, 6); ` `push(&head, 5); ` `push(&head, 4); ` `push(&head, 3); ` `push(&head, 2); ` `push(&head, 1); ` `cout<<` `"Given Linked List\n"` `; ` `printList(head); ` `/* Convert List to BST */` `Node *root = sortedListToBST(head); ` `cout<<`​​ `"\nPreOrder Traversal of constructed BST \n "` `; ` `preOrder(root); `[H TG276] `return` `0; ``} ``// This code is contributed by rathbhupendra` |

*chevron_right**filter_none*