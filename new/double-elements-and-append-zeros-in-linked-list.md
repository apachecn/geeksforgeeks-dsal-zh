# 双元素并将零添加到链表

给定一个链表，在零之前有两个相邻的重复节点，任务是将第一个加倍，然后使下一个0。此后，将所有零附加到尾部。

**先决条件：** [单链接列表](https://www.geeksforgeeks.org/data-structures/linked-list/#singlyLinkedList)的实现基础

例子 ：

```
Input : 4 -> 4 -> 0 -> 2 -> 3 -> 4 -> 
        3 -> 3 -> 0 -> 4 -> 
Output : 8-> 2-> 3-> 4-> 6-> 4-> 0-> 
         0-> 0-> 0-> 

Explanation :
First, after doubling the first element and making
second element 0 before all zeros.
8 -> 0 -> 0 -> 2 -> 3 -> 4 -> 6 -> 0 
-> 0 -> 4 ->
Next :
8 -> 6 -> 5 -> 6 -> 0 -> 0 -> 0 -> 
0 -> 0 -> 0 -> 0 -> 

Input : 0 -> 4 -> 4 -> 0 -> 3 -> 3 -> 0 
        -> 5 -> 0 -> 0 -> 6 ->
Output : 8 -> 6 -> 5 -> 6 -> 0 -> 0 -> 0 
         -> 0 -> 0 -> 0 -> 0 ->

```

遍历链接列表，并且在0之前的节点上有两个相邻的相同数据（例如4-> 4-> 0），然后将第一个元素加倍，并将另一个设为0（例如8-> 0-> 0- >）。 最后，遍历链表并将所有零线性指向尾。

## 爪哇

```

// Java code to modify linked list 
import java.util.*; 

// Linked List Node 
class Node 
{ 
    int data; 
    Node next; 

    // Constructor 
    public Node(int data) 
    { 
        this.data = data; 
        next = null; 
    } 
} 

// Class ro perform operations 
// on linked list 
class GfG 
{ 
    // Recursive function to double the one of two 
    // elements and make next one as 0, 
    // which are equal before 0 
    public static void changeTwoBefore0(Node head) 
    { 
        // there should be atleast three elements 
        // to perform required operation 
        if (head == null || head.next == null || 
                         head.next.next == null) 
            return; 

        // when two continuous elements 
        // are same 
        if ((head.data == head.next.data) && 
                (head.next.next.data == 0)) 
        { 

            int temp = head.data; 
            head.data = 2*temp; 
            head.next.data = 0; 

            if (head.next.next.next != null) 
                head = head.next.next.next; 
            else
                return; 
        } 
        else
            head = head.next; 

        // recursive call to changeTwoBefore0 
        // for next element 
        changeTwoBefore0(head); 
    } 

    // function to append zeros at tail 
    public static Node appendZero(Node head) 
    { 
        if (head == null || head.next == null) 
            return head; 

        // Find tail node 
        Node tail = head; 
        while (tail.next != null) 
            tail = tail.next; 
        Node  origTail = tail; 

        // Case when starting nodes have 0 values 
        // we need to change head in this case. 
        Node curr = head; 
        while (curr.next != null && curr.data == 0) 
        { 
            tail.next = curr; 
            tail = curr; 
            curr = curr.next; 
        } 
        head  = curr; 

        // Now moving other 0s to end 
        Node prev = curr; 
        curr = curr.next; 

        // We check until original tail 
        while (curr != origTail) 
        { 
            // If current data is 0, append 
            // after tail and update tail. 
            if (curr.data == 0) 
            { 
                tail.next = curr; 
                tail = curr; 
                prev.next = curr.next; 
            } 
            else
                prev = curr; 

            // We always move current         
            curr = curr.next; 
        } 

        // Finally making sure that linked 
        // list is null terminated. 
        tail.next = null; 

        return head; 
    } 

    public static Node doubleAndAppend0(Node head) 
    { 
        // Change two same nodes before 0 
        changeTwoBefore0(head); 

        // Move all 0s to end 
        return appendZero(head); 
    } 

    // function to display the nodes 
    public static void display(Node head) 
    { 
        while (head != null) 
        { 
            System.out.print(head.data + " -> "); 
            head = head.next; 
        } 
    } 

    // Driver code 
    public static void main(String[] args) 
    { 

        Node head = new Node(4); 
        head.next = new Node(4); 
        head.next.next = new Node(0); 
        head.next.next.next = new Node(2); 
        head.next.next.next.next = new Node(3); 
        head.next.next.next.next.next = new Node(4); 
        head.next.next.next.next.next.next = new Node(3); 
        head.next.next.next.next.next.next.next = new Node(3); 
        head.next.next.next.next.next.next.next.next = new Node(0); 
        head.next.next.next.next.next.next.next.next.next = new Node(4); 

        System.out.println("Original linked list :"); 
        display(head); 

        head = doubleAndAppend0(head); 

        System.out.println("\nModified linked list :"); 
        display(head); 
    } 
} 

```

## Python3

```

# Python3 code to modify linked list 

# Linked List Node 
class Node: 

    # Constructor 
    def __init__(self, data): 

        self.data = data 
        self.next = None

# Recursive function to double the one of two 
# elements and make next one as 0, 
# which are equal before 0 
def changeTwoBefore0 (head): 

    # there should be atleast three elements 
    # to perform required operation 
    if (head == None or head.next == None or head.next.next == None): 
        return

    # when two continuous elements 
    # are same 
    if ((head.data == head.next.data) and (head.next.next.data == 0)): 

        temp = head.data 
        head.data = 2*temp 
        head.next.data = 0

        if (head.next.next.next != None): 
            head = head.next.next.next
        else: 
            return

    else: 
        head = head.next

    # recursive call to changeTwoBefore0 
    # for next element 
    changeTwoBefore0(head) 

# function to append zeros at tail 
def appendZero( head): 

    if (head == None or head.next == None): 
        return head 

    # Find tail node 
    tail = head 
    while (tail.next != None): 
        tail = tail.next
    origTail = tail 

    # Case when starting nodes have 0 values 
    # we need to change head in this case. 
    curr = head 
    while (curr.next != None and curr.data == 0): 

        tail.next = curr 
        tail = curr 
        curr = curr.next

    head = curr 

    # Now moving other 0s to end 
    prev = curr 
    curr = curr.next

    # We check until original tail 
    while (curr != origTail): 

        # If current data is 0, append 
        # after tail and update tail. 
        if (curr.data == 0): 

            tail.next = curr 
            tail = curr 
            prev.next = curr.next

        else: 
            prev = curr 

        # We always move current      
        curr = curr.next

    # Finally making sure that linked 
    # list is None terminated. 
    tail.next = None

    return head 

def doubleAndAppend0(head): 

    # Change two same nodes before 0 
    changeTwoBefore0(head) 

    # Move all 0s to end 
    return appendZero(head) 

# function to display the nodes 
def display( head): 

    while (head != None): 

        print(head.data ,end = " -> ") 
        head = head.next

# Driver code 

head = Node(4) 
head.next = Node(4) 
head.next.next = Node(0) 
head.next.next.next = Node(2) 
head.next.next.next.next = Node(3) 
head.next.next.next.next.next = Node(4) 
head.next.next.next.next.next.next = Node(3) 
head.next.next.next.next.next.next.next = Node(3) 
head.next.next.next.next.next.next.next.next = Node(0) 
head.next.next.next.next.next.next.next.next.next = Node(4) 

print("Original linked list :") 
display(head) 

head = doubleAndAppend0(head) 

print("\nModified linked list :") 
display(head) 

# This code is contributed by Arnab Kundu 

```

## C＃

```

// C# code to modify linked list  
using System; 

// Linked List Node  
public class Node  
{  
    public int data;  
    public Node next;  

    // Constructor  
    public Node(int data)  
    {  
        this.data = data;  
        next = null;  
    }  
}  

// Class ro perform operations  
// on linked list  
public class GfG  
{  
    // Recursive function to double the one of two  
    // elements and make next one as 0,  
    // which are equal before 0  
    public static void changeTwoBefore0(Node head)  
    {  
        // there should be atleast three elements  
        // to perform required operation  
        if (head == null || head.next == null ||  
                        head.next.next == null)  
            return;  

        // when two continuous elements  
        // are same  
        if ((head.data == head.next.data) &&  
                (head.next.next.data == 0))  
        {  

            int temp = head.data;  
            head.data = 2*temp;  
            head.next.data = 0;  

            if (head.next.next.next != null)  
                head = head.next.next.next;  
            else
                return;  
        }  
        else
            head = head.next;  

        // recursive call to changeTwoBefore0  
        // for next element  
        changeTwoBefore0(head);  
    }  

    // function to append zeros at tail  
    public static Node appendZero(Node head)  
    {  
        if (head == null || head.next == null)  
            return head;  

        // Find tail node  
        Node tail = head;  
        while (tail.next != null)  
            tail = tail.next;  
        Node origTail = tail;  

        // Case when starting nodes have 0 values  
        // we need to change head in this case.  
        Node curr = head;  
        while (curr.next != null && curr.data == 0)  
        {  
            tail.next = curr;  
            tail = curr;  
            curr = curr.next;  
        }  
        head = curr;  

        // Now moving other 0s to end  
        Node prev = curr;  
        curr = curr.next;  

        // We check until original tail  
        while (curr != origTail)  
        {  
            // If current data is 0, append  
            // after tail and update tail.  
            if (curr.data == 0)  
            {  
                tail.next = curr;  
                tail = curr;  
                prev.next = curr.next;  
            }  
            else
                prev = curr;  

            // We always move current      
            curr = curr.next;  
        }  

        // Finally making sure that linked  
        // list is null terminated.  
        tail.next = null;  

        return head;  
    }  

    public static Node doubleAndAppend0(Node head)  
    {  
        // Change two same nodes before 0  
        changeTwoBefore0(head);  

        // Move all 0s to end  
        return appendZero(head);  
    }  

    // function to display the nodes  
    public static void display(Node head)  
    {  
        while (head != null)  
        {  
            Console.Write(head.data + " -> ");  
            head = head.next;  
        }  
    }  

    // Driver code  
    public static void Main()  
    {  

        Node head = new Node(4);  
        head.next = new Node(4);  
        head.next.next = new Node(0);  
        head.next.next.next = new Node(2);  
        head.next.next.next.next = new Node(3);  
        head.next.next.next.next.next = new Node(4);  
        head.next.next.next.next.next.next = new Node(3);  
        head.next.next.next.next.next.next.next = new Node(3);  
        head.next.next.next.next.next.next.next.next = new Node(0);  
        head.next.next.next.next.next.next.next.next.next = new Node(4);  

        Console.Write("Original linked list :\n");  
        display(head);  

        head = doubleAndAppend0(head);  

        Console.WriteLine("\nModified linked list :");  
        display(head);  
    }  
}  

/* This code contributed by PrinciRaj1992 */

```

**输出：**

```
Original linked list :
4 -> 4 -> 0 -> 2 -> 3 -> 4 -> 3 -> 3 -> 0 -> 4 -> 
Modified linked list :
8 -> 2 -> 3 -> 4 -> 6 -> 4 -> 0 -> 0 -> 0 -> 0 -> 

```

**时间复杂度：** O（n），其中n是链表的节点数。

注意读者！ 现在不要停止学习。 通过 [**DSA自学课程**](https://practice.geeksforgeeks.org/courses/dsa-self-paced?utm_source=geeksforgeeks&utm_medium=article&utm_campaign=gfg_article_dsa_content_bottom) 以对学生方便的价格掌握所有重要的DSA概念，并为行业做好准备。

* * *

* * *

如果您喜欢GeeksforGeeks并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至tribution@geeksforgeeks.org。 查看您的文章出现在GeeksforGeeks主页上，并帮助其他Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。