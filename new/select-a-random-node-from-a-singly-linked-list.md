# 从单链接列表中选择一个随机节点

给定一个单链列表，请从链列表中选择一个随机节点（如果列表中有N个节点，则选择一个节点的概率应为1 / N）。 您将获得一个随机数生成器。

以下是一个简单的解决方案
1）通过遍历列表来计算节点数。
2）再次遍历列表，并以1 / N的概率选择每个节点。 可以通过为第i个节点生成一个从0到N-i的随机数，然后仅在生成的数字等于0（或从0到N-i的任何其他固定数）的情况下选择第i个节点来完成选择。

通过以上方案，我们得到了统一的概率。

```
i = 1, probability of selecting first node = 1/N
i = 2, probability of selecting second node =
                   [probability that first node is not selected] * 
                   [probability that second node is selected]
                  = ((N-1)/N)* 1/(N-1)
                  = 1/N  
```

同样，其他选择其他节点的概率为1 / N

上述解决方案需要两次遍历链接列表。

**如何选择只允许一个遍历的随机节点？**
这个想法是使用[储层采样](https://www.geeksforgeeks.org/reservoir-sampling/)。 以下是步骤。 这是[储层采样](https://www.geeksforgeeks.org/reservoir-sampling/)的简单版本，因为我们只需要选择一个键即可，而不是k个键。

```
(1) Initialize result as first node
   result = head->key 
(2) Initialize n = 2
(3) Now one by one consider all nodes from 2nd node onward.
    (3.a) Generate a random number from 0 to n-1\. 
         Let the generated random number is j.
    (3.b) If j is equal to 0 (we could choose other fixed number 
          between 0 to n-1), then replace result with current node.
    (3.c) n = n+1
    (3.d) current = current->next
```

下面是上述算法的实现。

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `/* C++ program to randomly select a node from a singly``linked list */``#include<stdio.h>``#include<stdlib.h>``#include <time.h>``#include<iostream>``using` `namespace` `std;``/* Link list node */``class` `Node``{` `public` `:` `int` `key;` `Node* next;` `void` `printRandom(Node*);` `void` `push(Node**,` `int` `);``};``// A reservoir sampling based function to print a``// random node from a linked list``void` `Node::printRandom(Node *head)``{` `// IF list is empty` `if` `(head == NULL)` `return` `;` `// Use a different seed value so that we don't get` `// same result each time we run this program` `srand` `(` `time` `(NULL));` [ `// Initialize result as first node` `int` `result = head->key;` `// Iterate from the (k+1)th element to nth element` `Node *current = head;` `int` `n;` `for` `(n = 2; current != NULL; n++)` `{` `// change result with probability 1/n` `if` `(` `rand` `() % n == 0)` `result = current->key;`​​ `// Move to next node` `current = current->next;` `}` `cout<<` `"Randomly selected key is \n"` `<< result;``}``/* BELOW FUNCTIONS ARE JUST UTILITY TO TEST */` [`/* A utility function to create a new node */``Node* newNode(` `int` `new_key)``{` `// allocate node ` `Node* new_node = (Node*)` `malloc` `(` `sizeof` `( Node));` `/// put in the key ` `new_node->key = new_key;` `new_node->next = NULL;` `return` `new_node;``}``/* A utility function to insert a node at the beginning``of linked list */``void` `Node:: push(Node** head_ref,` `int` `new_key)``{` `/* allocate node */` `Node* new_node =` `new` `Node;` `/* put in the key */` `new_node->key = new_key;` HTG337]  `new_node->next = (*head_ref);` `/* move the head to point to the new node */` `(*head_ref) = new_node;``}``// Driver program to test above functions``int` `main()``{` `Node n1;` ] `Node *head = NULL;` `n1.push(&head, 5);` `n1.push(&head, 20);` `n1.push(&head, 4);` `n1.push(&head, 3);` `n1.push(&head, 30);` `n1.printRandom(head);` `return` `0;``}``// This code is contributed by SoumikMondal` |

*chevron_right**filter_none*