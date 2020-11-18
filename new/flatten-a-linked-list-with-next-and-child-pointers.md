# 展平多级链接列表

给定一个链表，除了下一个指针外，每个节点还具有一个子指针，该子指针可以指向也可以不指向单独的列表。 这些子列表可能具有自己的一个或多个子列表，依此类推，以产生一个多级数据结构，如下图所示。 您将获得列表第一级的标题。 展平列表，以便所有节点都出现在单级链接列表中。 您需要以第一层的所有节点都应排在第一位，然后是第二层的节点在前的方式来整理列表。

每个节点都是具有以下定义的C结构。

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `struct` `List``{` `int` `data;` `struct` `List *next;` `struct` `List *child;``};` |

*chevron_right**filter_none*

[![](img/55ec5b7c1827265a492de094d7906b79.png "flattenList")](https://media.geeksforgeeks.org/wp-content/cdn-uploads/flattenList.png)

**上面的列表应转换为10- > 5- > 12- > 7- > 11- > 4- > 20- > 13- > 17- > 6- > 2- > 16- > 9- > 8- > 3- > 19- > 15** 

问题清楚地表明，我们需要逐级扁平化。 解决方案的想法是，我们从第一级开始，一个接一个地处理所有节点，如果一个节点有一个子代，那么我们将该子代追加到列表的末尾，否则我们什么也不做。 在处理完第一级后，所有下一级节点将被附加到第一级之后。 附加节点遵循相同的过程。

```
1) Take "cur" pointer, which will point to head of the fist level of the list
2) Take "tail" pointer, which will point to end of the first level of the list
3) Repeat the below procedure while "curr" is not NULL.
    I) if current node has a child then
    a) append this new child list to the "tail"
        tail->next = cur->child
    b) find the last node of new child list and update "tail"
        tmp = cur->child;
        while (tmp->next != NULL)
            tmp = tmp->next;
        tail = tmp;
    II) move to the next node. i.e. cur = cur->next 
```

以下是上述算法的实现。

## C ++

*filter_none*

*编辑*
*关闭*

*play_arrow*

*链接*
*亮度_4*
*代码*

| `// C++ Program to flatten list with``// next and child pointers ``#include <bits/stdc++.h>``using` `namespace` `std;``// Macro to find number of elements in array ``#define SIZE(arr) (sizeof(arr)/sizeof(arr[0])) ``// A linked list node has data, ``// next pointer and child pointer ``class` `Node ``{ ` `public` `:` `int` `data; ` `Node *next; ` `Node *child; ``}; ``// A utility function to create a linked list`]`// with n nodes. The data of nodes is taken ``// from arr[]. All child pointers are set as NULL ``Node *createList(` `int` `*arr,` `int` `n) ``{ ` `Node *head = NULL; ` `Node *p; ` `int` `i; ` `for` `(i = 0; i < n; ++i) ` `{ ` `if` `(head == NULL) ` `head = p =` `new` `Node();` `else` `{ ` `p->next =` `new` `Node();` `p = p->next; ` `} ` `p->data = arr[i]; ` `p->next = p->child = NULL; ` `} ` `return` `head; ``} ``// A utility function to print ``// all nodes of a linked list ``void` `printList(Node *head) ``{ ` `while` `(head != NULL) ` `{ ` `cout << head->data <<` `" "` `; ` `head = head->next; ` `} ` `cout<<endl; ``} `，`// This function creates the input ``// list. The created list is same ``// as shown in the above figure ``Node *createList(` `void` `) ``{ ` `int` `arr1[] = {10, 5, 12, 7, 11}; ` `int` `arr2[] = {4, 20, 13}; ` `int` `arr3[] = {17, 6}; ` `int` `arr4[] = {9, 8}; ` `int` `arr5[] = {19, 15}; ` `int` `arr6[] = {2}; ` `int` `arr7[] = {16}; ` `int` `arr8[] = {3}; ` `/* create 8 linked lists */` `Node *head1 = createList(arr1, SIZE(arr1)); ` `Node *head2 = createList(arr2, SIZE(arr2)); ` `Node *head3 = createList(arr3, SIZE(arr3)); ` `Node *head4 = createList(arr4, SIZE(arr4)); ` `Node *head5 = createList(arr5, SIZE(arr5)); ` `Node *head6 = createList(arr6, SIZE(arr6)); ` `Node *head7 = createList(arr7, SIZE(arr7)); ` `Node *head8 = createList(arr8, SIZE(arr8)); ` `/* modify child pointers to ` `create the list shown above */` `head1->child = head2; ` `head1->next->next->next->child = head3; ` `head3->child = head4; ` `head4->child = head5; ` `head2->next->child = head6; ` `head2->next->next->child = head7; ` `head7->child = head8; ` `/* Return head pointer of first ` `linked list. Note that all nodes are ` `reachable from head1 */` `return` `head1; ``} ``/* The main function that flattens``a multilevel linked list */`] `void` `flattenList(Node *head) ``{ ` `/*Base case*/` `if` `(head == NULL) ` `return` `; ` `Node *tmp; ` ] `/* Find tail node of first level linked list */` `Node *tail = head; ` `while` `(tail->next != NULL) ` `tail = tail->next; ` `// One by one traverse through all nodes of first level ` `// linked list till we reach the tail node ` `Node *cur = head; ` `while` `(cur != tail) ` `{ ` `// If current node has a child ` `if` `(cur->child) ` `{ ` `// then append the child at the end of current list ` `tail->next = cur->child; ` `// and update the tail to new last node ` `tmp = cur->child; ` `while` `(tmp->next) ` `tmp = tmp->next; ` `tail = tmp; ` `} ` `// Change current node `] `cur = cur->next; ` `} ``} ``// Driver code``int` `main(` `void` `) ``{ ` `Node *head = NULL; ` `head = createList(); ` `flattenList(head); ` `printList(head); `​​ `return` `0; ``} `，`// This code is contributed by rathbhupendra` |

*chevron_right**filter_none*