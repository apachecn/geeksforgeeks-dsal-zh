# 仅由数字 0 和 9 组成的给定数字的最小倍数

> 原文:[https://www . geesforgeks . org/给定数字的最小倍数-仅数字 0 和 9/](https://www.geeksforgeeks.org/smallest-multiple-of-a-given-number-made-of-digits-0-and-9-only/)

给我们一个整数 n，我们需要写一个程序来求最小正整数 X，它只由数字 9 和 0 组成，这样，X 就是 n 的倍数

**注**:假设 X 的值不超过 10 <sup>6</sup> 。

**示例:**

```
Input : N = 5
Output : X = 90
Exaplanation: 90 is the smallest number made up 
of 9's and 0's which is divisible by 5.

Input : N = 7
Output : X = 9009
Exaplanation: 9009 is smallest number made up 
of 9's and 0's which is divisible by 7.
```

解决这个问题的想法是生成并存储所有可以用数字 0 和 9 构成的数字。然后在这些生成的数中找出能被 n 整除的最小数
我们将使用生成二进制数的[方法生成所有能用数字 0 & 9 构成的数。](https://www.geeksforgeeks.org/interesting-method-generate-binary-numbers-1-n/)

以下是上述想法的实现:

## C++

```
// CPP program to find smallest multiple of a
// given number made of digits 0 and 9 only
#include <bits/stdc++.h>
using namespace std;

// Maximum number of numbers made of 0 and 9
#define MAX_COUNT 10000

// vector to store all numbers that can be formed
// using digits 0 and 9 and are less than 10^5
vector<string> vec;

/* Preprocessing function to generate all possible
   numbers formed by 0 and 9 */
void generateNumbersUtil()
{  
    // Create an empty queue of strings
    queue<string> q;

    // enqueue the first number
    q.push("9");

    // This loops is like BFS of a tree with 9 as root
    // 0 as left child and 9 as right child and so on
    for (int count = MAX_COUNT; count > 0; count--)
    {
        string s1 = q.front();
        q.pop();

        // storing the front of queue in the vector
        vec.push_back(s1);

        string s2 = s1;

        // Append "0" to s1 and enqueue it
        q.push(s1.append("0"));

        // Append "9" to s2 and enqueue it. Note that
        // s2 contains the previous front
        q.push(s2.append("9"));
    }
}

// function to find smallest number made up of only
// digits 9’s and 0’s, which is a multiple of n.
string findSmallestMultiple(int n)
{  
    // traverse the vector to find the smallest
    // multiple of n
    for (int i = 0; i < vec.size(); i++)

        // stoi() is used for string to int conversion
        if (stoi(vec[i])%n == 0)
            return vec[i];       
}

// Driver Code
int main()
{
    generateNumbersUtil();   
    int n = 7;   
    cout << findSmallestMultiple(n);   
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find smallest
// multiple of a given number
// made of digits 0 and 9 only
import java.util.*;

class GFG
{

    // Maximum number of
    // numbers made of 0 and 9
    static int MAX_COUNT = 10000;

    // vector to store all numbers
    // that can be formed using
    // digits 0 and 9 and are
    // less than 10^5
    static List<String> vec = new LinkedList<String>();

    /* Preprocessing function
    to generate all possible
    numbers formed by 0 and 9 */
    static void generateNumbersUtil()
    {
        // Create an empty
        // queue of Strings
        Queue<String> q = new LinkedList<String>();

        // enqueue the
        // first number
        q.add("9");

        // This loops is like BFS of
        // a tree with 9 as root
        // 0 as left child and 9 as
        // right child and so on
        for (int count = MAX_COUNT;
                count > 0; count--)
        {
            String s1 = q.peek();
            q.remove();

            // storing the Peek of
            // queue in the vector
            vec.add(s1);

            String s2 = s1;

            // Append "0" to s1
            // and enqueue it
            q.add(s1 + "0");

            // Append "9" to s2 and
            // enqueue it. Note that
            // s2 contains the previous Peek
            q.add(s2 + "9");
        }
    }

    // function to find smallest
    // number made up of only
    // digits 9's and 0's, which
    // is a multiple of n.
    static String findSmallestMultiple(int n)
    {
        // traverse the vector
        // to find the smallest
        // multiple of n
        for (int i = 0; i < vec.size(); i++) // stoi() is used for
        // String to int conversion
        {
            if (Integer.parseInt(vec.get(i)) % n == 0)
            {
                return vec.get(i);
            }
        }
        return "";
    }

    // Driver Code
    public static void main(String[] args)
    {
        generateNumbersUtil();
        int n = 7;
        System.out.println(findSmallestMultiple(n));
    }
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 program to find smallest multiple of
# a given number made of digits 0 and 9 only
from queue import Queue

# Preprocessing function to generate
# all possible numbers formed by 0 and 9
def generateNumbersUtil():
    global vec

    # Create an empty queue of strings
    q = Queue()

    # enqueue the first number
    q.put("9")

    # This loops is like BFS of a tree
    # with 9 as root, 0 as left child
    # and 9 as right child and so on
    for count in range(MAX_COUNT, -1, -1):
        s1 = q.queue[0]
        q.get()

        # storing the front of queue
        # in the vector
        vec.append(s1)

        s2 = s1

        # Append "0" to s1 and enqueue it
        s1 += "0"
        q.put(s1)

        # Append "9" to s2 and enqueue it. Note
        # that s2 contains the previous front
        s2 += "9"
        q.put(s2)

# function to find smallest number made
# up of only digits 9’s and 0’s, which
# is a multiple of n.
def findSmallestMultiple(n):
    global vec

    # traverse the vector to find
    # the smallest multiple of n
    for i in range(len(vec)):

        # int is used for string to
        # conversion
        if (int(vec[i]) % n == 0):
            return vec[i]

# Driver Code

# Maximum number of numbers
# made of 0 and 9
MAX_COUNT = 10000

# stack to store all numbers that
# can be formed using digits 0 and
# 9 and are less than 10^5
vec = []
generateNumbersUtil()    
n = 7   
print(findSmallestMultiple(n))

# This code is contributed by PranchalK
```

## C#

```
// C# program to find smallest
// multiple of a given number
// made of digits 0 and 9 only
using System;
using System.Collections.Generic;

class GFG
{
    // Maximum number of
    // numbers made of 0 and 9
    static int MAX_COUNT = 10000;

    // vector to store all numbers
    // that can be formed using
    // digits 0 and 9 and are
    // less than 10^5
    static List<string> vec = new List<string>();

    /* Preprocessing function
    to generate all possible
    numbers formed by 0 and 9 */
    static void generateNumbersUtil()
    {
        // Create an empty
        // queue of strings
        Queue<string> q = new Queue<string>();

        // enqueue the
        // first number
        q.Enqueue("9");

        // This loops is like BFS of
        // a tree with 9 as root
        // 0 as left child and 9 as
        // right child and so on
        for (int count = MAX_COUNT;
                 count > 0; count--)
        {
            string s1 = q.Peek();
            q.Dequeue();

            // storing the Peek of
            // queue in the vector
            vec.Add(s1);

            string s2 = s1;

            // Append "0" to s1
            // and enqueue it
            q.Enqueue(s1 + "0");

            // Append "9" to s2 and
            // enqueue it. Note that
            // s2 contains the previous Peek
            q.Enqueue(s2 + "9");
        }
    }

    // function to find smallest
    // number made up of only
    // digits 9’s and 0’s, which
    // is a multiple of n.
    static string findSmallestMultiple(int n)
    {
        // traverse the vector
        // to find the smallest
        // multiple of n
        for (int i = 0; i < vec.Count; i++)

            // stoi() is used for
            // string to int conversion
            if (int.Parse(vec[i]) % n == 0)
                return vec[i];    
        return "";
    }

    // Driver Code
    static void Main()
    {
        generateNumbersUtil();
        int n = 7;
        Console.Write(findSmallestMultiple(n));
    }
}

// This code is contributed by
// Manish Shaw(manishshaw1)
```

**输出:**

```
9009
```

**时间复杂度** : O(n)