# 检查给定的链表中是否存在一个字符串作为子序列

> 原文:[https://www . geeksforgeeks . org/check-if-a-string-presented-in-给定的链表作为子序列/](https://www.geeksforgeeks.org/check-if-a-string-is-present-in-the-given-linked-list-as-a-subsequence/)

给定一个大小为 **N** 的字符串 **S** 和一个**链表**，任务是检查链表是否包含一个字符串作为子序列。如果包含子序列，则打印**是**，否则打印**否**。

**示例:**

> **输入:** S =“坏”，链表:b - > r - > a - > d - >空
> T3】输出:是
> 
> **输入:** S =“坏”，链表:a->p->p->l->e->NULL
> **输出:**否

**方法:**这个问题可以用**两个指针**解决，一个在字符串上，一个在链表上。现在，按照以下步骤解决这个问题:

1.  创建变量 **i** ，并用 0 初始化。另外，创建一个指向链表头部的指针**曲线**。
2.  现在，运行一段时间循环，直到 I 小于 **N** 并且 **cur** 不是 **NULL** 为止，并且在每次迭代中:
    1.  检查 S[i]是否等于节点 **cur** 中的数据。如果是增量 **i** 到 **(i+1)** ，移动 **cur** 到下一个节点。
    2.  如果不是，那么只移动**曲线**到下一个节点。
3.  如果循环结束，则检查 **i** 是否变为 **N** 。如果是，则打印**是**，否则打印**否**

下面是上述方法的实现:

## C++

```
// C++ code for the above approach

#include <bits/stdc++.h>
using namespace std;

// Node of Linked List
class Node {
public:
    char data;
    Node* next;

    Node(char d)
    {
        data = d;
        next = NULL;
    }
};

// Function to check if the linked list contains
// a string as a subsequence
bool checkSub(Node* head, string S)
{
    Node* cur = head;
    int i = 0, N = S.size();

    while (i < N and cur) {
        if (S[i] == cur->data) {
            i += 1;
        }
        cur = cur->next;
    }

    if (i == N) {
        return 1;
    }
    return 0;
}

// Driver Code
int main()
{
    Node* head = new Node('b');
    head->next = new Node('r');
    head->next->next = new Node('a');
    head->next->next->next = new Node('d');

    string S = "bad";

    if (checkSub(head, S)) {
        cout << "Yes";
    }
    else {
        cout << "No";
    }
}
```

**Output**

```
Yes
```

**时间复杂度:**O(N)
T3】辅助空间: O(1)