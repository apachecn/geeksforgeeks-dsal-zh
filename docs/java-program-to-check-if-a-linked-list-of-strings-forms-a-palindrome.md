# 检查字符串链表是否形成回文的 Java 程序

> 原文:[https://www . geesforgeks . org/Java-program-to-check-if-a-link-list-string-forms-a-回文/](https://www.geeksforgeeks.org/java-program-to-check-if-a-linked-list-of-strings-forms-a-palindrome/)

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

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to check if a given linked list 
// of strings form a palindrome
import java.util.Scanner;

// Linked List node
class Node
{
    String data;
    Node next;

    Node(String d)
    {
        data = d;
        next = null;
    }
}

class LinkedList_Palindrome
{
    Node head;

    // A utility function to check if 
    // str is palindrome or not
    boolean isPalidromeUtil(String str)
    {
        int length = str.length();

        // Match characters from beginning 
        // and end.
        for (int i = 0; i < length / 2; i++)
            if (str.charAt(i) != 
                str.charAt(length - i - 1))
                return false;

        return true;
    }

    // Returns true if string formed by 
    // linked list is palindrome
    boolean isPalindrome()
    {
        Node node = head;

        // Append all nodes to form a 
        // string
        String str = "";
        while (node != null)
        {
            str = str.concat(node.data);
            node = node.next;
        }

        // Check if the formed string is 
        // palindrome
        return isPalidromeUtil(str);
    }

    // Driver code
    public static void main(String[] args)
    {
        LinkedList_Palindrome list = 
           new LinkedList_Palindrome();
        list.head = new Node("a");
        list.head.next = new Node("bc");
        list.head.next.next = new Node("d");
        list.head.next.next.next = 
             new Node("dcb");
        list.head.next.next.next.next = 
             new Node("a");
        System.out.println(list.isPalindrome());
    }
}
// This code is contributed by Amit Khandelwal
```

**Output:**

```
true
```

更多详情请参考[查看字符串链表是否形成回文](https://www.geeksforgeeks.org/check-linked-list-strings-form-palindrome/)整篇文章！