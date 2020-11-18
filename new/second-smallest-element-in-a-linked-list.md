# 链表中第二小的元素

给定整数数据的链接列表。 任务是编写一个程序，以有效地找到链表中存在的第二个最小元素。

**示例**：

```
Input : List = 12 -> 35 -> 1 -> 10 -> 34 -> 1
Output : The second smallest element is 10.

Input : List = 10 -> 5 -> 10
Output : The second largest element is 10.

```

**简单解决方案**将是首先按升序对链表进行排序，然后从排序的链表中打印第二个元素。 该解决方案的时间复杂度为 O（nlogn）。

**更好的解决方案**是遍历链接列表两次。 在第一个遍历中找到最小元素。 在第二遍历中找到比在第一遍历中获得的元素更大的最小元素。 该解决方案的时间复杂度为`O(n)`。

更有效的**解决方案**是在单个遍历中查找第二小的元素。

## C++

```cpp

// C++ program to print second smallest 
// value in a linked list 
#include <climits> 
#include <iostream> 

using namespace std; 

// A linked list node 
struct Node { 
    int data; 
    struct Node* next; 
}; 

// Function to add a node at the 
// beginning of Linked List 
void push(struct Node** head_ref, int new_data) 
{ 
    struct Node* new_node = new Node; 
    new_node->data = new_data; 
    new_node->next = (*head_ref); 
    (*head_ref) = new_node; 
} 

// Function to print the second 
// smallest element 
void print2smallest(struct Node* head) 
{ 
    int first = INT_MAX, second = INT_MAX; 

    struct Node* temp = head; 
    while (temp != NULL) { 

        if (temp->data < first) { 
            second = first; 
            first = temp->data; 
        } 

        // If current node's data is in between 
        // first and second then update second 
        else if (temp->data < second && temp->data != first) 
            second = temp->data; 

        temp = temp->next; 
    } 

    if (second == INT_MAX) 
        cout << "There is no second smallest element\n"; 
    else
        cout << "The second smallest element is " << second; 
} 

// Driver program to test above function 
int main() 
{ 
    struct Node* start = NULL; 

    /* The constructed linked list is:   
     12 -> 35 -> 1 -> 10 -> 34 -> 1 */
    push(&start, 1); 
    push(&start, 34); 
    push(&start, 10); 
    push(&start, 1); 
    push(&start, 35); 
    push(&start, 12); 

    print2smallest(start); 

    return 0; 
} 

```

## Java

```java

// Java program to print second smallest 
// value in a linked list 
class GFG 
{ 

// A linked list node 
static class Node  
{ 
    int data; 
    Node next; 
}; 

// Function to add a node at the 
// beginning of Linked List 
static Node push(Node head_ref, int new_data) 
{ 
    Node new_node = new Node(); 
    new_node.data = new_data; 
    new_node.next = head_ref; 
    head_ref = new_node; 
    return new_node; 
} 

// Function to print the second 
// smallest element 
static void print2smallest(Node head) 
{ 
    int first = Integer.MAX_VALUE,  
        second = Integer.MAX_VALUE; 

    Node temp = head; 
    while (temp != null) 
    { 

        if (temp.data < first) 
        { 
            second = first; 
            first = temp.data; 
        } 

        // If current node's data is in between 
        // first and second then update second 
        else if (temp.data < second && temp.data != first) 
            second = temp.data; 

        temp = temp.next; 
    } 

    if (second == Integer.MAX_VALUE) 
        System.out.print("There is no second smallest element\n"); 
    else
        System.out.print("The second smallest element is " + second); 
} 

// Driver code 
public static void main(String[] args) 
{ 
    Node start = null; 

    /* The constructed linked list is:  
    12.35.1.10.34.1 */
    start = push(start, 1); 
    start = push(start, 34); 
    start = push(start, 10); 
    start = push(start, 1); 
    start = push(start, 35); 
    start = push(start, 12); 

    print2smallest(start); 
} 
} 

// This code is contributed by PrinciRaj1992 

```

## Python3

```py

# Python3 program to print second smallest 
# value in a linked list 

# A linked list node 
class Node : 
    def __init__(self): 
        self.data = 0
        self.next = None

# Function to add a node at the 
# beginning of Linked List 
def push(head_ref, new_data): 

    new_node = Node() 
    new_node.data = new_data 
    new_node.next = head_ref 
    head_ref = new_node 
    return new_node 

# Function to print the second 
# smallest element 
def print2smallest(head): 

    first = 32676
    second = 32676

    temp = head 
    while (temp != None): 

        if (temp.data < first): 

            second = first 
            first = temp.data 

        # If current node's data is in between 
        # first and second then update second 
        elif (temp.data < second and temp.data != first): 
            second = temp.data 

        temp = temp.next

    if (second == 32676): 
        print("There is no second smallest element") 
    else: 
        print("The second smallest element is " , second) 

# Driver code 

start = None

# The constructed linked list is:  
# 12.35.1.10.34.1 
start = push(start, 1) 
start = push(start, 34) 
start = push(start, 10) 
start = push(start, 1) 
start = push(start, 35) 
start = push(start, 12) 

print2smallest(start) 

# This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# program to print second smallest 
// value in a linked list 
using System; 

class GFG 
{ 

// A linked list node 
class Node  
{ 
    public int data; 
    public Node next; 
}; 

// Function to add a node at the 
// beginning of Linked List 
static Node push(Node head_ref, int new_data) 
{ 
    Node new_node = new Node(); 
    new_node.data = new_data; 
    new_node.next = head_ref; 
    head_ref = new_node; 
    return new_node; 
} 

// Function to print the second 
// smallest element 
static void print2smallest(Node head) 
{ 
    int first = int.MaxValue,  
        second = int.MaxValue; 

    Node temp = head; 
    while (temp != null) 
    { 

        if (temp.data < first) 
        { 
            second = first; 
            first = temp.data; 
        } 

        // If current node's data is in between 
        // first and second then update second 
        else if (temp.data < second &&  
                 temp.data != first) 
            second = temp.data; 

        temp = temp.next; 
    } 

    if (second == int.MaxValue) 
        Console.Write("There is no second smallest element\n"); 
    else
        Console.Write("The second smallest element is " +  
                                                 second); 
} 

// Driver code 
public static void Main(String[] args) 
{ 
    Node start = null; 

    /* The constructed linked list is:  
    12 -> 35 -> 1 -> 10 -> 34 -> 1 */
    start = push(start, 1); 
    start = push(start, 34); 
    start = push(start, 10); 
    start = push(start, 1); 
    start = push(start, 35); 
    start = push(start, 12); 

    print2smallest(start); 
} 
} 

// This code is contributed by Rajput-Ji 

```

**Output:**

```
The second smallest element is 10

```

**时间复杂度**：`O(n)`



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。