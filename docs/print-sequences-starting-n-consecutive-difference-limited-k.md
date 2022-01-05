# 打印所有以 n 开头的序列，连续差值限制为 k

> 原文:[https://www . geesforgeks . org/print-sequence-start-n-continuous-difference-limited-k/](https://www.geeksforgeeks.org/print-sequences-starting-n-consecutive-difference-limited-k/)

给定三个正整数 **n，s** 和 **k** 。任务是打印长度为 s 的所有可能序列，从 n 开始，连续元素之间的绝对差值小于 k。
**示例:**

```
Input : n = 5, s = 3, k = 2
Output :
5 5 5 
5 5 6 
5 5 4 
5 6 6 
5 6 7 
5 6 5 
5 4 4 
5 4 5 
5 4 3 

Input : n = 3, s = 2, k = 1
Output :
3 3 
```

观察，为了得到小于 k 的连续元素之间的绝对差，我们可以从 0 增加到 k–1。同样，我们可以将下一个元素从 1 减少到 k–1。
现在，为了形成所需的序列，我们首先将‘n’推送到向量。然后尝试通过对序列中的每个元素进行递归调用来填充序列的另一个元素。每次递归调用时，我们运行一个从 0 到 k–1 的循环，并将(n + i)添加到序列中。一旦我们制作了大小为 s 的序列，我们将打印整个序列并返回递归调用函数并移除(n + i)。
类似地，我们可以运行从 1 到 k–1 的循环，并插入(n–I)到下一个元素位置。
为了检查所需剩余元素的数量，我们将把 size–1 传递给递归调用，当 size 变为 0 时，我们将打印整个序列。
以下是本办法的实施:

## C++

```
// CPP Program all sequence of length s
// starting with n such that difference
// between consecutive element is less than k.
#include <bits/stdc++.h>
using namespace std;

// Recursive function to print all sequence
// of length s starting with n such that
// difference between consecutive element
// is less than k.
void printSequence(vector<int>& v, int n,
                               int s, int k)
{
    // If size become 0, print the sequence.
    if (s == 0) {
        for (int i = 0; i < v.size(); i++)
            cout << v[i] << " ";
        cout << endl;
        return;
    }

    // Increment the next element and make
    // recursive call after inserting the
    // (n + i) to the sequence.
    for (int i = 0; i < k; i++) {
        v.push_back(n + i);
        printSequence(v, n + i, s - 1, k);
        v.pop_back();
    }

    // Decrementing the next element and'
    // make recursive call after inserting
    // the (n - i) to the sequence.
    for (int i = 1; i < k; i++) {
        v.push_back(n - i);
        printSequence(v, n - i, s - 1, k);
        v.pop_back();
    }
}

// Wrapper Function
void wrapper(int n, int s, int k)
{
    vector<int> v;
    v.push_back(n);
    printSequence(v, n, s - 1, k);
}

// Driven Program
int main()
{
    int n = 5, s = 3, k = 2;
    wrapper(n, s, k);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program all sequence of length s
// starting with n such that difference
// between consecutive element is less than k.
import java.io.*;
import java.util.*;

public class GFG {

    static List<Integer> v = new ArrayList<Integer>();
    // Recursive function to print all sequence
    // of length s starting with n such that
    // difference between consecutive element
    // is less than k.
    static void printSequence(int n,
                                   int s, int k)
    {
        // If size become 0, print the sequence.
        if (s == 0) {
            for (int i = 0; i < v.size(); i++)
                System.out.print(v.get(i) + " ");
            System.out.println();
            return;
        }

        // Increment the next element and make
        // recursive call after inserting the
        // (n + i) to the sequence.
        for (int i = 0; i < k; i++) {
            v.add(n + i);
            printSequence(n + i, s - 1, k);
            v.remove(v.size() - 1);
        }

        // Decrementing the next element and'
        // make recursive call after inserting
        // the (n - i) to the sequence.
        for (int i = 1; i < k; i++) {
            v.add(n - i);
            printSequence(n - i, s - 1, k);
            v.remove(v.size() - 1);
        }
    }

    // Wrapper Function
    static void wrapper(int n, int s, int k)
    {
        v.add(n);
        printSequence(n, s - 1, k);
    }

    // Driven Program
    public static void main(String args[])
    {
        int n = 5, s = 3, k = 2;
        wrapper(n, s, k);
    }
}

// This code is contributed by Manish Shaw
// (manishshaw1)
```

## 蟒蛇 3

```
# Python3 Program all sequence of length s
# starting with n such that difference
# between consecutive element is less than k.

# Recursive function to print all sequence
# of length s starting with n such that
# difference between consecutive element
# is less than k.
def printSequence(v, n, s, k):

    # If size become 0, print the sequence.
    if (s == 0) :
        for i in range(0, len(v)):
            print ("{} ".format(v[i]), end="")
        print ("")
        return;

    # Increment the next element and make
    # recursive call after inserting the
    # (n + i) to the sequence.
    for i in range(0,k):
        v.append(n + i)
        printSequence(v, n + i, s - 1, k)
        v.pop()

    # Decrementing the next element and'
    # make recursive call after inserting
    # the (n - i) to the sequence.
    for i in range(1,k):
        v.append(n - i)
        printSequence(v, n - i, s - 1, k)
        v.pop()

# Wrapper Function
def wrapper(n, s, k):
    v = []
    v.append(n)
    printSequence(v, n, s - 1, k)

# Driven Program
n = 5; s = 3; k = 2;
wrapper(n, s, k);

# This code is contributed by
# Manish Shaw(manishshaw1)
```

## C#

```
// C# Program all sequence of length s
// starting with n such that difference
// between consecutive element is less than k.
using System;
using System.Collections.Generic;
using System.Linq;
using System.Collections;

class GFG {

    // Recursive function to print all sequence
    // of length s starting with n such that
    // difference between consecutive element
    // is less than k.
    static void printSequence(ref List<int> v, int n,
                                   int s, int k)
    {
        // If size become 0, print the sequence.
        if (s == 0) {
            for (int i = 0; i < v.Count; i++)
                Console.Write(v[i] + " ");
            Console.WriteLine();
            return;
        }

        // Increment the next element and make
        // recursive call after inserting the
        // (n + i) to the sequence.
        for (int i = 0; i < k; i++) {
            v.Add(n + i);
            printSequence(ref v, n + i, s - 1, k);
            v.RemoveAt(v.Count - 1);
        }

        // Decrementing the next element and'
        // make recursive call after inserting
        // the (n - i) to the sequence.
        for (int i = 1; i < k; i++) {
            v.Add(n - i);
            printSequence(ref v, n - i, s - 1, k);
            v.RemoveAt(v.Count - 1);
        }
    }

    // Wrapper Function
    static void wrapper(int n, int s, int k)
    {
        List<int> v = new List<int>();
        v.Add(n);
        printSequence(ref v, n, s - 1, k);
    }

    // Driven Program
    public static void Main()
    {
        int n = 5, s = 3, k = 2;
        wrapper(n, s, k);
    }
}

// This code is contributed by Manish Shaw
// (manishshaw1)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP Program all sequence of
// length s starting with n 
// such that difference between
// consecutive element is less than k.

// Recursive function to print
// all sequence of length s
// starting with n such that
// difference between consecutive
// element is less than k.
function printSequence($v, $n,
                       $s, $k)
{
    // If size become 0,
    // print the sequence.
    if ($s == 0)
    {
        for ($i = 0; $i < count($v); $i++)
            echo ($v[$i]." ");
        echo ("\n");
        return;
    }

    // Increment the next element
    // and make recursive call
    // after inserting the (n + i)
    // to the sequence.
    for ($i = 0; $i < $k; $i++)
    {
        array_push($v, $n + $i);
        printSequence($v, $n + $i,
                      $s - 1, $k);
        array_pop($v);
    }

    // Decrementing the next element
    // and make recursive call after 
    // inserting the (n - i) to the
    // sequence.
    for ($i = 1; $i < $k; $i++)
    {
        array_push($v, $n - $i);
        printSequence($v, $n - $i,
                      $s - 1, $k);
        array_pop($v);
    }
}

// Wrapper Function
function wrapper($n, $s, $k)
{
    $v = array();;
    array_push($v, $n);
    printSequence($v, $n, $s - 1, $k);
}

// Driver Code
$n = 5;
$s = 3;
$k = 2;
wrapper($n, $s, $k);

// This code is contributed by
// Manish Shaw(manishshaw1)
?>
```

## java 描述语言

```
<script>

// Javascript Program all sequence of length s
// starting with n such that difference
// between consecutive element is less than k.

v = []

// Recursive function to print all sequence
// of length s starting with n such that
// difference between consecutive element
// is less than k.
function printSequence(n, s, k)
{
    // If size become 0, print the sequence.
    if (s == 0) {
        for (var i = 0; i < v.length; i++)
            document.write( v[i] + " ");
        document.write("<br>");
        return;
    }

    // Increment the next element and make
    // recursive call after inserting the
    // (n + i) to the sequence.
    for (var i = 0; i < k; i++) {
        v.push(n + i);
        printSequence(n + i, s - 1, k);
        v.pop();
    }

    // Decrementing the next element and'
    // make recursive call after inserting
    // the (n - i) to the sequence.
    for (var i = 1; i < k; i++) {
        v.push(n - i);
        printSequence(n - i, s - 1, k);
        v.pop();
    }
}

// Wrapper Function
function wrapper(n, s, k)
{
    v.push(n);
    printSequence( n, s - 1, k);
}

// Driven Program
var n = 5, s = 3, k = 2;
wrapper(n, s, k);

// This code is contributed by itsok.
</script>
```

**输出:**

```
5 5 5 
5 5 6 
5 5 4 
5 6 6 
5 6 7 
5 6 5 
5 4 4 
5 4 5 
5 4 3
```