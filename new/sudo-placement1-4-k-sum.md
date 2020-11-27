# Sudo 放置 1.4 | `K`总和

> 原文：[https://www.geeksforgeeks.org/sudo-placement1-4-k-sum/](https://www.geeksforgeeks.org/sudo-placement1-4-k-sum/)

给定整数和整数`k`的链表的开头，您的任务是按如下方式修改链表：

*   考虑大小为`k`的组中的节点。 在每个组中，将第一个节点的值替换为组和。

*   另外，删除组中除第一个节点以外的元素。

*   在遍历期间，如果链表中的其余节点小于`k`，则也要考虑剩余节点，执行上述操作。

**示例**：

> **输入**：`N = 6, K = 2`
> `1 -> 2 -> 3 -> 4 -> 5 -> 6`
> **输出**：`3 7 11`
> 
> 我们用`()`表示对`k`个元素的分组。 `()`中的元素相加。
>
> ```
> 1 -> 2 -> 3 -> 4 -> 5 -> 6 -> null
> (1 -> 2) -> 3  -> 4 -> 5 -> 6 -> null
> (3) -> 3 -> 4 -> 5 -> 6 -> null
> 3 -> (3 -> 4) -> 5 -> 6 -> null
> 3 -> (7) -> 5 -> 6 -> null
> 3 -> 7 -> (5 -> 6) -> null
> 3 -> 7 -> (11) -> null
> 3 -> 7 -> 11 -> null
> ```

**方法**：将给定的节点插入“链接”列表中。 插入方法[已进行了讨论](https://www.geeksforgeeks.org/linked-list-set-2-inserting-a-node/)。 插入节点后，从列表的开头进行迭代。 将第一个节点标记为`temp`节点。 迭代接下来的`k-1`个节点，并在`sum`变量中求和。 如果节点数少于`K`，则将临时节点的数据替换为`sum`，并将`temp`指向`NULL`。 如果存在一个由`K`个节点组成的组，则用`sum`替换临时数据，并将`temp`移到`K`个节点之后的节点。 继续上述操作，直到`temp`指向`NULL`。 一旦`temp`到达末尾，则意味着遍历了所有大小为`K`的组，并且已用大小为`K`的节点总和替换了该节点。一旦完成了替换操作，就可以打印由此形成的链表。 [在这里已讨论了打印链表的方法](https://www.geeksforgeeks.org/linked-list-set-1-introduction/)。

下面是上述方法的实现：

## C++

```cpp

// C++ program for 
// SP - K Sum 

#include <iostream> 
using namespace std; 

// structure for linked list 
struct Node { 
    long long data; 
    Node* next; 
}; 

// allocated new node 
Node* newNode(int key) 
{ 
    Node* temp = new Node; 
    temp->data = key; 
    temp->next = NULL; 
    return temp; 
} 

// function to insert node in a Linked List 
Node* insertNode(Node* head, int key) 
{ 
    if (head == NULL) 
        head = newNode(key); 
    else
        head->next = insertNode(head->next, key); 

    return head; 
} 

// traverse the node 
// to print it 
void print(Node* head) 
{ 
    // travere the linked list 
    while (head) { 
        cout << head->data << " "; 
        head = head->next; 
    } 
    cout << endl; 
} 

// function to perform the following operation 
void KSum(Node* head, int k) 
{ 
    // initially pointing to start 
    Node* temp = head; 

    // iterate till end 
    while (temp) { 

        // dummy variable to store k 
        long long count = k; 

        // summation of nodes 
        long long sum = 0; 

        // currently at node from 
        // which itearation is done 
        Node* curr = temp; 

        // till k nodes are visited and 
        // last node is not visited 
        while (count-- && curr) { 
            // add to sum the node data 
            sum = sum + curr->data; 

            // move to the next node 
            curr = curr->next; 
        } 

        // change pointer's data of temp to sum 
        temp->data = sum; 

        // move temp to next pointer 
        temp->next = curr; 

        // move temp to the next pointer 
        temp = temp->next; 
    } 
} 

// Driver Code 
int main() 
{ 

    Node* head = NULL; 

    // inserts nodes in the linked list 
    head = insertNode(head, 1); 
    head = insertNode(head, 2); 
    head = insertNode(head, 3); 
    head = insertNode(head, 4); 
    head = insertNode(head, 5); 
    head = insertNode(head, 6); 

    int k = 2; 
    // Function call to perform the 
    // given operations 
    KSum(head, k); 

    // print the linked list 
    print(head); 

    return 0; 
} 

```

## Java

```java

// Java program for 
// SP - K Sum 

import java.io.*; 
import java.util.*; 

// structure for linked list 
class Node  
{ 
    int data; 
    Node next; 
    Node(int key) 
    { 
        data = key; 
        next = null; 
    } 
} 

class GFG 
{ 

// allocated new node 
static Node head; 

// function to insert node 
// in a Linked List 
public static Node insertNode(Node head, int key) 
{ 
    if (head == null) 
        head = new Node(key); 
    else
        head.next = insertNode(head.next, key); 

    return head; 
} 

// traverse the node 
// to print it 
public static void print(Node head) 
{ 
    // travere the linked list 
    while (head != null)  
    { 
        System.out.print(head.data + " "); 
        head = head.next; 
    } 
    System.out.println(); 
} 

// function to perform  
// the following operation 
public static void KSum(Node head, int k) 
{ 
    // initially pointing 
    // to start 
    Node temp = head; 

    // iterate till end 
    while (temp != null)  
    { 

        // dummy variable 
        // to store k 
        int count = k; 

        // summation of nodes 
        int sum = 0; 

        // currently at node from 
        // which itearation is done 
        Node curr = temp; 

        // till k nodes are visited and 
        // last node is not visited 
        while (count > 0 && curr != null)  
        { 
            // add to sum the node data 
            sum = sum + curr.data; 

            // move to the next node 
            curr = curr.next; 
            count--; 
        } 

        // change pointer's data 
        // of temp to sum 
        temp.data = sum; 

        // move temp to 
        // next pointer 
        temp.next = curr; 

        // move temp to  
        // the next pointer 
        temp = temp.next; 
    } 

    //return temp; 
} 

// Driver Code 
public static void main(String args[]) 
{ 
     head = null; 

    // inserts nodes in 
    // the linked list 
    head = insertNode(head, 1); 
    head = insertNode(head, 2); 
    head = insertNode(head, 3); 
    head = insertNode(head, 4); 
    head = insertNode(head, 5); 
    head = insertNode(head, 6); 

    int k = 2; 

    // Function call to perform  
    // the given operations 
     KSum(head, k); 

    // print the linked list 
    print(head); 
} 
} 

```

## Python3

```py

# Python program for 
# SP - K Sum 

# structure for linked list 
class Node: 
    def __init__(self, key): 
        self.data = key 
        self.next = None

# function to insert node in a Linked List 
def insertNode(head: Node, key: int) -> Node: 
    if head is None: 
        head = Node(key) 
    else: 
        head.next = insertNode(head.next, key) 

    return head 

# traverse the node 
# to print it 
def Print(head: Node): 

    # travere the linked list 
    while head: 
        print(head.data, end = " ") 
        head = head.next
    print() 

# function to perform the following operation 
def KSum(head: Node, k: int): 

    # initially pointing to start 
    temp = head 

    # iterate till end 
    while temp: 

        # dummy variable to store k 
        count = k 

        # summation of nodes 
        sum = 0

        # currently at node from 
        # which itearation is done 
        curr = temp 

        # till k nodes are visited and 
        # last node is not visited 
        while count and curr: 

            # add to sum the node data 
            sum = sum + curr.data 

            # move to the next node 
            curr = curr.next
            count -= 1

        # change pointer's data of temp to sum 
        temp.data = sum

        # move temp to next pointer 
        temp.next = curr 

        # move temp to the next pointer 
        temp = temp.next

# Driver Code 
if __name__ == "__main__": 
    head = None

    # inserts nodes in the linked list 
    head = insertNode(head, 1) 
    head = insertNode(head, 2) 
    head = insertNode(head, 3) 
    head = insertNode(head, 4) 
    head = insertNode(head, 5) 
    head = insertNode(head, 6) 

    k = 2

    # Function call to perform the 
    # given operations 
    KSum(head, k) 

    # print the linked list 
    Print(head) 

# This code is contributed by 
# sanjeev2552 

```

## C#

```cs

// C# program for SP - K Sum 
using System; 

// structure for linked list 
public class Node  
{ 
    public int data; 
    public Node next; 
    public Node(int key) 
    { 
        data = key; 
        next = null; 
    } 
} 

public class GFG 
{ 

// allocated new node 
static Node head; 

// function to insert node 
// in a Linked List 
public static Node insertNode(Node head, int key) 
{ 
    if (head == null) 
        head = new Node(key); 
    else
        head.next = insertNode(head.next, key); 

    return head; 
} 

// traverse the node 
// to print it 
public static void print(Node head) 
{ 
    // travere the linked list 
    while (head != null)  
    { 
        Console.Write(head.data + " "); 
        head = head.next; 
    } 
    Console.WriteLine(); 
} 

// function to perform  
// the following operation 
public static void KSum(Node head, int k) 
{ 
    // initially pointing 
    // to start 
    Node temp = head; 

    // iterate till end 
    while (temp != null)  
    { 

        // dummy variable 
        // to store k 
        int count = k; 

        // summation of nodes 
        int sum = 0; 

        // currently at node from 
        // which itearation is done 
        Node curr = temp; 

        // till k nodes are visited and 
        // last node is not visited 
        while (count > 0 && curr != null)  
        { 
            // add to sum the node data 
            sum = sum + curr.data; 

            // move to the next node 
            curr = curr.next; 
            count--; 
        } 

        // change pointer's data 
        // of temp to sum 
        temp.data = sum; 

        // move temp to 
        // next pointer 
        temp.next = curr; 

        // move temp to  
        // the next pointer 
        temp = temp.next; 
    } 
    // return temp; 
} 

// Driver Code 
public static void Main() 
{ 
    head = null; 

    // inserts nodes in 
    // the linked list 
    head = insertNode(head, 1); 
    head = insertNode(head, 2); 
    head = insertNode(head, 3); 
    head = insertNode(head, 4); 
    head = insertNode(head, 5); 
    head = insertNode(head, 6); 

    int k = 2; 

    // Function call to perform  
    // the given operations 
    KSum(head, k); 

    // print the linked list 
    print(head); 
} 
} 

/* This code contributed by PrinciRaj1992 */

```

**输出**：

```
3 7 11
```

被誉为业界最抢手的技能之一，拥有我们的 [**C++ STL**](https://practice.geeksforgeeks.org/courses/cpp-stl?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=GFG_Article_Bottom_CPP_STL) 课程的编码基础，并通过严格的问题解决方法掌握了这些概念。

本文由 **Team Geeksforgeeks** 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。