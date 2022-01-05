# 将链表划分为 K 个大小相差最多 1 的连续组

> 原文:[https://www . geeksforgeeks . org/partition-a-linked-list-in-k-continuous-group-with-size-顶多差-1/](https://www.geeksforgeeks.org/partition-a-linked-list-into-k-continuous-groups-with-difference-in-their-sizes-at-most-1/)

给定一个由 **N** 节点和一个整数 **K** 组成的[链表](https://www.geeksforgeeks.org/data-structures/linked-list/)，任务是[将给定的链表](https://www.geeksforgeeks.org/alternating-split-of-a-given-singly-linked-list/)拆分成 **K** 连续组，这样拆分后相邻组的大小之差最多为**1**，这些组按照其长度降序排列[。](https://www.geeksforgeeks.org/sorting-algorithms/)

***注**:也可以组成一个 0 元素的团。*

**示例:**

> **输入:** 1 → 2 → 3 → 4，K = 5
> **输出:** {{1}、{2}、{3}、{4}、{ }
> **说明:**要求拆分为{{1 - > NULL}、{2 - > NULL}、{3 - > NULL}、{4 - > NULL}、{NULL}}。
> 
> **输入:** LL: 1 → 2 → 3 → 4 → 5 → 6 → 7 → 8，K = 3
> **输出:** {{1，2，3}，{4，5，6}，{7，8}

**方法:**根据观察，首先形成 **N % K** 组尺寸 **(N / K + 1)** 和剩余**K –( N % K)**组尺寸 **N / K** 满足条件，即可解决给定问题。按照以下步骤解决问题:

*   初始化[链表](https://www.geeksforgeeks.org/data-structures/linked-list/)的[向量](https://www.geeksforgeeks.org/sorting-vector-of-pairs-in-c-set-1-sort-by-first-and-second/)，表示**和**，存储 **K** 组。
*   将 **N / K** 和 **N % K** 的值存储在变量中，比如 **L** 和 **R** 。
*   [遍历给定的链表](https://www.geeksforgeeks.org/linked-list-set-1-introduction/)并执行以下步骤:
    *   将 **L** 的值存储在变量中，比如说 **X** ，将 **head** 的值存储在变量中，比如说 **currHead** 和 **last** 。
    *   如果 **R** 的值为正，则将**头**的值更新为**头- >下一个**。
    *   [迭代一个循环，直到 X 非零](https://www.geeksforgeeks.org/range-based-loop-c/)并执行以下步骤:
        *   如果**最后一个节点**与**头节点**相同，则将**头节点**移动到下一个节点。
        *   否则，加入**最后一个节点**和**头节点**之间的链接，将**最后一个**更新为头，并将**头节点**移动到下一个节点。
        *   将当前链表作为向量**和**中的**当前和**推送。
*   如果 **K** 的值大于 **0** ，则推送 **ans** 中的[空链表](https://www.geeksforgeeks.org/linked-list-set-1-introduction/)，并将 **K** 减 1。
*   完成以上步骤后，[打印矢量**ans【】**中存储的所有链表](https://www.geeksforgeeks.org/print-nodes-of-linked-list-at-given-indexes/)的元素。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Link List Node
struct ListNode {
    int val;
    struct ListNode* next;
};

// Function to insert a node
// into the Linked List
void push(ListNode** head_ref,
          int node_val)
{
    // Allocate a new dynamic node
    ListNode* new_node = new ListNode();

    // Update new_node->val
    new_node->val = node_val;

    // Stores the head_ref
    new_node->next = (*head_ref);

    // Update (*head_ref)
    (*head_ref) = new_node;
}

// Function to split the linked list
// in K groups
void splitListInParts(ListNode* head,
                      int K)
{
    // Stores the K groups
    vector<ListNode*> ans;

    // If head is NULL
    if (!head) {

        // Iterate until K is non-zero
        while (K--)
            ans.push_back(NULL);
    }

    // Stores the length of the
    // linked list
    int N = 0;

    // Stores the head node of the
    // linked list
    ListNode* p = head;

    // Iterate over the linked list
    while (p) {

        // Update p
        p = p->next;

        // Update N
        N++;
    }

    int len = N / K;
    int rem = N % K;

    p = head;

    // Iterate over the linked list
    while (K > 0 && p) {

        // Stores the length
        // of the current group
        int x = len;

        // Stores the current node
        ListNode* curr_head = p;

        // Stores the previous node
        ListNode* last = p;

        // If rem is greater than 0
        if (rem > 0) {

            // Update p
            p = p->next;

            // Decrement rem by 1
            rem--;
        }

        // Iterate until x is non-zero
        while (x--) {

            // If the last is equal to p
            if (last == p)
                p = p->next;

            // Otherwise
            else {

                // Join the link between
                // last and the current
                // element
                last->next = p;

                // Update the last node
                last = p;

                // Update p node
                p = p->next;
            }
        }

        // Assign NULL to last->next
        last->next = NULL;

        // Push the current linked
        // list in ans
        ans.push_back(curr_head);

        // Decrement K
        K--;
    }

    // While K greater than 0
    while (K > 0) {

        // Update the value of ans
        ans.push_back(NULL);

        // Increment K
        K--;
    }

    // Print the result
    cout << "{";
    for (int i = 0; i < ans.size(); i++) {
        cout << "{";

        while (ans[i]) {

            // Print the value
            cout << ans[i]->val << "  ";

            // Update ans[i]
            ans[i] = ans[i]->next;
        }
        cout << "}";
        if (i != ans.size() - 1)
            cout << ", ";
    }
    cout << "}";
}

// Driver Code
int main()
{
    ListNode* root = NULL;
    push(&root, 8);
    push(&root, 7);
    push(&root, 6);
    push(&root, 5);
    push(&root, 4);
    push(&root, 3);
    push(&root, 2);
    push(&root, 1);
    int K = 3;

    splitListInParts(root, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Link List Node
static class ListNode
{
    int val;
    ListNode next;
};

// Function to insert a node
// into the Linked List
static ListNode push(ListNode head_ref,
                     int node_val)
{

    // Allocate a new dynamic node
    ListNode new_node = new ListNode();

    // Update new_node.val
    new_node.val = node_val;

    // Stores the head_ref
    new_node.next = head_ref;

    // Update head_ref
    head_ref = new_node;
    return head_ref;
}

// Function to split the linked list
// in K groups
static void splitListInParts(ListNode head,
                             int K)
{

    // Stores the K groups
    Vector<ListNode> ans = new Vector<ListNode>();

    // If head is null
    if (head == null)
    {

        // Iterate until K is non-zero
        while (K-- > 0)
            ans.add(null);
    }

    // Stores the length of the
    // linked list
    int N = 0;

    // Stores the head node of the
    // linked list
    ListNode p = head;

    // Iterate over the linked list
    while (p.next != null)
    {

        // Update p
        p = p.next;

        // Update N
        N++;
    }

    int len = N / K;
    int rem = N % K;

    p = head;

    // Iterate over the linked list
    while (K > 0 && p.next != null)
    {

        // Stores the length
        // of the current group
        int x = len;

        // Stores the current node
        ListNode curr_head = p;

        // Stores the previous node
        ListNode last = p;

        // If rem is greater than 0
        if (rem > 0)
        {

            // Update p
            p = p.next;

            // Decrement rem by 1
            rem--;
        }

        // Iterate until x is non-zero
        while (x-- > 0)
        {

            // If the last is equal to p
            if (last == p)
                p = p.next;

            // Otherwise
            else
            {

                // Join the link between
                // last and the current
                // element
                last.next = p;

                // Update the last node
                last = p;

                // Update p node
                p = p.next;
            }
        }

        // Assign null to last.next
        last.next = null;

        // Push the current linked
        // list in ans
        ans.add(curr_head);

        // Decrement K
        K--;
    }

    // While K greater than 0
    while (K > 0)
    {

        // Update the value of ans
        ans.add(null);

        // Increment K
        K--;
    }

    // Print the result
    System.out.print("{");
    for(int i = 0; i < ans.size(); i++)
    {
        System.out.print("{");

        while (ans.get(i) != null)
        {

            // Print the value
            System.out.print(ans.get(i).val + "  ");

            // Update ans[i]
            ans.set(i, ans.get(i).next);

        }
        System.out.print("}");
        if (i != ans.size() - 1)
            System.out.print(", ");
    }
    System.out.print("}");
}

// Driver Code
public static void main(String[] args)
{
    ListNode root = new ListNode();
    root = push(root, 8);
    root = push(root, 7);
    root = push(root, 6);
    root = push(root, 5);
    root = push(root, 4);
    root = push(root, 3);
    root = push(root, 2);
    root = push(root, 1);
    int K = 3;

    splitListInParts(root, K);
}
}

// This code is contributed by shikhasingrajput
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

public class GFG{

// Link List Node
class ListNode
{
    public int val;
    public ListNode next;
};

// Function to insert a node
// into the Linked List
static ListNode push(ListNode head_ref,
                     int node_val)
{

    // Allocate a new dynamic node
    ListNode new_node = new ListNode();

    // Update new_node.val
    new_node.val = node_val;

    // Stores the head_ref
    new_node.next = head_ref;

    // Update head_ref
    head_ref = new_node;
    return head_ref;
}

// Function to split the linked list
// in K groups
static void splitListInParts(ListNode head,
                             int K)
{

    // Stores the K groups
    List<ListNode> ans = new List<ListNode>();

    // If head is null
    if (head == null)
    {

        // Iterate until K is non-zero
        while (K-- > 0)
            ans.Add(null);
    }

    // Stores the length of the
    // linked list
    int N = 0;

    // Stores the head node of the
    // linked list
    ListNode p = head;

    // Iterate over the linked list
    while (p.next != null)
    {

        // Update p
        p = p.next;

        // Update N
        N++;
    }

    int len = N / K;
    int rem = N % K;

    p = head;

    // Iterate over the linked list
    while (K > 0 && p.next != null)
    {

        // Stores the length
        // of the current group
        int x = len;

        // Stores the current node
        ListNode curr_head = p;

        // Stores the previous node
        ListNode last = p;

        // If rem is greater than 0
        if (rem > 0)
        {

            // Update p
            p = p.next;

            // Decrement rem by 1
            rem--;
        }

        // Iterate until x is non-zero
        while (x-- > 0)
        {

            // If the last is equal to p
            if (last == p)
                p = p.next;

            // Otherwise
            else
            {

                // Join the link between
                // last and the current
                // element
                last.next = p;

                // Update the last node
                last = p;

                // Update p node
                p = p.next;
            }
        }

        // Assign null to last.next
        last.next = null;

        // Push the current linked
        // list in ans
        ans.Add(curr_head);

        // Decrement K
        K--;
    }

    // While K greater than 0
    while (K > 0)
    {

        // Update the value of ans
        ans.Add(null);

        // Increment K
        K--;
    }

    // Print the result
    Console.Write("{");
    for(int i = 0; i < ans.Count; i++)
    {
        Console.Write("{");

        while (ans[i] != null)
        {

            // Print the value
            Console.Write(ans[i].val + "  ");

            // Update ans[i]
            ans[i] = ans[i].next;

        }
        Console.Write("}");
        if (i != ans.Count - 1)
            Console.Write(", ");
    }
    Console.Write("}");
}

// Driver Code
public static void Main(String[] args)
{
    ListNode root = new ListNode();
    root = push(root, 8);
    root = push(root, 7);
    root = push(root, 6);
    root = push(root, 5);
    root = push(root, 4);
    root = push(root, 3);
    root = push(root, 2);
    root = push(root, 1);
    int K = 3;

    splitListInParts(root, K);
}
}

// This code contributed by shikhasingrajput
```

## java 描述语言

```
<script>

// javascript program for the above approach

// Link List Node
class ListNode {

    constructor()
    {
        this.val = 0;
        this.next = null;
    }
};

// Function to insert a node
// into the Linked List
function pushIn(head_ref, node_val)
{
    // Allocate a new dynamic node
    var new_node = new ListNode();

    // Update new_node.val
    new_node.val = node_val;

    // Stores the head_ref
    new_node.next = (head_ref);

    // Update (*head_ref)
    head_ref = new_node;

    return head_ref;
}

// Function to split the linked list
// in K groups
function splitListInParts(head, K)
{
    // Stores the K groups
    var ans = [];

    // If head is null
    if (!head) {

        // Iterate until K is non-zero
        while (K--)
            ans.push(null);
    }

    // Stores the length of the
    // linked list
    var N = 0;

    // Stores the head node of the
    // linked list
    var p = head;

    // Iterate over the linked list
    while (p) {

        // Update p
        p = p.next;

        // Update N
        N++;
    }

    var len = parseInt(N / K);
    var rem = N % K;

    p = head;

    // Iterate over the linked list
    while (K > 0 && p) {

        // Stores the length
        // of the current group
        var x = len;

        // Stores the current node
        var curr_head = p;

        // Stores the previous node
        var last = p;

        // If rem is greater than 0
        if (rem > 0) {

            // Update p
            p = p.next;

            // Decrement rem by 1
            rem--;
        }

        // Iterate until x is non-zero
        while (x--) {

            // If the last is equal to p
            if (last == p)
                p = p.next;

            // Otherwise
            else {

                // Join the link between
                // last and the current
                // element
                last.next = p;

                // Update the last node
                last = p;

                // Update p node
                p = p.next;
            }
        }

        // Assign null to last.next
        last.next = null;

        // Push the current linked
        // list in ans
        ans.push(curr_head);

        // Decrement K
        K--;
    }

    // While K greater than 0
    while (K > 0) {

        // Update the value of ans
        ans.push(null);

        // Increment K
        K--;
    }

    // Print the result
    document.write( "{");
    for (var i = 0; i < ans.length; i++) {
        document.write( "{");

        while (ans[i]) {

            // Print the value
            document.write( ans[i].val + "  ");

            // Update ans[i]
            ans[i] = ans[i].next;
        }
        document.write( "}");
        if (i != ans.length - 1)
            document.write( ", ");
    }
    document.write( "}");
}

// Driver Code
var root = null;
root = pushIn(root, 8);
root = pushIn(root, 7);
root = pushIn(root, 6);
root = pushIn(root, 5);
root = pushIn(root, 4);
root = pushIn(root, 3);
root = pushIn(root, 2);
root = pushIn(root, 1);
var K = 3;
splitListInParts(root, K);

// This code is contributed by rrrtnx.
</script>
```

**Output:** 

```
{{1  2  3  }, {4  5  6  }, {7  8  }}
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)