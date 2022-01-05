# 检查字符串链表是否形成回文的 Python 程序

> 原文:[https://www . geesforgeks . org/python-program-to-check-if-a-link-list-string-forms-a-回文/](https://www.geeksforgeeks.org/python-program-to-check-if-a-linked-list-of-strings-forms-a-palindrome/)

给定一个处理字符串数据的链表，检查数据是否是回文？
**例:**

```
Input: a -> bc -> d -> dcb -> a -> NULL
Output: True
String "abcddcba" is palindrome.

Input: a -> bc -> d -> ba -> NULL
Output: False
String "abcdba" is not palindrome. 
```

想法很简单。从给定的链表中构造一个字符串，并检查构造的字符串是否是回文。

## 计算机编程语言

```
# Python program to check if given linked list 
# of strings form a palindrome

# Node class 
class Node:

    # Constructor to initialize the 
    # node object
    def __init__(self, data):
        self.data = data
        self.next = None

class LinkedList:

    # Function to initialize head
    def __init__(self):
        self.head = None

    # A utility function to check if str 
    # is palindrome or not
    def isPalindromeUtil(self, string):
        return (string == string[::-1])

    # Returns true if string formed by 
    # linked list is palindrome
    def isPalindrome(self):
        node = self.head

        # Append all nodes to form a string 
        temp = []
        while (node is not None):
            temp.append(node.data)
            node = node.next
        string = "".join(temp)
        return self.isPalindromeUtil(string)

    # Utility function to print the 
    # linked LinkedList
    def printList(self):
        temp = self.head
        while (temp):
            print temp.data,
            temp = temp.next

# Driver code
llist = LinkedList()
llist.head = Node('a')
llist.head.next = Node('bc')
llist.head.next.next = Node("d")
llist.head.next.next.next = Node("dcb")
llist.head.next.next.next.next = Node("a")
print "true" if llist.isPalindrome() else "false"
# This code is contributed by Nikhil Kumar Singh(nickzuck_007)
```

**Output:**

```
true
```

更多详情请参考[查看字符串链表是否形成回文](https://www.geeksforgeeks.org/check-linked-list-strings-form-palindrome/)整篇文章！