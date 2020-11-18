# 循环链表

中值为偶数和的节点的总和和乘积

给定一个包含 **N** 个节点的循环单链接列表，任务是从列表中找到其数据值具有偶数和的所有节点的和与乘积。

**范例**：

> **输入**：列表= 15-> 16-> 8-> 6-> 13
> **输出**：总和= 42，乘积= 9360
> **解释**：
> 循环链表包含：
> 15-> 1 + 5 = 6
> 16-> 1 + 6 = 7
> 8- > 8
> 6-> 6
> 13-> 1 + 3 = 4
> 该列表包含 4 个偶数总和数据值 15、8、6 和 13。
> 总和 = 15 + 8 + 6 + 13 = 42
> 乘积= 15 * 8 * 6 * 13 = 9360
> 
> **输入**：列表= 5-> 3-> 4-> 2-> 9
> **输出**：总和= 6，乘积= 8
> **说明**：
> 该列表包含 2 个偶数总和数据值 4 和 2。
> 总和= 4 + 2 = 6
> 乘积= 4 * 2 = 8

**方法**：

1.  用循环链表的开头初始化指针电流，并将和变量**和**设为 0，并将乘积变量**积**设为 1。

2.  开始使用 do-while 循环遍历链接列表，直到遍历所有节点。

3.  当前节点数据值是否具有偶数和。

    *   将当前节点的值添加到总和，即 **sum =总和+当前->数据**。

    *   将当前节点的值乘以乘积，即**乘积=乘积*当前->数据**。

    *   递增指向链表的下一个节点的指针，即 **temp = temp-> next** 。

4.  打印总和和乘积。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation to find the sum and 
// product of all of the Even Digit sum nodes 
// in a circularly linked list 
#include <bits/stdc++.h> 
using namespace std; 

// Circular list node 
struct Node { 
    int data; 
    struct Node* next; 
}; 

// Function to find the digit sum 
// for a number 
int digitSum(int num) 
{ 
    int sum = 0; 
    while (num) { 
        sum += (num % 10); 
        num /= 10; 
    } 

    return sum; 
} 

// Function to calculate sum and 
// product 
void SumProduct(struct Node* head, 
                int key) 
{ 
    struct Node* current = head; 

    int sum = 0, product = 1; 

    // If list is empty simply  
    // show message 
    if (head == NULL) { 
        printf("\nList is empty\n"); 
        return; 
    } 
    // Traverse first to last node 
    else { 
        do { 
            // Check if current node's 
            // data has an even digit sum 
            if (!(digitSum(current->data)  
                  & 1)) 
            { 

                // Calculate sum 
                sum += current->data; 

                // Calculate product 
                product *= current->data; 
            } 

            current = current->next; 
        } while (current != head); 
    } 

    cout << "Sum = " << sum  
        << ", Product = " << product; 
} 

// Function print the list 
void DisplayList(struct Node* head) 
{ 
    struct Node* current = head; 

    // If list is empty simply 
    // show message 
    if (head == NULL) 
    { 
        printf("\nList is empty\n"); 
        return; 
    } 
    // Traverse first to last node 
    else { 
        do { 
            printf("%d ", current->data); 
            current = current->next; 
        } while (current != head); 
    } 
} 

// Function to insert a node at the  
// end of a Circular linked list 
void InsertNode(struct Node** head, 
                int data) 
{ 
    struct Node* current = *head; 

    // Create a new node 
    struct Node* newNode = new Node; 

    // Check node is created or not 
    if (!newNode) { 
        printf("\nMemory Error\n"); 
        return; 
    } 

    // Insert data into newly 
    // created node 
    newNode->data = data; 

    // Check list is empty 
    // if not have any node then 
    // make first node it 
    if (*head == NULL) { 
        newNode->next = newNode; 
        *head = newNode; 
        return; 
    } 
    // If list have already some node 
    else { 

        // Move first node to last  
        // node 
        while (current->next != *head) 
        { 
            current = current->next; 
        } 

        // Put first or head node  
        // address in new node link 
        newNode->next = *head; 

        // Put new node address into  
        // last node link(next) 
        current->next = newNode; 
    } 
} 

// Driver Code 
int main() 
{ 
    struct Node* head = NULL; 
    InsertNode(&head, 13); 
    InsertNode(&head, 6); 
    InsertNode(&head, 8); 
    InsertNode(&head, 15); 
    InsertNode(&head, 16); 

    cout << "Initial List: "; 
    DisplayList(head); 

    cout << endl; 
    SumProduct(head, 11); 

    return 0; 
} 

```

## Java

```java

// Java implementation to find the sum and  
// product of all of the Even Digit sum nodes  
// in a circularly linked list  
class GFG{ 

// Structure for a node 
static class Node{ 
    int data; 
    Node next; 
} 

// Function to calulate the sum of 
// indivdual digits 
static int digitSum(int n) 
{ 
    int sum = 0; 
    while (n != 0)  
    { 
        sum += n % 10; 
        n /= 10; 
    } 
    return sum; 
} 

// Function to calculate sum and 
// product 
static void SumProduct(Node head) 
{ 
    Node temp = head; 
    int Sum = 0; 
    int Prod = 1; 

    do 
    { 

        // Check if current node's 
        // data has an even digit sum 
        if (digitSum(temp.data) % 2 == 0) 
        { 
            Sum += temp.data; 
            Prod *= temp.data; 
        } 

        temp = temp.next; 

    } while (temp != head); 

    System.out.print("Sum = " + Sum); 
    System.out.print(", Product = " + Prod); 
} 

// Function print the list 
static void DisplayList(Node head) 
{ 
    Node temp = head; 
    if (head != null) 
    { 
        do
        { 

            // Traverse first to last node 
            System.out.print(temp.data + " "); 
            temp = temp.next; 
        } while (temp != head); 
    } 
    System.out.println(); 
} 

// Function to insert a node at the ending 
// of a Circular linked list 
static Node InsertNode(int key, Node head) 
{ 

    // Create a new node 
    Node new_node = new Node(); 
    new_node.data = key; 

    // If linked list is null then 
    // make the first node as head  
    // after insertion 
    if (head == null) 
    { 
        head = new_node; 
        new_node.next = head; 

    }  
    else
    { 

        // traverse to the end and insert 
        // node at the end and make 
        // it point to the head 
        Node temp = head; 
        while (temp.next != head)  
        { 
            temp = temp.next; 
        } 

        temp.next = new_node; 
        new_node.next = head; 
    } 
    return head; 
} 

// Driver code 
public static void main(String args[])  
{ 
    Node head = null; 

    head = InsertNode(13, head); 
    head = InsertNode(6, head); 
    head = InsertNode(8, head); 
    head = InsertNode(15, head); 
    head = InsertNode(16, head); 

    System.out.print("Initial List: "); 

    DisplayList(head); 
    SumProduct(head); 
} 
} 

// This code is contributed by nishkarsh146 

```

## C#

```cs

// C# implementation to find the sum and  
// product of all of the Even Digit sum nodes  
// in a circularly linked list  
using System; 

class GFG{ 

// Structure for a node 
class Node 
{ 
    public int data; 
    public Node next; 
} 

// Function to calulate the sum of 
// indivdual digits 
static int digitSum(int n) 
{ 
    int sum = 0; 
    while (n != 0)  
    { 
        sum += n % 10; 
        n /= 10; 
    } 
    return sum; 
} 

// Function to calculate sum and 
// product 
static void SumProduct(Node head) 
{ 
    Node temp = head; 
    int Sum = 0; 
    int Prod = 1; 

    do
    { 

        // Check if current node's 
        // data has an even digit sum 
        if (digitSum(temp.data) % 2 == 0) 
        { 
            Sum += temp.data; 
            Prod *= temp.data; 
        } 

        temp = temp.next; 

    } while (temp != head); 

    Console.Write("Sum = " + Sum); 
    Console.Write(", Product = " + Prod); 
} 

// Function print the list 
static void DisplayList(Node head) 
{ 
    Node temp = head; 
    if (head != null) 
    { 
        do
        { 

            // Traverse first to last node 
            Console.Write(temp.data + " "); 
            temp = temp.next; 
        } while (temp != head); 
    } 
    Console.WriteLine(); 
} 

// Function to insert a node at the ending 
// of a Circular linked list 
static Node InsertNode(int key, Node head) 
{ 

    // Create a new node 
    Node new_node = new Node(); 
    new_node.data = key; 

    // If linked list is null then 
    // make the first node as head  
    // after insertion 
    if (head == null) 
    { 
        head = new_node; 
        new_node.next = head; 

    }  
    else
    { 

        // traverse to the end and insert 
        // node at the end and make 
        // it point to the head 
        Node temp = head; 
        while (temp.next != head)  
        { 
            temp = temp.next; 
        } 

        temp.next = new_node; 
        new_node.next = head; 
    } 
    return head; 
} 

// Driver code 
public static void Main(String []args)  
{ 
    Node head = null; 

    head = InsertNode(13, head); 
    head = InsertNode(6, head); 
    head = InsertNode(8, head); 
    head = InsertNode(15, head); 
    head = InsertNode(16, head); 

    Console.Write("Initial List: "); 

    DisplayList(head); 
    SumProduct(head); 
} 
} 

// This code is contributed by 29AjayKumar 

```

**Output:** 

```
Initial List: 13 6 8 15 16 
Sum = 42, Product = 9360

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。