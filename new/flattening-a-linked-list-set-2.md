# 展平链表 | 系列 2

> 原文：[https://www.geeksforgeeks.org/flattening-a-linked-list-set-2/](https://www.geeksforgeeks.org/flattening-a-linked-list-set-2/)

给定[链表](http://www.geeksforgeeks.org/data-structures/linked-list/)，其中每个节点代表一个链表，并包含两个其类型的指针：

*   指向主列表中下一个节点的指针（在下面的代码中我们称其为“正确”指针）

*   指向此节点位于头的链表的指针（在下面的代码中我们称之为“向下”指针）。

所有链表均已排序。 请参见以下示例

**示例**：

```
Input: 
5 -> 10 -> 19 -> 28
|    |     |     |
V    V     V     V
7    20    22    35
|          |     |
V          V     V
8          50    40
|                |
V                V
30               45

Output: 5->7->8->10->19->20->22->28->30->35->40->45->50

Input: 
5 -> 10 -> 19 -> 28
|          |   
V          V    
7          22   
|          |   
V          V    
8          50 
|              
V               
30              

Output: 5->7->8->10->19->20->22->30->50

```

在[之前的帖子](https://www.geeksforgeeks.org/flattening-a-linked-list/)中，我们必须对链表使用[合并排序的 **merge（）**处理，以使链表平坦化。

在本文中，我们将使用](https://www.geeksforgeeks.org/merge-sort-for-linked-list/)[堆](https://www.geeksforgeeks.org/heap-data-structure/)解决该问题。

**方法**：的想法是观察从每个顶部节点向下方向连接的 **N** 个节点，但观察到所有向下的节点都是按排序的顺序。 因此，任务是按升序（或降序）对整个事物进行排序。

1.  在[优先级队列](https://www.geeksforgeeks.org/priority-queue-set-1-introduction/)中将所有链表的开头推入向下列表。

2.  从优先级队列中弹出最小的节点。

3.  检查节点的位置，以便可以将当前节点指向的下一个节点推入优先级队列。

4.  再次弹出最小的元素，并插入当前节点指向的下一个节点，直到堆变空。

5.  继续在弹出的新链表中添加节点的数据。

6.  打印上面形成的链表。

下面是上述方法的实现：

## C++

```cpp

// C++ program for Flattening
// a linked list using Heaps
#include <bits/stdc++.h>
using namespace std;

// Structure of given Linked list
struct Node {
    int data;
    struct Node* right;
    struct Node* down;

    Node(int x)
    {
        data = x;
        right = NULL;
        down = NULL;
    }
};

// Function to print the
// linked list
void printList(Node* Node)
{
    while (Node != NULL) {
        printf("%d ", Node->data);
        Node = Node->down;
    }
}

// Function that compares the value
// pointed by node and returns true
// if first data is greater
struct compare {
    bool operator()(Node* a, Node* b)
    {
        return a->data > b->data;
    }
};

// Function which returns the root
// of the flattened linked list
Node* flatten(Node* root)
{
    Node* ptr = root;
    Node* head = NULL;

    // Min Heap which will return
    // smallest element currently
    // present in heap
    priority_queue<Node*, 
            vector<Node*>, 
             compare> pq;

    // Push the head nodes of each
    // downward linked list
    while (ptr != NULL) {
        pq.push(ptr);
        ptr = ptr->right;
    }

    // This loop will execute
    // till the map becomes empty
    while (!pq.empty()) {

        // Pop out the node that
        // contains element
        // currently in heap
        Node* temp = pq.top();
        pq.pop();

        // Push the next node pointed by
        // the current node into heap
        // if it is not null
        if (temp->down != NULL) {
            pq.push(temp->down);
        }

        // Create new linked list
        // that is to be returned
        if (head == NULL) {
            head = temp;
            ptr = temp;
            ptr->right = NULL;
        }
        else {
            ptr->down = temp;
            ptr = temp;
            ptr->right = NULL;
        }
    }

    // Pointer to head node
    // in the linked list
    return head;
}

// Create and push new nodes
void push(Node** head_ref, int new_data)
{
    Node* new_node = (Node*)malloc(sizeof(Node));
    new_node->right = NULL;
    new_node->data = new_data;
    new_node->down = (*head_ref);

    (*head_ref) = new_node;
}

// Driver Code
int main()
{
    Node* root = NULL;

    // Given Linked List
    push(&root, 30);
    push(&root, 8);
    push(&root, 7);
    push(&root, 5);

    push(&(root->right), 20);
    push(&(root->right), 10);

    push(&(root->right->right), 50);
    push(&(root->right->right), 22);
    push(&(root->right->right), 19);

    push(&(root->right->right->right), 45);
    push(&(root->right->right->right), 40);
    push(&(root->right->right->right), 35);
    push(&(root->right->right->right), 20);

    // Flatten the list
    root = flatten(root);

    // Print the flatened linked list
    printList(root);

    return 0;
}

```

## Java

```java

// Java program for Flattening
// a linked list using Heaps
import java.util.*;

// Linked list Node
class Node {
    int data;
    Node right, down;
    Node(int data)
    {
        this.data = data;
        right = null;
        down = null;
    }
}

class pair {
    int val;
    Node head;

    pair(Node head, int val)
    {
        this.val = val;
        this.head = head;
    }
}

// Class that compares the value
// pointed by node and make
// LinkedList sorted
class pairComp implements Comparator<pair> {
    public int compare(pair p1, pair p2)
    {
        return p1.val - p2.val;
    }
}

class GFG {

    // Function which returns the root
    // of the flattened linked list
    public static Node flatten(Node root)
    {
        Node ptr = root;
        Node h = null;

        // Min Heap which will return
        // smallest element currently
        // present in heap
        PriorityQueue<pair> pq
            = new PriorityQueue<pair>(
                        new pairComp());

        // Push the head nodes of each
        // downward linked list
        while (ptr != null) {
            pq.add(new pair(ptr, ptr.data));
            ptr = ptr.right;
        }

        // This loop will execute
        // till the pq becomes empty
        while (!pq.isEmpty()) {

            // Pop out the node that
            // contains element
            // currently in heap
            Node temp = pq.poll().head;

            // Push the next node pointed by
            // the current node into heap
            // if it is not null
            if (temp.down != null) {
                pq.add(new pair(temp.down, 
                                temp.down.data));
            }

            // Create new linked list
            // that is to be returned
            if (h == null) {
                h = temp;
                ptr = temp;
                ptr.right = null;
            }
            else {
                ptr.down = temp;
                ptr = temp;
                ptr.right = null;
            }
        }

        // Pointer to head node
        // in the linked list
        return h;
    }

    // Create and push new nodes
    public static Node push(Node head_ref, 
                            int data)
    {

        // Allocate the Node &
        // Put in the data
        Node new_node = new Node(data);

        // Make next of new Node as head
        new_node.down = head_ref;

        // Move the head to point to new Node
        head_ref = new_node;

        // return to link it back
        return head_ref;
    }

    // Function to print the
    // linked list
    public static void printList(Node h)
    {
        while (h != null) {
            System.out.print(h.data + " ");
            h = h.down;
        }
    }

    // Driver code
    public static void main(String args[])
    {
        Node head = null;

        head = push(head, 30);
        head = push(head, 8);
        head = push(head, 7);
        head = push(head, 5);

        head.right = push(head.right, 20);
        head.right = push(head.right, 10);

        head.right.right = push(
                  head.right.right, 50);
        head.right.right = push(
                  head.right.right, 22);
        head.right.right = push(
                  head.right.right, 19);

        head.right.right.right
            = push(
          head.right.right.right, 45);
        head.right.right.right
            = push(
              head.right.right.right, 40);
        head.right.right.right
            = push(
              head.right.right.right, 35);
        head.right.right.right
            = push(head.right.right.right, 20);

        // Flatten the list
        head = flatten(head);

        printList(head);
    }
}

// This code is contributed by Naresh Saharan
// and Sagar Jangra and Tridib Samanta

```

**Output**

```
5 7 8 10 19 20 20 22 30 35 40 45 50 
```

**时间复杂度**：*O（k * log k）+ O（（Nk）* log k）=* **O（N * log k）**，其中“ *k* '是最上面的水平链表中的节点数，' *N* '是所有链表中的节点总数。 ‘ *log k* ’占用最小堆时间。

**辅助空间：[min-heap]的** **O（k）**，其中“ *k* ”是最顶部水平链表中的节点数。 最小堆在任何时候最多具有“ *k* ”个节点。



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。