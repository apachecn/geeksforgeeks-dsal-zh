# 使用递归

> 原文：[https://www.geeksforgeeks.org/create-a-circular-list-structure-for-given-value-k-using-recursion/](https://www.geeksforgeeks.org/create-a-circular-list-structure-for-given-value-k-using-recursion/)

为给定值 K 创建循环列表结构

给定数字 **K** ，任务是使用四个指针创建循环链表结构，四个指针分别是“使用递归”的下一个，上一个，上一个和下一个。

**注意**：不允许使用任何指针数组或 2D 矩阵

参见此示例，了解 K = 3

![](img/b7b2f0b6093d41ddc7ff7b2e6c2fe9d7.png)

**示例**：

```
Input: k = 3
Output: 1 2 3 
        4 5 6
        7 8 9
Explanation:
The structure will look like below

```

**方法**：

逐步执行以下步骤：

*   首先创建与右指针连接的单个 K 列表

*   每个列表的第一个节点应通过向下指针指向其下方节点

*   现在，将 K 列表与向下的指针逐行合并

*   然后在列表中按行和按列创建循环

下面是上述方法的实现：

## C++

```cpp

// C++ program to recursively create 
// loopy linked list with four 
// pointer left, right, up, down 
// by given value K without using 
// array of pointer and 2D matrix 

#include <iostream> 
using namespace std; 

// Struct node of Circular linked 
// list with four pointer 
// next, prev, up, down 
struct Node { 
    int data; 
    Node* left; 
    Node* right; 
    Node* up; 
    Node* down; 
}; 

// Function to create a new node 
Node* createNode(int value) 
{ 
    Node* temp = new Node(); 
    temp->data = value; 
    temp->left = NULL; 
    temp->right = NULL; 
    temp->up = NULL; 
    temp->down = NULL; 
    return temp; 
} 

// Function to create Singly list 
// whose nodes are connected with 
// right pointer 
Node* createListWithRightPointer(int k, 
                                 int i) 
{ 
    if (i > k) 
        return NULL; 
    Node* node = createNode(i); 
    // Recursively call the function to 
    // create list with the right pointer 
    node->right =  
        createListWithRightPointer(k, 
                                i + 1); 
    return node; 
} 

// Function to create the k singly 
// linked list and first node of 
// each list is connected with 
// down pointer 
Node* createKsinglyLinkedList(int k) 
{ 
    int rNum = 1; 
    int limit = k; 
    Node* head = NULL; 
    Node* rowPointer = NULL; 
    // Loop to create the k singly list 
    // for each list first node points 
    // to its below node by down pinter 
    for (int i = 1; i <= k; i++) { 
        Node* templist = 
          createListWithRightPointer(limit, 
                                     rNum); 
        if (head == NULL) { 
            head = templist; 
            rowPointer = head; 
        } 
        else { 
            rowPointer->down = templist; 
            rowPointer = rowPointer->down; 
        } 
        rNum = rNum + k; 
        limit = limit + k; 
    } 
    return head; 
} 

// Function to merge all list with 
// level wise via down pointer 
void mergeKListWithDownPointer(Node* head) 
{ 
    Node* first = NULL; 
    Node* second = NULL; 
    Node* start = head; 
    first = start; 
    second = first->down; 

    // Run while loop to merge k list 
    // row wise with down pointer 
    while (second) { 

        while (first || second) { 
            first->down = second; 
            first = first->right; 
            second = second->right; 
        } 
        first = start->down; 
        second = first->down; 
        start = start->down; 
    } 
} 

// Function to create the loop 
// for each coloumn 
void createLoopForEachColoumn(Node* head) 
{ 
    Node* first = NULL; 
    Node* last = NULL; 
    first = head; 
    last = first; 
    while (last->down) { 
        last = last->down; 
    } 
    // Run while loop to create 
    // loop for each coloumn 
    while (first || last) { 
        last->down = first; 
        first = first->right; 
        last = last->right; 
    } 
} 

// Function to create the loop 
// for each row 
void createLoopForEachRow(Node* head) 
{ 
    Node* first = NULL; 
    Node* last = NULL; 
    Node* start = NULL; 
    start = head; 
    first = head; 
    last = first; 
    while (last->right) { 
        last = last->right; 
    } 
    // Run while loop to create 
    // loop for each row 
    while (first->down != start) { 
        last->right = first; 
        first = first->down; 
        last = last->down; 
    } 
    last->right = first; 
} 

// Function to display the structre 
// of the list 
void display(Node* head) 
{ 
    // Pointer to move right 
    Node* rPtr; 

    // Pointer to move down 
    Node* dPtr = head; 

    // Pointer to stop printing 
    Node* start = head; 

    // Loop till node->down is not NULL 
    while (dPtr->down != start) { 

        rPtr = dPtr; 

        // Loop till node->right is 
        // not NULL 
        while (rPtr->right != dPtr) { 
            cout << rPtr->data << " "; 
            rPtr = rPtr->right; 
        } 
        cout << rPtr->data << " "; 

        cout << "\n"; 
        dPtr = dPtr->down; 
    } 
    rPtr = dPtr; 

    // Loop till node->right is  
    // not NULL 
    while (rPtr->right != dPtr) { 
        cout << rPtr->data << " "; 
        rPtr = rPtr->right; 
    } 
    cout << rPtr->data << " "; 

    cout << "\n"; 
} 

void createLoopInList(int k) 
{ 
    // Create k singly Linked List each 
    // first node of all list contain 
    // address of it's below first node 
    Node* head = createKsinglyLinkedList(k); 

    mergeKListWithDownPointer(head); 

    createLoopForEachColoumn(head); 

    createLoopForEachRow(head); 

    display(head); 
} 
int main() 
{ 
    int K = 4; 
    // Create the list structre 
    createLoopInList(K); 
} 

```

## Java

```java

// Java program to recursively create 
// loopy linked list with four 
// pointer left, right, up, down 
// by given value K without using 
// array of pointer and 2D matrix 

class GFG{ 

// Struct node of Circular linked 
// list with four pointer 
// next, prev, up, down 
static class Node { 
    int data; 
    Node left; 
    Node right; 
    Node up; 
    Node down; 
}; 

// Function to create a new node 
static Node createNode(int value) 
{ 
    Node temp = new Node(); 
    temp.data = value; 
    temp.left = null; 
    temp.right = null; 
    temp.up = null; 
    temp.down = null; 
    return temp; 
} 

// Function to create Singly list 
// whose nodes are connected with 
// right pointer 
static Node createListWithRightPointer(int k, 
                                 int i) 
{ 
    if (i > k) 
        return null; 
    Node node = createNode(i); 
    // Recursively call the function to 
    // create list with the right pointer 
    node.right =  
        createListWithRightPointer(k, 
                                i + 1); 
    return node; 
} 

// Function to create the k singly 
// linked list and first node of 
// each list is connected with 
// down pointer 
static Node createKsinglyLinkedList(int k) 
{ 
    int rNum = 1; 
    int limit = k; 
    Node head = null; 
    Node rowPointer = null; 
    // Loop to create the k singly list 
    // for each list first node points 
    // to its below node by down pinter 
    for (int i = 1; i <= k; i++) { 
        Node templist = 
          createListWithRightPointer(limit, 
                                     rNum); 
        if (head == null) { 
            head = templist; 
            rowPointer = head; 
        } 
        else { 
            rowPointer.down = templist; 
            rowPointer = rowPointer.down; 
        } 
        rNum = rNum + k; 
        limit = limit + k; 
    } 
    return head; 
} 

// Function to merge all list with 
// level wise via down pointer 
static void mergeKListWithDownPointer(Node head) 
{ 
    Node first = null; 
    Node second = null; 
    Node start = head; 
    first = start; 
    second = first.down; 

    // Run while loop to merge k list 
    // row wise with down pointer 
    while (second!=null) { 

        while (first!=null || second!=null) { 
            first.down = second; 
            first = first.right; 
            second = second.right; 
        } 
        first = start.down; 
        second = first.down; 
        start = start.down; 
    } 
} 

// Function to create the loop 
// for each coloumn 
static void createLoopForEachColoumn(Node head) 
{ 
    Node first = null; 
    Node last = null; 
    first = head; 
    last = first; 
    while (last.down!=null) { 
        last = last.down; 
    } 
    // Run while loop to create 
    // loop for each coloumn 
    while (first!=null || last!=null) { 
        last.down = first; 
        first = first.right; 
        last = last.right; 
    } 
} 

// Function to create the loop 
// for each row 
static void createLoopForEachRow(Node head) 
{ 
    Node first = null; 
    Node last = null; 
    Node start = null; 
    start = head; 
    first = head; 
    last = first; 
    while (last.right!=null) { 
        last = last.right; 
    } 
    // Run while loop to create 
    // loop for each row 
    while (first.down != start) { 
        last.right = first; 
        first = first.down; 
        last = last.down; 
    } 
    last.right = first; 
} 

// Function to display the structre 
// of the list 
static void display(Node head) 
{ 
    // Pointer to move right 
    Node rPtr; 

    // Pointer to move down 
    Node dPtr = head; 

    // Pointer to stop printing 
    Node start = head; 

    // Loop till node.down is not null 
    while (dPtr.down != start) { 

        rPtr = dPtr; 

        // Loop till node.right is 
        // not null 
        while (rPtr.right != dPtr) { 
            System.out.print(rPtr.data+ " "); 
            rPtr = rPtr.right; 
        } 
        System.out.print(rPtr.data+ " "); 

        System.out.print("\n"); 
        dPtr = dPtr.down; 
    } 
    rPtr = dPtr; 

    // Loop till node.right is  
    // not null 
    while (rPtr.right != dPtr) { 
        System.out.print(rPtr.data+ " "); 
        rPtr = rPtr.right; 
    } 
    System.out.print(rPtr.data+ " "); 

    System.out.print("\n"); 
} 

static void createLoopInList(int k) 
{ 
    // Create k singly Linked List each 
    // first node of all list contain 
    // address of it's below first node 
    Node head = createKsinglyLinkedList(k); 

    mergeKListWithDownPointer(head); 

    createLoopForEachColoumn(head); 

    createLoopForEachRow(head); 

    display(head); 
} 
public static void main(String[] args) 
{ 
    int K = 4; 
    // Create the list structre 
    createLoopInList(K); 
} 
} 

// This code contributed by sapnasingh4991 

```

## C#

```cs

// C# program to recursively create 
// loopy linked list with four 
// pointer left, right, up, down 
// by given value K without using 
// array of pointer and 2D matrix 
using System; 

class GFG{ 

// Struct node of circular linked 
// list with four pointer 
// next, prev, up, down 
class Node 
{ 
    public int data; 
    public Node left; 
    public Node right; 
    public Node up; 
    public Node down; 
}; 

// Function to create a new node 
static Node createNode(int value) 
{ 
    Node temp = new Node(); 
    temp.data = value; 
    temp.left = null; 
    temp.right = null; 
    temp.up = null; 
    temp.down = null; 

    return temp; 
} 

// Function to create Singly list 
// whose nodes are connected with 
// right pointer 
static Node createListWithRightPointer(int k, 
                                       int i) 
{ 
    if (i > k) 
        return null; 
    Node node = createNode(i); 

    // Recursively call the function to 
    // create list with the right pointer 
    node.right = createListWithRightPointer(k,  
                                            i + 1); 
    return node; 
} 

// Function to create the k singly 
// linked list and first node of 
// each list is connected with 
// down pointer 
static Node createKsinglyList(int k) 
{ 
    int rNum = 1; 
    int limit = k; 

    Node head = null; 
    Node rowPointer = null; 

    // Loop to create the k singly list 
    // for each list first node points 
    // to its below node by down pinter 
    for(int i = 1; i <= k; i++)  
    { 
       Node templist =createListWithRightPointer(limit,  
                                                 rNum); 
       if (head == null) 
       { 
           head = templist; 
           rowPointer = head; 
       } 
       else
       { 
           rowPointer.down = templist; 
           rowPointer = rowPointer.down; 
       } 
       rNum = rNum + k; 
       limit = limit + k; 
    } 
    return head; 
} 

// Function to merge all list with 
// level wise via down pointer 
static void mergeKListWithDownPointer(Node head) 
{ 
    Node first = null; 
    Node second = null; 
    Node start = head; 
    first = start; 
    second = first.down; 

    // Run while loop to merge k list 
    // row wise with down pointer 
    while (second != null) 
    { 
        while (first != null || second != null) 
        { 
            first.down = second; 
            first = first.right; 
            second = second.right; 
        } 
        first = start.down; 
        second = first.down; 
        start = start.down; 
    } 
} 

// Function to create the loop 
// for each coloumn 
static void createLoopForEachColoumn(Node head) 
{ 
    Node first = null; 
    Node last = null; 
    first = head; 
    last = first; 

    while (last.down != null) 
    { 
        last = last.down; 
    } 

    // Run while loop to create 
    // loop for each coloumn 
    while (first != null || last != null) 
    { 
        last.down = first; 
        first = first.right; 
        last = last.right; 
    } 
} 

// Function to create the loop 
// for each row 
static void createLoopForEachRow(Node head) 
{ 
    Node first = null; 
    Node last = null; 
    Node start = null; 
    start = head; 
    first = head; 
    last = first; 

    while (last.right != null) 
    { 
        last = last.right; 
    } 

    // Run while loop to create 
    // loop for each row 
    while (first.down != start)  
    { 
        last.right = first; 
        first = first.down; 
        last = last.down; 
    } 
    last.right = first; 
} 

// Function to display the structre 
// of the list 
static void display(Node head) 
{ 

    // Pointer to move right 
    Node rPtr; 

    // Pointer to move down 
    Node dPtr = head; 

    // Pointer to stop printing 
    Node start = head; 

    // Loop till node.down is not null 
    while (dPtr.down != start) 
    { 
        rPtr = dPtr; 

        // Loop till node.right is 
        // not null 
        while (rPtr.right != dPtr) 
        { 
            Console.Write(rPtr.data + " "); 
            rPtr = rPtr.right; 
        } 
        Console.Write(rPtr.data + " "); 
        Console.Write("\n"); 

        dPtr = dPtr.down; 
    } 
    rPtr = dPtr; 

    // Loop till node.right is  
    // not null 
    while (rPtr.right != dPtr)  
    { 
        Console.Write(rPtr.data + " "); 
        rPtr = rPtr.right; 
    } 
    Console.Write(rPtr.data + " "); 
    Console.Write("\n"); 
} 

static void createLoopInList(int k) 
{ 

    // Create k singly Linked List each 
    // first node of all list contain 
    // address of it's below first node 
    Node head = createKsinglyList(k); 

    mergeKListWithDownPointer(head); 
    createLoopForEachColoumn(head); 

    createLoopForEachRow(head); 
    display(head); 
} 

// Driver code 
public static void Main(String[] args) 
{ 
    int K = 4; 

    // Create the list structre 
    createLoopInList(K); 
} 
} 

// This code is contributed by 29AjayKumar 

```

**Output:**

```
1 2 3 4 
5 6 7 8 
9 10 11 12 
13 14 15 16

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。