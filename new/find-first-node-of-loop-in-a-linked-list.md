# 在链表

中查找循环的第一个节点

编写一个函数 *findFirstLoopNode（）*，该函数检查给定的链表是否包含循环。 如果存在循环，则它将点返回到循环的第一个节点。 否则返回 NULL。

**示例：**

```
Input : Head of below linked list

```

![](img/712a32386dfe621abfb081cc905aa457.png)

```
Output : Pointer to node 2

```

我们已经讨论了 [Floyd 的环路检测算法](https://www.geeksforgeeks.org/detect-loop-in-a-linked-list/)。 以下是查找循环的第一个节点的步骤。
1.如果找到循环，则初始化慢速指针以使其开头，让快速指针位于其位置。
2.一次将慢速指针和快速指针移动一个节点。
3.它们相遇的点是循环的起点。

## C++

```cpp

// C++ program to return first node of loop.
#include <bits/stdc++.h>
using namespace std;

struct Node {
    int key;
    struct Node* next;
};

Node* newNode(int key)
{
    Node* temp = new Node;
    temp->key = key;
    temp->next = NULL;
    return temp;
}

// A utility function to print a linked list
void printList(Node* head)
{
    while (head != NULL) {
        cout << head->key << " ";
        head = head->next;
    }
    cout << endl;
}

// Function to detect and remove loop
// in a linked list that may contain loop
Node* detectAndRemoveLoop(Node* head)
{
    // If list is empty or has only one node
    // without loop
    if (head == NULL || head->next == NULL)
        return NULL;

    Node *slow = head, *fast = head;

    // Move slow and fast 1 and 2 steps
    // ahead respectively.
    slow = slow->next;
    fast = fast->next->next;

    // Search for loop using slow and
    // fast pointers
    while (fast && fast->next) {
        if (slow == fast)
            break;
        slow = slow->next;
        fast = fast->next->next;
    }

    // If loop does not exist
    if (slow != fast)
        return NULL;

    // If loop exists. Start slow from
    // head and fast from meeting point.
    slow = head;
    while (slow != fast) {
        slow = slow->next;
        fast = fast->next;
    }

    return slow;
}

/* Driver program to test above function*/
int main()
{
    Node* head = newNode(50);
    head->next = newNode(20);
    head->next->next = newNode(15);
    head->next->next->next = newNode(4);
    head->next->next->next->next = newNode(10);

    /* Create a loop for testing */
    head->next->next->next->next->next = head->next->next;

    Node* res = detectAndRemoveLoop(head);
    if (res == NULL)
        cout << "Loop does not exist";
    else
        cout << "Loop starting node is " << res->key;

    return 0;
}

```

## Java

```java

// Java program to return 
// first node of loop.
import java.util.*;
class GFG{

static class Node 
{
  int key;
  Node next;
};

static Node newNode(int key)
{
  Node temp = new Node();
  temp.key = key;
  temp.next = null;
  return temp;
}

// A utility function to 
// print a linked list
static void printList(Node head)
{
  while (head != null) 
  {
    System.out.print(head.key + " ");
    head = head.next;
  }
  System.out.println();
}

// Function to detect and remove loop
// in a linked list that may contain loop
static Node detectAndRemoveLoop(Node head)
{
  // If list is empty or has 
  // only one node without loop
  if (head == null || head.next == null)
    return null;

  Node slow = head, fast = head;

  // Move slow and fast 1 
  // and 2 steps ahead 
  // respectively.
  slow = slow.next;
  fast = fast.next.next;

  // Search for loop using 
  // slow and fast pointers
  while (fast != null && 
         fast.next != null) 
  {
    if (slow == fast)
      break;
    slow = slow.next;
    fast = fast.next.next;
  }

  // If loop does not exist
  if (slow != fast)
    return null;

  // If loop exists. Start slow from
  // head and fast from meeting point.
  slow = head;
  while (slow != fast) 
  {
    slow = slow.next;
    fast = fast.next;
  }

  return slow;
}

// Driver code
public static void main(String[] args)
{
  Node head = newNode(50);
  head.next = newNode(20);
  head.next.next = newNode(15);
  head.next.next.next = newNode(4);
  head.next.next.next.next = newNode(10);

  // Create a loop for testing
  head.next.next.next.next.next = head.next.next;

  Node res = detectAndRemoveLoop(head);
  if (res == null)
    System.out.print("Loop does not exist");
  else
    System.out.print("Loop starting node is " +  res.key);
}
}

// This code is contributed by shikhasingrajput

```

## C#

```cs

// C# program to return 
// first node of loop.
using System;
class GFG{

class Node 
{
  public int key;
  public Node next;
};

static Node newNode(int key)
{
  Node temp = new Node();
  temp.key = key;
  temp.next = null;
  return temp;
}

// A utility function to 
// print a linked list
static void printList(Node head)
{
  while (head != null) 
  {
    Console.Write(head.key + " ");
    head = head.next;
  }
  Console.WriteLine();
}

// Function to detect and remove loop
// in a linked list that may contain loop
static Node detectAndRemoveLoop(Node head)
{
  // If list is empty or has 
  // only one node without loop
  if (head == null || head.next == null)
    return null;

  Node slow = head, fast = head;

  // Move slow and fast 1 
  // and 2 steps ahead 
  // respectively.
  slow = slow.next;
  fast = fast.next.next;

  // Search for loop using 
  // slow and fast pointers
  while (fast != null && 
         fast.next != null) 
  {
    if (slow == fast)
      break;
    slow = slow.next;
    fast = fast.next.next;
  }

  // If loop does not exist
  if (slow != fast)
    return null;

  // If loop exists. Start slow from
  // head and fast from meeting point.
  slow = head;
  while (slow != fast) 
  {
    slow = slow.next;
    fast = fast.next;
  }

  return slow;
}

// Driver code
public static void Main(String[] args)
{
  Node head = newNode(50);
  head.next = newNode(20);
  head.next.next = newNode(15);
  head.next.next.next = newNode(4);
  head.next.next.next.next = newNode(10);

  // Create a loop for testing
  head.next.next.next.next.next = 
                      head.next.next;

  Node res = detectAndRemoveLoop(head);

  if (res == null)
    Console.Write("Loop does not exist");
  else
    Console.Write("Loop starting node is " +  
                   res.key);
}
}

// This code is contributed by shikhasingrajput

```

**Output:** 

```
Loop starting node is 15

```

**这种方法如何起作用？**
在弗洛伊德（Floyd）的循环发现算法之后的某个时间点让慢速和快速相遇。 下图显示了找到循环时的情况。

![LinkedListCycle](img/b3eac71cdcbdac2e7aabe8f7e7a6a103.png)

我们可以从上图得出以下结论

```
Distance traveled by fast pointer = 2 * (Distance traveled 
                                         by slow pointer)

(m + n*x + k) = 2*(m + n*y + k)

Note that before meeting the point shown above, fast
was moving at twice speed.

x -->  Number of complete cyclic rounds made by 
       fast pointer before they meet first time

y -->  Number of complete cyclic rounds made by 
       slow pointer before they meet first time

```

从上面的等式，我们可以得出以下结论

```
    m + k = (x-2y)*n

Which means m+k is a multiple of n. 

```

因此，如果我们再次以**相同的速度**开始移动两个指针，以使一个指针（例如慢速）从链接列表的头节点开始，而其他指针（例如快速）从会合点开始。 当慢速指针到达循环的起点（已进行 m 步）时，快速指针也将进行 m 步的移动，因为它们现在以相同的速度移动。 因为 m + k 是 n 的倍数，并且从 k 快速开始，所以它们将在开始时相遇。 他们还可以见面吗？ 否，因为慢速指针会在 m 步后第一次进入循环。

**方法 2：**
在此方法中，将创建一个临时节点。 使遍历的每个节点的下一个指针指向该临时节点。 这样，我们将节点的下一个指针用作标志来指示该节点是否已遍历。 检查每个节点以查看下一个节点是否指向临时节点。 在循环的第一个节点的情况下，第二次遍历该条件将为真，因此我们返回该节点。
该代码以 O（n）时间复杂度运行，并使用恒定的存储空间。

下面是上述方法的实现：

## C++

```cpp

// C++ program to return first node of loop
#include <bits/stdc++.h>
using namespace std;

struct Node {
    int key;
    struct Node* next;
};

Node* newNode(int key)
{
    Node* temp = new Node;
    temp->key = key;
    temp->next = NULL;
    return temp;
}

// A utility function to print a linked list
void printList(Node* head)
{
    while (head != NULL) {
        cout << head->key << " ";
        head = head->next;
    }
    cout << endl;
}

// Function to detect first node of loop
// in a linked list that may contain loop
Node* detectLoop(Node* head)
{

    // Create a temporary node
    Node* temp = new Node;
    while (head != NULL) {

        // This condition is for the case
        // when there is no loop
        if (head->next == NULL) {
            return NULL;
        }

        // Check if next is already
        // pointing to temp
        if (head->next == temp) {
            break;
        }

        // Store the pointer to the next node
        // in order to get to it in the next step
        Node* nex = head->next;

        // Make next point to temp
        head->next = temp;

        // Get to the next node in the list
        head = nex;
    }

    return head;
}

/* Driver program to test above function*/
int main()
{
    Node* head = newNode(50);
    head->next = newNode(20);
    head->next->next = newNode(15);
    head->next->next->next = newNode(4);
    head->next->next->next->next = newNode(10);

    /* Create a loop for testing */
    head->next->next->next->next->next = head->next->next;

    Node* res = detectLoop(head);
    if (res == NULL)
        cout << "Loop does not exist";
    else
        cout << "Loop starting node is " << res->key;

    return 0;
}

```

## Java

```java

// Java program to return first node of loop
import java.util.*;
class GFG{

static class Node 
{
    int key;
    Node next;
};

static Node newNode(int key)
{
    Node temp = new Node();
    temp.key = key;
    temp.next = null;
    return temp;
}

// A utility function to print a linked list
static void printList(Node head)
{
    while (head != null) 
    {
        System.out.print(head.key + " ");
        head = head.next;
    }
    System.out.println();
}

// Function to detect first node of loop
// in a linked list that may contain loop
static Node detectLoop(Node head)
{

    // Create a temporary node
    Node temp = new Node();
    while (head != null) 
    {

        // This condition is for the case
        // when there is no loop
        if (head.next == null) 
        {
            return null;
        }

        // Check if next is already
        // pointing to temp
        if (head.next == temp)
        {
            break;
        }

        // Store the pointer to the next node
        // in order to get to it in the next step
        Node nex = head.next;

        // Make next point to temp
        head.next = temp;

        // Get to the next node in the list
        head = nex;
    }

    return head;
}

/* Driver program to test above function*/
public static void main(String[] args)
{
    Node head = newNode(50);
    head.next = newNode(20);
    head.next.next = newNode(15);
    head.next.next.next = newNode(4);
    head.next.next.next.next = newNode(10);

    /* Create a loop for testing */
    head.next.next.next.next.next = head.next.next;

    Node res = detectLoop(head);
    if (res == null)
        System.out.print("Loop does not exist");
    else
        System.out.print("Loop starting node is " + 
                                         res.key);

}
}

// This code is contributed by gauravrajput1

```

## C#

```cs

// C# program to return first node of loop
using System;

class GFG{

class Node 
{
    public int key;
    public Node next;
};

static Node newNode(int key)
{
    Node temp = new Node();
    temp.key = key;
    temp.next = null;
    return temp;
}

// A utility function to print a linked list
static void printList(Node head)
{
    while (head != null) 
    {
        Console.Write(head.key + " ");
        head = head.next;
    }
    Console.WriteLine();
}

// Function to detect first node of loop
// in a linked list that may contain loop
static Node detectLoop(Node head)
{

    // Create a temporary node
    Node temp = new Node();

    while (head != null) 
    {

        // This condition is for the case
        // when there is no loop
        if (head.next == null) 
        {
            return null;
        }

        // Check if next is already
        // pointing to temp
        if (head.next == temp)
        {
            break;
        }

        // Store the pointer to the next node
        // in order to get to it in the next step
        Node nex = head.next;

        // Make next point to temp
        head.next = temp;

        // Get to the next node in the list
        head = nex;
    }
    return head;
}

// Driver code
public static void Main(String[] args)
{
    Node head = newNode(50);
    head.next = newNode(20);
    head.next.next = newNode(15);
    head.next.next.next = newNode(4);
    head.next.next.next.next = newNode(10);

    // Create a loop for testing 
    head.next.next.next.next.next = head.next.next;

    Node res = detectLoop(head);

    if (res == null)
        Console.Write("Loop does not exist");
    else
        Console.Write("Loop starting node is " + 
                       res.key);
}
}

// This code is contributed by Amit Katiyar

```

**Output:** 

```
Loop starting node is 15

```

**方法 3：**
我们也可以使用**哈希**的概念来检测循环的第一个节点。 这个想法很简单，只需遍历整个链表，然后将节点地址一个接一个地存储在集合（ **C++ STL** ）中，同时将节点地址添加到集合中，检查是否已经包含该特定节点地址，如果 如果在集合中已经存在节点地址，则不添加它，则当前节点是循环的第一个节点。

## C++ 14

```

// The below function take head of Linked List as
// input and return Address of first node in
// the loop if present else return NULL.

/* Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };*/
ListNode* detectCycle(ListNode* A)
{

    // declaring map to store node address
    unordered_set<ListNode*> uset;

    ListNode *ptr = A;

    // Default consider that no cycle is present
    while (ptr != NULL) {

        // checking if address is already present in map 
        if (uset.find(ptr) != uset.end()) 
          return ptr;

        // if address not present then insert into the set
        else
            uset.insert(ptr); 

        ptr = ptr->next;
    }
    return NULL;
}
// This code is contributed by Pankaj_Joshi

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。