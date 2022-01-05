# 检查一个数是否可以表示为两个连续立方体的差

> 原文:[https://www . geesforgeks . org/check-一个数字是否可以表示为两个连续立方体的差值/](https://www.geeksforgeeks.org/check-whether-a-number-can-be-represented-as-difference-of-two-consecutive-cubes/)

给定一个数字 **N** ，任务是检查数字 **N** 是否可以表示为两个连续立方体的差。如果**是**，则打印这些数字，否则打印**否**。

**示例:**

> **输入:**N = 19
> T3】输出:T5】是
> 2 3
> T8】说明:T10】3<sup>3</sup>–2<sup>3</sup>= 19
> 
> **输入:**N = 10
> T3】输出:否

**方法:**问题中的关键观察是，一个数可以表示为两个连续立方体的差，当且仅当:

> = > N =(K+1)<sup>3</sup>–K<sup>3</sup>T4】=>N = 3 * K<sup>2</sup>+3 * K+1
> =>12 * N = 36 * K<sup>2</sup>+36 * K+12
> =>12 * N =(6 * K+3)<sup>2</sup>+3
> =>11

因此，如果上述条件成立，那么我们将通过检查**(I+1)<sup>3</sup>–I<sup>3</sup>= N**来打印数字，并打印数字 **i** 和 **i + 1** 。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// Function to print the two consecutive
// numbers whose difference is N
void print(int N)
{
    // Iterate in the range [0, 10^5]
    for (int i = 0; i < 100000; i++) {

        if (pow(i + 1, 3)
                - pow(i, 3)
            == N) {

            cout << i << ' ' << i + 1;
            return;
        }
    }
}

// Function to check if N is a
// perfect cube
bool isPerfectSquare(long double x)
{
    // Find floating point value of
    // square root of x.
    long double sr = sqrt(x);

    // If square root is an integer
    return ((sr - floor(sr)) == 0);
}

// Function to check whether a number
// can be represented as difference
// of two consecutive cubes
bool diffCube(int N)
{
    // Check if 12 * N - 3 is a
    // perfect square or not
    return isPerfectSquare(12 * N - 3);
}

// Driver Code
int main()
{
    // Given Number N
    int N = 19;
    if (diffCube(N)) {
        cout << "Yes\n";
        print(N);
    }
    else {
        cout << "No\n";
    }
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG{

// Function to print the two consecutive
// numbers whose difference is N
static void print(int N)
{
    // Iterate in the range [0, 10^5]
    for (int i = 0; i < 100000; i++)
    {

        if (Math.pow(i + 1, 3) - Math.pow(i, 3) == N)
        {
            int j = i + 1;
            System.out.println(i + " " + j);
            return;
        }
    }
}

// Function to check if N is a
// perfect cube
static boolean isPerfectSquare(double x)
{
    // Find floating point value of
    // square root of x.
    double sr = Math.sqrt(x);

    // If square root is an integer
    return ((sr - Math.floor(sr)) == 0);
}

// Function to check whether a number
// can be represented as difference
// of two consecutive cubes
static boolean diffCube(int N)
{
    // Check if 12 * N - 3 is a
    // perfect square or not
    return isPerfectSquare(12 * N - 3);
}

// Driver Code
public static void main(String[] args)
{
    // Given Number N
    int N = 19;
    if (diffCube(N))
    {
        System.out.println("Yes");
        print(N);
    }
    else
    {
        System.out.println("No");
    }
}
}

// This code is contributed by rock_cool
```

## 蟒蛇 3

```
# Python3 program for the above approach
import math

# Function to print the two consecutive
# numbers whose difference is N
def printt(N):

    # Iterate in the range [0, 10^5]
    for i in range(100000):
        if (pow(i + 1, 3) - pow(i, 3) == N):
            print(i, '', i + 1)
            return

# Function to check if N is a
# perfect cube
def isPerfectSquare(x):

    # Find floating povalue of
    # square root of x.
    sr = math.sqrt(x)

    # If square root is an integer
    return ((sr - math.floor(sr)) == 0)

# Function to check whether a number
# can be represented as difference
# of two consecutive cubes
def diffCube(N):

    # Check if 12 * N - 3 is a
    # perfect square or not
    return isPerfectSquare(12 * N - 3)

# Driver Code

# Given number N
N = 19

if (diffCube(N)):
    print("Yes")
    printt(N)

else:
    print("No")

# This code is contributed by sanjoy_62
```

## C#

```
// C# program for the above approach
using System;
class GFG{

// Function to print the two consecutive
// numbers whose difference is N
static void print(int N)
{
    // Iterate in the range [0, 10^5]
    for (int i = 0; i < 100000; i++)
    {

        if (Math.Pow(i + 1, 3) - Math.Pow(i, 3) == N)
        {
            int j = i + 1;
            Console.WriteLine(i + " " + j);
            return;
        }
    }
}

// Function to check if N is a
// perfect cube
static bool isPerfectSquare(double x)
{
    // Find floating point value of
    // square root of x.
    double sr = Math.Sqrt(x);

    // If square root is an integer
    return ((sr - Math.Floor(sr)) == 0);
}

// Function to check whether a number
// can be represented as difference
// of two consecutive cubes
static bool diffCube(int N)
{
    // Check if 12 * N - 3 is a
    // perfect square or not
    return isPerfectSquare(12 * N - 3);
}

// Driver Code
public static void Main(String[] args)
{
    // Given Number N
    int N = 19;
    if (diffCube(N))
    {
        Console.WriteLine("Yes");
        print(N);
    }
    else
    {
        Console.WriteLine("No");
    }
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Function to print the two consecutive
// numbers whose difference is N
function print(N)
{

    // Iterate in the range [0, 10^5]
    for(let i = 0; i < 100000; i++)
    {
        if (parseInt(Math.pow(i + 1, 3), 10) -
            parseInt(Math.pow(i, 3), 10) == N)
        {
            document.write(i + " " + (i + 1));
            return;
        }
    }
}

// Function to check if N is a
// perfect cube
function isPerfectSquare(x)
{

    // Find floating point value of
    // square root of x.
    let sr = Math.sqrt(x);

    // If square root is an integer
    return ((sr - Math.floor(sr)) == 0);
}

// Function to check whether a number
// can be represented as difference
// of two consecutive cubes
function diffCube(N)
{

    // Check if 12 * N - 3 is a
    // perfect square or not
    return isPerfectSquare(12 * N - 3);
}

// Driver code

// Given Number N
let N = 19;

if (diffCube(N) != 0)
{
    document.write("Yes" + "</br>");
    print(N);
}
else
{
    document.write("No");
}

// This code is contributed by divyeshrabadiya07

</script>
```

**Output:** 

```
Yes
2 3
```

***时间复杂度:** O(N)，其中 N 在范围 10 <sup>5</sup>*
***辅助空间:** O(1)*