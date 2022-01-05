# 检查给定数组的所有元素是否可以通过成对递减值而变为 0

> 原文:[https://www . geeksforgeeks . org/check-如果给定数组的所有元素都可以通过成对递减值 0 来生成/](https://www.geeksforgeeks.org/check-if-all-elements-of-the-given-array-can-be-made-0-by-decrementing-value-in-pairs/)

给定一个由正整数组成的数组 **arr[]** ，任务是通过执行以下操作检查给定数组的所有元素是否都可以为 0:

*   选择两个指数 **i** 和 **j** ，这样 **i！= j** 并从 arr[i]和 arr[j]中减去 1
*   上述操作可以执行任何次数

**例:**

> **输入:** arr[] = {1，2，3，4}
> **输出:**是
> **说明:**
> 首先选择值 2 和 4，执行上述操作 2 次。然后数组变成 1 0 3 2。
> 现在选择 1 和 3，应用上述操作一次，得到 0 0 2 2。
> 现在选择两个 2s，执行上述操作两次。
> 最后数组变成 0 0 0 0。
> **输入:** arr[] = {5，5，5，5，5}
> **输出:**否

**做法:**在仔细观察问题时，可以观察到，如果只有 1 个元素或者所有元素之和为奇数，那么不可能使所有元素都为 0。因为在每次迭代中，从所有元素的和中减去 2，因此，只有当数组中所有元素的和为偶数时，数组才能变成 0。此外，当数组中最大的数字小于或等于剩余元素的总和时，可以使数组为 0。
以下是上述办法的实施情况:

## C++

```
// C++ program to make the array zero
// by decrementing value in pairs

#include <bits/stdc++.h>
using namespace std;

// Function to check if all the elements
// can be made 0 in an array
void canMake(int n, int ar[])
{

    // Variable to store
    // sum and maximum element
    // in an array
    int sum = 0, maxx = -1;

    // Loop to calculate the sum and max value
    // of the given array
    for (int i = 0; i < n; i++) {
        sum += ar[i];
        maxx = max(maxx, ar[i]);
    }

    // If n is 1 or sum is odd or
    // sum - max element < max
    // then no solution
    if (n == 1 || sum % 2 == 1
        || sum - maxx < maxx) {
        cout << "No\n";
    }
    else {

        // For the remaining case, print Yes
        cout << "Yes\n";
    }
}

// Driver code
int main()
{

    int n = 6;
    int arr[] = { 1, 1, 2, 3, 6, 11 };

    canMake(n, arr);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to make the array zero
// by decrementing value in pairs
class GFG
{

// Function to check if all the elements
// can be made 0 in an array
static void canMake(int n, int ar[])
{

    // Variable to store
    // sum and maximum element
    // in an array
    int sum = 0, maxx = -1;

    // Loop to calculate the sum and max value
    // of the given array
    for (int i = 0; i < n; i++)
    {
        sum += ar[i];
        maxx = Math.max(maxx, ar[i]);
    }

    // If n is 1 or sum is odd or
    // sum - max element < max
    // then no solution
    if (n == 1 || sum % 2 == 1
        || sum - maxx < maxx)
    {
        System.out.print("No\n");
    }
    else
    {

        // For the remaining case, print Yes
        System.out.print("Yes\n");
    }
}

// Driver code
public static void main(String[] args)
{

    int n = 6;
    int arr[] = { 1, 1, 2, 3, 6, 11 };

    canMake(n, arr);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to make the array zero
# by decrementing value in pairs

# Function to check if all the elements
# can be made 0 in an array
def canMake(n, ar) :

    # Variable to store
    # sum and maximum element
    # in an array
    sum = 0; maxx = -1;

    # Loop to calculate the sum and max value
    # of the given array
    for i in range(n) :
        sum += ar[i];
        maxx = max(maxx, ar[i]);

    # If n is 1 or sum is odd or
    # sum - max element < max
    # then no solution
    if (n == 1 or sum % 2 == 1
        or sum - maxx < maxx) :
        print("No");

    else :

        # For the remaining case, print Yes
        print("Yes");

# Driver code
if __name__ == "__main__" :

    n = 6;
    arr = [ 1, 1, 2, 3, 6, 11 ];

    canMake(n, arr);

# This code is contributed by AnkitRai01
```

## C#

```
// C# program to make the array zero
// by decrementing value in pairs
using System;

class GFG
{

// Function to check if all the elements
// can be made 0 in an array
static void canMake(int n, int []ar)
{

    // Variable to store
    // sum and maximum element
    // in an array
    int sum = 0, maxx = -1;

    // Loop to calculate the sum and max value
    // of the given array
    for (int i = 0; i < n; i++)
    {
        sum += ar[i];
        maxx = Math.Max(maxx, ar[i]);
    }

    // If n is 1 or sum is odd or
    // sum - max element < max
    // then no solution
    if (n == 1 || sum % 2 == 1
        || sum - maxx < maxx)
    {
        Console.Write("No\n");
    }
    else
    {

        // For the remaining case, print Yes
        Console.Write("Yes\n");
    }
}

// Driver code
public static void Main(String[] args)
{

    int n = 6;
    int []arr = { 1, 1, 2, 3, 6, 11 };

    canMake(n, arr);
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript program to make the array zero
// by decrementing value in pairs

// Function to check if all the elements
// can be made 0 in an array
function canMake(n, ar)
{

    // Variable to store
    // sum and maximum element
    // in an array
    var sum = 0, maxx = -1;

    // Loop to calculate the sum and max value
    // of the given array
    for (var i = 0; i < n; i++) {
        sum += ar[i];
        maxx = Math.max(maxx, ar[i]);
    }

    // If n is 1 or sum is odd or
    // sum - max element < max
    // then no solution
    if (n == 1 || sum % 2 == 1
        || sum - maxx < maxx) {
        document.write( "No");
    }
    else {

        // For the remaining case, print Yes
        document.write( "Yes");
    }
}

// Driver code
var n = 6;
var arr = [1, 1, 2, 3, 6, 11];
canMake(n, arr);

</script>
```

**Output:** 

```
Yes
```