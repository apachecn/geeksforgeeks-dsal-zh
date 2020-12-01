# 链表中的下一个更大元素

> 原文：[https://www.geeksforgeeks.org/next-greater-element-in-the-linked-list/](https://www.geeksforgeeks.org/next-greater-element-in-the-linked-list/)

给定整数的[链表](http://www.geeksforgeeks.org/data-structures/linked-list/)`L`，任务是返回整数的链表，以使其在给定链接的每个元素中都包含[下一个更大的元素](http://www.geeksforgeeks.org/next-greater-element/) 列表。 如果任何元素都没有更大的元素，请为其插入`0`。

**示例**：

> **输入**：`2 -> 1 -> 3 -> 0 -> 5`
>
> **输出**：`3 -> 3 -> 5 -> 5 -> 0`
>
> **输入**：`1 -> 2 -> 3`
>
> **输出**：`2 -> 3  -> 0`

**朴素的方法**：朴素的方法是遍历链表`L`，对于链表中的每个元素，通过遍历当前元素的整个字符串，可以找到列表中的下一个更大的元素 。

**时间复杂度**：`O(N ^ 2)`

**高效方法**：可以通过保持上述朴素的方法来优化 遍历元素的单调递减[栈](http://www.geeksforgeeks.org/stack-data-structure/)。 如果找到更大的元素，则将其附加到结果链表`L`上，否则将`0`附加。 步骤如下：

1.  将第一个节点压入栈。

2.  一个接一个地选取其余节点，然后在循环中执行以下步骤：

    *   将当前节点标记为下一个节点。

    *   如果栈不为空，则将栈的顶部节点值与下一个节点值进行比较。

    *   如果下一个节点的值大于顶部节点的值，则从栈中弹出顶部节点，而下一个是弹出节点的下一个更大的元素。

    *   当弹出的节点值小于下一个节点值时，请继续从栈中弹出节点。 下一个节点将成为所有此类弹出节点的下一个更大元素。

3.  最后，将下一个节点推入栈中。

4.  在**步骤 2** 中的循环结束之后，从栈中弹出所有节点，并打印`0`作为它们的下一个元素。

下面是上述方法的实现：

## C++

```cpp

// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// List Node
struct ListNode {
    int val;
    ListNode* next;
    ListNode(int x)
    {
        val = x;
        next = NULL;
    }
};

// Function to reverse the LL
void rev(ListNode** head)
{
    ListNode *pre, *curr, *nex;

    pre = NULL;
    curr = *head;
    nex = curr->next;

    // Till current is not NULL
    while (curr) {
        curr->next = pre;
        pre = curr;
        curr = nex;
        nex = (curr)
                  ? curr->next
                  : NULL;
    }
    *head = pre;
}

// Function to print a LL node
void printList(ListNode* head)
{
    while (head) {

        cout << head->val
             << ' ';
        head = head->next;
    }
}

// Function to find the next greater
// element in the list
ListNode* nextLargerLL(ListNode* head)
{
    if (head == NULL)
        return NULL;

    // Dummy Node
    ListNode* res
        = new ListNode(-1);
    ListNode* temp = res;

    // Reverse the LL
    rev(&head);
    stack<int> st;

    while (head) {

        // Initial Condition
        if (st.empty()) {
            temp->next
                = new ListNode(0);
            st.push(head->val);
        }
        else {

            // Maintain Monotonicity
            // Decreasing stack of element
            while (!st.empty()
                   && st.top()
                          <= head->val)
                st.pop();

            // Update result LL
            if (st.empty()) {
                temp->next
                    = new ListNode(0);

                st.push(head->val);
            }
            else {
                temp->next
                    = new ListNode(st.top());
                st.push(head->val);
            }
        }
        head = head->next;
        temp = temp->next;
    }

    // Delete Dummy Node
    temp = res;
    res = res->next;
    delete temp;

    // Reverse result LL
    rev(&res);
    return res;
}

// Driver Code
int main()
{
    // Given Linked List
    ListNode* head = new ListNode(2);
    ListNode* curr = head;

    curr->next = new ListNode(1);
    curr = curr->next;

    curr->next = new ListNode(3);
    curr = curr->next;

    curr->next = new ListNode(0);
    curr = curr->next;

    curr->next = new ListNode(5);
    curr = curr->next;

    // Function Call
    printList(nextLargerLL(head));
    return 0;
}

```

## Java

```java

// Java program for the above approach
import java.util.*;
public class linkedList 
{
    ListNode head = null;

    // ListNode
    class ListNode 
    {
        int val;
        ListNode next;

        public ListNode(int val)
        {
            this.val = val;
            next = null;
        }
    }

    // Function to reverse the Linked List
    ListNode reverse(ListNode head)
    {
        ListNode prev = null, next = null, 
                               curr = head;

        while (curr != null) 
        {
            next = curr.next;
            curr.next = prev;
            prev = curr;
            curr = next;
        }
        return prev;
    }

    // Function to find the next greater
    // element in the list
    ListNode nextLargerLL(ListNode head)
    {
        if (head == null)
            return head;

        // Dummy Node
        ListNode res = new ListNode(-1);
        ListNode temp = res;

        // Reverse the Linked List
        head = reverse(head);
        Stack<Integer> st = new Stack<>();

        while (head != null) 
        {

            // Initial Condition
            if (st.empty()) 
            {
                temp.next = new ListNode(0);
                st.push(head.val);
            }
            else {

                // Maintain Monotonicity
                // Decreasing stack of element
                while (!st.empty() && 
                           st.peek() <= head.val)
                    st.pop();

                // Update result Linked List
                if (st.empty()) 
                {
                    temp.next = new ListNode(0);
                    st.push(head.val);
                }
                else
                {
                    temp.next = new ListNode(st.peek());
                    st.push(head.val);
                }
            }
            head = head.next;
            temp = temp.next;
        }
        temp = res;
        res = res.next;

        // Reverse result Linked List
        res = reverse(res);

        return res;
    }

    public void push(int new_data)
    {
        /* allocate node */
        ListNode new_node = new ListNode(new_data);

        /* link the old list off the new node */
        new_node.next = head;

        /* move the head to point to the new node */
        head = new_node;
    }

    // Utility function to print the linked list
    public void printList(ListNode head)
    {
        ListNode temp = head;
        while (temp != null) 
        {
            System.out.print(temp.val + " ");
            temp = temp.next;
        }
    }

    // Driver Code
    public static void main(String[] args)
    {
        linkedList ll = new linkedList();

        ll.push(5);
        ll.push(0);
        ll.push(3);
        ll.push(1);
        ll.push(2);

        // Function Call
        ll.printList(ll.nextLargerLL(ll.head));
    }
}

```

**输出**： 

```
3 3 5 5 0

```

**时间复杂度**：*`O(n)`*；

**辅助空间**：*`O(n)`*



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。