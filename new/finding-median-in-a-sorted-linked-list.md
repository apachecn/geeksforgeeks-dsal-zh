# 在排序的链接列表中查找中位数

给定![N](img/19e409e13c1238e1f3ff3dbd06cdd45e.png "Rendered by QuickLaTeX.com")元素的排序链表。 任务是在给定的排序链表中找到中位数。

我们知道排序数组中的**中位数**是中间元素。

**查找N个排序数字中位数**的过程：

```
if N is odd:
    median is N/2th element
else
    median is N/2th element + (N/2+1)th element 

```

**示例：**

```
Input : 1->2->3->4->5->NULL
Output : 3

Input : 1->2->3->4->5->6->NULL
Output : 3.5

```

**简单方法**

1.  遍历链接列表并计算所有元素。
2.  如果count是奇数，则再次遍历链接列表并找到第n / 2个元素。
3.  如果count是偶数，则再次遍历链接列表并找到：
    （第n / 2个元素+第（n / 2 + 1）个元素）/ 2

**注意**：上述解决方案两次遍历链表。

**有效方法**：一种有效方法是使用两个指针遍历列表以查找元素数。 [参见此帖子的方法2](https://www.geeksforgeeks.org/write-a-c-function-to-print-the-middle-of-the-linked-list/) 。

我们可以使用上述算法来找到链表的中位数。 使用此算法，我们无需计算元素的数量：

1.  如果 *fast_ptr* 不为NULL，则意味着链表包含奇数元素，我们仅打印 *slow_ptr* 的数据。
2.  否则，如果 *fast_ptr* 达到NULL，则意味着链接列表包含偶数元素，我们创建了 *slow_ptr* 的前一个节点的备份并打印（lower_ptr + slow_ptr- >数据的前一个节点）/ 2

下面是上述方法的实现：

## C ++

```

// C++ program to find median 
// of a linked list 
#include <bits/stdc++.h> 
using namespace std; 

// Link list node 
struct Node { 
    int data; 
    struct Node* next; 
}; 

/* Function to get the median of the linked list */
void printMidean(Node* head) 
{ 
    Node* slow_ptr = head; 
    Node* fast_ptr = head; 
    Node* pre_of_slow = head; 

    if (head != NULL) { 
        while (fast_ptr != NULL && fast_ptr->next != NULL) { 

            fast_ptr = fast_ptr->next->next; 

            // previous of slow_ptr 
            pre_of_slow = slow_ptr; 
            slow_ptr = slow_ptr->next; 
        } 

        // if the below condition is true linked list 
        // contain odd Node 
        // simply return middle element 
        if (fast_ptr != NULL) 
            cout << "Median is : " << slow_ptr->data; 

        // else linked list contain even element 
        else
            cout << "Median is : "
                 << float(slow_ptr->data + pre_of_slow->data) / 2; 
    } 
} 

/* Given a reference (pointer to  
    pointer) to the head of a list  
    and an int, push a new node on  
    the front of the list. */
void push(struct Node** head_ref, int new_data) 
{ 
    // allocate node 
    Node* new_node = new Node; 

    // put in the data 
    new_node->data = new_data; 

    // link the old list 
    // off the new node 
    new_node->next = (*head_ref); 

    // move the head to point 
    // to the new node 
    (*head_ref) = new_node; 
} 

// Driver Code 
int main() 
{ 
    // Start with the 
    // empty list 
    struct Node* head = NULL; 

    // Use push() to construct 
    // below list 
    // 1->2->3->4->5->6 
    push(&head, 6); 
    push(&head, 5); 
    push(&head, 4); 
    push(&head, 3); 
    push(&head, 2); 
    push(&head, 1); 

    // Check the count 
    // function 
    printMidean(head); 

    return 0; 
} 

```

## 爪哇

```

// Java program to find median 
// of a linked list 
class GFG  
{ 

    // Link list node 
    static class Node 
    { 

        int data; 
        Node next; 
    }; 

    /* Function to get the median of the linked list */
    static void printMidean(Node head) 
    { 
        Node slow_ptr = head; 
        Node fast_ptr = head; 
        Node pre_of_slow = head; 

        if (head != null)  
        { 
            while (fast_ptr != null && fast_ptr.next != null)  
            { 

                fast_ptr = fast_ptr.next.next; 

                // previous of slow_ptr 
                pre_of_slow = slow_ptr; 
                slow_ptr = slow_ptr.next; 
            } 

            // if the below condition is true linked list 
            // contain odd Node 
            // simply return middle element 
            if (fast_ptr != null) 
            { 
                System.out.print("Median is : " + slow_ptr.data); 
            } 

            // else linked list contain even element 
            else 
            { 
                System.out.print("Median is : "
                        + (float) (slow_ptr.data + pre_of_slow.data) / 2); 
            } 
        } 
    } 

    /* Given a reference (pointer to  
    pointer) to the head of a list  
    and an int, push a new node on  
    the front of the list. */
    static Node push(Node head_ref, int new_data) 
    { 
        // allocate node 
        Node new_node = new Node(); 

        // put in the data 
        new_node.data = new_data; 

        // link the old list 
        // off the new node 
        new_node.next = head_ref; 

        // move the head to point 
        // to the new node 
        head_ref = new_node; 
        return head_ref; 
    } 

    // Driver Code 
    public static void main(String[] args)  
    { 
        // Start with the 
        // empty list 
        Node head = null; 

        // Use push() to construct 
        // below list 
        // 1.2.3.4.5.6 
        head = push(head, 6); 
        head = push(head, 5); 
        head = push(head, 4); 
        head = push(head, 3); 
        head = push(head, 2); 
        head = push(head, 1); 

        // Check the count 
        // function 
        printMidean(head); 
    } 
} 

// This code is contributed by PrinciRaj1992 

```

## C＃

```

// C# program to find median 
// of a linked list 
using System; 

class GFG  
{ 

    // Link list node 
    class Node 
    { 

        public int data; 
        public Node next; 
    }; 

    /* Function to get the median  
    of the linked list */
    static void printMidean(Node head) 
    { 
        Node slow_ptr = head; 
        Node fast_ptr = head; 
        Node pre_of_slow = head; 

        if (head != null)  
        { 
            while (fast_ptr != null &&  
                   fast_ptr.next != null)  
            { 
                fast_ptr = fast_ptr.next.next; 

                // previous of slow_ptr 
                pre_of_slow = slow_ptr; 
                slow_ptr = slow_ptr.next; 
            } 

            // if the below condition is true linked list 
            // contain odd Node 
            // simply return middle element 
            if (fast_ptr != null) 
            { 
                Console.Write("Median is : " +  
                               slow_ptr.data); 
            } 

            // else linked list contain even element 
            else
            { 
                Console.Write("Median is : " +  
                       (float)(slow_ptr.data +  
                               pre_of_slow.data) / 2); 
            } 
        } 
    } 

    /* Given a reference (pointer to  
    pointer) to the head of a list  
    and an int, push a new node on  
    the front of the list. */
    static Node push(Node head_ref, int new_data) 
    { 
        // allocate node 
        Node new_node = new Node(); 

        // put in the data 
        new_node.data = new_data; 

        // link the old list 
        // off the new node 
        new_node.next = head_ref; 

        // move the head to point 
        // to the new node 
        head_ref = new_node; 
        return head_ref; 
    } 

    // Driver Code 
    public static void Main(String[] args)  
    { 
        // Start with the 
        // empty list 
        Node head = null; 

        // Use push() to construct 
        // below list 
        // 1->2->3->4->5->6 
        head = push(head, 6); 
        head = push(head, 5); 
        head = push(head, 4); 
        head = push(head, 3); 
        head = push(head, 2); 
        head = push(head, 1); 

        // Check the count 
        // function 
        printMidean(head); 
    } 
}  

// This code is contributed by Rajput-Ji 

```

**Output:**

```
Median is : 3.5

```

注意读者！ 现在不要停止学习。 通过 [**DSA自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的DSA概念，并为行业做好准备。

* * *

* * *

如果您喜欢GeeksforGeeks并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至tribution@geeksforgeeks.org。 查看您的文章出现在GeeksforGeeks主页上，并帮助其他Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。