# 重新排列数组，最大化数组前缀和中的素数

> 原文:[https://www . geeksforgeeks . org/重排数组以最大化前缀和数组中的素数数量/](https://www.geeksforgeeks.org/rearrange-the-array-to-maximize-the-number-of-primes-in-prefix-sum-of-the-array/)

给定一个由 **1 的**和 **2 的**组成的数组 **arr[]** ，任务是重新排列数组，使得重新排列的数组的前缀和具有最大的素数。**注意**可以有多个答案。
**举例:**

> **输入:** arr[] = {1，2，1，2，1}
> **输出:** 2 1 1 1 2
> 前缀和数组为{2，3，4，5，7}，其中{2，3，5，7}为素数
> 为最大可能。
> **输入:** arr[] = {1，1，2，1，1，1，2，1，1}
> **输出:**2 1 1 1 1 1 1 2

**做法:**这个问题可以用两个观察来解决，一个是第一个素数是 2，之后的所有其他素数都是奇数(所有奇数都不是素数)。因此，只要在第一个位置填充 2(如果有的话)，然后填充奇数个 1，然后填充剩余的 2。在末尾插入剩下的 1(如果最初的 1 是偶数)。
这样做，我们从 2 开始，在一个奇数处结束，将一个奇数加 1，然后再加 2，我们从一个奇数跳到另一个奇数，从而最大化素数的概率。
以下是上述办法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the re-arranged array
void solve(int a[], int n)
{
    int ones = 0, twos = 0;

    // Count the number of
    // ones and twos in a[]
    for (int i = 0; i < n; i++) {

        // If the array element is 1
        if (a[i] == 1)
            ones++;

        // Array element is 2
        else
            twos++;
    }
    int ind = 0;

    // If it has at least one 2
    // Fill up first 2
    if (twos)
        a[ind++] = 2;

    // Decrease the cnt of
    // ones if even
    bool evenOnes = (ones % 2 == 0) ? true : false;
    if (evenOnes)
        ones -= 1;

    // Fill up with odd count of ones
    for (int i = 0; i < ones; i++)
        a[ind++] = 1;

    // Fill up with remaining twos
    for (int i = 0; i < twos - 1; i++)
        a[ind++] = 2;

    // If even ones, then fill last position
    if (evenOnes)
        a[ind++] = 1;

    // Print the rearranged array
    for (int i = 0; i < n; i++)
        cout << a[i] << " ";
}

// Driver code
int main()
{
    int a[] = { 1, 2, 1, 2, 1 };
    int n = sizeof(a) / sizeof(a[0]);
    solve(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.io.*;

class GFG {

    // Function to print the re-arranged array
    static void solve(int a[], int n)
    {
        int ones = 0, twos = 0;

        // Count the number of
        // ones and twos in a[]
        for (int i = 0; i < n; i++) {

            // If the array element is 1
            if (a[i] == 1)
                ones++;

            // Array element is 2
            else
                twos++;
        }
        int ind = 0;

        // If it has at least one 2
        // Fill up first 2
        if (twos > 0)
            a[ind++] = 2;

        // Decrease the cnt of
        // ones if even
        boolean evenOnes = (ones % 2 == 0) ? true : false;
        if (evenOnes)
            ones -= 1;

        // Fill up with odd count of ones
        for (int i = 0; i < ones; i++)
            a[ind++] = 1;

        // Fill up with remaining twos
        for (int i = 0; i < twos - 1; i++)
            a[ind++] = 2;

        // If even ones, then fill last position
        if (evenOnes)
            a[ind++] = 1;

        // Print the rearranged array
        for (int i = 0; i < n; i++)
            System.out.print(a[i] + " ");
    }

    // Driver code
    public static void main(String[] args)
    {

        int a[] = { 1, 2, 1, 2, 1 };
        int n = a.length;
        solve(a, n);
    }
}

// This code is contributed by ajit.
```

## 计算机编程语言

```
# Python3 implementation of the approach

# Function to print the re-arranged array
def solve(a, n):

    ones, twos = 0, 0

    # Count the number of
    # ones and twos in a[]
    for i in range(n):

        # If the array element is 1
        if (a[i] == 1):
            ones+=1

        # Array element is 2
        else:
            twos+=1

    ind = 0

    # If it has at least one 2
    # Fill up first 2
    if (twos):
        a[ind] = 2
        ind+=1

    # Decrease the cnt of
    # ones if even
    if ones % 2 == 0:
        evenOnes = True
    else:
        evenOnes = False

    if (evenOnes):
        ones -= 1

    # Fill up with odd count of ones
    for i in range(ones):
        a[ind] = 1
        ind += 1

    # Fill up with remaining twos
    for i in range(twos-1):
        a[ind] = 2
        ind += 1

    # If even ones, then fill last position
    if (evenOnes):
        a[ind] = 1
        ind += 1

    # Print the rearranged array
    for i in range(n):
        print(a[i],end = " ")

# Driver code

a = [1, 2, 1, 2, 1]
n = len(a)
solve(a, n)

# This code is contributed by mohit kumar 29
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    // Function to print the re-arranged array
    static void solve(int []a, int n)
    {
        int ones = 0, twos = 0;

        // Count the number of
        // ones and twos in a[]
        for (int i = 0; i < n; i++)
        {

            // If the array element is 1
            if (a[i] == 1)
                ones++;

            // Array element is 2
            else
                twos++;
        }
        int ind = 0;

        // If it has at least one 2
        // Fill up first 2
        if (twos > 0)
            a[ind++] = 2;

        // Decrease the cnt of
        // ones if even
        bool evenOnes = (ones % 2 == 0) ? true : false;
        if (evenOnes)
            ones -= 1;

        // Fill up with odd count of ones
        for (int i = 0; i < ones; i++)
            a[ind++] = 1;

        // Fill up with remaining twos
        for (int i = 0; i < twos - 1; i++)
            a[ind++] = 2;

        // If even ones, then fill last position
        if (evenOnes)
            a[ind++] = 1;

        // Print the rearranged array
        for (int i = 0; i < n; i++)
            Console.Write(a[i] + " ");
    }

    // Driver code
    static public void Main ()
    {
        int []a = { 1, 2, 1, 2, 1 };
        int n = a.Length;
        solve(a, n);
    }
}

// This code is contributed by Tushil.
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to print the re-arranged array
function solve($a, $n)
{
    $ones = 0; $twos = 0;

    // Count the number of
    // ones and twos in a[]
    for ($i = 0; $i < $n; $i++)
    {

        // If the array element is 1
        if ($a[$i] == 1)
            $ones++;

        // Array element is 2
        else
            $twos++;
    }
    $ind = 0;

    // If it has at least one 2
    // Fill up first 2
    if ($twos)
        $a[$ind++] = 2;

    // Decrease the cnt of
    // ones if even
    $evenOnes = ($ones % 2 == 0) ? true : false;
    if ($evenOnes)
        $ones -= 1;

    // Fill up with odd count of ones
    for ($i = 0; $i < $ones; $i++)
        $a[$ind++] = 1;

    // Fill up with remaining twos
    for ($i = 0; $i < $twos - 1; $i++)
        $a[$ind++] = 2;

    // If even ones, then fill last position
    if ($evenOnes)
        $a[$ind++] = 1;

    // Print the rearranged array
    for ($i = 0; $i < $n; $i++)
        echo $a[$i], " ";
}

// Driver code
$a = array( 1, 2, 1, 2, 1 );
$n = count($a);
solve($a, $n);

// This code is contributed by AnkitRai01

?>
```

## java 描述语言

```
<script>
    // Javascript implementation of the approach

    // Function to print the re-arranged array
    function solve(a, n)
    {
        let ones = 0, twos = 0;

        // Count the number of
        // ones and twos in a[]
        for (let i = 0; i < n; i++)
        {

            // If the array element is 1
            if (a[i] == 1)
                ones++;

            // Array element is 2
            else
                twos++;
        }
        let ind = 0;

        // If it has at least one 2
        // Fill up first 2
        if (twos > 0)
            a[ind++] = 2;

        // Decrease the cnt of
        // ones if even
        let evenOnes = (ones % 2 == 0) ? true : false;
        if (evenOnes)
            ones -= 1;

        // Fill up with odd count of ones
        for (let i = 0; i < ones; i++)
            a[ind++] = 1;

        // Fill up with remaining twos
        for (let i = 0; i < twos - 1; i++)
            a[ind++] = 2;

        // If even ones, then fill last position
        if (evenOnes)
            a[ind++] = 1;

        // Print the rearranged array
        for (let i = 0; i < n; i++)
            document.write(a[i] + " ");
    }

    let a = [ 1, 2, 1, 2, 1 ];
    let n = a.length;
    solve(a, n);

</script>
```

**Output:** 

```
2 1 1 1 2
```