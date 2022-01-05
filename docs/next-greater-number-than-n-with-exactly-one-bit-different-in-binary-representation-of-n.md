# 下一个大于 N 的数字，在 N 的二进制表示中正好有一位不同

> 原文:[https://www . geeksforgeeks . org/next-大于 n 的二进制表示中正好有一位不同于 n/](https://www.geeksforgeeks.org/next-greater-number-than-n-with-exactly-one-bit-different-in-binary-representation-of-n/)

给定一个数 n，任务是找到大于 n 的最小数，并且在 n 的二进制表示中只有一位不同。
**注**:这里 n 可以是非常大的 10^9 < N < 10^15.
**示例:**

```
Input : N = 11
Output : The next number is 15
The binary representation of 11 is 1011
So the smallest number greater than 11 
with one bit different is 1111 which is 15.

Input : N = 17
Output : The next number is 19
```

**简单方法**:我们将从 N+1 开始循环，直到找到一个与 N 正好相差一位的数字。如果是大数目的话，这个过程可能需要很长时间来处理
**高效方法**:在高效方法中，我们必须用二进制形式来表示数字。现在，只有当我们保持数字 N 的所有设置位不变，并将最低可能位从 0 切换到 1 时，只有 1 位不同的大于 N 的数字才是可能的。
我们举个例子，1001 是 9 的二进制形式，
如果我们把 1001 的设定位转换成 1000 或 0001，那么我们发现数字是 8 和 1，它们都小于 N。而如果我们把 0 的位转换成 1，我们发现数字是 11 (1011)或 13 (1101)，所以如果我们把最小的可能位转换成 1，那么我们得到大于 N 的最小可能数，只有 1 位不同，在这种情况下
**注**:保证输入数 N 没有全部位都置位。在 n 的二进制表示中至少存在一个未设置的位。下面是上述方法的实现:

## C++

```
// CPP program to find next greater number than N
// with exactly one bit different in binary
// representation of N

#include <bits/stdc++.h>
using namespace std;

// Function to find next greater number than N
// with exactly one bit different in binary
// representation of N
long long nextGreater(long long N)
{
    long long power_of_2 = 1, shift_count = 0;

    // It is guaranteed that there
    // is a bit zero in the number
    while (true) {
        // If the shifted bit is zero then break
        if (((N >> shift_count) & 1) % 2 == 0)
            break;

        // increase the bit shift
        shift_count++;

        // increase the power of 2
        power_of_2 = power_of_2 * 2;
    }

    // set the lowest bit of the number
    return (N + power_of_2);
}

// Driver code
int main()
{
    long long N = 11;

    // display the next number
    cout << "The next number is = " << nextGreater(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find next greater number than N
// with exactly one bit different in binary
// representation of N

class GFG{
// Function to find next greater number than N
// with exactly one bit different in binary
// representation of N
static int nextGreater(int N)
{
    int power_of_2 = 1, shift_count = 0;

    // It is guaranteed that there
    // is a bit zero in the number
    while (true) {
        // If the shifted bit is zero then break
        if (((N >> shift_count) & 1) % 2 == 0)
            break;

        // increase the bit shift
        shift_count++;

        // increase the power of 2
        power_of_2 = power_of_2 * 2;
    }

    // set the lowest bit of the number
    return (N + power_of_2);
}

// Driver code
public static void main(String[]a)
{
    int N = 11;

    // display the next number
    System.out.println("The next number is = " + nextGreater(N));

}
}
```

## 蟒蛇 3

```
# Python3 program to find next greater
# number than N with exactly one
# bit different in binary
# representation of N

# Function to find next greater
# number than N with exactly
# one bit different in binary
# representation of N
def nextGreater(N):

    power_of_2 = 1;
    shift_count = 0;

    # It is guaranteed that there
    # is a bit zero in the number
    while (True):

        # If the shifted bit is
        # zero then break
        if (((N >> shift_count) & 1) % 2 == 0):
            break;

        # increase the bit shift
        shift_count += 1;

        # increase the power of 2
        power_of_2 = power_of_2 * 2;

    # set the lowest bit
    # of the number
    return (N + power_of_2);

# Driver code
N = 11;

# display the next number
print("The next number is =",
             nextGreater(N));

# This code is contributed by mits
```

## C#

```
// C# program to find next
// greater number than N with 
// exactly one bit different in
// binary representation of N
using System;

class GFG
{
// Function to find next greater
// number than N with exactly
// one bit different in binary
// representation of N
static int nextGreater(int N)
{
    int power_of_2 = 1,
        shift_count = 0;

    // It is guaranteed that there
    // is a bit zero in the number
    while (true)
    {
        // If the shifted bit is
        // zero then break
        if (((N >> shift_count) & 1) % 2 == 0)
            break;

        // increase the bit shift
        shift_count++;

        // increase the power of 2
        power_of_2 = power_of_2 * 2;
    }

    // set the lowest bit
    // of the number
    return (N + power_of_2);
}

// Driver code
public static void Main()
{
    int N = 11;

    // display the next number
    Console.WriteLine("The next number is = " +
                               nextGreater(N));
}
}

// This code is contributed
// by anuj_67
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to find next greater
// number than N with exactly one
// bit different in binary
// representation of N

// Function to find next greater
// number than N with exactly
// one bit different in binary
// representation of N
function nextGreater($N)
{
    $power_of_2 = 1;
    $shift_count = 0;

    // It is guaranteed that there
    // is a bit zero in the number
    while (true)
    {
        // If the shifted bit is
        // zero then break
        if ((($N >> $shift_count) & 1) % 2 == 0)
            break;

        // increase the bit shift
        $shift_count++;

        // increase the power of 2
        $power_of_2 = $power_of_2 * 2;
    }

    // set the lowest bit of the number
    return ($N + $power_of_2);
}

// Driver code
$N = 11;

// display the next number
echo "The next number is = " ,
              nextGreater($N);

// This code is contributed
// by anuj_67
?>
```

## java 描述语言

```
<script>

//Javascript program to find next greater number than N
// with exactly one bit different in binary
// representation of N

// Function to find next greater number than N
// with exactly one bit different in binary
// representation of N
function nextGreater(N)
{
   var power_of_2 = 1, shift_count = 0;

    // It is guaranteed that there
    // is a bit zero in the number
    while (true) {
        // If the shifted bit is zero then break
        if (((N >> shift_count) & 1) % 2 == 0)
            break;

        // increase the bit shift
        shift_count++;

        // increase the power of 2
        power_of_2 = power_of_2 * 2;
    }

    // set the lowest bit of the number
    return (N + power_of_2);
}

var N = 11;
// display the next number
document.write("The next number is = " + nextGreater(N));

// This code is contributed bby SoumikMondal

</script>
```

**Output:** 

```
The next number is = 15
```

**时间复杂度:** O(log(N))