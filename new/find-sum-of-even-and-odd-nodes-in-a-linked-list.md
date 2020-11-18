# 在链表

中查找偶数和奇数节点的总和

给定一个链表，任务是在其中分别查找偶数和奇数节点的总和。

**示例：**

> **输入：** 1-> 2-> 3-> 4-> 5-> 6-> 7
> **输出：**
> 偶数和= 12
> 奇数和= 16
> 
> **输入：** 5-> 7-> 8-> 10-> 15
> **输出：**
> 偶数= 18
> 赔率总和= 27

**方法：**遍历整个链表以及每个节点：

1.  如果元素是偶数，那么我们将该元素添加到保存偶数元素之和的变量中。
2.  如果元素是奇数，那么我们将该元素添加到保存奇数元素之和的变量中。

下面是上述方法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ implementation of the approach``#include <iostream>``using` `namespace` `std;``// Represents node of the linked list``struct` `Node {` `int` `data;` `Node* next;``};``// Function to insert a node at the``// end of the linked list``void` `insert(Node** root,` `int` `item)``{` `Node *ptr = *root, *temp =` `new` `Node;` `temp->data = item;` `temp->next = NULL;` [ `if` `(*root == NULL)` `*root = temp;` `else` `{` `while` `(ptr->next != NULL)` `ptr = ptr->next;` `ptr->next = temp;` `}``}``// Function to print the sum of even``// and odd nodes of the linked lists``void` `evenOdd(Node* root)``{` `int` `odd = 0, even = 0;` `Node* ptr = root;` `while` `(ptr != NULL) {`的 `// If current node's data is even` `if` `(ptr->data % 2 == 0)` `even += ptr->data;`的 `// If current node's data is odd` `else` `odd += ptr->data;` `// ptr now points to the next node` `ptr = ptr->next;` `}` `cout <<` `"Even Sum = "` `<< even << endl;` `cout <<` `"Odd Sum = "` `<< odd << endl;``}``// Driver code` [`int` `main()``{` `Node* root = NULL;` `insert(&root, 1);` `insert(&root, 2);` `insert(&root, 3);` `insert(&root, 4);` `insert(&root, 5);` `insert(&root, 6);` `insert(&root, 7);` `evenOdd(root);` `return` `0;``}` |

*chevron_right**filter_none*