# 在单链表

中查找最小和最大元素

给定 n 个节点的单链列表，并在链列表中找到最小和最大的元素。

例子：

```
Input : 15 14 13 22 17
Output : Linked list are:
        17 -> 22 -> 13 -> 14 -> 15 -> NULL
        Maximum element in linked list: 22
        Minimum element in linked list: 13

Input : 20 25 23 68 54 13 45
Output : Linked list are:
        45 -> 13 -> 54 -> 68 -> 23 -> 25 -> 20 -> NULL
        Maximum element in linked list: 68
        Minimum element in linked list: 13

```

这个想法是在不等于 NULL 的情况下遍历链接列表，并将 **max** 和 **min** 变量分别初始化为 **INT_MIN** 和 **INT_MAX** 。 之后检查一个条件，如果最大值小于头值，则将头值分配给 max 或最小值，然后将头值分配给 min，否则头值分配给 min，否则头点指向下一个节点。 继续此过程，直到 head 不等于 NULL。

## C++

```cpp

// C++ Program to find smallest and largest 
// elements in singly linked list. 
#include <bits/stdc++.h> 

using namespace std; 
/* Linked list node */
struct Node { 
    int data; 
    struct Node* next; 
}; 

// Function that returns the largest element 
// from the linked list. 
int largestElement(struct Node* head) 
{ 
    // Declare a max variable and initialize 
    // it with INT_MIN value. 
    // INT_MIN is integer type and its value 
    // is -32767 or less. 
    int max = INT_MIN; 

    // Check loop while head not equal to NULL 
    while (head != NULL) { 

        // If max is less then head->data then 
        // assign value of head->data to max 
        // otherwise node point to next node. 
        if (max < head->data) 
            max = head->data; 
        head = head->next; 
    } 
    return max; 
} 

// Function that returns smallest element 
// from the linked list. 
int smallestElement(struct Node* head) 
{ 
    // Declare a min variable and initialize 
    // it with INT_MAX value. 
    // INT_MAX is integer type and its value 
    // is 32767 or greater. 
    int min = INT_MAX; 

    // Check loop while head not equal to NULL 
    while (head != NULL) { 

        // If min is greater then head->data then 
        // assign value of head->data to min 
        // otherwise node point to next node. 
        if (min > head->data) 
            min = head->data; 

        head = head->next; 
    } 
    return min; 
} 

// Function that push the element in linked list. 
void push(struct Node** head, int data) 
{ 
    // Allocate dynamic memory for newNode. 
    struct Node* newNode =  
         (struct Node*)malloc(sizeof(struct Node)); 

    // Assign the data into newNode. 
    newNode->data = data; 

    // newNode->next assign the address of 
    // head node. 
    newNode->next = (*head); 

    // newNode become the headNode. 
    (*head) = newNode; 
} 

// Display linked list. 
void printList(struct Node* head) 
{ 
    while (head != NULL) { 
        printf("%d -> ", head->data); 
        head = head->next; 
    } 
    cout << "NULL" << endl; 
} 

// Driver program to test the functions 
int main() 
{ 
    // Start with empty list 
    struct Node* head = NULL; 

    // Using push() function to construct 
    // singly linked list 
    // 17->22->13->14->15 
    push(&head, 15); 
    push(&head, 14); 
    push(&head, 13); 
    push(&head, 22); 
    push(&head, 17); 
    cout << "Linked list is : " << endl; 

    // Call printList() function to display 
    // the linked list. 
    printList(head); 
    cout << "Maximum element in linked list:"; 

    // Call largestElement() function to get largest 
    // element in linked list. 
    cout << largestElement(head) << endl; 
    cout << "Minimum element in linked list:"; 

    // Call smallestElement() function to get smallest 
    // element in linked list. 
    cout << smallestElement(head) << endl; 

    return 0; 
} 

```

## Java

```java

// Java program to find smallest and largest  
// elements in singly linked list.  
class GfG  
{  

/* Linked list node */
static class Node 
{  
    int data;  
    Node next;  
} 
static Node head = null; 

// Function that returns the largest element  
// from the linked list.  
static int largestElement(Node head)  
{  

    // Declare a max variable and initialize  
    // it with INT_MIN value.  
    // INT_MIN is integer type and its value  
    // is -32767 or less.  
    int max = Integer.MIN_VALUE;  

    // Check loop while head not equal to NULL  
    while (head != null) 
    {  

        // If max is less then head->data then  
        // assign value of head->data to max  
        // otherwise node point to next node.  
        if (max < head.data)  
            max = head.data;  
        head = head.next;  
    }  
    return max;  
}  

// Function that returns smallest element  
// from the linked list.  
static int smallestElement(Node head)  
{  

    // Declare a min variable and initialize  
    // it with INT_MAX value.  
    // INT_MAX is integer type and its value  
    // is 32767 or greater.  
    int min = Integer.MAX_VALUE;  

    // Check loop while head not equal to NULL  
    while (head != null)  
    {  

        // If min is greater then head->data then  
        // assign value of head->data to min  
        // otherwise node point to next node.  
        if (min > head.data)  
            min = head.data;  

        head = head.next;  
    }  
    return min;  
}  

// Function that push the element in linked list.  
static void push(int data)  
{  
    // Allocate dynamic memory for newNode.  
    Node newNode = new Node();  

    // Assign the data into newNode.  
    newNode.data = data;  

    // newNode->next assign the address of  
    // head node.  
    newNode.next = (head);  

    // newNode become the headNode.  
    (head) = newNode;  
}  

// Display linked list.  
static void printList(Node head)  
{  
    while (head != null) {  
        System.out.print(head.data + " -> ");  
        head = head.next;  
    }  
    System.out.println("NULL");  
}  

// Driver  code 
public static void main(String[] args)  
{  
    // Start with empty list  
    // head = new Node();  

    // Using push() function to construct  
    // singly linked list  
    // 17->22->13->14->15  
    push( 15);  
    push( 14);  
    push( 13);  
    push( 22);  
    push( 17);  
    System.out.println("Linked list is : ") ; 

    // Call printList() function to   
    // display the linked list.  
    printList(head);  
    System.out.print("Maximum element in linked list: ");  

    // Call largestElement() function to get  
    // largest element in linked list.  
    System.out.println(largestElement(head));  
    System.out.print("Minimum element in linked list: ");  

    // Call smallestElement() function to get   
    // smallest element in linked list.  
    System.out.print(smallestElement(head));  
} 
}  

// This code is contributed by Prerna saini. 

```

## Python

```py

# Python3 program to find smallest and largest  
# elements in singly linked list.  

# Linked list node  
class Node: 

    def __init__(self): 
        self.data = None
        self.next = None

head = None

# Function that returns the largest element  
# from the linked list.  
def largestElement(head):  

    # Declare a max variable and initialize  
    # it with INT_MIN value.  
    # INT_MIN is integer type and its value  
    # is -32767 or less.  
    max = -32767

    # Check loop while head not equal to None  
    while (head != None): 

        # If max is less then head.data then  
        # assign value of head.data to max  
        # otherwise node point to next node.  
        if (max < head.data) : 
            max = head.data  
        head = head.next

    return max

# Function that returns smallest element  
# from the linked list.  
def smallestElement(head):  

    # Declare a min variable and initialize  
    # it with INT_MAX value.  
    # INT_MAX is integer type and its value  
    # is 32767 or greater.  
    min = 32767

    # Check loop while head not equal to None  
    while (head != None) : 

        # If min is greater then head.data then  
        # assign value of head.data to min  
        # otherwise node point to next node.  
        if (min > head.data) : 
            min = head.data  
        head = head.next

    return min

# Function that push the element in linked list.  
def push( data) : 

    global head 

    # Allocate dynamic memory for newNode.  
    newNode = Node()  

    # Assign the data into newNode.  
    newNode.data = data  

    # newNode.next assign the address of  
    # head node.  
    newNode.next = (head)  

    # newNode become the headNode.  
    (head) = newNode  

# Display linked list.  
def printList( head) : 

    while (head != None) : 
        print(head.data ,end= " -> ")  
        head = head.next

    print("None")  

# Driver code 

# Start with empty list  
# head = new Node()  

# Using push() function to construct  
# singly linked list  
# 17.22.13.14.15  
push( 15)  
push( 14)  
push( 13)  
push( 22)  
push( 17)  
print("Linked list is : ")  

# Call printList() function to  
# display the linked list.  
printList(head)  
print("Maximum element in linked list: ",end="")  

# Call largestElement() function to get  
# largest element in linked list.  
print(largestElement(head))  
print("Minimum element in linked list: ",end="")  

# Call smallestElement() function to get  
# smallest element in linked list.  
print(smallestElement(head),end="")  

# This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# program to find smallest and largest  
// elements in singly linked list.  
using System; 

class GfG  
{  

    /* Linked list node */
    class Node 
    {  
        public int data;  
        public Node next;  
    } 
    static Node head = null; 

    // Function that returns the largest element  
    // from the linked list.  
    static int largestElement(Node head)  
    {  

        // Declare a max variable and initialize  
        // it with INT_MIN value.  
        // INT_MIN is integer type and its value  
        // is -32767 or less.  
        int max = int.MinValue;  

        // Check loop while head not equal to NULL  
        while (head != null) 
        {  

            // If max is less then head->data then  
            // assign value of head->data to max  
            // otherwise node point to next node.  
            if (max < head.data)  
                max = head.data;  
            head = head.next;  
        }  
        return max;  
    }  

    // Function that returns smallest element  
    // from the linked list.  
    static int smallestElement(Node head)  
    {  

        // Declare a min variable and initialize  
        // it with INT_MAX value.  
        // INT_MAX is integer type and its value  
        // is 32767 or greater.  
        int min = int.MaxValue;  

        // Check loop while head not equal to NULL  
        while (head != null)  
        {  

            // If min is greater then head->data then  
            // assign value of head->data to min  
            // otherwise node point to next node.  
            if (min > head.data)  
                min = head.data;  

            head = head.next;  
        }  
        return min;  
    }  

    // Function that push the element in linked list.  
    static void push(int data)  
    {  
        // Allocate dynamic memory for newNode.  
        Node newNode = new Node();  

        // Assign the data into newNode.  
        newNode.data = data;  

        // newNode->next assign the address of  
        // head node.  
        newNode.next = (head);  

        // newNode become the headNode.  
        (head) = newNode;  
    }  

    // Display linked list.  
    static void printList(Node head)  
    {  
        while (head != null)  
        {  
            Console.Write(head.data + " -> ");  
            head = head.next;  
        }  
        Console.WriteLine("NULL");  
    }  

    // Driver code 
    public static void Main()  
    {  
        // Start with empty list  
        // head = new Node();  

        // Using push() function to construct  
        // singly linked list  
        // 17->22->13->14->15  
        push( 15);  
        push( 14);  
        push( 13);  
        push( 22);  
        push( 17);  
        Console.WriteLine("Linked list is : ") ; 

        // Call printList() function to  
        // display the linked list.  
        printList(head);  
        Console.Write("Maximum element in linked list: ");  

        // Call largestElement() function to get  
        // largest element in linked list.  
        Console.WriteLine(largestElement(head));  
        Console.Write("Minimum element in linked list: ");  

        // Call smallestElement() function to get  
        // smallest element in linked list.  
        Console.Write(smallestElement(head));  
    } 
} 

// This code is contributed by PrinciRaj1992 

```

**Output:**

```
Linked list is :
17 -> 22 -> 13 -> 14 -> 15 -> NULL
Maximum element in linked list: 22
Minimum element in linked list: 13

```

本文由 **Dharmendra kumar** 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论。

