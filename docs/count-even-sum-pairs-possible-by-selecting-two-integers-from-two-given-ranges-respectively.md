# 通过分别从两个给定范围内选择两个整数来计算可能的偶和对

> 原文:[https://www . geeksforgeeks . org/count-even-sum-pairs-通过分别从两个给定范围中选择两个整数来可能/](https://www.geeksforgeeks.org/count-even-sum-pairs-possible-by-selecting-two-integers-from-two-given-ranges-respectively/)

给定两个正整数 **X** 和 **Y** ，任务是通过从范围 **1** 到 **X** 中选择任意一个整数以及从范围 **1** 到 **Y** 中选择另一个整数来计数可能具有偶数和的对。

**示例:**

> **输入:** X = 2，Y = 3
> **输出:** 3
> **解释:**所有这样的可能对都是{1，1}、{1，3}、{2，2}。

**方法:**按照以下步骤解决问题:

*   初始化一个变量，比如 **cntXEvenNums** ，将偶数的计数存储在**【1，X】**范围内，该范围是通过将 **X** 除以 **2** 得到的。
*   初始化一个变量，比如 **cntXOddNums** ，将奇数的计数存储在**【1，X】**范围内，该范围是通过将 **(X + 1)** 除以 **2** 得到的。
*   初始化一个变量，比如**cntyevenums**，通过将 **Y** 除以 **2** 来存储 **1** 到 **Y** 之间的偶数计数。
*   初始化一个变量，比如 **cntYOddNums** ，通过将 **(Y + 1)** 除以 **2** 来存储 **1** 到 **Y** 之间的奇数计数。
*   初始化一个变量，比如说 **cntPairs** ，通过将 **cntXEvenNums** 乘以**cntyevenums**并将 **cntXOddNums** 乘以 **cntYOddNums** 来存储偶和对的计数，并求两者的和。
*   最后，打印得到的 **cntPairs** 的值。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to count even
// sum pairs in the given range
long long cntEvenSumPairs(long long X, long long Y)
{
    // Stores the count of even
    // numbers between 1 to X
    long long cntXEvenNums = X / 2;

    // Stores the count of odd
    // numbers between 1 to X
    long long cntXOddNums = (X + 1) / 2;

    // Stores the count of even
    // numbers between 1 to Y
    long long cntYEvenNums = Y / 2;

    // Stores the count of odd
    // numbers between 1 to Y
    long long cntYOddNums = (Y + 1) / 2;

    // Stores the count of
    // pairs having even sum
    long long cntPairs
        = (cntXEvenNums * 1LL * cntYEvenNums)
          + (cntXOddNums * 1LL * cntYOddNums);

    // Retuens the count of pairs
    // having even sum
    return cntPairs;
}

// Driver Code
int main()
{
    long long X = 2;
    long long Y = 3;

    cout << cntEvenSumPairs(X, Y);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach

import java.io.*;

class GFG {

    // Function to count maximum  even
    // sum pairs in the given range
    static long cntEvenSumPairs(long X, long Y)
    {

        // Stores the count of even
        // numbers between 1 to X
        long cntXEvenNums = X / 2;

        // Stores the count of odd
        // numbers between 1 to X
        long cntXOddNums = (X + 1) / 2;

        // Stores the count of even
        // numbers between 1 to Y
        long cntYEvenNums = Y / 2;

        // Stores the count of odd
        // numbers between 1 to Y
        long cntYOddNums = (Y + 1) / 2;

        // Stores the count of
        // pairs having even sum
        long cntPairs = (cntXEvenNums * cntYEvenNums)
                        + (cntXOddNums * cntYOddNums);

        // Retuens the count of pairs
        // having even sum
        return cntPairs;
    }

    // Driver Code
    public static void main(String[] args)
    {
        long X = 2;
        long Y = 3;

        System.out.println(cntEvenSumPairs(X, Y));
    }
}
```

## 计算机编程语言

```
# Python program to implement
# the above approach

# Function to count even
# sum pairs in the given range
def cntEvenSumPairs(X, Y):

    # Stores the count of even
    # numbers between 1 to X
    cntXEvenNums = X / 2

    # Stores the count of odd
    # numbers between 1 to X
    cntXOddNums = (X + 1) / 2

    # Stores the count of even
    # numbers between 1 to Y
    cntYEvenNums = Y / 2

    # Stores the count of odd
    # numbers between 1 to Y
    cntYOddNums = (Y + 1) / 2

    # Stores the count of
    # pairs having even sum
    cntPairs = ((cntXEvenNums * cntYEvenNums) +
                 (cntXOddNums * cntYOddNums))

    # Returns the count of pairs
    # having even sum
    return cntPairs

# Driver code
X = 2
Y = 3

print(cntEvenSumPairs(X, Y))

# This code is contributed by hemanth gadarla
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG{

// Function to count maximum  even
// sum pairs in the given range
static long cntEvenSumPairs(long X, long Y)
{

    // Stores the count of even
    // numbers between 1 to X
    long cntXEvenNums = X / 2;

    // Stores the count of odd
    // numbers between 1 to X
    long cntXOddNums = (X + 1) / 2;

    // Stores the count of even
    // numbers between 1 to Y
    long cntYEvenNums = Y / 2;

    // Stores the count of odd
    // numbers between 1 to Y
    long cntYOddNums = (Y + 1) / 2;

    // Stores the count of
    // pairs having even sum
    long cntPairs = (cntXEvenNums * cntYEvenNums) +
                     (cntXOddNums * cntYOddNums);

    // Retuens the count of pairs
    // having even sum
    return cntPairs;
}

// Driver Code
public static void Main(string[] args)
{
    long X = 2;
    long Y = 3;

    Console.WriteLine(cntEvenSumPairs(X, Y));
}
}

// This code is contributed by chitranayal
```

## java 描述语言

```
<script>

// Javascript program to implement
// the above approach   

     // Function to count maximum even
    // sum pairs in the given range
    function cntEvenSumPairs(X , Y) {

        // Stores the count of even
        // numbers between 1 to X
        var cntXEvenNums = parseInt(X / 2);

        // Stores the count of odd
        // numbers between 1 to X
        var cntXOddNums = parseInt((X + 1) / 2);

        // Stores the count of even
        // numbers between 1 to Y
        var cntYEvenNums = parseInt(Y / 2);

        // Stores the count of odd
        // numbers between 1 to Y
        var cntYOddNums =parseInt( (Y + 1) / 2);

        // Stores the count of
        // pairs having even sum
        var cntPairs = (cntXEvenNums * cntYEvenNums) +
        (cntXOddNums * cntYOddNums);

        // Retuens the count of pairs
        // having even sum
        return cntPairs;
    }

    // Driver Code

        var X = 2;
        var Y = 3;

        document.write(cntEvenSumPairs(X, Y));

// This code contributed by Rajput-Ji

</script>
```

**Output:** 

```
3
```

***时间复杂度** : O(1)*
***辅助空间** : O(1)*