# 从给定数组

创建链接列表

给定大小为 **N** 的数组 **arr []** 。 任务是从给定数组创建链接列表。

**示例：**

```
Input : arr[]={1, 2, 3, 4, 5}
Output : 1->2->3->4->5

Input :arr[]={10, 11, 12, 13, 14}
Output : 10->11->12->13->14

```

**简单方法：**对于数组 **arr []** 的每个元素，我们在链接列表中创建一个节点，并将其插入到末尾。

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `#include <iostream>``using` `namespace` `std;``// Representation of a node``struct` `Node {` `int` `data;` `Node* next;``};`的`// Function to insert node``void` `insert(Node** root,` `int` `item)``{` `Node* temp =` `new` `Node;` `Node* ptr;` `temp->data = item;` `temp->next = NULL;`] `if` `(*root == NULL)` `*root = temp;` `else` `{` `ptr = *root;` `while` `(ptr->next != NULL)` `ptr = ptr->next;` `ptr->next = temp;` `}`[H TG162] `}``void` `display(Node* root)``{` `while` `(root != NULL) {` `cout << root->data <<` `" "` `;` `root = root->next;` `}``}``Node *arrayToList(` `int` `arr[],` `int` `n)``{` `Node *root = NULL;` `for` `(` `int` `i = 0; i < n; i++)` `insert(&root, arr[i]);` `return` `root;``}``// Driver code``int` `main()``{`] `int` `arr[] = { 1, 2, 3, 4, 5 };` `int` `n =` `sizeof` `(arr) /` `sizeof` `(arr[0]);` [ `Node* root = arrayToList(arr, n);` [HTG2 09] `display(root);` `return` `0;``}` |

*chevron_right**filter_none*