# L 至 R 范围内第 k 个最小偶数

> 原文:[https://www . geeksforgeeks . org/kth-最小范围偶数-l 到-r/](https://www.geeksforgeeks.org/kth-smallest-even-number-in-range-l-to-r/)

给定两个变量 **L** 和 **R** ，表示从 **L** 到 **R** 的整数范围，以及一个数字 **K** ，任务是找到 **Kth** 最小的偶数。如果 **K** 大于 **L** 至 **R** 范围内的偶数，则返回-1。**LLONG _ MIN<= L<= R<=****LLONG _ MAX**。

**示例**:

> **输入** : L = 3，R = 9，K = 3
> **输出** : 8
> **说明**:范围内的偶数是 4、6、8，第三个最小的偶数是 8
> 
> **输入** : L = -3，R = 3，K = 2
> 输出 : 0

**天真做法:**基本思路是从 L 到 R 遍历数字，然后打印第 k 个偶数。

***时间复杂度*** : O(R-L)
***辅助空间*** : O(1)

**逼近**:利用基础数学，利用 [cmath 库](https://www.geeksforgeeks.org/c-mathematical-functions/)的天花板和地板，可以解决给定的问题。想法是检查 **L** 是奇数还是偶数，并据此计算出最小的偶数。以下步骤可用于解决问题:

*   如果 **K < =0** ，则返回 **-1**
*   初始化**计数**计算范围内的偶数个数
*   如果 **L** 是奇数
    *   **计数=楼层((浮动)(R-L+1)/2)**
    *   如果 **K >计数**返回 **-1**
    *   否则返回**(L+2 * K–1)**
*   如果 **R** 为偶数
    *   **计数=上限((浮动)(R-L+1)/2)**
    *   如果 **K >计数**返回 **-1**
    *   否则返回**(L+2 * K–2)**

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <cmath>
#include <iostream>
#define ll long long
using namespace std;

// Function to return Kth smallest
// even number if it exists
ll findEven(ll L, ll R, ll K)
{

    // Base Case
    if (K <= 0)
        return -1;

    if (L % 2) {

        // Calculate count of even numbers
        // within the range
        ll Count = floor((float)(R - L + 1) / 2);

        // if k > range then kth smallest
        // even number is not in this range
        // then return -1
        return (K > Count) ? -1 : (L + 2 * K - 1);
    }

    else {
        // Calculate count of even numbers
        // within the range

        ll Count = ceil((float)(R - L + 1) / 2);

        // if k > range then kth smallest
        // even number is not in this range
        // then return -1
        return (K > Count) ? -1 : (L + 2 * K - 2);
    }
}

// Driver Code
int main()
{
    ll L = 3, R = 9, K = 3;

    cout << findEven(L, R, K);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
public class GFG
{
// Function to return Kth smallest
// even number if it exists
static long findEven(long L, long R, long K)
{

    // Base Case
    if (K <= 0)
        return -1;

    if (L % 2 == 1) {

        // Calculate count of even numbers
        // within the range
        long Count = (int)Math.floor((float)(R - L + 1) / 2);

        // if k > range then kth smallest
        // even number is not in this range
        // then return -1
        return (K > Count) ? -1 : (L + 2 * K - 1);
    }

    else {
        // Calculate count of even numbers
        // within the range

        long Count = (int)Math.ceil((float)(R - L + 1) / 2);

        // if k > range then kth smallest
        // even number is not in this range
        // then return -1
        return (K > Count) ? -1 : (L + 2 * K - 2);
    }
}

// Driver Code
public static void main(String args[])
{
    long L = 3, R = 9, K = 3;

    System.out.println(findEven(L, R, K));

}
}
// This code is contributed by Samim Hossain Mondal.
```

## 蟒蛇 3

```
# Python program for the above approach

# Function to return Kth smallest
# even number if it exists
def findEven(L, R, K):

    # Base Case
    if (K <= 0):
        return -1

    if (L % 2):

        # Calculate count of even numbers
        # within the range
        Count = (R - L + 1) // 2

        # if k > range then kth smallest
        # even number is not in this range
        # then return -1
        return -1 if (K > Count) else (L + 2 * K - 1)

    else:
        # Calculate count of even numbers
        # within the range

        Count = (R - L + 1) // 2

        # if k > range then kth smallest
        # even number is not in this range
        # then return -1
        return -1 if (K > Count) else (L + 2 * K - 2)

# Driver Code
L = 3
R = 9
K = 3

print(findEven(L, R, K))

# This code is contributed by Saurabh Jaiswal
```

## C#

```
// C# program for the above approach
using System;
class GFG
{
// Function to return Kth smallest
// even number if it exists
static long findEven(long L, long R, long K)
{

    // Base Case
    if (K <= 0)
        return -1;

    if (L % 2 == 1) {

        // Calculate count of even numbers
        // within the range
        long Count = (int)Math.Floor((float)(R - L + 1) / 2);

        // if k > range then kth smallest
        // even number is not in this range
        // then return -1
        return (K > Count) ? -1 : (L + 2 * K - 1);
    }

    else {
        // Calculate count of even numbers
        // within the range

        long Count = (int)Math.Ceiling((float)(R - L + 1) / 2);

        // if k > range then kth smallest
        // even number is not in this range
        // then return -1
        return (K > Count) ? -1 : (L + 2 * K - 2);
    }
}

// Driver Code
public static void Main()
{
    long L = 3, R = 9, K = 3;

    Console.Write(findEven(L, R, K));

}
}
// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to return Kth smallest
// even number if it exists
function findEven(L, R, K)
{

    // Base Case
    if (K <= 0)
        return -1;

    if (L % 2) {

        // Calculate count of even numbers
        // within the range
        let Count = Math.floor((R - L + 1) / 2);

        // if k > range then kth smallest
        // even number is not in this range
        // then return -1
        return (K > Count) ? -1 : (L + 2 * K - 1);
    }

    else {
        // Calculate count of even numbers
        // within the range

        let Count = Math.ceil((float)(R - L + 1) / 2);

        // if k > range then kth smallest
        // even number is not in this range
        // then return -1
        return (K > Count) ? -1 : (L + 2 * K - 2);
    }
}

// Driver Code
let L = 3, R = 9, K = 3;

document.write(findEven(L, R, K));

// This code is contributed by Samim Hossain Mondal.
</script>
```

**Output**

```
8
```

***时间复杂度*** : O(1)
***辅助空间*** : O(1)