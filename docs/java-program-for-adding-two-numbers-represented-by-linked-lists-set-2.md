# 用链表表示的两个数相加的 Java 程序-集合 2

> 原文:[https://www . geesforgeks . org/Java-用于添加两个数字的程序-由链表表示-set-2/](https://www.geeksforgeeks.org/java-program-for-adding-two-numbers-represented-by-linked-lists-set-2/)

给定两个由两个链表表示的数字，编写一个返回求和列表的函数。求和列表是两个输入数字相加的链表表示。不允许修改列表。另外，不允许使用显式的额外空间(提示:使用递归)。

**例**:

```
Input:
First List: 5->6->3  
Second List: 8->4->2 

Output:
Resultant list: 1->4->0->5
```

我们在这里讨论了一个解决方案，它适用于链表，其中最低有效位是链表的第一个节点，最高有效位是最后一个节点。在这个问题中，最重要的节点是第一个节点，最不重要的数字是最后一个节点，我们不允许修改列表。这里使用递归从右向左计算总和。

以下是步骤。

1.  Calculate sizes of given two linked lists.
2.  如果大小相同，则使用递归计算总和。将递归调用堆栈中的所有节点保留到最右边的节点，计算最右边节点的总和，并向左侧结转。
3.  如果大小不一样，则按照以下步骤操作:
    *   计算两个链表的大小差。让差异不同。
    *   在更大的链表中向前移动 *diff* 节点。现在使用步骤 2 计算较小列表和较大列表的右边子列表(大小相同)的总和。另外，存储这个总和的进位。
    *   计算进位(在上一步中计算)与较大列表的剩余左子列表的总和。此总和的节点被添加到上一步获得的总和列表的开头。

以下是上述方法的模拟运行:

![](img/dee4d25298ae9b88a4fb4ed12da5149e.png)

下图是上述方法的实现。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// A Java recursive program to add 
// two linked lists
public class linkedlistATN 
{
    class node 
    {
        int val;
        node next;

        public node(int val) 
        {
            this.val = val;
        }
    }

    // Function to print linked list
    void printlist(node head) 
    {
        while (head != null) 
        {
            System.out.print(
                   head.val + " ");
            head = head.next;
        }
    }

    node head1, head2, result;
    int carry;

    /* A utility function to push a 
       value to linked list */
    void push(int val, int list) 
    {
        node newnode = new node(val);
        if (list == 1) 
        {
            newnode.next = head1;
            head1 = newnode;
        } 
        else if (list == 2) 
        {
            newnode.next = head2;
            head2 = newnode;
        } 
        else 
        {
            newnode.next = result;
            result = newnode;
        }

    }

    // Adds two linked lists of same size 
    // represented by head1 and head2 and 
    // returns head of the resultant linked 
    // list. Carry is propagated while 
    // returning from the recursion
    void addsamesize(node n, node m) 
    {
        // Since the function assumes 
        // linked lists are of same 
        // size, check any of the two
        // head pointers
        if (n == null)
            return;

        // Recursively add remaining nodes 
        // and get the carry
        addsamesize(n.next, m.next);

        // Add digits of current nodes and 
        // propagated carry
        int sum = n.val + m.val + carry;
        carry = sum / 10;
        sum = sum % 10;

        // Push this to result list
        push(sum, 3);
    }

    node cur;

    // This function is called after the 
    // smaller list is added to the bigger 
    // lists's sublist of same size. Once 
    // the right sublist is added, the carry 
    // must be added to the left side of 
    // larger list to get the final result.
    void propogatecarry(node head1) 
    {
        // If diff. number of nodes are 
        // not traversed, add carry
        if (head1 != cur) 
        {
            propogatecarry(head1.next);
            int sum = carry + head1.val;
            carry = sum / 10;
            sum %= 10;

            // Add this node to the front 
            // of the result
            push(sum, 3);
        }
    }

    int getsize(node head) 
    {
        int count = 0;
        while (head != null) 
        {
            count++;
            head = head.next;
        }
        return count;
    }

    // The main function that adds two 
    // linked lists represented by head1 
    // and head2\. The sum of two lists is 
    // stored in a list referred by result
    void addlists() 
    {
        // first list is empty
        if (head1 == null) 
        {
            result = head2;
            return;
        }

        // first list is empty
        if (head2 == null) 
        {
            result = head1;
            return;
        }

        int size1 = getsize(head1);
        int size2 = getsize(head2);

        // Add same size lists
        if (size1 == size2) 
        {
            addsamesize(head1, head2);
        } 
        else 
        {
            // First list should always be 
            // larger than second list. If 
            // not, swap pointers
            if (size1 < size2) 
            {
                node temp = head1;
                head1 = head2;
                head2 = temp;
            }
            int diff = Math.abs(size1 - size2);

            // Move diff. number of nodes in 
            // first list
            node temp = head1;
            while (diff-- >= 0) 
            {
                cur = temp;
                temp = temp.next;
            }

            // Get addition of same size lists
            addsamesize(cur, head2);

            // Get addition of remaining first 
            // list and carry
            propogatecarry(head1);
        }
            // If some carry is still there, add 
            // a new node to the front of the 
            // result list. e.g. 999 and 87
            if (carry > 0)
                push(carry, 3);        
    }

    // Driver code
    public static void main(String args[])
    {
        linkedlistATN list = new linkedlistATN();
        list.head1 = null;
        list.head2 = null;
        list.result = null;
        list.carry = 0;
        int arr1[] = { 9, 9, 9 };
        int arr2[] = { 1, 8 };

        // Create first list as 9->9->9
        for (int i = arr1.length - 1; 
                 i >= 0; --i)
            list.push(arr1[i], 1);

        // Create second list as 1->8
        for (int i = arr2.length - 1; 
                 i >= 0; --i)
            list.push(arr2[i], 2);

        list.addlists();

        list.printlist(list.result);
    }
}
// This code is contributed by Rishabh Mahrsee
```

**输出:**

```
1 0 1 7
```

**时间复杂度:**
O(m+n)，其中 m 和 n 是给定的两个链表的大小。

**迭代方法:**
这个实现没有任何递归调用开销，这意味着它是一个迭代的解决方案。
因为我们需要从两个链表的最后一个开始添加数字。因此，这里我们将使用堆栈数据结构来实现这一点。

*   我们将首先从给定的两个链表中创建两个栈。
*   然后，我们将运行一个循环，直到两个堆栈都变空。
*   在每次迭代中，我们跟踪进位。
*   最后，如果进位> 0，这意味着我们需要在结果列表的开始处有一个额外的节点来容纳这个进位。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Iterative program to add 
// two linked lists  
import java.io.*;
import java.util.*;

class GFG{

static class Node
{
    int data;
    Node next;

    public Node(int data)
    { 
        this.data = data;
    }
}

static Node l1, l2, result;

// To push a new node to linked list
public static void push(int new_data)
{    
    // Allocate node 
    Node new_node = new Node(0);

    // Put in the data 
    new_node.data = new_data;

    // Link the old list off the 
    // new node 
    new_node.next = l1;

    // Move the head to point to the
    // new node 
    l1 = new_node;
}

public static void push1(int new_data)
{    
    // Allocate node 
    Node new_node = new Node(0);

    // Put in the data 
    new_node.data = new_data;

    // Link the old list off the 
    // new node 
    new_node.next = l2;

    // Move the head to point to
    // the new node 
    l2 = new_node;
}

// To add two new numbers
public static Node addTwoNumbers()
{
    Stack<Integer> stack1 = 
                   new Stack<>();
    Stack<Integer> stack2 = 
                   new Stack<>();

    while (l1 != null)
    {
        stack1.add(l1.data);
        l1 = l1.next;
    }

    while (l2 != null) 
    {
        stack2.add(l2.data);
        l2 = l2.next;
    }

    int carry = 0;
    Node result = null;

    while (!stack1.isEmpty() ||
           !stack2.isEmpty()) 
    {
        int a = 0, b = 0;

        if (!stack1.isEmpty()) 
        {
            a = stack1.pop();
        }

        if (!stack2.isEmpty()) 
        {
            b = stack2.pop();
        }

        int total = a + b + carry;

        Node temp = new Node(total % 10);
        carry = total / 10;

        if (result == null) 
        {
            result = temp;
        }
        else
        {
            temp.next = result;
            result = temp;
        }
    }

    if (carry != 0)
    {
        Node temp = new Node(carry);
        temp.next = result;
        result = temp;
    }
    return result;
}

// To print a linked list
public static void printList()
{
    while (result != null) 
    {
        System.out.print(result.data + 
                         " ");
        result = result.next;
    }
    System.out.println();
}

// Driver code
public static void main(String[] args)
{
    int arr1[] = {5, 6, 7};
    int arr2[] = {1, 8};

    int size1 = 3;
    int size2 = 2;

    // Create first list as 5->6->7
    int i;
    for(i = size1 - 1; 
        i >= 0; --i)
        push(arr1[i]);

    // Create second list as 1->8
    for(i = size2 - 1; 
        i >= 0; --i)
        push1(arr2[i]);

    result = addTwoNumbers();

    printList();
}
}
// This code is contributed by RohitOberoi
```

**输出:**

```
5 8 5
```

相关文章:[添加两个链表表示的数字|集合 1](https://www.geeksforgeeks.org/add-two-numbers-represented-by-linked-lists/)
详情请参考[添加两个链表表示的数字|集合 2](https://www.geeksforgeeks.org/sum-of-two-linked-lists/) 完整文章！