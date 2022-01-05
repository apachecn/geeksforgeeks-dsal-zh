# 检查 N 个数字的最后一位组成的数字是否能被 10 整除

> 原文:[https://www . geesforgeks . org/check-n-numbers 的最后一位数字构成的数字是否可被 10 整除/](https://www.geeksforgeeks.org/check-if-the-number-formed-by-the-last-digits-of-n-numbers-is-divisible-by-10-or-not/)

给定一个由非零正整数组成的大小为 **N** 的数组 **arr[]** 。任务是确定通过选择所有数字的最后几个数字形成的数字是否能被 10 整除。如果数字可被 10 整除，则打印“是”，否则打印“否”
**示例:**

> **输入:** arr[] = {12，65，46，37，99}
> **输出:**否
> 25679 不能被 10 整除。
> **输入:** arr[] = {24，37，46，50}
> **输出:**是
> 4760 可被 10 整除。

**方法:**一个整数要被 10 整除，必须以 0 结尾。所以，数组的最后一个元素将决定形成的数字是否能被 10 整除。如果最后一个元素的最后一位数字是 0，则打印是，否则打印否
以下是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <iostream>
using namespace std;

// Function that returns true if the
// number formed by the last digits of
// all the elements is divisible by 10
bool isDivisible(int arr[], int n)
{
    // Last digit of the last element
    int lastDigit = arr[n - 1] % 10;

    // Number formed will be divisible by 10
    if (lastDigit == 0)
        return true;

    return false;
}

// Driver code
int main()
{
    int arr[] = { 12, 65, 46, 37, 99 };
    int n = sizeof(arr) / sizeof(arr[0]);

    if (isDivisible(arr, n))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function that returns true if the
// number formed by the last digits of
// all the elements is divisible by 10
static boolean isDivisible(int arr[], int n)
{
    // Last digit of the last element
    int lastDigit = arr[n - 1] % 10;

    // Number formed will be divisible by 10
    if (lastDigit == 0)
        return true;

    return false;
}

// Driver code
static public void main ( String []arg)
{
    int arr[] = { 12, 65, 46, 37, 99 };
    int n = arr.length;

    if (isDivisible(arr, n))
        System.out.println("Yes");
    else
        System.out.println("No");
}
}

// This code is contributed by Rajput-Ji
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that returns true if the
# number formed by the last digits of
# all the elements is divisible by 10
def isDivisible(arr, n) :

    # Last digit of the last element
    lastDigit = arr[n - 1] % 10;

    # Number formed will be divisible by 10
    if (lastDigit == 0) :
        return True;

    return False;

# Driver code
if __name__ == "__main__" :

    arr = [ 12, 65, 46, 37, 99 ];
    n = len(arr);

    if (isDivisible(arr, n)) :
        print("Yes");
    else :
        print("No");

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

// Function that returns true if the
// number formed by the last digits of
// all the elements is divisible by 10
static bool isDivisible(int []arr, int n)
{
    // Last digit of the last element
    int lastDigit = arr[n - 1] % 10;

    // Number formed will be divisible by 10
    if (lastDigit == 0)
        return true;

    return false;
}

// Driver code
static public void Main(String []arg)
{
    int []arr = { 12, 65, 46, 37, 99 };
    int n = arr.Length;

    if (isDivisible(arr, n))
        Console.WriteLine("Yes");
    else
        Console.WriteLine("No");
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function that returns true if the
// number formed by the last digits of
// all the elements is divisible by 10
function isDivisible(arr, n)
{
    // Last digit of the last element
    let lastDigit = arr[n - 1] % 10;

    // Number formed will be divisible by 10
    if (lastDigit == 0)
        return true;

    return false;
}

// Driver code
    let arr = [ 12, 65, 46, 37, 99 ];
    let n = arr.length;

    if (isDivisible(arr, n))
        document.write("Yes");
    else
        document.write("No");

</script>
```

**Output:** 

```
No
```