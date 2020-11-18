# 反转堆栈，而无需在O（n）中使用多余的空间

在不使用递归和多余空间的情况下反转[堆栈](https://www.geeksforgeeks.org/stack-data-structure/)。 甚至连功能堆栈都不允许。

**示例：**

```
Input : 1->2->3->4
Output : 4->3->2->1

Input :  6->5->4
Output : 4->5->6

```

我们在下面的文章中讨论了一种反转字符串的方法。

[使用递归](https://www.geeksforgeeks.org/reverse-a-stack-using-recursion/)反转堆栈

上述解决方案需要O（n）额外空间。 如果我们内部将堆栈表示为链表，则可以在O（1）时间内反转字符串。 反转堆栈需要反转链表，这可以用O（n）时间和O（1）额外空间来完成。

请注意，push（）和pop（）操作仍然需要O（1）时间。

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// CPP program to implement Stack ``// using linked list so that reverse``// can be done with O(1) extra space.``#include<bits/stdc++.h>``using` `namespace` `std;``class` `StackNode {` `public` `:` `int` `data;` `StackNode *next;` `StackNode(` `int` `data)` `{` `this` `->data = data;` `this` `->next = NULL;` `}``};``class` `Stack {` `StackNode *top;` `public` `:` `// Push and pop operations` `void` `push(` `int` `data)` `{` `if` `(top == NULL) {` `top =` `new` `StackNode(data);` `return` `;` `}` `StackNode *s =` `new` `StackNode(data);` `s->next = top;` `top = s;` `}` `StackNode* pop()`​​  `{` `StackNode *s = top;` `top = top->next;` `return` `s;` `}` `// prints contents of stack` `void` `display()` `{` `StackNode *s = top;` `while` `(s != NULL) {` [ `cout << s->data <<` `" "` `;` `s = s->next;` `}` `cout << endl;` `}` `// Reverses the stack using simple` `// linked list reversal logic.` `void` `reverse()` `{` `StackNode *prev, *cur, *succ;` `cur = prev = top;` `cur = cur->next;` `prev->next = NULL;` `while` `(cur != NULL) {` `succ = cur->next;` `cur->next = prev;` `prev = cur;` `cur = succ;` `}` `top = prev;` `}``};``// driver code``int` `main()``{` `Stack *s =` `new` `Stack();` `s->push(1);` `s->push(2);` `s->push(3);` `s->push(4);` `cout <<` `"Original Stack"` `<< endl;;` `s->display();` `cout << endl;` `// reverse` `s->reverse();` `cout <<` `"Reversed Stack"` `<< endl;` ] `s->display();` `return` `0;``}``// This code is contribute by Chhavi.`[ |

*chevron_right**filter_none*