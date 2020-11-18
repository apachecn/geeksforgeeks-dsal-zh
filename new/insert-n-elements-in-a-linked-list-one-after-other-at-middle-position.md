# 在链接列表的中间位置一个接一个地插入 N 个元素

> 原文：[https://www.geeksforgeeks.org/insert-n-elements-in-a-linked-list-one-after-other-at-middle-position/](https://www.geeksforgeeks.org/insert-n-elements-in-a-linked-list-one-after-other-at-middle-position/)

给定 N 个元素的数组。 任务是将给定元素一个接一个地插入链表的中间位置。 每个插入操作应占用`O(1)`时间复杂度。

**示例**：

> **输入**：arr [] = {1、2、3、4、5}
> **输出**：1-> 3-> 5-> 4 -> 2->空
> 1->空
> 1-> 2->空
> 1-> 3-> 2->空
> 1-> 3-> 4-> 2->空
> 1-> 3-> 5-> 4-> 2 -> NULL
> 
> **输入**：arr [] = {5，4，1，2}
> **输出**：5-> 1-> 2-> 4-[ > NULL

**方法**：有两种情况：

1.  列表中存在的元素数少于 2。

2.  列表中存在的元素数大于 2。

    *   甚至已经存在的元素数为 **N** ，然后将新元素插入到中间位置，即**（N / 2）+ 1** 。

    *   已经存在的元素数为奇数，然后将新元素插入到当前中间元素**（N / 2）+ 2** 旁边。

我们再增加一个指针“中间”，该指针存储当前中间元素的地址，还有一个计数器，用于计算元素总数。

如果链表中已经存在的元素少于 2 个，那么 Middle 总是指向第一个位置，我们在当前中间位置之后插入新节点。

如果链接列表中已经存在的元素大于 2，则我们在当前中间位置旁边插入新节点并增加计数器。

如果插入后元素的数量为奇数，则中间点指向新插入的节点，否则中间指针没有变化。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation of the approach 
#include <iostream> 
using namespace std; 

// Node structure 
struct Node { 

    int value; 
    struct Node* next; 
}; 

// Class to represent a node 
// of the linked list 
class LinkedList { 

private: 
    struct Node *head, *mid; 
    int count; 

public: 
    LinkedList(); 
    void insertAtMiddle(int); 
    void show(); 
}; 

LinkedList::LinkedList() 
{ 
    head = NULL; 
    mid = NULL; 
    count = 0; 
} 

// Function to insert a node in 
// the middle of the linked list 
void LinkedList::insertAtMiddle(int n) 
{ 

    struct Node* temp = new struct Node(); 
    struct Node* temp1; 

    temp->next = NULL; 
    temp->value = n; 

    // If the number of elements 
    // already present are less than 2 
    if (count < 2) { 
        if (head == NULL) { 
            head = temp; 
        } 
        else { 
            temp1 = head; 
            temp1->next = temp; 
        } 
        count++; 

        // mid points to first element 
        mid = head; 
    } 

    // If the number of elements already present 
    // are greater than 2 
    else { 

        temp->next = mid->next; 
        mid->next = temp; 
        count++; 

        // If number of elements after insertion 
        // are odd 
        if (count % 2 != 0) { 

            // mid points to the newly 
            // inserted node 
            mid = mid->next; 
        } 
    } 
} 

// Function to print the nodes 
// of the linked list 
void LinkedList::show() 
{ 

    struct Node* temp; 

    temp = head; 

    // Initializing temp to head 
    // Iterating and printing till 
    // The end of linked list 
    // That is, till temp is null 
    while (temp != NULL) { 

        cout << temp->value << " -> "; 
        temp = temp->next; 
    } 
    cout << "NULL"; 
    cout << endl; 
} 

// Driver code 
int main() 
{ 
    // Elements to be inserted one after another 
    int arr[] = { 1, 2, 3, 4, 5 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 

    LinkedList L1; 

    // Insert the elements 
    for (int i = 0; i < n; i++) 
        L1.insertAtMiddle(arr[i]); 

    // Print the nodes of the linked list 
    L1.show(); 

    return 0; 
} 

```

## Java

```java

// Java implementation of the approach  
class GFG 
{ 

// Node ure  
static class Node  
{  

    int value;  
    Node next;  
};  

// Class to represent a node  
// of the linked list  
static class LinkedList  
{  
    Node head, mid;  
    int count;  

LinkedList()  
{  
    head = null;  
    mid = null;  
    count = 0;  
}  

// Function to insert a node in  
// the middle of the linked list  
void insertAtMiddle(int n)  
{  

    Node temp = new Node();  
    Node temp1;  

    temp.next = null;  
    temp.value = n;  

    // If the number of elements  
    // already present are less than 2  
    if (count < 2)  
    {  
        if (head == null)  
        {  
            head = temp;  
        }  
        else 
        {  
            temp1 = head;  
            temp1.next = temp;  
        }  
        count++;  

        // mid points to first element  
        mid = head;  
    }  

    // If the number of elements already present  
    // are greater than 2  
    else 
    {  

        temp.next = mid.next;  
        mid.next = temp;  
        count++;  

        // If number of elements after insertion  
        // are odd  
        if (count % 2 != 0)  
        {  

            // mid points to the newly  
            // inserted node  
            mid = mid.next;  
        }  
    }  
}  

// Function to print the nodes  
// of the linked list  
void show()  
{  

    Node temp;  

    temp = head;  

    // Initializing temp to head  
    // Iterating and printing till  
    // The end of linked list  
    // That is, till temp is null  
    while (temp != null)  
    {  

        System.out.print( temp.value + " -> ");  
        temp = temp.next;  
    }  
    System.out.print( "null");  
    System.out.println(); 
}  

} 

// Driver code  
public static void main(String args[]) 
{  
    // Elements to be inserted one after another  
    int arr[] = { 1, 2, 3, 4, 5 };  
    int n = arr.length;  

    LinkedList L1=new LinkedList();  

    // Insert the elements  
    for (int i = 0; i < n; i++)  
        L1.insertAtMiddle(arr[i]);  

    // Print the nodes of the linked list  
    L1.show();  
} 
} 

// This code is contributed by Arnab Kundu 

```

## Python3

```py

# Python3 implementation of the approach  

# Node ure  
class Node:  
    def __init__(self): 
        self.value = 0
        self.next = None

# Class to represent a node  
# of the linked list  
class LinkedList:  

    def __init__(self) : 
        self.head = None
        self.mid = None
        self.count = 0

    # Function to insert a node in  
    # the middle of the linked list  
    def insertAtMiddle(self , n):  

        temp = Node()  
        temp1 = None

        temp.next = None
        temp.value = n  

        # If the number of elements  
        # already present are less than 2  
        if (self.count < 2):  

            if (self.head == None) : 

                self.head = temp  

            else: 

                temp1 = self.head  
                temp1.next = temp  

            self.count = self.count + 1

            # mid points to first element  
            self.mid = self.head  

        # If the number of elements already present  
        # are greater than 2  
        else: 

            temp.next = self.mid.next
            self.mid.next = temp  
            self.count = self.count + 1

            # If number of elements after insertion  
            # are odd  
            if (self.count % 2 != 0):  

                # mid points to the newly  
                # inserted node  
                self.mid = self.mid.next

    # Function to print the nodes  
    # of the linked list  
    def show(self):  
        temp = None

        temp = self.head  

        # Initializing temp to self.head  
        # Iterating and printing till  
        # The end of linked list  
        # That is, till temp is None  
        while (temp != None) : 

            print( temp.value, end = " -> ")  
            temp = temp.next

        print( "None")  

# Driver code  

# Elements to be inserted one after another  
arr = [ 1, 2, 3, 4, 5]  
n = len(arr)  

L1 = LinkedList()  

# Insert the elements  
for i in range(n):  
    L1.insertAtMiddle(arr[i])  

# Print the nodes of the linked list  
L1.show()  

# This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# implementation of the approach  
using System; 

class GFG 
{ 

// Node ure  
public class Node  
{  

    public int value;  
    public Node next;  
};  

// Class to represent a node  
// of the linked list  
public class LinkedList  
{  
    public Node head, mid;  
    public int count;  

public LinkedList()  
{  
    head = null;  
    mid = null;  
    count = 0;  
}  

// Function to insert a node in  
// the middle of the linked list  
public void insertAtMiddle(int n)  
{  

    Node temp = new Node();  
    Node temp1;  

    temp.next = null;  
    temp.value = n;  

    // If the number of elements  
    // already present are less than 2  
    if (count < 2)  
    {  
        if (head == null)  
        {  
            head = temp;  
        }  
        else
        {  
            temp1 = head;  
            temp1.next = temp;  
        }  
        count++;  

        // mid points to first element  
        mid = head;  
    }  

    // If the number of elements already present  
    // are greater than 2  
    else
    {  

        temp.next = mid.next;  
        mid.next = temp;  
        count++;  

        // If number of elements after insertion  
        // are odd  
        if (count % 2 != 0)  
        {  

            // mid points to the newly  
            // inserted node  
            mid = mid.next;  
        }  
    }  
}  

// Function to print the nodes  
// of the linked list  
public void show()  
{  

    Node temp;  

    temp = head;  

    // Initializing temp to head  
    // Iterating and printing till  
    // The end of linked list  
    // That is, till temp is null  
    while (temp != null)  
    {  

        Console.Write( temp.value + " -> ");  
        temp = temp.next;  
    }  
    Console.Write( "null");  
    Console.WriteLine(); 
}  

} 

// Driver code  
public static void Main(String []args) 
{  
    // Elements to be inserted one after another  
    int []arr = { 1, 2, 3, 4, 5 };  
    int n = arr.Length;  

    LinkedList L1=new LinkedList();  

    // Insert the elements  
    for (int i = 0; i < n; i++)  
        L1.insertAtMiddle(arr[i]);  

    // Print the nodes of the linked list  
    L1.show();  
} 
} 

// This code contributed by Rajput-Ji 

```

**Output:**

```
1 -> 3 -> 5 -> 4 -> 2 -> NULL

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。