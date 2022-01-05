# 将字符串转换为单链表

> 原文:[https://www . geesforgeks . org/convert-a-string-to-a-single-link-list/](https://www.geeksforgeeks.org/convert-a-string-to-a-singly-linked-list/)

给定字符串**字符串**，任务是将其转换为[单链表](https://www.geeksforgeeks.org/data-structures/linked-list/singly-linked-list/)。
**例:**

```
Input: str = "ABCDABC"
Output: A -> B -> C -> D -> A -> B -> C

Input: str = "GEEKS"
Output: G -> E -> E -> K -> S
```

**进场:**

*   创建链接列表
*   获取字符串的每个字符，并将其插入链表中的新节点
*   打印链接列表

以下是上述方法的实现:

## C++

```
// C++ program to Convert a String
// to a Singly Linked List

#include <iostream>
using namespace std;

// Structure for a Singly Linked List
struct node {
    char data;
    node* next;
};

// Function to add a new node to the Linked List
node* add(char data)
{
    node* newnode = new node;
    newnode->data = data;
    newnode->next = NULL;
    return newnode;
}

// Function to convert the string to Linked List.
node* string_to_SLL(string text, node* head)
{
    head = add(text[0]);
    node* curr = head;

    // curr pointer points to the current node
    // where the insertion should take place
    for (int i = 1; i < text.size(); i++) {
        curr->next = add(text[i]);
        curr = curr->next;
    }
    return head;
}

// Function to print the data present in all the nodes
void print(node* head)
{
    node* curr = head;
    while (curr != NULL) {
        cout << curr->data << " -> ";
        curr = curr->next;
    }
}

// Driver code
int main()
{

    string text = "GEEKS";

    node* head = NULL;
    head = string_to_SLL(text, head);

    print(head);
    return 0;
}

// This code is contributed by code_freak
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to Convert a String
// to a Singly Linked List
class GFG
{

// Structure for a Singly Linked List
static class node
{
    char data;
    node next;
};

// Function to add a new node to the Linked List
static node add(char data)
{
    node newnode = new node();
    newnode.data = data;
    newnode.next = null;
    return newnode;
}

// Function to convert the string
// to Linked List.
static node string_to_SLL(String text,
                            node head)
{
    head = add(text.charAt(0));
    node curr = head;

    // curr pointer points to the current node
    // where the insertion should take place
    for (int i = 1; i < text.length(); i++)
    {
        curr.next = add(text.charAt(i));
        curr = curr.next;
    }
    return head;
}

// Function to print the data
// present in all the nodes
static void print(node head)
{
    node curr = head;
    while (curr != null)
    {
        System.out.print(curr.data + " -> ");
        curr = curr.next;
    }
}

// Driver code
public static void main(String[] args)
{
    String text = "GEEKS";

    node head = null;
    head = string_to_SLL(text, head);

    print(head);
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to Convert a String
# to a Singly Linked List

# Structure for a Singly Linked List
class node:
    def __init__(self):
        data = None
        next = None

# Function to add a node to the Linked List
def add(data):

    newnode = node()
    newnode.data = data
    newnode.next = None
    return newnode

# Function to convert the string
# to Linked List.
def string_to_SLL(text,head):

    head = add(text[0])
    curr = head

    # curr pointer points to the current node
    # where the insertion should take place
    for i in range(len(text) - 1):

        curr.next = add(text[i + 1])
        curr = curr.next

    return head

# Function to print the data
# present in all the nodes
def print_(head):

    curr = head
    while (curr != None) :

        print ((curr.data), end = " - > " )
        curr = curr.next

# Driver code
text = "GEEKS"
head = None
head = string_to_SLL(text, head)
print_(head)

# This code is contributed by Arnab Kundu
```

## C#

```
// C# program to Convert a String
// to a Singly Linked List
using System;

class GFG
{

// Structure for a Singly Linked List
class node
{
    public char data;
    public node next;
};

// Function to add a new node
// to the Linked List
static node add(char data)
{
    node newnode = new node();
    newnode.data = data;
    newnode.next = null;
    return newnode;
}

// Function to convert the string
// to Linked List.
static node string_to_SLL(String text,
                            node head)
{
    head = add(text[0]);
    node curr = head;

    // curr pointer points to the current node
    // where the insertion should take place
    for (int i = 1; i < text.Length; i++)
    {
        curr.next = add(text[i]);
        curr = curr.next;
    }
    return head;
}

// Function to print the data
// present in all the nodes
static void print(node head)
{
    node curr = head;
    while (curr != null)
    {
        Console.Write(curr.data + " -> ");
        curr = curr.next;
    }
}

// Driver code
public static void Main(String[] args)
{
    String text = "GEEKS";

    node head = null;
    head = string_to_SLL(text, head);

    print(head);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript program to Convert a String
// to a Singly Linked List

class node
{
    constructor()
    {
        this.data='';
        this.next=null;
    }
}

// Function to add a new node to the Linked List   
function add(data)
{
    let newnode = new node();
    newnode.data = data;
    newnode.next = null;
    return newnode;
}

// Function to convert the string
// to Linked List.
function string_to_SLL(text,head)
{
    head = add(text[0]);
    let curr = head;

    // curr pointer points to the current node
    // where the insertion should take place
    for (let i = 1; i < text.length; i++)
    {
        curr.next = add(text[i]);
        curr = curr.next;
    }
    return head;
}

// Function to print the data
// present in all the nodes
function print(head)
{
    let curr = head;
    while (curr != null)
    {
        document.write(curr.data + " -> ");
        curr = curr.next;
    }
}

// Driver code
let text = "GEEKS";

let head = null;
head = string_to_SLL(text, head);

print(head);

// This code is contributed by avanitrachhadiya2155
</script>
```

**Output:** 

```
G -> E -> E -> K -> S ->
```