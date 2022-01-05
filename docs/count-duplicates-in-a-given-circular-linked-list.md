# 计算给定循环链表中的重复数

> 原文:[https://www . geesforgeks . org/count-给定循环链表中的重复项/](https://www.geeksforgeeks.org/count-duplicates-in-a-given-circular-linked-list/)

给定一个[循环链表](https://www.geeksforgeeks.org/circular-linked-list/)，任务是检查给定的链表是否有重复。

**示例:**

> **输入:**列表= {5，7，5，1，4，4}
> **输出:** 2
> **说明:**给定列表有 2 个索引，其整数在遍历过程中已经出现在列表中。
> 
> **输入:**列表= {1，1，1，1，1}
> 输出: 4

**方法:**给定的问题有一个非常类似的解决方案[在链表](https://www.geeksforgeeks.org/count-duplicates-in-a-given-linked-list/)中找到重复的计数。想法是使用[哈希](https://www.geeksforgeeks.org/hashing-data-structure/)。使用这里[和](https://www.geeksforgeeks.org/circular-linked-list-set-2-traversal/)讨论的算法遍历给定的循环链表。创建一个 hashmap 来存储列表中出现的整数，对于每个整数，检查该整数是否已经出现。保持变量中已经出现的整数的计数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Class to store Node of the list
class Node {
public:
    int data;
    Node* next;

      Node(int data) {
         this->data = data;
          this->next = NULL;
    }
};

// Function to find the count of the
// duplicate integers in the list
static int checkDuplicate(Node* head)
{
    if (head == NULL)
        return 0;

    // Stores the count of duplicate
    // integers
    int cnt = 0;

    // Stores the integers occurred
    set<int> s;
    s.insert(head->data);
    Node *curr = head->next;

    // Loop to traverse the given list
    while (curr != head) {

        // If integer already occurred
        if (s.find(curr->data) != s.end())
            cnt++;

        // Add current integer into
        // the hashmap
        s.insert(curr->data);
        curr = curr->next;
    }

    // Return answer
    return cnt;
}

// Driver Code
int main()
{

      Node *head = new Node(5);
    head->next = new Node(7);
      head->next->next = new Node(5);
    head->next->next->next = new Node(1);
    head->next->next->next->next = new Node(4);
    head->next->next->next->next->next = new Node(4);
    head->next->next->next->next->next->next = head;

    cout << checkDuplicate(head) << endl;

    return 0;
}

// This code is contributed by Dharanendra L V.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.util.HashSet;

class GFG {

    // Class to store Node of the list
    static class Node {
        int data;
        Node next;

        public Node(int data)
        {
            this.data = data;
        }
    };

    // Stores head pointer of the list
    static Node head;

    // Function to find the count of the
    // duplicate integers in the list
    static int checkDuplicate(Node head)
    {
        if (head == null)
            return 0;

        // Stores the count of duplicate
        // integers
        int cnt = 0;

        // Stores the integers occurred
        HashSet<Integer> s = new HashSet<>();
        s.add(head.data);
        Node curr = head.next;

        // Loop to traverse the given list
        while (curr != head) {

            // If integer already occurred
            if (s.contains(curr.data))
                cnt++;

            // Add current integer into
            // the hashmap
            s.add(curr.data);
            curr = curr.next;
        }

        // Return answer
        return cnt;
    }

    // Driver Code
    public static void main(String[] args)
    {
        head = new Node(5);
        head.next = new Node(7);
        head.next.next = new Node(5);
        head.next.next.next = new Node(1);
        head.next.next.next.next = new Node(4);
        head.next.next.next.next.next = new Node(4);
        head.next.next.next.next.next.next = head;

        System.out.println(checkDuplicate(head));
    }
}
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG {

    // Class to store Node of the list
     class Node {
        public int data;
        public Node next;

        public Node(int data)
        {
            this.data = data;
        }
    };

    // Stores head pointer of the list
    static Node head;

    // Function to find the count of the
    // duplicate integers in the list
    static int checkDuplicate(Node head)
    {
        if (head == null)
            return 0;

        // Stores the count of duplicate
        // integers
        int cnt = 0;

        // Stores the integers occurred
        HashSet<int> s = new HashSet<int>();
        s.Add(head.data);
        Node curr = head.next;

        // Loop to traverse the given list
        while (curr != head) {

            // If integer already occurred
            if (s.Contains(curr.data))
                cnt++;

            // Add current integer into
            // the hashmap
            s.Add(curr.data);
            curr = curr.next;
        }

        // Return answer
        return cnt;
    }

    // Driver Code
    public static void Main()
    {
        head = new Node(5);
        head.next = new Node(7);
        head.next.next = new Node(5);
        head.next.next.next = new Node(1);
        head.next.next.next.next = new Node(4);
        head.next.next.next.next.next = new Node(4);
        head.next.next.next.next.next.next = head;

        Console.Write(checkDuplicate(head));
    }
}

// This code is contributed by ipg2016107.
```

## java 描述语言

```
<script>
// javascript program for the above approach

    // Class to store Node of the list
class Node {
    constructor(val) {
        this.data = val;
        this.next = null;
    }
}

    // Stores head pointer of the list
    var head;

    // Function to find the count of the
    // duplicate integers in the list
    function checkDuplicate(head) {
        if (head == null)
            return 0;

        // Stores the count of duplicate
        // integers
        var cnt = 0;

        // Stores the integers occurred
        var s = new Set();
        s.add(head.data);
var curr = head.next;

        // Loop to traverse the given list
        while (curr != head) {

            // If integer already occurred
            if (s.has(curr.data))
                cnt++;

            // Add current integer into
            // the hashmap
            s.add(curr.data);
            curr = curr.next;
        }

        // Return answer
        return cnt;
    }

    // Driver Code
        head = new Node(5);
        head.next = new Node(7);
        head.next.next = new Node(5);
        head.next.next.next = new Node(1);
        head.next.next.next.next = new Node(4);
        head.next.next.next.next.next = new Node(4);
        head.next.next.next.next.next.next = head;

        document.write(checkDuplicate(head));

// This code is contributed by gauravrajput1
</script>
```

**Output:** 

```
2
```

***时间复杂度:**O(N)*
T5**辅助空间:** O(N)