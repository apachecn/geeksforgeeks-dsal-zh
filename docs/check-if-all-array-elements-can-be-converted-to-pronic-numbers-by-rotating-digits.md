# 通过旋转数字

检查是否所有数组元素都可以转换成拼音数字

> 原文:[https://www . geeksforgeeks . org/check-if-all-array-elements-可通过旋转数字转换为 pronic-numbers/](https://www.geeksforgeeks.org/check-if-all-array-elements-can-be-converted-to-pronic-numbers-by-rotating-digits/)

给定一个大小为 **N** 的[数组](https://www.geeksforgeeks.org/array-data-structure/) **arr[]** ，任务是通过旋转数组元素的数字任意多次来检查是否有可能将所有数组元素转换为[音位数字](https://www.geeksforgeeks.org/check-given-number-pronic/)。

**示例:**

> **输入:{** 321，402，246，299}
> **输出:**真
> **解释:**
> arr[0] →右旋转一次将 arr[0]修改为 132 (= 11 × 12)。
> arr[1] →向右旋转一次将 arr[0]修改为 240 (= 15 × 16)。
> arr[2] →向右旋转两次将 arr[2]修改为 462 (= 21 × 22)。
> arr[3] →向右旋转两次将 arr[3]修改为 992 (= 31 × 32)。
> 
> **输入:{** 433，653，402，186}
> 输出:假

**方法:**按照以下步骤解决问题:

*   [遍历数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/)并检查每个数组元素，是否可以将其转换为[音位数字](https://www.geeksforgeeks.org/check-given-number-pronic/)。
*   对于每个数组元素，应用所有可能的旋转，并在每次旋转后检查生成的数字是否为正旋。
*   如果无法将任何数组元素转换为音位数字，则打印**“假”**。
*   否则，打印**“真”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach
#include <bits/stdc++.h>
using namespace std;

// function to check Pronic Number
bool isPronic(int x)
{
    for (int i = 0; i < (int)(sqrt(x)) + 1; i++)
    {

        // Checking Pronic Number
        // by multiplying consecutive
        // numbers
        if (x == i * (i + 1))
        {
            return true;
        }
    }
    return false;
}

// Function to check if any permutation
// of val is a pronic number or not
bool checkRot(int val)
{

    string temp = to_string(val);
    for (int i = 0; i < temp.length(); i++)
    {
        if (isPronic(stoi(temp)) == true)
        {
            return true;
        }
        temp = temp.substr(1, temp.size() - 1) + temp[0];
    }
    return false;
}

// Function to check if all array
// elements can be converted to
// a pronic number or not
bool check(int arr[], int N)
{

    // Traverse the array
    for (int i = 0; i < N; i++)
    {

        // If current element
        // cannot be converted
        // to a pronic number
        if (checkRot(arr[i]) == false)
        {
            return false;
        }
    }
    return true;
}

// Driven Program
int main()
{

    // Given array
    int arr[] = { 321, 402, 246, 299 };
    int N = sizeof(arr) / sizeof(arr[0]);

    // function call
    cout << (check(arr, N) ? "True" : "False");

    return 0;
}

// This code is contributed by Kingash.
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach

import java.io.*;
import java.lang.*;
import java.util.*;

class GFG {

  // function to check Pronic Number
  static boolean isPronic(int x)
  {

    for (int i = 0; i < (int)(Math.sqrt(x)) + 1; i++) {

      // Checking Pronic Number
      // by multiplying consecutive
      // numbers
      if (x == i * (i + 1)) {
        return true;
      }
    }

    return false;
  }

  // Function to check if any permutation
  // of val is a pronic number or not
  static boolean checkRot(int val)
  {
    String temp = Integer.toString(val);
    for (int i = 0; i < temp.length(); i++)
    {
      if (isPronic(Integer.parseInt(temp)) == true) {
        return true;
      }

      temp = temp.substring(1) + temp.charAt(0);
    }
    return false;
  }

  // Function to check if all array
  // elements can be converted to
  // a pronic number or not
  static boolean check(int arr[], int N)
  {

    // Traverse the array
    for (int i = 0; i < N; i++)
    {

      // If current element
      // cannot be converted
      // to a pronic number
      if (checkRot(arr[i]) == false)
      {
        return false;
      }
    }
    return true;
  }

  // Driver code
  public static void main(String[] args)
  {

    // Given array
    int arr[] = { 321, 402, 246, 299 };
    int N = arr.length;

    // Function call
    System.out.println(
      (check(arr, N) ? "True" : "False"));
  }
}

// This code is contributed by Kingash.
```

## 蟒蛇 3

```
# Python implementation of
# the above approach

# Function to check if a number
# is a pronic number or not
def isPronic(n):

  for i in range(int(n**(1 / 2)) + 1):
    if i * (i + 1) == n:
      return True

  return False

# Function to check if any permutation
# of n is a pronic number or not
def checkRot(n):

  temp = str(n)

  for i in range(len(temp)):

    if isPronic(int(temp)):
      return True

    temp = temp[1:]+temp[0]

  return False

# Function to check if all array
# elements can be converted to
# a pronic number or not
def check(arr):

  # Traverse the array
  for i in arr:

    # If current element
    # cannot be converted
    # to a pronic number
    if not checkRot(i):
      return False
  return True

# Driver Code
arr = [ 321, 402, 246, 299 ]
print(check(arr))
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;

class GFG{

  // function to check Pronic Number
  static bool isPronic(int x)
  {
    int val  = (int)Math.Sqrt(x);
    val += 1;
    for (int i = 0; i < val; i++)
    {

      // Checking Pronic Number
      // by multiplying consecutive
      // numbers
      if (x == i * (i + 1))
      {
        return true;
      }
    }
    return false;
  }

  // Function to check if any permutation
  // of val is a pronic number or not
  static bool checkRot(int val)
  {

    string temp = val.ToString();
    for (int i = 0; i < temp.Length; i++)
    {
      int a = Int32.Parse(temp);
      if (isPronic(a) == true)
      {
        return true;
      }
      temp = temp.Substring(1, temp.Length - 1) + temp[0];
    }
    return false;
  }

  // Function to check if all array
  // elements can be converted to
  // a pronic number or not
  static bool check(int []arr, int N)
  {

    // Traverse the array
    for (int i = 0; i < N; i++)
    {

      // If current element
      // cannot be converted
      // to a pronic number
      if (checkRot(arr[i]) == false)
      {
        return false;
      }
    }
    return true;
  }

  // Driven Program
  public static void Main()
  {

    // Given array
    int []arr = { 321, 402, 246, 299 };
    int N = arr.Length;

    // function call
    Console.WriteLine(check(arr, N) ? "True" : "False");
  }
}

// This code is contributed by ipg2016107.
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// function to check Pronic Number
function isPronic(x)
{
    for (var i = 0; i < parseInt(Math.sqrt(x)) + 1; i++)
    {

        // Checking Pronic Number
        // by multiplying consecutive
        // numbers
        if (x == i * (i + 1))
        {
            return true;
        }
    }
    return false;
}

// Function to check if any permutation
// of val is a pronic number or not
function checkRot(val)
{

    var temp = (val).toString();
    for (var i = 0; i < temp.length; i++)
    {
        if (isPronic(parseInt(temp)) == true)
        {
            return true;
        }
        temp = temp.substring(1) + temp[0];
    }
    return false;
}

// Function to check if all array
// elements can be converted to
// a pronic number or not
function check(arr, N)
{

    // Traverse the array
    for (var i = 0; i < N; i++)
    {

        // If current element
        // cannot be converted
        // to a pronic number
        if (checkRot(arr[i]) == false)
        {
            return false;
        }
    }
    return true;
}

// Driven Program

// Given array
var arr = [ 321, 402, 246, 299 ]
var N = arr.length;

// function call
document.write(check(arr, N) ? "True" : "False");

// This code is contributed by noob2000.
</script>
```

**Output:** 

```
True
```

***时间复杂度:**O(N<sup>3/2</sup>)*
***辅助空间:** O(1)*