# 检查给定的普鲁弗序列是否有效

> 原文:[https://www . geesforgeks . org/check-if-the-given-prufer-sequence-is-valid-or-not/](https://www.geeksforgeeks.org/check-if-the-given-prufer-sequence-is-valid-or-not/)

给定一个 **N** 整数的[普鲁弗序列](https://www.geeksforgeeks.org/prufer-code-tree-creation/)，任务是检查给定的序列是否是有效的普鲁弗序列。
**例:**

```
Input: arr[] = {4, 1, 3, 4} 
Output: Valid 
The tree is:
2----4----3----1----5
     |
     6                 

Input: arr[] = {4, 1, 7, 4} 
Output: Invalid 
```

**方法:**因为我们知道普鲁弗序列的长度是**N–2**，其中 **N** 是顶点的数量。因此，我们需要检查普鲁弗序列是否由[1，N]范围内的元素组成。
以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if
// given Prufer sequence is valid
bool isValidSeq(int a[], int n)
{
    int nodes = n + 2;

    // Iterate in the Prufer sequence
    for (int i = 0; i < n; i++) {

        // If out of range
        if (a[i] < 1 || a[i] > nodes)
            return false;
    }

    return true;
}

// Driver code
int main()
{
    int a[] = { 4, 1, 3, 4 };
    int n = sizeof(a) / sizeof(a[0]);
    if (isValidSeq(a, n))
        cout << "Valid";
    else
        cout << "Invalid";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG
{

// Function that returns true if
// given Prufer sequence is valid
static boolean isValidSeq(int []a, int n)
{
    int nodes = n + 2;

    // Iterate in the Prufer sequence
    for (int i = 0; i < n; i++)
    {

        // If out of range
        if (a[i] < 1 || a[i] > nodes)
            return false;
    }

    return true;
}

// Driver code
public static void main (String[] args)
{
    int a[] = { 4, 1, 3, 4 };
    int n = a.length;
    if (isValidSeq(a, n))
        System.out.println( "Valid");
    else
        System.out.print( "Invalid");
}
}

// This code is contributed by anuj_67..
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that returns true if
# given Prufer sequence is valid
def isValidSeq(a, n) :

    nodes = n + 2;

    # Iterate in the Prufer sequence
    for i in range(n) :

        # If out of range
        if (a[i] < 1 or a[i] > nodes) :
            return False;

    return True;

# Driver code
if __name__ == "__main__" :

    a = [ 4, 1, 3, 4 ];

    n = len(a);

    if (isValidSeq(a, n)) :
        print("Valid");
    else :
        print("Invalid");

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function that returns true if
// given Prufer sequence is valid
static Boolean isValidSeq(int []a, int n)
{
    int nodes = n + 2;

    // Iterate in the Prufer sequence
    for (int i = 0; i < n; i++)
    {

        // If out of range
        if (a[i] < 1 || a[i] > nodes)
            return false;
    }

    return true;
}

// Driver code
public static void Main (String[] args)
{
    int []a = { 4, 1, 3, 4 };
    int n = a.Length;
    if (isValidSeq(a, n))
        Console.WriteLine( "Valid");
    else
    Console.WriteLine( "Invalid");
}
}

// This code has been contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function that returns true if
// given Prufer sequence is valid
function isValidSeq( a, n)
{
    var nodes = n + 2;

    // Iterate in the Prufer sequence
    for (var i = 0; i < n; i++) {

        // If out of range
        if (a[i] < 1 || a[i] > nodes)
            return false;
    }

    return true;
}

// Driver code
var a = [     4, 1, 3, 4 ];
var n = a.length;
if (isValidSeq(a, n))
    document.write( "Valid" );
else
    document.write( "Invalid");

// This code is contributed by itsok.
</script>
```

**Output:** 

```
Valid
```