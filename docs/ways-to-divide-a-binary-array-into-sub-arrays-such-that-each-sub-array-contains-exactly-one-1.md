# 将二进制数组分成子数组的方法，这样每个子数组恰好包含一个 1

> 原文:[https://www . geesforgeks . org/将二进制数组划分为子数组的方法-这样-每个子数组-包含-恰好一-1/](https://www.geeksforgeeks.org/ways-to-divide-a-binary-array-into-sub-arrays-such-that-each-sub-array-contains-exactly-one-1/)

给出由集合 **{0，1}** 中的元素组成的整数数组 **arr[]** 。任务是打印阵列可以分成子阵列的方式数，使得每个子阵列恰好包含一个 **1** 。

**示例:**

> **输入:** arr[] = {1，0，1，0，1}
> **输出:** 4
> 以下是可能的方式:
> 
> *   {1, 0}, {1, 0}, {1}
> *   {1}, {0, 1, 0}, {1}
> *   {1, 0}, {1}, {0, 1}
> *   {1}, {0, 1}, {0, 1}
> 
> **输入:** arr[] = {0，0，0 }
> T3】输出: 0

**进场:**

*   当数组的所有元素都为 **0** 时，那么结果将为零。
*   否则，在相邻的两个之间，我们只能有一次分离。所以，答案等于值**pos<sub>I+1</sub>–pos<sub>I</sub>**(对于所有有效对)的乘积，其中**pos<sub>I</sub>T9】是 i <sup>th</sup> **1** 的位置。**

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the number of ways
// the array can be divided into sub-arrays
// satisfying the given condition
int countWays(int arr[], int n)
{

    int pos[n], p = 0, i;

    // for loop for saving the positions of all 1s
    for (i = 0; i < n; i++) {
        if (arr[i] == 1) {
            pos[p] = i + 1;
            p++;
        }
    }

    // If array contains only 0s
    if (p == 0)
        return 0;

    int ways = 1;
    for (i = 0; i < p - 1; i++) {
        ways *= pos[i + 1] - pos[i];
    }

    // Return the total ways
    return ways;
}

// Driver code
int main()
{
    int arr[] = { 1, 0, 1, 0, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);
    cout << countWays(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function to return the number of ways
// the array can be divided into sub-arrays
// satisfying the given condition
static int countWays(int arr[], int n)
{
    int pos[] = new int[n];
    int p = 0, i;

    // for loop for saving the
    // positions of all 1s
    for (i = 0; i < n; i++)
    {
        if (arr[i] == 1)
        {
            pos[p] = i + 1;
            p++;
        }
    }

    // If array contains only 0s
    if (p == 0)
        return 0;

    int ways = 1;
    for (i = 0; i < p - 1; i++)
    {
        ways *= pos[i + 1] - pos[i];
    }

    // Return the total ways
    return ways;
}

// Driver code
public static void main(String args[])
{
    int[] arr = { 1, 0, 1, 0, 1 };
    int n = arr.length;
    System.out.println(countWays(arr, n));
}
}

// This code is contributed
// by Akanksha Rai
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to return the number of ways
# the array can be divided into sub-arrays
# satisfying the given condition
def countWays(are, n):
    pos = [0 for i in range(n)]
    p = 0

    # for loop for saving the positions
    # of all 1s
    for i in range(n):
        if (arr[i] == 1):
            pos[p] = i + 1
            p += 1

    # If array contains only 0s
    if (p == 0):
        return 0

    ways = 1
    for i in range(p - 1):
        ways *= pos[i + 1] - pos[i]

    # Return the total ways
    return ways

# Driver code
if __name__ == '__main__':
    arr = [1, 0, 1, 0, 1]
    n = len(arr)
    print(countWays(arr, n))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the number of ways
// the array can be divided into sub-arrays
// satisfying the given condition
static int countWays(int[] arr, int n)
{
    int[] pos = new int[n];
    int p = 0, i;

    // for loop for saving the positions
    // of all 1s
    for (i = 0; i < n; i++)
    {
        if (arr[i] == 1)
        {
            pos[p] = i + 1;
            p++;
        }
    }

    // If array contains only 0s
    if (p == 0)
        return 0;

    int ways = 1;
    for (i = 0; i < p - 1; i++)
    {
        ways *= pos[i + 1] - pos[i];
    }

    // Return the total ways
    return ways;
}

// Driver code
public static void Main()
{
    int[] arr = { 1, 0, 1, 0, 1 };
    int n = arr.Length;
    Console.Write(countWays(arr, n));
}
}

// This code is contributed
// by Akanksha Rai
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the number of ways
// the array can be divided into sub-arrays
// satisfying the given condition
function countWays($arr, $n)
{
    $pos = array_fill(0, $n, 0);
    $p = 0 ;

    // for loop for saving the positions
    // of all 1s
    for ($i = 0; $i < $n; $i++)
    {
        if ($arr[$i] == 1)
        {
            $pos[$p] = $i + 1;
            $p++;
        }
    }

    // If array contains only 0s
    if ($p == 0)
        return 0;

    $ways = 1;
    for ($i = 0; $i < $p - 1; $i++)
    {
        $ways *= $pos[$i + 1] - $pos[$i];
    }

    // Return the total ways
    return $ways;
}

// Driver code
$arr = array(1, 0, 1, 0, 1);
$n = sizeof($arr);
echo countWays($arr, $n);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>
      // JavaScript implementation of the approach
      // Function to return the number of ways
      // the array can be divided into sub-arrays
      // satisfying the given condition
      function countWays(arr, n) {
        var pos = new Array(n).fill(0);
        var p = 0, i;

        // for loop for saving the positions
        // of all 1s
        for (i = 0; i < n; i++) {
          if (arr[i] === 1) {
            pos[p] = i + 1;
            p++;
          }
        }

        // If array contains only 0s
        if (p === 0)
            return 0;

        var ways = 1;
        for (i = 0; i < p - 1; i++) {
          ways *= pos[i + 1] - pos[i];
        }

        // Return the total ways
        return ways;
      }

      // Driver code
      var arr = [1, 0, 1, 0, 1];
      var n = arr.length;
      document.write(countWays(arr, n));
</script>
```

**Output:** 

```
4
```