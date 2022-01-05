# 数组操作和求和

> 原文:[https://www.geeksforgeeks.org/array-manipulation-and-sum/](https://www.geeksforgeeks.org/array-manipulation-and-sum/)

给定一个由 **N** 个整数和一个整数 **S** 组成的数组 **arr[]** 。任务是在数组中找到一个元素 **K** ，这样如果数组中的所有元素 **> K** 都等于 **K** ，那么结果数组中所有元素的总和就等于 **S** 。如果无法找到这样的元素，则打印 **-1** 。
**举例:**

> **输入:** M = 15，arr[] = {12，3，6，7，8}
> **输出:** 3
> 合成数组= {3，3，3，3，3，3}
> 数组元素之和= 15 = S
> **输入:** M = 5，arr[] = {1，3，2，5，8}
> **输出:** 1

**方法:**对数组进行排序。考虑到 **K** 的值等于当前元素，遍历数组，然后检查**先前元素的和+ (K *剩余元素的数量)= S** 。如果**是**则打印 **K** 的值，如果没有找到这样的元素则打印 **-1** 到最后。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the required element
int getElement(int a[], int n, int S)
{
    // Sort the array
    sort(a, a + n);

    int sum = 0;

    for (int i = 0; i < n; i++) {

        // If current element
        // satisfies the condition
        if (sum + (a[i] * (n - i)) == S)
            return a[i];
        sum += a[i];
    }

    // No element found
    return -1;
}

// Driver code
int main()
{
    int S = 5;
    int a[] = { 1, 3, 2, 5, 8 };
    int n = sizeof(a) / sizeof(a[0]);

    cout << getElement(a, n, S);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
//Java implementation of the approach
import java.util.Arrays;

class GFG
{
    // Function to return the required element
    static int getElement(int a[], int n, int S)
    {
        // Sort the array
        Arrays.sort(a);

        int sum = 0;

        for (int i = 0; i < n; i++)
        {

            // If current element
            // satisfies the condition
            if (sum + (a[i] * (n - i)) == S)
                return a[i];
            sum += a[i];
        }

        // No element found
        return -1;
    }

    // Driver code
    public static void main(String[] args)
    {
        int S = 5;
        int a[] = { 1, 3, 2, 5, 8 };
        int n = a.length;

        System.out.println(getElement(a, n, S));
    }
}

// This code is contributed by Mukul singh.
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the required element
def getElement(a, n, S) :

    # Sort the array
    a.sort();

    sum = 0;

    for i in range(n) :

        # If current element
        # satisfies the condition
        if (sum + (a[i] * (n - i)) == S) :
            return a[i];

        sum += a[i];

    # No element found
    return -1;

# Driver Code
if __name__ == "__main__" :

    S = 5;
    a = [ 1, 3, 2, 5, 8 ];
    n = len(a) ;

    print(getElement(a, n, S)) ;

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
    // Function to return the required element
    static int getElement(int[] a, int n, int S)
    {
        // Sort the array
        Array.Sort(a);

        int sum = 0;

        for (int i = 0; i < n; i++)
        {

            // If current element
            // satisfies the condition
            if (sum + (a[i] * (n - i)) == S)
                return a[i];
            sum += a[i];
        }

        // No element found
        return -1;
    }

    // Driver code
    public static void Main()
    {
        int S = 5;
        int[] a = { 1, 3, 2, 5, 8 };
        int n = a.Length;

        Console.WriteLine(getElement(a, n, S));
    }
}

// This code is contributed by Mukul singh.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the required element
function getElement($a, $n, $S)
{
    // Sort the array
    sort($a, 0);

    $sum = 0;

    for ($i = 0; $i < $n; $i++)
    {

        // If current element
        // satisfies the condition
        if ($sum + ($a[$i] *
           ($n - $i)) == $S)
            return $a[$i];
        $sum += $a[$i];
    }

    // No element found
    return -1;
}

// Driver code
$S = 5;
$a = array(1, 3, 2, 5, 8);
$n = sizeof($a);

echo getElement($a, $n, $S);

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>
 //Javascript implementation of the approach

// Function to return the required element
function getElement(a, n, S)
{
    // Sort the array
    a.sort();

    var sum = 0;

    for (var i = 0; i < n; i++) {

        // If current element
        // satisfies the condition
        if (sum + (a[i] * (n - i)) == S)
            return a[i];
        sum += a[i];
    }

    // No element found
    return -1;
}

var S = 5;
var a = [ 1, 3, 2, 5, 8 ];
var n = a.length;
document.write(getElement(a, n, S));

// This code is contributed by SoumikMondal
</script>
```

**Output:** 

```
1
```

**时间复杂度:**O(N * logN)
T3】辅助空间: O(1)