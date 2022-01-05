# 对一个数的数字进行逐位运算

> 原文:[https://www . geeksforgeeks . org/按位数字运算/](https://www.geeksforgeeks.org/bitwise-operations-on-digits-of-a-number/)

给定一个数字 **N** ，任务是对给定数字 **N** 的数字执行按位运算。位运算包括:

*   求给定数 **N** 所有数字的异或
*   求给定数 **N** 所有数字的或
*   求给定数 **N** 所有数字的与

**例:**

```
Input: N = 486
Output: 
XOR = 10
OR = 14
AND = 0

Input: N = 123456
Output: 
XOR = 10
OR = 14
AND = 0
```

**进场:**

1.  获取号码

2.  [找到数字](https://www.geeksforgeeks.org/program-count-digits-integer-3-different-methods/)的位数，并将其存储在数组中，以便计算。

3.  现在对这个数组逐一执行各种[位操作](https://www.geeksforgeeks.org/bitwise-algorithms/) ( [异或](https://www.geeksforgeeks.org/tag/xor/)、[或](https://www.geeksforgeeks.org/tag/bitwise-or/)、[和](https://www.geeksforgeeks.org/tag/bitwise-and/))。

以下是上述方法的实现:

## C++

```
// C++ implementation of the approach

#include <bits/stdc++.h>
using namespace std;

int digit[100000];

// Function to find the digits
int findDigits(int n)
{
    int count = 0;

    while (n != 0) {

        digit[count] = n % 10;
        n = n / 10;
        ++count;
    }

    return count;
}

// Function to Find OR
// of all digits of a number
int OR_of_Digits(int n, int count)
{

    int ans = 0;

    for (int i = 0; i < count; i++) {
        // Find OR of all digits
        ans = ans | digit[i];
    }

    // return OR of digits
    return ans;
}

// Function to Find AND
// of all digits of a number
int AND_of_Digits(int n, int count)
{

    int ans = 0;

    for (int i = 0; i < count; i++) {
        // Find AND of all digits
        ans = ans & digit[i];
    }

    // return AND of digits
    return ans;
}

// Function to Find XOR
// of all digits of a number
int XOR_of_Digits(int n, int count)
{

    int ans = 0;

    for (int i = 0; i < count; i++) {
        // Find XOR of all digits
        ans = ans ^ digit[i];
    }

    // return XOR of digits
    return ans;
}

// Driver code
void bitwise_operation(int N)
{

    // Find and store all digits
    int countOfDigit = findDigits(N);

    // Find XOR of digits
    cout << "XOR = "
         << XOR_of_Digits(N, countOfDigit)
         << endl;

    // Find OR of digits
    cout << "OR = "
         << OR_of_Digits(N, countOfDigit)
         << endl;

    // Find AND of digits
    cout << "AND = "
         << AND_of_Digits(N, countOfDigit)
         << endl;
}

// Driver code
int main()
{

    int N = 123456;

    bitwise_operation(N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG{

static int []digit = new int[100000];

// Function to find the digits
static int findDigits(int n)
{
    int count = 0;

    while (n != 0) {

        digit[count] = n % 10;
        n = n / 10;
        ++count;
    }

    return count;
}

// Function to Find OR
// of all digits of a number
static int OR_of_Digits(int n, int count)
{

    int ans = 0;

    for (int i = 0; i < count; i++) {

        // Find OR of all digits
        ans = ans | digit[i];
    }

    // return OR of digits
    return ans;
}

// Function to Find AND
// of all digits of a number
static int AND_of_Digits(int n, int count)
{

    int ans = 0;

    for (int i = 0; i < count; i++) {

        // Find AND of all digits
        ans = ans & digit[i];
    }

    // return AND of digits
    return ans;
}

// Function to Find XOR
// of all digits of a number
static int XOR_of_Digits(int n, int count)
{

    int ans = 0;

    for (int i = 0; i < count; i++) {

        // Find XOR of all digits
        ans = ans ^ digit[i];
    }

    // return XOR of digits
    return ans;
}

// Driver code
static void bitwise_operation(int N)
{

    // Find and store all digits
    int countOfDigit = findDigits(N);

    // Find XOR of digits
    System.out.print("XOR = "
        + XOR_of_Digits(N, countOfDigit)
        +"\n");

    // Find OR of digits
    System.out.print("OR = "
        + OR_of_Digits(N, countOfDigit)
        +"\n");

    // Find AND of digits
    System.out.print("AND = "
        + AND_of_Digits(N, countOfDigit)
        +"\n");
}

// Driver code
public static void main(String[] args)
{

    int N = 123456;

    bitwise_operation(N);
}
}

// This code is contributed by sapnasingh4991
```

## 蟒蛇 3

```
# Python 3 implementation of the approach
digit = [0]*(100000)

# Function to find the digits
def findDigits(n):
    count = 0

    while (n != 0):

        digit[count] = n % 10;
        n = n // 10;
        count += 1

    return count

# Function to Find OR
# of all digits of a number
def OR_of_Digits( n,count):
    ans = 0

    for i in range(count):

        # Find OR of all digits
        ans = ans | digit[i]

    # return OR of digits
    return ans

# Function to Find AND
# of all digits of a number
def AND_of_Digits(n, count):

    ans = 0

    for i in range(count):

        # Find AND of all digits
        ans = ans & digit[i]

    # return AND of digits
    return ans

# Function to Find XOR
# of all digits of a number
def XOR_of_Digits(n, count):

    ans = 0

    for i in range(count):

        # Find XOR of all digits
        ans = ans ^ digit[i]

    # return XOR of digits
    return ans

# Driver code
def bitwise_operation( N):

    # Find and store all digits
    countOfDigit = findDigits(N)

    # Find XOR of digits
    print("XOR = ",XOR_of_Digits(N, countOfDigit))

    # Find OR of digits
    print("OR = ",OR_of_Digits(N, countOfDigit))

    # Find AND of digits
    print("AND = ",AND_of_Digits(N, countOfDigit))

# Driver code
N = 123456;
bitwise_operation(N)

# This code is contributed by apurva raj
```

## C#

```
// C# implementation of the approach
using System;

class GFG{

static int []digit = new int[100000];

// Function to find the digits
static int findDigits(int n)
{
    int count = 0;

    while (n != 0) {

        digit[count] = n % 10;
        n = n / 10;
        ++count;
    }

    return count;
}

// Function to Find OR
// of all digits of a number
static int OR_of_Digits(int n, int count)
{

    int ans = 0;

    for (int i = 0; i < count; i++) {

        // Find OR of all digits
        ans = ans | digit[i];
    }

    // return OR of digits
    return ans;
}

// Function to Find AND
// of all digits of a number
static int AND_of_Digits(int n, int count)
{

    int ans = 0;

    for (int i = 0; i < count; i++) {

        // Find AND of all digits
        ans = ans & digit[i];
    }

    // return AND of digits
    return ans;
}

// Function to Find XOR
// of all digits of a number
static int XOR_of_Digits(int n, int count)
{

    int ans = 0;

    for (int i = 0; i < count; i++) {

        // Find XOR of all digits
        ans = ans ^ digit[i];
    }

    // return XOR of digits
    return ans;
}

// Driver code
static void bitwise_operation(int N)
{

    // Find and store all digits
    int countOfDigit = findDigits(N);

    // Find XOR of digits
    Console.Write("XOR = "
        + XOR_of_Digits(N, countOfDigit)
        +"\n");

    // Find OR of digits
    Console.Write("OR = "
        + OR_of_Digits(N, countOfDigit)
        +"\n");

    // Find AND of digits
    Console.Write("AND = "
        + AND_of_Digits(N, countOfDigit)
        +"\n");
}

// Driver code
public static void Main(String[] args)
{

    int N = 123456;

    bitwise_operation(N);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

let digit = [];

// Function to find the digits
function findDigits(n)
{
    let count = 0;

    while (n != 0) {

        digit[count] = n % 10;
        n = n / 10;
        ++count;
    }

    return count;
}

// Function to Find OR
// of all digits of a number
function OR_of_Digits(n, count)
{

    let ans = 0;

    for (let i = 0; i < count; i++) {

        // Find OR of all digits
        ans = ans | digit[i];
    }

    // return OR of digits
    return ans;
}

// Function to Find AND
// of all digits of a number
function AND_of_Digits(n, count)
{

    let ans = 0;

    for (let i = 0; i < count; i++) {

        // Find AND of all digits
        ans = ans & digit[i];
    }

    // return AND of digits
    return ans;
}

// Function to Find XOR
// of all digits of a number
function XOR_of_Digits(n, count)
{

    let ans = 0;

    for (let i = 0; i < count; i++) {

        // Find XOR of all digits
        ans = ans ^ digit[i];
    }

    // return XOR of digits
    return ans;
}

// Driver code
function bitwise_operation(N)
{

    // Find and store all digits
    let countOfDigit = findDigits(N);

    // Find XOR of digits
    document.write("XOR = "
        + XOR_of_Digits(N, countOfDigit)
         + "<br/>");

    // Find OR of digits
    document.write("OR = "
        + OR_of_Digits(N, countOfDigit)
        + "<br/>");

    // Find AND of digits
    document.write("AND = "
        + AND_of_Digits(N, countOfDigit)
        + "<br/>");
}

// Driver Code

    let N = 123456;

    bitwise_operation(N);

</script>
```

**Output:** 

```
XOR = 7
OR = 7
AND = 0
```

**时间复杂度:**O(logN)
T3】辅助空间: O(logN)