# 使用双指针

删除链接列表中多次出现的键

给定一个单链表，请删除其中所有出现的给定键。 例如，考虑以下列表。

```
Input: 2 -> 2 -> 4 -> 3 -> 2
       Key to delete = 2
Output:  4 -> 3 

```

这主要是[的替代方案，该帖子使用针对头节点和其余节点](https://www.geeksforgeeks.org/delete-occurrences-given-key-linked-list/)的单独条件循环来删除多次出现的给定键。 在这里，我们使用双指针方法来使用单个循环，而与元素的位置（头，尾或中间）无关。 Linus Torvalds 在他的“ Linux 25 周年” TED 演讲中解释了从链接列表中删除节点而无需额外检查头部的原始方法。 本文使用该逻辑删除键的多次重复，而无需对头部进行额外检查。

说明：
1.将头的地址存储在双指针中，直到找到非“关键”节点。 这需要处理第一个 while 循环来处理头部的特殊情况。
2.如果某个节点不是“关键”节点，则将其地址->接下来的地址存储在 pp 中。
3.如果稍后再找到“关键”节点，则更改 pp（最终将节点- >接下来）指向当前节点->接下来。

以下是相同的 C++实现。

```

// CPP program to delete multiple 
// occurrences of a key using single 
// loop. 
#include <iostream> 
using namespace std; 

// A linked list node 
struct Node { 
    int data; 
    struct Node* next; 
}; 

struct Node* head = NULL; 

void printList(struct Node* node) 
{ 
    while (node != NULL) { 
        printf(" %d ", node->data); 
        node = node->next; 
    } 
} 

void push(int new_data) 
{ 
    struct Node* new_node = new Node; 
    new_node->data = new_data; 
    new_node->next = (head); 
    (head) = new_node; 
} 

void deleteEntry(int key) 
{ 
    // Start from head 
    struct Node** pp = &head; 
    while (*pp) { 

        struct Node* entry = *pp; 

        // If key found, then put 
        // next at the address of pp 
        // delete entry. 
        if (entry->data == key) { 
            *pp = entry->next; 
            delete (entry); 
        } 

        // Else move to next 
        else
            pp = &(entry->next); 
    } 
} 

int main() 
{ 
    push(2); 
    push(2); 
    push(4); 
    push(3); 
    push(2); 

    int key = 2; // key to delete 

    puts("Created Linked List: "); 
    printList(head); 
    printf("\n"); 
    deleteEntry(key); 
    printf("\nLinked List after Deletion of 2: \n"); 
    printList(head); 
    return 0; 
} 

```

**Output:**

```
Created Linked List: 
 2  3  4  2  2 

Linked List after Deletion of 2: 
 3  4

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。