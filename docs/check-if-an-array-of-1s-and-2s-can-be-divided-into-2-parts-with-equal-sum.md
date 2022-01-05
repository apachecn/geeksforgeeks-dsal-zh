# 检查 1 和 2 的数组是否可以等和分成 2 部分

> 原文:[https://www . geesforgeks . org/check-如果一个 1 和 2 的数组可以被等和分成 2 部分/](https://www.geeksforgeeks.org/check-if-an-array-of-1s-and-2s-can-be-divided-into-2-parts-with-equal-sum/)

给定一个包含 **N** 个元素的数组，每个元素要么是 1，要么是 2。任务是找出数组是否可以分成两部分，使得两部分的元素之和相等。
**例:**

```
Input : N = 3, arr[] = {1, 1, 2}
Output : YES

Input : N = 4, arr[] = {1, 2, 2, }
Output : NO
```

其思想是观察到只有当数组的总和为偶数，即可被 2 整除时，数组才能被分成两个和相等的部分。
假设数组的总和用**和**表示。
现在，出现了两种情况:

*   **如果 sum/2 为偶数**:当 sum/2 的值也为偶数时，意味着两部分的每一部分的和也为偶数，我们不需要考虑什么特别的。所以，这个案子还真有。
*   **如果和/2 为奇数**:当和/2 的值为奇数时，表示各部分之和也为奇数。只有当数组的两个部分都包含至少一个 1 时，这才是可能的。考虑 sum = 2 或 6 或 10 的情况。因此，当 sum/2 为奇数时，检查数组中是否至少有一个 1。

以下是上述方法的实现:

## C++

```
// C++ implementation of the above
// approach:

#include <bits/stdc++.h>
using namespace std;

// Function to check if it is possible to
// split the array in two parts with
// equal sum
bool isSpiltPossible(int n, int a[])
{
    int sum = 0, c1 = 0;

    // Calculate sum of elements
    // and count of 1's
    for (int i = 0; i < n; i++) {
        sum += a[i];

        if (a[i] == 1) {
            c1++;
        }
    }

    // If total sum is odd, return False
    if (sum % 2)
        return false;

    // If sum of each part is even,
    // return True
    if ((sum / 2) % 2 == 0)
        return true;

    // If sum of each part is even but
    // there is atleast one 1
    if (c1 > 0)
        return true;
    else
        return false;
}

// Driver Code
int main()
{
    int n = 3;
    int a[] = { 1, 1, 2 };

    if (isSpiltPossible(n, a))
        cout << "YES";
    else
        cout << "NO";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above
// approach:
class GFG
{

// Function to check if it is possible
// to split the array in two parts with
// equal sum
static boolean isSpiltPossible(int n,
                               int a[])
{
    int sum = 0, c1 = 0;

    // Calculate sum of elements
    // and count of 1's
    for (int i = 0; i < n; i++)
    {
        sum += a[i];

        if (a[i] == 1)
        {
            c1++;
        }
    }

    // If total sum is odd, return False
    if(sum % 2 != 0)
        return false;

    // If sum of each part is even,
    // return True
    if ((sum / 2) % 2 == 0)
        return true;

    // If sum of each part is even but
    // there is atleast one 1
    if (c1 > 0)
        return true;
    else
        return false;
}

// Driver Code
public static void main(String[] args)
{
    int n = 3;
    int a[] = { 1, 1, 2 };

    if (isSpiltPossible(n, a))
        System.out.println("YES");
    else
        System.out.println("NO");
}
}

// This code is contributed by
// Code Mech
```

## 蟒蛇 3

```
# Python3 implementation of the above
# approach:

# Function to check if it is possible
# to split the array in two halfs with
# equal Sum
def isSpiltPossible(n, a):

    Sum = 0
    c1 = 0

    # Calculate Sum of elements
    # and count of 1's
    for i in range(n):
        Sum += a[i]

        if (a[i] == 1):
            c1 += 1

    # If total Sum is odd, return False
    if (Sum % 2):
        return False

    # If Sum of each half is even,
    # return True
    if ((Sum // 2) % 2 == 0):
        return True

    # If Sum of each half is even
    # but there is atleast one 1
    if (c1 > 0):
        return True
    else:
        return False

# Driver Code
n = 3
a = [ 1, 1, 2 ]

if (isSpiltPossible(n, a)):
    print("YES")
else:
    print("NO")

# This code is contributed
# by Mohit Kumar
```

## C#

```
// C# implementation of the above
// approach:
using System;

class GFG
{

// Function to check if it is possible
// to split the array in two parts with
// equal sum
static bool isSpiltPossible(int n,
                            int[] a)
{
    int sum = 0, c1 = 0;

    // Calculate sum of elements
    // and count of 1's
    for (int i = 0; i < n; i++)
    {
        sum += a[i];

        if (a[i] == 1)
        {
            c1++;
        }
    }

    // If total sum is odd, return False
    if(sum % 2 != 0)
        return false;

    // If sum of each part is even,
    // return True
    if ((sum / 2) % 2 == 0)
        return true;

    // If sum of each part is even but
    // there is atleast one 1
    if (c1 > 0)
        return true;
    else
        return false;
}

// Driver Code
public static void Main()
{
    int n = 3;
    int[] a = { 1, 1, 2 };

    if (isSpiltPossible(n, a))
        Console.WriteLine("YES");
    else
        Console.WriteLine("NO");
}
}

// This code is contributed by
// Code Mech
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the above
// approach:

// Function to check if it is possible
// to split the array in two parts with
// equal sum
function isSpiltPossible($n, $a)
{
    $sum = 0; $c1 = 0;

    // Calculate sum of elements
    // and count of 1's
    for ($i = 0; $i < $n; $i++)
    {
        $sum += $a[$i];

        if ($a[$i] == 1)
        {
            $c1++;
        }
    }

    // If total sum is odd, return False
    if($sum % 2 != 0)
        return false;

    // If sum of each part is even,
    // return True
    if (($sum / 2) % 2 == 0)
        return true;

    // If sum of each part is even but
    // there is atleast one 1
    if ($c1 > 0)
        return true;
    else
        return false;
}

// Driver Code
$n = 3;
$a = array( 1, 1, 2 );

if (isSpiltPossible($n, $a))
    echo("YES");
else
    echo("NO");

// This code is contributed by
// Code Mech
?>
```

## java 描述语言

```
<script>

// Javascript implementation of the above approach

// Function to check if it is possible
// to split the array in two parts with
// equal sum
function isSpiltPossible(n, a)
{
    let sum = 0, c1 = 0;

    // Calculate sum of elements
    // and count of 1's
    for (let i = 0; i < n; i++)
    {
        sum += a[i];

        if (a[i] == 1)
        {
            c1++;
        }
    }

    // If total sum is odd, return False
    if(sum % 2 != 0)
        return false;

    // If sum of each part is even,
    // return True
    if ((sum / 2) % 2 == 0)
        return true;

    // If sum of each part is even but
    // there is atleast one 1
    if (c1 > 0)
        return true;
    else
        return false;
}

// driver program

        let n = 3;
    let a = [ 1, 1, 2 ];

    if (isSpiltPossible(n, a))
        document.write("YES");
    else
        document.write("NO");

</script>
```

**Output:** 

```
YES
```

**时间复杂度:** O(N)