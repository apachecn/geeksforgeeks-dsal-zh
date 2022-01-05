# 在二进制数组中精确擦除一个元素以使异或为零的方法数

> 原文:[https://www . geeksforgeeks . org/擦除二进制数组中恰好一个元素的方法数-进行异或-零/](https://www.geeksforgeeks.org/number-of-ways-to-erase-exactly-one-element-in-the-binary-array-to-make-xor-zero/)

给定一个由 0 和 1 组成的二进制数组，任务是找出从这个数组中精确删除一个元素的方法，使异或为零。
**例:**

```
Input: arr = {1, 1, 1, 1, 1 }
Output: 5 
You can erase any of the given 5 1's,
it will make the XOR of the rest equal to zero.

Input: arr = {1, 0, 0, 1, 0 }
Output: 3 
Since the XOR of array is already 0,
You can erase any of the given 3 0's
so that the XOR remains unaffected.
```

**方法:**既然我们知道，要使二进制元素的异或为 0，1 的个数应该是偶数。因此这个问题可以分为 4 种情况:

*   **当给定数组中 1 的个数为偶数，0 的个数也为偶数时:**在这种情况下，数组的异或已经为 0。因此，为了保持异或不受影响，我们只能移除 0。因此，从该数组中精确擦除一个元素以使异或为零的方法数量是该数组中 0 的**数量**。

*   **当给定数组中 1 的个数为偶数，0 的个数为奇数时:**在这种情况下，数组的异或已经为 0。因此，为了保持异或不受影响，我们只能移除 0。因此，从该数组中精确擦除一个元素以使异或为零的方法数量是该数组中 0 的**数量**。

*   **当给定数组中 1 的个数为奇数，0 的个数为偶数时:**在这种情况下，数组的异或为 1。因此，要使异或为 0，我们可以去掉任何 1。因此，从这个数组中删除一个元素使异或为零的方法数是这个数组中 1 的**数**。

*   **当给定数组中 1 的个数为奇数，0 的个数也为奇数时:**在这种情况下，数组的异或为 1。因此，要使异或为 0，我们可以去掉任何 1。因此，从这个数组中删除一个元素使异或为零的方法数是这个数组中 1 的**数**。

以下是上述方法的实现:

## C++

```
// C++ program to find the number of ways
// to erase exactly one element
// from this array to make XOR zero

#include <bits/stdc++.h>
using namespace std;

// Function to find the number of ways
int no_of_ways(int a[], int n)
{
    int count_0 = 0, count_1 = 0;

    // Calculate the number of 1's and 0's
    for (int i = 0; i < n; i++) {
        if (a[i] == 0)
            count_0++;
        else
            count_1++;
    }

    // Considering the 4 cases
    if (count_1 % 2 == 0)
        return count_0;
    else
        return count_1;
}

// Driver code
int main()
{
    int n = 4;
    int a1[4] = { 1, 1, 0, 0 };
    cout << no_of_ways(a1, n) << endl;

    n = 5;
    int a2[5] = { 1, 1, 1, 0, 0 };
    cout << no_of_ways(a2, n) << endl;

    n = 5;
    int a3[5] = { 1, 1, 0, 0, 0 };
    cout << no_of_ways(a3, n) << endl;

    n = 6;
    int a4[6] = { 1, 1, 1, 0, 0, 0 };
    cout << no_of_ways(a4, n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the number of ways
// to erase exactly one element
// from this array to make XOR zero
class GFG
{

    // Function to find the number of ways
    static int no_of_ways(int a[], int n)
    {
        int count_0 = 0, count_1 = 0;

        // Calculate the number of 1's and 0's
        for (int i = 0; i < n; i++)
        {
            if (a[i] == 0)
                count_0++;
            else
                count_1++;
        }

        // Considering the 4 cases
        if (count_1 % 2 == 0)
            return count_0;
        else
            return count_1;
    }

    // Driver code
    public static void main (String[] args)
    {
        int n = 4;
        int a1[] = { 1, 1, 0, 0 };
        System.out.println(no_of_ways(a1, n));

        n = 5;
        int a2[] = { 1, 1, 1, 0, 0 };
        System.out.println(no_of_ways(a2, n));

        n = 5;
        int a3[] = { 1, 1, 0, 0, 0 };
        System.out.println(no_of_ways(a3, n));

        n = 6;
        int a4[] = { 1, 1, 1, 0, 0, 0 };
        System.out.println(no_of_ways(a4, n));
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 program to find the number of ways
# to erase exactly one element
# from this array to make XOR zero

# Function to find the number of ways
def no_of_ways(a, n):

    count_0 = 0
    count_1 = 0

    # Calculate the number of 1's and 0's
    for i in range(0, n):
        if (a[i] == 0):
            count_0 += 1
        else:
            count_1 += 1

    # Considering the 4 cases
    if (count_1 % 2 == 0):
        return count_0
    else:
        return count_1

# Driver code
if __name__ == '__main__':
    n = 4
    a1 = [ 1, 1, 0, 0 ]
    print(no_of_ways(a1, n))

    n = 5
    a2 = [ 1, 1, 1, 0, 0 ]
    print(no_of_ways(a2, n))

    n = 5
    a3 = [ 1, 1, 0, 0, 0 ]
    print(no_of_ways(a3, n))

    n = 6
    a4 = [ 1, 1, 1, 0, 0, 0 ]
    print(no_of_ways(a4, n))

# This code is contributed by ashutosh450
```

## C#

```
// C# program to find the number of ways
// to erase exactly one element
// from this array to make XOR zero
using System;

class GFG
{

    // Function to find the number of ways
    static int no_of_ways(int []a, int n)
    {
        int count_0 = 0, count_1 = 0;

        // Calculate the number of 1's and 0's
        for (int i = 0; i < n; i++)
        {
            if (a[i] == 0)
                count_0++;
            else
                count_1++;
        }

        // Considering the 4 cases
        if (count_1 % 2 == 0)
            return count_0;
        else
            return count_1;
    }

    // Driver code
    public static void Main ()
    {
        int n = 4;
        int [] a1 = { 1, 1, 0, 0 };
        Console.WriteLine(no_of_ways(a1, n));

        n = 5;
        int [] a2 = { 1, 1, 1, 0, 0 };
        Console.WriteLine(no_of_ways(a2, n));

        n = 5;
        int [] a3 = { 1, 1, 0, 0, 0 };
        Console.WriteLine(no_of_ways(a3, n));

        n = 6;
        int [] a4 = { 1, 1, 1, 0, 0, 0 };
        Console.WriteLine(no_of_ways(a4, n));
    }
}

// This code is contributed by Mohit kumar
```

## java 描述语言

```
<script>

// Javascript program to find the number of ways
// to erase exactly one element
// from this array to make XOR zero

// Function to find the number of ways
function no_of_ways(a, n)
{
    let count_0 = 0, count_1 = 0;

    // Calculate the number of 1's and 0's
    for (let i = 0; i < n; i++) {
        if (a[i] == 0)
            count_0++;
        else
            count_1++;
    }

    // Considering the 4 cases
    if (count_1 % 2 == 0)
        return count_0;
    else
        return count_1;
}

// Driver code
    let n = 4;
    let a1 = [ 1, 1, 0, 0 ];
    document.write(no_of_ways(a1, n) + "<br>");

    n = 5;
    let a2 = [ 1, 1, 1, 0, 0 ];
    document.write(no_of_ways(a2, n) + "<br>");

    n = 5;
    let a3 = [ 1, 1, 0, 0, 0 ];
    document.write(no_of_ways(a3, n) + "<br>");

    n = 6;
    let a4 = [ 1, 1, 1, 0, 0, 0 ];
    document.write(no_of_ways(a4, n) + "<br>");

</script>
```

**Output:** 

```
2
3
3
3
```

**时间复杂度:** O(n)