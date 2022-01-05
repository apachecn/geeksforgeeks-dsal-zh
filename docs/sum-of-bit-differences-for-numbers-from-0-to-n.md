# 从 0 到 N 的数字的位差之和

> 原文:[https://www . geesforgeks . org/0 到 n 的数字位差总和/](https://www.geeksforgeeks.org/sum-of-bit-differences-for-numbers-from-0-to-n/)

给定一个数字 **N** ，任务是为从 **0 到 N** 的每个连续数字计算二进制表示中对应不同位的[总数。
**举例:**](https://www.geeksforgeeks.org/number-of-mismatching-bits-in-the-binary-representation-of-two-integers/) 

> **输入:** N = 5
> **输出:** 8
> **解释:**
> 数字的二进制表示为:
> 0 - > 000、
> 1 - > 001、
> 2 - > 010、
> 3 - > 011、
> 4 - > 100、
> 5->101
> 1 和 0 之间- > 1 位不同
> 2 和 1 之间- > 2 位不同
> 3 和 2 之间- > 1 位不同
> 4 和 3 之间- > 3 位不同
> 5 和 4 之间- > 1 位不同
> T21 总计= 1+2+1+3+1 = 8
> T24

**天真方法:**想法是从 **0 迭代到 N** ，对于每对连续的元素，使用本文[中讨论的方法找到每对元素的不同位数。
**时间复杂度:** *O(N*log N)*
**辅助空间:** *(1)*
**高效进场:**对于高效进场我们要观察以下几点:](https://www.geeksforgeeks.org/number-of-mismatching-bits-in-the-binary-representation-of-two-integers/) 

```
number:   1 2 3 4 5 6  7  8
bit_diff: 1 2 1 3 1 2  1  4
sum_diff: 1 3 4 7 8 10 11 15
```

从上面的计算我们可以观察到以下情况:

1.  如果 **N** 是 2 的完美幂，那么从 **0 到 N** 对应的不同位的总和由:
    给出

> sum_diff = (2 <sup>x+1</sup> -1)
> 其中 x = log2(N)

2.  如果 **N** 不是 2 的完美幂，那么它可以表示为 2 的完美幂之和为:

> n = 2<sup>a</sup>+2<sup>b</sup>+…+2<sup>x</sup>T6】

1.  因此 **0 到 N** 对应的不同位的总和可以计算为:

> sum _ diff =(2<sup>a+1</sup>-1)+(2<sup>b+1</sup>-1)+…+(2<sup>x+1</sup>-1)。

**例如:**

> 如果 N = 8，那么
> 8 的二进制表示为“1000”
> 因此 11 = 2<sup>3</sup>T4】总计数=(2<sup>3+1</sup>–1)
> 总计数= 8–1 = 7。
> 如果 N = 11，则【T11 的二进制表示为“1011”
> 因此 11 = 2<sup>3</sup>+2<sup>1</sup>+2<sup>0</sup>
> =>总计数=(2<sup>3+1</sup>–1)+(2<sup>1+1</sup>–1)+(2<sup>0+1</sup>–2

以下是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to implement fast
// exponentiation
int binpow(int a, int b)
{
    int res = 1;

    while (b) {
        if (b & 1)
            res = res * a;
        a = a * a;
        b /= 2;
    }
    return res;
}

// Function to return the value
// for powers of 2
int find(int x)
{
    if (x == 0)
        return 0;
    int p = log2(x);
    return binpow(2, p + 1) - 1;
}

// Function to convert N into binary
string getBinary(int n)
{
    // To store binary representation
    string ans = "";

    // Iterate each digit of n
    while (n) {
        int dig = n % 2;
        ans += to_string(dig);
        n /= 2;
    }

    // Return binary representation
    return ans;
}

// Function to find difference in bits
int totalCountDifference(int n)
{
    // Get binary representation
    string ans = getBinary(n);

    // total number of bit
    // differences from 0 to N
    int req = 0;

    // Iterate over each binary bit
    for (int i = 0; i < ans.size(); i++) {

        // If current bit is '1' then add
        // the count of current bit
        if (ans[i] == '1') {

            req += find(binpow(2, i));
        }
    }
    return req;
}

// Driver Code
int main()
{
    // Given Number
    int N = 5;

    // Function Call
    cout << totalCountDifference(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.io.*;
import java.lang.Math;

class GFG{

// Function to implement fast
// exponentiation
static int binpow(int a, int b)
{
    int res = 1;

    while (b > 0)
    {
        if (b % 2 == 1)
            res = res * a;
        a = a * a;
        b /= 2;
    }
    return res;
}

// Function to return the
// value for powers of 2
static int find(int x)
{
    if (x == 0)
        return 0;

    int p = (int)(Math.log(x) / Math.log(2));
    return binpow(2, p + 1) - 1;
}

// Function to convert N into binary
static String getBinary(int n)
{

    // To store the binary representation
    String ans = "";

    // Iterate each digit of n
    while (n > 0)
    {
        int dig = n % 2;
        ans += dig;
        n /= 2;
    }

    // Return binary representation
    return ans;
}

// Function to find difference in bits
static int totalCountDifference(int n)
{

    // Get binary representation
    String ans = getBinary(n);

    // total number of bit
    // differences from 0 to N
    int req = 0;

    // Iterate over each binary bit
    for(int i = 0; i < ans.length(); i++)
    {

       // If current bit is '1' then add
       // the count of current bit
       if (ans.charAt(i) == '1')
       {
           req += find(binpow(2, i));
       }
    }
    return req;
}

// Driver code
public static void main (String[] args)
{
    // Given number
    int n = 5;

    System.out.print(totalCountDifference(n));
}
}

// This code is contributed by spp____
```

## 蟒蛇 3

```
# Python3 program for the above approach
from math import log

# Function to implement fast
# exponentiation
def binpow(a, b):

    res = 1
    while (b > 0):
        if (b % 2 == 1):
            res = res * a
        a = a * a
        b //= 2
    return res

# Function to return the value
# for powers of 2
def find(x):

    if (x == 0):
        return 0
    p = log(x) / log(2)
    return binpow(2, p + 1) - 1

# Function to convert N into binary
def getBinary(n):

    # To store binary representation
    ans = ""

    # Iterate each digit of n
    while (n > 0):
        dig = n % 2
        ans += str(dig)
        n //= 2

    # Return binary representation
    return ans

# Function to find difference in bits
def totalCountDifference(n):

    # Get binary representation
    ans = getBinary(n)

    # total number of bit
    # differences from 0 to N
    req = 0

    # Iterate over each binary bit
    for i in range(len(ans)):

        # If current bit is '1' then add
        # the count of current bit
        if (ans[i] == '1'):
            req += find(binpow(2, i))
    return req

# Driver Code

# Given Number
N = 5

# Function Call
print(totalCountDifference(N))

# This code is contributed by shubhamsingh10
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to implement fast
// exponentiation
static int binpow(int a, int b)
{
    int res = 1;

    while (b > 0)
    {
        if (b % 2 == 1)
            res = res * a;
        a = a * a;
        b /= 2;
    }
    return res;
}

// Function to return the
// value for powers of 2
static int find(int x)
{
    if (x == 0)
        return 0;

    int p = (int)(Math.Log(x) / Math.Log(2));
    return binpow(2, p + 1) - 1;
}

// Function to convert N into binary
static String getBinary(int n)
{

    // To store the binary representation
    String ans = "";

    // Iterate each digit of n
    while (n > 0)
    {
        int dig = n % 2;
        ans += dig;
        n /= 2;
    }

    // Return binary representation
    return ans;
}

// Function to find difference in bits
static int totalCountDifference(int n)
{

    // Get binary representation
    string ans = getBinary(n);

    // total number of bit
    // differences from 0 to N
    int req = 0;

    // Iterate over each binary bit
    for(int i = 0; i < ans.Length; i++)
    {

       // If current bit is '1' then add
       // the count of current bit
       if (ans[i] == '1')
       {
           req += find(binpow(2, i));
       }
    }
    return req;
}

// Driver code
public static void Main()
{
    // Given number
    int n = 5;

    Console.Write(totalCountDifference(n));
}
}

// This code is contributed by Nidhi_biet
```

## java 描述语言

```
<script>
// Javascript program for the above approach\

// Function to implement fast
// exponentiation
function binpow(a, b) {
    let res = 1;

    while (b) {
        if (b & 1)
            res = res * a;
        a = a * a;
        b = Math.floor(b / 2);
    }
    return res;
}

// Function to return the value
// for powers of 2
function find(x) {
    if (x == 0)
        return 0;
    let p = Math.log2(x);
    return binpow(2, p + 1) - 1;
}

// Function to convert N into binary
function getBinary(n) {
    // To store binary representation
    let ans = "";

    // Iterate each digit of n
    while (n) {
        let dig = n % 2;
        ans += String(dig);
        n = Math.floor(n / 2);
    }

    // Return binary representation
    return ans;
}

// Function to find difference in bits
function totalCountDifference(n)
{

    // Get binary representation
    let ans = getBinary(n);

    // total number of bit
    // differences from 0 to N
    let req = 0;

    // Iterate over each binary bit
    for (let i = 0; i < ans.length; i++) {

        // If current bit is '1' then add
        // the count of current bit
        if (ans[i] == '1') {

            req += find(binpow(2, i));
        }
    }
    return req;
}

// Driver Code

// Given Number
let N = 5;

// Function Call
document.write(totalCountDifference(N));

// This code is contributed by _saurabh_jaiswal
</script>
```

**Output:** 

```
8
```

**时间复杂度:***O((log N)<sup>2</sup>)*
**辅助空间:** *(1)*