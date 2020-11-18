# 使用`O(1)`额外空间的链表中最长回文列表的长度

> 原文：[https://www.geeksforgeeks.org/length-longest-palindrome-list-linked-list-using-o1-extra-space/](https://www.geeksforgeeks.org/length-longest-palindrome-list-linked-list-using-o1-extra-space/)

给定一个链表，找到该链表中存在的最长回文列表的长度。

例子：

```
Input  : List = 2->3->7->3->2->12->24
Output : 5
The longest palindrome list is 2->3->7->3->2

Input  : List = 12->4->4->3->14
Output : 2
The longest palindrome list is 4->4

```

一个简单的解决方案是将链接列表的内容复制到数组，然后在数组中找到最长的回文子数组，但是此解决方案是不允许的，因为它需要额外的空间。

该思想基于[迭代链表反向过程](https://www.geeksforgeeks.org/write-a-function-to-reverse-the-nodes-of-a-linked-list/)。 我们遍历给定的链表，并从左开始逐个反向地翻转链表的每个前缀。 反转前缀后，我们找到从反转前缀开始的最长公共列表，并在反转前缀之后找到列表。

以下是上述想法的实现。

## C++

```cpp

// C++ program to find longest palindrome 
// sublist in a list in O(1) time. 
#include<bits/stdc++.h> 
using namespace std; 

//structure of the linked list 
struct Node 
{ 
    int data; 
    struct Node* next; 
}; 

// function for counting the common elements 
int countCommon(Node *a, Node *b) 
{ 
    int count = 0; 

    // loop to count coomon in the list starting 
    // from node a and b 
    for (; a && b; a = a->next, b = b->next) 

        // increment the count for same values 
        if (a->data == b->data) 
            ++count; 
        else
            break; 

    return count; 
} 

// Returns length of the longest palindrome 
// sublist in given list 
int maxPalindrome(Node *head) 
{ 
    int result = 0; 
    Node *prev = NULL, *curr = head; 

    // loop till the end of the linked list 
    while (curr) 
    { 
        // The sublist from head to current 
        // reversed. 
        Node *next = curr->next; 
        curr->next = prev; 

        // check for odd length palindrome 
        // by finding longest common list elements 
        // beginning from prev and from next (We 
        // exclude curr) 
        result = max(result, 
                     2*countCommon(prev, next)+1); 

        // check for even length palindrome 
        // by finding longest common list elements 
        // beginning from curr and from next 
        result = max(result, 
                     2*countCommon(curr, next)); 

        // update prev and curr for next iteration 
        prev = curr; 
        curr = next; 
    } 
    return result; 
} 

// Utility function to create a new list node 
Node *newNode(int key) 
{ 
    Node *temp = new Node; 
    temp->data = key; 
    temp->next = NULL; 
    return temp; 
} 

/* Driver program to test above functions*/
int main() 
{ 
    /* Let us create a linked lists to test 
       the functions 
    Created list is a: 2->4->3->4->2->15 */
    Node *head = newNode(2); 
    head->next = newNode(4); 
    head->next->next = newNode(3); 
    head->next->next->next = newNode(4); 
    head->next->next->next->next = newNode(2); 
    head->next->next->next->next->next = newNode(15); 

    cout << maxPalindrome(head) << endl; 
    return 0; 
} 

```

## Java

```java

// Java program to find longest palindrome  
// sublist in a list in O(1) time.  
class GfG  
{  

//structure of the linked list  
static class Node  
{  
    int data;  
    Node next;  
} 

// function for counting the common elements  
static int countCommon(Node a, Node b)  
{  
    int count = 0;  

    // loop to count coomon in the list starting  
    // from node a and b  
    for (; a != null && b != null; 
            a = a.next, b = b.next)  

        // increment the count for same values  
        if (a.data == b.data)  
            ++count;  
        else
            break;  

    return count;  
}  

// Returns length of the longest palindrome  
// sublist in given list  
static int maxPalindrome(Node head)  
{  
    int result = 0;  
    Node prev = null, curr = head;  

    // loop till the end of the linked list  
    while (curr != null)  
    {  
        // The sublist from head to current  
        // reversed.  
        Node next = curr.next;  
        curr.next = prev;  

        // check for odd length  
        // palindrome by finding  
        // longest common list elements  
        // beginning from prev and  
        // from next (We exclude curr)  
        result = Math.max(result,  
                    2 * countCommon(prev, next)+1);  

        // check for even length palindrome  
        // by finding longest common list elements  
        // beginning from curr and from next  
        result = Math.max(result,  
                    2*countCommon(curr, next));  

        // update prev and curr for next iteration  
        prev = curr;  
        curr = next;  
    }  
    return result;  
}  

// Utility function to create a new list node  
static Node newNode(int key)  
{  
    Node temp = new Node();  
    temp.data = key;  
    temp.next = null;  
    return temp;  
}  

/* Driver code*/
public static void main(String[] args)  
{  
    /* Let us create a linked lists to test  
    the functions  
    Created list is a: 2->4->3->4->2->15 */
    Node head = newNode(2);  
    head.next = newNode(4);  
    head.next.next = newNode(3);  
    head.next.next.next = newNode(4);  
    head.next.next.next.next = newNode(2);  
    head.next.next.next.next.next = newNode(15);  

    System.out.println(maxPalindrome(head));  
}  
}  

// This code is contributed by  
// Prerna Saini. 

```

## Python

```py

# Python program to find longest palindrome  
# sublist in a list in O(1) time.  

# Linked List node  
class Node:  
    def __init__(self, data):  
        self.data = data  
        self.next = None

# function for counting the common elements  
def countCommon(a, b) : 

    count = 0

    # loop to count coomon in the list starting  
    # from node a and b  
    while ( a != None and b != None ) : 

        # increment the count for same values  
        if (a.data == b.data) : 
            count = count + 1
        else: 
            break

        a = a.next
        b = b.next

    return count  

# Returns length of the longest palindrome  
# sublist in given list  
def maxPalindrome(head) : 

    result = 0
    prev = None
    curr = head  

    # loop till the end of the linked list  
    while (curr != None) : 

        # The sublist from head to current  
        # reversed.  
        next = curr.next
        curr.next = prev  

        # check for odd length  
        # palindrome by finding  
        # longest common list elements  
        # beginning from prev and  
        # from next (We exclude curr)  
        result = max(result,  
                    2 * countCommon(prev, next) + 1)  

        # check for even length palindrome  
        # by finding longest common list elements  
        # beginning from curr and from next  
        result = max(result,  
                    2 * countCommon(curr, next))  

        # update prev and curr for next iteration  
        prev = curr  
        curr = next

    return result  

# Utility function to create a new list node  
def newNode(key) : 

    temp = Node(0)  
    temp.data = key  
    temp.next = None
    return temp  

# Driver code 

# Let us create a linked lists to test  
# the functions  
# Created list is a: 2->4->3->4->2->15  
head = newNode(2)  
head.next = newNode(4)  
head.next.next = newNode(3)  
head.next.next.next = newNode(4)  
head.next.next.next.next = newNode(2)  
head.next.next.next.next.next = newNode(15)  

print(maxPalindrome(head))  

# This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# program to find longest palindrome  
// sublist in a list in O(1) time.  
using System; 

class GfG  
{  

//structure of the linked list  
public class Node  
{  
    public int data;  
    public Node next;  
}  

// function for counting the common elements  
static int countCommon(Node a, Node b)  
{  
    int count = 0;  

    // loop to count coomon in the list starting  
    // from node a and b  
    for (; a != null && b != null;  
            a = a.next, b = b.next)  

        // increment the count for same values  
        if (a.data == b.data)  
            ++count;  
        else
            break;  

    return count;  
}  

// Returns length of the longest palindrome  
// sublist in given list  
static int maxPalindrome(Node head)  
{  
    int result = 0;  
    Node prev = null, curr = head;  

    // loop till the end of the linked list  
    while (curr != null)  
    {  
        // The sublist from head to current  
        // reversed.  
        Node next = curr.next;  
        curr.next = prev;  

        // check for odd length  
        // palindrome by finding  
        // longest common list elements  
        // beginning from prev and  
        // from next (We exclude curr)  
        result = Math.Max(result,  
                    2 * countCommon(prev, next)+1);  

        // check for even length palindrome  
        // by finding longest common list elements  
        // beginning from curr and from next  
        result = Math.Max(result,  
                    2*countCommon(curr, next));  

        // update prev and curr for next iteration  
        prev = curr;  
        curr = next;  
    }  
    return result;  
}  

// Utility function to create a new list node  
static Node newNode(int key)  
{  
    Node temp = new Node();  
    temp.data = key;  
    temp.next = null;  
    return temp;  
}  

/* Driver code*/
public static void Main(String []args)  
{  
    /* Let us create a linked lists to test  
    the functions  
    Created list is a: 2->4->3->4->2->15 */
    Node head = newNode(2);  
    head.next = newNode(4);  
    head.next.next = newNode(3);  
    head.next.next.next = newNode(4);  
    head.next.next.next.next = newNode(2);  
    head.next.next.next.next.next = newNode(15);  

    Console.WriteLine(maxPalindrome(head));  
}  
}  

// This code is contributed by Arnab Kundu 

```

**Output :**

```
5
```

**时间复杂度**：O（n <sup>2</sup> ）

请注意，上面的代码修改了给定的链表，并且如果不允许对链表进行修改，则可能无法正常工作。 但是，我们最终可以再做一次反向操作，以恢复原始列表。

本文由 **Niteesh kumar** 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论。

