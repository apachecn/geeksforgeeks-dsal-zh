# 检查两个链表是否是字谜

> 原文:[https://www . geesforgeks . org/check-two-linked-list-is-or-anagram/](https://www.geeksforgeeks.org/check-whether-two-linked-lists-are-anagrams-or-not/)

给定链表形式的两个字符串，任务是检查一个字符串是否是另一个字符串的 [**字谜**](https://en.wikipedia.org/wiki/Anagram) 。如果是，打印**是**，否则打印**否**。

**示例:**

> **输入:**
> 链表 1 = T->R->I->A->N->G->L->E->NULL
> 链表 2 = I->N->T->E->G->R->A->L->NULL
> T5】输出:【T0
> 
> **输入:**
> 链表 1 = S->I->L->E->N->T->NULL
> 链表 2 = L->I->S->T->E->N->NULL
> T5】输出:是

**方法:**这个问题可以通过对链表进行排序，然后检查两者是否相同来解决。如果排序后它们是相同的，那么它们就是字谜。否则，它们不是。现在按照以下步骤解决这个问题:

1.  使用冒泡排序对两个链表进行排序。
2.  现在，从头开始遍历这两个链表，并匹配每个对应的节点。
3.  如果对应的两个节点不同，则打印**否**返回。
4.  循环结束后最后打印**是**。

下面是上述方法的实现:

## C++14

```
// C++ program for the above approach
#include <iostream>
using namespace std;

// Structure for a node
struct Node {
    int data;
    Node* next;
} Node;

// Function to swap the nodes
struct Node* swap(struct Node* ptr1, 
                  struct Node* ptr2)
{
    struct Node* tmp = ptr2->next;
    ptr2->next = ptr1;
    ptr1->next = tmp;
    return ptr2;
}

// Function to sort the list
void bubbleSort(struct Node*** head, 
                int count)
{
    struct Node** h;
    int i, j, swapped;

    for (i = 0; i <= count; i++) {

        h = *head;
        swapped = 0;

        for (j = 0; j < count - i - 1; 
             j++) {

            struct Node* p1 = *h;
            struct Node* p2 = p1->next;

            if (p1->data > p2->data) {

                // Update the link 
                // after swapping
                *h = swap(p1, p2);
                swapped = 1;
            }

            h = &(*h)->next;
        }

        // Break if the loop ended 
        // without any swap
        if (swapped == 0)
            break;
    }
}

// Function to insert a struct Node
// at the end of a linked list
void insert(struct Node*** head, int data)
{
    struct Node* ptr = new struct Node();

    ptr->data = data;
    ptr->next = NULL;
    if (**head == NULL) {
        **head = ptr;
    }
    else {
        struct Node* ptr1 = **head;
        while (ptr1->next != NULL) {
            ptr1 = ptr1->next;
        }
        ptr1->next = ptr;
    }
}

// Function to check if both strings 
// are anagrams or not
bool checkAnagram(struct Node** head1, 
                  struct Node** head2,
                  int N, int M)
{

    // Sort the linked list
    bubbleSort(&head1, N);
    bubbleSort(&head2, M);

    struct Node* ptr1 = *head1;
    struct Node* ptr2 = *head2;
    int flag = 0;
    while (ptr1 != NULL) {
        if (ptr1->data == ptr2->data) {
            ptr1 = ptr1->next;
            ptr2 = ptr2->next;
        }
        else {
            return 0;
        }
    }

    // If one of the linked list
    // doesn't end
    if (!ptr1 and !ptr2) {
        return 1;
    }

    return 0;
}

// Function to create linked lists
// from the strings
void createLinkedList(struct Node** head1,
                      struct Node** head2, 
                      string s1, string s2)
{

    int N = s1.size();
    int M = s2.size();

    // Create linked list from the array s1
    for (int i = 0; i < N; i++) {
        insert(&head1, s1[i]);
    }

    // Create linked list from the array s2
    for (int i = 0; i < M; i++) {
        insert(&head2, s2[i]);
    }
}

// Driver Code
int main()
{
    string s1 = "TRIANGLE";
    string s2 = "INTEGRAL";

    int N = s1.size(), M = s2.size();

    // start with empty linked list
    struct Node* head1 = NULL;
    struct Node* head2 = NULL;

    createLinkedList(&head1, &head2, s1, s2);

    if (checkAnagram(&head1, &head2, N, M))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

**Output**

```
Yes
```

***时间复杂度:***O(N<sup>2</sup>)
***辅助空间:*** O(1)