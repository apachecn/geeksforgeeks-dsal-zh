# 链表

中出现的最大字符

给定一个字符链接列表。 任务是在链表中找到最大出现的字符。 如果有多个答案，则返回出现的第一个最大字符。

**范例**：

```
Input  : g -> e -> e -> k -> s
Output : e

Input  : a -> a -> b -> b -> c -> c -> d -> d
Output : d

```

**方法 1**：

迭代计算字符串中每个字符的频率，并返回出现次数最多的一个字符。

## C++

```cpp

// CPP program to count the maximum
// occurring character in linked list
#include <bits/stdc++.h>
using namespace std;

/* Link list node */
struct Node {
  char data;
  struct Node *next;
};

char maxChar(struct Node *head) {
  struct Node *p = head;

  int max = -1;
  char res;

  while (p != NULL) {

    // counting the frequency of current element
    // p->data
    struct Node *q = p->next;
    int count = 1;
    while (q != NULL) {
      if (p->data == q->data)
        count++;

      q = q->next;
    }

    // if current counting is greater than max
    if (max < count) {
      res = p->data;
      max = count;
    }

    p = p->next;
  }

  return res;
}

/* Push a node to linked list. Note that
   this function changes the head */
void push(struct Node **head_ref, char new_data) {
  struct Node *new_node = new Node;
  new_node->data = new_data;
  new_node->next = (*head_ref);
  (*head_ref) = new_node;
}

/* Driver program to test above function*/
int main() {
  /* Start with the empty list */
  struct Node *head = NULL;
  char str[] = "skeegforskeeg";
  int i;

  // this will create a linked list of
  // character "geeksforgeeks"
  for (i = 0; str[i] != '\0'; i++)
    push(&head, str[i]);

  cout << maxChar(head);

  return 0;
}

```

## Java

```java

// JAVA program to count the
// maximum occurring character 
// in linked list
import java.util.*;
class GFG{

// Link list node 
static class Node 
{
  char data;
  Node next;
};

static Node head_ref;

static char maxChar(Node head) 
{
  Node p = head;
  int max = -1;
  char res = '0';

  while (p != null) 
  {
    // counting the frequency 
    // of current element
    // p.data
    Node q = p.next;
    int count = 1;

    while (q != null) 
    {
      if (p.data == q.data)
        count++;

      q = q.next;
    }

    // if current counting 
    // is greater than max
    if (max < count) 
    {
      res = p.data;
      max = count;
    }

    p = p.next;
  }

  return res;
}

// Push a node to linked list. 
// Note that this function 
// changes the head 
static void push(char new_data) 
{
  Node new_node = new Node();
  new_node.data = new_data;
  new_node.next = head_ref;
  head_ref = new_node;
}

// Driver code
public static void main(String[] args) 
{
  // Start with the empty list
   head_ref = null;
  String str = "skeegforskeeg";
  char st[] = str.toCharArray();
  int i;

  // this will create a linked
  // list of character "geeksforgeeks"
  for (i = 0; i < st.length; i++)
     push(st[i]);

  System.out.print(maxChar(head_ref));
}
}

// This code is contributed by shikhasingrajput

```

**Output:** 

```
e

```

**时间复杂度**：（N * N）

**方法 2 ：（使用计数数组）**

创建一个计数数组，并对每个字符频率进行计数，以返回最大出现的字符。

## C++

```cpp

// CPP program to count the maximum
// occurring character in linked list
#include <bits/stdc++.h>
using namespace std;

/* Link list node */
struct Node {
  char data;
  struct Node *next;
};

char maxChar(struct Node *head) {
  struct Node *p = head;
  int hash[256] = {0};

  // Storing element's frequencies
  // in a hash table.
  while (p != NULL) {
    hash[p->data]++;
    p = p->next;
  }

  p = head;

  int max = -1;
  char res;

  // calculating the first maximum element
  while (p != NULL) {
    if (max < hash[p->data]) {
      res = p->data;
      max = hash[p->data];
    }
    p = p->next;
  }
  return res;
}

/* Push a node to linked list. Note that
   this function changes the head */
void push(struct Node **head_ref, char new_data) {
  struct Node *new_node = new Node;
  new_node->data = new_data;
  new_node->next = (*head_ref);
  (*head_ref) = new_node;
}

/* Driver program to test above function*/
int main() {
  struct Node *head = NULL;
  char str[] = "skeegforskeeg";
  for (int i = 0; str[i] != '\0'; i++)
    push(&head, str[i]);
  cout << maxChar(head);
  return 0;
}

```

## Java

```java

// Java program to count the maximum
// occurring character in linked list
import java.util.*;

class GFG 
{

/* Link list node */
static class Node 
{
    char data;
    Node next;
};

static Node head;
static char maxChar(Node head)
{
    Node p = head;
    int []hash = new int[256];

    // Storing element's frequencies
    // in a hash table.
    while (p != null) 
    {
        hash[p.data]++;
        p = p.next;
    }

    p = head;

    int max = -1;
    char res = 0;

    // calculating the first maximum element
    while (p != null)
    {
        if (max < hash[p.data])
        {
            res = p.data;
            max = hash[p.data];
        }
        p = p.next;
    }
    return res;
}

/* Push a node to linked list. Note that
this function changes the head */
static void push(Node head_ref, char new_data) 
{
    Node new_node = new Node();
    new_node.data = new_data;
    new_node.next = head_ref;
    head_ref = new_node;
    head = head_ref;
}

// Driver Code
public static void main(String[] args)
{
    head = null;
    char str[] = "skeegforskeeg".toCharArray();
    for (int i = 0; i < str.length; i++) 
    {
        push(head, str[i]);
    }
    System.out.println(maxChar(head));
    }
}

// This code is contributed by Rajput-Ji

```

## C#

```cs

// C# program to count the maximum
// occurring character in linked list
using System;

public class GFG 
{

/* Link list node */
class Node 
{
    public char data;
    public Node next;
};

static Node head;
static char maxChar(Node head)
{
    Node p = head;
    int []hash = new int[256];

    // Storing element's frequencies
    // in a hash table.
    while (p != null) 
    {
        hash[p.data]++;
        p = p.next;
    }

    p = head;

    int max = -1;
    char res= '\x0000';

    // calculating the first maximum element
    while (p != null)
    {
        if (max < hash[p.data])
        {
            res = p.data;
            max = hash[p.data];
        }
        p = p.next;
    }
    return res;
}

/* Push a node to linked list. Note that
this function changes the head */
static void push(Node head_ref, char new_data) 
{
    Node new_node = new Node();
    new_node.data = new_data;
    new_node.next = head_ref;
    head_ref = new_node;
    head = head_ref;
}

// Driver Code
public static void Main(String[] args)
{
    head = null;
    char []str = "skeegforskeeg".ToCharArray();
    for (int i = 0; i < str.Length; i++) 
    {
        push(head, str[i]);
    }
    Console.WriteLine(maxChar(head));
    }
}

// This code is contributed by 29AjayKumar

```

**Output:** 

```
e

```

**时间复杂度**：（否）



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。