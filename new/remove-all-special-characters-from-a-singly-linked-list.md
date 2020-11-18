# 从单个链接列表

中删除所有特殊字符

给定一个单链表，其中每个节点代表一个包含特殊字符的字符，任务是从链表中删除所有出现的特殊字符，以便在链表中仅出现有效字符。

**示例：**

> **输入：**列表=（--> G-> E-> E-> *-> K-> S-> *-> NULL
> **输出：** G-> E-> E-> K-> S-> NULL
> 
> **输入：** A-> B-> C-> *-> @->空
> **输出：** A-> B-> C-> NULL

**方法：**遍历链表，如果当前节点的数据是特殊字符，则使前一个节点的下一个指向当前节点的下一个。 对具有特殊字符的每个节点执行此操作，最后打印更新的列表。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation of the approach 
#include <iostream> 
using namespace std; 

// Structure for the node 
// of the linked list 
struct node { 
    char data; 
    node* next; 
}; 

// Utility function to add a new 
// node to the linked list 
node* add(char data) 
{ 
    node* newnode = new node; 

    // Assign the data to the data part 
    // and assign NULL to the address part 
    newnode->data = data; 
    newnode->next = NULL; 
    return newnode; 
} 

// Function to print the linked list 
void print(node* head) 
{ 
    while (head != NULL) { 
        cout << head->data << " -> "; 
        head = head->next; 
    } 
    cout << "NULL"; 
} 

// Function that returns true if 
// ch is a special character 
bool isSpecialChar(char ch) 
{ 

    // If lower-case character 
    if (ch >= 'a' && ch <= 'z') 
        return false; 

    // If upper-case character 
    if (ch >= 'A' && ch <= 'Z') 
        return false; 

    // If digit 
    if (ch >= '0' && ch <= '9') 
        return false; 

    // ch is a special character 
    return true; 
} 

// Function to remove the special 
// characters from the linked list 
node* removeFromLL(node* head) 
{ 

    // Declare two variables curr and 
    // prev both pointing to head 
    node *curr = head, *prev = head; 

    // The following loop removes special 
    // characters from the head of the linked list 
    // In case the special character is present at 
    // the head of the linked list, make head point 
    // to the next valid character 
    while (curr != NULL && isSpecialChar(curr->data)) { 
        node* temp = curr; 
        head = curr->next; 
        curr = curr->next; 
        delete temp; 
    } 

    // Make prev point to head 
    prev = head; 

    // Repeat the process for 
    // the entire Linked list 
    while (curr != NULL) { 

        // Repeat the process for all the elements 
        // of linked list, in case a special character 
        // is encountered then make the previous valid 
        // character point to the next valid character 
        // and remove the current node from the linked list 
        while (curr != NULL && isSpecialChar(curr->data)) { 
            node* temp = curr; 
            prev->next = curr->next; 
            curr = curr->next; 
            delete temp; 
        } 

        // If the end is reached 
        if (curr == NULL) 
            break; 
        prev = curr; 
        curr = curr->next; 
    } 
    return head; 
} 

// Driver code 
int main() 
{ 

    // Create the linked list 
    node* head = NULL; 
    head = add('('); 
    head->next = add('G'); 
    head->next->next = add('E'); 
    head->next->next->next = add('E'); 
    head->next->next->next->next = add('*'); 
    head->next->next->next->next->next = add('K'); 
    head->next->next->next->next->next->next = add('S'); 
    head->next->next->next->next->next->next->next = add('*'); 

    // Remove the special characters 
    // from the linked list 
    head = removeFromLL(head); 

    // Print the updated list 
    print(head); 

    return 0; 
} 

```

## Java

```java

// Java implementation of the approach 
class GFG 
{ 

// Structure for the node 
// of the linked list 
static class node 
{ 
    char data; 
    node next; 
}; 

// Utility function to add a new 
// node to the linked list 
static node add(char data) 
{ 
    node newnode = new node(); 

    // Assign the data to the data part 
    // and assign null to the address part 
    newnode.data = data; 
    newnode.next = null; 
    return newnode; 
} 

// Function to print the linked list 
static void print(node head) 
{ 
    while (head != null)  
    { 
        System.out.print(head.data + " -> "); 
        head = head.next; 
    } 
    System.out.print("null"); 
} 

// Function that returns true if 
// ch is a special character 
static boolean isSpecialChar(char ch) 
{ 

    // If lower-case character 
    if (ch >= 'a' && ch <= 'z') 
        return false; 

    // If upper-case character 
    if (ch >= 'A' && ch <= 'Z') 
        return false; 

    // If digit 
    if (ch >= '0' && ch <= '9') 
        return false; 

    // ch is a special character 
    return true; 
} 

// Function to remove the special 
// characters from the linked list 
static node removeFromLL(node head) 
{ 

    // Declare two variables curr and 
    // prev both pointing to head 
    node curr = head; node prev = head; 

    // The following loop removes special 
    // characters from the head of the linked list 
    // In case the special character is present at 
    // the head of the linked list, make head point 
    // to the next valid character 
    while (curr != null &&  
           isSpecialChar(curr.data))  
    { 
        node temp = curr; 
        head = curr.next; 
        curr = curr.next; 
        temp = null; 
    } 

    // Make prev point to head 
    prev = head; 

    // Repeat the process for 
    // the entire Linked list 
    while (curr != null) 
    { 

        // Repeat the process for all the elements 
        // of linked list, in case a special character 
        // is encountered then make the previous valid 
        // character point to the next valid character 
        // and remove the current node from the linked list 
        while (curr != null && 
               isSpecialChar(curr.data)) 
        { 
            node temp = curr; 
            prev.next = curr.next; 
            curr = curr.next; 
            temp = null; 
        } 

        // If the end is reached 
        if (curr == null) 
            break; 
        prev = curr; 
        curr = curr.next; 
    } 
    return head; 
} 

// Driver code 
public static void main(String[] args) 
{ 
    // Create the linked list 
    node head = null; 
    head = add('('); 
    head.next = add('G'); 
    head.next.next = add('E'); 
    head.next.next.next = add('E'); 
    head.next.next.next.next = add('*'); 
    head.next.next.next.next.next = add('K'); 
    head.next.next.next.next.next.next = add('S'); 
    head.next.next.next.next.next.next.next = add('*'); 

    // Remove the special characters 
    // from the linked list 
    head = removeFromLL(head); 

    // Print the updated list 
    print(head); 
} 
} 

// This code is contributed by PrinciRaj1992 

```

## Python3

```py

# Python3 implementation of the approach 
import math  

# Structure for the node 
# of the linked list 
class Node:  
    def __init__(self, data):  
        self.data = data  
        self.next = None

# Utility function to add a new 
# node to the linked list 
def add(data): 
    newnode = Node(data) 

    # Assign the data to the data part 
    # and assign None to the address part 
    newnode.data = data 
    newnode.next = None
    return newnode 

# Function to print the linked list 
def printlist(head): 
    while (head != None) : 
        print(head.data, end = " -> ") 
        head = head.next

    print("None") 

# Function that returns true if 
# ch is a special character 
def isSpecialChar(ch): 

    # If lower-case character 
    if (ch >= 'a' and ch <= 'z'): 
        return False

    # If upper-case character 
    if (ch >= 'A' and ch <= 'Z'): 
        return False

    # If digit 
    if (ch >= '0' and ch <= '9'): 
        return False

    # ch is a special character 
    return True

# Function to remove the special 
# characters from the linked list 
def removeFromLL(head): 

    # Declare two variables curr and 
    # prev both pointing to head 
    curr = head 
    prev = head 

    # The following loop removes special 
    # characters from the head of the linked list 
    # In case the special character is present at 
    # the head of the linked list, make head point 
    # to the next valid character 
    while (curr != None and 
           isSpecialChar(curr.data)): 
        temp = curr 
        head = curr.next
        curr = curr.next
        temp = None

    # Make prev point to head 
    prev = head 

    # Repeat the process for 
    # the entire Linked list 
    while (curr != None): 

        # Repeat the process for all the elements 
        # of linked list, in case a special character 
        # is encountered then make the previous valid 
        # character point to the next valid character 
        # and remove the current node from the linked list 
        while (curr != None and 
               isSpecialChar(curr.data)): 
            temp = curr 
            prev.next = curr.next
            curr = curr.next
            temp = None

        # If the end is reached 
        if (curr == None): 
            break
        prev = curr 
        curr = curr.next

    return head 

# Driver code 
if __name__=='__main__': 

    # Create the linked list 
    head = None
    head = add('(') 
    head.next = add('G') 
    head.next.next = add('E') 
    head.next.next.next = add('E') 
    head.next.next.next.next = add('*') 
    head.next.next.next.next.next = add('K') 
    head.next.next.next.next.next.next = add('S') 
    head.next.next.next.next.next.next.next = add('*') 

    # Remove the special characters 
    # from the linked list 
    head = removeFromLL(head) 

    # Print the updated list 
    printlist(head) 

# This code is contributed by Srathore 

```

## C#

```cs

// C# implementation of the approach 
using System; 

class GFG 
{ 

// Structure for the node 
// of the linked list 
class node 
{ 
    public char data; 
    public node next; 
}; 

// Utility function to add a new 
// node to the linked list 
static node add(char data) 
{ 
    node newnode = new node(); 

    // Assign the data to the data part 
    // and assign null to the address part 
    newnode.data = data; 
    newnode.next = null; 
    return newnode; 
} 

// Function to print the linked list 
static void print(node head) 
{ 
    while (head != null)  
    { 
        Console.Write(head.data + " -> "); 
        head = head.next; 
    } 
    Console.Write("null"); 
} 

// Function that returns true if 
// ch is a special character 
static Boolean isSpecialChar(char ch) 
{ 

    // If lower-case character 
    if (ch >= 'a' && ch <= 'z') 
        return false; 

    // If upper-case character 
    if (ch >= 'A' && ch <= 'Z') 
        return false; 

    // If digit 
    if (ch >= '0' && ch <= '9') 
        return false; 

    // ch is a special character 
    return true; 
} 

// Function to remove the special 
// characters from the linked list 
static node removeFromLL(node head) 
{ 

    // Declare two variables curr and 
    // prev both pointing to head 
    node curr = head; node prev = head; 

    // The following loop removes special 
    // characters from the head of the linked list 
    // In case the special character is present at 
    // the head of the linked list, make head point 
    // to the next valid character 
    while (curr != null &&  
           isSpecialChar(curr.data))  
    { 
        node temp = curr; 
        head = curr.next; 
        curr = curr.next; 
        temp = null; 
    } 

    // Make prev point to head 
    prev = head; 

    // Repeat the process for 
    // the entire Linked list 
    while (curr != null) 
    { 

        // Repeat the process for all the elements 
        // of linked list, in case a special character 
        // is encountered then make the previous valid 
        // character point to the next valid character 
        // and remove the current node from the linked list 
        while (curr != null && 
               isSpecialChar(curr.data)) 
        { 
            node temp = curr; 
            prev.next = curr.next; 
            curr = curr.next; 
            temp = null; 
        } 

        // If the end is reached 
        if (curr == null) 
            break; 
        prev = curr; 
        curr = curr.next; 
    } 
    return head; 
} 

// Driver code 
public static void Main(String[] args) 
{ 
    // Create the linked list 
    node head = null; 
    head = add('('); 
    head.next = add('G'); 
    head.next.next = add('E'); 
    head.next.next.next = add('E'); 
    head.next.next.next.next = add('*'); 
    head.next.next.next.next.next = add('K'); 
    head.next.next.next.next.next.next = add('S'); 
    head.next.next.next.next.next.next.next = add('*'); 

    // Remove the special characters 
    // from the linked list 
    head = removeFromLL(head); 

    // Print the updated list 
    print(head); 
} 
} 

// This code is contributed by PrinciRaj1992 

```

**Output:**

```
G -> E -> E -> K -> S -> NULL

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。