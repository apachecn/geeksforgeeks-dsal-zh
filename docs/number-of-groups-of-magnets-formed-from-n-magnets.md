# 由 N 个磁体形成的磁体组的数量

> 原文:[https://www . geesforgeks . org/磁体组数-由 n 个磁体形成/](https://www.geeksforgeeks.org/number-of-groups-of-magnets-formed-from-n-magnets/)

给定 N 个磁体，它们一个接一个地排成一行，要么负极在左边，正极在右边(01)，要么正极在左边，负极在右边(10)。考虑到这样一个事实，如果两个连续的磁铁有不同的磁极彼此面对，它们形成一个组并相互吸引，找到可能的组的总数。

**示例**:

```
Input : N = 6
        magnets = {10, 10, 10, 01, 10, 10}
Output : 3
The groups are formed by the following magnets:
1, 2, 3
4
5, 6

Input : N = 5
        magnets = {10, 10, 10, 10, 10, 01}
Output : 1 
```

让我们考虑每对连续的磁铁。有两种可能的情况:

*   两者配置相同。在这种情况下，连接端将具有不同的极点，因此它们将属于同一组。
*   两者都有不同的配置。在这种情况下，连接端将具有相同的极，因此它们将相互排斥以形成不同的组。

因此，只有在两个连续的磁体具有不同配置的情况下，才会形成新的组。遍历磁体阵列，找出具有不同配置的连续对的数量。

下面是上述方法的实现:

## C++

```
// C++ program to find number of groups
// of magnets formed from N magnets

#include <bits/stdc++.h>
using namespace std;

// Function to count number of groups of
// magnets formed from N magnets
int countGroups(int n, string m[])
{
    // Intinially only a single group
    // for the first magnet
    int count = 1;

    for (int i = 1; i < n; i++)

        // Different configuration increases
        // number of groups by 1
        if (m[i] != m[i - 1])
            count++;

    return count;
}

// Driver Code
int main()
{
    int n = 6;

    string m[n] = { "10", "10", "10", "01", "10", "10" };

    cout << countGroups(n, m);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the maximum number
// of elements that can be added to a set
// such that it is the absolute difference // of magnets formed from N magnets

import java.util.*;
import java.lang.*;
import java.io.*;

class GFG{ 

// Function to count number of groups of
// magnets formed from N magnets
static int countGroups(int n, String m[])
{
    // Intinially only a single group
    // for the first magnet
    int count = 1;

    for (int i = 1; i < n; i++)

        // Different configuration increases
        // number of groups by 1
        if (m[i] != m[i - 1])
            count++;

    return count;
}

// Driver Code
public static void main(String args[])
{
    int n = 6;

    String []m = { "10", "10", "10", "01", "10", "10" };

    System.out.println( countGroups(n, m));

}
}
```

## 蟒蛇 3

```
# Python 3 program to find number
# of groups of magnets formed
# from N magnets

# Function to count number of
# groups of magnets formed
# from N magnets
def countGroups(n, m):

    # Intinially only a single
    # group for the first magnet
    count = 1

    for i in range(1, n):

        # Different configuration increases
        # number of groups by 1
        if (m[i] != m[i - 1]):
            count += 1

    return count

# Driver Code
if __name__ == "__main__":

    n = 6

    m = [ "10", "10", "10",
          "01", "10", "10" ]

    print(countGroups(n, m))

# This code is contributed
# by ChitraNayal
```

## C#

```
// C# program to find number of groups
// of magnets formed from N magnets
using System;

class GFG {

    // Function to count number of groups of
    // magnets formed from N magnets
    static int countGroups(int n, String []m)
    {

        // Intinially only a single group
        // for the first magnet
        int count = 1;

        for (int i = 1; i < n; i++)

            // Different configuration increases
            // number of groups by 1
            if (m[i] != m[i - 1])
                count++;

        return count;
}

// Driver Code
public static void Main()
{
    int n = 6;
    String [] m = {"10", "10", "10",
                    "01", "10", "10"};

    Console.WriteLine(countGroups(n, m));
}
}

// This code is contributed by ANKITRAI1
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find number of groups
// of magnets formed from N magnets

// Function to count number of groups
// of magnets formed from N magnets
function countGroups($n, $m)
{
    // Intinially only a single group
    // for the first magnet
    $count = 1;

    for ($i = 1; $i < $n; $i++)

        // Different configuration increases
        // number of groups by 1
        if ($m[$i] != $m[$i - 1])
            $count++;

    return $count;
}

// Driver Code
$n = 6;

$m = array( "10", "10", "10",
            "01", "10", "10" );

echo(countGroups($n, $m));

// This code is contributed
// by Shivi_Aggarwal
?>
```

## java 描述语言

```
<script>
// Javascript program to find the maximum number
// of elements that can be added to a set
// such that it is the absolute difference
// of magnets formed from N magnets

// Function to count number of groups of
// magnets formed from N magnets
function countGroups(n,m) {
    // Intinially only a single group
    // for the first magnet
    let count = 1;

    for (let i = 1; i < n; i++)

        // Different configuration increases
        // number of groups by 1
        if (m[i] != m[i - 1])
            count++;

    return count;
}

    // Driver Code
    let n = 6;
    let m=[ "10", "10", "10", "01", "10", "10"];
    document.write( countGroups(n, m));

// This code is contributed by rag2127
</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(N)