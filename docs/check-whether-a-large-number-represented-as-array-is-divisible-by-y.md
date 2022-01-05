# 检查数组表示的大数是否可以被 Y 整除

> 原文:[https://www . geeksforgeeks . org/check-一个以数组形式表示的大数是否可被 y 整除/](https://www.geeksforgeeks.org/check-whether-a-large-number-represented-as-array-is-divisible-by-y/)

给定一个大整数 **X** 表示为一个数组 **arr[]** ，其中每个 **arr[i]** 在 **X** 中存储一个数字。任务是检查数组表示的数字是否能被给定的整数 **Y** 整除。
**举例:**

> **输入:** arr[] = {1，2，1，5，6}，Y = 4
> **输出:**是
> 12156 / 4 = 3039
> **输入:** arr[] = {1，1，1，1，1，1，1，1，1，1，Y = 14
> **输出:**否

**逼近:**从左边开始遍历给定数字的数字，取小于等于 **Y** 的最大数字，用 **Y** 除。如果余数不是 **0** 那么它将被携带到由剩余数字形成的下一个可能的数字，就像在[长除法](https://www.geeksforgeeks.org/divide-large-number-represented-string/)中一样。处理完完整的数字后，如果余数仍然不是 0，则表示的数字不能被 **Y** 整除，否则就是 0。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

// Function that returns true if the number represented
// by the given array is divisible by y
bool isDivisible(int* arr, int n, int y)
{
    int d = 0, i = 0;

    // While there are digits left
    while (i < n) {

        // Select the next part of the number
        // i.e. the maximum number which is <= y
        while (d < y && i < n)
            d = d * 10 + arr[i++];

        // Get the current remainder
        d = d % y;
    }

    // If the final remainder is 0
    if (d == 0)
        return true;
    return false;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 1, 5, 6 };
    int x = sizeof(arr) / sizeof(int);
    int y = 4;

    cout << (isDivisible(arr, x, y) ? "Yes" : "No");

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    // Function that returns true if the number represented
    // by the given array is divisible by y
    static boolean isDivisible(int [] arr, int n, int y)
    {
        int d = 0, i = 0;

        // While there are digits left
        while (i < n)
        {

            // Select the next part of the number
            // i.e. the maximum number which is <= y
            while (d < y && i < n)
                d = d * 10 + arr[i++];

            // Get the current remainder
            d = d % y;
        }

        // If the final remainder is 0
        if (d == 0)
            return true;
        return false;
    }

    // Driver code
    public static void main (String[] args)
    {

        int [] arr = { 1, 2, 1, 5, 6 };
        int x = arr.length;
        int y = 4;

        System.out.println(isDivisible(arr, x, y) ? "Yes" : "No");
    }
}

// This code is contributed by ihritik
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that returns true if the number represented
# by the given array is divisible by y
def isDivisible(arr, n, y):
    d, i = 0, 0

    # While there are digits left
    while i < n:

        # Select the next part of the number
        # i.e. the maximum number which is <= y
        while d < y and i < n:
            d = d * 10 + arr[i]
            i += 1

        # Get the current remainder
        d = d % y

    # If the final remainder is 0
    if d == 0:
        return True
    return False

# Driver code
if __name__ == "__main__":
    arr = [ 1, 2, 1, 5, 6 ]
    x = len(arr)
    y = 4
    if (isDivisible(arr, x, y)):
        print("Yes")
    else:
        print("No")

# This code is contributed by
# sanjeev2552
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function that returns true if the number represented
    // by the given array is divisible by y
    static bool isDivisible(int [] arr, int n, int y)
    {
        int d = 0, i = 0;

        // While there are digits left
        while (i < n)
        {

            // Select the next part of the number
            // i.e. the maximum number which is <= y
            while (d < y && i < n)
                d = d * 10 + arr[i++];

            // Get the current remainder
            d = d % y;
        }

        // If the final remainder is 0
        if (d == 0)
            return true;
        return false;
    }

    // Driver code
    public static void Main ()
    {

        int [] arr = { 1, 2, 1, 5, 6 };
        int x = arr.Length;
        int y = 4;

        Console.WriteLine(isDivisible(arr, x, y) ? "Yes" : "No");
    }
}

// This code is contributed by ihritik
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function that returns true if the number represented
// by the given array is divisible by y
function isDivisible(vararr , n , y)
{
    var d = 0, i = 0;

    // While there are digits left
    while (i < n)
    {

        // Select the next part of the number
        // i.e. the maximum number which is <= y
        while (d < y && i < n)
            d = d * 10 + arr[i++];

        // Get the current remainder
        d = d % y;
    }

    // If the final remainder is 0
    if (d == 0)
        return true;
    return false;
}

// Driver code
var  arr = [ 1, 2, 1, 5, 6 ];
var x = arr.length;
var y = 4;

document.write(isDivisible(arr, x, y) ? "Yes" : "No");

// This code is contributed by 29AjayKumar

</script>
```

**Output:** 

```
Yes
```