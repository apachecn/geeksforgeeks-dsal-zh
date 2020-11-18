# 以Zig-Zag格式重新排列链接列表

给定一个链表，重新排列它，以便转换后的链表的形式应为< b > c < d > e

**示例：**

```
Input:  1->2->3->4
Output: 1->3->2->4 

Input:  11->15->20->5->10
Output: 11->20->5->15->10

```

## 强烈建议您在继续解决方案之前，单击此处进行练习。

**一种简单的方法**就是通过合并排序对[排序链表，然后交换备用，但这需要O（n Log n）时间复杂度。 这里n是链表中元素的数量。](https://www.geeksforgeeks.org/merge-sort-for-linked-list/)

一种需要O（n）时间的**有效方法**，是使用类似于冒泡排序的单次扫描，然后维护一个标志来表示当前的顺序（）。 如果当前的两个元素不按该顺序排列，则交换这些元素，否则不进行交换。 有关交换顺序的详细说明，请参考[和](http://geeksquiz.com/converting-an-array-of-integers-into-zig-zag-fashion/)。

## C ++

```

// C++ program to arrange linked 
// list in zigzag fashion 
#include <bits/stdc++.h> 
using namespace std; 

/* Link list Node */
struct Node { 
    int data; 
    struct Node* next; 
}; 

// This function distributes the 
// Node in zigzag fashion 
void zigZagList(Node* head) 
{ 
    // If flag is true, then next 
    // node should be greater 
    // in the desired output. 
    bool flag = true; 

    // Traverse linked list starting from head. 
    Node* current = head; 
    while (current->next != NULL) { 
        if (flag) /* "<" relation expected */
        { 
            /* If we have a situation like A > B > C 
               where A, B and C are consecutive Nodes 
               in list we get A > B < C by swapping B 
               and C */
            if (current->data > current->next->data) 
                swap(current->data, current->next->data); 
        } 
        else /* ">" relation expected */
        { 
            /* If we have a situation like A < B < C where 
               A, B and C  are consecutive Nodes in list we 
               get A < C > B by swapping B and C */
            if (current->data < current->next->data) 
                swap(current->data, current->next->data); 
        } 

        current = current->next; 
        flag = !flag; /* flip flag for reverse checking */
    } 
} 

/* UTILITY FUNCTIONS */
/* Function to push a Node */
void push(Node** head_ref, int new_data) 
{ 
    /* allocate Node */
    struct Node* new_Node = new Node; 

    /* put in the data  */
    new_Node->data = new_data; 

    /* link the old list off the new Node */
    new_Node->next = (*head_ref); 

    /* move the head to point to the new Node */
    (*head_ref) = new_Node; 
} 

/* Function to print linked list */
void printList(struct Node* Node) 
{ 
    while (Node != NULL) { 
        printf("%d->", Node->data); 
        Node = Node->next; 
    } 
    printf("NULL"); 
} 

/* Driver program to test above function*/
int main(void) 
{ 
    /* Start with the empty list */
    struct Node* head = NULL; 

    // create a list 4 -> 3 -> 7 -> 8 -> 6 -> 2 -> 1 
    // answer should be -> 3  7  4  8  2  6  1 
    push(&head, 1); 
    push(&head, 2); 
    push(&head, 6); 
    push(&head, 8); 
    push(&head, 7); 
    push(&head, 3); 
    push(&head, 4); 

    printf("Given linked list \n"); 
    printList(head); 

    zigZagList(head); 

    printf("\nZig Zag Linked list \n"); 
    printList(head); 

    return (0); 
} 

```

## 爪哇

```

// Java program to arrange 
// linked list in zigzag fashion 
class GfG { 

    /* Link list Node */
    static class Node { 
        int data; 
        Node next; 
    } 
    static Node head = null; 
    static int temp = 0; 

    // This function distributes 
    // the Node in zigzag fashion 
    static void zigZagList(Node head) 
    { 
        // If flag is true, then 
        // next node should be greater 
        // in the desired output. 
        boolean flag = true; 

        // Traverse linked list starting from head. 
        Node current = head; 
        while (current != null && current.next != null) { 
            if (flag == true) /* "<" relation expected */
            { 
                /* If we have a situation like A > B > C  
            where A, B and C are consecutive Nodes  
            in list we get A > B < C by swapping B  
            and C */
                if (current.data > current.next.data) { 
                    temp = current.data; 
                    current.data = current.next.data; 
                    current.next.data = temp; 
                } 
            } 
            else /* ">" relation expected */
            { 
                /* If we have a situation like A < B < C where  
            A, B and C are consecutive Nodes in list we  
            get A < C > B by swapping B and C */
                if (current.data < current.next.data) { 
                    temp = current.data; 
                    current.data = current.next.data; 
                    current.next.data = temp; 
                } 
            } 

            current = current.next; 

            /* flip flag for reverse checking */
            flag = !(flag); 
        } 
    } 

    /* UTILITY FUNCTIONS */
    /* Function to push a Node */
    static void push(int new_data) 
    { 
        /* allocate Node */
        Node new_Node = new Node(); 

        /* put in the data */
        new_Node.data = new_data; 

        /* link the old list off the new Node */
        new_Node.next = (head); 

        /* move the head to point to the new Node */
        (head) = new_Node; 
    } 

    /* Function to print linked list */
    static void printList(Node Node) 
    { 
        while (Node != null) { 
            System.out.print(Node.data + "->"); 
            Node = Node.next; 
        } 
        System.out.println("NULL"); 
    } 

    /* Driver code*/
    public static void main(String[] args) 
    { 
        /* Start with the empty list */
        // Node head = null; 

        // create a list 4 -> 3 -> 7 -> 8 -> 6 -> 2 -> 1 
        // answer should be -> 3 7 4 8 2 6 1 
        push(1); 
        push(2); 
        push(6); 
        push(8); 
        push(7); 
        push(3); 
        push(4); 

        System.out.println("Given linked list "); 
        printList(head); 

        zigZagList(head); 

        System.out.println("Zig Zag Linked list "); 
        printList(head); 
    } 
} 

// This code is contributed by 
// Prerna Saini. 

```

## 蟒蛇

```

# Python code to rearrange linked list in zig zac fashion 

# Node class  
class Node:  

    # Constructor to initialize the node object  
    def __init__(self, data):  
        self.data = data  
        self.next = None

# This function distributes the Node in zigzag fashion 
def zigZagList(head): 

    # If flag is true, then next node should be greater 
    # in the desired output. 
    flag = True

    # Traverse linked list starting from head. 
    current = head 
    while (current.next != None): 

        if (flag): # "<" relation expected 

            # If we have a situation like A > B > C 
            # where A, B and C are consecutive Nodes 
            # in list we get A > B < C by swapping B 
            # and C  
            if (current.data > current.next.data): 
                t = current.data 
                current.data = current.next.data 
                current.next.data = t 

        else :# ">" relation expected 

            # If we have a situation like A < B < C where 
            # A, B and C are consecutive Nodes in list we 
            # get A < C > B by swapping B and C  
            if (current.data < current.next.data): 
                t = current.data 
                current.data = current.next.data 
                current.next.data = t 

        current = current.next
        if(flag): 
            flag = False # flip flag for reverse checking  
        else: 
            flag = True
    return head 

# function to insert a Node in  
# the linked list at the beginning. 
def push(head, k): 

    tem = Node(0) 
    tem.data = k 
    tem.next = head 
    head = tem 
    return head 

# function to display Node of linked list. 
def display( head): 

    curr = head 
    while (curr != None):  
        print( curr.data, "->", end =" ") 
        curr = curr.next

    print("None") 

# Driver code 

head = None

# create a list 4 -> 3 -> 7 -> 8 -> 6 -> 2 -> 1 
# answer should be -> 3 7 4 8 2 6 1 
head = push(head, 1) 
head = push(head, 2) 
head = push(head, 6) 
head = push(head, 8) 
head = push(head, 7) 
head = push(head, 3) 
head = push(head, 4) 

print("Given linked list \n") 
display(head) 

head = zigZagList(head) 

print("\nZig Zag Linked list \n") 
display(head) 

# This code is contributed by Arnab Kundu 

```

## C＃

```

// C# program to arrange 
// linked list in zigzag fashion 
using System; 

class GfG { 

    /* Link list Node */
    class Node { 
        public int data; 
        public Node next; 
    } 
    static Node head = null; 
    static int temp = 0; 

    // This function distributes 
    // the Node in zigzag fashion 
    static void zigZagList(Node head) 
    { 
        // If flag is true, then 
        // next node should be greater 
        // in the desired output. 
        bool flag = true; 

        // Traverse linked list starting from head. 
        Node current = head; 
        while (current != null && current.next != null) { 
            if (flag == true) /* "<" relation expected */
            { 
                /* If we have a situation like A > B > C  
                where A, B and C are consecutive Nodes  
                in list we get A > B < C by swapping B  
                and C */
                if (current != null && current.next != null && current.data > current.next.data) { 
                    temp = current.data; 
                    current.data = current.next.data; 
                    current.next.data = temp; 
                } 
            } 
            else /* ">" relation expected */
            { 
                /* If we have a situation like A < B < C where  
                A, B and C are consecutive Nodes in list we  
                get A < C > B by swapping B and C */
                if (current != null && current.next != null && current.data < current.next.data) { 
                    temp = current.data; 
                    current.data = current.next.data; 
                    current.next.data = temp; 
                } 
            } 

            current = current.next; 

            /* flip flag for reverse checking */
            flag = !(flag); 
        } 
    } 

    /* UTILITY FUNCTIONS */
    /* Function to push a Node */
    static void push(int new_data) 
    { 
        /* allocate Node */
        Node new_Node = new Node(); 

        /* put in the data */
        new_Node.data = new_data; 

        /* link the old list off the new Node */
        new_Node.next = (head); 

        /* move the head to point to the new Node */
        (head) = new_Node; 
    } 

    /* Function to print linked list */
    static void printList(Node Node) 
    { 
        while (Node != null) { 
            Console.Write(Node.data + "->"); 
            Node = Node.next; 
        } 
        Console.WriteLine("NULL"); 
    } 

    /* Driver code*/
    public static void Main() 
    { 
        /* Start with the empty list */
        // Node head = null; 

        // create a list 4 -> 3 -> 7 -> 8 -> 6 -> 2 -> 1 
        // answer should be -> 3 7 4 8 2 6 1 
        push(1); 
        push(2); 
        push(6); 
        push(8); 
        push(7); 
        push(3); 
        push(4); 

        Console.WriteLine("Given linked list "); 
        printList(head); 

        zigZagList(head); 

        Console.WriteLine("Zig Zag Linked list "); 
        printList(head); 
    } 
} 
/* This code is contributed PrinciRaj1992 */

```

**Output:**

```
Given linked list 
4->3->7->8->6->2->1->NULL

Zig Zag Linked list 
3->7->4->8->2->6->1->NULL 

```

在上面的代码中，push函数将节点推入链表的最前面，可以轻松修改代码以将节点推到链表的末尾。 要注意的另一件事是，为简单起见，两个节点之间的数据交换是通过按值交换而不是通过链接交换来完成的，有关通过链接交换的技术，请参见[此](https://www.geeksforgeeks.org/swap-nodes-in-a-linked-list-without-swapping-data/)。

**复杂度分析：**

*   **时间复杂度：** O（n）。
    列表的遍历仅执行一次，并且包含“ n”个元素。
*   **辅助空间：** O（1）。
    不使用额外的数据结构来存储值。

本文由 [Utkarsh Trivedi](http://qa.geeksforgeeks.org/user/utkarsh111) 提供。 如果发现任何不正确的地方，或者您想分享有关上述主题的更多信息，请发表评论

注意读者！ 现在不要停止学习。 通过 [**DSA自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的DSA概念，并为行业做好准备。