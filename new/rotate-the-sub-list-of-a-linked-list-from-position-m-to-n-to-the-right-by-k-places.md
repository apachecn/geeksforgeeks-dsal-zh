# 将链接列表的子列表从位置 M 向右旋转 K 个位置

给定一个链表和两个位置“ m”和“ n”。 任务是将子列表从位置 m 旋转到 n，向右旋转 k 个位置。

**示例**：

> **输入**：列表= 1- > 2- > 3- > 4- > 5- > 6，m = 2，n = 5，k = 2
> **输出**：1- > 4- > 5- > 2- > 3- > 6
> 将子列表 2 3 4 5 向右旋转 2 倍
> ，则修改后的列表为：1 4 5 2 3 6
> 
> **输入**：列表= 20- > 45- > 32- > 34- > 22- > 28，m = 3，n = 6，k = 3
> **输出**：20- > 45- > 34- > 22- > 28- > 32
> 将子列表 32 34 22 28 向右旋转 3 倍
> ，则修改后的列表为：20 45 34 22 28 32

**方法**：要旋转从 m 到 n 元素的给定子列表，请将列表从（n-k + 1）<sup>第</sup>移到第<sup>第</sup>节点到 开始子列表以完成轮换。

如果 k 大于子列表的大小，则将其与子列表的大小取模。 因此，使用指针和计数器遍历列表，我们将保存（m-1）个<sup>第</sup>个节点，然后使其指向（n-k + 1）个<sup>第</sup>个节点，因此 将（n-k + 1）个<sup>节点</sup>移到子列表的开头（前面）。

同样，我们将保存第<sup>个</sup>节点，然后使第<sup>个</sup>节点指向该节点。 为了保持列表的其余部分不变，我们将使[n-k]个<sup>节点指向 n 的下一个节点（可能为 NULL）。 最后，我们将获得 k 次正确旋转的子列表。</sup>

下面是上述方法的实现：

## C++

```cpp

// C++ implementation of the above approach 
#include <bits/stdc++.h> 
using namespace std; 

// Definition of node of linkedlist 
struct ListNode { 
    int data; 
    struct ListNode* next; 
}; 

// This function take head pointer of list, start and 
// end points of sublist that is to be rotated and the 
// number k and rotate the sublist to right by k places. 
void rotateSubList(ListNode* A, int m, int n, int k) 
{ 
    int size = n - m + 1; 

    // If k is greater than size of sublist then  
    // we will take its modulo with size of sublist 
    if (k > size) { 
        k = k % size; 
    } 

    // If k is zero or k is equal to size or k is 
    // a multiple of size of sublist then list  
    // remains intact 
    if (k == 0 || k == size) { 
        ListNode* head = A; 
        while (head != NULL) { 
            cout << head->data; 
            head = head->next; 
        } 
        return; 
    } 

    ListNode* link = NULL;  // m-th node 
    if (m == 1) { 
        link = A; 
    } 

    // This loop will traverse all node till 
    // end node of sublist.     
    ListNode* c = A;  // Current traversed node 
    int count = 0;  // Count of traversed nodes 
    ListNode* end = NULL;   
    ListNode* pre = NULL; // Previous of m-th node 
    while (c != NULL) { 
        count++; 

        // We will save (m-1)th node and later 
        // make it point to (n-k+1)th node 
        if (count == m - 1) { 
            pre = c; 
            link = c->next; 
        } 
        if (count == n - k) { 
            if (m == 1) { 
                end = c; 
                A = c->next; 
            } 
            else { 
                end = c; 

                // That is how we bring (n-k+1)th 
                // node to front of sublist. 
                pre->next = c->next; 
            } 
        } 

        // This keeps rest part of list intact. 
        if (count == n) { 
            ListNode* d = c->next; 
            c->next = link; 
            end->next = d; 
            ListNode* head = A; 
            while (head != NULL) { 
                cout << head->data << " "; 
                head = head->next; 
            } 
            return; 
        } 
        c = c->next; 
    } 
} 

// Function for creating and linking new nodes 
void push(struct ListNode** head, int val) 
{ 
    struct ListNode* new_node = new ListNode; 
    new_node->data = val; 
    new_node->next = (*head); 
    (*head) = new_node; 
} 

// Driver code 
int main() 
{ 
    struct ListNode* head = NULL; 
    push(&head, 70); 
    push(&head, 60); 
    push(&head, 50); 
    push(&head, 40); 
    push(&head, 30); 
    push(&head, 20); 
    push(&head, 10); 
    ListNode* tmp = head; 
    cout << "Given List: "; 
    while (tmp != NULL) { 
        cout << tmp->data << " "; 
        tmp = tmp->next; 
    } 
    cout << endl; 

    int m = 3, n = 6, k = 2; 
    cout << "After rotation of sublist: "; 
    rotateSubList(head, m, n, k); 

    return 0; 
} 

```

## Java

```java

// Java implementation of the above approach  
import java.util.*; 

class Solution 
{ 

// Definition of node of linkedlist  
static class ListNode {  
    int data;  
     ListNode next;  
} 

// This function take head pointer of list, start and  
// end points of sublist that is to be rotated and the  
// number k and rotate the sublist to right by k places.  
static void rotateSubList(ListNode A, int m, int n, int k)  
{  
    int size = n - m + 1;  

    // If k is greater than size of sublist then   
    // we will take its modulo with size of sublist  
    if (k > size) {  
        k = k % size;  
    }  

    // If k is zero or k is equal to size or k is  
    // a multiple of size of sublist then list   
    // remains intact  
    if (k == 0 || k == size) {  
        ListNode head = A;  
        while (head != null) {  
            System.out.print( head.data);  
            head = head.next;  
        }  
        return;  
    }  

    ListNode link = null;  // m-th node  
    if (m == 1) {  
        link = A;  
    }  

    // This loop will traverse all node till  
    // end node of sublist.      
    ListNode c = A;  // Current traversed node  
    int count = 0;  // Count of traversed nodes  
    ListNode end = null;    
    ListNode pre = null; // Previous of m-th node  
    while (c != null) {  
        count++;  

        // We will save (m-1)th node and later  
        // make it point to (n-k+1)th node  
        if (count == m - 1) {  
            pre = c;  
            link = c.next;  
        }  
        if (count == n - k) {  
            if (m == 1) {  
                end = c;  
                A = c.next;  
            }  
            else {  
                end = c;  

                // That is how we bring (n-k+1)th  
                // node to front of sublist.  
                pre.next = c.next;  
            }  
        }  

        // This keeps rest part of list intact.  
        if (count == n) {  
            ListNode d = c.next;  
            c.next = link;  
            end.next = d;  
            ListNode head = A;  
            while (head != null) {  
                System.out.print( head.data+" ");  
                head = head.next;  
            }  
            return;  
        }  
        c = c.next;  
    }  
}  

// Function for creating and linking new nodes  
static ListNode push( ListNode head, int val)  
{  
     ListNode new_node = new ListNode();  
    new_node.data = val;  
    new_node.next = (head);  
    (head) = new_node;  
    return head; 
}  

// Driver code  
public static void main(String args[]) 
{  
     ListNode head = null;  
    head =push(head, 70);  
    head =push(head, 60);  
    head =push(head, 50);  
    head =push(head, 40);  
    head =push(head, 30);  
    head =push(head, 20);  
    head =push(head, 10);  
    ListNode tmp = head;  
    System.out.print("Given List: ");  
    while (tmp != null) {  
        System.out.print( tmp.data + " ");  
        tmp = tmp.next;  
    }  
    System.out.println(); 

    int m = 3, n = 6, k = 2;  
    System.out.print( "After rotation of sublist: ");  
    rotateSubList(head, m, n, k);  

}  
} 

// This code is contributed 
// by Arnab Kundu 

```

## Python3

```py

# Python3 implementation of the above approach 
import math 

# Definition of node of linkedlist 
class Node:  
    def __init__(self, data):  
        self.data = data  
        self.next = None

# This function take head pointer of list,  
# start and end points of sublist that is  
# to be rotated and the number k and 
# rotate the sublist to right by k places. 
def rotateSubList(A, m, n, k): 
    size = n - m + 1

    # If k is greater than size of sublist then  
    # we will take its modulo with size of sublist 
    if (k > size): 
        k = k % size 

    # If k is zero or k is equal to size or k is 
    # a multiple of size of sublist then list  
    # remains intact 
    if (k == 0 or k == size): 
        head = A 
        while (head != None): 
            print(head.data) 
            head = head.next

        return

    link = None # m-th node 
    if (m == 1) : 
        link = A 

    # This loop will traverse all node till 
    # end node of sublist.  
    c = A # Current traversed node 
    count = 0 # Count of traversed nodes 
    end = None
    pre = None # Previous of m-th node 
    while (c != None) : 
        count = count + 1

        # We will save (m-1)th node and later 
        # make it point to (n-k+1)th node 
        if (count == m - 1) : 
            pre = c 
            link = c.next

        if (count == n - k) : 
            if (m == 1) : 
                end = c 
                A = c.next

            else : 
                end = c 

                # That is how we bring (n-k+1)th 
                # node to front of sublist. 
                pre.next = c.next

        # This keeps rest part of list intact. 
        if (count == n) : 
            d = c.next
            c.next = link 
            end.next = d 
            head = A 
            while (head != None) : 
                print(head.data, end = " ") 
                head = head.next

            return

        c = c.next

# Function for creating and linking new nodes 
def push(head, val): 
    new_node = Node(val) 
    new_node.data = val 
    new_node.next = head 
    head = new_node 
    return head 

# Driver code 
if __name__=='__main__':  
    head = None
    head = push(head, 70) 
    head = push(head, 60) 
    head = push(head, 50) 
    head = push(head, 40) 
    head = push(head, 30) 
    head = push(head, 20) 
    head = push(head, 10) 
    tmp = head 
    print("Given List: ", end = "") 
    while (tmp != None) : 
        print(tmp.data, end = " ") 
        tmp = tmp.next

    print() 

    m = 3
    n = 6
    k = 2 
    print("After rotation of sublist: ", end = "") 
    rotateSubList(head, m, n, k) 

# This code is contributed by Srathore 

```

## C#

```cs

// C# implementation of the above approach  
using System; 

class GFG 
{ 

// Definition of node of linkedlist  
public class ListNode 
{ 
    public int data; 
    public ListNode next; 
} 

// This function take head pointer of list,  
// start and end points of sublist that is  
// to be rotated and the number k and rotate  
// the sublist to right by k places.  
public static void rotateSubList(ListNode A, int m,  
                                      int n, int k) 
{ 
    int size = n - m + 1; 

    // If k is greater than size of sublist  
    // then we will take its modulo with  
    // size of sublist  
    if (k > size) 
    { 
        k = k % size; 
    } 

    // If k is zero or k is equal to size  
    // or k is a multiple of size of sublist  
    // then list remains intact  
    if (k == 0 || k == size) 
    { 
        ListNode head = A; 
        while (head != null) 
        { 
            Console.Write(head.data); 
            head = head.next; 
        } 
        return; 
    } 

    ListNode link = null; // m-th node 
    if (m == 1) 
    { 
        link = A; 
    } 

    // This loop will traverse all node till  
    // end node of sublist.      
    ListNode c = A; // Current traversed node 
    int count = 0;  // Count of traversed nodes 
    ListNode end = null; 
    ListNode pre = null; // Previous of m-th node 
    while (c != null) 
    { 
        count++; 

        // We will save (m-1)th node and later  
        // make it point to (n-k+1)th node  
        if (count == m - 1) 
        { 
            pre = c; 
            link = c.next; 
        } 
        if (count == n - k) 
        { 
            if (m == 1) 
            { 
                end = c; 
                A = c.next; 
            } 
            else
            { 
                end = c; 

                // That is how we bring (n-k+1)th  
                // node to front of sublist.  
                pre.next = c.next; 
            } 
        } 

        // This keeps rest part of list intact.  
        if (count == n) 
        { 
            ListNode d = c.next; 
            c.next = link; 
            end.next = d; 
            ListNode head = A; 
            while (head != null) 
            { 
                Console.Write(head.data + " "); 
                head = head.next; 
            } 
            return; 
        } 
        c = c.next; 
    } 
} 

// Function for creating and linking new nodes  
public static ListNode push(ListNode head, int val) 
{ 
    ListNode new_node = new ListNode(); 
    new_node.data = val; 
    new_node.next = (head); 
    (head) = new_node; 
    return head; 
} 

// Driver code  
public static void Main(string[] args) 
{ 
    ListNode head = null; 
    head = push(head, 70); 
    head = push(head, 60); 
    head = push(head, 50); 
    head = push(head, 40); 
    head = push(head, 30); 
    head = push(head, 20); 
    head = push(head, 10); 
    ListNode tmp = head; 
    Console.Write("Given List: "); 
    while (tmp != null) 
    { 
        Console.Write(tmp.data + " "); 
        tmp = tmp.next; 
    } 
    Console.WriteLine(); 

    int m = 3, n = 6, k = 2; 
    Console.Write("After rotation of sublist: "); 
    rotateSubList(head, m, n, k); 
} 
} 

// This code is contributed by Shrikant13 

```

**Output:**

```
Given List: 10 20 30 40 50 60 70 
After rotation of sublist: 10 20 50 60 30 40 70

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。