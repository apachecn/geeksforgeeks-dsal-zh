# 使用链表对给定字符数组进行排序

> 原文:[https://www . geesforgeks . org/排序-给定字符-数组-使用-链表/](https://www.geeksforgeeks.org/sorting-given-character-array-using-linked-list/)

给定一个包含小写英文字母 **N** 的数组 **arr[]** ，任务是使用链表对这个数组 **arr[]** 进行排序。

**示例:**

> **输入:**arr[]=[‘b’、【c】、【d】、【e】、【f】、【b】、【b】、【a】、【a】**输出:**【a】>【a】>【b】>【b】>【b】>【b】
> 
> **输入:**arr[]=【g】、【e】、【k】、【s】、【f】、【r】、【g】、【e】、【k】、【s】、
> **输出:**【e】>【e】>【e】>【f】>

**方法:**要解决这个问题，首先从字符数组创建链表。链表形成后，使用[冒泡排序](https://www.geeksforgeeks.org/bubble-sort-for-linked-list-by-swapping-nodes/)进行排序。

下面是上述方法的实现:

## C++

```
#include <iostream>
using namespace std;

// Structure for a node
struct Node {
    int data;
    Node* next;
} Node;

// Function to swap the nodes
struct Node* swap(struct Node* ptr1, struct Node* ptr2)
{
    struct Node* tmp = ptr2->next;
    ptr2->next = ptr1;
    ptr1->next = tmp;
    return ptr2;
}

// Function to sort the list
int bubbleSort(struct Node** head, int count)
{
    struct Node** h;
    int i, j, swapped;

    for (i = 0; i <= count; i++) {

        h = head;
        swapped = 0;

        for (j = 0; j < count - i - 1; j++) {

            struct Node* p1 = *h;
            struct Node* p2 = p1->next;

            if (p1->data > p2->data) {

                // Update the link after swapping
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

// Function to print the list
void printList(struct Node* n)
{
    while (n != NULL) {
        cout << char(n->data) << " -> ";
        n = n->next;
    }
    cout << endl;
}

// Function to insert a struct Node
// at the end of a linked list
void insert(struct Node** head, int data)
{
    struct Node* ptr = new struct Node();

    ptr->data = data;
    ptr->next = NULL;
    if (*head == NULL) {
        *head = ptr;
    }
    else {
        struct Node* ptr1 = *head;
        while (ptr1->next != NULL) {
            ptr1 = ptr1->next;
        }
        ptr1->next = ptr;
    }
}

// Driver Code
int main()
{
    int arr[] = { 'b', 'b', 'c', 'c', 'd', 'e',
                  'f', 'b', 'b', 'a', 'a' };
    int list_size, i;

    // start with empty linked list
    struct Node* start = NULL;
    list_size = sizeof(arr) / sizeof(arr[0]);

    // Create linked list from the array arr[]
    for (i = 0; i < list_size; i++)
        insert(&start, arr[i]);

    // sort the linked list
    bubbleSort(&start, list_size);

    // Print list after sorting
    printList(start);

    return 0;
}
```

**Output**

```
a -> a -> b -> b -> b -> b -> c -> c -> d -> e -> f -> 
```

**时间复杂度:** O(N <sup>2</sup> )