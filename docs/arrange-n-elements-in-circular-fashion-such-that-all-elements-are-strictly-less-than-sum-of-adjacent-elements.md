# 以圆形方式排列 N 个元素，使得所有元素严格小于相邻元素的总和

> 原文:[https://www . geesforgeks . org/array-n-elements-in-circular-fashion-这样-所有元素-严格来说-都小于相邻元素的和/](https://www.geeksforgeeks.org/arrange-n-elements-in-circular-fashion-such-that-all-elements-are-strictly-less-than-sum-of-adjacent-elements/)

给定一个由 **N 个**整数组成的数组，任务是以一种**圆形**排列方式排列它们，使得元素严格小于其相邻元素的和。如果这样的安排是不可能的，那么打印 **-1** 。
**注意**可以有多种排列元素的方式，以满足条件，任务是找到任何这样的排列。
**举例:**

> **输入:** arr[] = {1，4，4，3，2 }
> T3】输出:1 3 4 4 2
> arr[0]= 1<(2+3)
> arr[1]= 4<(1+4)
> arr[2]= 4<(4+3)
> arr[3]= 3<(4+2)
> arr[4]= 2<(3+3)

**方法:**这个问题可以用贪婪的方法来解决，我们首先对数组进行排序，然后将最小的元素放在开头，第二个最小的放在末尾，第三个最小的放在第二个位置，第四个最小的放在另一个数组的倒数第二个位置。一旦安排完成，检查给定的条件是否满足。
以下是上述办法的实施情况:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the arrangement that
// satisifes the given condition
void printArrangement(int a[], int n)
{

    // Sort the array initially
    sort(a, a + n);

    // Array that stores the arrangement
    int b[n];

    // Once the array is sorted
    // Re-fill the array again in the
    // mentioned way in the approach
    int low = 0, high = n - 1;
    for (int i = 0; i < n; i++) {
        if (i % 2 == 0)
            b[low++] = a[i];
        else
            b[high--] = a[i];
    }

    // Iterate in the array
    // and check if the arrangement made
    // satisfies the given condition or not
    for (int i = 0; i < n; i++) {

        // For the first element
        // the adjacents will be a[1] and a[n-1]
        if (i == 0) {
            if (b[n - 1] + b[1] <= b[i]) {
                cout << -1;
                return;
            }
        }

        // For the last element
        // the adjacents will be a[0] and a[n-2]
        else if (i == (n - 1)) {
            if (b[n - 2] + b[0] <= b[i]) {
                cout << -1;
                return;
            }
        }
        else {
            if (b[i - 1] + b[i + 1] <= b[i]) {
                cout << -1;
                return;
            }
        }
    }

    // If we reach this position then
    // the arrangement is possible
    for (int i = 0; i < n; i++)
        cout << b[i] << " ";
}

// Driver code
int main()
{
    int a[] = { 1, 4, 4, 3, 2 };
    int n = sizeof(a) / sizeof(a[0]);

    printArrangement(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.Arrays;

class GFG
{

// Function to print the arrangement that
// satisifes the given condition
static void printArrangement(int a[], int n)
{

    // Sort the array initially
    Arrays.sort(a);

    // Array that stores the arrangement
    int b[] = new int[n];

    // Once the array is sorted
    // Re-fill the array again in the
    // mentioned way in the approach
    int low = 0, high = n - 1;
    for (int i = 0; i < n; i++)
    {
        if (i % 2 == 0)
            b[low++] = a[i];
        else
            b[high--] = a[i];
    }

    // Iterate in the array
    // and check if the arrangement made
    // satisfies the given condition or not
    for (int i = 0; i < n; i++)
    {

        // For the first element
        // the adjacents will be a[1] and a[n-1]
        if (i == 0)
        {
            if (b[n - 1] + b[1] <= b[i])
            {
                System.out.print(-1);
                return;
            }
        }

        // For the last element
        // the adjacents will be a[0] and a[n-2]
        else if (i == (n - 1))
        {
            if (b[n - 2] + b[0] <= b[i])
            {
                System.out.print(-1);
                return;
            }
        }
        else
        {
            if (b[i - 1] + b[i + 1] <= b[i])
            {
                System.out.print(-1);
                return;
            }
        }
    }

    // If we reach this position then
    // the arrangement is possible
    for (int i = 0; i < n; i++)
        System.out.print(b[i] + " ");
}

// Driver code
public static void main (String[] args)
{
    int a[] = { 1, 4, 4, 3, 2 };
    int n = a.length;

    printArrangement(a, n);
}
}

// This code is contributed by anuj_67..
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to print the arrangement that
# satisifes the given condition
def printArrangement(a, n):

    # Sort the array initially
    a = sorted(a)

    # Array that stores the arrangement
    b = [0 for i in range(n)]

    # Once the array is sorted
    # Re-fill the array again in the
    # mentioned way in the approach
    low = 0
    high = n - 1
    for i in range(n):
        if (i % 2 == 0):
            b[low] = a[i]
            low += 1
        else:
            b[high] = a[i]
            high -= 1

    # Iterate in the array
    # and check if the arrangement made
    # satisfies the given condition or not
    for i in range(n):

        # For the first element
        # the adjacents will be a[1] and a[n-1]
        if (i == 0):
            if (b[n - 1] + b[1] <= b[i]):
                print("-1")
                return

        # For the last element
        # the adjacents will be a[0] and a[n-2]
        elif (i == (n - 1)) :
            if (b[n - 2] + b[0] <= b[i]):
                print("-1")
                return

        else:
            if (b[i - 1] + b[i + 1] <= b[i]):
                print("-1")
                return

    # If we reach this position then
    # the arrangement is possible
    for i in range(n):
        print(b[i], end = " ")

# Driver code
a = [ 1, 4, 4, 3, 2 ]
n = len(a)

printArrangement(a, n)

# This code is contributed by Mohit Kumar
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function to print the arrangement that
// satisifes the given condition
static void printArrangement(int []a, int n)
{

    // Sort the array initially
    Array.Sort(a);

    // Array that stores the arrangement
    int []b = new int[n];

    // Once the array is sorted
    // Re-fill the array again in the
    // mentioned way in the approach
    int low = 0, high = n - 1;
    for (int i = 0; i < n; i++)
    {
        if (i % 2 == 0)
            b[low++] = a[i];
        else
            b[high--] = a[i];
    }

    // Iterate in the array
    // and check if the arrangement made
    // satisfies the given condition or not
    for (int i = 0; i < n; i++)
    {

        // For the first element
        // the adjacents will be a[1] and a[n-1]
        if (i == 0)
        {
            if (b[n - 1] + b[1] <= b[i])
            {
                Console.Write(-1);
                return;
            }
        }

        // For the last element
        // the adjacents will be a[0] and a[n-2]
        else if (i == (n - 1))
        {
            if (b[n - 2] + b[0] <= b[i])
            {
                Console.Write(-1);
                return;
            }
        }
        else
        {
            if (b[i - 1] + b[i + 1] <= b[i])
            {
                Console.Write(-1);
                return;
            }
        }
    }

    // If we reach this position then
    // the arrangement is possible
    for (int i = 0; i < n; i++)
        Console.Write(b[i] + " ");
}

// Driver code
public static void Main ()
{
    int []a = { 1, 4, 4, 3, 2 };
    int n = a.Length;

    printArrangement(a, n);
}
}

// This code is contributed by anuj_67..
```

## java 描述语言

```
<script>
// javascript implementation of the approach

    // Function to print the arrangement that
    // satisifes the given condition
    function printArrangement(a, n)
    {

        // Sort the array initially
        a.sort();

        // Array that stores the arrangement
        var b = Array(n).fill(0);

        // Once the array is sorted
        // Re-fill the array again in the
        // mentioned way in the approach
        var low = 0, high = n - 1;
        for (i = 0; i < n; i++) {
            if (i % 2 == 0)
                b[low++] = a[i];
            else
                b[high--] = a[i];
        }

        // Iterate in the array
        // and check if the arrangement made
        // satisfies the given condition or not
        for (i = 0; i < n; i++) {

            // For the first element
            // the adjacents will be a[1] and a[n-1]
            if (i == 0) {
                if (b[n - 1] + b[1] <= b[i]) {
                    document.write(-1);
                    return;
                }
            }

            // For the last element
            // the adjacents will be a[0] and a[n-2]
            else if (i == (n - 1)) {
                if (b[n - 2] + b[0] <= b[i]) {
                    document.write(-1);
                    return;
                }
            } else {
                if (b[i - 1] + b[i + 1] <= b[i]) {
                    document.write(-1);
                    return;
                }
            }
        }

        // If we reach this position then
        // the arrangement is possible
        for (i = 0; i < n; i++)
            document.write(b[i] + " ");
    }

    // Driver code
        var a = [ 1, 4, 4, 3, 2 ];
        var n = a.length;

        printArrangement(a, n);

// This code is contributed by todaysgaurav
</script>
```

**Output:** 

```
1 3 4 4 2
```

**时间复杂度:**O(N log N)
T3】辅助空间: O(n)