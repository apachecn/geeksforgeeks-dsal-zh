# 检查带有循环的链表是否为回文

给定一个带有循环的链表，任务是查找它是否是回文。 您无权删除循环。
![](img/de522899e01a1322ab2808eeff1ad73e.png)

例子：

```
Input : 1 -> 2 -> 3 -> 2
             /|\      \|/
               ------- 1  
Output: Palindrome
Linked list is 1 2 3 2 1 which is a 
palindrome.

Input : 1 -> 2 -> 3 -> 4
             /|\      \|/
               ------- 1  
Output: Not Palindrome
Linked list is 1 2 3 4 1 which is a 
not palindrome.

```

算法：

1.  使用弗洛伊德循环检测算法检测环路。
2.  然后按照[和](https://www.geeksforgeeks.org/detect-and-remove-loop-in-a-linked-list/)中的讨论找到循环的起始节点
3.  如[和](https://www.geeksforgeeks.org/function-to-check-if-a-singly-linked-list-is-palindrome/)中所述，检查链表是否是回文

下面是实现。

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ program to check if a linked list with``// loop is palindrome or not.``#include<bits/stdc++.h>``using` `namespace` `std;` [`/* Link list node */``struct` `Node``{` `int` `data;` `struct` `Node * next;``};``/* Function to find loop starting node.``loop_node --> Pointer to one of the loop nodes``head --> Pointer to the start node of the linked list */``Node* getLoopstart(Node *loop_node, Node *head)``{` `Node *ptr1 = loop_node;` `Node *ptr2 = loop_node;` [ `// Count the number of nodes in loop` `unsigned` `int` `k = 1, i;` `while` `(ptr1->next != ptr2)` `{` `ptr1 = ptr1->next;` `k++;` `}` ［HTG337］ ［HTG338］ ［HTG47］ ［HTG48］ ［HTG339］ ［HTG340］ ［HTG49］ ［HTG50］ ［HTG341］ ［HTG342］ ［HTG51］ ［HTG343］ ［HTG344］ ［HTG52］ ［HTG53］ ［HTG345 ] `ptr2 = head;` `for` `(i = 0; i < k; i++)` `ptr2 = ptr2->next;`的 `/* Move both pointers at the same pace,` `they will meet at loop starting node */` `while` `(ptr2 != ptr1)` `{` `ptr1 = ptr1->next;` `ptr2 = ptr2->next;` `}` `return` `ptr1;``}``/* This function detects and find loop starting` `node  in the list*/``Node* detectAndgetLoopstarting(Node *head)``{` `Node *slow_p = head, *fast_p = head,*loop_start;` `//Start traversing list and detect loop` `while` `(slow_p && fast_p && fast_p->next)` [H TG389] `{` `slow_p = slow_p->next;` `fast_p = fast_p->next->next;` `/* If slow_p and fast_p meet then find` `the loop starting node*/` `if` `(slow_p == fast_p)` `{` `loop_start = getLoopstart(slow_p, head);` `break` `;` `}` `}` `// Return starting node of loop` `return` `loop_start;``}``// Utility function to check if a linked list with loop``// is palindrome with given starting point.``bool` `isPalindromeUtil(Node *head, Node* loop_start)``{` `Node *ptr = head;` `stack<` `int` `> s;` `// Traverse linked list until last node is equal` [HTG4 39] `// to loop_start and store the elements till start` `// in a stack` `int` `count = 0;` `while` `(ptr != loop_start &#124;&#124; count != 1)` `{` `s.push(ptr->data);` `if` `(ptr == loop_start)` `count = 1;` `ptr = ptr->next;` `}` `ptr = head;` `count = 0;` `// Traverse linked list until last node is` `// equal to loop_start second time` `while` `(ptr != loop_start &#124;&#124; count != 1)` `{` `// Compare data of node with the top of stack` `// If equal then continue` `if` `(ptr->data == s.top())` `s.pop();` `// Else return false` `else` `return` `false` `;` `if` `(ptr == loop_start)` `count = 1;` `ptr = ptr->next;` `}` ] `// Return true if linked list is palindrome` `return` `true` `;``}``// Function to find if linked list is palindrome or not``bool` `isPalindrome(Node* head)``{` `// Find the loop starting node` `Node* loop_start = detectAndgetLoopstarting(head);` ［HTG521］ ［HTG522］ ［HTG225］ ［HTG226］ ［HTG523］ ［HTG524］ ［HTG227］ ［HTG228］ ［HTG229］ ［HTG525］ ［HTG526］ ［HTG230］ ［HTG527］ ［HTG528］ ［HTG231］ ［HTG529 ]`Node *newNode(` `int` `key)``{` `Node *temp =` `new` `Node;` `temp->data = key;` `temp->next = NULL;` `return` `temp;``}` [`/* Driver program to test above function*/``int` `main()``{` `Node *head = newNode(50);` `head->next = newNode(20);` `head->next->next = newNode(15);` `head->next->next->next = newNode(20);` `head->next->next->next->next = newNode(50);` `/* Create a loop for testing */` `head->next->next->next->next->next = head->next->next;` `isPalindrome(head)? cout <<` ] `"\nPalindrome"` `: cout <<` `"\nNot Palindrome"` `;` `return` `0;`[`}` |

*chevron_right**filter_none*