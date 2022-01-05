# 2019 年(i * j) %的最小可能值

> 原文:[https://www . geeksforgeeks . org/I-j-2019 最低可能价值/](https://www.geeksforgeeks.org/minimum-possible-value-of-i-j-2019/)

给定两个整数 **L** 和 **R** ，任务是求 **(i * j) % 2019** 的最小可能值，其中 **L ≤ i < j ≤ R**
**例:**

> **输入:** L = 2020，R = 2040
> **输出:**2
> (2020 * 2021)% 2019 = 2
> **输入:** L = 3，R = 4
> **输出:** 12

**进场:**

*   如果**R–L≥2019**，则答案为 0，因为我们将得到一个可被 2019 整除的数字，其余数为 0。
*   如果**R–L<2019**那么我们可以运行嵌套循环并找到最小值。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

const int MOD = 2019;

// Function to return the minimum
// possible value of (i * j) % 2019
int min_modulo(int l, int r)
{
    // If we can get a number
    // divisible by 2019
    if (r - l >= MOD)
        return 0;
    else {

        // Find the minimum value
        // by running nested loops
        int ans = MOD - 1;
        for (int i = l; i <= r; i++) {
            for (int j = i + 1; j <= r; j++) {
                ans = min(ans, (i * j) % MOD);
            }
        }
        return ans;
    }
}

// Driver code
int main()
{
    int l = 2020, r = 2040;

    cout << min_modulo(l, r);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{
static int MOD = 2019;

// Function to return the minimum
// possible value of (i * j) % 2019
static int min_modulo(int l, int r)
{
    // If we can get a number
    // divisible by 2019
    if (r - l >= MOD)
        return 0;
    else
    {

        // Find the minimum value
        // by running nested loops
        int ans = MOD - 1;
        for (int i = l; i <= r; i++)
        {
            for (int j = i + 1; j <= r; j++)
            {
                ans = Math.min(ans, (i * j) % MOD);
            }
        }
        return ans;
    }
}

// Driver code
public static void main(String []args)
{
    int l = 2020, r = 2040;

    System.out.println(min_modulo(l, r));
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach
MOD = 2019;

# Function to return the minimum
# possible value of (i * j) % 2019
def min_modulo(l, r) :

    # If we can get a number
    # divisible by 2019
    if (r - l >= MOD) :
        return 0;
    else :

        # Find the minimum value
        # by running nested loops
        ans = MOD - 1;
        for i in range(l, r + 1) :
            for j in range(i + 1, r + 1) :
                ans = min(ans, (i * j) % MOD);

        return ans;

# Driver code
if __name__ == "__main__" :

    l = 2020; r = 2040;

    print(min_modulo(l, r));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{
static int MOD = 2019;

// Function to return the minimum
// possible value of (i * j) % 2019
static int min_modulo(int l, int r)
{
    // If we can get a number
    // divisible by 2019
    if (r - l >= MOD)
        return 0;
    else
    {

        // Find the minimum value
        // by running nested loops
        int ans = MOD - 1;
        for (int i = l; i <= r; i++)
        {
            for (int j = i + 1; j <= r; j++)
            {
                ans = Math.Min(ans, (i * j) % MOD);
            }
        }
        return ans;
    }
}

// Driver code
public static void Main(String []args)
{
    int l = 2020, r = 2040;

    Console.WriteLine(min_modulo(l, r));
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

    // JavaScript implementation of the approach

    let MOD = 2019;

    // Function to return the minimum
    // possible value of (i * j) % 2019
    function min_modulo(l, r)
    {
        // If we can get a number
        // divisible by 2019
        if (r - l >= MOD)
            return 0;
        else
        {

            // Find the minimum value
            // by running nested loops
            let ans = MOD - 1;
            for (let i = l; i <= r; i++)
            {
                for (let j = i + 1; j <= r; j++)
                {
                    ans = Math.min(ans, (i * j) % MOD);
                }
            }
            return ans;
        }
    }

    let l = 2020, r = 2040;

    document.write(min_modulo(l, r));

</script>
```

**Output:** 

```
2
```