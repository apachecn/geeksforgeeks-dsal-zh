# 幸存者围成一圈| 剑拼图的代码解决方案

给定n个人站在第一个持剑的圈子中，找到圈子中最幸运的人，如果从第一个持剑的士兵中每个都必须杀死下一个士兵并将剑移交给下一个士兵，那么该士兵将 杀死相邻的士兵，并将剑移交给下一位士兵，以使一名士兵仍在这场战争中被任何人杀死。

先决条件：[拼图81 | 一圈有100人的枪谜游戏](https://www.geeksforgeeks.org/puzzle-100-people-in-a-circle-with-gun-puzzle/)

例子 ：

> 输入：5
> 输出：3
> 说明：
> N = 5
> 士兵1 2 3 4 5（5名士兵）
> 首先是1 3 5（剩余）为2和4被杀死 分别乘以1和3。
> 在第二步3中，有5人杀死了1，第3人杀死了5名士兵3。
> 
> 输入：100
> 输出：73
> 说明：
> N = 10
> 士兵1 2 3 4 5 6 7 8 9 10（10名士兵）
> 前1 3 5 7 9为2 4 6 8 10被1 3 5 7和9杀死。
> 在第二1 5 9中以9杀死1，然后5杀死第9名士兵。
> 在第三，第五，五名士兵中还活着

**方法：**的想法是使用[循环链表](https://www.geeksforgeeks.org/circular-linked-list/)。 根据士兵N的数量创建一个循环链表。根据规则，您必须杀死相邻的士兵并将剑移交给下一个士兵，而后者又会杀死其相邻​​的士兵并将剑移交给下一个士兵。 因此，在循环链表中，相邻的士兵被杀死，其余的士兵以循环的方式互相对抗，只有一名士兵被任何人杀害而幸存。

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// CPP code to find the luckiest person``#include <bits/stdc++.h>``using` `namespace` `std;``// Node structure``struct` `Node {` `int` `data;` `struct` `Node* next;``};``Node *newNode(` `int` `data)``{` `Node *node =` `new` `Node;` `node->data = data;` `node->next = NULL;` `return` `node;``}``// Function to find the luckiest person``int` `alivesol(` `int` `Num)``{` `if` `(Num == 1)` `return` `1;` `// Create a single node circular` `// linked list.` `Node *last = newNode(1);` `last->next = last;` `for` `(` `int` `i = 2; i <= Num; i++) {` `Node *temp = newNode(i);` `temp->next = last->next;        ` `last->next = temp;` `last = temp;     ` `}` `// Starting from first soldier.` `Node *curr = last->next;` `// condition for evaluating the existence` `// of single soldier who is not killed.` `Node *temp;` `while` `(curr->next != curr) {` `temp = curr;` `curr = curr->next;` `temp->next = curr->next;` `// deleting soldier from the circular` `// list who is killed in the fight.` `delete` `curr;` [HTG1 01] `curr = temp;` `}` `// Returning the Luckiest soldier who` `// remains alive.` `int` `res = temp->data;` `delete` `temp;`的 `return` `res;``}``// Driver code``int` `main()``{` `int` `N = 100;` `cout << alivesol(N) << endl;`​​ `return` `0;``}` |

*chevron_right**filter_none*