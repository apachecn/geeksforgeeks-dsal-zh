# 在链接列表

中从第K个节点开始，从末尾交换第K个节点。

给定一个单链表，从第k个节点开始从第k个节点开始交换。 **不允许交换数据，只应更改指针。** 在链表数据部分很大的许多情况下（例如，学生详细信息行名称，RollNo，地址等），此要求可能是合乎逻辑的。 指针总是固定的（大多数编译器为4个字节）。

**示例：**

```
Input: 1 -> 2 -> 3 -> 4 -> 5, K = 2
Output: 1 -> 4 -> 3 -> 2 -> 5 
Explanation: The 2nd node from 1st is 2 and 
2nd node from last is 4, so swap them.

Input: 1 -> 2 -> 3 -> 4 -> 5, K = 5
Output: 5 -> 2 -> 3 -> 4 -> 1 
Explanation: The 5th node from 1st is 5 and 
5th node from last is 1, so swap them.

```

**插图：**
![](img/5020d2aa46de8a3c1749bd32b34a9e80.png)

**方法：**这个想法很简单，从头开始找到第k个节点，从最后开始第k个节点是从头开始第n-k + 1个节点。 交换两个节点。
*但是，有些极端情况必须处理*

1.  Y在X旁边
2.  X在Y旁边
3.  X和Y相同
4.  X和Y不存在（k大于链接列表中的节点数）

下面是上述方法的实现。

## C ++

```

// A C++ program to swap Kth node 
// from beginning with kth node from end 
#include <bits/stdc++.h> 
using namespace std; 

// A Linked List node 
struct Node { 
    int data; 
    struct Node* next; 
}; 

/* Utility function to insert 
   a node at the beginning */
void push(struct Node** head_ref, int new_data) 
{ 
    struct Node* new_node 
        = (struct Node*)malloc( 
            sizeof(struct Node)); 
    new_node->data = new_data; 
    new_node->next = (*head_ref); 
    (*head_ref) = new_node; 
} 

/* Utility function for displaying linked list */
void printList(struct Node* node) 
{ 
    while (node != NULL) { 
        cout << node->data << " "; 
        node = node->next; 
    } 
    cout << endl; 
} 

/* Utility function for calculating  
   length of linked list */
int countNodes(struct Node* s) 
{ 
    int count = 0; 
    while (s != NULL) { 
        count++; 
        s = s->next; 
    } 
    return count; 
} 

/* Function for swapping kth nodes  
   from both ends of linked list */
void swapKth(struct Node** head_ref, int k) 
{ 
    // Count nodes in linked list 
    int n = countNodes(*head_ref); 

    // Check if k is valid 
    if (n < k) 
        return; 

    // If x (kth node from start) and 
    // y(kth node from end) are same 
    if (2 * k - 1 == n) 
        return; 

    // Find the kth node from the beginning of 
    // the linked list. We also find 
    // previous of kth node because we 
    // need to update next pointer of 
    // the previous. 
    Node* x = *head_ref; 
    Node* x_prev = NULL; 
    for (int i = 1; i < k; i++) { 
        x_prev = x; 
        x = x->next; 
    } 

    // Similarly, find the kth node from 
    // end and its previous. kth node 
    // from end is (n-k+1)th node from beginning 
    Node* y = *head_ref; 
    Node* y_prev = NULL; 
    for (int i = 1; i < n - k + 1; i++) { 
        y_prev = y; 
        y = y->next; 
    } 

    // If x_prev exists, then new next of 
    // it will be y. Consider the case 
    // when y->next is x, in this case, 
    // x_prev and y are same. So the statement 
    // "x_prev->next = y" creates a self loop. 
    // This self loop will be broken 
    // when we change y->next. 
    if (x_prev) 
        x_prev->next = y; 

    // Same thing applies to y_prev 
    if (y_prev) 
        y_prev->next = x; 

    // Swap next pointers of x and y. 
    // These statements also break self 
    // loop if x->next is y or y->next is x 
    Node* temp = x->next; 
    x->next = y->next; 
    y->next = temp; 

    // Change head pointers when k is 1 or n 
    if (k == 1) 
        *head_ref = y; 
    if (k == n) 
        *head_ref = x; 
} 

// Driver program to test above functions 
int main() 
{ 
    // Let us create the following 
    // linked list for testing 
    // 1->2->3->4->5->6->7->8 
    struct Node* head = NULL; 
    for (int i = 8; i >= 1; i--) 
        push(&head, i); 

    cout << "Original Linked List: "; 
    printList(head); 

    for (int k = 1; k < 9; k++) { 
        swapKth(&head, k); 
        cout << "\nModified List for k = " << k << endl; 
        printList(head); 
    } 

    return 0; 
} 

```

## 爪哇

```

// A Java program to swap kth 
// node from the beginning with 
// kth node from the end 

class Node { 
    int data; 
    Node next; 
    Node(int d) 
    { 
        data = d; 
        next = null; 
    } 
} 

class LinkedList { 
    Node head; 

    /* Utility function to insert  
       a node at the beginning */
    void push(int new_data) 
    { 
        Node new_node = new Node(new_data); 
        new_node.next = head; 
        head = new_node; 
    } 

    /* Utility function for displaying linked list */
    void printList() 
    { 
        Node node = head; 
        while (node != null) { 
            System.out.print(node.data + " "); 
            node = node.next; 
        } 
        System.out.println(""); 
    } 

    /* Utility function for calculating  
       length of linked list */
    int countNodes() 
    { 
        int count = 0; 
        Node s = head; 
        while (s != null) { 
            count++; 
            s = s.next; 
        } 
        return count; 
    } 

    /* Function for swapping kth nodes from  
       both ends of linked list */
    void swapKth(int k) 
    { 
        // Count nodes in linked list 
        int n = countNodes(); 

        // Check if k is valid 
        if (n < k) 
            return; 

        // If x (kth node from start) and 
        // y(kth node from end) are same 
        if (2 * k - 1 == n) 
            return; 

        // Find the kth node from beginning of linked list. 
        // We also find previous of kth node because we need 
        // to update next pointer of the previous. 
        Node x = head; 
        Node x_prev = null; 
        for (int i = 1; i < k; i++) { 
            x_prev = x; 
            x = x.next; 
        } 

        // Similarly, find the kth node from end and its 
        // previous. kth node from end is (n-k+1)th node 
        // from beginning 
        Node y = head; 
        Node y_prev = null; 
        for (int i = 1; i < n - k + 1; i++) { 
            y_prev = y; 
            y = y.next; 
        } 

        // If x_prev exists, then new next of it will be y. 
        // Consider the case when y->next is x, in this case, 
        // x_prev and y are same. So the statement 
        // "x_prev->next = y" creates a self loop. This self 
        // loop will be broken when we change y->next. 
        if (x_prev != null) 
            x_prev.next = y; 

        // Same thing applies to y_prev 
        if (y_prev != null) 
            y_prev.next = x; 

        // Swap next pointers of x and y. These statements 
        // also break self loop if x->next is y or y->next 
        // is x 
        Node temp = x.next; 
        x.next = y.next; 
        y.next = temp; 

        // Change head pointers when k is 1 or n 
        if (k == 1) 
            head = y; 

        if (k == n) 
            head = x; 
    } 

    // Driver code to test above 
    public static void main(String[] args) 
    { 
        LinkedList llist = new LinkedList(); 
        for (int i = 8; i >= 1; i--) 
            llist.push(i); 

        System.out.print("Original linked list: "); 
        llist.printList(); 
        System.out.println(""); 

        for (int i = 1; i < 9; i++) { 
            llist.swapKth(i); 
            System.out.println("Modified List for k = " + i); 
            llist.printList(); 
            System.out.println(""); 
        } 
    } 
} 

```

## Python3

```

""" 
A Python3 program to swap kth node from  
the beginning with kth node from the end 
"""
class Node: 
    def __init__(self, data, next = None): 
        self.data = data 
        self.next = next

class LinkedList: 

    def __init__(self, *args, **kwargs): 
        self.head = Node(None) 
    """ 
    Utility function to insert a node at the beginning 
    @args: 
        data: value of node 
    """
    def push(self, data): 
        node = Node(data) 
        node.next = self.head 
        self.head = node 

    # Print linked list 
    def printList(self): 
        node = self.head 
        while node.next is not None: 
            print(node.data, end = " ") 
            node = node.next

    # count number of node in linked list 
    def countNodes(self): 
        count = 0
        node = self.head 
        while node.next is not None: 
            count += 1
            node = node.next
        return count 

    """ 
    Function for swapping kth nodes from 
    both ends of linked list 
    """
    def swapKth(self, k): 

        # Count nodes in linked list 
        n = self.countNodes() 

        # check if k is valid 
        if n<k: 
            return

        """ 
        If x (kth node from start) and  
        y(kth node from end) are same  
        """
        if (2 * k - 1) == n: 
            return

        """ 
        Find the kth node from beginning of linked list.  
        We also find previous of kth node because we need  
        to update next pointer of the previous.  
        """
        x = self.head 
        x_prev = Node(None) 
        for i in range(k - 1): 
            x_prev = x 
            x = x.next

        """ 
        Similarly, find the kth node from end and its  
        previous. kth node from end is (n-k + 1)th node  
        from beginning  
        """
        y = self.head 
        y_prev = Node(None) 
        for i in range(n - k): 
            y_prev = y 
            y = y.next

        """ 
        If x_prev exists, then new next of it will be y.  
        Consider the case when y->next is x, in this case,  
        x_prev and y are same. So the statement  
        "x_prev->next = y" creates a self loop. This self  
        loop will be broken when we change y->next.  
        """
        if x_prev is not None: 
            x_prev.next = y 

        # Same thing applies to y_prev 
        if y_prev is not None: 
            y_prev.next = x 

        """ 
        Swap next pointers of x and y. These statements  
        also break self loop if x->next is y or y->next  
        is x  
        """
        temp = x.next
        x.next = y.next
        y.next = temp 

        # Change head pointers when k is 1 or n 
        if k == 1: 
            self.head = y 

        if k == n: 
            self.head = x 

# Driver Code 
llist = LinkedList() 
for i in range(8, 0, -1): 
    llist.push(i) 
llist.printList() 

for i in range(1, 9): 
    llist.swapKth(i) 
    print("Modified List for k = ", i) 
    llist.printList() 
    print("\n") 

# This code is contributed by Pulkit 

```

## C＃

```

// C# program to swap kth node from the beginning with 
// kth node from the end 
using System; 

public class Node { 
    public int data; 
    public Node next; 
    public Node(int d) 
    { 
        data = d; 
        next = null; 
    } 
} 

public class LinkedList { 
    Node head; 

    /* Utility function to insert  
    a node at the beginning */
    void push(int new_data) 
    { 
        Node new_node = new Node(new_data); 
        new_node.next = head; 
        head = new_node; 
    } 

    /* Utility function for displaying linked list */
    void printList() 
    { 
        Node node = head; 
        while (node != null) { 
            Console.Write(node.data + " "); 
            node = node.next; 
        } 
        Console.WriteLine(""); 
    } 

    /* Utility function for calculating  
    length of linked list */
    int countNodes() 
    { 
        int count = 0; 
        Node s = head; 
        while (s != null) { 
            count++; 
            s = s.next; 
        } 
        return count; 
    } 

    /* Function for swapping kth nodes from  
    both ends of linked list */
    void swapKth(int k) 
    { 
        // Count nodes in linked list 
        int n = countNodes(); 

        // Check if k is valid 
        if (n < k) 
            return; 

        // If x (kth node from start) and y(kth node from end) 
        // are same 
        if (2 * k - 1 == n) 
            return; 

        // Find the kth node from beginning of linked list. 
        // We also find previous of kth node because we need 
        // to update next pointer of the previous. 
        Node x = head; 
        Node x_prev = null; 
        for (int i = 1; i < k; i++) { 
            x_prev = x; 
            x = x.next; 
        } 

        // Similarly, find the kth node from end and its 
        // previous. kth node from end is (n-k+1)th node 
        // from beginning 
        Node y = head; 
        Node y_prev = null; 
        for (int i = 1; i < n - k + 1; i++) { 
            y_prev = y; 
            y = y.next; 
        } 

        // If x_prev exists, then new next of it will be y. 
        // Consider the case when y->next is x, in this case, 
        // x_prev and y are same. So the statement 
        // "x_prev->next = y" creates a self loop. This self 
        // loop will be broken when we change y->next. 
        if (x_prev != null) 
            x_prev.next = y; 

        // Same thing applies to y_prev 
        if (y_prev != null) 
            y_prev.next = x; 

        // Swap next pointers of x and y. These statements 
        // also break self loop if x->next is y or y->next 
        // is x 
        Node temp = x.next; 
        x.next = y.next; 
        y.next = temp; 

        // Change head pointers when k is 1 or n 
        if (k == 1) 
            head = y; 

        if (k == n) 
            head = x; 
    } 

    // Driver code 
    public static void Main(String[] args) 
    { 
        LinkedList llist = new LinkedList(); 
        for (int i = 8; i >= 1; i--) 
            llist.push(i); 

        Console.Write("Original linked list: "); 
        llist.printList(); 
        Console.WriteLine(""); 

        for (int i = 1; i < 9; i++) { 
            llist.swapKth(i); 
            Console.WriteLine("Modified List for k = " + i); 
            llist.printList(); 
            Console.WriteLine(""); 
        } 
    } 
} 

// This code has been contributed by 29AjayKumar 

```

**Output:**

```
Original Linked List: 1 2 3 4 5 6 7 8

Modified List for k = 1
8 2 3 4 5 6 7 1

Modified List for k = 2
8 7 3 4 5 6 2 1

Modified List for k = 3
8 7 6 4 5 3 2 1

Modified List for k = 4
8 7 6 5 4 3 2 1

Modified List for k = 5
8 7 6 4 5 3 2 1

Modified List for k = 6
8 7 3 4 5 6 2 1

Modified List for k = 7
8 2 3 4 5 6 7 1

Modified List for k = 8
1 2 3 4 5 6 7 8

```

**复杂度分析：**

*   **时间复杂度：** O（n），其中n是列表的长度。
    需要遍历该列表。
*   **辅助空间：** O（1）。
    不需要多余的空间。

请注意，以上代码运行三个单独的循环以对节点进行计数，查找x和x prev以及查找y和y_prev。 这三件事可以在一个循环中完成。 该代码使用三个循环来使事情保持简单易懂。

感谢 [Chandra Prakash](https://www.facebook.com/chandra.prakash.52643?fref=ts) 的初步解决方案。 如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论。

注意读者！ 现在不要停止学习。 通过 [**DSA自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的DSA概念，并为行业做好准备。