# 位于 Q 查询的[L，R]范围内的所有完美立方体的总和

> 原文:[https://www . geesforgeks . org/all-sum-of-perfect-cubes-in-range-l-r-for-q-query/](https://www.geeksforgeeks.org/sum-of-all-perfect-cubes-lying-in-the-range-l-r-for-q-queries/)

给定以 2D 数组**arr【】【】**形式的 **Q** 查询，其每行由两个数字 **L** 和表示范围【L，R】的 **R** 组成，任务是找到位于该范围内的所有[完美立方体](https://www.geeksforgeeks.org/perfect-cubes-range/)的总和。
**举例:**

> **输入:** Q = 2，arr[][] = {{4，9}，{4，44}}
> **输出:** 8 35
> 从 4 到 9:只有 8 是完美立方体。所以 8 是 ans
> 从 4 到 44: 8，27 是完美立方体。因此，8 + 27 = 35
> **输入:** Q = 4，arr[][] = {{ 1，10 }，{ 1，100 }，{ 2，25 }，{ 4，50 }}
> **输出:** 9 100 8 35

**方法:**思路是使用一个[前缀和数组](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)。

1.  所有立方的总和被预先计算并存储在数组 pref[]中，以便每个查询都可以在 O(1)时间内得到回答。
2.  pref[]数组中的第 i <sup>个</sup>索引代表从 1 到该数字的完美立方体的总和。
3.  因此，从给定范围“L”到“R”的完美立方体的和可以从前缀和数组 pref[]中找到。

以下是上述方法的实现:

## C++

```
// C++ program to find the sum of all
// perfect cubes in the given range

#include <bits/stdc++.h>
#define ll int
using namespace std;

// Array to precompute the sum of cubes
// from 1 to 100010 so that for every
// query, the answer can be returned in O(1).
long long pref[100010];

// Function to check if a number is
// a perfect Cube or not
int isPerfectCube(long long int x)
{
    // Find floating point value of
    // cube root of x.
    long double cr = round(cbrt(x));

    // If cube root of x is cr
    // return the x, else 0
    return (cr * cr * cr == x) ? x : 0;
}

// Function to precompute the perfect
// Cubes upto 100000.
void compute()
{
    for (int i = 1; i <= 100000; ++i) {
        pref[i] = pref[i - 1]
                  + isPerfectCube(i);
    }
}

// Function to print the sum for each query
void printSum(int L, int R)
{
    int sum = pref[R] - pref[L - 1];
    cout << sum << " ";
}

// Driver code
int main()
{
    // To calculate the precompute function
    compute();

    int Q = 4;
    int arr[][2] = { { 1, 10 },
                     { 1, 100 },
                     { 2, 25 },
                     { 4, 50 } };

    // Calling the printSum function
    // for every query
    for (int i = 0; i < Q; i++) {
        printSum(arr[i][0], arr[i][1]);
    }

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the sum of all
// perfect cubes in the given range
import java.util.*;
import java.lang.*;
import java.io.*;

/* Name of the class has to be "Main" only if the class is public. */
class GFG
{
    // Array to precompute the sum of cubes
    // from 1 to 100010 so that for every
    // query, the answer can be returned in O(1).
     public static int []pref=new int[100010];

    // Function to check if a number is
    // a perfect Cube or not
    static int isPerfectCube(int x)
    {
        // Find floating point value of
        // cube root of x.
        double cr = Math.round(Math.cbrt(x));

        // If cube root of x is cr
        // return the x, else 0
        if(cr*cr*cr==(double)x) return x;
        return 0;
    }

    // Function to precompute the perfect
    // Cubes upto 100000.
    static void compute()
    {
        for (int i = 1; i <= 100000; ++i) {
            pref[i] = pref[i - 1]+ isPerfectCube(i);
        }
    }

    // Function to print the sum for each query
    static void printSum(int L, int R)
    {
        long sum = pref[R] - pref[L - 1];
        System.out.print(sum+" ");
    }

    // Driver code
    public static void main (String[] args)
    {
         // To calculate the precompute function
        compute();

        int Q = 4;
        int [][] arr = { { 1, 10 },
                                { 1, 100 },
                                { 2, 25 },
                                { 4, 50 } };

        // Calling the printSum function
        // for every query
        for (int i = 0; i < Q; i++) {
            printSum(arr[i][0], arr[i][1]);
        }
    }
}

// This code is contributed by chitranayal
```

## 蟒蛇 3

```
# Python3 program to find the sum of all
# perfect cubes in the given range

# Array to precompute the sum of cubes
# from 1 to 100010 so that for every
# query, the answer can be returned in O(1).
pref = [0]*100010;

# Function to check if a number is
# a perfect Cube or not
def isPerfectCube(x) :

    # Find floating point value of
    # cube root of x.
    cr = round(x**(1/3));

    # If cube root of x is cr
    # return the x, else 0
    rslt = x if (cr * cr * cr == x) else 0;
    return rslt;

# Function to precompute the perfect
# Cubes upto 100000.
def compute() :
    for i in range(1, 100001) :
        pref[i] = pref[i - 1] + isPerfectCube(i);

# Function to print the sum for each query
def printSum(L, R) :

    sum = pref[R] - pref[L - 1];
    print(sum ,end= " ");

# Driver code
if __name__ == "__main__" :

    # To calculate the precompute function
    compute();

    Q = 4;
    arr= [ [ 1, 10 ],
            [ 1, 100 ],
            [ 2, 25 ],
            [ 4, 50 ] ];

    # Calling the printSum function
    # for every query
    for i in range(Q) :
        printSum(arr[i][0], arr[i][1]);

# This code is contributed by AnkitRai01
```

## C#

```
// C# program to find the sum of all
// perfect cubes in the given range
using System;

class GFG {
// Array to precompute the sum of cubes
// from 1 to 100010 so that for every
// query, the answer can be returned in O(1).
 public static long []pref=new long[100010];

// Function to check if a number is
// a perfect Cube or not
static long isPerfectCube(long x)
{
    // Find floating point value of
    // cube root of x.
    double cr = Math.Round(MathF.Cbrt(x));

    // If cube root of x is cr
    // return the x, else 0
    if(cr*cr*cr==(double)x) return x;
    return 0;
}

// Function to precompute the perfect
// Cubes upto 100000.
static void compute()
{
    for (long i = 1; i <= 100000; ++i) {
        pref[i] = pref[i - 1]
                  + isPerfectCube(i);
    }
}

// Function to print the sum for each query
static void printSum(int L, int R)
{
    long sum = pref[R] - pref[L - 1];
    Console.Write(sum+" ");
}

// Driver code
public static void Main()
  {
    // To calculate the precompute function
    compute();

    int Q = 4;
    int [,] arr = new int[,]{ { 1, 10 },
                            { 1, 100 },
                            { 2, 25 },
                            { 4, 50 } };

    // Calling the printSum function
    // for every query
    for (int i = 0; i < Q; i++) {
        printSum(arr[i,0], arr[i,1]);
    }
  }
} 

// This code is contributed by mohit kumar 29
```

## java 描述语言

```
<script>

// Javascript program to find the sum of all
// perfect cubes in the given range

// Array to precompute the sum of cubes
// from 1 to 100010 so that for every
// query, the answer can be returned in O(1).
var pref=Array(100010).fill(0);

// Function to check if a number is
// a perfect Cube or not
function isPerfectCube(x)
{
    // Find floating point value of
    // cube root of x.
    var cr = Math.round(Math.cbrt(x));

    // If cube root of x is cr
    // return the x, else 0
    return (cr * cr * cr == x) ? x : 0;
}

// Function to precompute the perfect
// Cubes upto 100000.
function compute()
{
    for (var i = 1; i <= 100000; ++i) {
        pref[i] = pref[i - 1]
                  + isPerfectCube(i);
    }
}

// Function to print the sum for each query
function printSum(L, R)
{
    var sum = pref[R] - pref[L - 1];
    document.write(sum + " ");
}

// Driver code

// To calculate the precompute function
compute();
var Q = 4;
var arr = [ [ 1, 10 ],
                 [ 1, 100 ],
                 [ 2, 25 ],
                 [ 4, 50 ] ];
// Calling the printSum function
// for every query
for (var i = 0; i < Q; i++) {
    printSum(arr[i][0], arr[i][1]);
}

</script>
```

**Output:** 

```
9 100 8 35
```

时间复杂度:0(100000)

辅助空间:0(100010)