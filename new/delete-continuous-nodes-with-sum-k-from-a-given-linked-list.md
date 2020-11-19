# 从给定的链表

> 原文：[https://www.geeksforgeeks.org/delete-continuous-nodes-with-sum-k-from-a-given-linked-list/](https://www.geeksforgeeks.org/delete-continuous-nodes-with-sum-k-from-a-given-linked-list/)

中删除总和为 K 的连续节点。

给定[单链接列表](https://www.geeksforgeeks.org/data-structures/linked-list/singly-linked-list/)和整数 **K** ，任务是从给定的[链接中删除总和为 **K** 的所有连续节点集。 列表](http://www.geeksforgeeks.org/data-structures/linked-list/)。 删除后打印更新的链表。 如果无法进行此类删除，请打印原始的链接列表。

**示例**：

> **输入**：链接列表：1-> 2-> -3-> 3-> 1，K = 3
> **输出**：-3 -> 1
> **解释**：
> 连续和为 3 的节点为：
> 1）1-> 2
> 2）3
> 因此， 删除这些节点链的链接列表将变为：-3- > 1
> 
> **输入**：链接列表：1-> 1-> -3-> -3-> -2，K = 5
> **输出**：1-> 1-> -3-> -3-> -2
> **解释**：
> 不存在总和为 K 的连续节点

**方法**：

1.  在链接列表的开头将 Node 的值附加为零。

2.  [遍历给定的链表](https://www.geeksforgeeks.org/recursive-insertion-and-traversal-linked-list/)。

3.  在遍历期间，将节点值的总和存储到该节点，并以 [unordered_map](http://www.geeksforgeeks.org/unordered_map-in-stl-and-its-applications/) 作为当前节点的参考。

4.  如果在 **unordered_map** 中存在值**（sum – K）**的节点，则从节点中删除与存储的值**（sum – K）**对应的所有节点 映射到当前节点，并将和更新为`0`。

5.  如果在 unordered_map 中不存在**（sum – K）**值的节点，则将当前总和与节点存储在映射中。

下面是上述方法的实现：

```

// C++ program for the above approach 

#include <bits/stdc++.h> 
using namespace std; 

// A Linked List Node 
struct ListNode { 
    int val; 
    ListNode* next; 

    // Contructor 
    ListNode(int x) 
        : val(x), next(NULL) 
    { 
    } 
}; 

// Function to create Node 
ListNode* getNode(int data) 
{ 
    ListNode* temp; 
    temp = (ListNode*)malloc(sizeof(ListNode)); 
    temp->val = data; 
    temp->next = NULL; 
    return temp; 
} 

// Function to print the Linked List 
void printList(ListNode* head) 
{ 
    while (head->next) { 
        cout << head->val << " -> "; 
        head = head->next; 
    } 
    printf("%d", head->val); 
} 

// Function that removes continuos nodes 
// whose sum is K 
ListNode* removeZeroSum(ListNode* head, 
                        int K) 
{ 
    // Root node initialise to 0 
    ListNode* root = new ListNode(0); 

    // Append at the front of the given 
    // Linked List 
    root->next = head; 

    // Map to store the sum and reference 
    // of the Node 
    unordered_map<int, ListNode*> umap; 

    umap[0] = root; 

    // To store the sum while traversing 
    int sum = 0; 

    // Traversing the Linked List 
    while (head != NULL) { 

        // Find sum 
        sum += head->val; 

        // If found value with (sum - K) 
        if (umap.find(sum - K) != umap.end()) { 

            ListNode* prev = umap[sum - K]; 
            ListNode* start = prev; 

            // Delete all the node 
            // traverse till current node 
            int aux = sum; 

            // Traverse till current head 
            while (prev != head) { 
                prev = prev->next; 
                aux += prev->val; 
                if (prev != head) { 
                    umap.erase(aux); 
                } 
            } 

            // Update the start value to 
            // the next value of current head 
            start->next = head->next; 

            // Update sum to zero 
            sum = 0; 
        } 

        // If (sum - K) value not found 
        else { 
            umap[sum] = head; 
        } 

        head = head->next; 
    } 

    // Return the value of updated 
    // head node 
    return root->next; 
} 

// Driver Code 
int main() 
{ 
    // head Node 
    ListNode* head; 

    // Create Linked List 
    head = getNode(1); 
    head->next = getNode(2); 
    head->next->next = getNode(-3); 
    head->next->next->next = getNode(3); 
    head->next->next->next->next = getNode(1); 

    // Given sum K 
    int K = 5; 

    // Function call to get head node 
    // of the updated Linked List 
    head = removeZeroSum(head, K); 

    // Print the updated Linked List 
    printList(head); 
    return 0; 
} 

```

**Output:**

```
1 -> 2 -> -3 -> 3 -> 1

```

***时间复杂度**：`O(n)`*，其中 N 是链​​接列表中 Node 的数目。

***辅助空间复杂度**：`O(n)`*，其中 N 是链​​接列表中 Node 的数目。



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。