# 从排序的链接列表

中删除所有出现的重复项

给定一个已排序的链表，删除所有具有重复编号（所有出现次数）的节点，仅保留在原始列表中仅出现一次的编号。
**范例：**

```
Input : 23->28->28->35->49->49->53->53
Output : 23->35

Input : 11->11->11->11->75->75
Output : empty List

```

请注意，这不同于[从链接列表](https://www.geeksforgeeks.org/remove-duplicates-from-a-sorted-linked-list/)中删除重复项

这个想法是要维护指向该节点的指针*（prev）*，该指针恰好在我们正在检查重复项的节点块之前。 在第一个示例中，当我们检查节点28的重复项时，指针 *prev* 将指向23。一旦到达最后一个具有值28的重复节点（将其命名为*当前*指针） ，我们可以将上一个节点的下一个字段作为当前字段的下一个字段，并更新 *current = current.next* 。 这将删除具有重复项的值为28的节点块。

## C ++

```

// C++ program to remove all  
// occurrences of duplicates  
// from a sorted linked list. 
#include <bits/stdc++.h> 
using namespace std; 

// A linked list node 
struct Node 
{ 
    int data; 
    struct Node *next; 
}; 

// Utility function  
// to create a new Node 
struct Node *newNode(int data) 
{ 
Node *temp = new Node; 
temp -> data = data; 
temp -> next = NULL; 
return temp; 
} 

// Function to print nodes  
// in a given linked list. 
void printList(struct Node *node) 
{ 
    while (node != NULL) 
    { 
        printf("%d ", node -> data); 
        node = node -> next; 
    } 
} 

// Function to remove all occurrences 
// of duplicate elements 
void removeAllDuplicates(struct Node* &start) 
{ 
    // create a dummy node  
    // that acts like a fake 
    // head of list pointing 
    // to the original head 
    Node* dummy = new Node; 

    // dummy node points 
    // to the original head 
    dummy -> next = start; 

    // Node pointing to last  
    // node which has no duplicate. 
    Node* prev = dummy; 

    // Node used to traverse 
    // the linked list. 
    Node* current = start; 

    while(current != NULL) 
    { 
        // Until the current and  
        // previous values are  
        // same, keep updating current 
        while(current -> next != NULL && 
              prev -> next -> data == current -> next -> data) 
            current = current -> next; 

        // if current has unique value  
        // i.e current is not updated,  
        // Move the prev pointer to  
        // next node 
        if (prev -> next == current) 
            prev = prev -> next; 

        // when current is updated  
        // to the last duplicate  
        // value of that segment,  
        // make prev the next of current 
        else
            prev -> next = current -> next; 

        current = current -> next; 
    } 

    // update original head to  
    // the next of dummy node  
    start = dummy -> next; 
} 

// Driver Code 
int main()  
{ 
    // 23->28->28->35->49->49->53->53 
    struct Node* start = newNode(23); 
    start -> next = newNode(28); 
    start -> next -> next = newNode(28); 
    start -> next ->  
     next -> next = newNode(35); 
    start -> next ->  
    next -> next -> next = newNode(49); 
    start -> next ->  
    next -> next ->  
    next -> next = newNode(49); 
    start -> next ->  
    next -> next ->  
    next -> next -> next = newNode(53); 
    start -> next ->  
    next -> next ->  
    next -> next ->  
    next -> next = newNode(53); 
    cout << "List before removal " << 
                  "of duplicates\n"; 
    printList(start); 

    removeAllDuplicates(start); 

    cout << "\nList after removal " <<  
                   "of duplicates\n"; 
    printList(start); 
    return 0; 
} 

// This code is contributed  
// by NIKHIL JINDAL 

```

## 爪哇

```

// Java program to remove all occurrences of 
// duplicates from a sorted linked list  

// class to create Linked lIst  
class LinkedList{ 

// head of linked list  
Node head = null;  
class Node 
{ 

    // value in the node  
    int val;  
    Node next; 
    Node(int v) 
    { 

        // default value of the next 
        // pointer field  
        val = v; 
        next = null; 
    } 
} 

// Function to insert data nodes into 
// the Linked List at the front 
public void insert(int data) 
{ 
    Node new_node = new Node(data); 
    new_node.next = head; 
    head = new_node; 
} 

// Function to remove all occurrences 
// of duplicate elements  
public void removeAllDuplicates() 
{ 

    // Create a dummy node that acts like a fake 
    // head of list pointing to the original head 
    Node dummy = new Node(0); 

    // Dummy node points to the original head 
    dummy.next = head; 
    Node prev = dummy; 
    Node current = head; 

    while (current != null) 
    { 
        // Until the current and previous values 
        // are same, keep updating current  
        while (current.next != null && 
               prev.next.val == current.next.val) 
               current = current.next; 

        // If current has unique value i.e current 
        // is not updated, Move the prev pointer 
        // to next node 
        if (prev.next == current) 
            prev = prev.next; 

        // When current is updated to the last 
        // duplicate value of that segment, make 
        // prev the next of current*/ 
        else
            prev.next = current.next; 

        current = current.next; 
    } 

    // Update original head to the next of dummy 
    // node  
    head = dummy.next; 
} 

// Function to print the list elements 
public void printList() 
{ 
    Node trav = head; 
    if (head == null) 
        System.out.print(" List is empty" ); 

    while (trav != null) 
    { 
        System.out.print(trav.val + " "); 
        trav = trav.next; 
    } 
} 

// Driver code 
public static void main(String[] args) 
{ 
    LinkedList ll = new LinkedList(); 
    ll.insert(53); 
    ll.insert(53); 
    ll.insert(49); 
    ll.insert(49); 
    ll.insert(35); 
    ll.insert(28); 
    ll.insert(28); 
    ll.insert(23); 

    System.out.println("Before removal of duplicates"); 
    ll.printList(); 

    ll.removeAllDuplicates(); 

    System.out.println("\nAfter removal of duplicates"); 
    ll.printList(); 
} 
} 

```

## Python3

```

# Python3 implementation for the above approach 

# Creating node 
class Node: 
    def __init__(self, val): 
        self.val = val 
        self.next = None
class LinkedList: 
    def __init__(self): 
        self.head = None

    # add node into beganing of linked list 
    def push(self, new_data): 
        new_node = Node(new_data) 
        new_node.next = self.head 
        self.head = new_node 
        return new_node 

    # Function to remove all occurrences 
    # of duplicate elements 
    def removeAllDuplicates(self, temp): 

        # temp is head node of linkedlist 
        curr = temp 
        # print(' print something') 
        head = prev = Node(None) 
        head.next = curr 

        # Here we use same as we do in removing  
        # duplicates and only extra thing is that 
        # we need to remove all elements  
        # having duplicates that we did in 30-31 
        while curr and curr.next: 

            # until the current value and next  
            # value are same keep updating the current value 
            if curr.val == curr.next.val: 
                while(curr and curr.next and 
                      curr.val == curr.next.val): 
                    curr = curr.next

                    # still one of duplicate values left 
                    # so point prec to curr 
                curr = curr.next
                prev.next = curr 
            else: 
                prev = prev.next
                curr = curr.next
        return head.next

    # for print the linkedlist 
    def printList(self): 
        temp1 = self.head 
        while temp1 is not None: 
            print(temp1.val, end = " ") 
            temp1 = temp1.next

    # For getting head of linkedlist 
    def get_head(self): 
        return self.head 

# Driver Code 
if __name__=='__main__': 
    llist = LinkedList() 
    llist.push(53) 
    llist.push(53) 
    llist.push(49) 
    llist.push(49) 
    llist.push(35) 
    llist.push(28) 
    llist.push(28) 
    llist.push(23) 

    print('Created linked list is:') 
    llist.printList() 
    print('\nLinked list after deletion of duplicates:') 
    head1 = llist.get_head() 
    #print(head1) 
    llist.removeAllDuplicates(head1) 
    llist.printList() 

# This code is contributed  
# by PRAVEEN KUMAR(IIIT KALYANI) 

```

## C＃

```

/* C# program to remove all occurrences of 
duplicates from a sorted linked list */

using System; 

/* class to create Linked lIst */
public class LinkedList 
{ 
    Node head = null; /* head of linked list */
    class Node 
    { 
        public int val; /* value in the node */
        public Node next; 
        public Node(int v) 
        { 
            /* default value of the next 
            pointer field */
            val = v; 
            next = null; 
        } 
    } 

    /* Function to insert data nodes into 
    the Linked List at the front */
    public void insert(int data) 
    { 
        Node new_node = new Node(data); 
        new_node.next = head; 
        head = new_node; 
    } 

    /* Function to remove all occurrences 
    of duplicate elements */
    public void removeAllDuplicates() 
    { 
    /* create a dummy node that acts like a fake 
        head of list pointing to the original head*/
        Node dummy = new Node(0); 

        /* dummy node points to the original head*/
        dummy.next = head; 
        Node prev = dummy; 
        Node current = head; 

        while (current != null) 
        { 
            /* Until the current and previous values 
            are same, keep updating current */
            while (current.next != null && 
                prev.next.val == current.next.val) 
                current = current.next; 

            /* if current has unique value i.e current 
                is not updated, Move the prev pointer 
                to next node*/
            if (prev.next == current) 
                prev = prev.next; 

            /* when current is updated to the last 
            duplicate value of that segment, make 
            prev the next of current*/
            else
                prev.next = current.next; 

            current = current.next; 
        } 

        /* update original head to the next of dummy 
        node */
        head = dummy.next; 
    } 

    /* Function to print the list elements */
    public void printList() 
    { 
        Node trav = head; 
        if (head == null) 
            Console.Write(" List is empty" ); 
        while (trav != null) 
        { 
            Console.Write(trav.val + " "); 
            trav = trav.next; 
        } 
    } 

    /* Driver code */
    public static void Main(String[] args) 
    { 
        LinkedList ll = new LinkedList(); 
        ll.insert(53); 
        ll.insert(53); 
        ll.insert(49); 
        ll.insert(49); 
        ll.insert(35); 
        ll.insert(28); 
        ll.insert(28); 
        ll.insert(23); 
        Console.WriteLine("Before removal of duplicates"); 
        ll.printList(); 

        ll.removeAllDuplicates(); 

        Console.WriteLine("\nAfter removal of duplicates"); 
        ll.printList(); 
    } 
} 

// This code is contributed by Rajput-Ji 

```

**输出：**

```
List before removal of duplicates
23 28 28 35 49 49 53 53 
List after removal of duplicates
23 35 

```

**时间复杂度：** O（n）

本文由 **Saloni Baweja** 提供。 如果您喜欢GeeksforGeeks并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至tribution@geeksforgeeks.org。 查看您的文章出现在GeeksforGeeks主页上，并帮助其他Geeks。
如果发现任何不正确的内容，或者想分享有关上述主题的更多信息，请发表评论。

注意读者！ 现在不要停止学习。 通过 [**DSA自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的DSA概念，并为行业做好准备。