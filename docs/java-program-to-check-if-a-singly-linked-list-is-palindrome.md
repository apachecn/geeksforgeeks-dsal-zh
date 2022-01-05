# 检查单链表是否回文的 Java 程序

> 原文:[https://www . geesforgeks . org/Java-程序检查单链表是否是回文/](https://www.geeksforgeeks.org/java-program-to-check-if-a-singly-linked-list-is-palindrome/)

给定一个字符的单链表，写一个函数，如果给定的列表是回文，则返回 true，否则返回 false。

![Palindrome Linked List](img/7eef7faffebfb5a692784722f81c0a42.png)

**方法 1(使用堆栈):**

*   一个简单的解决方案是使用列表节点的堆栈。这主要涉及三个步骤。
*   从头到尾遍历给定的列表，并将每个访问过的节点推送到堆栈。
*   再次遍历列表。对于每个访问的节点，从堆栈中弹出一个节点，并将弹出的节点的数据与当前访问的节点进行比较。
*   如果所有节点都匹配，则返回 true，否则返回 false。

下图是上述方法的模拟运行:

![](img/8a3805a79066e7839ba6a0ca7e487a44.png)

下面是上述方法的实现:

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if linked list 
// is palindrome recursively 
import java.util.*;

class linkeList 
{
    public static void main(String args[])
    {
        Node one = new Node(1);
        Node two = new Node(2);
        Node three = new Node(3);
        Node four = new Node(4);
        Node five = new Node(3);
        Node six = new Node(2);
        Node seven = new Node(1);
        one.ptr = two;
        two.ptr = three;
        three.ptr = four;
        four.ptr = five;
        five.ptr = six;
        six.ptr = seven;
        boolean condition = isPalindrome(one);
        System.out.println("isPalidrome :" + condition);
    }
    static boolean isPalindrome(Node head)
    {
        Node slow = head;
        boolean ispalin = true;
        Stack<Integer> stack = new Stack<Integer>();

        while (slow != null) 
        {
            stack.push(slow.data);
            slow = slow.ptr;
        }

        while (head != null) 
        {
            int i = stack.pop();
            if (head.data == i) 
            {
                ispalin = true;
            }
            else 
            {
                ispalin = false;
                break;
            }
            head = head.ptr;
        }
        return ispalin;
    }
}

class Node 
{
    int data;
    Node ptr;
    Node(int d)
    {
        ptr = null;
        data = d;
    }
}
```

**输出:**

```
 isPalindrome: true
```

**时间复杂度:** O(n)。

**方法 2(通过反转列表):**
这个方法需要 O(n)个时间和 O(1)个额外空间。
**1)** 获得链表的中间。
**2)** 反转后半部分链表。
**3)** 检查前半部分和后半部分是否相同。
**4)** 通过再次反转后半部分并将其附着回前半部分来构建原始链表

将列表分成两半，使用[这个](https://www.geeksforgeeks.org/write-a-c-function-to-print-the-middle-of-the-linked-list/)帖子的方法 2。

当节点数为偶数时，第一半和第二半正好包含一半节点。这种方法的挑战是处理节点数为奇数的情况。我们不希望中间节点成为列表的一部分，因为我们要比较它们是否相等。对于奇数情况，我们使用一个单独的变量“中间节点”。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if linked list
// is palindrome 

class LinkedList 
{
    // Head of list
    Node head; 
    Node slow_ptr, 
         fast_ptr, second_half;

    // Linked list Node
    class Node 
    {
        char data;
        Node next;

        Node(char d)
        {
            data = d;
            next = null;
        }
    }

    /* Function to check if given linked list 
       is palindrome or not */
    boolean isPalindrome(Node head)
    {
        slow_ptr = head;
        fast_ptr = head;
        Node prev_of_slow_ptr = head;

        // To handle odd size list
        Node midnode = null;

        // Initialize result 
        boolean res = true; 

        if (head != null && 
            head.next != null) 
        {
            /* Get the middle of the list. 
               Move slow_ptr by 1 and fast_ptrr 
               by 2, slow_ptr will have the middle
               node */
            while (fast_ptr != null &&
                   fast_ptr.next != null) 
            {
                fast_ptr = fast_ptr.next.next;

                /*We need previous of the slow_ptr for
                  linked lists  with odd elements */
                prev_of_slow_ptr = slow_ptr;
                slow_ptr = slow_ptr.next;
            }

            /* fast_ptr would become NULL when there 
               are even elements in the list and not 
               NULL for odd elements. We need to skip  
               the middle node for odd case and store 
               it somewhere so that we can restore the 
               original list */
            if (fast_ptr != null) 
            {
                midnode = slow_ptr;
                slow_ptr = slow_ptr.next;
            }

            // Now reverse the second half and 
            // compare it with first half
            second_half = slow_ptr;

            // NULL terminate first half
            prev_of_slow_ptr.next = null; 

            // Reverse the second half
            reverse(); 

            // compare
            res = compareLists(head, second_half); 

            // Construct the original list back
            // Reverse the second half again
            reverse(); 

            if (midnode != null) 
            {
                // If there was a mid node (odd size case) 
                // which was not part of either first half 
                // or second half.
                prev_of_slow_ptr.next = midnode;
                midnode.next = second_half;
            }
            else
                prev_of_slow_ptr.next = second_half;
        }
        return res;
    }

    /* Function to reverse the linked list 
       Note that this function may change
       the head */
    void reverse()
    {
        Node prev = null;
        Node current = second_half;
        Node next;
        while (current != null) 
        {
            next = current.next;
            current.next = prev;
            prev = current;
            current = next;
        }
        second_half = prev;
    }

    // Function to check if two input 
    // lists have same data
    boolean compareLists(Node head1,
                         Node head2)
    {
        Node temp1 = head1;
        Node temp2 = head2;

        while (temp1 != null && 
               temp2 != null) 
        {
            if (temp1.data == temp2.data)
            {
                temp1 = temp1.next;
                temp2 = temp2.next;
            }
            else
                return false;
        }

        // Both are empty reurn 1
        if (temp1 == null && 
            temp2 == null)
            return true;

        /* Will reach here when one is NULL
           and other is not */
        return false;
    }

    /* Push a node to linked list. Note that 
       this function changes the head */
    public void push(char new_data)
    {
        /* Allocate the Node &
           Put in the data */
        Node new_node = new Node(new_data);

        // Link the old list off the new one 
        new_node.next = head;

        // Move the head to point to new Node 
        head = new_node;
    }

    // A utility function to print a 
    // given linked list
    void printList(Node ptr)
    {
        while (ptr != null) 
        {
            System.out.print(ptr.data + "->");
            ptr = ptr.next;
        }
        System.out.println("NULL");
    }

    // Driver code
    public static void main(String[] args)
    {
        // Start with the empty list 
        LinkedList llist = new LinkedList();

        char str[] = {'a', 'b', 'a', 
                      'c', 'a', 'b', 'a'};
        String string = new String(str);
        for (int i = 0; i < 7; i++) 
        {
            llist.push(str[i]);
            llist.printList(llist.head);
            if (llist.isPalindrome(llist.head) != false) 
            {
                System.out.println("Is Palindrome");
                System.out.println("");
            }
            else 
            {
                System.out.println("Not Palindrome");
                System.out.println("");
            }
        }
    }
}
```

**输出:**

```
a->NULL
Is Palindrome

b->a->NULL
Not Palindrome

a->b->a->NULL
Is Palindrome

c->a->b->a->NULL
Not Palindrome

a->c->a->b->a->NULL
Not Palindrome

b->a->c->a->b->a->NULL
Not Palindrome

a->b->a->c->a->b->a->NULL
Is Palindrome
```

**时间复杂度:**O(n)
T3】辅助空间: O(1)

**方法 3(使用递归):**
使用左右两个指针。使用递归左右移动，并检查每个递归调用中的后续操作。
1)子列表是回文。
2)当前左右值匹配。

如果以上两个条件都成立，那么返回真。

其思想是使用函数调用堆栈作为容器。递归遍历，直到列表结束。当我们从最后一个空值返回时，我们将处于最后一个节点。最后一个节点将与列表的第一个节点进行比较。

为了访问列表的第一个节点，我们需要列表头在递归的最后一次调用中可用。因此，我们也将 head 传递给递归函数。如果它们都匹配，我们需要比较(2，n-2)个节点。同样，当递归回落到(n-2)第二个节点时，我们需要从头部引用第二个节点。我们在前面的调用中推进头指针，以引用列表中的下一个节点。
然而，诀窍在于识别双指针。传递一个指针就像传递一个值一样好，我们会一次又一次地传递同一个指针。我们需要传递头指针的地址，以反映父递归调用的变化。
感谢**沙拉德·钱德拉**提出这个方法。

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
public class LinkedList
{    
    // Head of the list
    Node head; 
    Node left;

    public class Node
    {
        public char data;
        public Node next;

        // Linked list node
        public Node(char d)
        {
            data = d;
            next = null;
        }
    }

    // Initial parameters to this 
    // function are &head and head
    boolean isPalindromeUtil(Node right)
    {
        left = head;

        // Stop recursion when right 
        // becomes null
        if (right == null)
            return true;

        // If sub-list is not palindrome then 
        // no need to check for the current 
        // left and right, return false
        boolean isp = isPalindromeUtil(right.next);
        if (isp == false)
            return false;

        // Check values at current left and right
        boolean isp1 = (right.data == left.data);

        left = left.next;

        // Move left to next node;
        return isp1;
    }

    // A wrapper over isPalindrome(Node head)
    boolean isPalindrome(Node head)
    {
        boolean result = isPalindromeUtil(head);
        return result;
    }

    // Push a node to linked list. 
    // Note that this function changes 
    // the head
    public void push(char new_data)
    {    
        // Allocate the node and put in 
        // the data
        Node new_node = new Node(new_data);

        // Link the old list off the the
        // new one
        new_node.next = head;

        // Move the head to point to 
        // new node
        head = new_node;
    }

    // A utility function to print a 
    // given linked list
    void printList(Node ptr)
    {
        while (ptr != null) 
        {
            System.out.print(ptr.data + "->");
            ptr = ptr.next;
        }
        System.out.println("Null");
    }

    // Driver Code
    public static void main(String[] args)
    {
        LinkedList llist = new LinkedList();
        char[] str = {'a', 'b', 'a', 
                      'c', 'a', 'b', 'a'};
        for(int i = 0; i < 7; i++)
        {
             llist.push(str[i]);
             llist.printList(llist.head);

             if (llist.isPalindrome(llist.head)) 
             {
                 System.out.println("Is Palindrome");
                 System.out.println("");
             }
             else 
             {
                 System.out.println("Not Palindrome");
                 System.out.println("");
             }
        }
    }
}
// This code is contributed by abhinavjain194
```

**输出:**

```
a->NULL
Not Palindrome

b->a->NULL
Not Palindrome

a->b->a->NULL
Is Palindrome

c->a->b->a->NULL
Not Palindrome

a->c->a->b->a->NULL
Not Palindrome

b->a->c->a->b->a->NULL
Not Palindrome

a->b->a->c->a->b->a->NULL
Is Palindrome
```

**时间复杂度:**O(n)
T3】辅助空间: O(n)如果考虑函数调用栈大小，否则为 O(1)。

更多详情请参考[函数整篇文章，查看单链表是否回文](https://www.geeksforgeeks.org/function-to-check-if-a-singly-linked-list-is-palindrome/)！