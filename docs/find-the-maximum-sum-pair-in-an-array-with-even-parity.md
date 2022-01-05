# 找到偶宇称数组中的最大和对

> 原文:[https://www . geeksforgeeks . org/find-偶数奇偶校验数组中的最大和对/](https://www.geeksforgeeks.org/find-the-maximum-sum-pair-in-an-array-with-even-parity/)

给定一个由 **N** 个整数组成的数组 **arr[]** ，任务是找到一对具有偶宇称和最大和的整数。

**示例:**

> **输入:** arr[] = {18，15，8，9，14}
> **输出:** 18 15
> **解释:**
> 元素的二进制表示–
> 18 =>10010，奇偶性= 2
> 15 = > 1111，奇偶性= 4
> 8 = > 1000，奇偶性= 1
> 9 =>1000
> 
> **输入:** arr[] = {5，3，4，2，9}
> **输出:** 9 5
> **解释:**
> 数组包含三个偶数奇偶校验值 5、3 和 9。
> 因此，具有最大和的对将是 9 和 5。

**方法:**问题中的关键观察是，如果我们选择两个偶宇称的最大数，那么它将是期望的答案。
遍历数组并检查[当前元素是否具有偶数奇偶校验](https://www.geeksforgeeks.org/program-to-find-parity/)。然后，用偶数更新两个最大值。

```
if (findParity(arr[i]) % 2 == 0)
    if (arr[i] >= firstMaximum)
         secondMaximum = firstMaximum
         firstMaximum  = arr[i]
    elif (arr[i] >= secondMaximum)
         secondMaximum = arr[i]
```

下面是上述方法的实现:

## C++

```
// C++ implementation to find
// a pair with even parity and
// maximum sum

#include <bits/stdc++.h>
using namespace std;

const int sz = 1e3;

// Function that returns true
// if count of set bits
// in given number is even
bool isEvenParity(int x)
{
    // Parity will store the
    // count of set bits
    int parity = 0;
    while (x != 0) {
        if (x & 1)
            parity++;
        x = x >> 1;
    }

    if (parity % 2 == 0)
        return true;
    else
        return false;
}

// Function to print the
// elements of the array
void printArray(int arr[], int len)
{
    for (int i = 0; i < len; i++) {
        cout << arr[i] << ' ';
    }
}

// Function to remove all the
// even parity elements from
// the given array
void findPairEvenParity(
            int arr[], int len)
{
    int firstMaximum = INT_MIN;
    int secondMaximum = INT_MIN;

    // Traverse the array
    for (int i = 0; i < len; i++) {

        // If the current element
        // has even parity
        if (isEvenParity(arr[i])) {

            if (arr[i] >= firstMaximum){
                secondMaximum = firstMaximum;
                firstMaximum = arr[i];
            }
            else if (arr[i] >= secondMaximum){
                secondMaximum = arr[i];
            }
        }
    }

    cout << firstMaximum
         << " " << secondMaximum;
}

// Driver Code
int main()
{
    int arr[] = { 18, 15, 8, 9, 14 };
    int len = sizeof(arr) / sizeof(int);

    // Function Call
    findPairEvenParity(arr, len);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find
// a pair with even parity and
// maximum sum
import java.util.*;

class GFG{

static int sz = (int) 1e3;

// Function that returns true
// if count of set bits
// in given number is even
static boolean isEvenParity(int x)
{

    // Parity will store the
    // count of set bits
    int parity = 0;

    while (x != 0)
    {
        if (x % 2 == 1)
            parity++;
        x = x >> 1;
    }

    if (parity % 2 == 0)
        return true;
    else
        return false;
}

// Function to print the
// elements of the array
static void printArray(int arr[],
                       int len)
{
    for(int i = 0; i < len; i++)
    {
       System.out.print(arr[i] + " ");
    }
}

// Function to remove all the
// even parity elements from
// the given array
static void findPairEvenParity(int arr[],
                               int len)
{
    int firstMaximum = Integer.MIN_VALUE;
    int secondMaximum = Integer.MIN_VALUE;

    // Traverse the array
    for(int i = 0; i < len; i++)
    {

       // If the current element
       // has even parity
       if (isEvenParity(arr[i]))
       {
           if (arr[i] >= firstMaximum)
           {
               secondMaximum = firstMaximum;
               firstMaximum = arr[i];
           }
           else if (arr[i] >= secondMaximum)
           {
               secondMaximum = arr[i];
           }
       }
    }
    System.out.print(firstMaximum + " " +
                     secondMaximum);
}

// Driver Code
public static void main(String[] args)
{
    int arr[] = { 18, 15, 8, 9, 14 };
    int len = arr.length;

    // Function Call
    findPairEvenParity(arr, len);
}
}

// This code is contributed by amal kumar choubey
```

## 蟒蛇 3

```
# Python3 implementation to find
# a pair with even parity and
# maximum sum
import sys

sz = 1e3

# Function that returns true
# if count of set bits
# in given number is even
def isEvenParity(x):

    # Parity will store the
    # count of set bits
    parity = 0

    while x != 0:
        if (x & 1):
            parity = parity + 1;

        x = x >> 1

    if (parity % 2 == 0):
        return True
    else:
        return False

# Function to print the
# elements of the array
def printArray(arr, n):

    for i in range(0, n):
        print(arr[i], end = ' ')

# Function to remove all the
# even parity elements from
# the given array
def findPairEvenParity(arr, n):

    firstMaximum = -1
    secondMaximum = -1

    # Traverse the array
    for i in range(0, n):

        # If the current element
        # has even parity
        if isEvenParity(arr[i]) == True:
            if (arr[i] >= firstMaximum):
                secondMaximum = firstMaximum
                firstMaximum = arr[i]

            elif (arr[i] >= secondMaximum):
                secondMaximum = arr[i]

    print(firstMaximum, secondMaximum)

# Driver Code
if __name__ == "__main__":

    arr = [ 18, 15, 8, 9, 14 ]
    n = len(arr)

    # Function call
    findPairEvenParity(arr, n)

# This code is contributed by akhilsaini
```

## C#

```
// C# implementation to find
// a pair with even parity and
// maximum sum
using System;
class GFG{

static int sz = (int) 1e3;

// Function that returns true
// if count of set bits
// in given number is even
static bool isEvenParity(int x)
{

    // Parity will store the
    // count of set bits
    int parity = 0;

    while (x != 0)
    {
        if (x % 2 == 1)
            parity++;
        x = x >> 1;
    }

    if (parity % 2 == 0)
        return true;
    else
        return false;
}

// Function to print the
// elements of the array
static void printArray(int []arr,
                       int len)
{
    for(int i = 0; i < len; i++)
    {
        Console.Write(arr[i] + " ");
    }
}

// Function to remove all the
// even parity elements from
// the given array
static void findPairEvenParity(int []arr,
                               int len)
{
    int firstMaximum = Int32.MinValue;
    int secondMaximum = Int32.MinValue;

    // Traverse the array
    for(int i = 0; i < len; i++)
    {

        // If the current element
        // has even parity
        if (isEvenParity(arr[i]))
        {
            if (arr[i] >= firstMaximum)
            {
                secondMaximum = firstMaximum;
                firstMaximum = arr[i];
            }
            else if (arr[i] >= secondMaximum)
            {
                secondMaximum = arr[i];
            }
        }
    }
    Console.Write(firstMaximum + " " +
                  secondMaximum);
}

// Driver Code
public static void Main()
{
    int []arr = { 18, 15, 8, 9, 14 };
    int len = arr.Length;

    // Function Call
    findPairEvenParity(arr, len);
}
}

// This code is contributed by Code_Mech
```

## java 描述语言

```
<script>
// Javascript implementation to find
// a pair with even parity and
// maximum sum

let sz = 1e3;

// Function that returns true
// if count of set bits
// in given number is even
function isEvenParity(x)
{

    // Parity will store the
    // count of set bits
    let parity = 0;

    while (x != 0)
    {
        if (x % 2 == 1)
            parity++;
        x = x >> 1;
    }

    if (parity % 2 == 0)
        return true;
    else
        return false;
}

// Function to prlet the
// elements of the array
function prletArray(arr, len)
{
    for(let i = 0; i < len; i++)
    {
       document.write(arr[i] + " ");
    }
}

// Function to remove all the
// even parity elements from
// the given array
function findPairEvenParity(arr, len)
{
    let firstMaximum = Number.MIN_VALUE;
    let secondMaximum = Number.MIN_VALUE;

    // Traverse the array
    for(let i = 0; i < len; i++)
    {

       // If the current element
       // has even parity
       if (isEvenParity(arr[i]))
       {
           if (arr[i] >= firstMaximum)
           {
               secondMaximum = firstMaximum;
               firstMaximum = arr[i];
           }
           else if (arr[i] >= secondMaximum)
           {
               secondMaximum = arr[i];
           }
       }
    }
    document.write(firstMaximum + " " +
                     secondMaximum);
}

// Driver Code

      let arr = [ 18, 15, 8, 9, 14 ];
    let len = arr.length;

    // Function Call
    findPairEvenParity(arr, len);;

</script>
```

**Output:** 

```
18 15
```

时间复杂度:0(n)

辅助空间:0(1)