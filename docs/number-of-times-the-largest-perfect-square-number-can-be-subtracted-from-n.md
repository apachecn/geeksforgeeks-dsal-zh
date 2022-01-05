# 可以从 N 中减去最大完美平方数的次数

> 原文:[https://www . geeksforgeeks . org/次数-最大完美平方数-可以从 n 中减去的数/](https://www.geeksforgeeks.org/number-of-times-the-largest-perfect-square-number-can-be-subtracted-from-n/)

给定一个数字 **N** 。在每一步中，从 N 中减去最大的完美平方(≤ N)。当 **N > 0** 时重复这一步。任务是计算可以执行的步骤数。

**示例:**

> **输入:** N = 85
> **输出:** 2
> 第一步，85–(9 * 9)= 4
> 第二步 4–(2 * 2)= 0
> 
> **输入:** N = 114
> **输出:** 4
> 第一步，114 –( 10 * 10)= 14
> 第二步 14–(3 * 3)= 5
> 第三步 5–(2 * 2)= 1
> 第四步 1–(1 * 1)= 0

**逼近**:在 **N > 0** 的同时，从 **N** 中迭代减去最大完美平方 **(≤ N)** ，并计算步数。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of steps
int countSteps(int n)
{

    // Variable to store the count of steps
    int steps = 0;

    // Iterate while N > 0
    while (n) {

        // Get the largest perfect square
        // and subtract it from N
        int largest = sqrt(n);
        n -= (largest * largest);

        // Increment steps
        steps++;
    }

    // Return the required count
    return steps;
}

// Driver code
int main()
{
    int n = 85;
    cout << countSteps(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.lang.Math;

public class GfG{

    // Function to return the count of steps
    static int countSteps(int n)
    {
        // Variable to store the count of steps
        int steps = 0;

        // Iterate while N > 0
        while (n > 0) {

            // Get the largest perfect square
            // and subtract it from N
            int largest = (int)Math.sqrt(n);
            n -= (largest * largest);

            // Increment steps
            steps++;
        }

        // Return the required count
        return steps;
    }

     public static void main(String []args){

        int n = 85;
        System.out.println(countSteps(n));
     }
}

// This code is contributed by Rituraj Jain
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from math import sqrt

# Function to return the count of steps
def countSteps(n) :

    # Variable to store the count of steps
    steps = 0;

    # Iterate while N > 0
    while (n) :

        # Get the largest perfect square
        # and subtract it from N
        largest = int(sqrt(n));
        n -= (largest * largest);

        # Increment steps
        steps += 1;

    # Return the required count
    return steps;

# Driver code
if __name__ == "__main__" :

    n = 85;
    print(countSteps(n));

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;

class GfG
{

    // Function to return the count of steps
    static int countSteps(int n)
    {
        // Variable to store the count of steps
        int steps = 0;

        // Iterate while N > 0
        while (n > 0)
        {

            // Get the largest perfect square
            // and subtract it from N
            int largest = (int)Math.Sqrt(n);
            n -= (largest * largest);

            // Increment steps
            steps++;
        }

        // Return the required count
        return steps;
    }

    // Driver code
    public static void Main()
    {
        int n = 85;
        Console.WriteLine(countSteps(n));
    }
}

// This code is contributed by Code_Mech.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to return the count of steps
function countSteps($n)
{

    // Variable to store the count of steps
    $steps = 0;

    // Iterate while N > 0
    while ($n)
    {

        // Get the largest perfect square
        // and subtract it from N
        $largest = (int)sqrt($n);
        $n -= ($largest * $largest);

        // Increment steps
        $steps++;
    }

    // Return the required count
    return $steps;
}

// Driver code
$n = 85;
echo countSteps($n);

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to return the count of steps
function countSteps(n)
{

    // Variable to store the count of steps
    let steps = 0;

    // Iterate while N > 0
    while (n)
    {

        // Get the largest perfect square
        // and subtract it from N
        let largest = Math.floor(Math.sqrt(n));
        n -= (largest * largest);

        // Increment steps
        steps++;
    }

    // Return the required count
    return steps;
}

// Driver code

let n = 85;

document.write(countSteps(n));

// This code is contributed by Manoj.

</script>
```

**Output:** 

```
2
```

**时间复杂度:** O(1)

**辅助空间:** O(1)