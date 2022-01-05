# 将链表分成 3 个部分，使得它们的大小之间的最大差异最小

> 原文:[https://www . geeksforgeeks . org/partition-a-linked-list-in-3-parts-so-size 之间的最大差异最小/](https://www.geeksforgeeks.org/partition-a-linked-list-into-3-parts-such-that-the-maximum-difference-between-their-sizes-is-minimum/)

给定一个[单链表](https://www.geeksforgeeks.org/data-structures/linked-list/singly-linked-list/)，任务是将给定的链表精确地分成三个部分，这样被分割的链表之间的最大长度差最小。

**示例:**

> **输入:**1->2->3->4->5
> **输出:**
> 1->2
> 3->4
> 5
> **说明:**
> 将链表拆分为:
> 
> 1.  **1- > 2:** 大小为 1。
> 2.  **3- > 4:** 大小为 1。
> 3.  **5:** 大小为 1。
> 
> 任何两个分开的链表的最大长度差是 1，这是最小值。
> 
> **输入:** 7 - > 2 - > 1
> **输出:**
> 7
> 2
> 1

**方法:**按照以下步骤解决给定问题:

*   初始化一个[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/)，比如说**ans【】**存储拆分链表
*   如果给定链表的**大小**小于 **3** ，则创建只有一个节点的**大小**时间[链表](https://www.geeksforgeeks.org/data-structures/linked-list/)和有**空**节点的**3–大小**链表，并将其添加到 **ans** 向量中，**返回**。
*   初始化一个变量，将 **minSize** 设为 **size / 3** ，这将是要划分的[链表](https://www.geeksforgeeks.org/data-structures/linked-list/)的最小大小，将 **rem** 设为 **size % 3** 。
*   [迭代链表](https://www.geeksforgeeks.org/iterate-over-a-list-in-python/)直到大小变为 **0** 并执行以下步骤:
    *   在每次迭代中，如果 **rem** 等于 **0** ，那么[再次迭代](https://www.geeksforgeeks.org/iterate-over-a-list-in-python/)次 **minSize** 到链表中，并将该[链表](https://www.geeksforgeeks.org/data-structures/linked-list/)添加到 **ans** 中，并将 **rem** 递减 **1。**
    *   否则，将 **(minSize + 1)** 多次迭代到链表中，并将该链表添加到 **ans** 中。
*   完成以上步骤后，打印矢量**ans【】**中存储的所有链表。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Structure of a Node
class Node {
public:
    int data;
    Node* next;
};

// Function to find the length of
// the Linked List
int sizeOfLL(Node* head)
{
    int size = 0;

    // While head is not null
    while (head != NULL) {
        ++size;
        head = head->next;
    }
    return size;
}

// Function to partition list into
// 3 parts such that maximum size
// difference between parts is minimum
vector<Node*> Partition_of_list(Node* head)
{
    int size = sizeOfLL(head);
    Node* temp = head;
    vector<Node*> ans;

    // If size is less than 3
    if (3 >= size) {
        // Partition linked list
        // into one node each
        while (temp != NULL) {
            Node* next = temp->next;
            temp->next = NULL;
            ans.push_back(temp);
            temp = next;
        }

        // The remaining parts (3-size)
        // will be filled by empty
        // the linked list
        int y = 3 - size;
        while (y != 0) {
            ans.push_back(NULL);
            y--;
        }
    }
    else {
        // Minimum size
        int minSize = size / 3;
        int rem = size % 3;

        // While size is positive
        // and temp is not null
        while (size > 0 && temp != NULL) {
            int m = 0;

            // If remainder > 0, then
            // partition list on the
            // basis of minSize + 1
            if (rem != 0) {
                m = minSize + 1;
                rem--;
            }

            // Otherwise, partition
            // on the basis of minSize
            else {
                m = minSize;
            }
            Node* curr = temp;

            // Iterate for m-1 steps
            // in the list
            for (int j = 1; j < m
                            && temp->next != NULL;
                 j++) {
                temp = temp->next;
            }

            // Change the next of the
            // current node to NULL
            // and add it to the ans
            if (temp->next != NULL) {
                Node* x = temp->next;
                temp->next = NULL;
                temp = x;
                ans.push_back(curr);
            }

            // Otherwise
            else {
                // Pushing to ans
                ans.push_back(curr);
                break;
            }
            size -= m;
        }
    }

    // Return the resultant lists
    return ans;
}

// Function to insert elements in list
void push(Node** head, int d)
{
    Node* temp = new Node();
    temp->data = d;
    temp->next = NULL;

    // If the head is NULL
    if ((*head) == NULL)
        (*head) = temp;

    // Otherwise
    else {
        Node* curr = (*head);

        // While curr->next is not NULL
        while (curr->next != NULL) {
            curr = curr->next;
        }
        curr->next = temp;
    }
}

// Function to display the Linked list
void display(Node* head)
{
    // While head is not null
    while (head->next != NULL) {
        // Print the data
        cout << head->data << "->";
        head = head->next;
    }
    cout << head->data << "\n";
}

// Driver Code
int main()
{
    // Given Input
    Node* head = NULL;
    push(&head, 1);
    push(&head, 2);
    push(&head, 3);
    push(&head, 4);
    push(&head, 5);

    // Function Call
    vector<Node*> v = Partition_of_list(head);

    for (int i = 0; i < v.size(); i++) {
        display(v[i]);
    }
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Structure of a Node
static class Node {

    int data;Node next;
};

    // Function to find the length of
    // the Linked List
static int sizeOfLL(Node head)
{
    int size = 0;

    // While head is not null
    while (head != null) {
        ++size;
        head = head.next;
    }
    return size;
}

// Function to partition list into
// 3 parts such that maximum size
// difference between parts is minimum
static Vector<Node> Partition_of_list(Node head)
{
    int size = sizeOfLL(head);
    Node temp = head;
    Vector<Node> ans = new Vector<>();

    // If size is less than 3
    if (3 >= size) {
        // Partition linked list
        // into one node each
        while (temp != null) {
            Node next = temp.next;
            temp.next = null;
            ans.add(temp);
            temp = next;
        }

        // The remaining parts (3-size)
        // will be filled by empty
        // the linked list
        int y = 3 - size;
        while (y != 0) {
            ans.add(null);
            y--;
        }
    }
    else {
        // Minimum size
        int minSize = size / 3;
        int rem = size % 3;

        // While size is positive
        // and temp is not null
        while (size > 0 && temp != null) {
            int m = 0;

            // If remainder > 0, then
            // partition list on the
            // basis of minSize + 1
            if (rem != 0) {
                m = minSize + 1;
                rem--;
            }

            // Otherwise, partition
            // on the basis of minSize
            else {
                m = minSize;
            }
            Node curr = temp;

            // Iterate for m-1 steps
            // in the list
            for (int j = 1; j < m
                            && temp.next != null;
                 j++) {
                temp = temp.next;
            }

            // Change the next of the
            // current node to null
            // and add it to the ans
            if (temp.next != null) {
                Node x = temp.next;
                temp.next = null;
                temp = x;
                ans.add(curr);
            }

            // Otherwise
            else {
                // Pushing to ans
                ans.add(curr);
                break;
            }
            size -= m;
        }
    }

    // Return the resultant lists
    return ans;
}

    // Function to insert elements in list
static Node push(Node head, int d)
{
    Node temp = new Node();
    temp.data = d;
    temp.next = null;

    // If the head is null
    if ((head) == null)
        (head) = temp;

    // Otherwise
    else {
        Node curr = (head);

        // While curr.next is not null
        while (curr.next != null) {
            curr = curr.next;
        }
        curr.next = temp;
    }
    return head;
}

    // Function to display the Linked list
static void display(Node head)
{
    // While head is not null
    while (head.next != null) {
        // Print the data
        System.out.print(head.data+ "->");
        head = head.next;
    }
    System.out.print(head.data+ "\n");
}

    // Driver Code
public static void main(String[] args)
{
    // Given Input
    Node head = null;
    head = push(head, 1);
    head = push(head, 2);
    head = push(head, 3);
    head = push(head, 4);
    head = push(head, 5);

    // Function Call
    Vector<Node> v = Partition_of_list(head);

    for (int i = 0; i < v.size(); i++) {
        display(v.get(i));
    }
}
}
// This code is contributed by gauravrajput1
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

public class GFG {

    // Structure of a Node
public    class Node {

    public    int data;
    public    Node next;
    };

    // Function to find the length of
    // the Linked List
    static int sizeOfLL(Node head) {
        int size = 0;

        // While head is not null
        while (head != null) {
            ++size;
            head = head.next;
        }
        return size;
    }

    // Function to partition list into
    // 3 parts such that maximum size
    // difference between parts is minimum
    static List<Node> Partition_of_list(Node head) {
        int size = sizeOfLL(head);
        Node temp = head;
        List<Node> ans = new List<Node>();

        // If size is less than 3
        if (3 >= size) {
            // Partition linked list
            // into one node each
            while (temp != null) {
                Node next = temp.next;
                temp.next = null;
                ans.Add(temp);
                temp = next;
            }

            // The remaining parts (3-size)
            // will be filled by empty
            // the linked list
            int y = 3 - size;
            while (y != 0) {
                ans.Add(null);
                y--;
            }
        } else {
            // Minimum size
            int minSize = size / 3;
            int rem = size % 3;

            // While size is positive
            // and temp is not null
            while (size > 0 && temp != null) {
                int m = 0;

                // If remainder > 0, then
                // partition list on the
                // basis of minSize + 1
                if (rem != 0) {
                    m = minSize + 1;
                    rem--;
                }

                // Otherwise, partition
                // on the basis of minSize
                else {
                    m = minSize;
                }
                Node curr = temp;

                // Iterate for m-1 steps
                // in the list
                for (int j = 1; j < m && temp.next != null; j++) {
                    temp = temp.next;
                }

                // Change the next of the
                // current node to null
                // and add it to the ans
                if (temp.next != null) {
                    Node x = temp.next;
                    temp.next = null;
                    temp = x;
                    ans.Add(curr);
                }

                // Otherwise
                else {
                    // Pushing to ans
                    ans.Add(curr);
                    break;
                }
                size -= m;
            }
        }

        // Return the resultant lists
        return ans;
    }

    // Function to insert elements in list
    static Node push(Node head, int d) {
        Node temp = new Node();
        temp.data = d;
        temp.next = null;

        // If the head is null
        if ((head) == null)
            (head) = temp;

        // Otherwise
        else {
            Node curr = (head);

            // While curr.next is not null
            while (curr.next != null) {
                curr = curr.next;
            }
            curr.next = temp;
        }
        return head;
    }

    // Function to display the Linked list
    static void display(Node head) {
        // While head is not null
        while (head.next != null) {
            // Print the data
            Console.Write(head.data + "->");
            head = head.next;
        }
        Console.Write(head.data + "\n");
    }

    // Driver Code
    public static void Main(String[] args)
    {

        // Given Input
        Node head = null;
        head = push(head, 1);
        head = push(head, 2);
        head = push(head, 3);
        head = push(head, 4);
        head = push(head, 5);

        // Function Call
        List<Node> v = Partition_of_list(head);

        for (int i = 0; i < v.Count; i++) {
            display(v[i]);
        }
    }
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>
// javascript program for the above approach

    // Structure of a Node
     class Node {
        constructor() {
            this.data = 0;
            this.next = null;
        }
    }

    // Function to find the length of
    // the Linked List
    function sizeOfLL(head) {
        var size = 0;

        // While head is not null
        while (head != null) {
            ++size;
            head = head.next;
        }
        return size;
    }

    // Function to partition list into
    // 3 parts such that maximum size
    // difference between parts is minimum
     function Partition_of_list(head) {
        var size = sizeOfLL(head);
        var temp = head;
        var ans = [];

        // If size is less than 3
        if (3 >= size) {
            // Partition linked list
            // into one node each
            while (temp != null) {
        var next = temp.next;
                temp.next = null;
                ans.push(temp);
                temp = next;
            }

            // The remaining parts (3-size)
            // will be filled by empty
            // the linked list
            var y = 3 - size;
            while (y != 0) {
                ans.push(null);
                y--;
            }
        } else {
            // Minimum size
            var minSize = parseInt(size / 3);
            var rem = size % 3;

            // While size is positive
            // and temp is not null
            while (size > 0 && temp != null) {
                var m = 0;

                // If remainder > 0, then
                // partition list on the
                // basis of minSize + 1
                if (rem != 0) {
                    m = minSize + 1;
                    rem--;
                }

                // Otherwise, partition
                // on the basis of minSize
                else {
                    m = minSize;
                }
                var curr = temp;

                // Iterate for m-1 steps
                // in the list
                for (var j = 1; j < m && temp.next != null; j++) {
                    temp = temp.next;
                }

                // Change the next of the
                // current node to null
                // and add it to the ans
                if (temp.next != null) {
                    var x = temp.next;
                    temp.next = null;
                    temp = x;
                    ans.push(curr);
                }

                // Otherwise
                else {
                    // Pushing to ans
                    ans.push(curr);
                    break;
                }
                size -= m;
            }
        }

        // Return the resultant lists
        return ans;
    }

    // Function to insert elements in list
    function push(head , d) {
        var temp = new Node();
        temp.data = d;
        temp.next = null;

        // If the head is null
        if ((head) == null)
            (head) = temp;

        // Otherwise
        else {
            var curr = (head);

            // While curr.next is not null
            while (curr.next != null) {
                curr = curr.next;
            }
            curr.next = temp;
        }
        return head;
    }

    // Function to display the Linked list
    function display(head) {
        // While head is not null
        while (head.next != null) {
            // Print the data
            document.write(head.data + "->");
            head = head.next;
        }
        document.write(head.data + "<br/>");
    }

    // Driver Code

        // Given Input
        var head = null;
        head = push(head, 1);
        head = push(head, 2);
        head = push(head, 3);
        head = push(head, 4);
        head = push(head, 5);

        // Function Call
        var v = Partition_of_list(head);

        for (i = 0; i < v.length; i++) {
            display(v[i]);
        }

// This code is contributed by gauravrajput1
</script>
```

**Output:** 

```
1->2
3->4
5
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)