# 在生成的数组中找到第 kth 个位置的值

> 原文:[https://www . geeksforgeeks . org/find-the-value-at-kth-position-in-generated-array/](https://www.geeksforgeeks.org/find-the-value-at-kth-position-in-the-generated-array/)

给定三个整数 **n** 、 **m** 和 **k** 。重复给定的操作 **n** 次后，找到 **k <sup>th</sup>** 位置的元素。在单个操作中，大于数组中最大元素的整数 1 被追加到数组中，然后原始数组被追加。比如 **arr[] = {3，4，1}** 单次操作后会是 **arr[] = {3，4，1，5，3，4，1}** 。
**注意**数组开头包含单个元素，即 **m** 。
**例:**

> **输入:** n = 3，m = 3，k = 3
> **输出:** 3
> 每一步后的数组:
> 操作 1: arr[] = {3，4，3}
> 操作 2: arr[] = {3，4，3，5，3，4，3}
> 操作 3: arr[] = {3，4，3，5，3，4，6，3，4，3，5，3，4，3}

****方法:**对于蛮力方法，生成结果数组，然后在 k 位置找到元素，但是时间消耗和内存消耗会相当高。因此，在进行实际解决之前，让我们对问题陈述进行一些分析。** 

*   **第一个元素总是 m，无论上述步骤重复多少次，m 都会交替出现。**
*   **类似地，第二个元素将是 m+1，并且在每个第四个元素之后重复。意味着它的位置是 2，6，10..**
*   **第三个元素将再次是 m。**
*   **第四个元素是 m+2，在第八个元素之后重复。意味着它的位置是 4，12，20…**

**从应用反向方法后的上述分析中可以得出结论，位置 k 处的元素取决于 k 的二进制表示，即位置处的元素等于(m-1)+k 中最右边设置位的位置。
下面是上述方法的实现:** 

## **C++**

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find value at k-th position
int findValueAtK(int n, int m, int k)
{
    // __builtin_ffsll return the position
    // of rightmost setbit
    int positionOfRightmostSetbit = __builtin_ffs(k);

    // Return the required element
    return ((m - 1) + positionOfRightmostSetbit);
}

// Driver code
int main()
{
    int k = 100, n = 9, m = 74;
    cout << findValueAtK(n, m, k);

    return 0;
}
```

## **Java 语言(一种计算机语言，尤用于创建网站)**

```
// Java implementation of the approach
class GFG
{

    static int INT_SIZE = 32;

    // function returns the position
    // of rightmost setbit
    static int Right_most_setbit(int num)
    {
        int pos = 1;
        // counting the position of first set bit
        for (int i = 0; i < INT_SIZE; i++)
        {
            if ((num & (1 << i))== 0)
                pos++;

            else
                break;
        }
        return pos;
    }

    // Function to find value at k-th position
    static int findValueAtK(int n, int m, int k)
    {

        int positionOfRightmostSetbit = Right_most_setbit(k);

        // Return the required element
        return ((m - 1) + positionOfRightmostSetbit);
    }

    // Driver code
    public static void main (String[] args)
    {
        int k = 100, n = 9, m = 74;
        System.out.println(findValueAtK(n, m, k));

    }

}

// This code is contributed by ihritik
```

## **蟒蛇 3**

```
# Python3 implementation of the approach
import math

# Function to find value
# at k-th position
def findValueAtK(n, m, k):

    # __builtin_ffsll return the position
    # of rightmost setbit
    positionOfRightmostSetbit = math.log2(k & -k) + 1

    # Return the required element
    return ((m - 1) + positionOfRightmostSetbit)

# Driver code
k = 100
n = 9
m = 74
print(findValueAtK(n, m, k))

# This code is contributed
# by mohit kumar
```

## **C#**

```
// C# implementation of the approach
using System;

class GFG
{

    static int INT_SIZE = 32;

    // function returns the position
    // of rightmost setbit
    static int Right_most_setbit(int num)
    {
        int pos = 1;

        // counting the position of first set bit
        for (int i = 0; i < INT_SIZE; i++)
        {
            if ((num & (1 << i)) == 0)
                pos++;

            else
                break;
        }
        return pos;
    }

    // Function to find value at k-th position
    static int findValueAtK(int n, int m, int k)
    {

        int positionOfRightmostSetbit = Right_most_setbit(k);

        // Return the required element
        return ((m - 1) + positionOfRightmostSetbit);
    }

    // Driver code
    public static void Main ()
    {
        int k = 100, n = 9, m = 74;
        Console.WriteLine(findValueAtK(n, m, k));

    }
}

// This code is contributed by ihritik
```

## **服务器端编程语言（Professional Hypertext Preprocessor 的缩写）**

```
<?php
// PHP implementation of the approach

// Function to find value
// at k-th position
function findValueAtK($n, $m, $k)
{

    // __builtin_ffsll return the position
    // of rightmost setbit
    $temp = $k & -$k ;
    $positionOfRightmostSetbit = log($temp, 2) + 1;

    // Return the required element
    return (($m - 1) + $positionOfRightmostSetbit);
}

// Driver code
$k = 100;
$n = 9;
$m = 74;

echo findValueAtK($n, $m, $k);

// This code is contributed by Ryuga
?>
```

## **java 描述语言**

```
<script>

// Javascript implementation of the approach

    var INT_SIZE = 32;

    // function returns the position
    // of rightmost setbit
    function Right_most_setbit(num)
    {
        var pos = 1;

        // counting the position of first set bit
        for (var i = 0; i < INT_SIZE; i++)
        {
            if ((num & (1 << i)) == 0)
                pos++;

            else
                break;
        }
        return pos;
    }

    // Function to find value at k-th position
    function findValueAtK(n, m,  k)
    {

        var positionOfRightmostSetbit = Right_most_setbit(k);

        // Return the required element
        return ((m - 1) + positionOfRightmostSetbit);
    }

    // Driver code

        var k = 100, n = 9, m = 74;
        document.write(findValueAtK(n, m, k))
</script>
```

****Output:** 

```
76
```** 

**时间复杂度:0(1)**

**辅助空间:0(1)**