# 最小索引，其右侧没有 0 或 1

> 原文:[https://www . geesforgeks . org/minist-index-so-to-no-0 或-1-to-it-right/](https://www.geeksforgeeks.org/smallest-index-such-that-there-are-no-0-or-1-to-its-right/)

给定一个由 **N** 个数字组成的二进制数组。任务是找到最小的索引，使得在索引的右边没有 1 或 0。
**注**:数组至少有一个 0 和一个 1。
**例:**

> **输入:** a[] = {1，1，1，0，0，1，0，1}
> **输出:** 6
> 在第 6 个索引处，索引右侧没有 0。
> **输入:** a[] = {0，1，0，0，0}
> **输出:** 1

**逼近**:存储最右边出现的索引 1 和 0，返回两者的最小值。
以下是上述办法的实施情况:

## C++

```
// C++ program to implement
// the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the smallest index
// such that there are no 0 or 1 to its right
int smallestIndex(int a[], int n)
{
    // Initially
    int right1 = 0, right0 = 0;

    // Traverse in the array
    for (int i = 0; i < n; i++) {

        // Check if array element is 1
        if (a[i] == 1)
            right1 = i;

        // a[i] = 0
        else
            right0 = i;
    }

    // Return minimum of both
    return min(right1, right0);
}
// Driver code
int main()
{

    int a[] = { 1, 1, 1, 0, 0, 1, 0, 1, 1 };
    int n = sizeof(a) / sizeof(a[0]);
    cout << smallestIndex(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
class GFG
{

// Function to find the smallest index
// such that there are no 0 or 1 to its right
static int smallestIndex(int []a, int n)
{
    // Initially
    int right1 = 0, right0 = 0;

    // Traverse in the array
    for (int i = 0; i < n; i++)
    {

        // Check if array element is 1
        if (a[i] == 1)
            right1 = i;

        // a[i] = 0
        else
            right0 = i;
    }

    // Return minimum of both
    return Math.min(right1, right0);
}

// Driver code
public static void main(String[] args)
{
    int []a = { 1, 1, 1, 0, 0, 1, 0, 1, 1 };
    int n = a.length;
    System.out.println(smallestIndex(a, n));
}
}

// This code is contributed
// by Code_Mech.
```

## 蟒蛇 3

```
# Python 3 program to implement
# the above approach

# Function to find the smallest
# index such that there are no
# 0 or 1 to its right
def smallestIndex(a, n):

    # Initially
    right1 = 0
    right0 = 0

    # Traverse in the array
    for i in range(n):

        # Check if array element is 1
        if (a[i] == 1):
            right1 = i

        # a[i] = 0
        else:
            right0 = i

    # Return minimum of both
    return min(right1, right0)

# Driver code
if __name__ == '__main__':
    a = [1, 1, 1, 0, 0, 1, 0, 1, 1]
    n = len(a)
    print(smallestIndex(a, n))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to implement
// the above approach
using System;
class GFG
{

// Function to find the smallest index
// such that there are no 0 or 1 to its right
static int smallestIndex(int []a, int n)
{
    // Initially
    int right1 = 0, right0 = 0;

    // Traverse in the array
    for (int i = 0; i < n; i++)
    {

        // Check if array element is 1
        if (a[i] == 1)
            right1 = i;

        // a[i] = 0
        else
            right0 = i;
    }

    // Return minimum of both
    return Math.Min(right1, right0);
}

// Driver code
public static void Main()
{
    int []a = { 1, 1, 1, 0, 0, 1, 0, 1, 1 };
    int n = a.Length;
    Console.Write(smallestIndex(a, n));
}
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to implement
// the above approach

// Function to find the smallest index
// such that there are no 0 or 1 to its right
function smallestIndex($a, $n)
{
    // Initially
    $right1 = 0; $right0 = 0;

    // Traverse in the array
    for ($i = 0; $i < $n; $i++)
    {

        // Check if array element is 1
        if ($a[$i] == 1)
            $right1 = $i;

        // a[i] = 0
        else
            $right0 = $i;
    }

    // Return minimum of both
    return min($right1, $right0);
}

// Driver code
$a = array(1, 1, 1, 0, 0, 1, 0, 1, 1);
$n = sizeof($a);
echo smallestIndex($a, $n);

// This code is contributed by Akanksha Rai
?>
```

## java 描述语言

```
<script>
// Javascript program to implement
// the above approach

    // Function to find the smallest index
    // such that there are no 0 or 1 to its right
    function smallestIndex(a, n)
    {

        // Initially
        let right1 = 0, right0 = 0;

        // Traverse in the array
        let i;
        for (i = 0; i < n; i++)
        {

            // Check if array element is 1
            if (a[i] == 1)
                right1 = i;

            // a[i] = 0
            else
                right0 = i;
        }

        // Return minimum of both
        return Math.min(right1, right0);
    }

    // Driver Code

    var a = [ 1, 1, 1, 0, 0, 1, 0, 1, 1 ];
    let n = a.length;
    document.write(smallestIndex(a, n));

    // This code is contributed by ajaykrsharma132.
</script>
```

**Output:** 

```
6
```

**时间复杂度** : O(N)