# 按相对顺序打印数组中最后出现的元素

> 原文:[https://www . geeksforgeeks . org/print-相对顺序数组中最后出现的元素/](https://www.geeksforgeeks.org/print-the-last-occurrence-of-elements-in-array-in-relative-order/)

给定一个由 N 个元素组成的数组，按照给定的相对顺序打印元素，删除除最后一次出现的元素之外的所有出现的元素。
**例** :

> **输入:** a[] = {1，5，5，1，6，1}
> **输出:** 5 6 1
> 去掉两个整数 1，在位置 1 和 4。另外，删除整数 5，它位于位置 2。
> 因此左数组为{5，6，1}
> **输入:** a[] = {2，5，5，2}
> **输出:** 5 2

**进场:**

*   散列每个元素的最后一次出现。
*   迭代 N 个元素的数组，如果元素的索引被散列，那么打印数组元素。

以下是上述方法的实现:

## C++

```
// C++ program to print the last occurrence
// of every element in relative order
#include <bits/stdc++.h>
using namespace std;

// Function to print the last occurrence
// of every element in an array
void printLastOccurrence(int a[], int n)
{

    // used in hashing
    unordered_map<int, int> mp;

    // iterate and store the last index
    // of every element
    for (int i = 0; i < n; i++)
        mp[a[i]] = i;

    // iterate and check for the last
    // occurrence of every element
    for (int i = 0; i < n; i++) {
        if (mp[a[i]] == i)
            cout << a[i] << " ";
    }
}
// Driver Code
int main()
{
    int a[] = { 1, 5, 5, 1, 6, 1 };
    int n = sizeof(a) / sizeof(a[0]);
    printLastOccurrence(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print the
// last occurrence of every
// element in relative order
import java.util.*;

class GFG
{

    // Function to print the last
    // occurrence of every element
    // in an array
    public static void printLastOccurrence(int a[],
                                           int n)
    {
        HashMap<Integer,
                Integer> map = new HashMap<Integer,
                                           Integer>();

        // iterate and store the last
        // index of every element
        for (int i = 0; i < n; i++)
            map.put(a[i], i);

        for (int i = 0; i < n; i++)
        {
        if (map.get(a[i]) == i)
            System.out.print(a[i] +" ");
        }
    }

    // Driver Code
    public static void main (String[] args)
    {
        int a[] = { 1, 5, 5, 1, 6, 1 };
        int n = a.length;
        printLastOccurrence(a, n);
    }
}

// This code is contributed
// by ankita_saini
```

## 蟒蛇 3

```
# Python 3 program to print the last occurrence
# of every element in relative order

# Function to print the last occurrence
# of every element in an array
def printLastOccurrence(a, n):

    # used in hashing
    mp = {i:0 for i in range(7)}

    # iterate and store the last
    # index of every element
    for i in range(n):
        mp[a[i]] = i

    # iterate and check for the last
    # occurrence of every element
    for i in range(n):
        if (mp[a[i]] == i):
            print(a[i], end = " ")

# Driver Code
if __name__ == '__main__':
    a = [1, 5, 5, 1, 6, 1]
    n = len(a)
    printLastOccurrence(a, n)

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to print the
// last occurrence of every
// element in relative order
using System;

class GFG
{

// Function to print the last
// occurrence of every element
// in an array
public static void printLastOccurrence(int[] a,
                                       int n)
{
    HashMap<Integer,
            Integer> map = new HashMap<Integer,
                                       Integer>();

    // iterate and store the last
    // index of every element
    for (int i = 0; i < n; i++)
        map.put(a[i], i);

    for (int i = 0; i < n; i++)
    {
    if (map.get(a[i]) == i)
        Console.Write(a[i] + " ");
    }
}

// Driver Code
public static void Main ()
{
    int[] a = { 1, 5, 5, 1, 6, 1 };
    int n = a.Length;
    printLastOccurrence(a, n);
}
}

// This code is contributed
// by ChitraNayal
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print the last
// occurrence of every element
// in relative order

// Function to print the last
// occurrence of every element
// in an array
function printLastOccurrence(&$a, $n)
{

    // used in hashing
    $mp = array();

    // iterate and store the last
    // index of every element
    for ($i = 0; $i < $n; $i++)
        $mp[$a[$i]] = $i;

    // iterate and check for the last
    // occurrence of every element
    for ($i = 0; $i < $n; $i++)
    {
        if ($mp[$a[$i]] == $i)
            echo $a[$i] . " ";
    }
}

// Driver Code
$a = array(1, 5, 5, 1, 6, 1);
$n = sizeof($a);
printLastOccurrence($a, $n);

// This code is contributed
// by ChitraNayal
?>
```

## java 描述语言

```
<script>

// Javascript program to print the last
// occurrence of every element
// in relative order

// Function to print the last
// occurrence of every element
// in an array
function printLastOccurrence(a, n)
{

    // used in hashing
    let mp = [];

    // iterate and store the last
    // index of every element
    for (let i = 0; i < n; i++)
        mp[a[i]] = i;

    // iterate and check for the last
    // occurrence of every element
    for (let i = 0; i < n; i++)
    {
        if (mp[a[i]] == i)
            document.write( a[i] + " ");
    }
}

// Driver Code
let a = [1, 5, 5, 1, 6, 1];
let n = a.length;
printLastOccurrence(a, n);

// This code is contributed by sravan kumar

</script>
```

**输出:**

```
5 6 1
```

**时间复杂度:** O(N * log N)