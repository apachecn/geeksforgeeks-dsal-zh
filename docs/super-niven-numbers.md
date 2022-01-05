# 超级尼文号码

> 原文:[https://www.geeksforgeeks.org/super-niven-numbers/](https://www.geeksforgeeks.org/super-niven-numbers/)

**超级尼文数**是一个数 **N** ，如果它不仅能被它的位数之和整除，还能被它的(非零)位数的任何子集之和整除。
**例如:**

> 68040 是一个**超级尼文数**，因为它可以被 6，8，4，6+8，6+4，4+8，6+4+8 整除。

### 检查 N 是否是超级尼文数

给定一个数字 **N** ，任务是检查 **N** 是否为**超级尼文号**。如果 **N** 是超级尼文号码，则打印**“是”**否则打印**“否”**。
**示例:**

> **输入:** N = 68040
> **输出:**是
> **说明:**
> 68040 可被 6、8、4、6+8、6+4、4+8、6+4+8 整除。
> 和 **N** 也以‘25’开头。
> **输入:** N = 72
> **输出:**否

**进场:**:

1.  我们将在数组 arr 中存储数字 **N** 的所有数字
2.  现在我们将找到数组每个子集的和，并检查数字 **N** 是否能被所有子集整除
3.  如果 N 不能被任何子集整除，那么返回假，否则最后返回真。

下面是上述方法的实现:

## C++

```
// C++ implementation to check if a number
// is Super Niven Number or not.

#include <bits/stdc++.h>
using namespace std;

// Checks if sums of all subsets of digits array
// divides the number N
bool isDivBySubsetSums(vector<int> arr, int num)
{
    // to calculate length of array arr
    int n = arr.size();

    // There are totoal 2^n subsets
    long long total = 1 << n;

    // Consider all numbers from 0 to 2^n - 1
    for (long long i = 0; i < total; i++) {
        long long sum = 0;

        // Consider binary representation of
        // current i to decide which elements
        // to pick.
        for (int j = 0; j < n; j++)
            if (i & (1 << j))
                sum += arr[j];

        // check sum of picked elements.
        if (sum != 0 && num % sum != 0)
            return false;
    }
    return true;
}

// Function to check if a number is
// a super-niven number
bool isSuperNivenNum(int n)
{
    int temp = n;
    // to stor digits of N
    vector<int> digits;

    while (n != 0) {
        int digit = n % 10;
        digits.push_back(digit);
        n = n / 10;
    }

    return isDivBySubsetSums(digits, temp);
}

// Driver code
int main()
{
    int n = 500;
    if (isSuperNivenNum(n))
        cout << "yes";
    else
        cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to check if a number
// is Super Niven Number or not.
import java.util.*;
class GFG{

// Checks if sums of all subsets of digits array
// divides the number N
static boolean isDivBySubsetSums(Vector<Integer> arr,
                                             int num)
{
    // to calculate length of array arr
    int n = arr.size();

    // There are totoal 2^n subsets
    long total = 1 << n;

    // Consider all numbers from 0 to 2^n - 1
    for (long i = 0; i < total; i++)
    {
        long sum = 0;

        // Consider binary representation of
        // current i to decide which elements
        // to pick.
        for (int j = 0; j < n; j++)
            if ((i & (1 << j)) > 0)
                sum += arr.get(j);

        // check sum of picked elements.
        if (sum != 0 && num % sum != 0)
            return false;
    }
    return true;
}

// Function to check if a number is
// a super-niven number
static boolean isSuperNivenNum(int n)
{
    int temp = n;
    // to stor digits of N
    Vector<Integer> digits = new Vector<Integer>();

    while (n != 0)
    {
        int digit = n % 10;
        digits.add(digit);
        n = n / 10;
    }

    return isDivBySubsetSums(digits, temp);
}

// Driver code
public static void main(String[] args)
{
    int n = 500;
    if (isSuperNivenNum(n))
        System.out.print("yes");
    else
        System.out.print("No");
}
}

// This code is contributed by Amit Katiyar
```

## 蟒蛇 3

```
# Python3 implementation to check if a
# number is Super Niven Number or not.

# Checks if sums of all subsets of digits
# array divides the number N
def isDivBySubsetSums(arr, num):

    # To calculate length of array arr
    n = len(arr)

    # There are totoal 2^n subsets
    total = 1 << n

    # Consider all numbers from 0 to 2^n - 1
    i = 0
    while i < total:
        sum = 0

        # Consider binary representation of
        # current i to decide which elements
        # to pick.
        j = 0
        while j < n:
            if (i & (1 << j)):
                sum += arr[j]

            j += 1

        # Check sum of picked elements.
        if (sum != 0) and (num % sum != 0):
            return False

        i += 1

    return True

# Function to check if a number is
# a super-niven number
def isSuperNivenNum(n):

    temp = n

    # To store digits of N
    digits = []

    while (n > 1):
        digit = int(n) % 10
        digits.append(digit)
        n = n / 10

    return isDivBySubsetSums(digits, temp)

# Driver code
if __name__ == '__main__':

    n = 500

    if isSuperNivenNum(n):
        print("Yes")
    else:
        print("No")

# This code is contributed by jana_sayantan
```

## C#

```
// C# implementation to check if a number
// is Super Niven Number or not.
using System;
using System.Collections.Generic;

class GFG{

// Checks if sums of all subsets of digits array
// divides the number N
static bool isDivBySubsetSums(List<int> arr,
                                   int num)
{
    // to calculate length of array arr
    int n = arr.Count;

    // There are totoal 2^n subsets
    long total = 1 << n;

    // Consider all numbers from 0 to 2^n - 1
    for (long i = 0; i < total; i++)
    {
        long sum = 0;

        // Consider binary representation of
        // current i to decide which elements
        // to pick.
        for (int j = 0; j < n; j++)
            if ((i & (1 << j)) > 0)
                sum += arr[j];

        // check sum of picked elements.
        if (sum != 0 && num % sum != 0)
            return false;
    }
    return true;
}

// Function to check if a number is
// a super-niven number
static bool isSuperNivenNum(int n)
{
    int temp = n;
    // to stor digits of N
    List<int> digits = new List<int>();

    while (n != 0)
    {
        int digit = n % 10;
        digits.Add(digit);
        n = n / 10;
    }
    return isDivBySubsetSums(digits, temp);
}

// Driver code
public static void Main(String[] args)
{
    int n = 500;
    if (isSuperNivenNum(n))
        Console.Write("yes");
    else
        Console.Write("No");
}
}

// This code is contributed by gauravrajput1
```

## java 描述语言

```
<script>

// Javascript implementation to check if a number
// is Super Niven Number or not.

// Checks if sums of all subsets of digits array
// divides the number N
function isDivBySubsetSums(arr, num)
{
    // to calculate length of array arr
    var n = arr.length;

    // There are totoal 2^n subsets
    var total = 1 << n;

    // Consider all numbers from 0 to 2^n - 1
    for (var i = 0; i < total; i++) {
        var sum = 0;

        // Consider binary representation of
        // current i to decide which elements
        // to pick.
        for (var j = 0; j < n; j++)
            if (i & (1 << j))
                sum += arr[j];

        // check sum of picked elements.
        if (sum != 0 && num % sum != 0)
            return false;
    }
    return true;
}

// Function to check if a number is
// a super-niven number
function isSuperNivenNum(n)
{
    var temp = n;
    // to stor digits of N
    var digits = [];

    while (n != 0) {
        var digit = n % 10;
        digits.push(digit);
        n = parseInt(n / 10);
    }

    return isDivBySubsetSums(digits, temp);
}

// Driver code
var n = 500;
if (isSuperNivenNum(n))
    document.write("yes");
else
    document.write("No");

</script>
```

**Output:** 

```
yes
```