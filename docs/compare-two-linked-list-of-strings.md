# 比较两个字符串链表

> 原文:[https://www . geesforgeks . org/compare-two-link-list-of-strings/](https://www.geeksforgeeks.org/compare-two-linked-list-of-strings/)

给定两个[链表](https://www.geeksforgeeks.org/data-structures/linked-list/)**和 **L2** ，其中每个节点存储一个字符串。任务是检查组合所有节点的字符串是否相似。**

****示例:****

> ****输入:**L1 =[“He”、“llo”、“wor”、“LD”]，
> L2 =[“H”、“e”、“ll”、“owo”、“r”、“LD”]
> **输出:**真
> **说明:**两个列表组成了“Helloworld”的字符串。**
> 
> ****输入:**L1 =【“w”、“o”、“l”、“d”】、
> L2 =【“wo”、“d”、“rl”】
> T4】输出:假
> T7】解释: L1 造“世界”但 L2 造“wodrl”二者不同。**
> 
>  ****输入:**L1 =[“w”、“”、“orl”、“d”]、
> L2 =[“worl”、“”、“”、“”、“”、“d”]
> T4】输出:真
> T7】说明:两个列表都组成了“世界”的字符串。**

****天真的做法:**这是简单的做法。遍历这两个列表，并将它们的值存储在另一个字符串中，如果相等，则比较这两个字符串，否则返回 false。**

**下面是上述方法的实现。**

## **C++**

```
// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

// Structure of Node of linked list
class Node {
public:
    string s;
    Node* next;
    Node(string s)
    {
        this->s = s;
        next = NULL;
    }
};

// Function to compare if two linkedlists
// are similar or not
bool compare(Node* list1, Node* list2)
{
    // Declare string variables to store 
    // the strings formed from the linked lists
    string s1, s2;

    while (list1 != NULL) {
        s1 += list1->s;
        list1 = list1->next;
    }
    while (list2 != NULL) {
        s2 += list2->s;
        list2 = list2->next;
    }
    return s1 == s2;
}

// Driver Code
int main()
{
    Node* n1 = new Node("w");
    Node* head1 = n1;
    Node* n2 = new Node("");
    Node* n3 = new Node("orl");
    Node* n4 = new Node("d");
    Node* n5 = new Node("worl");
    Node* head2 = n5;
    Node* n6 = new Node("");
    Node* n7 = new Node("");
    Node* n8 = new Node("nd");
    n1->next = n2;
    n2->next = n3;
    n3->next = n4;
    n5->next = n6;
    n6->next = n7;
    n7->next = n8;

    if (compare(head1, head2) == true)
        cout << "true";
    else
        cout << "false";
    return 0;
}
```

****Output**

```
false
```** 

*****时间复杂度:*** O(N+M)，其中 N 和 M 是字符串的长度。
***辅助空间:*** O(N+M)**

****高效进场:**这个问题可以用[两点进场](https://www.geeksforgeeks.org/two-pointers-technique/)解决。按照以下步骤解决给定的问题。**

*   **遍历两个列表，同时为字符保留两个指针**。****
*   ****分别比较每个字符。如果不同，返回**假**否则，继续比较。****
*   ****如果指针的值变成节点中字符串的大小，则移动到下一个节点。****
*   ****重复上述步骤，直到节点不变成**空值**。****

****下面是上述方法的实现。****

## ****C++****

```
**// C++ program for above approach
#include <bits/stdc++.h>
using namespace std;

// Structure of Node of a linked list
class Node {
public:
    string s;
    Node* next;
    Node(string s)
    {
        this->s = s;
        next = NULL;
    }
};

// Compare function
bool compare(Node* list1, Node* list2)
{
    int i = 0, j = 0;

    while (list1 != NULL && list2 != NULL) {
        while (i < list1->s.size() && 
               j < list2->s.size()) {
            if (list1->s[i] != list2->s[j])
                return false;
            i++;
            j++;
        }
        if (i == list1->s.size()) {
            i = 0;
            list1 = list1->next;
        }
        if (j == list2->s.size()) {
            j = 0;
            list2 = list2->next;
        }
    }
    return list1 == NULL && list2 == NULL;
}

// Driver Code
int main()
{
    Node* n1 = new Node("w");
    Node* head1 = n1;
    Node* n2 = new Node("");
    Node* n3 = new Node("orl");
    Node* n4 = new Node("d");
    Node* n5 = new Node("worl");
    Node* head2 = n5;
    Node* n6 = new Node("");
    Node* n7 = new Node("");
    Node* n8 = new Node("nd");
    n1->next = n2;
    n2->next = n3;
    n3->next = n4;
    n5->next = n6;
    n6->next = n7;
    n7->next = n8;

    if (compare(head1, head2) == true)
        cout << "true";
    else
        cout << "false";
    return 0;
}**
```

******Output**

```
false
```**** 

*******时间复杂度:*** O(N+M)，其中 N 和 M 是字符串的长度。
***辅助空间*** : O(1)。****