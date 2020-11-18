# 程序从链接列表

中删除元音

给定[单链接列表](https://www.geeksforgeeks.org/data-structures/linked-list/singly-linked-list/)，任务是从给定[链接列表](http://www.geeksforgeeks.org/data-structures/linked-list/)中删除元音。

**示例：**

> **输入：** g-> e-> e-> k-> s-> f-> o-> r-> g- > e-> e-> k-> s
> **输出：** g-> k-> s-> f-> r-> g-> k-> s
> **解释：**
> 去除了元音{e，e}，{o}，{e，e}之后。 链接列表变为
> g-> k-> s-> f-> r-> g-> k-> s
> 
> **输入：** a-> a-> a-> g-> e-> e-> k-> s-> i- > i-> i-> m
> **输出：** g-> k-> s-> m
> **说明：[**
> 删除了元音{a，a，a}，{e，e}，{i，i，i}之后。 链接列表变为
> g-> k-> s-> f-> r-> g-> k-> s

**方法：**

在三种情况下，我们可以在给定的链表中找到元音：

1.  <u>**At starting of the linked list**</u>: For removing vowels from the starting of the [linked list](http://www.geeksforgeeks.org/data-structures/linked-list/), move the **head Node** to the first consonant occurs in the [linked list](http://www.geeksforgeeks.org/data-structures/linked-list/).

    For Example:

    ```
    For Linked List:
    a -> e -> i -> a -> c -> r -> d -> NULL
    After moving the head Node from Node a to Node c,  We have 
    c -> r -> d -> NULL

    ```

2.  <u>**In between of the linked list**</u>: For removing vowels from the between of the [linked list](http://www.geeksforgeeks.org/data-structures/linked-list/), the idea is to keep a marker of the last consonant found in the [linked list](http://www.geeksforgeeks.org/data-structures/linked-list/) before the **vowel Nodes** and change the next link of that Node with the next consonant Node found in the [linked list](http://www.geeksforgeeks.org/data-structures/linked-list/) after **vowel Nodes**.

    For Example:

    ```
    For Linked List:
    c -> r -> d -> a -> e -> i -> a -> c -> r -> z -> NULL
    last consonant before vowels {a, e, i, a} is d
    and next consonant after vowels {a, e, i, a} is r
    After linking next pointer of Node d to Node r, We have 
    c -> r -> d -> r -> z -> NULL

    ```

3.  <u>**At the end of the linked list**</u>: For removing vowels from the end of the [linked list](http://www.geeksforgeeks.org/data-structures/linked-list/), the idea is to keep a marker of the last consonant found in the [linked list](http://www.geeksforgeeks.org/data-structures/linked-list/) before the **vowel Nodes** and change the next link of that Node with NULL.

    For Example:

    ```
    For Linked List:
    c -> r -> d -> a -> e -> i -> a -> NULL
    last consonant before vowels {a, e, i, a} is d
    After changing the next link of Node  to NULL, We have 
    c -> r -> d -> NULL

    ```

下面是上述方法的实现：

```

// C++ program to remove vowels 
// Nodes in a linked list 
#include <bits/stdc++.h> 
using namespace std; 

// A linked list node 
struct Node { 
    char data; 
    struct Node* next; 
}; 

// Head Node 
struct Node* head; 

// Function to add new node to the 
// List 
Node* newNode(char key) 
{ 
    Node* temp = new Node; 
    temp->data = key; 
    temp->next = NULL; 
    return temp; 
} 

// Utility function to print the 
// linked list 
void printlist(Node* head) 
{ 
    if (!head) { 
        cout << "Empty List\n"; 
        return; 
    } 
    while (head != NULL) { 
        cout << head->data << " "; 
        if (head->next) 
            cout << "-> "; 
        head = head->next; 
    } 
    cout << endl; 
} 

// Utility function for checking vowel 
bool isVowel(char x) 
{ 
    return (x == 'a' || x == 'e' || x == 'i'
            || x == 'o' || x == 'u' || x == 'A'
            || x == 'E' || x == 'I' || x == 'O'
            || x == 'U'); 
} 

// Function to remove the vowels Node 
void removeVowels() 
{ 
    // Node pointing to head Node 
    struct Node* ptr = head; 

    // Case 1 : Remove the trailing 
    // vowels 
    while (ptr != NULL) { 

        // If current Node is a vowel 
        // node then move the pointer 
        // to next node 
        if (isVowel(ptr->data)) 
            ptr = ptr->next; 

        // Else break if a consonant 
        // node is found 
        else
            break; 
    } 

    // This prev node used to link 
    // prev consonant to next 
    // consonant after vowels 
    struct Node* prev = ptr; 

    // Head points to the first 
    // consonant of the linked list 
    head = ptr; 

    ptr = ptr->next; 

    // Case 2: If vowels found in 
    // between of the linked list 
    while (ptr != NULL) { 

        // If current node is vowel 
        if (isVowel(ptr->data)) { 

            // Move ptr to the next 
            // node 
            ptr = ptr->next; 

            // Check for vowels 
            // occurring continuously 
            while (ptr != NULL) { 

                // If ptr is a vowel 
                // move to next pointer 
                if (isVowel(ptr->data)) { 
                    ptr = ptr->next; 
                } 
                // Else break if 
                // consonant found 
                else
                    break; 
            } 

            // Case 3: If we have ending 
            // vowels then link the prev 
            // consonant to NULL 
            if (ptr == NULL) { 
                prev->next = NULL; 
                break; 
            } 

            // Case 2: change the next 
            // link of prev to current 
            // consonant pointing to 
            // ptr 
            else { 
                prev->next = ptr; 
            } 
        } 

        // Move prev and ptr to next 
        // for next iteration 
        prev = prev->next; 
        ptr = ptr->next; 
    } 
} 

// Driver code 
int main() 
{ 
    // Initialise the Linked List 
    head = newNode('a'); 
    head->next = newNode('b'); 
    head->next->next = newNode('c'); 
    head->next->next->next = newNode('e'); 
    head->next->next->next->next = newNode('f'); 
    head->next->next->next->next->next = newNode('g'); 
    head->next->next->next->next->next->next = newNode('i'); 
    head->next->next->next->next->next->next->next = newNode('o'); 

    // Print the given Linked List 
    printf("Linked list before :\n"); 
    printlist(head); 

    removeVowels(); 

    // Print the Linked List after 
    // removing vowels 
    printf("Linked list after :\n"); 
    printlist(head); 

    return 0; 
} 

```

**Output:**

```
Linked list before :
a -> b -> c -> e -> f -> g -> i -> o 
Linked list after :
b -> c -> f -> g

```

**时间复杂度：**`O(n)`，其中 N 是链​​表中节点的数量。



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。