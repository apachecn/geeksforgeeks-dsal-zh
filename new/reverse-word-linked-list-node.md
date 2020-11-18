# 反转链接列表节点

> 原文：[https://www.geeksforgeeks.org/reverse-word-linked-list-node/](https://www.geeksforgeeks.org/reverse-word-linked-list-node/)

中的每个单词

给定一个字符串链接列表，我们需要反转给定链接列表中字符串的每个单词。

例子：

```
Input: geeksforgeeks a computer science portal for geeks 
Output: skeegrofskeeg a retupmoc ecneics latrop rof skeeg

Input: Publish your own articles on geeksforgeeks
Output: hsilbuP ruoy nwo selcitra no skeegrofskeeg 

```

使用循环将列表迭代到 null，然后从每个节点获取字符串并反转字符串。

## C++

```cpp

// C++ program to reverse each word 
// in a linked list 
#include <bits/stdc++.h> 
using namespace std; 

// Linked list Node structure 
struct Node { 
    string c; 
    struct Node* next; 
}; 

// Function to create newNode 
// in a linked list 
struct Node* newNode(string c) 
{ 
    Node* temp = new Node; 
    temp->c = c; 
    temp->next = NULL; 
    return temp; 
}; 

// reverse each node data 
void reverse_word(string& str) 
{ 
    reverse(str.begin(), str.end()); 
} 

void reverse(struct Node* head) 
{ 
    struct Node* ptr = head; 

    // iterate each node and call reverse_word 
    // for each node data 
    while (ptr != NULL) { 
        reverse_word(ptr->c); 
        ptr = ptr->next; 
    } 
} 

// printing linked list 
void printList(struct Node* head) 
{ 
    while (head != NULL) { 
        cout << head->c << " "; 
        head = head->next; 
    } 
} 

// Driver program 
int main() 
{ 
    Node* head = newNode("Geeksforgeeks"); 
    head->next = newNode("a"); 
    head->next->next = newNode("computer"); 
    head->next->next->next = newNode("science"); 
    head->next->next->next->next = newNode("portal"); 
    head->next->next->next->next->next = newNode("for"); 
    head->next->next->next->next->next->next = newNode("geeks"); 

    cout << "List before reverse: \n"; 
    printList(head); 

    reverse(head); 

    cout << "\n\nList after reverse: \n"; 
    printList(head); 

    return 0; 
} 

```

## Java

```java

// Java program to reverse each word  
// in a linked list  
class GFG 
{ 

// Linked list Node ure  
static class Node 
{  
    String c;  
    Node next;  
};  

// Function to create newNode  
// in a linked list  
static Node newNode(String c)  
{  
    Node temp = new Node();  
    temp.c = c;  
    temp.next = null;  
    return temp;  
};  

// reverse each node data  
static String reverse_word(String str)  
{  
    String s = ""; 
    for(int i = 0; i < str.length(); i++) 
    s = str.charAt(i) + s; 
    return s; 
}  

static Node reverse( Node head)  
{  
    Node ptr = head;  

    // iterate each node and call reverse_word  
    // for each node data  
    while (ptr != null) 
    {  
        ptr.c = reverse_word(ptr.c);  
        ptr = ptr.next;  
    }  
    return head; 
}  

// printing linked list  
static void printList( Node head)  
{  
    while (head != null) 
    {  
        System.out.print( head.c + " ");  
        head = head.next;  
    }  
}  

// Driver program  
public static void main(String args[]) 
{  
    Node head = newNode("Geeksforgeeks");  
    head.next = newNode("a");  
    head.next.next = newNode("computer");  
    head.next.next.next = newNode("science");  
    head.next.next.next.next = newNode("portal");  
    head.next.next.next.next.next = newNode("for");  
    head.next.next.next.next.next.next = newNode("geeks");  

    System.out.print( "List before reverse: \n");  
    printList(head);  

    head = reverse(head);  

    System.out.print( "\n\nList after reverse: \n");  
    printList(head);  

}  
} 

// This code is contributed by Arnab Kundu 

```

## Python3

```py

# Python3 program to reverse each word  
# in a linked list  

# Node of a linked list  
class Node:  
    def __init__(self, next = None, data = None):  
        self.next = next
        self.data = data  

# Function to create newNode  
# in a linked list  
def newNode(c) : 

    temp = Node()  
    temp.c = c  
    temp.next = None
    return temp  

# reverse each node data  
def reverse_word(str) : 
    s = "" 
    i = 0
    while(i < len(str) ): 
        s = str[i] + s 
        i = i + 1
    return s 

def reverse( head) : 
    ptr = head  

    # iterate each node and call reverse_word  
    # for each node data  
    while (ptr != None): 
        ptr.c = reverse_word(ptr.c)  
        ptr = ptr.next

    return head 

# printing linked list  
def printList( head) : 

    while (head != None): 
        print( head.c ,end = " ")  
        head = head.next

# Driver program  
head = newNode("Geeksforgeeks")  
head.next = newNode("a")  
head.next.next = newNode("computer")  
head.next.next.next = newNode("science")  
head.next.next.next.next = newNode("portal")  
head.next.next.next.next.next = newNode("for")  
head.next.next.next.next.next.next = newNode("geeks")  

print( "List before reverse: ")  
printList(head)  

head = reverse(head)  

print( "\n\nList after reverse: ")  
printList(head)  

# This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# program to reverse each word  
// in a linked list 
using System; 

class GFG  
{  

    // Linked list Node ure  
    public class Node  
    {  
        public String c;  
        public Node next;  
    };  

    // Function to create newNode  
    // in a linked list  
    static Node newNode(String c)  
    {  
        Node temp = new Node();  
        temp.c = c;  
        temp.next = null;  
        return temp;  
    }  

    // reverse each node data  
    static String reverse_word(String str)  
    {  
        String s = "";  
        for(int i = 0; i < str.Length; i++)  
            s = str[i] + s;  
        return s;  
    }  

    static Node reverse( Node head)  
    {  
        Node ptr = head;  

        // iterate each node and call reverse_word  
        // for each node data  
        while (ptr != null)  
        {  
            ptr.c = reverse_word(ptr.c);  
            ptr = ptr.next;  
        }  
        return head;  
    }  

    // printing linked list  
    static void printList( Node head)  
    {  
        while (head != null)  
        {  
            Console.Write( head.c + " ");  
            head = head.next;  
        }  
    }  

    // Driver program  
    public static void Main(String []args)  
    {  
        Node head = newNode("Geeksforgeeks");  
        head.next = newNode("a");  
        head.next.next = newNode("computer");  
        head.next.next.next = newNode("science");  
        head.next.next.next.next = newNode("portal");  
        head.next.next.next.next.next = newNode("for");  
        head.next.next.next.next.next.next = newNode("geeks");  

        Console.Write( "List before reverse: \n");  
        printList(head);  

        head = reverse(head);  

        Console.Write( "\n\nList after reverse: \n");  
        printList(head);  

    }  
}  

// This code contributed by Rajput-Ji 

```

**Output:**

```
List before reverse: 
Geeksforgeeks a computer science portal for geeks 

List after reverse: 
skeegrofskeeG a retupmoc ecneics latrop rof skeeg

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。