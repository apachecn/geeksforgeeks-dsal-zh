# 链表

的替代排序

给定一个包含 **n** 个节点的链表。 问题是要重新排列列表中的节点，以使第一节点中的数据为第一最小值，第二节点为第一最大值，第三节点为第二最小值，第四节点为第二最大值，依此类推。

例子：

```
Input : list: 4->1->3->5->2
Output : 1->5->2->4->3

Input : list: 10->9->8->7->6->5
Output : 5->10->6->9->7->8

```

**方法：**以下是步骤：

1.  使用[合并排序](https://www.geeksforgeeks.org/merge-sort-for-linked-list/)技术对链接列表进行排序。
2.  将列表分为**前**和**后**列表。 请参阅此帖子的 **FrontBackProcedure** 。
3.  现在，将**返回**列表。 请参阅此帖子的[。](https://www.geeksforgeeks.org/reverse-a-linked-list/)
4.  最后，以交替顺序将**的节点首先**和**的列表合并回**列表。

```

// C++ implementation of alternative sorting 
// of the Linked list 
#include <bits/stdc++.h> 

using namespace std; 

// node of a linked list 
struct Node { 
    int data; 
    struct Node* next; 
}; 

// function to get a new node 
Node* getNode(int data) 
{ 
    // allocate space for node 
    Node* newNode = (Node*)malloc(sizeof(Node)); 

    // put in the data 
    newNode->data = data; 
    newNode->next = NULL; 

    return newNode; 
} 

// Split the nodes of the given list into front and  
// back halves, and return the two lists using the  
// reference parameters. If the length is odd, the  
// extra node should go in the front list. Uses the  
// fast/slow pointer strategy. 
void FrontBackSplit(Node* source, 
                    Node** frontRef, Node** backRef) 
{ 
    Node* fast; 
    Node* slow; 
    if (source == NULL || source->next == NULL) { 
        // length < 2 cases 
        *frontRef = source; 
        *backRef = NULL; 
    } 
    else { 
        slow = source; 
        fast = source->next; 

        // Advance 'fast' two nodes, and 
        // advance 'slow' one node 
        while (fast != NULL) { 
            fast = fast->next; 
            if (fast != NULL) { 
                slow = slow->next; 
                fast = fast->next; 
            } 
        } 

        // 'slow' is before the midpoint in the list, 
        // so split it in two at that point. 
        *frontRef = source; 
        *backRef = slow->next; 
        slow->next = NULL; 
    } 
} 

// function to merge two sorted lists in 
// sorted order 
Node* SortedMerge(Node* a, Node* b) 
{ 
    Node* result = NULL; 

    // Base cases 
    if (a == NULL) 
        return b; 
    else if (b == NULL) 
        return a; 

    // Pick either a or b, and recur 
    if (a->data <= b->data) { 
        result = a; 
        result->next = SortedMerge(a->next, b); 
    } 
    else { 
        result = b; 
        result->next = SortedMerge(a, b->next); 
    } 

    return result; 
} 

// sorts the linked list by changing 
// next pointers (not data) 
void MergeSort(Node** headRef) 
{ 
    Node* head = *headRef; 
    Node *a, *b; 

    // Base case -- length 0 or 1 
    if ((head == NULL) || (head->next == NULL)) 
        return; 

    // Split head into 'a' and 'b' sublists 
    FrontBackSplit(head, &a, &b); 

    // Recursively sort the sublists 
    MergeSort(&a); 
    MergeSort(&b); 

    // merge the two sorted lists together 
    *headRef = SortedMerge(a, b); 
} 

// function to reverse the linked list 
static void reverse(Node** head_ref) 
{ 
    Node* prev = NULL; 
    Node* current = *head_ref; 
    Node* next; 

    while (current != NULL) { 
        next = current->next; 
        current->next = prev; 
        prev = current; 
        current = next; 
    } 

    *head_ref = prev; 
} 

// function to alternately merge two lists 
void alternateMerge(Node* head1, Node* head2) 
{ 
    Node *p, *q; 
    while (head1 != NULL && head2 != NULL) { 

        // merging nodes alternately by 
        // making the desired links 
        p = head1->next; 
        head1->next = head2; 
        head1 = p; 
        q = head2->next; 
        head2->next = head1; 
        head2 = q; 
    } 
} 

// function for alternative sort of the 
// linked list 
Node* altSortForLinkedList(Node* head) 
{ 
    // sort the linked list 
    MergeSort(&head); 

    Node *front, *back; 

    // Split head into 'front' and 'back' sublists 
    FrontBackSplit(head, &front, &back); 

    // reversing the 'back' list 
    reverse(&back); 

    // merging the nodes of 'front' and 'back' 
    // lists alternately 
    alternateMerge(front, back); 

    // required head of final list 
    return front; 
} 

// Function to print nodes in 
// a given linked list 
void printList(Node* head) 
{ 
    while (head != NULL) { 
        cout << head->data << " "; 
        head = head->next; 
    } 
} 

// Driver program to test above 
int main() 
{ 
    // linked list: 10->9->8->7->6->5 
    Node* head = getNode(10); 
    head->next = getNode(9); 
    head->next->next = getNode(8); 
    head->next->next->next = getNode(7); 
    head->next->next->next->next = getNode(6); 
    head->next->next->next->next->next = getNode(5); 

    cout << "Original list: "; 
    printList(head); 

    head = altSortForLinkedList(head); 

    cout << "\nModified list: "; 
    printList(head); 

    return 0; 
} 

```

输出：

```
Original list: 10 9 8 7 6 5
Modified list: 5 10 6 9 7 8

```

时间复杂度：O（n * logn）。



* * *

* * *

如果您喜欢GeeksforGeeks并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至tribution@geeksforgeeks.org。 查看您的文章出现在GeeksforGeeks主页上，并帮助其他Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。