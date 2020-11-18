# 查找通过链接链接列表

的 k 个连续节点形成的字符串

给定一个整数 **K** 和一个链表，其中每个节点都存储一个字符。 任务是加入链表的每个 **K** 个连续节点，以形成一个单词。 最后，打印通过连接这些单词获得的字符串（以空格分隔）。

**示例：**

> **输入：**列表='a'->'b'->'c'->'d'->'e'-> NULL，k = 3
> **输出：** abc de
> 前三个节点形成第一个单词“ abc”
> ，后两个节点形成第二个单词“ de”。
> 
> **输入：**列表='a'->'b'->'c'->'d'->'e'->'f'-> NULL，k = 2
> **输出：** ab cd ef

**方法：**想法是遍历链表，并在每个结点处添加字符，直到到目前为止形成的单词。 跟踪遍历的节点数，当计数等于 k 时，将到目前为止形成的单词添加到结果字符串中，将单词重置为空字符串，并将计数重置为零。 重复此操作，直到没有遍历整个链表。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation of the approach 
#include <bits/stdc++.h> 
using namespace std; 

// Structure of a node 
struct Node { 
    char data; 
    Node* next; 
}; 

// Function to get a new node 
Node* getNode(char data) 
{ 
    // Allocate space 
    Node* newNode = new Node; 

    // Put in data 
    newNode->data = data; 
    newNode->next = NULL; 
    return newNode; 
} 

// Function to find string formed by joining words 
// obtained by joining k consecutive nodes of 
// linked list. 
string findKWordString(Node* head, int k) 
{ 
    // Stores the final string 
    string ans = ""; 

    // Keep track of the number of 
    // nodes traversed 
    int cnt = 0; 

    // Stores the word formed by k consecutive 
    // nodes of the linked list 
    string word = ""; 

    while (head) { 

        // Check if k nodes are traversed 
        // If yes then add the word obtained 
        // to the result string 
        if (cnt == k) { 
            if (ans != "") { 
                ans = ans + " "; 
            } 

            ans = ans + word; 
            word = ""; 
            cnt = 0; 
        } 

        // Add the current character to the word 
        // formed so far and increase the count 
        word = word + string(1, head->data); 
        cnt++; 
        head = head->next; 
    } 

    // Add the final word to the result 
    // Length of the final word can be less than k 
    if (ans != " ") { 
        ans = ans + " "; 
    } 
    ans = ans + word; 

    return ans; 
} 

// Driver code 
int main() 
{ 

    // Create list: a -> b -> c -> d -> e 
    Node* head = getNode('a'); 
    head->next = getNode('b'); 
    head->next->next = getNode('c'); 
    head->next->next->next = getNode('d'); 
    head->next->next->next->next = getNode('e'); 

    int k = 3; 

    cout << findKWordString(head, k); 

    return 0; 
} 

```

## Java

```java

// Java implementation of the approach 
class GFG{ 

// Class of a node 
static class Node 
{ 
    char data; 
    Node next; 
}; 

// Function to get a new node 
static Node getNode(char data) 
{ 

    // Allocate space 
    Node newNode = new Node(); 

    // Put in data 
    newNode.data = data; 
    newNode.next = null; 
    return newNode; 
} 

// Function to find string formed by  
// joining words obtained by joining  
// k consecutive nodes of linked list. 
static String findKWordString(Node head, int k) 
{ 

    // Stores the final string 
    String ans = ""; 

    // Keep track of the number of 
    // nodes traversed 
    int cnt = 0; 

    // Stores the word formed by k consecutive 
    // nodes of the linked list 
    String word = ""; 

    while (head != null) 
    { 

        // Check if k nodes are traversed 
        // if yes then add the word obtained 
        // to the result String 
        if (cnt == k) 
        { 
            if (ans != "")  
            { 
                ans = (ans + " "); 
            } 

            ans = ans + word; 
            word = ""; 
            cnt = 0; 
        } 

        // Add the current character to the word 
        // formed so far and increase the count 
        word = word + head.data; 
        cnt++; 
        head = head.next; 
    } 

    // Add the final word to the result 
    // Length of the final word can be 
    // less than k 
    if (ans != " ") 
    { 
        ans = (ans + " "); 
    } 
    ans = ans + word; 
    return ans; 
} 

// Driver code 
public static void main(String[] args) 
{ 

    // Create list: a.b.c.d.e 
    Node head = getNode('a'); 
    head.next = getNode('b'); 
    head.next.next = getNode('c'); 
    head.next.next.next = getNode('d'); 
    head.next.next.next.next = getNode('e'); 

    int k = 3; 

    System.out.print(findKWordString(head, k)); 
} 
} 

// This code is contributed by GauravRajput1 

```

## C#

```cs

// C# implementation of the approach 
using System; 

class GFG{ 

// Class of a node 
class Node 
{ 
    public char data; 
    public Node next; 
}; 

// Function to get a new node 
static Node getNode(char data) 
{ 

    // Allocate space 
    Node newNode = new Node(); 

    // Put in data 
    newNode.data = data; 
    newNode.next = null; 
    return newNode; 
} 

// Function to find string formed by  
// joining words obtained by joining  
// k consecutive nodes of linked list. 
static String findKWordString(Node head, int k) 
{ 

    // Stores the final string 
    String ans = ""; 

    // Keep track of the number  
    // of nodes traversed 
    int cnt = 0; 

    // Stores the word formed by k  
    // consecutive nodes of the  
    // linked list 
    String word = ""; 

    while (head != null) 
    { 

        // Check if k nodes are traversed 
        // if yes then add the word obtained 
        // to the result String 
        if (cnt == k) 
        { 
            if (ans != "")  
            { 
                ans = (ans + " "); 
            } 

            ans = ans + word; 
            word = ""; 
            cnt = 0; 
        } 

        // Add the current character to the word 
        // formed so far and increase the count 
        word = word + head.data; 
        cnt++; 
        head = head.next; 
    } 

    // Add the readonly word to the result 
    // Length of the readonly word can be 
    // less than k 
    if (ans != " ") 
    { 
        ans = (ans + " "); 
    } 
    ans = ans + word; 
    return ans; 
} 

// Driver code 
public static void Main(String[] args) 
{ 

    // Create list: a.b.c.d.e 
    Node head = getNode('a'); 
    head.next = getNode('b'); 
    head.next.next = getNode('c'); 
    head.next.next.next = getNode('d'); 
    head.next.next.next.next = getNode('e'); 

    int k = 3; 

    Console.Write(findKWordString(head, k)); 
} 
} 

// This code is contributed by gauravrajput1 

```

**Output:**

```
abc de

```

**时间复杂度：** O（N）

**辅助空间：** O（1）



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。