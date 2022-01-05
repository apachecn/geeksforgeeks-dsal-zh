# 由三个给定的非零数字组成的 3 的最小倍数

> 原文:[https://www . geesforgeks . org/3 的最小倍数，由三个给定的非零数字组成/](https://www.geeksforgeeks.org/smallest-multiple-of-3-which-consists-of-three-given-non-zero-digits/)

给定三个非零数字 **0 < A、B、C < 9** 。任务是找到能被 **3** 整除的最小数，所有的数字都在集合{A，B，C}中。
**注:**不必全部包括三位数字。结果可以是 **A** 、 **AA** 、 **AB** 、 **CCA** 等。
**举例:**

> **输入:** A = 2，B = 4，C = 7
> **输出:** 24
> 24 是给定数字能构成的最小可被 3 整除数。
> **输入:** A = 1，B = 2，C = 3
> **输出:** 3

**方法:**取一个数组中的所有三个数字，按升序排序。现在检查任何一个数是否能被 **3** 整除，如果**是**，那么这个数就是答案。
如果**不是**，则再次通过取两个数字中的任何一个来检查是否。最后取最小的数，我们的结果是这个数重复三次。
**为什么不能得到长度超过三位数的答案？**
即使任意一个数不能被 3 整除，把最小的数重复 3 次也会使其被 3 整除。注意[一个数如果其位数之和可被 3 整除](https://www.geeksforgeeks.org/check-large-number-divisible-3-not/)。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum number
// divisible by 3 formed by the given digits
int printSmallest(int a[3])
{
    int sum, sum1;

    // Sort the given array in ascending
    sort(a, a + 3);

    int i, j, k, num;

    // Check if any single digit is divisible by 3
    for (int i = 0; i < 3; i++) {
        if (a[i] % 3 == 0)
            return a[i];
    }

    // Check if any two digit number formed by
    // the given digits is divisible by 3
    // starting from the minimum
    for (i = 0; i < 3; i++) {
        for (j = 0; j < 3; j++) {

            // Generate the two digit number
            num = (a[i] * 10) + a[j];
            if (num % 3 == 0)
                return num;
        }
    }

    // If none of the above is true, we can
    // form three digit number by taking a[0]
    // three times.
    return a[0]*100 + a[0]*10 + a[0];
}

// Driver code
int main()
{
    int arr[] = { 7, 7, 1 };
    cout << printSmallest(arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.Arrays;
public class GFG {

// Function to return the minimum number
// divisible by 3 formed by the given digits
    static int printSmallest(int a[]) {
        int sum, sum1;

        // Sort the given array in ascending
        Arrays.sort(a);

        int i, j, k, num;

        // Check if any single digit is divisible by 3
        for (i = 0; i < 3; i++) {
            if (a[i] % 3 == 0) {
                return a[i];
            }
        }

        // Check if any two digit number formed by
        // the given digits is divisible by 3
        // starting from the minimum
        for (i = 0; i < 3; i++) {
            for (j = 0; j < 3; j++) {

                // Generate the two digit number
                num = (a[i] * 10) + a[j];
                if (num % 3 == 0) {
                    return num;
                }
            }
        }

        // If none of the above is true, we can
        // form three digit number by taking a[0]
        // three times.
        return a[0] * 100 + a[0] * 10 + a[0];
    }

// Driver code
    public static void main(String[] args) {

        int arr[] = {7, 7, 1};
        System.out.println(printSmallest(arr));

    }
}
// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the minimum
# number divisible by 3 formed by
# the given digits
def printSmallest(a, n):

    sum0, sum1 = 0, 0

    # Sort the given array in ascending
    a = sorted(a)

    # Check if any single digit is
    # divisible by 3
    for i in range(n):
        if (a[i] % 3 == 0):
            return a[i]

    # Check if any two digit number
    # formed by the given digits is
    # divisible by 3 starting from
    # the minimum
    for i in range(n):
        for j in range(n):

            # Generate the two digit number
            num = (a[i] * 10) + a[j]
            if (num % 3 == 0):
                return num

    # If none of the above is true, we can
    # form three digit number by taking a[0]
    # three times.
    return a[0] * 100 + a[0] * 10 + a[0]

# Driver code
arr = [7, 7, 1 ]
n = len(arr)

print(printSmallest(arr, n))

# This code is contributed
# by mohit kumar 29
```

## C#

```

// C# implementation of the approach
using System;

public class GFG {

// Function to return the minimum number
// divisible by 3 formed by the given digits
    static int printSmallest(int []a) {

        // Sort the given array in ascending
        Array.Sort(a);

        int i, j, num;

        // Check if any single digit is divisible by 3
        for (i = 0; i < 3; i++) {
            if (a[i] % 3 == 0) {
                return a[i];
            }
        }

        // Check if any two digit number formed by
        // the given digits is divisible by 3
        // starting from the minimum
        for (i = 0; i < 3; i++) {
            for (j = 0; j < 3; j++) {

                // Generate the two digit number
                num = (a[i] * 10) + a[j];
                if (num % 3 == 0) {
                    return num;
                }
            }
        }

        // If none of the above is true, we can
        // form three digit number by taking a[0]
        // three times.
        return a[0] * 100 + a[0] * 10 + a[0];
    }

// Driver code
    public static void Main() {

        int []arr = {7, 7, 1};
        Console.Write(printSmallest(arr));

    }
}
//This code is contributed by Rajput-Ji
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the minimum number
// divisible by 3 formed by the given digits
function printSmallest($a)
{

    // Sort the given array in ascending
    sort($a);

    // Check if any single digit
    // is divisible by 3
    for ($i = 0; $i < 3; $i++)
    {
        if ($a[$i] % 3 == 0)
            return $a[$i];
    }

    // Check if any two digit number formed
    // by the given digits is divisible by 3
    // starting from the minimum
    for ($i = 0; $i < 3; $i++)
    {
        for ($j = 0; $j < 3; $j++)
        {

            // Generate the two digit number
            $num = ($a[$i] * 10) + $a[$j];
            if ($num % 3 == 0)
                return $num;
        }
    }

    // If none of the above is true, we can
    // form three digit number by taking a[0]
    // three times.
    return $a[0] * 100 + $a[0] * 10 + $a[0];
}

// Driver code
$arr = array( 7, 7, 1 );
echo printSmallest($arr);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

    // JavaScript implementation of the approach

    // Function to return the minimum number
    // divisible by 3 formed by the given digits
    function printSmallest(a) {

        // Sort the given array in ascending
        a.sort(function(a, b){return a - b});

        let i, j, num;

        // Check if any single digit is divisible by 3
        for (i = 0; i < 3; i++) {
            if (a[i] % 3 == 0) {
                return a[i];
            }
        }

        // Check if any two digit number formed by
        // the given digits is divisible by 3
        // starting from the minimum
        for (i = 0; i < 3; i++) {
            for (j = 0; j < 3; j++) {

                // Generate the two digit number
                num = (a[i] * 10) + a[j];
                if (num % 3 == 0) {
                    return num;
                }
            }
        }

        // If none of the above is true, we can
        // form three digit number by taking a[0]
        // three times.
        return a[0] * 100 + a[0] * 10 + a[0];
    }

    let arr = [7, 7, 1];
      document.write(printSmallest(arr));

</script>
```

**Output:** 

```
111
```