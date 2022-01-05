# 不使用 sqrt()函数的楼层平方根:递归

> 原文:[https://www . geesforgeks . org/floor-平方根-不使用-sqrt-function-recursive/](https://www.geeksforgeeks.org/floor-square-root-without-using-sqrt-function-recursive/)

给定一个数字 **N** ，任务是在不使用内置平方根函数的情况下，求数字 N 的楼层平方根。**一个数的落地平方根**是小于或等于其平方根的最大整数。

**示例:**

> **输入:** N = 25
> **输出:** 5
> **解释:**
> 25 的平方根= 5。因此，5 是小于等于 25 的平方根的最大整数。
> 
> **输入:** N = 30
> **输出:** 5
> **解释:**
> 30 的平方根= 5.47
> 因此 5 是小于等于 30(5.47)
> 平方根的最大整数

**<u>天真法:</u>**
在求一个数的落地平方根的基本方法中，求从 **1 到 N** 的数的平方，直到某个数的平方 **K** 变得大于 **N** 。因此**(K–1)**的值将是 n 的地板平方根

下面是使用朴素方法解决这个问题的算法:

*   在 k 中从数字 1 到 N 迭代一个循环
*   对于任意 K，如果它的平方变得大于 N，那么 K-1 就是 N 的地板平方根。

**时间复杂度:** O(√N)

**<u>高效逼近:</u>**
从天真逼近来看，很明显 N 的地板平方根将位于[1，N]范围内。因此，我们可以**在这个范围**内有效地搜索所需的号码，而不是检查这个范围内的每个号码。因此，想法是使用[二分搜索法](https://www.geeksforgeeks.org/binary-search/)，以便高效地找到**对数 N** 中数字 N 的楼层平方根。

下面是使用二分搜索法解决上述问题的递归算法:

*   在 0 到 n 的范围内实施二分搜索法
*   使用公式计算范围的中间值:

```
mid = (start + end) / 2
```

*   **基本情况:**递归调用将被执行，直到 mid 的平方小于或等于 N 并且(mid+1)的平方大于或等于 N

```
(mid2 ≤ N) and ((mid + 1)2 > N)
```

*   如果基本情况不满足，那么范围将相应地改变。
    *   如果 mid 的平方小于或等于 N，则范围更新为[mid + 1，end]

```
if(mid2 ≤ N)
    updated range = [mid + 1, end]
```

*   如果中间值的平方大于 N，则范围更新为[低，中间+ 1]

```
if(mid2 > N)
    updated range = [low, mid - 1]
```

下面是上述方法的实现:

## C++

```
// C++ implementation to find the
// square root of the number N
// without using sqrt() function

#include <bits/stdc++.h>
using namespace std;

// Function to find the square
// root of the number N using BS
int sqrtSearch(int low, int high, int N)
{

    // If the range is still valid
    if (low <= high) {

        // Find the mid-value of the range
        int mid = (low + high) / 2;

        // Base Case
        if ((mid * mid <= N)
            && ((mid + 1) * (mid + 1) > N)) {
            return mid;
        }

        // Condition to check if the
        // left search space is useless
        else if (mid * mid < N) {
            return sqrtSearch(mid + 1, high, N);
        }
        else {
            return sqrtSearch(low, mid - 1, N);
        }
    }
    return low;
}

// Driver Code
int main()
{
    int N = 25;
    cout << sqrtSearch(0, N, N)
         << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// square root of the number N
// without using sqrt() function
class GFG {

    // Function to find the square
    // root of the number N using BS
    static int sqrtSearch(int low, int high, int N)
    {

        // If the range is still valid
        if (low <= high) {

            // Find the mid-value of the range
            int mid = (int)(low + high) / 2;

            // Base Case
            if ((mid * mid <= N)
                && ((mid + 1) * (mid + 1) > N)) {
                return mid;
            }

            // Condition to check if the
            // left search space is useless
            else if (mid * mid < N) {
                return sqrtSearch(mid + 1, high, N);
            }
            else {
                return sqrtSearch(low, mid - 1, N);
            }
        }
        return low;
    }

    // Driver Code
    public static void main (String[] args)
    {
        int N = 25;
        System.out.println(sqrtSearch(0, N, N));
    }
}

// This code is contributed by Yash_R
```

## 蟒蛇 3

```
# Python3 implementation to find the
# square root of the number N
# without using sqrt() function

# Function to find the square
# root of the number N using BS
def sqrtSearch(low, high, N) :

    # If the range is still valid
    if (low <= high) :

        # Find the mid-value of the range
        mid = (low + high) // 2;

        # Base Case
        if ((mid * mid <= N) and ((mid + 1) * (mid + 1) > N)) :
            return mid;

        # Condition to check if the
        # left search space is useless
        elif (mid * mid < N) :
            return sqrtSearch(mid + 1, high, N);

        else :
            return sqrtSearch(low, mid - 1, N);

    return low;

# Driver Code
if __name__ == "__main__" :

    N = 25;
    print(sqrtSearch(0, N, N))

# This code is contributed by Yash_R
```

## C#

```
// C# implementation to find the
// square root of the number N
// without using sqrt() function
using System;

class GFG {

    // Function to find the square
    // root of the number N using BS
    static int sqrtSearch(int low, int high, int N)
    {

        // If the range is still valid
        if (low <= high) {

            // Find the mid-value of the range
            int mid = (int)(low + high) / 2;

            // Base Case
            if ((mid * mid <= N)
                && ((mid + 1) * (mid + 1) > N)) {
                return mid;
            }

            // Condition to check if the
            // left search space is useless
            else if (mid * mid < N) {
                return sqrtSearch(mid + 1, high, N);
            }
            else {
                return sqrtSearch(low, mid - 1, N);
            }
        }
        return low;
    }

    // Driver Code
    public static void Main(String[] args)
    {
        int N = 25;
        Console.WriteLine(sqrtSearch(0, N, N));
    }
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript implementation to find the
// square root of the number N
// without using sqrt() function

// Function to find the square
// root of the number N using BS
function sqrtSearch(low, high, N)
{

    // If the range is still valid
    if (low <= high)
    {

        // Find the mid-value of the range
        var mid = parseInt( (low + high) / 2);

        // Base Case
        if ((mid * mid <= N) &&
           ((mid + 1) * (mid + 1) > N))
        {
            return mid;
        }

        // Condition to check if the
        // left search space is useless
        else if (mid * mid < N)
        {
            return sqrtSearch(mid + 1, high, N);
        }
        else
        {
            return sqrtSearch(low, mid - 1, N);
        }
    }
    return low;
}

// Driver Code
var N = 25;

document.write(sqrtSearch(0, N, N));

// This code is contributed by todaysgaurav

</script>
```

**Output:** 

```
5
```

**性能分析:**

*   **时间复杂度:**和上面的方法一样，在 0 到 N 的搜索空间上使用了二分搜索法，在最坏的情况下需要 O(log N)时间，因此时间复杂度将是 **O(log N)** 。
*   **空间复杂度:**和上面的方法一样，考虑到递归调用中使用的堆栈空间，在最坏的情况下可以占用 O(logN)空间，因此空间复杂度为 **O(log N)**