# 以相反的顺序打印链接列表的最后 k 个节点| 递归方法

给定一个包含 **N 个**节点和正整数 **k** 的链表应小于或等于 N。任务是打印该节点的最后 **k** 个节点。 以相反的顺序列出。

**示例：**

```
Input: list: 1->2->3->4->5, k = 2                       
Output: 5 4

Input: list: 3->10->6->9->12->2->8, k = 4 
Output: 8 2 12 9

```

**来源：** [校园外 Amazon Interview Experience SDE](https://www.geeksforgeeks.org/amazon-interview-experience-sde-off-campus/) 。

**递归方法：**递归遍历链表。 从每个递归调用返回时，请跟踪节点编号，将最后一个节点视为编号 1，将倒数第二个节点视为编号 2，依此类推。 可以借助全局变量或指针变量来跟踪此计数。 借助此 count 变量，打印节点号小于或等于 **k** 的节点。

下面是上述方法的实现：

## C++

```cpp

// C++ implementation to print the last k nodes 
// of linked list in reverse order 
#include <bits/stdc++.h> 
using namespace std; 

// Structure of a node 
struct Node { 
    int data; 
    Node* next; 
}; 

// Function to get a new node 
Node* getNode(int data) 
{ 
    // allocate space 
    Node* newNode = new Node; 

    // put in data 
    newNode->data = data; 
    newNode->next = NULL; 
    return newNode; 
} 

// Function to print the last k nodes 
// of linked list in reverse order 
void printLastKRev(Node* head, 
                     int& count, int k) 
{ 
    // if list is empty 
    if (!head) 
        return; 

    // Recursive call with the next node 
    // of the list 
    printLastKRev(head->next, count, k); 

    // Count variable to keep track of 
    // the last k nodes 
    count++; 

    // Print data 
    if (count <= k) 
        cout << head->data << " "; 
} 

// Driver code 
int main() 
{ 
    // Create list: 1->2->3->4->5 
    Node* head = getNode(1); 
    head->next = getNode(2); 
    head->next->next = getNode(3); 
    head->next->next->next = getNode(4); 
    head->next->next->next->next = getNode(5); 

    int k = 4, count = 0; 

    // print the last k nodes 
    printLastKRev(head, count, k); 

    return 0; 
} 

```

## Java

```java

// Java implementation to print the last k nodes  
// of linked list in reverse order  
class GfG  
{ 

// Structure of a node  
static class Node  
{  
    int data;  
    Node next;  
} 

// Function to get a new node  
static Node getNode(int data)  
{  
    // allocate space  
    Node newNode = new Node();  

    // put in data  
    newNode.data = data;  
    newNode.next = null;  
    return newNode;  
}  

static class C 
{ 
    int count = 0; 
} 

// Function to print the last k nodes  
// of linked list in reverse order  
static void printLastKRev(Node head, C c, int k)  
{  
    // if list is empty  
    if (head == null)  
        return;  

    // Recursive call with the next node  
    // of the list  
    printLastKRev(head.next, c, k);  

    // Count variable to keep track of  
    // the last k nodes  
    c.count++;  

    // Print data  
    if (c.count <= k)  
        System.out.print(head.data + " ");  
}  

// Driver code  
public static void main(String[] args)  
{  
    // Create list: 1->2->3->4->5  
    Node head = getNode(1);  
    head.next = getNode(2);  
    head.next.next = getNode(3);  
    head.next.next.next = getNode(4);  
    head.next.next.next.next = getNode(5);  

    int k = 4; 
    C c = new C(); 

    // print the last k nodes  
    printLastKRev(head, c, k);  
} 
}  

// This code is contributed by prerna saini 

```

## 蟒蛇

```

# Python implementation to print the last k nodes  
# of linked list in reverse order  

# Node class  
class Node:  

    # Function to initialise the node object  
    def __init__(self, data):  
        self.data = data # Assign data  
        self.next =None

# Function to get a new node  
def getNode(data):  

    # allocate space  
    newNode = Node(0)  

    # put in data  
    newNode.data = data  
    newNode.next = None
    return newNode  

class C:  
    def __init__(self, data):  
        self.count = data  

# Function to print the last k nodes  
# of linked list in reverse order  
def printLastKRev(head, c, k):  

    # if list is empty  
    if (head == None):  
        return

    # Recursive call with the next node  
    # of the list  
    printLastKRev(head.next, c, k)  

    # Count variable to keep track of  
    # the last k nodes  
    c.count = c.count + 1

    # Print data  
    if (c.count <= k) : 
        print(head.data, end = " ")  

# Driver code  

# Create list: 1->2->3->4->5  
head = getNode(1)  
head.next = getNode(2)  
head.next.next = getNode(3)  
head.next.next.next = getNode(4)  
head.next.next.next.next = getNode(5)  

k = 4
c = C(0) 

# print the last k nodes  
printLastKRev(head, c, k)  

# This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# implementation to print the last k   
// nodes of linked list in reverse order 
using System; 

class GFG  
{ 

// Structure of a node  
public class Node  
{  
    public int data;  
    public Node next;  
} 

// Function to get a new node  
static Node getNode(int data)  
{  
    // allocate space  
    Node newNode = new Node();  

    // put in data  
    newNode.data = data;  
    newNode.next = null;  
    return newNode;  
}  

public class C 
{ 
    public int count = 0; 
} 

// Function to print the last k nodes  
// of linked list in reverse order  
static void printLastKRev(Node head, C c, int k)  
{  
    // if list is empty  
    if (head == null)  
        return;  

    // Recursive call with the next  
    // node of the list  
    printLastKRev(head.next, c, k);  

    // Count variable to keep track   
    // of the last k nodes  
    c.count++;  

    // Print data  
    if (c.count <= k)  
        Console.Write(head.data + " ");  
}  

// Driver code  
public static void Main(String []args)  
{  

    // Create list: 1->2->3->4->5  
    Node head = getNode(1);  
    head.next = getNode(2);  
    head.next.next = getNode(3);  
    head.next.next.next = getNode(4);  
    head.next.next.next.next = getNode(5);  

    int k = 4; 
    C c = new C(); 

    // print the last k nodes  
    printLastKRev(head, c, k);  
} 
}  

// This code is contributed by Arnab Kundu 

```

**Output:**

```
5 4 3 2

```

**时间复杂度：**`O(n)`。

**迭代方法：**的想法是使用[堆栈数据结构](http://www.geeksforgeeks.org/stack-data-structure/)。

1.  将所有链接列表节点推入堆栈。

2.  从堆栈中弹出 k 个节点并进行打印。

**时间复杂度：**`O(n)`。

**两指针方法**的想法类似于[从链接列表](https://www.geeksforgeeks.org/nth-node-from-the-end-of-a-linked-list/)的末尾找到第 k 个节点。

1.  将第一个指针向前移动 k 个节点。

2.  现在从头开始第二个指针。

3.  当第一个指针到达末尾时，第二个指针指向第 k 个节点。

4.  最后使用第二个指针，打印最后 k 个节点。

**时间复杂度：**`O(n)`。



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。