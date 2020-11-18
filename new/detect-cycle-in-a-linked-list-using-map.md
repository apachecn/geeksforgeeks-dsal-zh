# 使用地图

检测链接列表中的周期

给定[链接列表](http://www.geeksforgeeks.org/data-structures/linked-list/)，检查链接列表是否具有循环。

这里显示了各种方法：[链接列表](https://www.geeksforgeeks.org/detect-loop-in-a-linked-list/)中的检测周期

**范例**

> **输入：** 20- > 4- > 54- > 6- >空
> **输出：**未检测到循环。
> **说明：**
> 在遍历链接列表时，我们到达了链接列表的末尾。 因此，链表中没有循环。
> 
> **输入：** 20- > 4- > 5- > 10- > 20
> **输出：**检测到环路。
> **说明：**
> 在遍历链接列表时，我们到达值为 10 的节点与表示链接列表中循环的头节点链接。 因此，循环出现在链表中。

**方法：**

1.  创建一个[映射](http://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)，它将被访问的节点存储在[链接列表](http://www.geeksforgeeks.org/data-structures/linked-list/)中。
2.  遍历[链接列表](http://www.geeksforgeeks.org/data-structures/linked-list/)并执行以下操作：
    *   检查地图中是否存在当前节点。
    *   如果[映射](http://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中不存在当前节点，则在映射中插入当前节点。
    *   如果节点存在于映射中，则检测到链表中的循环。
3.  如果在遍历[链表](http://www.geeksforgeeks.org/data-structures/linked-list/)时到达**空节点**，则给定的链表中没有循环。

下面是上述方法的实现：

```

// C++ program to detect loop in 
// given linked list using map 
#include <bits/stdc++.h> 
using namespace std; 

// Structure for a node in Linked List 
struct Node { 
    int data; 
    Node* next; 
}; 

// Function to create Linked List 
// Node 
Node* newNode(int d) 
{ 
    Node* temp = new Node; 
    temp->data = d; 
    temp->next = NULL; 
    return temp; 
} 

// Declaration of Map to keep 
// mark of visited Node 
map<Node*, bool> vis; 
bool flag = 0; 

// Function to check cycle in Linked 
// List 
void check(Node* head) 
{ 
    // If head is NULL return ; 
    if (head == NULL) { 
        flag = 0; 
        return; 
    } 

    // Mark the incoming Node as 
    // visited if it is not visited yet 
    if (!vis[head]) { 
        vis[head] = true; 
        check(head->next); 
    } 

    // If a visited Node is found 
    // Update the flag value to 1 
    // and return ; 
    else { 
        flag = 1; 
        return; 
    } 
} 

// Driver Code 
int main() 
{ 
    // Create a head Node 
    Node* head = newNode(20); 

    // Inserting Node in Linked List 
    head->next = newNode(4); 
    head->next->next = newNode(5); 
    head->next->next->next = newNode(10); 

    // Just to make a cycle 
    head->next->next->next->next = head; 

    // Function that detect cycle in 
    // Linked List 
    check(head); 

    // If flag is true, loop is found 
    if (flag) 
        cout << "Loop detected."; 

    // If flag is false, No Loop 
    // detected 
    else
        cout << "No Loop Found."; 
    cout << endl; 

    return 0; 
} 

```

**Output:**

```
Loop detected.

```

**时间复杂度：** O（N * log N）
**辅助空间：** O（N）



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。