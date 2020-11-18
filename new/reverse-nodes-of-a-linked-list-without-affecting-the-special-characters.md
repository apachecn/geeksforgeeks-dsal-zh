# 链表的反向节点而不影响特殊字符

给定一个字母和特殊字符的链接列表。 反转给定的链表，而不会影响特殊字符的位置。

**示例：**

> **输入**：g-> @-> e->＃-> e-> $-> k-> s-> NULL
> **输出**：s-> @-> k->＃-> e-> $-> e-> g-> NULL
> **解释**：在这里我们可以看到输出中特殊字符的位置不变，并且链表也相反。

想法是遍历链接列表，并将不包括特殊字符的字符存储在临时数组中。 再次遍历链表，并以相反的方式将元素从数组复制到链表的节点。

**以下是逐步算法**：

1.  取一个临时数组TEMP_ARR。
2.  遍历链接列表并执行以下操作
    *   如果当前元素是字母，则将链接列表的该元素存储到TEMP_ARR。
    *   否则，将节点指针增加一

下面是上述方法的实现：

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// CPP program to reverse a linked list`​​ `// without affecting special characters``#include <iostream>`] `using` `namespace` `std;``// Link list node ``struct` `Node {` `char` `data;` `struct` `Node* next;``};``// Function to reverse the linked list``// without affecting special characters``void` `reverse(` `struct` `Node** head_ref,` `int` `size)``{` `struct` `Node* current = *head_ref;` `char` `TEMP_ARR[size];` `int` `i = 0;` `// Traverse the linked list and insert` `// linked list elements to TEMP_ARR` `while` `(current != NULL) {` `// if the cuurent data is any alphabet than` `// store it in to TEMP_ARR` `if` `((current->data >= 97 && current->data <= 122) &#124;&#124; ` `(current->data >= 65 && current->data <= 90)) {` `TEMP_ARR[i++] = current->data;` `current = current->next;` `}` `// else increase the node position` `else` `current = current->next;` `}` `current = *head_ref;` `// Traverse the linked list again` `while` `(current != NULL) ` `{` `// if current character is an alphabet than` `// replace the current element in the linked list` `// with the last element of the TEMP_ARR` `if` `((current->data >= 97 && current->data <= 122) &#124;&#124; ` `(current->data >= 65 && current->data <= 90)) {` `current->data = TEMP_ARR[--i];` `current = current->next;` `}` [[HT G99] `// else increase the node` `else` `current = current->next;` `}``}``// Function to push a node ``void` `push(` `struct` `Node** head_ref,` `char` `new_data)``{` `/* allocate node */` `struct` `Node* new_node = (` `struct` `Node*)` `malloc` `(` `sizeof` `(` `struct` `Node));` `/* put in the data */` `new_node->data = new_data;` `/* link the old list off the new node */` `new_node->next = (*head_ref);` `/* move the head to point to the new node */` `(*head_ref) = new_node;``}``/* Function to print linked list */``void` `printList(` `struct` `Node* head)``{` `struct` `Node* temp = head;` `while` `(temp != NULL) {` `cout << temp->data;` `temp = temp->next;` `}``}``// Driver program to test above function``int` `main()``{` `/* Start with the empty list */` `struct` `Node* head = NULL;` `push(&head,` `'s'` `);` `push(&head,` `'{content}apos;` `);` `push(&head,` `'k'` `);` `push(&head,` `'e'` `);` `push(&head,` [ `'e'` `);` `push(&head,` `'@'` `);` `push(&head,` `'#'` `);` `push(&head,` `'g'` `);` `push(&head,` `'r'` `);` `push(&head,` `'o'` `);` `push(&head,` `'f'` `);` `push(&head,` `'s'` `);` `push(&head,` `'{content}apos;` `);` `push(&head,` `'k'` `);` `push(&head,` `'e'` `);` `push(&head,` `'e'` `);` `push(&head,` `'g'` `);` `cout <<` `"Given linked list: "` `;` `printList(head);` `reverse(&head, 13);`] `cout <<` `"\nReversed Linked list: "` `;` `printList(head);` `return` `0;``}` |

*chevron_right**filter_none*