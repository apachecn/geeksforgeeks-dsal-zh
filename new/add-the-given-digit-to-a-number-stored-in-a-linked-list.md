# 将给定的数字添加到链接列表中存储的数字中

给定一个表示整数的链表，其中每个节点都是一个数字（如果表示整数）。 任务是将给定的数字 **N** 添加到表示的整数。

**范例**：

> **输入**：`9 -> 9 -> 3 -> NULL, N = 7`
>
> **输出**：
>
> ```
> 9 -> 9 -> 3 -> NULL
> 1 -> 0 -> 0 -> 0 -> NULL
> ```
> 
> **输入**：`2 -> 9 -> 9 -> NULL, N = 5`
>
> **输出**：
>
> ```
> 2 -> 9 -> 9 -> NULL
> 3 -> 0 -> 4 -> NULL
> ```

**方法**：我们已经讨论了将`1`添加到此文章 int [中存储的数字中的方法，但是代码需要反转链接列表。

在本文中，我们将问题扩展到将任何数字添加到链表中存储的数字中，并实现该数字而无需反转或递归。](https://www.geeksforgeeks.org/add-1-number-represented-linked-list/)

想法是遍历列表，并且遍历时保持指向最后一个节点的指针，该节点的值小于 9。这是因为我们要向链接列表中存储的数字添加一个数字。 因此，进位的最大值（如果存在）可以为`1`。 假设我们开始从最低有效位向最高有效位传播进位，那么一旦发现小于 9 的数字，传播就会停止。

以这种方式完全遍历列表之后，我们终于到达了链表的最后一个节点，并且还维护了指向值小于 9 的最新节点的指针。

可能出现两种情况：

1.  在最后一位中添加数字即节点上的值大于 9 后可能会溢出。

2.  没有溢出，即在节点上添加的值小于 10 之后。

在第一种情况下，我们必须将进位从值小于 9 的最新节点传播到最后一个节点。

在第二种情况下，我们无需执行其他任何操作。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation of the approach
#include <iostream>
using namespace std;

// Node structure containing data
// and pointer to the next Node
struct node {

    int key;
    node* next;

    node(int n)
    {
        key = n;
        next = NULL;
    }
};

// Linked list class
class LinkedList {

    node* head;

public:
    // Default constructor for
    // creating empty list
    LinkedList();

    // Insert a node in linked list
    void insert(node* n);

    // Adding a single digit to the list
    void addDigit(int n);

    // Print the linked list
    void printList();
};

LinkedList::LinkedList()
{
    // Empty List
    head = NULL;
}

// Function to insert a node at the
// head of the linked list
void LinkedList::insert(node* n)
{
    // Empty List
    if (head == NULL)
        head = n;

    // Insert in the beginning of the list
    else {
        n->next = head;
        head = n;
    }
}

// Function to print the linked list
void LinkedList::printList()
{
    node* ptr = head;

    while (ptr) {
        cout << ptr->key << " -> ";
        ptr = ptr->next;
    }
    cout << "NULL" << endl;
}

// Function to add a digit to the integer
// represented as a linked list
void LinkedList::addDigit(int n)
{

    // To keep track of the last node
    // whose value is less than 9
    node* lastNode = NULL;
    node* curr = head;

    while (curr->next) {

        // If found a node with value
        // less than 9
        if (curr->key < 9)
            lastNode = curr;

        // Otherwise keep traversing
        // the list till end
        curr = curr->next;
    }

    // Add the given digit to the last node
    curr->key = curr->key + n;

    // In case of overflow in the last node
    if (curr->key > 9) {

        curr->key = curr->key % 10;

        // If the list is of the
        // form 9 -> 9 -> 9 -> ...
        if (lastNode == NULL) {

            // Insert a node at the beginnig as
            // there would be overflow in the
            // head in this case
            insert(new node(1));

            // Adjust the lastNode pointer to
            // propagate the carry effect to
            // all the nodes of the list
            lastNode = head->next;
        }

        // Forward propagate carry effect
        while (lastNode != curr) {
            lastNode->key = (lastNode->key + 1) % 10;
            lastNode = lastNode->next;
        }
    }
}

// Driver code
int main()
{
    // Creating the linked list
    LinkedList* l1 = new LinkedList();

    // Adding elements to the linked list
    l1->insert(new node(9));
    l1->insert(new node(9));
    l1->insert(new node(1));

    // Printing the original list
    l1->printList();

    // Adding the digit
    l1->addDigit(5);

    // Printing the modified list
    l1->printList();

    return 0;
}

```

## Java

```java

// Java implementation of the approach

// Node structure containing data
// and pointer to the next Node
class node 
{
    int key;
    node next;

    node(int n) 
    {
        key = n;
        next = null;
    }
};

// Linked list class
class LinkedList
{
    static node head;

    // Default constructor for
    // creating empty list
    public LinkedList() 
    {
        // Empty List
        head = null;
    }

    // Function to insert a node at the
    // head of the linked list
    void insert(node n)
    {

        // Empty List
        if (head == null)
            head = n;

        // Insert in the beginning of the list
        else
        {
            n.next = head;
            head = n;
        }
    }

    // Function to print the linked list
    void printList()
    {
        node ptr = head;

        while (ptr != null) 
        {
            System.out.print(ptr.key + "->");
            ptr = ptr.next;
        }
        System.out.print("null" + "\n");
    }

    // Function to add a digit to the integer
    // represented as a linked list
    void addDigit(int n) 
    {

        // To keep track of the last node
        // whose value is less than 9
        node lastNode = null;
        node curr = head;

        while (curr.next != null)
        {

            // If found a node with value
            // less than 9
            if (curr.key < 9)
                lastNode = curr;

            // Otherwise keep traversing
            // the list till end
            curr = curr.next;
        }

        // Add the given digit to the last node
        curr.key = curr.key + n;

        // In case of overflow in the last node
        if (curr.key > 9)
        {
            curr.key = curr.key % 10;

            // If the list is of the
            // form 9.9.9....
            if (lastNode == null) 
            {

                // Insert a node at the beginnig as
                // there would be overflow in the
                // head in this case
                insert(new node(1));

                // Adjust the lastNode pointer to
                // propagate the carry effect to
                // all the nodes of the list
                lastNode = head.next;
            }

            // Forward propagate carry effect
            while (lastNode != curr) 
            {
                lastNode.key = (lastNode.key + 1) % 10;
                lastNode = lastNode.next;
            }
        }
    }

    // Driver code
    public static void main(String[] args) 
    {

        // Creating the linked list
        LinkedList l1 = new LinkedList();

        // Adding elements to the linked list
        l1.insert(new node(9));
        l1.insert(new node(9));
        l1.insert(new node(1));

        // Printing the original list
        l1.printList();

        // Adding the digit
        l1.addDigit(5);

        // Printing the modified list
        l1.printList();
    }
}

// This code is contributed by Rajput-Ji

```

## C#

```cs

// C# implementation of the approach
using System;

// Node structure containing data
// and pointer to the next Node
public class node 
{
    public int key;
    public node next;

    public node(int n) 
    {
        key = n;
        next = null;
    }
};

// Linked list class
public class List
{
    static node head;

    // Default constructor for
    // creating empty list
    public List() 
    {
        // Empty List
        head = null;
    }

    // Function to insert a node at the
    // head of the linked list
    void insert(node n)
    {

        // Empty List
        if (head == null)
            head = n;

        // Insert in the beginning of the list
        else
        {
            n.next = head;
            head = n;
        }
    }

    // Function to print the linked list
    void printList()
    {
        node ptr = head;

        while (ptr != null) 
        {
            Console.Write(ptr.key + "->");
            ptr = ptr.next;
        }
        Console.Write("null" + "\n");
    }

    // Function to add a digit to the integer
    // represented as a linked list
    void addDigit(int n) 
    {

        // To keep track of the last node
        // whose value is less than 9
        node lastNode = null;
        node curr = head;

        while (curr.next != null)
        {

            // If found a node with value
            // less than 9
            if (curr.key < 9)
                lastNode = curr;

            // Otherwise keep traversing
            // the list till end
            curr = curr.next;
        }

        // Add the given digit to the last node
        curr.key = curr.key + n;

        // In case of overflow in the last node
        if (curr.key > 9)
        {
            curr.key = curr.key % 10;

            // If the list is of the
            // form 9.9.9....
            if (lastNode == null) 
            {

                // Insert a node at the beginnig as
                // there would be overflow in the
                // head in this case
                insert(new node(1));

                // Adjust the lastNode pointer to
                // propagate the carry effect to
                // all the nodes of the list
                lastNode = head.next;
            }

            // Forward propagate carry effect
            while (lastNode != curr) 
            {
                lastNode.key = (lastNode.key + 1) % 10;
                lastNode = lastNode.next;
            }
        }
    }

    // Driver code
    public static void Main(String[] args) 
    {

        // Creating the linked list
        List l1 = new List();

        // Adding elements to the linked list
        l1.insert(new node(9));
        l1.insert(new node(9));
        l1.insert(new node(1));

        // Printing the original list
        l1.printList();

        // Adding the digit
        l1.addDigit(5);

        // Printing the modified list
        l1.printList();
    }
}

// This code is contributed by 29AjayKumar

```

**Output:** 

```
1 -> 9 -> 9 -> NULL
2 -> 0 -> 4 -> NULL

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。