# 一种有趣的从 1 到 n 生成二进制数的方法

> 原文:[https://www . geesforgeks . org/interior-method-generate-binary-numbers-1-n/](https://www.geeksforgeeks.org/interesting-method-generate-binary-numbers-1-n/)

给定一个数字 n，编写一个函数，生成并打印所有二进制数，十进制值从 1 到 n。

**示例:**

```
Input: n = 2
Output: 1, 10

Input: n = 5
Output: 1, 10, 11, 100, 101
```

**天真方法–**

一个简单的方法是运行一个从 1 到 n 的循环，在循环内部调用十进制到二进制。

**高效方法–**

下面是一个有趣的使用[队列数据结构](http://geeksquiz.com/queue-set-1introduction-and-array-implementation/)打印二进制数的方法。感谢[维维克](https://www.geeksforgeeks.org/amazon-interview-set-96-campus-internship/)提出这种方法。

```
1) Create an empty queue of strings 
2) Enqueue the first binary number "1" to queue. 
3) Now run a loop for generating and printing n binary numbers. 
......a) Dequeue and Print the front of queue. 
......b) Append "0" at the end of front item and enqueue it. 
......c) Append "1" at the end of front item and enqueue it.
```

以下是上述算法的实现。

## C++

```
// C++ program to generate binary numbers from 1 to n
#include <bits/stdc++.h>
using namespace std;

// This function uses queue data structure to print binary
// numbers
void generatePrintBinary(int n)
{
    // Create an empty queue of strings
    queue<string> q;

    // Enqueue the first binary number
    q.push("1");

    // This loops is like BFS of a tree with 1 as root
    // 0 as left child and 1 as right child and so on
    while (n--) {
        // print the front of queue
        string s1 = q.front();
        q.pop();
        cout << s1 << "\n";

        string s2 = s1; // Store s1 before changing it

        // Append "0" to s1 and enqueue it
        q.push(s1.append("0"));

        // Append "1" to s2 and enqueue it. Note that s2
        // contains the previous front
        q.push(s2.append("1"));
    }
}

// Driver program to test above function
int main()
{
    int n = 10;
    generatePrintBinary(n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to generate binary numbers from 1 to n

import java.util.LinkedList;
import java.util.Queue;

public class GenerateBNo {
    // This function uses queue data structure to print
    // binary numbers
    static void generatePrintBinary(int n)
    {
        // Create an empty queue of strings
        Queue<String> q = new LinkedList<String>();

        // Enqueue the first binary number
        q.add("1");

        // This loops is like BFS of a tree with 1 as root
        // 0 as left child and 1 as right child and so on
        while (n-- > 0) {
            // print the front of queue
            String s1 = q.peek();
            q.remove();
            System.out.println(s1);

            // Store s1 before changing it
            String s2 = s1;

            // Append "0" to s1 and enqueue it
            q.add(s1 + "0");

            // Append "1" to s2 and enqueue it. Note that s2
            // contains the previous front
            q.add(s2 + "1");
        }
    }

    // Driver program to test above function
    public static void main(String[] args)
    {
        int n = 10;
        generatePrintBinary(n);
    }
}
// This code is contributed by Sumit Ghosh
```

## 计算机编程语言

```
# Python program to generate binary numbers from
# 1 to n

# This function uses queu data structure to print binary numbers

def generatePrintBinary(n):

    # Create an empty queue
    from Queue import Queue
    q = Queue()

    # Enqueu the first binary number
    q.put("1")

    # This loop is like BFS of a tree with 1 as root
    # 0 as left child and 1 as right child and so on
    while(n > 0):
        n -= 1
        # Print the front of queue
        s1 = q.get()
        print s1

        s2 = s1  # Store s1 before changing it

        # Append "0" to s1 and enqueue it
        q.put(s1+"0")

        # Append "1" to s2 and enqueue it. Note that s2
        # contains the previous front
        q.put(s2+"1")

# Driver program to test above function
n = 10
generatePrintBinary(n)

# This code is contributed by Nikhil Kumar Singh(nickzuck_007)
```

## C#

```
// C# program to generate binary
// numbers from 1 to n
using System;
using System.Collections.Generic;

class GFG {
    // This function uses queue data
    // structure to print binary numbers
    public static void generatePrintBinary(int n)
    {
        // Create an empty queue of strings
        LinkedList<string> q = new LinkedList<string>();

        // Enqueue the first binary number
        q.AddLast("1");

        // This loops is like BFS of a tree
        // with 1 as root 0 as left child
        // and 1 as right child and so on
        while (n-- > 0) {
            // print the front of queue
            string s1 = q.First.Value;
            q.RemoveFirst();
            Console.WriteLine(s1);

            // Store s1 before changing it
            string s2 = s1;

            // Append "0" to s1 and enqueue it
            q.AddLast(s1 + "0");

            // Append "1" to s2 and enqueue it.
            // Note that s2 contains the previous front
            q.AddLast(s2 + "1");
        }
    }

    // Driver Code
    public static void Main(string[] args)
    {
        int n = 10;
        generatePrintBinary(n);
    }
}

// This code is contributed by Shrikant13
```

## java 描述语言

```
<script>

// JavaScript program to generate binary numbers from 1 to n

// This function uses queue data structure to print binary
// numbers
function generatePrintBinary(n)
{
    // Create an empty queue of strings
    var q = [];

    // Enqueue the first binary number
    q.push("1");

    // This loops is like BFS of a tree with 1 as root
    // 0 as left child and 1 as right child and so on
    while (n--) {
        // print the front of queue
        var s1 = q[0];
        q.shift();
        document.write( s1 + "<br>");

        var s2 = s1; // Store s1 before changing it

        // Append "0" to s1 and enqueue it
        q.push(s1+"0");

        // Append "1" to s2 and enqueue it. Note that s2
        // contains the previous front
        q.push(s2+"1");
    }
}

// Driver program to test above function
var n = 10;
generatePrintBinary(n);

</script>
```

**Output**

```
1
10
11
100
101
110
111
1000
1001
1010
```

**时间复杂度:** O(n)

本文由 **Abhishek** 供稿。如果您发现任何不正确的地方，或者您想分享更多关于上面讨论的主题的信息，请写评论