# 找到第 n 个纯数字

> 原文:[https://www.geeksforgeeks.org/find-the-nth-pure-number/](https://www.geeksforgeeks.org/find-the-nth-pure-number/)

给定一个整数 **N** ，任务是找到第 N 个[纯数](https://www.geeksforgeeks.org/find-the-first-n-pure-numbers/)。

> 一个纯数必须满足三个条件:
> 1)它的位数是偶数。
> 2)所有数字不是 4 就是 5。
> 3)数字是回文。
> 纯数字系列为:44、55、4444、4554、5445、5555、444444、445544、454454、455554 等等。

**示例:**

```
Input: 5
Output: 5445
Explanation: 
5445 is the 5th pure number in the series.

Input: 19
Output: 45444454
Explanation: 
45444454 is the 19th pure number in the series. 
```

**方法:**我们将假设 2 个数字组成一个单个块。每个区块有 2 个<sup>区块</sup>纯数字。对于 1 块的纯数字，有 2 个 <sup>1 个</sup>纯数字；对于有 2 个区块的编号，有 2 个 <sup>2 个</sup>编号，以此类推。

*   从 4 开始的纯数字，从位置 **2 <sup>块</sup>–1**开始，例如，4444 位于(2 <sup>2</sup> -1 = 3)，这意味着它位于系列中的第三个位置。
*   以 5 开头的纯数字从位置**2<sup>block</sup>+2<sup>(block-1)</sup>-1**开始，例如，5555 位于(2^2 + 2^1 -1 =5)，这意味着它位于系列中的第五个位置。

块中的纯数字基本上夹在两个 4 或 5 之间，并且是所有先前块数字的组合。为了更好地理解它，让我们考虑下面的例子:

*   第一个纯数是 44，第二个纯数是 55。
*   4444(“4”+“44”+“4”)44 来自前一个块
*   4554(“4”+“55”+“4”)55 来自前一个块
*   5445(“5”+“44”+“5”)44 来自前一个块
*   来自前一个块的 5555(“5”+“55”+“5”)55

这个模式对序列中的所有数字都重复。
**以下是上述方法的实施:**

## C++

```
#include<bits/stdc++.h>
using namespace std;

// CPP program to find
// the Nth pure num

// Function to check if it
// is a power of 2 or not
bool isPowerOfTwo(int N)
{
    double number = log(N)/log(2);
    int checker = int(number);
    return number - checker == 0;
}

// if a number belongs to 4 series
// it should lie between 2^blocks -1 to
// 2^blocks + 2^(blocks-1) -1
bool isSeriesFour(int N, int digits)
{
    int upperBound = int(pow(2, digits)+pow(2, digits - 1)-1);
    int lowerBound = int(pow(2, digits)-1);
    return (N >= lowerBound) && (N < upperBound);
}

// Method to find pure number
string getPureNumber(int N)
{
    string numbers[N + 1];

    numbers[0] = "";

    int blocks = 0;
    int displacement = 0;

    // Iterate from 1 to N
    for (int i = 1; i < N + 1; i++) {

        // Check if number is power of two
        if (isPowerOfTwo(i + 1)) {
            blocks = blocks + 1;
        }

        if (isSeriesFour(i, blocks)) {
            displacement
                = int(pow(2, blocks - 1));

            // Distance to previous
            // block numbers
            numbers[i] = "4" + numbers[i - displacement] + "4";
        }

        else {

            displacement = int(pow(2, blocks));

            // Distance to previous
            // block numbers
            numbers[i] = "5" + numbers[i - displacement] + "5";
        }
    }

    return numbers[N];
}

// Driver Code
int main()
{
    int N = 5;

    string pure = getPureNumber(N);

    cout << pure << endl;
}

// This code is contributed by Surendra_Gangwar
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find
// the Nth pure number

import java.io.*;

class PureNumbers {

    // Function to check if it
    // is a power of 2 or not
    public boolean isPowerOfTwo(int N)
    {
        double number
            = Math.log(N) / Math.log(2);
        int checker = (int)number;
        return number - checker == 0;
    }

    // if a number belongs to 4 series
    // it should lie between 2^blocks -1 to
    // 2^blocks + 2^(blocks-1) -1
    public boolean isSeriesFour(
        int N, int digits)
    {
        int upperBound
            = (int)(Math.pow(2, digits)
                    + Math.pow(2, digits - 1)
                    - 1);
        int lowerBound
            = (int)(Math.pow(2, digits)
                    - 1);
        return (N >= lowerBound)
            && (N < upperBound);
    }

    // Method to find pure number
    public String getPureNumber(int N)
    {
        String[] numbers
            = new String[N + 1];

        numbers[0] = "";

        int blocks = 0;
        int displacement = 0;

        // Iterate from 1 to N
        for (int i = 1; i < N + 1; i++) {

            // Check if number is power of two
            if (isPowerOfTwo(i + 1)) {
                blocks = blocks + 1;
            }

            if (isSeriesFour(i, blocks)) {
                displacement
                    = (int)Math.pow(
                        2, blocks - 1);

                // Distance to previous
                // block numbers
                numbers[i]
                    = "4"
                      + numbers[i - displacement]
                      + "4";
            }
            else {

                displacement
                    = (int)Math.pow(
                        2, blocks);

                // Distance to previous
                // block numbers
                numbers[i]
                    = "5"
                      + numbers[i - displacement]
                      + "5";
            }
        }

        return numbers[N];
    }

    // Driver Code
    public static void main(String[] args)
        throws Exception
    {
        int N = 5;

        // Create an object of the class
        PureNumbers ob = new PureNumbers();

        // Function call to find the
        // Nth pure number
        String pure = ob.getPureNumber(N);

        System.out.println(pure);
    }
}
```

## C#

```
// C# program to find
// the Nth pure number
using System;

class PureNumbers {

    // Function to check if it
    // is a power of 2 or not
    public bool isPowerOfTwo(int N)
    {
        double number
            = Math.Log(N) / Math.Log(2);
        int checker = (int)number;
        return number - checker == 0;
    }

    // if a number belongs to 4 series
    // it should lie between 2^blocks -1 to
    // 2^blocks + 2^(blocks-1) -1
    public bool isSeriesFour(
        int N, int digits)
    {
        int upperBound
            = (int)(Math.Pow(2, digits)
                    + Math.Pow(2, digits - 1)
                    - 1);
        int lowerBound
            = (int)(Math.Pow(2, digits)
                    - 1);
        return (N >= lowerBound)
            && (N < upperBound);
    }

    // Method to find pure number
    public string getPureNumber(int N)
    {
        string[] numbers
            = new string[N + 1];

        numbers[0] = "";

        int blocks = 0;
        int displacement = 0;

        // Iterate from 1 to N
        for (int i = 1; i < N + 1; i++) {

            // Check if number is power of two
            if (isPowerOfTwo(i + 1)) {
                blocks = blocks + 1;
            }

            if (isSeriesFour(i, blocks)) {
                displacement
                    = (int)Math.Pow(
                        2, blocks - 1);

                // Distance to previous
                // block numbers
                numbers[i]
                    = "4"
                      + numbers[i - displacement]
                      + "4";
            }
            else {

                displacement
                    = (int)Math.Pow(
                        2, blocks);

                // Distance to previous
                // block numbers
                numbers[i]
                    = "5"
                      + numbers[i - displacement]
                      + "5";
            }
        }

        return numbers[N];
    }

    // Driver Code
    public static void Main()
    {
        int N = 5;

        // Create an object of the class
        PureNumbers ob = new PureNumbers();

        // Function call to find the
        // Nth pure number
        string pure = ob.getPureNumber(N);

        Console.Write(pure);
    }
}

// This code is contributed by chitranayal
```

## java 描述语言

```
<script>
// Javascript program to find
// the Nth pure num

// Function to check if it
// is a power of 2 or not
function isPowerOfTwo(N)
{
    let number = Math.log(N)/Math.log(2);
    let checker = Math.floor(number);
    return number - checker == 0;
}

// if a number belongs to 4 series
// it should lie between 2^blocks -1 to
// 2^blocks + 2^(blocks-1) -1
function isSeriesFour(N, digits)
{
    let upperBound = Math.floor(Math.pow(2, digits) + Math.pow(2, digits - 1)-1);
    let lowerBound = Math.floor(Math.pow(2, digits)-1);
    return (N >= lowerBound) && (N < upperBound);
}

// Method to find pure number
function getPureNumber(N)
{
    let numbers = new Array(N + 1);

    numbers[0] = "";

    let blocks = 0;
    let displacement = 0;

    // Iterate from 1 to N
    for (let i = 1; i < N + 1; i++) {

        // Check if number is power of two
        if (isPowerOfTwo(i + 1)) {
            blocks = blocks + 1;
        }

        if (isSeriesFour(i, blocks)) {
            displacement
                = Math.floor(Math.pow(2, blocks - 1));

            // Distance to previous
            // block numbers
            numbers[i] = "4" + numbers[i - displacement] + "4";
        }

        else {

            displacement = Math.floor(Math.pow(2, blocks));

            // Distance to previous
            // block numbers
            numbers[i] = "5" + numbers[i - displacement] + "5";
        }
    }

    return numbers[N];
}

// Driver Code

let N = 5;

let pure = getPureNumber(N);

document.write(pure + "<br>");

// This code is contributed by _saurabh_jaiswal
</script>
```

**Output:** 

```
5445
```

时间复杂度:0(N)

辅助空间:O(N)