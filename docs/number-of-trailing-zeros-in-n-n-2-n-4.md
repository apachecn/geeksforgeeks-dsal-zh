# N *(N–2)*(N–4)*…中尾随零的数量。

> 原文:[https://www . geesforgeks . org/n-n-2-n-4 中尾随零的数量/](https://www.geeksforgeeks.org/number-of-trailing-zeros-in-n-n-2-n-4/)

给定一个整数 **N** ，任务是找出 **f(N)** 十进制记数法中尾随零的个数，其中 **f(N) = 1** 如果 **N < 2** 和**f(N)= N * f(N–2)**如果 **N ≥ 2**

**示例:**

> **输入:**N = 12
> T3】输出:1
> f(12)= 12 * 10 * 8 * 6 * 4 * 2 = 46080
> 
> **输入:**N = 7
> T3】输出: 0

**方法:**用十进制表示 **f(N)** 时尾随零的个数是 **f(N)** 被 **2** 整除的次数和 **f(N)** 被 **5** 整除的次数。有两种情况:

1.  当 **N** 为奇数时，则 **f(N)** 是一些奇数的乘积，因此它不会在 **2** 处断开。所以答案总是 **0** 。
2.  当 **N** 为偶数时，则 **f(N)** 可以表示为**2(1 * 2 * 3 *……。* N/2)** 。 **f(N)** 被 **2** 整除的次数大于被 **5** 整除的次数，所以只考虑被 **5** 整除的次数。现在，这个问题类似于[计算一个数的阶乘](https://www.geeksforgeeks.org/count-trailing-zeroes-factorial-number/)中的尾随零。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of
// trailing 0s in the given function
int findTrailingZeros(int n)
{
    // If n is odd
    if (n & 1)
        return 0;

    // If n is even
    else {
        int ans = 0;

        // Find the trailing zeros
        // in n/2 factorial
        n /= 2;
        while (n) {
            ans += n / 5;
            n /= 5;
        }

        // Return the required answer
        return ans;
    }
}

// Driver code
int main()
{
    int n = 12;

    cout << findTrailingZeros(n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

    // Function to return the count of
    // trailing 0s in the given function
    static int findTrailingZeros(int n)
    {
        // If n is odd
        if ((n & 1) == 1)
            return 0;

        // If n is even
        else
        {
            int ans = 0;

            // Find the trailing zeros
            // in n/2 factorial
            n /= 2;
            while (n != 0)
            {
                ans += n / 5;
                n /= 5;
            }

            // Return the required answer
            return ans;
        }
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 12;

        System.out.println(findTrailingZeros(n));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count of
# trailing 0s in the given function
def findTrailingZeros(n):

    # If n is odd
    if (n & 1):
        return 0

    # If n is even
    else:
        ans = 0

        # Find the trailing zeros
        # in n/2 factorial
        n //= 2
        while (n):
            ans += n // 5
            n //= 5

        # Return the required answer
        return ans

# Driver code

n = 12

print(findTrailingZeros(n))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to return the count of
    // trailing 0s in the given function
    static int findTrailingZeros(int n)
    {
        // If n is odd
        if ((n & 1) == 1)
            return 0;

        // If n is even
        else
        {
            int ans = 0;

            // Find the trailing zeros
            // in n/2 factorial
            n /= 2;
            while (n != 0)
            {
                ans += n / 5;
                n /= 5;
            }

            // Return the required answer
            return ans;
        }
    }

    // Driver code
    public static void Main(String[] args)
    {
        int n = 12;

        Console.WriteLine(findTrailingZeros(n));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the count of
// trailing 0s in the given function
function findTrailingZeros(n)
{

    // If n is odd
    if (n & 1)
        return 0;

    // If n is even
    else
    {
        let ans = 0;

        // Find the trailing zeros
        // in n/2 factorial
        n = parseInt(n / 2);

        while (n)
        {
            ans += parseInt(n / 5);
            n = parseInt(n / 5);
        }

        // Return the required answer
        return ans;
    }
}

// Driver code
let n = 12;

document.write(findTrailingZeros(n));

// This code is contributed by subhammahato348

</script>
```

**Output:** 

```
1
```