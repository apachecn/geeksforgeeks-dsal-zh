# 使用链接列表实现行程编码的程序

给定链接列表作为输入。 任务是使用[游程长度编码](https://www.geeksforgeeks.org/run-length-encoding/)对给定的链表进行编码。 就是说，要用一个字符代替一个连续的字符，然后加上计数。

例如，在游程编码中，“ a-> a-> a-> a-> a”将被替换为“ a-> 5”。

**注意**：对于非重复节点，请勿附加计数 1。例如，a- > b- > b 将被替换为“ a- > b- >”。 2”而不是“ a- > 1- > b- > 2”。

**示例：**

> **输入：**列表= a- > a- > a- > a- > a- > b- > r- > r- > r- >空
> **输出：** a- > 5- > b- > r- > 3- >空
> **说明 ：**
> 字符**'a'**重复 **5** 次。
> 字符**'b'**重复 **1** 次。
> 字符**'r'**重复 **3** 次。
> 因此，输出为 **a- > 5- > b- > r- > 3- > NULL** 。
> 
> **输入：** a- > a- > a- > a- > a- > a- > a- > a- > a- > a- > b- > r- > r- > r- > a- > a- > a- > NULL
> **输出：** a- > 1- > 0- > b- > r- > 3- > a- > 3- > NULL

**方法**：

*   遍历列表。
*   将第一个字符视为 **c** 。
*   将当前字符视为 **x** 。
*   如果字符与 **c** 相同，则增加计数。
*   如果字符不同，则将计数添加到列表中，然后将下一个字符添加到列表中，将计数重置为 **1** 。

## C++

```cpp

// C++ program to encode a linked list 
// using Run Length Encoding 

#include <bits/stdc++.h> 
using namespace std; 

// A linked list node 
struct Node { 
    char data; 
    struct Node* next; 
    Node(int x) 
    { 
        data = x; 
        next = NULL; 
    } 
}; 

// Function to append nodes to a list 
void append(struct Node* head_ref, char new_data) 
{ 
    struct Node* new_node = new Node(new_data); 

    struct Node* last = head_ref; 

    if (head_ref == NULL) { 
        head_ref = new_node; 
        return; 
    } 

    while (last->next != NULL) 
        last = last->next; 

    last->next = new_node; 
    return; 
} 

// Function to print list 
void printList(Node* node) 
{ 
    while (node != NULL) { 
        cout << node->data << " "; 

        node = node->next; 
    } 
} 

// Function to encode the list 
void RLE(Node* head) 
{ 
    // Pointer used to traverse through 
    // all the nodes in the list 
    Node* p = head; 

    // List to store the encoded message 
    Node* temp = new Node(p->data); 

    // Store the first character in c 
    char c = p->data; 
    p = p->next; 

    // Count to count the number of 
    // continuous elements 
    int count = 1; 

    // Taverse through all the 
    // elements in the list 
    while (p != NULL) { 

        // Store the current character in x 
        char x = p->data; 

        // If the characters are same 
        if (c == x) 
            // Increment count 
            count++; 
        // Else 
        else { 

            // If the count is greater than 1 
            if (count > 1) { 

                // Append the count to list 
                if (count > 9) 
                    append(temp, '0' + (count / 10)); 

                append(temp, '0' + (count % 10)); 
            } 

            // Reset the count 
            count = 1; 

            // Add the next character 
            // to the list 
            append(temp, x); 

            // Take the character to check as 
            // the current character 
            c = x; 
        } 
        p = p->next; 
    } 

    // Add the final count 
    if (count != 0) 
        append(temp, '0' + count); 

    // Print the list 
    printList(temp); 
} 

// Driver code 
int main() 
{ 
    // Creating the linked list 
    Node* head = new Node('a'); 
    head->next = new Node('a'); 
    head->next->next = new Node('a'); 
    head->next->next->next = new Node('b'); 
    head->next->next->next->next = new Node('r'); 
    head->next->next->next->next->next = new Node('r'); 

    RLE(head); 

    return 0; 
} 

```

## Java

```java

// Java program to encode a linked list 
// using Run Length Encoding 
class GFG  
{ 

// A linked list node 
static class Node  
{ 
    char data; 
    Node next; 
}; 

// Utility function to create a new Node 
static Node newNode(char data) 
{ 
    Node temp = new Node(); 
    temp.data = data; 
    temp.next = null; 

    return temp; 
} 

// Function to append nodes to a list 
static void append(Node head_ref, char new_data) 
{ 
    Node new_node = newNode(new_data); 

    Node last = head_ref; 

    if (head_ref == null) 
    { 
        head_ref = new_node; 
        return; 
    } 

    while (last.next != null) 
        last = last.next; 

    last.next = new_node; 
    return; 
} 

// Function to print list 
static void printList(Node node) 
{ 
    while (node != null) 
    { 
        System.out.print(node.data+" "); 

        node = node.next; 
    } 
} 

// Function to encode the list 
static void RLE(Node head) 
{ 
    // Pointer used to traverse through 
    // all the nodes in the list 
    Node p = head; 

    // List to store the encoded message 
    Node temp = newNode(p.data); 

    // Store the first character in c 
    char c = p.data; 
    p = p.next; 

    // Count to count the number of 
    // continuous elements 
    int count = 1; 

    // Taverse through all the 
    // elements in the list 
    while (p != null) 
    { 

        // Store the current character in x 
        char x = p.data; 

        // If the characters are same 
        if (c == x) 
            // Increment count 
            count++; 
        // Else 
        else 
        { 

            // If the count is greater than 1 
            if (count > 1)  
            { 

                // Append the count to list 
                if (count > 9) 
                    append(temp, (char) ('0' + (count / 10))); 

                append(temp, (char) ('0' + (count % 10))); 
            } 

            // Reset the count 
            count = 1; 

            // Add the next character 
            // to the list 
            append(temp, x); 

            // Take the character to check as 
            // the current character 
            c = x; 
        } 
        p = p.next; 
    } 

    // Add the final count 
    if (count != 0) 
        append(temp, (char) ('0' + count)); 

    // Print the list 
    printList(temp); 
} 

// Driver code 
public static void main(String[] args)  
{ 
    // Creating the linked list 
    Node head = newNode('a'); 
    head.next = newNode('a'); 
    head.next.next = newNode('a'); 
    head.next.next.next = newNode('b'); 
    head.next.next.next.next = newNode('r'); 
    head.next.next.next.next.next = newNode('r'); 

    RLE(head); 
    } 
} 

// This code has been contributed by 29AjayKumar 

```

## C#

```cs

// C# program to encode a linked list 
// using Run Length Encoding 
using System; 

class GFG  
{ 

// A linked list node 
public class Node  
{ 
    public char data; 
    public Node next; 
}; 

// Utility function to create a new Node 
static Node newNode(char data) 
{ 
    Node temp = new Node(); 
    temp.data = data; 
    temp.next = null; 

    return temp; 
} 

// Function to append nodes to a list 
static void append(Node head_ref, char new_data) 
{ 
    Node new_node = newNode(new_data); 

    Node last = head_ref; 

    if (head_ref == null) 
    { 
        head_ref = new_node; 
        return; 
    } 

    while (last.next != null) 
        last = last.next; 

    last.next = new_node; 
    return; 
} 

// Function to print list 
static void printList(Node node) 
{ 
    while (node != null) 
    { 
        Console.Write(node.data+" "); 

        node = node.next; 
    } 
} 

// Function to encode the list 
static void RLE(Node head) 
{ 
    // Pointer used to traverse through 
    // all the nodes in the list 
    Node p = head; 

    // List to store the encoded message 
    Node temp = newNode(p.data); 

    // Store the first character in c 
    char c = p.data; 
    p = p.next; 

    // Count to count the number of 
    // continuous elements 
    int count = 1; 

    // Taverse through all the 
    // elements in the list 
    while (p != null) 
    { 

        // Store the current character in x 
        char x = p.data; 

        // If the characters are same 
        if (c == x) 

            // Increment count 
            count++; 

        // Else 
        else
        { 

            // If the count is greater than 1 
            if (count > 1)  
            { 

                // Append the count to list 
                if (count > 9) 
                    append(temp, (char) ('0' + (count / 10))); 

                append(temp, (char) ('0' + (count % 10))); 
            } 

            // Reset the count 
            count = 1; 

            // Add the next character 
            // to the list 
            append(temp, x); 

            // Take the character to check as 
            // the current character 
            c = x; 
        } 
        p = p.next; 
    } 

    // Add the final count 
    if (count != 0) 
        append(temp, (char) ('0' + count)); 

    // Print the list 
    printList(temp); 
} 

// Driver code 
public static void Main()  
{ 
    // Creating the linked list 
    Node head = newNode('a'); 
    head.next = newNode('a'); 
    head.next.next = newNode('a'); 
    head.next.next.next = newNode('b'); 
    head.next.next.next.next = newNode('r'); 
    head.next.next.next.next.next = newNode('r'); 

    RLE(head); 
} 
} 

/* This code contributed by PrinciRaj1992 */

```

**Output:**

```
a 3 b r 2

```

**就地转换**：此处的想法是根据字符的频率来修改现有列表，而不是在系统强制执行空间限制的情况下创建新列表。

1.  遍历列表。
2.  比较当前字符和下一个字符。 如果相同，则增加计数值。
3.  删除频率大于 2 的节点。
4.  如果字符不同，则更新计数值。

```

// C++ program implementing run length encoding 
#include<stdio.h> 
#include<stdlib.h> 

struct Node 
{ 
    char data; 
    struct Node* next; 
    Node(int x) 
    { 
        data = x; 
        next = NULL; 
    } 
}; 

// Function to add node to the list 
Node* insert (Node *head, int data) 
{ 
    if (head == NULL) 
        return new Node(data); 
    head->next = insert(head->next, data); 
    return head; 
} 

// Function to print the list 
void printList (Node* head) 
{ 
    while (head != NULL) 
    { 
        printf ("%c ",head->data); 
        head = head->next; 
    } 
    return; 
} 

void runLengthEncode (Node* head) 
{ 
    Node* temp = NULL; 
    Node* ptr = NULL; 
    int count = 0; //count the number of characters 

    temp = head; 
    while (temp != NULL) 
    { 
        ptr = temp; 
        count = 1; 
        //check if current data and next data is same.If same, then increment count 
        while (temp->next != NULL && 
                temp->data == temp->next->data) 
        { 
            count++; 
            if (count > 2) 
            { 
                // delete only when the node value is repeated more than 
                // twice. 
                ptr->next = temp->next; 
                free(temp); 
                temp = ptr; 
            } 
            temp = temp->next; 
        } 

        // update only when the node value is repeated more than one time. 
        if (count > 1) 
            temp->data = count + '0'; 
        temp = temp->next; 
    } 
    return; 
} 

// Driver code 
int main() 
{ 
    // Creating the linked list 
    Node* head = new Node('a'); 
    head->next = new Node('a'); 
    head->next->next = new Node('a'); 
    head->next->next->next = new Node('b'); 
    head->next->next->next->next = new Node('r'); 
    head->next->next->next->next->next = new Node('r'); 

    runLengthEncode (head); 
    printList (head); 
    return 0; 
} 

```

**Output:**

```
a 3 b r 2

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。