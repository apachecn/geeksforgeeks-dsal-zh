# 检查单链表是否回文的 Python 程序

> 原文:[https://www . geesforgeks . org/python-程序检查单链表是否是回文/](https://www.geeksforgeeks.org/python-program-to-check-if-a-singly-linked-list-is-palindrome/)

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

## 蟒蛇 3

```
# Python3 program to check if linked
# list is palindrome using stack
class Node:
    def __init__(self, data):        
        self.data = data
        self.ptr = None

# Function to check if the linked list
# is palindrome or not
def ispalindrome(head):

    # Temp pointer
    slow = head

    # Declare a stack
    stack = []

    ispalin = True

    # Push all elements of the list
    # to the stack
    while slow != None:
        stack.append(slow.data)

        # Move ahead
        slow = slow.ptr

    # Iterate in the list again and
    # check by popping from the stack
    while head != None:

        # Get the top most element
        i = stack.pop()

        # Check if data is not
        # same as popped element
        if head.data == i:
            ispalin = True
        else:
            ispalin = False
            break

        # Move ahead
        head = head.ptr

    return ispalin

# Driver Code

# Addition of linked list
one = Node(1)
two = Node(2)
three = Node(3)
four = Node(4)
five = Node(3)
six = Node(2)
seven = Node(1)

# Initialize the next pointer
# of every current pointer
one.ptr = two
two.ptr = three
three.ptr = four
four.ptr = five
five.ptr = six
six.ptr = seven
seven.ptr = None

# Call function to check 
# palindrome or not
result = ispalindrome(one)

print("isPalindrome:", result)

# This code is contributed by Nishtha Goel
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

## 蟒蛇 3

```
# Python program to check if
# linked list is palindrome

# Node class
class Node:

    # Constructor to initialize
    # the node object
    def __init__(self, data):        
        self.data = data
        self.next = None

class LinkedList:

    # Function to initialize head
    def __init__(self):        
        self.head = None

    # Function to check if given
    # linked list is pallindrome or not
    def isPalindrome(self, head):        
        slow_ptr = head
        fast_ptr = head
        prev_of_slow_ptr = head

        # To handle odd size list
        midnode = None

        # Initialize result
        res = True  

        if (head != None and 
            head.next != None):

            # Get the middle of the list. 
            # Move slow_ptr by 1 and 
            # fast_ptrr by 2, slow_ptr 
            # will have the middle node
            while (fast_ptr != None and 
                   fast_ptr.next != None):

                # We need previous of the slow_ptr 
                # for linked lists  with odd 
                # elements
                fast_ptr = fast_ptr.next.next
                prev_of_slow_ptr = slow_ptr
                slow_ptr = slow_ptr.next

            # fast_ptr would become NULL when 
            # there are even elements in the 
            # list and not NULL for odd elements. 
            # We need to skip the middle node for 
            # odd case and store it somewhere so 
            # that we can restore the original list
            if (fast_ptr != None):
                midnode = slow_ptr
                slow_ptr = slow_ptr.next

            # Now reverse the second half 
            # and compare it with the first half
            second_half = slow_ptr

            # NULL terminate first half
            prev_of_slow_ptr.next = None 

            # Reverse the second half
            second_half = self.reverse(second_half) 

            # Compare
            res = self.compareLists(head, second_half)  

            # Construct the original list back
            # Reverse the second half again
            second_half = self.reverse(second_half)

            if (midnode != None):

                # If there was a mid node (odd size
                # case) which was not part of either
                # first half or second half.
                prev_of_slow_ptr.next = midnode
                midnode.next = second_half
            else:
                prev_of_slow_ptr.next = second_half
        return res

    # Function to reverse the linked list 
    # Note that this function may change 
    # the head
    def reverse(self, second_half):

        prev = None
        current = second_half
        next = None

        while current != None:
            next = current.next
            current.next = prev
            prev = current
            current = next

        second_half = prev
        return second_half

    # Function to check if two input 
    # lists have same data
    def compareLists(self, head1, head2):

        temp1 = head1
        temp2 = head2

        while (temp1 and temp2):
            if (temp1.data == temp2.data):
                temp1 = temp1.next
                temp2 = temp2.next
            else:
                return 0

        # Both are empty return 1
        if (temp1 == None and temp2 == None):
            return 1

        # Will reach here when one is NULL
        # and other is not
        return 0

    # Function to insert a new node
    # at the beginning
    def push(self, new_data):

        # Allocate the Node &
        # Put in the data
        new_node = Node(new_data)

        # Link the old list off the new one
        new_node.next = self.head

        # Move the head to point to the 
        # new Node
        self.head = new_node

    # A utility function to print
    # a given linked list 
    def printList(self):

        temp = self.head

        while(temp):
            print(temp.data, end = "->")
            temp = temp.next

        print("NULL")

# Driver code
if __name__ == '__main__':    
    l = LinkedList()
    s = ['a', 'b', 'a', 
         'c', 'a', 'b', 'a']

    for i in range(7):
        l.push(s[i])
        l.printList()

        if (l.isPalindrome(l.head) != False):
            print("Is Palindrome")
        else:
            print("Not Palindrome")
        print()

# This code is contributed by MuskanKalra1 
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

更多详情请参考[函数整篇文章，查看单链表是否回文](https://www.geeksforgeeks.org/function-to-check-if-a-singly-linked-list-is-palindrome/)！