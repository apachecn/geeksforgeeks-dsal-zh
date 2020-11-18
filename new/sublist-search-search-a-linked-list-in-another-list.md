# 子列表搜索（在另一个列表中搜索链接列表）

> 原文：[https://www.geeksforgeeks.org/sublist-search-search-a-linked-list-in-another-list/](https://www.geeksforgeeks.org/sublist-search-search-a-linked-list-in-another-list/)

给定两个链接列表，任务是检查第一个列表是否存在于第二个列表中。

**范例**：

```
Input  : list1 =  10->20
         list2  = 5->10->20
Output : LIST FOUND

Input  : list1 =  1->2->3->4
         list2  = 1->2->1->2->3->4
Output : LIST FOUND

Input  : list1 =  1->2->3->4
         list2  = 1->2->2->1->2->3
Output : LIST NOT FOUND

```

算法：

1-获取第二个列表的第一个节点。

2-从第一个节点开始匹配第一个列表。

3-如果整个列表匹配，则返回 true。

4-否则，再次将第一个列表带到第一个节点。

5-将第二个列表带到第二个节点。

6-重复这些步骤，直到任何链接列表变为空。

7-如果第一个列表为空，则找到列表，否则为否。

下面是实现。

## C++

```cpp

// C++ program to find a list in second list 
#include <bits/stdc++.h> 
using namespace std; 

// A Linked List node 
struct Node 
{ 
    int data; 
    Node* next; 
}; 

// Returns true if first list is present in second 
// list 
bool findList(Node* first, Node* second) 
{ 
    Node* ptr1 = first, *ptr2 = second; 

    // If both linked lists are empty, return true 
    if (first == NULL && second == NULL) 
        return true; 

    // Else If one is empty and other is not return 
    // false 
    if ( first == NULL || 
        (first != NULL && second == NULL)) 
        return false; 

    // Traverse the second list by picking nodes 
    // one by one 
    while (second != NULL) 
    { 
        // Initialize ptr2 with current node of second 
        ptr2 = second; 

        // Start matching first list with second list 
        while (ptr1 != NULL) 
        { 
            // If second list becomes empty and first 
            // not then return false 
            if (ptr2 == NULL) 
                return false; 

            // If data part is same, go to next 
            // of both lists 
            else if (ptr1->data == ptr2->data) 
            { 
                ptr1 = ptr1->next; 
                ptr2 = ptr2->next; 
            } 

            // If not equal then  break the loop 
            else break; 
        } 

        // Return true if first list gets traversed 
        // completely that means it is matched. 
        if (ptr1 == NULL) 
            return true; 

        // Initialize ptr1 with first again 
        ptr1 = first; 

        // And go to next node of second list 
        second = second->next; 
    } 

    return false; 
} 

/* Function to print nodes in a given linked list */
void printList(Node* node) 
{ 
    while (node != NULL) 
    { 
        printf("%d ", node->data); 
        node = node->next; 
    } 
} 

// Function to add new node to linked lists 
Node *newNode(int key) 
{ 
    Node *temp = new Node; 
    temp-> data= key; 
    temp->next = NULL; 
    return temp; 
} 

/* Driver program to test above functions*/
int main() 
{ 
    /* Let us create two linked lists to test 
    the above functions. Created lists shall be 
        a: 1->2->3->4 
        b: 1->2->1->2->3->4*/
    Node *a = newNode(1); 
    a->next = newNode(2); 
    a->next->next = newNode(3); 
    a->next->next->next = newNode(4); 

    Node *b = newNode(1); 
    b->next = newNode(2); 
    b->next->next = newNode(1); 
    b->next->next->next = newNode(2); 
    b->next->next->next->next = newNode(3); 
    b->next->next->next->next->next = newNode(4); 

    findList(a,b) ? cout << "LIST FOUND" : 
                    cout << "LIST NOT FOUND"; 

    return 0; 
} 

```

## Java

```java

// Java program to find a list in second list 
import java.util.*; 
class GFG  
{  

// A Linked List node 
static class Node  
{ 
    int data; 
    Node next; 
}; 

// Returns true if first list is  
// present in second list 
static boolean findList(Node first, 
                        Node second) 
{ 
    Node ptr1 = first, ptr2 = second; 

    // If both linked lists are empty, 
    // return true 
    if (first == null && second == null) 
        return true; 

    // Else If one is empty and  
    // other is not, return false 
    if (first == null || 
       (first != null && second == null)) 
        return false; 

    // Traverse the second list by  
    // picking nodes one by one 
    while (second != null) 
    { 
        // Initialize ptr2 with  
        // current node of second 
        ptr2 = second; 

        // Start matching first list  
        // with second list 
        while (ptr1 != null) 
        { 
            // If second list becomes empty and  
            // first not then return false 
            if (ptr2 == null) 
                return false; 

            // If data part is same, go to next 
            // of both lists 
            else if (ptr1.data == ptr2.data) 
            { 
                ptr1 = ptr1.next; 
                ptr2 = ptr2.next; 
            } 

            // If not equal then break the loop 
            else break; 
        } 

        // Return true if first list gets traversed 
        // completely that means it is matched. 
        if (ptr1 == null) 
            return true; 

        // Initialize ptr1 with first again 
        ptr1 = first; 

        // And go to next node of second list 
        second = second.next; 
    } 
    return false; 
} 

/* Function to print nodes in a given linked list */
static void printList(Node node) 
{ 
    while (node != null) 
    { 
        System.out.printf("%d ", node.data); 
        node = node.next; 
    } 
} 

// Function to add new node to linked lists 
static Node newNode(int key) 
{ 
    Node temp = new Node(); 
    temp.data= key; 
    temp.next = null; 
    return temp; 
} 

// Driver Code 
public static void main(String[] args)  
{ 
    /* Let us create two linked lists to test 
    the above functions. Created lists shall be 
        a: 1->2->3->4 
        b: 1->2->1->2->3->4*/
    Node a = newNode(1); 
    a.next = newNode(2); 
    a.next.next = newNode(3); 
    a.next.next.next = newNode(4); 

    Node b = newNode(1); 
    b.next = newNode(2); 
    b.next.next = newNode(1); 
    b.next.next.next = newNode(2); 
    b.next.next.next.next = newNode(3); 
    b.next.next.next.next.next = newNode(4); 

    if(findList(a, b) == true)  
        System.out.println("LIST FOUND"); 
    else
        System.out.println("LIST NOT FOUND"); 
} 
} 

// This code is contributed by Princi Singh 

```

## Python3

```py

# Python3 program to find a list in second list  
class Node: 
    def __init__(self, value = 0): 

        self.value = value 
        self.next = None

# Returns true if first list is  
# present in second list  
def findList(first, second): 

    # If both linked lists are empty/None, 
    # return True 
    if not first and not second: 
        return True

    # If ONLY one of them is empty, 
    # return False 
    if not first or not second: 
        return False

    ptr1 = first 
    ptr2 = second 

    # Traverse the second LL by  
    # picking nodes one by one 
    while ptr2: 

        # Initialize 'ptr2' with current 
        # node of 'second' 
        ptr2 = second 

        # Start matching first LL  
        # with second LL 
        while ptr1: 

            # If second LL become empty and  
            # first not, return False, 
            # since first LL has not been  
            # traversed completely 
            if not ptr2: 
                return False

            # If value of both nodes from both 
            # LLs are equal, increment pointers 
            # for both LLs so that next value  
            # can be matched 
            elif ptr1.value == ptr2.value: 
                ptr1 = ptr1.next
                ptr2 = ptr2.next

            # If a single mismatch is found 
            # OR ptr1 is None/empty,break out 
            # of the while loop and do some checks 
            else: 
                break

        # check 1 : 
        # If 'ptr1' is None/empty,that means 
        # the 'first LL' has been completely 
        # traversed and matched so return True 
        if not ptr1: 
            return True

        # If check 1 fails, that means, some  
        # items for 'first' LL are still yet 
        # to be matched, so start again by  
        # bringing back the 'ptr1' to point 
        # to 1st node of 'first' LL 
        ptr1 = first 

        # And increment second node element to next 
        second = second.next

    return False

# Driver Code 

# Let us create two linked lists to 
# test the above functions. 
# Created lists would be be 
# node_a: 1->2->3->4 
# node_b: 1->2->1->2->3->4 
node_a = Node(1) 
node_a.next = Node(2) 
node_a.next.next = Node(3) 
node_a.next.next.next = Node(4) 

node_b = Node(1) 
node_b.next = Node(2) 
node_b.next.next = Node(1) 
node_b.next.next.next = Node(2) 
node_b.next.next.next.next = Node(3) 
node_b.next.next.next.next.next = Node(4) 

if findList(node_a, node_b): 
    print("LIST FOUND") 
else: 
    print("LIST NOT FOUND") 

# This code is contributed by GauriShankarBadola 

```

## C#

```cs

// C# program to find a list in second list 
using System; 

class GFG  
{  

// A Linked List node 
class Node  
{ 
    public int data; 
    public Node next; 
}; 

// Returns true if first list is  
// present in second list 
static Boolean findList(Node first, 
                        Node second) 
{ 
    Node ptr1 = first, ptr2 = second; 

    // If both linked lists are empty, 
    // return true 
    if (first == null && second == null) 
        return true; 

    // Else If one is empty and  
    // other is not, return false 
    if (first == null || 
       (first != null && second == null)) 
        return false; 

    // Traverse the second list by  
    // picking nodes one by one 
    while (second != null) 
    { 
        // Initialize ptr2 with  
        // current node of second 
        ptr2 = second; 

        // Start matching first list  
        // with second list 
        while (ptr1 != null) 
        { 
            // If second list becomes empty and  
            // first not then return false 
            if (ptr2 == null) 
                return false; 

            // If data part is same, go to next 
            // of both lists 
            else if (ptr1.data == ptr2.data) 
            { 
                ptr1 = ptr1.next; 
                ptr2 = ptr2.next; 
            } 

            // If not equal then break the loop 
            else break; 
        } 

        // Return true if first list gets traversed 
        // completely that means it is matched. 
        if (ptr1 == null) 
            return true; 

        // Initialize ptr1 with first again 
        ptr1 = first; 

        // And go to next node of second list 
        second = second.next; 
    } 
    return false; 
} 

/* Function to print nodes 
in a given linked list */
static void printList(Node node) 
{ 
    while (node != null) 
    { 
        Console.Write("{0} ", node.data); 
        node = node.next; 
    } 
} 

// Function to add new node to linked lists 
static Node newNode(int key) 
{ 
    Node temp = new Node(); 
    temp.data= key; 
    temp.next = null; 
    return temp; 
} 

// Driver Code 
public static void Main(String[] args)  
{ 
    /* Let us create two linked lists to test 
    the above functions. Created lists shall be 
        a: 1->2->3->4 
        b: 1->2->1->2->3->4*/
    Node a = newNode(1); 
    a.next = newNode(2); 
    a.next.next = newNode(3); 
    a.next.next.next = newNode(4); 

    Node b = newNode(1); 
    b.next = newNode(2); 
    b.next.next = newNode(1); 
    b.next.next.next = newNode(2); 
    b.next.next.next.next = newNode(3); 
    b.next.next.next.next.next = newNode(4); 

    if(findList(a, b) == true)  
        Console.Write("LIST FOUND"); 
    else
        Console.Write("LIST NOT FOUND"); 
} 
} 

// This code is contributed by Rajput-Ji 

```

**输出**：

```
LIST FOUND

```

时间复杂度：O（m * n），其中 m 是第二个列表中的节点数，而 n 是第一个列表中的节点数。

**优化**：

上面的代码可以通过使用额外的空间进行优化，即将列表存储在两个字符串中并应用 [KMP 算法](https://www.geeksforgeeks.org/searching-for-patterns-set-2-kmp-algorithm/)。 请参阅 [https://ide.geeksforgeeks.org/3fXUaV](https://ide.geeksforgeeks.org/3fXUaV) 以获取 [**Nishant Singh**](https://practice.geeksforgeeks.org/user-profile.php?user=_code) 提供的实施方案。

本文由 [**Sahil Chhabra（akku）**](https://practice.geeksforgeeks.org/user-profile.php?user=sahil_coder) 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则也可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的内容，或者想共享有关上述主题的更多信息，请发表评论。

