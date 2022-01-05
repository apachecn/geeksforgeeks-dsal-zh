# 数组中总和等于乘积的对的数量

> 原文:[https://www . geeksforgeeks . org/数组中具有等于乘积和的对数/](https://www.geeksforgeeks.org/number-of-pairs-in-an-array-having-sum-equal-to-product/)

给定一个数组 **arr[]** ，任务是找出数组中的对的数量 **(arr[i]，arr[j])** ，使得**arr[I]+arr[j]= arr[I]* arr[j]**
**示例:**

> **输入:** arr[] = {2，2，3，4，6}
> **输出:** 1
> (2，2)是唯一可能的对，因为(2 + 2) = (2 * 2) = 4。
> **输入:** arr[] = {1，2，3，4，5}
> **输出:** 0

**方法:**唯一可能满足给定条件的整数对是 **(0，0)** 和 **(2，2)** 。所以现在的任务是统计数组中**0**和 **2s** 的个数，分别存储在 **cnt0** 和 **cnt2** 中，那么需要的个数就是**(CNT 0 *(CNT 0–1))/2+(CNT 2 *(CNT 2–1))/2**。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count
// of the required pairs
int sumEqualProduct(int a[], int n)
{
    int zero = 0, two = 0;

    // Find the count of 0s
    // and 2s in the array
    for (int i = 0; i < n; i++) {
        if (a[i] == 0) {
            zero++;
        }
        if (a[i] == 2) {
            two++;
        }
    }

    // Find the count of required pairs
    int cnt = (zero * (zero - 1)) / 2
              + (two * (two - 1)) / 2;

    // Return the count
    return cnt;
}

// Driver code
int main()
{
    int a[] = { 2, 2, 3, 4, 2, 6 };
    int n = sizeof(a) / sizeof(a[0]);

    cout << sumEqualProduct(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG {
    // Function to return the count
    // of the required pairs
    static int sumEqualProduct(int a[], int n)
    {
        int zero = 0, two = 0;

        // Find the count of 0s
        // and 2s in the array
        for (int i = 0; i < n; i++) {
            if (a[i] == 0) {
                zero++;
            }
            if (a[i] == 2) {
                two++;
            }
        }

        // Find the count of required pairs
        int cnt = (zero * (zero - 1)) / 2
                  + (two * (two - 1)) / 2;

        // Return the count
        return cnt;
    }

    // Driver code
    public static void main(String[] args)
    {
        int a[] = { 2, 2, 3, 4, 2, 6 };
        int n = a.length;

        System.out.print(sumEqualProduct(a, n));
    }
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python 3 implementation of the approach

# Function to return the count
# of the required pairs
def sumEqualProduct(a, n):
    zero = 0
    two = 0

    # Find the count of 0s
    # and 2s in the array
    for i in range(n):
        if a[i] == 0:
            zero += 1
        if a[i] == 2:
            two += 1

    # Find the count of required pairs
    cnt = (zero * (zero - 1)) // 2 + \
            (two * (two - 1)) // 2

    # Return the count
    return cnt

# Driver code
a = [ 2, 2, 3, 4, 2, 6 ]
n = len(a)

print(sumEqualProduct(a, n))

# This code is contributed by Ankit kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to return the count
// of the required pairs
static int sumEqualProduct(int []a, int n)
{
    int zero = 0, two = 0;

    // Find the count of 0s
    // and 2s in the array
    for (int i = 0; i < n; i++)
    {
        if (a[i] == 0)
        {
            zero++;
        }
        if (a[i] == 2)
        {
            two++;
        }
    }

    // Find the count of required pairs
    int cnt = (zero * (zero - 1)) / 2 +
               (two * (two - 1)) / 2;

    // Return the count
    return cnt;
}

// Driver code
public static void Main(String[] args)
{
    int []a = { 2, 2, 3, 4, 2, 6 };
    int n = a.Length;

    Console.Write(sumEqualProduct(a, n));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the count
// of the required pairs
function sumEqualProduct(a, n)
{
    var zero = 0, two = 0;

    // Find the count of 0s
    // and 2s in the array
    for (var i = 0; i < n; i++) {
        if (a[i] == 0) {
            zero++;
        }
        if (a[i] == 2) {
            two++;
        }
    }

    // Find the count of required pairs
    var cnt = (zero * (zero - 1)) / 2
              + (two * (two - 1)) / 2;

    // Return the count
    return cnt;
}

// Driver code
var a = [2, 2, 3, 4, 2, 6];
var n = a.length;
document.write( sumEqualProduct(a, n));

// This code is contributed by importantly.
</script>
```

**Output:** 

```
3
```

**时间复杂度:** O(N)

**辅助空间:** O(1)