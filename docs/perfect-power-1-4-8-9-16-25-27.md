# 完美幂(1，4，8，9，16，25，27，…)

> 原文:[https://www . geesforgeks . org/perfect-power-1-4-8-9-16-25-27/](https://www.geeksforgeeks.org/perfect-power-1-4-8-9-16-25-27/)

A [完美幂](https://en.wikipedia.org/wiki/Perfect_power)是可以用另一个正整数的幂来表示的数。
给定一个数字 n，找出从 1 到 n 的 x <sup>y</sup> 类型的数字的个数，其中 x > = 1，y > 1
**示例:**

```
Input : n = 10
Output : 4
1 4 8 and 9 are the numbers that are
of form x ^ y where x > 0 and y > 1

Input : n = 50
Output : 10
```

一个简单的解决方案是通过从 i = 2 到 n 的平方根的所有幂的数字

## C++

```
// CPP program to count number of numbers from
// 1 to n are of type x^y where x>0 and y>1
#include <bits/stdc++.h>
using namespace std;

// For our convenience
#define ll long long

// Function that keeps all the odd power
// numbers upto n
int powerNumbers(int n)
{
    // v is going to store all power numbers
    vector<int> v;
    v.push_back(1);

    // Traverse through all base numbers and
    // compute all their powers smaller than
    // or equal to n.
    for (ll i = 2; i * i <= n; i++) {
        ll j = i * i;
        v.push_back(j);
        while (j * i <= n) {
            v.push_back(j * i);
            j = j * i;
        }
    }

    // Remove all duplicates
    sort(v.begin(), v.end());
    v.erase(unique(v.begin(), v.end()), v.end());

    return v.size();
}

int main()
{
    cout << powerNumbers(50);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to count number of numbers from
// 1 to n are of type x^y where x>0 and y>1
import java.io.*;
import java.util.*;

public class GFG {

    // Function that keeps all the odd power
    // numbers upto n
    static int powerNumbers(int n)
    {
        // v is going to store all unique
        // power numbers
        HashSet<Integer> v = new HashSet<Integer>();
        v.add(1);

        // Traverse through all base numbers
        // and compute all their powers
        // smaller than or equal to n.
        for (int i = 2; i * i <= n; i++) {
            int j = i * i;
            v.add(j);
            while (j * i <= n) {
                v.add(j * i);
                j = j * i;
            }
        }
        return v.size();
    }

    // Driver code
    public static void main(String args[])
    {
        System.out.print(powerNumbers(50));
    }
}

// This code is contributed by Manish Shaw
// (manishshaw1)
```

## 蟒蛇 3

```
# Python3 program to count number
# of numbers from 1 to n are of
# type x^y where x>0 and y>1

# Function that keeps all the odd
# power numbers upto n
def powerNumbers(n):

    # v is going to store all
    # unique power numbers
    v = set();
    v.add(1);

    # Traverse through all base
    # numbers and compute all
    # their powers smaller than
    # or equal to n.
    for i in range(2, n+1):
        if(i * i <= n):
            j = i * i;
            v.add(j);
            while (j * i <= n):
                v.add(j * i);
                j = j * i;

    return len(v);

print (powerNumbers(50));
# This code is contributed by
# Manish Shaw (manishshaw1)
```

## C#

```
// C# program to count number of numbers from
// 1 to n are of type x^y where x>0 and y>1
using System;
using System.Collections.Generic;
using System.Linq;

class GFG {

    // Function that keeps all the odd power
    // numbers upto n
    static int powerNumbers(int n)
    {
        // v is going to store all unique
        // power numbers
        HashSet<int> v = new HashSet<int>();
        v.Add(1);

        // Traverse through all base numbers
        // and compute all their powers
        // smaller than or equal to n.
        for (int i = 2; i * i <= n; i++) {
            int j = i * i;
            v.Add(j);
            while (j * i <= n) {
                v.Add(j * i);
                j = j * i;
            }
        }
        return v.Count;
    }

    // Driver code
    public static void Main()
    {
        Console.WriteLine(powerNumbers(50));
    }
}

// This code is contributed by Manish Shaw
// (manishshaw1)
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to count number of
// numbers from 1 to n are of type
// x^y where x>0 and y>1

// Function that keeps all the
// odd power numbers upto n
function powerNumbers($n)
{
    // v is going to store
    // all power numbers
    $v = array();
    array_push($v, 1);

    // Traverse through all base
    // numbers and compute all
    // their powers smaller than
    // or equal to n.
    for ($i = 2; $i * $i <= $n; $i++)
    {
        $j = $i * $i;
        array_push($v, $j);
        while ($j * $i <= $n)
        {
            array_push($v, $j * $i);
            $j = $j * $i;
        }
    }

    // Remove all duplicates
    sort($v);
    $v = array_unique($v);

    return count($v);
}

// Driver Code
echo (powerNumbers(50));

// This code is contributed by
// Manish Shaw(manishshaw1)
?>
```

## java 描述语言

```
<script>

    // JavaScript program to count number of numbers from
    // 1 to n are of type x^y where x>0 and y>1

    // Function that keeps all the odd power
    // numbers upto n
    function powerNumbers(n)
    {
        // v is going to store all unique
        // power numbers
        let v = new Set();
        v.add(1);

        // Traverse through all base numbers
        // and compute all their powers
        // smaller than or equal to n.
        for (let i = 2; i * i <= n; i++) {
            let j = i * i;
            v.add(j);
            while (j * i <= n) {
                v.add(j * i);
                j = j * i;
            }
        }
        return v.size;
    }

    document.write(powerNumbers(50));

</script>
```

**Output:** 

```
10
```