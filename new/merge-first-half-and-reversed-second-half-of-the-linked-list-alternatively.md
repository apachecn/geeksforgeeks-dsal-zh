# 交替合并链接列表的前半部分和后半部分

给定一个链表，任务是按照以下方式重新排列链表：

1.  反转给定链表的后半部分。

类似地，以替代方式排列所有元素，即从上半部分获取链表的第3个元素，从下半部分获取链表的第4个元素。

**示例：**

```
Input: 1->2->3->4->5
Output: 1->5->2->4->3

Input: 1->2->3->4->5->6
Output: 1->6->2->5->3->4

```

**方法：**最初找到链表的中间节点。 该方法已在中讨论过。 从中间到结尾颠倒链接列表。 反向链接列表后，请从头开始遍历，并同时从列表的前半部分插入一个节点，并从链表的后半部分同时插入另一个节点。 继续此过程，直到到达中间节点。 到达中间节点后，将中间节​​点之前的节点指向NULL。

下面是上述方法的实现：

## C ++

```

// C++ program to sandwich the last part of 
// linked list in between the first part of 
// the linked list 
#include<bits/stdc++.h> 
#include <stdio.h> 
using namespace std; 

struct node { 
    int data; 
    struct node* next; 
}; 

// Function to reverse Linked List 
struct node* reverseLL(struct node* root) 
{ 
    struct node *prev = NULL, *current = root, *next; 
    while (current) { 
        next = current->next; 
        current->next = prev; 
        prev = current; 
        current = next; 
    } 

    // root needs to be upated after reversing 
    root = prev; 
    return root; 
} 

// Function to modify Linked List 
void modifyLL(struct node* root) 
{ 
    // Find the mid node 
    struct node *slow_ptr = root, *fast_ptr = root; 
    while (fast_ptr && fast_ptr->next) { 
        fast_ptr = fast_ptr->next->next; 
        slow_ptr = slow_ptr->next; 
    } 

    // Reverse the second half of the list 
    struct node* root2 = reverseLL(slow_ptr->next); 

    // partition the list 
    slow_ptr->next = NULL; 

    struct node *current1 = root, *current2 = root2; 

    // insert the elements in between 
    while (current1 && current2) { 

        // next node to be traversed in the first list 
        struct node* dnext1 = current1->next; 

        // next node to be traversed in the first list 
        struct node* dnext2 = current2->next; 
        current1->next = current2; 
        current2->next = dnext1; 
        current1 = dnext1; 
        current2 = dnext2; 
    } 
} 

// Function to insert node after the end 
void insertNode(struct node** start, int val) 
{ 

    // allocate memory 
    struct node* temp = (struct node*)malloc(sizeof(struct node)); 
    temp->data = val; 

    // if first node 
    if (*start == NULL) 
        *start = temp; 
    else { 

        // move to the end pointer of node 
        struct node* dstart = *start; 
        while (dstart->next != NULL) 
            dstart = dstart->next; 
        dstart->next = temp; 
    } 
} 

// function to print the linked list 
void display(struct node** start) 
{ 
    struct node* temp = *start; 

    // traverse till the entire linked 
    // list is printed 
    while (temp->next != NULL) { 
        printf("%d->", temp->data); 
        temp = temp->next; 
    } 
    printf("%d\n", temp->data); 
} 

// Driver Code 
int main() 
{ 
    // Odd Length Linked List 
    struct node* start = NULL; 
    insertNode(&start, 1); 
    insertNode(&start, 2); 
    insertNode(&start, 3); 
    insertNode(&start, 4); 
    insertNode(&start, 5); 

    printf("Before Modifying: "); 
    display(&start); 
    modifyLL(start); 
    printf("After Modifying: "); 
    display(&start); 

    // Even Length Linked List 
    start = NULL; 
    insertNode(&start, 1); 
    insertNode(&start, 2); 
    insertNode(&start, 3); 
    insertNode(&start, 4); 
    insertNode(&start, 5); 
    insertNode(&start, 6); 

    printf("\nBefore Modifying: "); 
    display(&start); 
    modifyLL(start); 
    printf("After Modifying: "); 
    display(&start); 

    return 0; 
} 

```

## 爪哇

```

// Java program to sandwich the  
// last part of linked list in  
// between the first part of 
// the linked list 
import java.util.*; 

class node  
{ 
    int data; 
    node next; 
    node(int key) 
    { 
        data = key; 
        next = null; 
    } 
} 

class GFG 
{ 

// Function to reverse 
// Linked List 
public static node reverseLL(node root) 
{ 

     node prev = null,  
     current = root, next; 
    while (current!= null)  
    { 
        next = current.next; 
        current.next = prev; 
        prev = current; 
        current = next; 
    } 

    // root needs to be  
    // upated after reversing 
    root = prev; 
    return root; 
} 

// Function to modify 
// Linked List 
public static void modifyLL( node root) 
{ 
    // Find the mid node 
     node slow_ptr = root, fast_ptr = root; 
    while (fast_ptr != null &&  
           fast_ptr.next != null)  
    { 
        fast_ptr = fast_ptr.next.next; 
        slow_ptr = slow_ptr.next; 
    } 

    // Reverse the second  
    // half of the list 
    node root2 = reverseLL(slow_ptr.next); 

    // partition the list 
    slow_ptr.next = null; 

     node current1 = root,  
          current2 = root2; 

    // insert the elements in between 
    while (current1 != null && 
           current2 != null)  
    { 

        // next node to be traversed 
        // in the first list 
        node dnext1 = current1.next; 

        // next node to be traversed 
        // in the first list 
        node dnext2 = current2.next; 
        current1.next = current2; 
        current2.next = dnext1; 
        current1 = dnext1; 
        current2 = dnext2; 
    } 
} 

// Function to insert  
// node after the end 
public static node insertNode(node start,  
                              int val) 
{ 

    // allocate memory 
    node temp = new node(val); 

    // if first node 
    if (start == null) 
        start = temp; 
    else 
    { 

        // move to the end  
        // pointer of node 
         node dstart = start; 
        while (dstart.next != null) 
            dstart = dstart.next; 
        dstart.next = temp; 
    } 

    return start; 
} 

// function to print 
// the linked list 
public static void display(node start) 
{ 
     node temp = start; 

    // traverse till the  
    // entire linked 
    // list is printed 
    while (temp.next != null) { 
        System.out.print(temp.data + "->"); 
        temp = temp.next; 
    } 
    System.out.println(temp.data); 
} 

// Driver Code 
public static void main(String args[]) 
{ 
    // Odd Length Linked List 
    node start = null; 
    start = insertNode(start, 1); 
    start = insertNode(start, 2); 
    start = insertNode(start, 3); 
    start = insertNode(start, 4); 
    start = insertNode(start, 5); 

    System.out.print("Before Modifying: "); 
    display(start); 
    modifyLL(start); 
    System.out.print("After Modifying: "); 
    display(start); 

    // Even Length Linked List 
    start = null; 
    start = insertNode(start, 1); 
    start = insertNode(start, 2); 
    start = insertNode(start, 3); 
    start = insertNode(start, 4); 
    start = insertNode(start, 5); 
    start = insertNode(start, 6); 

    System.out.print("Before Modifying: "); 
    display(start); 
    modifyLL(start); 
    System.out.print("After Modifying: "); 
    display(start); 
} 
} 

```

## C＃

```

// C# program to sandwich the last part  
// of linked list in between the first  
// part of the linked list 
using System; 

public class node  
{  
    public int data;  
    public node next;  
    public node(int key)  
    {  
        data = key;  
        next = null;  
    }  
}  

public class GFG  
{  

// Function to reverse  
// Linked List  
public static node reverseLL(node root)  
{  
    node prev = null,  
    current = root, next;  
    while (current!= null)  
    {  
        next = current.next;  
        current.next = prev;  
        prev = current;  
        current = next;  
    }  

    // root needs to be  
    // upated after reversing  
    root = prev;  
    return root;  
}  

// Function to modify  
// Linked List  
public static void modifyLL( node root)  
{  
    // Find the mid node  
    node slow_ptr = root, fast_ptr = root;  
    while (fast_ptr != null &&  
           fast_ptr.next != null)  
    {  
        fast_ptr = fast_ptr.next.next;  
        slow_ptr = slow_ptr.next;  
    }  

    // Reverse the second  
    // half of the list  
    node root2 = reverseLL(slow_ptr.next);  

    // partition the list  
    slow_ptr.next = null;  

    node current1 = root,  
        current2 = root2;  

    // insert the elements in between  
    while (current1 != null &&  
           current2 != null)  
    {  

        // next node to be traversed  
        // in the first list  
        node dnext1 = current1.next;  

        // next node to be traversed  
        // in the first list  
        node dnext2 = current2.next;  
        current1.next = current2;  
        current2.next = dnext1;  
        current1 = dnext1;  
        current2 = dnext2;  
    }  
}  

// Function to insert  
// node after the end  
public static node insertNode(node start,  
                               int val)  
{  

    // allocate memory  
    node temp = new node(val);  

    // if first node  
    if (start == null)  
        start = temp;  
    else
    {  

        // move to the end  
        // pointer of node  
        node dstart = start;  
        while (dstart.next != null)  
            dstart = dstart.next;  
        dstart.next = temp;  
    }  

    return start;  
}  

// function to print  
// the linked list  
public static void display(node start)  
{  
    node temp = start;  

    // traverse till the  
    // entire linked  
    // list is printed  
    while (temp.next != null)  
    {  
        Console.Write(temp.data + "->");  
        temp = temp.next;  
    }  
    Console.WriteLine(temp.data);  
}  

// Driver Code  
public static void Main(String []args)  
{  
    // Odd Length Linked List  
    node start = null;  
    start = insertNode(start, 1);  
    start = insertNode(start, 2);  
    start = insertNode(start, 3);  
    start = insertNode(start, 4);  
    start = insertNode(start, 5);  

    Console.Write("Before Modifying: ");  
    display(start);  
    modifyLL(start);  
    Console.Write("After Modifying: ");  
    display(start);  

    // Even Length Linked List  
    start = null;  
    start = insertNode(start, 1);  
    start = insertNode(start, 2);  
    start = insertNode(start, 3);  
    start = insertNode(start, 4);  
    start = insertNode(start, 5);  
    start = insertNode(start, 6);  

    Console.Write("Before Modifying: ");  
    display(start);  
    modifyLL(start);  
    Console.Write("After Modifying: ");  
    display(start);  
}  
}  

// This code has been contributed  
// by 29AjayKumar 

```

**Output:**

```
Before Modifying: 1->2->3->4->5
After Modifying: 1->5->2->4->3

Before Modifying: 1->2->3->4->5->6
After Modifying: 1->6->2->5->3->4

```

**时间复杂度：** O（N）

**练习：**解决该问题而无需从中间节点撤消链接列表。

注意读者！ 现在不要停止学习。 通过 [**DSA自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的DSA概念，并为行业做好准备。

* * *

* * *

如果您喜欢GeeksforGeeks并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至tribution@geeksforgeeks.org。 查看您的文章出现在GeeksforGeeks主页上，并帮助其他Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。