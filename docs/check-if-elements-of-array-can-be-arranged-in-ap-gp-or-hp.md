# 检查数组元素是否可以按 AP、GP 或 HP 排列

> 原文:[https://www . geesforgeks . org/check-if-elements-of-array-can-in-AP-gp-or-HP/](https://www.geeksforgeeks.org/check-if-elements-of-array-can-be-arranged-in-ap-gp-or-hp/)

给定一个由 **N** 个整数组成的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr[]** 。任务是检查通过排列[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)的元素，是否有可能生成算术级数、几何级数或调和级数。如果可能，打印“是”，类型为“前进”或“否则”打印“否”。
**举例:**

> **输入:** arr[] = {2，16，4，8}
> **输出:**可以形成一个 GP
> **解释:**
> 将给定数组重新排列为{2，4，8，16}，形成一个公比为 2 的几何级数。
> **输入:** arr[] = {15，10，15，5}
> **输出:**是，可以形成一个 AP
> **解释:**
> 将给定数组重新排列为{5，10，15，20}，形成公差 5 的等差数列。
> **输入:** arr[] = { 1.0/10.0，1.0/5.0，1.0/15.0，1.0/20.0 }
> **输出:**是，可以形成 A HP
> **解释:**
> 将给定数组重新排列为{ 1.0/5.0，1.0/10.0，1.0/15.0，1.0/20.0

**方法:**想法是观察三个级数 A.P .、G.P .或 H.P .中的任何一个中的元素都与排序顺序有些关系。因此，我们需要首先对给定的数组进行排序。

1.  **<u>对于算术级数</u> :** 检查排序后的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)的连续元素之间的差异是否相同。如果是，那么给定的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)元素形成一个**等差数列**。
2.  **<u>对于几何级数</u> :** 检查排序后的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)的连续元素的比例是否相同。如果是，那么给定的数组元素形成一个**几何级数**。
3.  **<u>对于调和级数</u> :** 检查排序后的[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)的所有连续元素的倒数之差是否相同。如果是，那么给定的数组元素形成一个**调和级数**。

以下是上述方法的实现:

## C++

```
// C++ program to check if a given
// array form AP, GP or HP
#include <bits/stdc++.h>
using namespace std;

// Returns true if arr[0..n-1]
// can form AP
bool checkIsAP(double arr[], int n)
{
    // Base Case
    if (n == 1)
        return true;

    // Sort array
    sort(arr, arr + n);

    // After sorting, difference
    // between consecutive elements
    // must be same.
    double d = arr[1] - arr[0];

    // Traverse the given array and
    // check if the difference
    // between ith element and (i-1)th
    // element is same or not
    for (int i = 2; i < n; i++) {
        if (arr[i] - arr[i - 1] != d) {
            return false;
        }
    }

    return true;
}

// Returns true if arr[0..n-1]
// can form GP
bool checkIsGP(double arr[], int n)
{
    // Base Case
    if (n == 1)
        return true;

    // Sort array
    sort(arr, arr + n);

    // After sorting, common ratio
    // between consecutive elements
    // must be same.
    double r = arr[1] / arr[0];

    // Traverse the given array and
    // check if the common ratio
    // between ith element and (i-1)th
    // element is same or not
    for (int i = 2; i < n; i++) {
        if (arr[i] / arr[i - 1] != r)
            return false;
    }

    return true;
}

// Returns true if arr[0..n-1]
// can form HP
bool checkIsHP(double arr[], int n)
{
    // Base Case
    if (n == 1) {
        return true;
    }

    double rec[n];

    // Find reciprocal of arr[]
    for (int i = 0; i < n; i++) {
        rec[i] = ((1 / arr[i]));
    }

    // After finding reciprocal, check if
    // the reciprocal is in A. P.
    // To check for A.P.
    if (checkIsAP(rec, n))
        return true;
    else
        return false;
}

// Driver's Code
int main()
{
    double arr[] = { 1.0 / 5.0, 1.0 / 10.0,
                     1.0 / 15.0, 1.0 / 20.0 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int flag = 0;

    // Function to check AP
    if (checkIsAP(arr, n)) {
        cout << "Yes, An AP can be formed"
             << endl;
        flag = 1;
    }

    // Function to check GP
    if (checkIsGP(arr, n)) {
        cout << "Yes, A GP can be formed"
             << endl;
        flag = 1;
    }

    // Function to check HP
    if (checkIsHP(arr, n)) {
        cout << "Yes, A HP can be formed"
             << endl;
        flag = 1;
    }

    else if (flag == 0) {
        cout << "No";
    }

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if a given
// array form AP, GP or HP
import java.util.*;

class GFG{

// Returns true if arr[0..n-1]
// can form AP
static boolean checkIsAP(double arr[], int n)
{
    // Base Case
    if (n == 1)
        return true;

    // Sort array
    Arrays.sort(arr);

    // After sorting, difference
    // between consecutive elements
    // must be same.
    double d = arr[1] - arr[0];

    // Traverse the given array and
    // check if the difference
    // between ith element and (i-1)th
    // element is same or not
    for (int i = 2; i < n; i++) {
        if (arr[i] - arr[i - 1] != d) {
            return false;
        }
    }

    return true;
}

// Returns true if arr[0..n-1]
// can form GP
static boolean checkIsGP(double arr[], int n)
{
    // Base Case
    if (n == 1)
        return true;

    // Sort array
    Arrays.sort(arr);

    // After sorting, common ratio
    // between consecutive elements
    // must be same.
    double r = arr[1] / arr[0];

    // Traverse the given array and
    // check if the common ratio
    // between ith element and (i-1)th
    // element is same or not
    for (int i = 2; i < n; i++) {
        if (arr[i] / arr[i - 1] != r)
            return false;
    }

    return true;
}

// Returns true if arr[0..n-1]
// can form HP
static boolean checkIsHP(double arr[], int n)
{
    // Base Case
    if (n == 1) {
        return true;
    }

    double []rec = new double[n];

    // Find reciprocal of arr[]
    for (int i = 0; i < n; i++) {
        rec[i] = ((1 / arr[i]));
    }

    // After finding reciprocal, check if
    // the reciprocal is in A. P.
    // To check for A.P.
    if (checkIsAP(rec, n))
        return true;
    else
        return false;
}

// Driver's Code
public static void main(String[] args)
{
    double arr[] = { 1.0 / 5.0, 1.0 / 10.0,
                     1.0 / 15.0, 1.0 / 20.0 };
    int n = arr.length;
    int flag = 0;

    // Function to check AP
    if (checkIsAP(arr, n)) {
        System.out.print("Yes, An AP can be formed"
             +"\n");
        flag = 1;
    }

    // Function to check GP
    if (checkIsGP(arr, n)) {
        System.out.print("Yes, A GP can be formed"
             +"\n");
        flag = 1;
    }

    // Function to check HP
    if (checkIsHP(arr, n)) {
        System.out.print("Yes, A HP can be formed"
             +"\n");
        flag = 1;
    }

    else if (flag == 0) {
        System.out.print("No");
    }
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to check if a 
# given array form AP, GP or HP

# Returns true if arr[0..n-1]
# can form AP
def checkIsAP(arr, n):

    # Base Case
    if (n == 1):
        return True

    # Sort array
    arr.sort();

    # After sorting, difference
    # between consecutive elements
    # must be same.
    d = arr[1] - arr[0]

    # Traverse the given array and
    # check if the difference
    # between ith element and (i-1)th
    # element is same or not
    for i in range(2, n):
        if (arr[i] - arr[i - 1] != d):
            return False

    return True

# Returns true if arr[0..n-1]
# can form GP
def checkIsGP(arr, n):

    # Base Case
    if (n == 1):
        return True

    # Sort array
    arr.sort()

    # After sorting, common ratio
    # between consecutive elements
    # must be same.
    r = arr[1] / arr[0]

    # Traverse the given array and
    # check if the common ratio
    # between ith element and (i-1)th
    # element is same or not
    for i in range(2, n):
        if (arr[i] / arr[i - 1] != r):
            return False

    return True

# Returns true if arr[0..n-1]
# can form HP
def checkIsHP(arr, n):

    # Base Case
    if (n == 1):
        return True

    rec = []

    # Find reciprocal of arr[]
    for i in range(0, n):
        rec.append((1 / arr[i]))

    # After finding reciprocal, check
    # if the reciprocal is in A. P.
    # To check for A.P.
    if (checkIsAP(rec, n)):
        return True
    else:
        return False

# Driver Code
arr = [ 1.0 / 5.0, 1.0 / 10.0,
        1.0 / 15.0, 1.0 / 20.0 ]
n = len(arr)
flag = 0

# Function to check AP
if (checkIsAP(arr, n)):
    print("Yes, An AP can be formed", end = '\n')
    flag = 1

# Function to check GP
if (checkIsGP(arr, n)):
    print("Yes, A GP can be formed", end = '\n')
    flag = 1

# Function to check HP
if (checkIsHP(arr, n)):
    print("Yes, A HP can be formed", end = '\n')
    flag = 1

elif (flag == 0):
    print("No", end = '\n')

# This code is contributed by Pratik
```

## C#

```
// C# program to check if a given
// array form AP, GP or HP
using System;

class GFG{

// Returns true if arr[0..n-1]
// can form AP
static bool checkIsAP(double []arr, int n)
{
    // Base Case
    if (n == 1)
        return true;

    // Sort array
    Array.Sort(arr);

    // After sorting, difference
    // between consecutive elements
    // must be same.
    double d = arr[1] - arr[0];

    // Traverse the given array and
    // check if the difference
    // between ith element and (i-1)th
    // element is same or not
    for (int i = 2; i < n; i++) {
        if (arr[i] - arr[i - 1] != d) {
            return false;
        }
    }

    return true;
}

// Returns true if arr[0..n-1]
// can form GP
static bool checkIsGP(double []arr, int n)
{
    // Base Case
    if (n == 1)
        return true;

    // Sort array
    Array.Sort(arr);

    // After sorting, common ratio
    // between consecutive elements
    // must be same.
    double r = arr[1] / arr[0];

    // Traverse the given array and
    // check if the common ratio
    // between ith element and (i-1)th
    // element is same or not
    for (int i = 2; i < n; i++) {
        if (arr[i] / arr[i - 1] != r)
            return false;
    }

    return true;
}

// Returns true if arr[0..n-1]
// can form HP
static bool checkIsHP(double []arr, int n)
{
    // Base Case
    if (n == 1) {
        return true;
    }

    double []rec = new double[n];

    // Find reciprocal of []arr
    for (int i = 0; i < n; i++) {
        rec[i] = ((1 / arr[i]));
    }

    // After finding reciprocal, check if
    // the reciprocal is in A. P.
    // To check for A.P.
    if (checkIsAP(rec, n))
        return true;
    else
        return false;
}

// Driver's Code
public static void Main(String[] args)
{
    double []arr = { 1.0 / 5.0, 1.0 / 10.0,
                     1.0 / 15.0, 1.0 / 20.0 };
    int n = arr.Length;
    int flag = 0;

    // Function to check AP
    if (checkIsAP(arr, n)) {
        Console.Write("Yes, An AP can be formed"
             +"\n");
        flag = 1;
    }

    // Function to check GP
    if (checkIsGP(arr, n)) {
        Console.Write("Yes, A GP can be formed"
             +"\n");
        flag = 1;
    }

    // Function to check HP
    if (checkIsHP(arr, n)) {
        Console.Write("Yes, A HP can be formed"
             +"\n");
        flag = 1;
    }

    else if (flag == 0) {
        Console.Write("No");
    }
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript program to check if a given
// array form AP, GP or HP

// Returns true if arr[0..n-1]
// can form AP
function checkIsAP(arr, n)
{
    // Base Case
    if (n == 1)
        return true;

    // Sort array
    arr.sort(function(a,b){return a-b;});

    // After sorting, difference
    // between consecutive elements
    // must be same.
    var d = arr[1] - arr[0];

    // Traverse the given array and
    // check if the difference
    // between ith element and (i-1)th
    // element is same or not
    for (var i = 2; i < n; i++) {
        if (arr[i] - arr[i - 1] != d) {
            return false;
        }
    }

    return true;
}

// Returns true if arr[0..n-1]
// can form GP
function checkIsGP(arr, n)
{
    // Base Case
    if (n == 1)
        return true;

    // Sort array
    arr.sort();

    // After sorting, common ratio
    // between consecutive elements
    // must be same.
    var r = arr[1] / arr[0];

    // Traverse the given array and
    // check if the common ratio
    // between ith element and (i-1)th
    // element is same or not
    for (var i = 2; i < n; i++) {
        if (arr[i] / arr[i - 1] != r)
            return false;
    }

    return true;
}

// Returns true if arr[0..n-1]
// can form HP
function checkIsHP(arr, n)
{
    // Base Case
    if (n == 1) {
        return true;
    }

    var rec = Array(n).fill(0);

    // Find reciprocal of arr[]
    for (var i = 0; i < n; i++) {
        rec[i] = ((1 / arr[i]));
    }

    // After finding reciprocal, check if
    // the reciprocal is in A. P.
    // To check for A.P.
    if (checkIsAP(rec, n))
        return true;
    else
        return false;
}

// Driver's Code
var arr = [ 1.0 / 5.0, 1.0 / 10.0,
                 1.0 / 15.0, 1.0 / 20.0 ];
var n = arr.length;
var flag = 0;

// Function to check AP
if (checkIsAP(arr, n)) {
    document.write("Yes, An AP can be formed");
    flag = 1;
}
// Function to check GP
if (checkIsGP(arr, n)) {
    document.write("Yes, A GP can be formed");
    flag = 1;
}
// Function to check HP
if (checkIsHP(arr, n)) {
    document.write("Yes, A HP can be formed");
    flag = 1;
}
else if (flag == 0) {
    document.write("No");
}

</script>
```

**Output:** 

```
Yes, A HP can be formed
```

**时间复杂度:** O(N*log N)

**辅助空间:** O(N)