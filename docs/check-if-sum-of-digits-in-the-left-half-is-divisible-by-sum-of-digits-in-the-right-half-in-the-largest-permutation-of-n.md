# 检查在 N 的最大排列中，左半部分的数字之和是否能被右半部分的数字之和整除

> 原文:[https://www . geesforgeks . org/check-如果左半部分的数字和被右半部分的数字和整除-n 的最大排列/](https://www.geeksforgeeks.org/check-if-sum-of-digits-in-the-left-half-is-divisible-by-sum-of-digits-in-the-right-half-in-the-largest-permutation-of-n/)

给定一个正整数 **N** ，任务是通过重新排列位数来最大化整数 **N** ，并检查左半位数的[和是否能被右半位数的和整除。如果发现是真的，则打印**“是”**。否则，打印**“否”**。](https://www.geeksforgeeks.org/program-for-sum-of-the-digits-of-a-given-number/)

> 如果给定数字 **N** 中的位数(比如 **D** )为奇数，则考虑以下两种可能性中的任何一种:
> 
> *   考虑左半部分的第一个 **(D/2)** 数字。
> *   考虑左半部分的第一个( **D/2 + 1)** 数字。

**示例:**

> **输入:** N = 43729
> **输出:**是
> **说明:**
> 通过重新排列数字可能得到的 N 的最大值为 97432。
> **例 1:**
> 左半部分位数之和= 9 + 7 = 16。
> 右半部分位数之和= 4 + 3 + 2 = 9。
> 由于，16 不能被 9 整除，所以不满足条件。
> **例 2:**
> 左半部分位数之和= 9 + 7 + 4 = 20。
> 右半部分位数之和= 3 + 2 = 5。
> 因为，20 可以被 5 整除，所以条件成立。
> 
> **输入:**N = 3746
> T3】输出:否

**方法:**给定的问题可以通过[对数字 **N** 的给定位数进行降序排序](https://www.geeksforgeeks.org/sort-c-stl/)最大化 **N** 的值，然后检查左右半位数之和的可除性来解决。按照以下步骤解决问题:

*   初始化一个变量，比如说 **D** 存储给定数字 **N** 的[位数](https://www.geeksforgeeks.org/program-count-digits-integer-3-different-methods/)。
*   将给定的数字作为字符串存储在变量中，比如 **temp** 。
*   [按降序排列字符串**温度**](https://www.geeksforgeeks.org/program-sort-string-descending-order/)。
*   现在检查第一个 **(D/2)** 位数的总和是否能被最后一个 **(D/2)** 位数的总和整除，然后打印**“是”**。否则，打印**“否”**。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include "bits/stdc++.h"
using namespace std;

// Function to check if sum of digits
// in left half is divisible by the sum
// of digits in the right half or not
void checkDivisible(int N)
{

    // Convert N to its equivalent string
    string temp = to_string(N);

    // Count of digits
    int D = temp.length();

    // Sort the digits in decreasing order
    sort(temp.begin(), temp.end(),
         greater<char>());

    int leftSum = 0, rightSum = 0;

    // Find the sum of digits
    for (int i = 0; temp[i]; i++) {
        rightSum += (temp[i] - '0');
    }

    for (int i = 0; i < D / 2; i++) {

        // Update the leftSum and the
        // rightSum
        leftSum += (temp[i] - '0');
        rightSum -= (temp[i] - '0');
    }

    if (D & 1) {

        // Consider Case 1: Check divisibility
        if (leftSum % rightSum == 0) {
            cout << "Yes";
        }
        else {

            leftSum += (temp[D / 2] - '0');
            rightSum -= (temp[D / 2] - '0');

            // Consider Case 2: Check divisibility
            if (leftSum % rightSum == 0) {
                cout << "Yes";
            }
            else {
                cout << "No";
            }
        }
    }

    else {

        // Check divisibility
        if (leftSum % rightSum == 0) {
            cout << "Yes";
        }
        else {
            cout << "No";
        }
    }
}

// Driver Code
int main()
{
    int N = 43729;
    checkDivisible(N);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
public class GFG
{

// Utility function to sort array in
// descending order
static void descOrder(char[] s)
{
    Arrays.sort(s);
    reverse(s);
}

// Utility function to reverse an array
static void reverse(char[] a)
{
    int i, n = a.length;
    char t;
    for (i = 0; i < n / 2; i++)
    {
    t = a[i];
        a[i] = a[n - i - 1];
        a[n - i - 1] = t;
    }
}

// Function to check if sum of digits
// in left half is divisible by the sum
// of digits in the right half or not
static void checkDivisible(int N)
{

    // Convert N to its equivalent string
    String temp = Integer.toString(N);
    char []arr = temp.toCharArray();

    // Count of digits
    int D = arr.length;

    // Sort the digits in decreasing order
    descOrder(arr);

    int leftSum = 0, rightSum = 0;

    // Find the sum of digits
    for (int i = 0; i < D; i++) {
        rightSum += (arr[i] - '0');
    }

    for (int i = 0; i < D / 2; i++) {

        // Update the leftSum and the
        // rightSum
        leftSum += (arr[i] - '0');
        rightSum -= (arr[i] - '0');
    }

    if (D%2 == 1) {

        // Consider Case 1: Check divisibility
        if (leftSum % rightSum == 0) {
            System.out.print("Yes");
        }
        else {

            leftSum += (arr[D / 2] - '0');
            rightSum -= (arr[D / 2] - '0');

            // Consider Case 2: Check divisibility
            if (leftSum % rightSum == 0) {
                System.out.print("Yes");
            }
            else {
                System.out.print("No");
            }
        }
    }

    else {

        // Check divisibility
        if (leftSum % rightSum == 0) {
            System.out.print("Yes");
        }
        else {
            System.out.print("No");
        }
    }
}

// Driver Code
public static void main(String args[])
{
    int N = 43729;
    checkDivisible(N);
}
}

// This code is contributed by Samim Hossain Mondal.
```

## C#

```
// C# program for the above approach
using System;
using System.Collections;

public class GFG
{
// Utility function to sort array in
// descending order
static void descOrder(char []s)
{
    Array.Sort(s);
    reverse(s);
}

// Utility function to reverse an array
static void reverse(char []a)
{
    int i, n = a.Length;
    char t;
    for (i = 0; i < n / 2; i++)
    {
    t = a[i];
        a[i] = a[n - i - 1];
        a[n - i - 1] = t;
    }
}

// Function to check if sum of digits
// in left half is divisible by the sum
// of digits in the right half or not
static void checkDivisible(int N)
{

    // Convert N to its equivalent string
    String temp = N.ToString();
    char []arr = temp.ToCharArray();

    // Count of digits
    int D = arr.Length;

    // Sort the digits in decreasing order
    descOrder(arr);

    int leftSum = 0, rightSum = 0;

    // Find the sum of digits
    for (int i = 0; i < D; i++) {
        rightSum += (arr[i] - '0');
    }

    for (int i = 0; i < D / 2; i++) {

        // Update the leftSum and the
        // rightSum
        leftSum += (arr[i] - '0');
        rightSum -= (arr[i] - '0');
    }

    if (D%2 == 1) {

        // Consider Case 1: Check divisibility
        if (leftSum % rightSum == 0) {
            Console.Write("Yes");
        }
        else {

            leftSum += (arr[D / 2] - '0');
            rightSum -= (arr[D / 2] - '0');

            // Consider Case 2: Check divisibility
            if (leftSum % rightSum == 0) {
                Console.Write("Yes");
            }
            else {
                Console.Write("No");
            }
        }
    }

    else {

        // Check divisibility
        if (leftSum % rightSum == 0) {
            Console.Write("Yes");
        }
        else {
            Console.Write("No");
        }
    }
}

// Driver Code
public static void Main()
{
    int N = 43729;
    checkDivisible(N);
}
}
// This code is contributed by Samim Hossain Mondal.
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to check if sum of digits
// in left half is divisible by the sum
// of digits in the right half or not
function checkDivisible(N)
{

    // Convert N to its equivalent string
    let temp = N.toString();

    // Count of digits
    let D = temp.length;

    // Sort the digits in decreasing order
    temp.sort().reverse();

    let leftSum = 0, rightSum = 0;

    // Find the sum of digits
    for (let i = 0; i < D; i++) {
        rightSum += (temp[i] - '0');
    }

    for (let i = 0; i < D / 2; i++) {

        // Update the leftSum and the
        // rightSum
        leftSum += (temp[i] - '0');
        rightSum -= (temp[i] - '0');
    }

    if (D % 2 == 1) {

        // Consider Case 1: Check divisibility
        if (leftSum % rightSum == 0) {
            document.write("Yes");
        }
        else {

            leftSum += (temp[D / 2] - '0');
            rightSum -= (temp[D / 2] - '0');

            // Consider Case 2: Check divisibility
            if (leftSum % rightSum == 0) {
                document.write("Yes");
            }
            else {
                document.write("No");
            }
        }
    }

    else {

        // Check divisibility
        if (leftSum % rightSum == 0) {
            document.write("Yes");
        }
        else {
            document.write("No");
        }
    }
}

// Driver Code
let N = 43729;
checkDivisible(N);

// This code is contributed by Samim Hossain Mondal.
</script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(log<sub>10</sub>N)*
***辅助空间:** O(log <sub>10</sub> N)*