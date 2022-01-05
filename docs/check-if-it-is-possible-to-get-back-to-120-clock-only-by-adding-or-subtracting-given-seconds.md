# 检查是否只能通过加减给定秒

回到 12 点钟

> 原文:[https://www . geeksforgeeks . org/check-如果可能的话-只能通过加减给定的秒来恢复到 120 时钟/](https://www.geeksforgeeks.org/check-if-it-is-possible-to-get-back-to-120-clock-only-by-adding-or-subtracting-given-seconds/)

给定 N 秒。任务是检查是否有可能从 12 点钟开始，只加或减给定的秒就回到 12 点。我们需要将所有给定的秒精确地使用一次，我们可以添加一个元素或者减去它。
**例:**

```
Input: a[] = {60, 60, 120} 
Output: YES 
Add the first two seconds and 
subtract the last one to get back to 0\. 

Input : a[] = {10, 20, 60, 180} 
Output : NO 
```

**简单方法:**生成所有可能的组合来解决上述问题。因此生成 N 个数的[功率组](https://www.geeksforgeeks.org/power-set/)。检查任何一个的**总和(24*60)** 是否等于零，如果是，则有可能不是。
以下是上述方法的实现:

## C++

```
// C++ program to check if we come back to
// zero or not in a clock
#include <bits/stdc++.h>
using namespace std;

// Function to check all combinations
bool checkCombinations(int a[], int n)
{

    // Generate all power sets
    int pow_set_size = pow(2, n);
    int counter, j;

    // Check for every combination
    for (counter = 0; counter < pow_set_size; counter++) {

        // Store sum for all combinations
        int sum = 0;
        for (j = 0; j < n; j++) {

            /* Check if jth bit in the counter is set
             If set then print jth element from set */
            if (counter & (1 << j))
                sum += a[j]; // if set then consider as '+'
            else
                sum -= a[j]; // else consider as '-'
        }

        // If we can get back to 0
        if (sum % (24 * 60) == 0)
            return true;
    }
    return false;
}
// Driver Code
int main()
{
    int a[] = { 60, 60, 120 };
    int n = sizeof(a) / sizeof(a[0]);

    if (checkCombinations(a, n))
        cout << "YES";
    else
        cout << "NO";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if we come
// back to zero or not in a clock
import java.lang.Math;

class GfG
{

    // Function to check all combinations
    static boolean checkCombinations(int a[], int n)
    {
        // Generate all power sets
        int pow_set_size = (int)Math.pow(2, n);
        int counter, j;

        // Check for every combination
        for (counter = 0; counter < pow_set_size; counter++)
        {

            // Store sum for all combinations
            int sum = 0;
            for (j = 0; j < n; j++)
            {

                /* Check if jth bit in the counter is set
                If set then print jth element from set */
                if ((counter & (1 << j)) != 0)
                    sum += a[j]; // if set then consider as '+'
                else
                    sum -= a[j]; // else consider as '-'
            }

            // If we can get back to 0
            if (sum % (24 * 60) == 0)
                return true;
        }
        return false;
    }

    // Driver code
    public static void main(String []args)
    {
        int a[] = { 60, 60, 120 };
        int n = a.length;

        if (checkCombinations(a, n))
            System.out.println("YES");
        else
            System.out.println("NO");
    }
}

// This code is contributed by Rituraj Jain
```

## 蟒蛇 3

```
# Python 3 program to check if we come
# back to zero or not in a clock

# Function to check all combinations
def checkCombinations(a, n):

    # Generate all power sets
    pow_set_size = pow(2, n)

    # Check for every combination
    for counter in range(pow_set_size):

        # Store sum for all combinations
        sum = 0
        for j in range(n) :

            # Check if jth bit in the counter is set
            # If set then print jth element from set
            if (counter & (1 << j)):
                sum += a[j] # if set then consider as '+'
            else:
                sum -= a[j] # else consider as '-'

        # If we can get back to 0
        if (sum % (24 * 60) == 0):
            return True
    return False

# Driver Code
if __name__ == "__main__":

    a = [ 60, 60, 120 ]
    n = len(a)

    if (checkCombinations(a, n)):
        print("YES")
    else:
        print("NO")

# This code is contributed by ita_c
```

## C#

```
// C# program to check if we come
// back to zero or not in a clock
using System;

class GfG
{

    // Function to check all combinations
    static bool checkCombinations(int [] a, int n)
    {
        // Generate all power sets
        int pow_set_size = (int)Math.Pow(2, n);
        int counter, j;

        // Check for every combination
        for (counter = 0; counter < pow_set_size; counter++)
        {

            // Store sum for all combinations
            int sum = 0;
            for (j = 0; j < n; j++)
            {

                /* Check if jth bit in the counter is set
                If set then print jth element from set */
                if ((counter & (1 << j)) != 0)
                    sum += a[j]; // if set then consider as '+'
                else
                    sum -= a[j]; // else consider as '-'
            }

            // If we can get back to 0
            if (sum % (24 * 60) == 0)
                return true;
        }
        return false;
    }

    // Driver code
    public static void Main()
    {
        int [] a = { 60, 60, 120 };
        int n = a.Length;

        if (checkCombinations(a, n))
            Console.WriteLine("YES");
        else
            Console.WriteLine("NO");
    }
}

// This code is contributed by ihritik
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to check if we come back to
// zero or not in a clock

// Function to check all combinations
function checkCombinations($a, $n)
{

    // Generate all power sets
    $pow_set_size = pow(2, $n);

    // Check for every combination
    for ($counter = 0;
         $counter < $pow_set_size; $counter++)
    {

        // Store sum for all combinations
        $sum = 0;
        for ($j = 0; $j < $n; $j++)
        {

            /* Check if jth bit in the counter is set
            If set then print jth element from set */
            if ($counter & (1 << $j))
                $sum += $a[$j]; // if set then consider as '+'
            else
                $sum -= $a[$j]; // else consider as '-'
        }

        // If we can get back to 0
        if ($sum % (24 * 60) == 0)
            return true;
    }
    return false;
}

// Driver Code
$a = array( 60, 60, 120 );
$n = sizeof($a);

if (checkCombinations($a, $n))
    echo "YES";
else
    echo "NO";

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// JavaScript program to check if we come
// back to zero or not in a clock

    // Function to check all combinations
    function checkCombinations(a , n) {
        // Generate all power sets
        var pow_set_size = parseInt( Math.pow(2, n));
        var counter, j;

        // Check for every combination
        for (counter = 0; counter < pow_set_size; counter++)
        {

            // Store sum for all combinations
            var sum = 0;
            for (j = 0; j < n; j++) {

                /*
                 * Check if jth bit in the counter is
                 set If set then print jth element from set
                 */
                if ((counter & (1 << j)) != 0)
                    sum += a[j]; // if set then consider as '+'
                else
                    sum -= a[j]; // else consider as '-'
            }

            // If we can get back to 0
            if (sum % (24 * 60) == 0)
                return true;
        }
        return false;
    }

    // Driver code

        var a = [ 60, 60, 120 ];
        var n = a.length;

        if (checkCombinations(a, n))
            document.write("YES");
        else
            document.write("NO");

// This code contributed by Rajput-Ji

</script>
```

**Output:** 

```
YES
```

如果我们仔细观察，可以发现这个问题基本上是[分区问题](https://www.geeksforgeeks.org/partition-problem-dp-18/)的一个变种。所以我们可以使用动态规划进行优化(请参考[分区问题](https://www.geeksforgeeks.org/partition-problem-dp-18/)的方法 2)。