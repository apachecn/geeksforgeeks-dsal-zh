# 打印给定范围内所有数字严格递增的数字

> 原文:[https://www . geesforgeks . org/print-给定范围内的所有数字都有严格递增顺序的数字/](https://www.geeksforgeeks.org/print-all-numbers-in-given-range-having-digits-in-strictly-increasing-order/)

给定两个正整数 **L** 和 **R** ，任务是打印**【L，R】**范围内的数字，这些数字的位数严格递增。

**示例:**

> **输入:** L = 10，R = 15
> **输出:** 12 13 14 15
> **说明:**
> 在[10，15]范围内，只有数字{12，13，14，15}的位数是严格递增的。
> 
> **输入:** L = 60，R = 70
> **输出:** 67 68 69
> **说明:**
> 在【60，70】范围内，只有数字{67，68，69}的位数是严格递增的。

**方法:**思路是迭代范围**【L，R】**，对于该范围内的每个数字，检查该数字的位数是否严格递增。如果是，则打印该号码，否则检查下一个号码。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print all numbers
// in the range [L, R] having digits
// in strictly increasing order
void printNum(int L, int R)
{
    // Iterate over the range
    for (int i = L; i <= R; i++) {

        int temp = i;
        int c = 10;
        int flag = 0;

        // Iterate over the digits
        while (temp > 0) {

            // Check if the current digit
            // is >= the previous digit
            if (temp % 10 >= c) {

                flag = 1;
                break;
            }

            c = temp % 10;
            temp /= 10;
        }

        // If the digits are in
        // ascending order
        if (flag == 0)
            cout << i << " ";
    }
}

// Driver Code
int main()
{
// Given range L and R
    int L = 10, R = 15;

// Function Call
    printNum(L, R);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;

class GFG{

// Function to print all numbers
// in the range [L, R] having digits
// in strictly increasing order
static void printNum(int L, int R)
{

    // Iterate over the range
    for(int i = L; i <= R; i++)
    {
        int temp = i;
        int c = 10;
        int flag = 0;

        // Iterate over the digits
        while (temp > 0)
        {

            // Check if the current digit
            // is >= the previous digit
            if (temp % 10 >= c)
            {
                flag = 1;
                break;
            }

            c = temp % 10;
            temp /= 10;
        }

        // If the digits are in
        // ascending order
        if (flag == 0)
            System.out.print(i + " ");
    }
}

// Driver code
public static void main(String[] args)
{

    // Given range L and R
    int L = 10, R = 15;

    // Function call
    printNum(L, R);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program for the above approach

# Function to print all numbers in
# the range [L, R] having digits
# in strictly increasing order
def printNum(L, R):

    # Iterate over the range
    for i in range(L, R + 1):
        temp = i
        c = 10
        flag = 0

        # Iterate over the digits
        while (temp > 0):

            # Check if the current digit
            # is >= the previous digit
            if (temp % 10 >= c):
                flag = 1
                break

            c = temp % 10
            temp //= 10

        # If the digits are in
        # ascending order
        if (flag == 0):
            print(i, end = " ")

# Driver Code

# Given range L and R
L = 10
R = 15

# Function call
printNum(L, R)

# This code is contributed by code_hunt
```

## C#

```
// C# program for the above approach
using System;

class GFG{

// Function to print all numbers
// in the range [L, R] having digits
// in strictly increasing order
static void printNum(int L, int R)
{

    // Iterate over the range
    for(int i = L; i <= R; i++)
    {
        int temp = i;
        int c = 10;
        int flag = 0;

        // Iterate over the digits
        while (temp > 0)
        {

            // Check if the current digit
            // is >= the previous digit
            if (temp % 10 >= c)
            {
                flag = 1;
                break;
            }

            c = temp % 10;
            temp /= 10;
        }

        // If the digits are in
        // ascending order
        if (flag == 0)
            Console.Write(i + " ");
    }
}

// Driver Code
public static void Main()
{

    // Given range L and R
    int L = 10, R = 15;

    // Function call
    printNum(L, R);
}
}

// This code is contributed by jrishabh99
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to print all numbers
// in the range [L, R] having digits
// in strictly increasing order
function printNum(L, R)
{

    // Iterate over the range
    for(let i = L; i <= R; i++)
    {
        let temp = i;
        let c = 10;
        let flag = 0;

        // Iterate over the digits
        while (temp > 0)
        {

            // Check if the current digit
            // is >= the previous digit
            if (temp % 10 >= c)
            {
                flag = 1;
                break;
            }
            c = temp % 10;
            temp /= 10;
        }

        // If the digits are in
        // ascending order
        if (flag == 0)
            document.write(i + " ");
    }
}

// Driver code

// Given range L and R
let L = 10, R = 15;

// Function call
printNum(L, R);

// This code is contributed by sravan kumar

</script>
```

**Output:** 

```
12 13 14 15
```

***时间复杂度** O(N)，N 是 L 和 r 的绝对差*
***辅助空间:** O(1)*