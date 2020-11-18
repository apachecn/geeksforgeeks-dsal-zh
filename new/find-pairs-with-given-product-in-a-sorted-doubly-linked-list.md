# 在排序的双链表

中查找与给定产品的对

给定**个正相异元素**的排序的双链表，任务是在双链表中查找乘积等于给定值 x 的对，而不使用任何额外空间。

**范例**：

```
Input : List = 1 <=> 2 <=> 4 <=> 5 <=> 6 <=> 8 <=> 9
        x = 8
Output: (1, 8), (2, 4)

Input : List = 1 <=> 2 <=> 3 <=> 4 <=> 5 <=> 6 <=> 7
        x = 6
Output: (1, 6), (2, 3)

```

解决此问题的一种简单方法**是使用两个嵌套循环遍历链表，并找到所有对，并检查乘积等于 x 的对。 这个问题的时间复杂度将是 O（n ^ 2），n 是双向链表中节点的总数。**

针对此问题的**有效解决方案**与该文章的[相同。 这是算法：](https://www.geeksforgeeks.org/find-pairs-given-sum-doubly-linked-list/)

*   初始化两个指针变量以在排序的双链表中找到候选元素。 首先以双向链表的开头初始化；即 **first = head** ，然后用双向链表的最后一个节点初始化**，然后初始化**；即， **second = last_node** 。

*   我们将第一个和第二个指针初始化为第一个和最后一个节点。 这里我们没有随机访问权限，因此要找到第二个指针，我们遍历列表以初始化第二个指针。

*   如果当前的第一乘积和第二乘积小于 x，则我们首先向前移动。 如果第一元素和第二元素的当前乘积大于 x，则我们向后移动第二个元素。

*   循环终止条件也与阵列不同。 当两个指针中的任何一个变为 NULL 或它们彼此交叉（第二个->下一个=第一个），或者它们变为相同（第一个==第二个）时，循环终止

下面是上述方法的实现：

## C++

```cpp

// C++ program to find a pair with 
// given product x in sorted Doubly 
// Linked List 
#include <bits/stdc++.h> 
using namespace std; 

// Doubly Linked List Node 
struct Node { 
    int data; 
    struct Node *next, *prev; 
}; 

// Function to find pair whose product 
// equal to given value x 
void pairProduct(struct Node* head, int x) 
{ 
    // Set two pointers, 
    // first to the beginning of DLL 
    // and second to the end of DLL. 
    struct Node* first = head; 
    struct Node* second = head; 
    while (second->next != NULL) 
        second = second->next; 

    // To track if we find a pair or not 
    bool found = false; 

    // The loop terminates when either of two pointers 
    // become NULL, or they cross each other (second->next 
    // == first), or they become same (first == second) 
    while (first != NULL && second != NULL && first != second 
           && second->next != first) { 
        // pair found 
        if ((first->data * second->data) == x) { 
            found = true; 
            cout << "(" << first->data << ", "
                 << second->data << ")" << endl; 

            // move first in forward direction 
            first = first->next; 

            // move second in backward direction 
            second = second->prev; 
        } 
        else { 
            if ((first->data * second->data) < x) 
                first = first->next; 
            else
                second = second->prev; 
        } 
    } 

    // if pair is not present 
    if (found == false) 
        cout << "No pair found"; 
} 

// A utility function to insert a new node at the 
// beginning of doubly linked list 
void insert(struct Node** head, int data) 
{ 
    struct Node* temp = new Node; 
    temp->data = data; 
    temp->next = temp->prev = NULL; 
    if (!(*head)) 
        (*head) = temp; 
    else { 
        temp->next = *head; 
        (*head)->prev = temp; 
        (*head) = temp; 
    } 
} 

// Driver Code 
int main() 
{ 
    // Create Doubly Linked List 
    struct Node* head = NULL; 
    insert(&head, 9); 
    insert(&head, 8); 
    insert(&head, 6); 
    insert(&head, 5); 
    insert(&head, 4); 
    insert(&head, 2); 
    insert(&head, 1); 

    int x = 8; 

    pairProduct(head, x); 

    return 0; 
} 

```

## Java

```java

// Java program to find a pair with 
// given product x in sorted Doubly 
// Linked List 

class GFG { 

    // Doubly Linked List Node 
    static class Node { 
        int data; 
        Node next, prev; 
    }; 

    // Function to find pair whose product 
    // equal to given value x 
    static void pairProduct(Node head, int x) 
    { 
        // Set two pointers, 
        // first to the beginning of DLL 
        // and second to the end of DLL. 
        Node first = head; 
        Node second = head; 
        while (second.next != null) 
            second = second.next; 

        // To track if we find a pair or not 
        boolean found = false; 

        // The loop terminates when either of two pointers 
        // become null, or they cross each other (second.next 
        // == first), or they become same (first == second) 
        while (first != null && second != null && first != second 
               && second.next != first) { 
            // pair found 
            if ((first.data * second.data) == x) { 
                found = true; 
                System.out.println("(" + first.data + ", "
                                   + second.data + ")"); 

                // move first in forward direction 
                first = first.next; 

                // move second in backward direction 
                second = second.prev; 
            } 
            else { 
                if ((first.data * second.data) < x) 
                    first = first.next; 
                else
                    second = second.prev; 
            } 
        } 

        // if pair is not present 
        if (found == false) 
            System.out.println("No pair found"); 
    } 

    // A utility function to insert a new node at the 
    // beginning of doubly linked list 
    static Node insert(Node head, int data) 
    { 
        Node temp = new Node(); 
        temp.data = data; 
        temp.next = temp.prev = null; 
        if ((head) == null) 
            (head) = temp; 
        else { 
            temp.next = head; 
            (head).prev = temp; 
            (head) = temp; 
        } 
        return head; 
    } 

    // Driver Code 
    public static void main(String args[]) 
    { 
        // Create Doubly Linked List 
        Node head = null; 
        head = insert(head, 9); 
        head = insert(head, 8); 
        head = insert(head, 6); 
        head = insert(head, 5); 
        head = insert(head, 4); 
        head = insert(head, 2); 
        head = insert(head, 1); 

        int x = 8; 

        pairProduct(head, x); 
    } 
} 

// This code is contributed by Arnab Kundu 

```

## Python3

```py

# Python3 program to find a pair with 
# given product x in sorted Doubly 
# Linked List 

# Node of the doubly linked list  
class Node:  

    def __init__(self, data):  
        self.data = data  
        self.prev = None
        self.next = None

# Function to find pair whose product 
# equal to given value x 
def pairProduct(head, x): 

    # Set two pointers, 
    # first to the beginning of DLL 
    # and second to the end of DLL. 
    first = head 
    second = head 
    while (second.next != None): 
        second = second.next

    # To track if we find a pair or not 
    found = False

    # The loop terminates when either of two pointers 
    # become None, or they cross each other (second.next 
    # == first), or they become same (first == second) 
    while (first != None and second != None and 
           first != second and second.next != first) : 
        # pair found 
        if ((first.data * second.data) == x) : 
            found = True
            print("(", first.data, ", ", second.data, ")") 

            # move first in forward direction 
            first = first.next

            # move second in backward direction 
            second = second.prev 

        else : 
            if ((first.data * second.data) < x): 
                first = first.next
            else: 
                second = second.prev 

    # if pair is not present 
    if (found == False): 
        print( "No pair found") 

# A utility function to insert a new node at the 
# beginning of doubly linked list 
def insert(head, data): 

    temp = Node(0) 
    temp.data = data 
    temp.next = temp.prev = None
    if (head == None): 
        (head) = temp 
    else : 
        temp.next = head 
        (head).prev = temp 
        (head) = temp 
    return head 

# Driver Code 
if __name__ == "__main__":  

    # Create Doubly Linked List 
    head = None
    head = insert(head, 9) 
    head = insert(head, 8) 
    head = insert(head, 6) 
    head = insert(head, 5) 
    head = insert(head, 4) 
    head = insert(head, 2) 
    head = insert(head, 1) 

    x = 8

    pairProduct(head, x) 

# This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# program to find a pair with 
// given product x in sorted Doubly 
// Linked List 
using System; 

class GFG { 

    // Doubly Linked List Node 
    public class Node { 
        public int data; 
        public Node next, prev; 
    }; 

    // Function to find pair whose product 
    // equal to given value x 
    static void pairProduct(Node head, int x) 
    { 
        // Set two pointers, 
        // first to the beginning of DLL 
        // and second to the end of DLL. 
        Node first = head; 
        Node second = head; 
        while (second.next != null) 
            second = second.next; 

        // To track if we find a pair or not 
        bool found = false; 

        // The loop terminates when either of two pointers 
        // become null, or they cross each other (second.next 
        // == first), or they become same (first == second) 
        while (first != null && second != null && first != second 
               && second.next != first) { 
            // pair found 
            if ((first.data * second.data) == x) { 
                found = true; 
                Console.WriteLine("(" + first.data + ", "
                                  + second.data + ")"); 

                // move first in forward direction 
                first = first.next; 

                // move second in backward direction 
                second = second.prev; 
            } 
            else { 
                if ((first.data * second.data) < x) 
                    first = first.next; 
                else
                    second = second.prev; 
            } 
        } 

        // if pair is not present 
        if (found == false) 
            Console.WriteLine("No pair found"); 
    } 

    // A utility function to insert a new node at the 
    // beginning of doubly linked list 
    static Node insert(Node head, int data) 
    { 
        Node temp = new Node(); 
        temp.data = data; 
        temp.next = temp.prev = null; 
        if ((head) == null) 
            (head) = temp; 
        else { 
            temp.next = head; 
            (head).prev = temp; 
            (head) = temp; 
        } 
        return head; 
    } 

    // Driver Code 
    public static void Main(String[] args) 
    { 
        // Create Doubly Linked List 
        Node head = null; 
        head = insert(head, 9); 
        head = insert(head, 8); 
        head = insert(head, 6); 
        head = insert(head, 5); 
        head = insert(head, 4); 
        head = insert(head, 2); 
        head = insert(head, 1); 

        int x = 8; 

        pairProduct(head, x); 
    } 
} 

// This code contributed by Rajput-Ji 

```

**Output:**

```
(1, 8)
(2, 4)

```

**时间复杂度**：`O(n)`



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。