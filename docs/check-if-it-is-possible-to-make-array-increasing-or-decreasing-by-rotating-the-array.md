# 检查是否可以通过旋转阵列

来增加或减少阵列

> 原文:[https://www . geesforgeks . org/check-如果有可能通过旋转阵列来增加或减少阵列数量/](https://www.geeksforgeeks.org/check-if-it-is-possible-to-make-array-increasing-or-decreasing-by-rotating-the-array/)

给定一个由 **N** 个不同元素组成的数组 **arr[]** ，任务是检查是否可以通过在任何方向旋转数组来增加或减少数组。
**例:**

> **输入:** arr[] = {4，5，6，2，3}
> **输出:**是
> 数组可以旋转为{2，3，4，5，6}
> **输入:** arr[] = {1，2，4，3，5}
> **输出:**否

**进场:**有四种可能:

*   如果数组**已经在增加**，那么答案是**是**。
*   如果数组**已经在减少**，那么答案是**是**。
*   如果可以使数组增加，那么如果给定的数组首先增加到最大元素，然后减少，这是可能的。
*   如果可以使数组递减，那么如果给定的数组先递减到最小元素，然后递增，这是可能的。

如果无法增加或减少阵列，则打印**否**。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if the array
// can be made increasing or decreasing
// after rotating it in any direction
bool isPossible(int a[], int n)
{
    // If size of the array is less than 3
    if (n <= 2)
        return true;

    int flag = 0;
    // Check if the array is already decreasing
    for (int i = 0; i < n - 2; i++) {
        if (!(a[i] > a[i + 1] and a[i + 1] > a[i + 2])) {
            flag = 1;
            break;
        }
    }

    // If the array is already decreasing
    if (flag == 0)
        return true;

    flag = 0;
    // Check if the array is already increasing
    for (int i = 0; i < n - 2; i++) {
        if (!(a[i] < a[i + 1] and a[i + 1] < a[i + 2])) {
            flag = 1;
            break;
        }
    }

    // If the array is already increasing
    if (flag == 0)
        return true;

    // Find the indices of the minimum
    // and the maximum value
    int val1 = INT_MAX, mini = -1, val2 = INT_MIN, maxi;
    for (int i = 0; i < n; i++) {
        if (a[i] < val1) {
            mini = i;
            val1 = a[i];
        }
        if (a[i] > val2) {
            maxi = i;
            val2 = a[i];
        }
    }

    flag = 1;
    // Check if we can make array increasing
    for (int i = 0; i < maxi; i++) {
        if (a[i] > a[i + 1]) {
            flag = 0;
            break;
        }
    }

    // If the array is increasing upto max index
    // and minimum element is right to maximum
    if (flag == 1 and maxi + 1 == mini) {
        flag = 1;
        // Check if array increasing again or not
        for (int i = mini; i < n - 1; i++) {
            if (a[i] > a[i + 1]) {
                flag = 0;
                break;
            }
        }
        if (flag == 1)
            return true;
    }

    flag = 1;
    // Check if we can make array decreasing
    for (int i = 0; i < mini; i++) {
        if (a[i] < a[i + 1]) {
            flag = 0;
            break;
        }
    }

    // If the array is decreasing upto min index
    // and minimum element is left to maximum
    if (flag == 1 and maxi - 1 == mini) {
        flag = 1;

        // Check if array decreasing again or not
        for (int i = maxi; i < n - 1; i++) {
            if (a[i] < a[i + 1]) {
                flag = 0;
                break;
            }
        }
        if (flag == 1)
            return true;
    }

    // If it is not possible to make the
    // array increasing or decreasing
    return false;
}

// Driver code
int main()
{
    int a[] = { 4, 5, 6, 2, 3 };
    int n = sizeof(a) / sizeof(a[0]);

    if (isPossible(a, n))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

// Function that returns true if the array
// can be made increasing or decreasing
// after rotating it in any direction
static boolean isPossible(int a[], int n)
{
    // If size of the array is less than 3
    if (n <= 2)
        return true;

    int flag = 0;

    // Check if the array is already decreasing
    for (int i = 0; i < n - 2; i++)
    {
        if (!(a[i] > a[i + 1] &&
              a[i + 1] > a[i + 2]))
        {
            flag = 1;
            break;
        }
    }

    // If the array is already decreasing
    if (flag == 0)
        return true;

    flag = 0;

    // Check if the array is already increasing
    for (int i = 0; i < n - 2; i++)
    {
        if (!(a[i] < a[i + 1] &&
              a[i + 1] < a[i + 2]))
        {
            flag = 1;
            break;
        }
    }

    // If the array is already increasing
    if (flag == 0)
        return true;

    // Find the indices of the minimum
    // && the maximum value
    int val1 = Integer.MAX_VALUE, mini = -1,
        val2 = Integer.MIN_VALUE, maxi = 0;
    for (int i = 0; i < n; i++)
    {
        if (a[i] < val1)
        {
            mini = i;
            val1 = a[i];
        }
        if (a[i] > val2)
        {
            maxi = i;
            val2 = a[i];
        }
    }

    flag = 1;

    // Check if we can make array increasing
    for (int i = 0; i < maxi; i++)
    {
        if (a[i] > a[i + 1])
        {
            flag = 0;
            break;
        }
    }

    // If the array is increasing upto max index
    // && minimum element is right to maximum
    if (flag == 1 && maxi + 1 == mini)
    {
        flag = 1;

        // Check if array increasing again or not
        for (int i = mini; i < n - 1; i++)
        {
            if (a[i] > a[i + 1])
            {
                flag = 0;
                break;
            }
        }
        if (flag == 1)
            return true;
    }

    flag = 1;

    // Check if we can make array decreasing
    for (int i = 0; i < mini; i++)
    {
        if (a[i] < a[i + 1])
        {
            flag = 0;
            break;
        }
    }

    // If the array is decreasing upto min index
    // && minimum element is left to maximum
    if (flag == 1 && maxi - 1 == mini)
    {
        flag = 1;

        // Check if array decreasing again or not
        for (int i = maxi; i < n - 1; i++)
        {
            if (a[i] < a[i + 1])
            {
                flag = 0;
                break;
            }
        }
        if (flag == 1)
            return true;
    }

    // If it is not possible to make the
    // array increasing or decreasing
    return false;
}

// Driver code
public static void main(String args[])
{
    int a[] = { 4, 5, 6, 2, 3 };
    int n = a.length;

    if (isPossible(a, n))
        System.out.println( "Yes");
    else
        System.out.println( "No");
}
}

// This code is contributed by Arnab Kundu
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import sys

# Function that returns True if the array
# can be made increasing or decreasing
# after rotating it in any direction
def isPossible(a, n):

    # If size of the array is less than 3
    if (n <= 2):
        return True;

    flag = 0;

    # Check if the array is already decreasing
    for i in range(n - 2):
        if (not(a[i] > a[i + 1] and
                a[i + 1] > a[i + 2])):
            flag = 1;
            break;

    # If the array is already decreasing
    if (flag == 0):
        return True;

    flag = 0;

    # Check if the array is already increasing
    for i in range(n - 2):
        if (not(a[i] < a[i + 1] and
                a[i + 1] < a[i + 2])):
            flag = 1;
            break;

    # If the array is already increasing
    if (flag == 0):
        return True;

    # Find the indices of the minimum
    # and the maximum value
    val1 = sys.maxsize; mini = -1;
    val2 = -sys.maxsize; maxi = -1;
    for i in range(n):
        if (a[i] < val1):
            mini = i;
            val1 = a[i];

        if (a[i] > val2):
            maxi = i;
            val2 = a[i];

    flag = 1;

    # Check if we can make array increasing
    for i in range(maxi):
        if (a[i] > a[i + 1]):
            flag = 0;
            break;

    # If the array is increasing upto max index
    # and minimum element is right to maximum
    if (flag == 1 and maxi + 1 == mini):
        flag = 1;

        # Check if array increasing again or not
        for i in range(mini, n - 1):
            if (a[i] > a[i + 1]):
                flag = 0;
                break;

        if (flag == 1):
            return True;

    flag = 1;

    # Check if we can make array decreasing
    for i in range(mini):
        if (a[i] < a[i + 1]):
            flag = 0;
            break;

    # If the array is decreasing upto min index
    # and minimum element is left to maximum
    if (flag == 1 and maxi - 1 == mini):
        flag = 1;

        # Check if array decreasing again or not
        for i in range(maxi, n - 1):
            if (a[i] < a[i + 1]):
                flag = 0;
                break;

        if (flag == 1):
            return True;

    # If it is not possible to make the
    # array increasing or decreasing
    return False;

# Driver code
a = [ 4, 5, 6, 2, 3 ];
n = len(a);

if (isPossible(a, n)):
    print("Yes");
else:
    print("No");

# This code is contributed by Rajput-Ji
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function that returns true if the array
    // can be made increasing or decreasing
    // after rotating it in any direction
    static bool isPossible(int []a, int n)
    {
        // If size of the array is less than 3
        if (n <= 2)
            return true;

        int flag = 0;

        // Check if the array is already decreasing
        for (int i = 0; i < n - 2; i++)
        {
            if (!(a[i] > a[i + 1] &&
                  a[i + 1] > a[i + 2]))
            {
                flag = 1;
                break;
            }
        }

        // If the array is already decreasing
        if (flag == 0)
            return true;

        flag = 0;

        // Check if the array is already increasing
        for (int i = 0; i < n - 2; i++)
        {
            if (!(a[i] < a[i + 1] &&
                  a[i + 1] < a[i + 2]))
            {
                flag = 1;
                break;
            }
        }

        // If the array is already increasing
        if (flag == 0)
            return true;

        // Find the indices of the minimum
        // && the maximum value
        int val1 = int.MaxValue, mini = -1,
            val2 = int.MinValue, maxi = 0;
        for (int i = 0; i < n; i++)
        {
            if (a[i] < val1)
            {
                mini = i;
                val1 = a[i];
            }
            if (a[i] > val2)
            {
                maxi = i;
                val2 = a[i];
            }
        }

        flag = 1;

        // Check if we can make array increasing
        for (int i = 0; i < maxi; i++)
        {
            if (a[i] > a[i + 1])
            {
                flag = 0;
                break;
            }
        }

        // If the array is increasing upto max index
        // && minimum element is right to maximum
        if (flag == 1 && maxi + 1 == mini)
        {
            flag = 1;

            // Check if array increasing again or not
            for (int i = mini; i < n - 1; i++)
            {
                if (a[i] > a[i + 1])
                {
                    flag = 0;
                    break;
                }
            }
            if (flag == 1)
                return true;
        }

        flag = 1;

        // Check if we can make array decreasing
        for (int i = 0; i < mini; i++)
        {
            if (a[i] < a[i + 1])
            {
                flag = 0;
                break;
            }
        }

        // If the array is decreasing upto min index
        // && minimum element is left to maximum
        if (flag == 1 && maxi - 1 == mini)
        {
            flag = 1;

            // Check if array decreasing again or not
            for (int i = maxi; i < n - 1; i++)
            {
                if (a[i] < a[i + 1])
                {
                    flag = 0;
                    break;
                }
            }
            if (flag == 1)
                return true;
        }

        // If it is not possible to make the
        // array increasing or decreasing
        return false;
    }

    // Driver code
    public static void Main()
    {
        int []a = { 4, 5, 6, 2, 3 };
        int n = a.Length;

        if (isPossible(a, n))
            Console.WriteLine( "Yes");
        else
            Console.WriteLine( "No");
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>
// javascript implementation of the approach   
// Function that returns true if the array
    // can be made increasing or decreasing
    // after rotating it in any direction
    function isPossible(a , n) {
        // If size of the array is less than 3
        if (n <= 2)
            return true;

        var flag = 0;

        // Check if the array is already decreasing
        for (i = 0; i < n - 2; i++) {
            if (!(a[i] > a[i + 1] && a[i + 1] > a[i + 2])) {
                flag = 1;
                break;
            }
        }

        // If the array is already decreasing
        if (flag == 0)
            return true;

        flag = 0;

        // Check if the array is already increasing
        for (i = 0; i < n - 2; i++) {
            if (!(a[i] < a[i + 1] && a[i + 1] < a[i + 2])) {
                flag = 1;
                break;
            }
        }

        // If the array is already increasing
        if (flag == 0)
            return true;

        // Find the indices of the minimum
        // && the maximum value
        var val1 = Number.MAX_VALUE, mini = -1, val2 = Number.MIN_VALUE, maxi = 0;
        for (i = 0; i < n; i++) {
            if (a[i] < val1) {
                mini = i;
                val1 = a[i];
            }
            if (a[i] > val2) {
                maxi = i;
                val2 = a[i];
            }
        }

        flag = 1;

        // Check if we can make array increasing
        for (i = 0; i < maxi; i++) {
            if (a[i] > a[i + 1]) {
                flag = 0;
                break;
            }
        }

        // If the array is increasing upto max index
        // && minimum element is right to maximum
        if (flag == 1 && maxi + 1 == mini) {
            flag = 1;

            // Check if array increasing again or not
            for (i = mini; i < n - 1; i++) {
                if (a[i] > a[i + 1]) {
                    flag = 0;
                    break;
                }
            }
            if (flag == 1)
                return true;
        }

        flag = 1;

        // Check if we can make array decreasing
        for (i = 0; i < mini; i++) {
            if (a[i] < a[i + 1]) {
                flag = 0;
                break;
            }
        }

        // If the array is decreasing upto min index
        // && minimum element is left to maximum
        if (flag == 1 && maxi - 1 == mini) {
            flag = 1;

            // Check if array decreasing again or not
            for (i = maxi; i < n - 1; i++) {
                if (a[i] < a[i + 1]) {
                    flag = 0;
                    break;
                }
            }
            if (flag == 1)
                return true;
        }

        // If it is not possible to make the
        // array increasing or decreasing
        return false;
    }

    // Driver code

        var a = [ 4, 5, 6, 2, 3 ];
        var n = a.length;

        if (isPossible(a, n))
            document.write("Yes");
        else
            document.write("No");

// This code contributed by umadevi9616
</script>
```

**Output**

```
Yes
```

**时间复杂度:** O(N)

**辅助空间:** O(1)