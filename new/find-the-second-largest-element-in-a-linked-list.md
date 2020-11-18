# 在链接列表中找到第二大元素

给定整数数据的链接列表。 任务是编写一个程序，以有效地找到链表中存在的第二大元素。

**范例**：

```
Input : List = 12 -> 35 -> 1 -> 10 -> 34 -> 1
Output : The second largest element is 34.

Input : List = 10 -> 5 -> 10
Output : The second largest element is 5.

```

**简单解决方案**将首先[按降序对链表](https://www.geeksforgeeks.org/merge-sort-for-linked-list/)排序，然后从排序的链表中打印第二个元素。 该解决方案的时间复杂度为 O（nlogn）。

**更好的解决方案**是遍历链接列表两次。 在第一个遍历中找到最大元素。 在第二遍历中找到小于在第一遍历中获得的元素的最大元素。 该解决方案的时间复杂度为`O(n)`。

一种更有效的**解决方案**是在单个遍历中查找第二大元素。

以下是完成此操作的完整算法：

```
1) Initialize two variables first and second to INT_MIN as,
   first = second = INT_MIN
2) Start traversing the Linked List,
   a) If the current element in Linked List say list[i] is greater
      than first. Then update first and second as,
      second = first
      first = list[i]
   b) If the current element is in between first and second,
      then update second to store the value of current variable as
      second = list[i]
3) Return the value stored in second node.

```

下面是上述方法的实现：

## C++

```cpp

// C++ program to print second largest 
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
    /* allocate node */
    struct Node* new_node = (struct Node*)malloc(sizeof(struct Node)); 

    /* put in the data */
    new_node->data = new_data; 

    /* link the old list off the new node */
    new_node->next = (*head_ref); 

    /* move the head to point to the new node */
    (*head_ref) = new_node; 
} 

// Function to count size of list 
int listSize(struct Node* node) 
{ 
    int count = 0; 

    while (node != NULL) { 
        count++; 

        node = node->next; 
    } 

    return count; 
} 

// Function to print the second 
// largest element 
void print2largest(struct Node* head) 
{ 
    int i, first, second; 

    int list_size = listSize(head); 

    /* There should be atleast two elements */
    if (list_size < 2) { 
        cout << "Invalid Input"; 
        return; 
    } 

    first = second = INT_MIN; 

    struct Node* temp = head; 

    while (temp != NULL) { 
        if (temp->data > first) { 
            second = first; 
            first = temp->data; 
        } 

        // If current node's data is in between 
        // first and second then update second 
        else if (temp->data > second && temp->data != first) 
            second = temp->data; 

        temp = temp->next; 
    } 

    if (second == INT_MIN) 
        cout << "There is no second largest element\n"; 
    else
        cout << "The second largest element is " << second; 
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

    print2largest(start); 

    return 0; 
} 

```

## Java

```java

// Java program to print second largest  
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
static Node push( Node head_ref, int new_data)  
{  
    // allocate node / 
    Node new_node = new Node();  

    // put in the data / 
    new_node.data = new_data;  

    // link the old list off the new node / 
    new_node.next = (head_ref);  

    // move the head to point to the new node / 
    (head_ref) = new_node;  
    return head_ref; 
}  

// Function to count size of list  
static int listSize( Node node)  
{  
    int count = 0;  

    while (node != null) 
    {  
        count++;  

        node = node.next;  
    }  

    return count;  
}  

// Function to print the second  
// largest element  
static void print2largest( Node head)  
{  
    int i, first, second;  

    int list_size = listSize(head);  

    // There should be atleast two elements / 
    if (list_size < 2)  
    {  
        System.out.print("Invalid Input");  
        return;  
    }  

    first = second = Integer.MIN_VALUE;  

    Node temp = head;  

    while (temp != null) 
    {  
        if (temp.data > first)  
        {  
            second = first;  
            first = temp.data;  
        }  

        // If current node's data is in between  
        // first and second then update second  
        else if (temp.data > second && temp.data != first)  
            second = temp.data;  

        temp = temp.next;  
    }  

    if (second == Integer.MIN_VALUE)  
        System.out.print( "There is no second largest element\n");  
    else
        System.out.print ("The second largest element is " + second);  
}  

// Driver program to test above function  
public static void main(String args[]) 
{  
    Node start = null;  

    // The constructed linked list is:  
    //12 . 35 . 1 . 10 . 34 . 1  
    start=push(start, 1);  
    start=push(start, 34);  
    start=push(start, 10);  
    start=push(start, 1);  
    start=push(start, 35);  
    start=push(start, 12);  

    print2largest(start);  
} 
}  

// This code is contributed by Arnab Kundu 

```

## Python3

```py

# Python3 program to print second largest  
# value in a linked list  

# A linked list node  
class Node : 
    def __init__(self): 
        self.data = 0
        self.next = None

# Function to add a node at the  
# beginning of Linked List  
def push( head_ref, new_data) : 

    # allocate node / 
    new_node = Node()  

    # put in the data / 
    new_node.data = new_data  

    # link the old list off the new node / 
    new_node.next = (head_ref)  

    # move the head to point to the new node / 
    (head_ref) = new_node  
    return head_ref 

# Function to count size of list  
def listSize( node):  

    count = 0
    while (node != None): 
        count = count + 1

        node = node.next

    return count  

# Function to print the second  
# largest element  
def print2largest( head):  

    i = 0
    first = 0
    second = 0

    list_size = listSize(head)  

    # There should be atleast two elements / 
    if (list_size < 2) : 

        print("Invalid Input")  
        return

    first = second = -323767
    temp = head  

    while (temp != None): 

        if (temp.data > first) : 
            second = first  
            first = temp.data  

        # If current node's data is in between  
        # first and second then update second  
        elif (temp.data > second and temp.data != first) : 
            second = temp.data  

        temp = temp.next

    if (second == -323767) : 
        print( "There is no second largest element\n")  
    else: 
        print ("The second largest element is " , second)  

# Driver code 

start = None

# The constructed linked list is:  
# 12 . 35 . 1 . 10 . 34 . 1  
start = push(start, 1)  
start = push(start, 34)  
start = push(start, 10)  
start = push(start, 1)  
start = push(start, 35)  
start = push(start, 12)  

print2largest(start)  

# This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# program to print second largest  
// value in a linked list  
using System; 

class GFG 
{ 

// A linked list node  
public class Node  
{  
    public int data;  
    public Node next;  
};  

// Function to add a node at the  
// beginning of Linked List  
static Node push( Node head_ref, int new_data)  
{  
    // allocate node  
    Node new_node = new Node();  

    // put in the data  
    new_node.data = new_data;  

    // link the old list off the new node  
    new_node.next = (head_ref);  

    // move the head to point to the new node  
    (head_ref) = new_node;  
    return head_ref; 
}  

// Function to count size of list  
static int listSize( Node node)  
{  
    int count = 0;  

    while (node != null) 
    {  
        count++;  

        node = node.next;  
    }  

    return count;  
}  

// Function to print the second  
// largest element  
static void print2largest(Node head)  
{  
    int first, second;  

    int list_size = listSize(head);  

    // There should be atleast two elements 
    if (list_size < 2)  
    {  
        Console.Write("Invalid Input");  
        return;  
    }  

    first = second = int.MinValue;  

    Node temp = head;  

    while (temp != null) 
    {  
        if (temp.data > first)  
        {  
            second = first;  
            first = temp.data;  
        }  

        // If current node's data is in between  
        // first and second then update second  
        else if (temp.data > second &&  
                 temp.data != first)  
            second = temp.data;  

        temp = temp.next;  
    }  

    if (second == int.MinValue)  
        Console.Write( "There is no second" + 
                       " largest element\n");  
    else
        Console.Write("The second largest " +  
                      "element is " + second);  
}  

// Driver Code 
public static void Main(String []args) 
{  
    Node start = null;  

    // The constructed linked list is:  
    //12 . 35 . 1 . 10 . 34 . 1  
    start = push(start, 1);  
    start = push(start, 34);  
    start = push(start, 10);  
    start = push(start, 1);  
    start = push(start, 35);  
    start = push(start, 12);  

    print2largest(start);  
} 
}  

// This code is contributed by 29AjayKumar 

```

**Output:**

```
The second largest element is 34

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。