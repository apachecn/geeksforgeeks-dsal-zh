# 使用递归将给定的数字与链表中存储的数字相加

> 原文：[https://www.geeksforgeeks.org/add-the-given-digit-to-a-number-stored-in-a-linked-list-using-recursion/](https://www.geeksforgeeks.org/add-the-given-digit-to-a-number-stored-in-a-linked-list-using-recursion/)

<<<<<<< HEAD
给定一个表示整数的链表，其中每个节点是所表示整数的数字。 任务是将给定的数字 **N** 添加到表示的整数。
=======
将给定的数字添加到链表中存储的数字中

给定一个表示整数的链表，其中每个节点是所表示整数的数字。 任务是将给定的数字`N`添加到表示的整数。
>>>>>>> 67ea03ac9ece65f623a6b1a9a1311be605210497

**示例**：

> **输入**：`LL = 9 -> 9 -> 3 -> NULL, N = 7`
>
> **输出**：`1 -> 0 -> 0 -> 0 -> NULL`
>
> `993 + 7 = 1000`
> 
> **输入**：`LL = 2 -> 9 -> 9 -> NULL, N = 5`
>
> **输出**：`3 -> 0 -> 4 -> NULL`

**方法**：在此中讨论了解决此问题的迭代方法。 在本文中，将讨论一种递归方法。

这个想法是递归地遍历链表，直到到达最后一个节点。 到达最后一个节点后，向其添加`N`的值。 添加后，如果该值大于 9，则将进位和设置模式（数字`% 10`）值保留为节点值，并将进位添加到先前的栈帧节点，并继续直到从栈中清除所有栈帧为止。

如果在清除所有栈帧之后仍然有一个进位，则使用此值创建一个新节点，该节点将是链表的新头，指向前一个头。

下面是上述方法的实现：

## Java

```java

// Java implementation of the approach 

// Node class contains value 
// and next node reference 
class ListNode { 
    int value; 
    ListNode next; 
} 

class GFG { 

    // To store the carry 
    private static int carry = 0; 

    // Function that calls the recursive method 
    // addNewValue to add a digit to the 
    // number represented as the linked list 
    public static ListNode addValue(ListNode head, int addValue) 
    { 

        // Add the digit recursively 
        addNewValue(head, addValue); 

        // If there is a carry after the addition 
        if (carry != 0) { 

            // Create a new node 
            ListNode newHead = new ListNode(); 

            // Assign it with carry 
            newHead.value = carry; 

            // Make it point to the head of 
            // the linked list 
            newHead.next = head; 
            carry = 0; 

            // Make it the new head 
            return newHead; 
        } 

        // If there's not carry then 
        // return the previous head 
        else { 
            return head; 
        } 
    } 

    // Recursive function to add a digit to the number 
    // represented as the given linked list 
    private static void addNewValue(ListNode head, int addValue) 
    { 

        // If it is the last node in the list 
        if (head.next == null) { 

            // Add the digit 
            int val = head.value + addValue; 

            // Find the carry if any 
            head.value = val % 10; 
            carry = val / 10; 
        } 
        else { 

            // Preserve the current node's value and call 
            // the recursive function for the next node 
            int val = head.value; 
            addNewValue(head.next, addValue); 
            val = val + carry; 
            head.value = val % 10; 
            carry = val / 10; 
        } 
    } 

    // Utility function to print the linked list 
    private static void printList(ListNode node) 
    { 
        while (node != null) { 
            System.out.print(node.value + " -> "); 
            node = node.next; 
        } 
        System.out.print("NULL"); 
    } 

    // Driver code 
    public static void main(String[] args) 
    { 

        // Create the linked list 9 -> 9 -> 3 -> NULL 
        ListNode head = new ListNode(); 
        head.value = 9; 
        head.next = new ListNode(); 
        head.next.value = 9; 
        head.next.next = new ListNode(); 
        head.next.next.value = 3; 
        head.next.next.next = null; 

        // Digit to be added 
        int n = 7; 
        head = addValue(head, n); 

        printList(head); 
    } 
} 

```

## Python

```py

# Python implementation of the approach 

# Node class contains value 
# and next node reference 
class ListNode:  
    def __init__(self, new_data):  
        self.value = new_data  
        self.next = None

# To store the carry 
carry = 0

# Function that calls the recursive method 
# addNewValue to add a digit to the 
# number represented as the linked list 
def addValue(head, addValue): 

    global carry 

    # Add the digit recursively 
    addNewValue(head, addValue) 

    # If there is a carry after the addition 
    if (carry != 0) : 

        # Create a node 
        newHead = ListNode(0) 

        # Assign it with carry 
        newHead.value = carry 

        # Make it point to the head of 
        # the linked list 
        newHead.next = head 
        carry = 0

        # Make it the head 
        return newHead 

    # If there's not carry then 
    # return the previous head 
    else : 
        return head 

# Recursive function to add a digit to the number 
# represented as the given linked list 
def addNewValue(head,addValue): 

    global carry 

    # If it is the last node in the list 
    if (head.next == None) : 

        # Add the digit 
        val = head.value + addValue 

        # Find the carry if any 
        head.value = val % 10
        carry = int(val / 10) 

    else : 

        # Preserve the current node's value and call 
        # the recursive function for the next node 
        val = head.value 
        addNewValue(head.next, addValue) 
        val = val + carry 
        head.value = val % 10
        carry = int(val / 10) 

# Utility function to print the linked list 
def printList(node): 

    while (node != None) : 
        print(node.value ,end= " -> ") 
        node = node.next

    print("None") 

# Driver code 

# Create the linked list 9 -> 9 -> 3 -> None 
head = ListNode(0) 
head.value = 9
head.next = ListNode(0) 
head.next.value = 9
head.next.next = ListNode(0) 
head.next.next.value = 3
head.next.next.next = None

# Digit to be added 
n = 7
head = addValue(head, n) 

printList(head) 

# This code is contributed by Arnab Kundu 

```

## C#

```cs

// C# implementation of the approach  
using System; 

// Node class contains value 
// and next node reference 
public class ListNode  
{ 
    public int value; 
    public ListNode next; 
} 

class GFG 
{ 

    // To store the carry 
    private static int carry = 0; 

    // Function that calls the recursive method 
    // addNewValue to add a digit to the 
    // number represented as the linked list 
    public static ListNode addValue(ListNode head,  
                                     int addValue) 
    { 

        // Add the digit recursively 
        addNewValue(head, addValue); 

        // If there is a carry after the addition 
        if (carry != 0)  
        { 

            // Create a new node 
            ListNode newHead = new ListNode(); 

            // Assign it with carry 
            newHead.value = carry; 

            // Make it point to the head of 
            // the linked list 
            newHead.next = head; 
            carry = 0; 

            // Make it the new head 
            return newHead; 
        } 

        // If there's not carry then 
        // return the previous head 
        else
        { 
            return head; 
        } 
    } 

    // Recursive function to add a digit to the number 
    // represented as the given linked list 
    private static void addNewValue(ListNode head,  
                                     int addValue) 
    { 

        // If it is the last node in the list 
        if (head.next == null) 
        { 

            // Add the digit 
            int val = head.value + addValue; 

            // Find the carry if any 
            head.value = val % 10; 
            carry = val / 10; 
        } 
        else 
        { 

            // Preserve the current node's value and call 
            // the recursive function for the next node 
            int val = head.value; 
            addNewValue(head.next, addValue); 
            val = val + carry; 
            head.value = val % 10; 
            carry = val / 10; 
        } 
    } 

    // Utility function to print the linked list 
    private static void printList(ListNode node) 
    { 
        while (node != null)  
        { 
            Console.Write(node.value + " -> "); 
            node = node.next; 
        } 
        Console.Write("NULL"); 
    } 

    // Driver code 
    public static void Main(String[] args) 
    { 

        // Create the linked list 9 -> 9 -> 3 -> NULL 
        ListNode head = new ListNode(); 
        head.value = 9; 
        head.next = new ListNode(); 
        head.next.value = 9; 
        head.next.next = new ListNode(); 
        head.next.next.value = 3; 
        head.next.next.next = null; 

        // Digit to be added 
        int n = 7; 
        head = addValue(head, n); 

        printList(head); 
    } 
} 

// This code is contributed by PrinciRaj1992 

```

**输出**：

```
1 -> 0 -> 0 -> 0 -> NULL

```



* * *

* * *

如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](https://contribute.geeksforgeeks.org/) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果您发现任何不正确的地方，请单击下面的“改进文章”按钮，以改进本文。