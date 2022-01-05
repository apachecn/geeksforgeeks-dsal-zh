# 通过重复减去相邻数字将数字减少到一位数

> 原文:[https://www . geeksforgeeks . org/通过重复减去相邻数字将数字减少到一位数/](https://www.geeksforgeeks.org/reduce-number-to-a-single-digit-by-subtracting-adjacent-digits-repeatedly/)

给定一个数字 **N** ，任务是通过重复减去相邻的数字将其减少到一位数。也就是说，在第一次迭代中，减去所有相邻的数字，生成一个新的数字，如果这个数字包含一个以上的数字，重复同样的过程，直到它变成一个位数。

**示例:**

> **输入:** N = 6972
> **输出:**2
> | 6–9 | = 3
> | 9–7 | = 2
> | 7–2 | = 5
> 第一步后我们得到 **325** 但是 **325** 不是一位数，所以我们会进一步减少，直到没有得到一位数。
> | 3–2 | = 1
> | 2–5 | = 3
> 而现在这个数字将变成 **13** ，我们将进一步减少它
> | 1–3 | = 2
> **输入:** N = 123456
> **输出:** 0

**方法:**这里为了简单起见，我们使用**数组**来表示初始数字 N。

1.  计算 **N** 中的位数，并将数值存储在 **l** 中。

2.  创建一个大小为 **l** 的数组**[]**。

3.  将给定的数字复制到数组 **a[]** 中。

4.  通过减去数组 **a** 的连续位数计算出 **RSF** 。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the resultant digit
// after performing the given operations
int RSF(int n)
{
    while (n >= 10) {

        // Creating an extra copy of n
        int x = n;
        int l = 0;

        // Counting the number of digits in n
        while (n > 0) {
            n = n / 10;
            l++;
        }

        // Now n is 0
        // Creating an array of length l
        int a[l];

        // Initializing i with the last index of array
        int i = l - 1;
        while (x > 0) {

            // Filling array from right to left
            a[i] = x % 10;
            x = x / 10;
            i--;
        }

        // Calculating the absolute consecutive difference
        for (int j = 0; j < l - 1; j++) {

            // Updating the value of n in every loop
            n = n * 10 + abs(a[j] - a[j + 1]);
        }
    }

    // While loop ends here and we have found
    // the RSF value of N
    return n;
}

// Driver code
int main()
{
    int n = 614;

    // Passing n to RSF function and getting answer
    int ans = RSF(n);

    // Printing the value stored in ans
    cout << ans;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG {

    // Function to return the resultant digit
    // after performing the given operations
    static int RSF(int n)
    {
        while (n >= 10) {

            // Creating an extra copy of n
            int x = n;
            int l = 0;

            // Counting the number of digits in n
            while (n > 0) {
                n = n / 10;
                l++;
            }

            // Now n is 0
            // Creating an array of length l
            int a[] = new int[l];

            // Initializing i with the last index of array
            int i = l - 1;

            while (x > 0) {

                // Filling array from right to left
                a[i] = x % 10;
                x = x / 10;
                i--;
            }

            // Calculating the absolute consecutive difference
            for (int j = 0; j < l - 1; j++) {

                // Updating the value of n in every loop
                n = n * 10 + Math.abs(a[j] - a[j + 1]);
            }
        }

        // While loop ends here and we have found
        // the RSF value of N
        return n;
    }

    // Driver code
    public static void main(String[] arg)
    {
        int n = 6972;

        // Passing n to RSF function and getting answer
        int ans = RSF(n);

        // Printing the value stored in ans
        System.out.println(ans);
    }
}
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the resultant digit
# after performing the given operations
def RSF(n):
    while (n >= 10):

        # Creating an extra copy of n
        x = n;
        l = 0;

        # Counting the number of digits in n
        while (n > 0):
            n = n // 10;
            l += 1;

        # Now n is 0
        # Creating an array of length l
        a = [0] * l;

        # Initializing i with the last index of array
        i = l - 1;
        while (x > 0):

            # Filling array from right to left
            a[i] = x % 10;
            x = x // 10;
            i -= 1;

        # Calculating the absolute
        # consecutive difference
        for j in range(0, l - 1):

            # Updating the value of n in every loop
            n = n * 10 + abs(a[j] - a[j + 1]);

    # While loop ends here and we have found
    # the RSF value of N
    return n;

# Driver code
if __name__ == '__main__':
    n = 614;

    # Passing n to RSF function
    # and getting answer
    ans = RSF(n);

    # Printing the value stored in ans
    print(ans);

# This code is contributed by Rajput-Ji
```

## C#

```
// C# implementation of the approach
using System;
class GFG
{

// Function to return the resultant digit
// after performing the given operations
static int RSF(int n)
{
    while (n >= 10)
    {

        // Creating an extra copy of n
        int x = n;
        int l = 0;

        // Counting the number of digits in n
        while (n > 0)
        {
            n = n / 10;
            l++;
        }

        // Now n is 0
        // Creating an array of length l
        int []a = new int[l];

        // Initializing i with the last index of array
        int i = l - 1;

        while (x > 0)
        {

            // Filling array from right to left
            a[i] = x % 10;
            x = x / 10;
            i--;
        }

        // Calculating the absolute
        // consecutive difference
        for (int j = 0; j < l - 1; j++)
        {

            // Updating the value of n in every loop
            n = n * 10 + Math.Abs(a[j] - a[j + 1]);
        }
    }

    // While loop ends here and we have found
    // the RSF value of N
    return n;
}

// Driver code
public static void Main(String[] arg)
{
    int n = 6972;

    // Passing n to RSF function and getting answer
    int ans = RSF(n);

    // Printing the value stored in ans
    Console.WriteLine(ans);
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
// javascript implementation of the approach   
// Function to return the resultant digit
    // after performing the given operations
    function RSF(n) {
        while (n >= 10) {

            // Creating an extra copy of n
            var x = n;
            var l = 0;

            // Counting the number of digits in n
            while (n > 0) {
                n = parseInt(n / 10);
                l++;
            }

            // Now n is 0
            // Creating an array of length l
            var a = Array(l).fill(0);

            // Initializing i with the last index of array
            var i = l - 1;

            while (x > 0) {

                // Filling array from right to left
                a[i] = x % 10;
                x = parseInt(x / 10);
                i--;
            }

            // Calculating the absolute consecutive difference
            for (j = 0; j < l - 1; j++) {

                // Updating the value of n in every loop
                n = n * 10 + Math.abs(a[j] - a[j + 1]);
            }
        }

        // While loop ends here and we have found
        // the RSF value of N
        return n;
    }

    // Driver code
        var n = 6972;

        // Passing n to RSF function and getting answer
        var ans = RSF(n);

        // Printing the value stored in ans
        document.write(ans);

// This code contributed by aashish1995
</script>
```

**Output:** 

```
2
```