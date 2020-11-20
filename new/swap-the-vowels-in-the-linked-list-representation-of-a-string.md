# 交换字符串的链表表示中的元音

> 原文：[https://www.geeksforgeeks.org/swap-the-vowels-in-the-linked-list-representation-of-a-string/](https://www.geeksforgeeks.org/swap-the-vowels-in-the-linked-list-representation-of-a-string/)

给定字符串的链表表示形式，任务是交换字符串中的每个后续元音对，以生成结果链表。

**示例**：

> **输入**：列表= g-> e-> e-> k-> s->空
> **输出**：g-[ > e-> e-> k-> s-> NULL
> 仅有的元音是'e'和'e'，它们将相互交换
> 。
> **输入**：列表= a-> b-> c-> d-> e->空
> **输出**：e-> b-> c-> d-> a-> NULL
> swap（a，e）

**方法**：

*   使用链表节点类型的两个指针来分别存储带有第一个元音的节点和遍历链表。

*   开始遍历链表，直到最后。

*   如果遇到元音，并且第一个指针的数据部分已经包含一个带有元音的节点，则交换当前节点和第一个节点的内容，并将第一个指针设置为 NULL。

*   如果遇到元音并且第一个指针不包含任何内容，请将第一个指针设置为指向此节点。

*   如果未遇到元音，请继续遍历。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation of the approach
#include <iostream>
using namespace std;

// Structure to hold the data and
// the address of next element
struct node {
    char data;
    node* next;
};

// Utility function to add a new
// node to the linked list
node* add(char data)
{
    node* newnode = new node;
    newnode->data = data;
    newnode->next = NULL;
    return newnode;
}

// Function to add the given character
// in the string to the linked list
node* addinll(node* head, char data)
{

    // If the linked list is empty then add
    // it to the head otherwise add
    // the character to the end
    if (head == NULL)
        head = add(data);
    else {
        node* curr = head;
        while (curr->next != NULL)
            curr = curr->next;
        curr->next = add(data);
    }
    return head;
}

// Function to print the linked list
void print(node* head)
{
    node* curr = head;
    while (curr != NULL) {
        cout << curr->data << " -> ";
        curr = curr->next;
    }
    cout << "NULL";
}

// Function that returns true if
// the character is vowel
bool isvowel(char data)
{
    if (data == 'a' || data == 'e'
        || data == 'i' || data == 'o'
        || data == 'u')
        return true;
    if (data == 'A' || data == 'E'
        || data == 'I' || data == 'O'
        || data == 'U')
        return true;
    return false;
}

// Function to reverse the vowels in the linked list
void reversevowels(node* head)
{

    // The pointer named first holds the
    // address of the node containing
    // the first vowel
    node* first = NULL;

    // The pointer curr is used
    // to point to head
    node* curr = head;

    // Traverse the linked list
    while (curr != NULL) {

        // If a vowel is encountered and first is
        // set to NULL then update the first
        // with the address of this node
        if (isvowel(curr->data) and first == NULL)
            first = curr;

        // If a vowel is encountered and the first
        // already contains the address of a vowel
        // then swap the current and the first's data
        else if (isvowel(curr->data) and first != NULL) {
            swap(first->data, curr->data);

            // Set the first pointer to NULL
            first = NULL;
        }
        curr = curr->next;
    }
}

// Driver code
int main()
{
    string s = "geeks";

    // Start with an empty linked list
    node* head = NULL;

    // Add the characters one by
    // one to the linked list
    for (int i = 0; i < s.size(); i++)
        head = addinll(head, s[i]);

    // Reverse the vowels
    // in the linked list
    reversevowels(head);

    // Print the linked list
    // with reversed vowels
    print(head);

    return 0;
}

```

## Java

```java

// Java implementation of the approach
class GFG{

// Structure to hold the data and
// the address of next element
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
    newnode.data = data;
    newnode.next = null;
    return newnode;
}

// Function to add the given character
// in the String to the linked list
static node addinll(node head, char data)
{

    // If the linked list is empty then add
    // it to the head otherwise add
    // the character to the end
    if (head == null)
        head = add(data);
    else
    {
        node curr = head;
        while (curr.next != null)
            curr = curr.next;
        curr.next = add(data);
    }
    return head;
}

// Function to print the linked list
static void print(node head)
{
    node curr = head;
    while (curr != null)
    {
        System.out.print(curr.data + " -> ");
        curr = curr.next;
    }
    System.out.print("NULL");
}

// Function that returns true if
// the character is vowel
static boolean isvowel(char data)
{
    if (data == 'a' || data == 'e' ||
        data == 'i' || data == 'o' || 
        data == 'u')
        return true;
    if (data == 'A' || data == 'E' || 
        data == 'I' || data == 'O' || 
        data == 'U')
        return true;
    return false;
}

// Function to reverse the vowels in the linked list
static void reversevowels(node head)
{

    // The pointer named first holds the
    // address of the node containing
    // the first vowel
    node first = null;

    // The pointer curr is used
    // to point to head
    node curr = head;

    // Traverse the linked list
    while (curr != null) 
    {

        // If a vowel is encountered and first is
        // set to null then update the first
        // with the address of this node
        if (isvowel(curr.data) && first == null)
            first = curr;

        // If a vowel is encountered and the first
        // already contains the address of a vowel
        // then swap the current and the first's data
        else if (isvowel(curr.data) && first != null)
        {
            swap(first.data, curr.data);

            // Set the first pointer to null
            first = null;
        }
        curr = curr.next;
    }
}

private static void swap(char data, char data2)
{
    // Auto-generated method stub
    char newdata = data;
    data = data2;
    data2 = newdata;

}

// Driver code
public static void main(String[] args)
{
    String s = "geeks";

    // Start with an empty linked list
    node head = null;

    // Add the characters one by
    // one to the linked list
    for(int i = 0; i < s.length(); i++)
       head = addinll(head, s.charAt(i));

    // Reverse the vowels
    // in the linked list
    reversevowels(head);

    // Print the linked list
    // with reversed vowels
    print(head);
}
}

// This code is contributed by gauravrajput1

```

## C#

```cs

// C# implementation of the approach
using System;
class GFG{

// Structure to hold the data and
// the address of next element
public class node
{
  public char data;
  public node next;
};

// Utility function to add a new
// node to the linked list
static node add(char data)
{
  node newnode = new node();
  newnode.data = data;
  newnode.next = null;
  return newnode;
}

// Function to add the given 
// character in the String to 
// the linked list
static node addinll(node head, 
                    char data)
{
  // If the linked list is 
  // empty then add it to the 
  // head otherwise add the 
  // character to the end
  if (head == null)
    head = add(data);
  else
  {
    node curr = head;
    while (curr.next != null)
      curr = curr.next;
    curr.next = add(data);
  }
  return head;
}

// Function to print the linked list
static void print(node head)
{
  node curr = head;
  while (curr != null)
  {
    Console.Write(curr.data + " -> ");
    curr = curr.next;
  }
  Console.Write("NULL");
}

// Function that returns true if
// the character is vowel
static bool isvowel(char data)
{
  if (data == 'a' || data == 'e' ||
      data == 'i' || data == 'o' || 
      data == 'u')
    return true;
  if (data == 'A' || data == 'E' || 
      data == 'I' || data == 'O' || 
      data == 'U')
    return true;
  return false;
}

// Function to reverse the vowels 
// in the linked list
static void reversevowels(node head)
{
  // The pointer named first 
  // holds the address of the 
  // node containing the first vowel
  node first = null;

  // The pointer curr is used
  // to point to head
  node curr = head;

  // Traverse the linked list
  while (curr != null) 
  {
    // If a vowel is encountered and first is
    // set to null then update the first
    // with the address of this node
    if (isvowel(curr.data) && 
        first == null)
      first = curr;

    // If a vowel is encountered and 
    // the first already contains the 
    // address of a vowel then swap the 
    // current and the first's data
    else if (isvowel(curr.data) && 
             first != null)
    {
      swap(first.data, curr.data);

      // Set the first pointer to null
      first = null;
    }
    curr = curr.next;
  }
}

private static void swap(char data, 
                         char data2)
{
  // Auto-generated method stub
  char newdata = data;
  data = data2;
  data2 = newdata;

}

// Driver code
public static void Main(String[] args)
{
    String s = "geeks";

    // Start with an empty linked list
    node head = null;

    // Add the characters one by
    // one to the linked list
    for(int i = 0; i < s.Length; i++)
       head = addinll(head, s[i]);

    // Reverse the vowels
    // in the linked list
    reversevowels(head);

    // Print the linked list
    // with reversed vowels
    print(head);
}
}

// This code contributed by gauravrajput1

```

**Output:** 

```
g -> e -> e -> k -> s -> NULL

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。