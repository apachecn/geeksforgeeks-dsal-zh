# 统计给定范围内奇数位为奇数，偶数位为偶数的数字

> 原文:[https://www . geesforgeks . org/count-numbers-from-给定范围-奇数位有奇数位和偶数位有偶数位/](https://www.geeksforgeeks.org/count-numbers-from-given-range-having-odd-digits-at-odd-places-and-even-digits-at-even-places/)

给定两个整数 **L** 和 **R** ，任务是从范围**【L，R】**中分别计数奇数位和偶数位的数字。

**示例:**

> **输入:** L = 3，R = 25
> **输出:** 9
> **说明:**满足条件的数字为 3、5、7、9、10、12、14、16、18。
> 
> **输入:** L = 128，R = 162
> **输出:** 7
> **说明:**满足条件的数字为 129、141、143、145、147、149、161。

**方法:**给定的问题可以基于以下观察来解决:

> 可以观察到，每个**偶数位置**都有 **5** 选择 **{0，2，4，6，8}** ，每个**奇数位置**也有 **5** 选择 **{1，3，5，7，9}** 。因此，每个职位都有 5 种可能。考虑到 **d** 是满足条件的任意数字中的位数， **D** 是 **N** 中的位数，可以进行以下观察:
> 
> *   **情况 1:** 如果 **d < D** ，则满足条件的由 **d** 个数字组成的总数的计数为**5<sup>D</sup>T9】，因为每个数字都有 **5** 个选择，做出的数字都将小于 **N** 。**
> *   **情况 2:** 如果 **D = d** ，那么满足长度 **d** 条件的总数计数为**5<sup>D</sup>T9】。但是超过 **N** 的数字需要丢弃，由以下决定:**
>     *   偶数的地方，如果**p<sup>th</sup>T3【地点】的数字是 **x** ，那么**(5—(x/2+1))* 5<sup>(D—p)</sup>**的数字大于 **N** 。**
>     *   奇数位，如果 **p <sup>th</sup>** 位中的数字为 **x** ，则**(5—(x+1)/2)* 5<sup>(D—p)</sup>**个数将大于 **N** 。

按照以下步骤解决问题:

*   定义一个函数 **countNumberUtill()** 来计算满足条件的范围**【1，N】**中的数字，其中 **N** 是一个自然数。
*   初始化一个整数变量，**计数**和[向量](https://www.geeksforgeeks.org/vector-in-cpp-stl/) **位数**来存储整数的位数 **N** 。
*   遍历给定数字的所有数字，即从 1 到 **D** ，并执行以下操作:
    *   将**5<sup>I</sup>T3】存储在变量中，说 **res** 。**
    *   从 **p = 1** 穿越到 **p = D** 并执行以下操作:
        *   初始化一个变量 **x** ，并在其中存储 **x =数字【p】**。
        *   如果 **p** 为偶数，则从 **res** 中减去**(5—(x/2+1))* 5<sup>(D—p)</sup>**。
        *   否则，从 **res** 中减去**(5—(x+1)/2)* 5<sup>(D—p)</sup>**。
*   将 **res** 添加到**计数**中。
*   返回**计数**。
*   打印**count numberutill(R)—count numberutill(L–1)**作为所需答案。

下面是上述方法的实现:

## C++

```
// C++ program to implement
// the above approach

#include <bits/stdc++.h>
using namespace std;

#define ll long long

// Function to calculate 5^p
ll getPower(int p)
{
    // Stores the result
    ll res = 1;

    // Multiply 5 p times
    while (p--) {
        res *= 5;
    }

    // Return the result
    return res;
}

// Function to count all numbers upto N
// having odd digits at odd places and
// even digits at even places
ll countNumbersUtil(ll N)
{
    // Stores the count
    ll count = 0;

    // Stores the digits of N
    vector<int> digits;

    // Insert the digits of N
    while (N) {
        digits.push_back(N % 10);
        N /= 10;
    }

    // Reverse the vector to arrange
    // the digits from first to last
    reverse(digits.begin(), digits.end());

    // Stores count of digits of n
    int D = digits.size();

    for (int i = 1; i <= D; i++) {

        // Stores the count of numbers
        // with i digits
        ll res = getPower(i);

        // If the last digit is reached,
        // subtract numbers eceeding range
        if (i == D) {

            // Iterate over all the places
            for (int p = 1; p <= D; p++) {

                // Stores the digit in the pth place
                int x = digits[p - 1];

                // Stores the count of numbers
                // having a digit greater than x
                // in the p-th position
                ll tmp = 0;

                // Calculate the count of numbers
                // exceeding the range if p is even
                if (p % 2 == 0) {
                    tmp = (5 - (x / 2 + 1))
                          * getPower(D - p);
                }

                // Calculate the count of numbers
                // exceeding the range if p is odd
                else {
                    tmp = (5 - (x + 1) / 2)
                          * getPower(D - p);
                }

                // Subtract the count of numbers
                // exceeding the range from total count
                res -= tmp;

                // If the parity of p and the
                // parity of x are not same
                if (p % 2 != x % 2) {
                    break;
                }
            }
        }

        // Add count of numbers having i digits
        // and satisfies the given conditions
        count += res;
    }

    // Return the total count of numbers till n
    return count;
}

// Function to calculate the count of numbers
// from given range having odd digits places
// and even digits at even places
void countNumbers(ll L, ll R)
{
    // Count of numbers in range [L, R] =
    // Count of numbers till R -
    cout << (countNumbersUtil(R)

             // Count of numbers till (L-1)
             - countNumbersUtil(L - 1))
         << endl;
}

// Driver Code
int main()
{
    ll L = 128, R = 162;
    countNumbers(L, R);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.util.*;
import java.util.Vector;
import java.util.Collections;

class GFG{

// Function to calculate 5^p
static int getPower(int p)
{

    // Stores the result
    int res = 1;

    // Multiply 5 p times
    while (p > 0)
    {
        res *= 5;
        p--;
    }

    // Return the result
    return res;
}

// Function to count all numbers upto N
// having odd digits at odd places and
// even digits at even places
static int countNumbersUtil(int N)
{

    // Stores the count
    int count = 0;

    // Stores the digits of N
    Vector<Integer> digits = new Vector<Integer>();

    // Insert the digits of N
    while (N > 0)
    {
        digits.add(N % 10);
        N /= 10;
    }

    // Reverse the vector to arrange
    // the digits from first to last
    Collections.reverse(digits);

    // Stores count of digits of n
    int D = digits.size();

    for(int i = 1; i <= D; i++)
    {

        // Stores the count of numbers
        // with i digits
        int res = getPower(i);

        // If the last digit is reached,
        // subtract numbers eceeding range
        if (i == D)
        {

            // Iterate over all the places
            for(int p = 1; p <= D; p++)
            {

                // Stores the digit in the pth place
                int x = digits.get(p - 1);

                // Stores the count of numbers
                // having a digit greater than x
                // in the p-th position
                int tmp = 0;

                // Calculate the count of numbers
                // exceeding the range if p is even
                if (p % 2 == 0)
                {
                    tmp = (5 - (x / 2 + 1)) *
                           getPower(D - p);
                }

                // Calculate the count of numbers
                // exceeding the range if p is odd
                else
                {
                    tmp = (5 - (x + 1) / 2) *
                       getPower(D - p);
                }

                // Subtract the count of numbers
                // exceeding the range from total count
                res -= tmp;

                // If the parity of p and the
                // parity of x are not same
                if (p % 2 != x % 2)
                {
                    break;
                }
            }
        }

        // Add count of numbers having i digits
        // and satisfies the given conditions
        count += res;
    }

    // Return the total count of numbers till n
    return count;
}

// Function to calculate the count of numbers
// from given range having odd digits places
// and even digits at even places
static void countNumbers(int L, int R)
{

    // Count of numbers in range [L, R] =
    // Count of numbers till R -
    System.out.println(countNumbersUtil(R) -

                       // Count of numbers till (L-1)
                       countNumbersUtil(L - 1));
}

// Driver Code
public static void main(String args[])
{
    int L = 128, R = 162;

    countNumbers(L, R);
}
}

// This code is contributed by ipg2016107
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach

# Function to calculate 5^p
def getPower(p) :

    # Stores the result
    res = 1

    # Multiply 5 p times
    while (p) :
        res *= 5
        p -= 1

    # Return the result
    return res

# Function to count anumbers upto N
# having odd digits at odd places and
# even digits at even places
def countNumbersUtil(N) :

    # Stores the count
    count = 0

    # Stores the digits of N
    digits = []

    # Insert the digits of N
    while (N) :
        digits.append(N % 10)
        N //= 10

    # Reverse the vector to arrange
    # the digits from first to last
    digits.reverse() 

    # Stores count of digits of n
    D = len(digits)

    for i in range(1, D + 1, 1) :

        # Stores the count of numbers
        # with i digits
        res = getPower(i)

        # If the last digit is reached,
        # subtract numbers eceeding range
        if (i == D) :

            # Iterate over athe places
            for p in range(1, D + 1, 1) :

                # Stores the digit in the pth place
                x = digits[p - 1]

                # Stores the count of numbers
                # having a digit greater than x
                # in the p-th position
                tmp = 0

                # Calculate the count of numbers
                # exceeding the range if p is even
                if (p % 2 == 0) :
                    tmp = ((5 - (x // 2 + 1))
                            * getPower(D - p))

                # Calculate the count of numbers
                # exceeding the range if p is odd
                else :
                    tmp = ((5 - (x + 1) // 2)
                            * getPower(D - p))

                # Subtract the count of numbers
                # exceeding the range from total count
                res -= tmp

                # If the parity of p and the
                # parity of x are not same
                if (p % 2 != x % 2) :
                    break

        # Add count of numbers having i digits
        # and satisfies the given conditions
        count += res

    # Return the total count of numbers tin
    return count

# Function to calculate the count of numbers
# from given range having odd digits places
# and even digits at even places
def countNumbers(L, R) :

    # Count of numbers in range [L, R] =
    # Count of numbers tiR -
    print(countNumbersUtil(R)

             # Count of numbers ti(L-1)
            - countNumbersUtil(L - 1))

# Driver Code

L = 128
R = 162

countNumbers(L, R) 

# This code is contributed by code_hunt
```

## C#

```
// C# program for
// the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to calculate 5^p
static int getPower(int p)
{

    // Stores the result
    int res = 1;

    // Multiply 5 p times
    while (p > 0)
    {
        res *= 5;
        p--;
    }

    // Return the result
    return res;
}

// Function to count all numbers upto N
// having odd digits at odd places and
// even digits at even places
static int countNumbersUtil(int N)
{

    // Stores the count
    int count = 0;

    // Stores the digits of N
    List<int> digits = new List<int>();

    // Insert the digits of N
    while (N > 0)
    {
        digits.Add(N % 10);
        N /= 10;
    }

    // Reverse the vector to arrange
    // the digits from first to last
    digits.Reverse();

    // Stores count of digits of n
    int D = digits.Count;

    for(int i = 1; i <= D; i++)
    {

        // Stores the count of numbers
        // with i digits
        int res = getPower(i);

        // If the last digit is reached,
        // subtract numbers eceeding range
        if (i == D)
        {

            // Iterate over all the places
            for(int p = 1; p <= D; p++)
            {

                // Stores the digit in the pth place
                int x = digits[p - 1];

                // Stores the count of numbers
                // having a digit greater than x
                // in the p-th position
                int tmp = 0;

                // Calculate the count of numbers
                // exceeding the range if p is even
                if (p % 2 == 0)
                {
                    tmp = (5 - (x / 2 + 1)) *
                           getPower(D - p);
                }

                // Calculate the count of numbers
                // exceeding the range if p is odd
                else
                {
                    tmp = (5 - (x + 1) / 2) *
                       getPower(D - p);
                }

                // Subtract the count of numbers
                // exceeding the range from total count
                res -= tmp;

                // If the parity of p and the
                // parity of x are not same
                if (p % 2 != x % 2)
                {
                    break;
                }
            }
        }

        // Add count of numbers having i digits
        // and satisfies the given conditions
        count += res;
    }

    // Return the total count of numbers till n
    return count;
}

// Function to calculate the count of numbers
// from given range having odd digits places
// and even digits at even places
static void countNumbers(int L, int R)
{

    // Count of numbers in range [L, R] =
    // Count of numbers till R -
    Console.WriteLine(countNumbersUtil(R) -

                       // Count of numbers till (L-1)
                       countNumbersUtil(L - 1));
}

// Driver Code
public static void Main(String[] args)
{
    int L = 128, R = 162;

    countNumbers(L, R);
}
}

// This code is contributed by jana_sayantan
```

## java 描述语言

```
<script>

// JavaScript  Program for the above approach

// Function to calculate 5^p
function getPower(p)
{
    // Stores the result
    var res = 1;

    // Multiply 5 p times
    while (p--) {
        res *= 5;
    }

    // Return the result
    return res;
}

// Function to count all numbers upto N
// having odd digits at odd places and
// even digits at even places
function countNumbersUtil( N)
{
    // Stores the count
    var count = 0;

    // Stores the digits of N
    var digits= [];

    // Insert the digits of N
    while (N) {
        digits.push(N % 10);
        N = parseInt(N / 10);
    }

    // Reverse the vector to arrange
    // the digits from first to last
    digits.reverse();

    // Stores count of digits of n
    var D = digits.length;

    for (var i = 1; i <= D; i++) {

        // Stores the count of numbers
        // with i digits
        var res = getPower(i);

        // If the last digit is reached,
        // subtract numbers eceeding range
        if (i == D) {

            // Iterate over all the places
            for (var p = 1; p <= D; p++) {

                // Stores the digit in the pth place
                var x = digits[p - 1];

                // Stores the count of numbers
                // having a digit greater than x
                // in the p-th position
                var tmp = 0;

                // Calculate the count of numbers
                // exceeding the range if p is even
                if (p % 2 == 0) {
                    tmp = (5 - parseInt(x / (2 + 1)))
                          * getPower(D - p);
                }

                // Calculate the count of numbers
                // exceeding the range if p is odd
                else {
                    tmp = (5 - parseInt( (x + 1) / 2))
                          * getPower(D - p);
                }

                // Subtract the count of numbers
                // exceeding the range from total count
                res -= tmp;

                // If the parity of p and the
                // parity of x are not same
                if (p % 2 != x % 2) {
                    break;
                }
            }
        }

        // Add count of numbers having i digits
        // and satisfies the given conditions
        count += res;
    }

    // Return the total count of numbers till n
    return count;
}

// Function to calculate the count of numbers
// from given range having odd digits places
// and even digits at even places
function countNumbers(L, R)
{
    // Count of numbers in range [L, R] =
    // Count of numbers till R -
    document.write( (countNumbersUtil(R)

             // Count of numbers till (L-1)
             - countNumbersUtil(L - 1)) + "<br>");
}

var L = 128, R = 162;
countNumbers(L, R);

// This code is contributed by SoumikMondal

</script>
```

**Output:** 

```
7
```

***时间复杂度:** O(N <sup>2</sup> ，其中 N 为 R*
***中的位数辅助空间:** O(N)*