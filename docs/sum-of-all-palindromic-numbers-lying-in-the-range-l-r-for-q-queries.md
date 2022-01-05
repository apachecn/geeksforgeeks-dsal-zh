# 位于范围[L，R]内的所有回文数字的总和，用于 Q 查询

> 原文:[https://www . geeksforgeeks . org/所有回文数字的总和-范围内-l-r-for-q-query/](https://www.geeksforgeeks.org/sum-of-all-palindromic-numbers-lying-in-the-range-l-r-for-q-queries/)

给定以 2D [数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**arr【】【】**形式的 **Q** 查询，其每行由表示范围【L，R】的两个数字 **L** 和 **R** 组成，任务是找到位于范围**【L，R】**中的所有[回文数字](https://www.geeksforgeeks.org/check-if-a-number-is-palindrome/)的总和。

> **输入:** Q = 2，arr[][] = { {10，13}，{12，21} }
> **输出:**
> 11
> 0
> **说明:**
> 从 10 到 13 只有 11 是回文号
> 从 12 到 21 没有回文号
> **输入:** Q = 4，arr[]= { { 10，10

**进场:**
思路是使用[前缀和阵](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)。直到特定索引所有[回文号](https://www.geeksforgeeks.org/check-if-a-number-is-palindrome/)的总和被预先计算并存储在一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/)**pref【】**中，这样每个查询都可以在 **O(1)** 时间内被回答。

1.  初始化前缀数组 **pref[]** 。
2.  从 1 到 N 迭代，检查数字是否回文:
    *   如果该数字是回文，则 **pref[]** 的当前索引将存储该数字与 **pref[]** 的先前索引处的数字之和。
    *   否则**pref【】**当前指数与**pref【】**前一指数值相同。
3.  对于 **Q** 查询范围**【L，R】**的所有[回文号](https://www.geeksforgeeks.org/generate-palindromic-numbers-less-n/)之和可以找到如下:

```
sum = pref[R] - pref[L - 1]
```

以下是上述方法的实施

## C++

```
// C++ program to find the sum
// of all palindrome numbers
// in the given range
#include <bits/stdc++.h>
using namespace std;

// pref[] array to precompute
// the sum of all palindromic
// number
long long pref[100001];

// Function that return number
// num if num is palindromic
// else return 0
int checkPalindrome(int num)
{

    // Convert num to string
    string str = to_string(num);

    int l = 0, r = str.length() - 1;

    while (l < r) {
        if (str[l] != str[r]) {
            return 0;
        }
        l++;
        r--;
    }
    return num;
}

// Function to precompute the
// sum of all palindrome numbers
// upto 100000
void preCompute()
{
    for (int i = 1; i <= 100000; ++i) {

        // checkPalindrome()
        // return the number i
        // if i is palindromic
        // else return 0
        pref[i] = pref[i - 1]
                  + checkPalindrome(i);
    }
}

// Function to print the sum
// for each query
void printSum(int L, int R)
{
    cout << pref[R] - pref[L - 1]
         << endl;
}

// Function to print sum of all
// palindromic numbers between
// [L, R]
void printSumPalindromic(int arr[][2],
                         int Q)
{

    // Function that pre computes
    // the sum of all palindromic
    // numbers
    preCompute();

    // Iterate over all Queries
    // to print the sum
    for (int i = 0; i < Q; i++) {
        printSum(arr[i][0], arr[i][1]);
    }
}

// Driver code
int main()
{
    // Queries
    int Q = 2;
    int arr[][2] = { { 10, 13 },
                     { 12, 21 } };

    // Function that print the
    // the sum of all palindromic
    // number in Range [L, R]
    printSumPalindromic(arr, Q);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the sum
// of all palindrome numbers
// in the given range
import java.util.*;

class GFG{

// pref[] array to precompute
// the sum of all palindromic
// number
static int []pref = new int[100001];

// Function that return number
// num if num is palindromic
// else return 0
static int checkPalindrome(int num)
{

    // Convert num to String
    String str = String.valueOf(num);

    int l = 0, r = str.length() - 1;

    while (l < r) {
        if (str.charAt(l) != str.charAt(r)) {
            return 0;
        }
        l++;
        r--;
    }
    return num;
}

// Function to precompute the
// sum of all palindrome numbers
// upto 100000
static void preCompute()
{
    for (int i = 1; i <= 100000; ++i) {

        // checkPalindrome()
        // return the number i
        // if i is palindromic
        // else return 0
        pref[i] = pref[i - 1]
                  + checkPalindrome(i);
    }
}

// Function to print the sum
// for each query
static void printSum(int L, int R)
{
    System.out.print(pref[R] - pref[L - 1]
         +"\n");
}

// Function to print sum of all
// palindromic numbers between
// [L, R]
static void printSumPalindromic(int arr[][],
                         int Q)
{

    // Function that pre computes
    // the sum of all palindromic
    // numbers
    preCompute();

    // Iterate over all Queries
    // to print the sum
    for (int i = 0; i < Q; i++) {
        printSum(arr[i][0], arr[i][1]);
    }
}

// Driver code
public static void main(String[] args)
{
    // Queries
    int Q = 2;
    int arr[][] = { { 10, 13 },
                     { 12, 21 } };

    // Function that print the
    // the sum of all palindromic
    // number in Range [L, R]
    printSumPalindromic(arr, Q);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find the sum
# of all palindrome numbers
# in the given range

# pref[] array to precompute
# the sum of all palindromic
# number
pref=[0]*100001

# Function that return number
# num if num is palindromic
# else return 0
def checkPalindrome(num):

    # Convert num to string
    strr = str(num)
    l = 0
    r = len(strr)- 1
    while (l < r):
        if (strr[l] != strr[r]):
            return 0

        l+=1
        r-=1

    return num

# Function to precompute the
# sum of all palindrome numbers
# upto 100000
def preCompute():
    for i in range(1,100001):
        # checkPalindrome()
        # return the number i
        # if i is palindromic
        # else return 0
        pref[i] = pref[i - 1]+ checkPalindrome(i)

# Function to print the sum
# for each query
def printSum(L, R):
    print(pref[R] - pref[L - 1])

# Function to prsum of all
# palindromic numbers between
# [L, R]
def printSumPalindromic(arr,Q):

    # Function that pre computes
    # the sum of all palindromic
    # numbers
    preCompute()

    # Iterate over all Queries
    # to print the sum
    for i in range(Q):
        printSum(arr[i][0], arr[i][1])

# Driver code

# Queries
Q = 2
arr= [[10, 13 ],[ 12, 21 ]]

# Function that print the
# the sum of all palindromic
# number in Range [L, R]
printSumPalindromic(arr, Q)

# This code is contributed by shivanisinghss2110
```

## C#

```
// C# program to find the sum
// of all palindrome numbers
// in the given range
using System;

class GFG{

// pref[] array to precompute
// the sum of all palindromic
// number
static int []pref = new int[100001];

// Function that return number
// num if num is palindromic
// else return 0
static int checkPalindrome(int num)
{

    // Convert num to String
    String str = String.Join("",num);

    int l = 0, r = str.Length - 1;

    while (l < r) {
        if (str[l] != str[r]) {
            return 0;
        }
        l++;
        r--;
    }
    return num;
}

// Function to precompute the
// sum of all palindrome numbers
// upto 100000
static void preCompute()
{
    for (int i = 1; i <= 100000; ++i) {

        // checkPalindrome()
        // return the number i
        // if i is palindromic
        // else return 0
        pref[i] = pref[i - 1]
                  + checkPalindrome(i);
    }
}

// Function to print the sum
// for each query
static void printSum(int L, int R)
{
    Console.Write(pref[R] - pref[L - 1]
         +"\n");
}

// Function to print sum of all
// palindromic numbers between
// [L, R]
static void printSumPalindromic(int [,]arr,
                         int Q)
{

    // Function that pre computes
    // the sum of all palindromic
    // numbers
    preCompute();

    // Iterate over all Queries
    // to print the sum
    for (int i = 0; i < Q; i++) {
        printSum(arr[i,0], arr[i,1]);
    }
}

// Driver code
public static void Main(String[] args)
{
    // Queries
    int Q = 2;
    int [,]arr = { { 10, 13 },
                     { 12, 21 } };

    // Function that print the
    // the sum of all palindromic
    // number in Range [L, R]
    printSumPalindromic(arr, Q);
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>

// Javascript program to find the sum
// of all palindrome numbers
// in the given range

// pref[] array to precompute
// the sum of all palindromic
// number
var pref=Array(100001).fill(0);

// Function that return number
// num if num is palindromic
// else return 0
function checkPalindrome(num)
{

    // Convert num to string
    var str = num.toString();

    var l = 0, r = str.length - 1;

    while (l < r) {
        if (str[l] != str[r]) {
            return 0;
        }
        l++;
        r--;
    }
    return num;
}

// Function to precompute the
// sum of all palindrome numbers
// upto 100000
function preCompute()
{
    for (var i = 1; i <= 100000; ++i) {

        // checkPalindrome()
        // return the number i
        // if i is palindromic
        // else return 0
        pref[i] = pref[i - 1]
                  + checkPalindrome(i);
    }
}

// Function to print the sum
// for each query
function printSum(L, R)
{
    document.write( pref[R] - pref[L - 1]+"<br>");
}

// Function to print sum of all
// palindromic numbers between
// [L, R]
function printSumPalindromic(arr, Q)
{

    // Function that pre computes
    // the sum of all palindromic
    // numbers
    preCompute();

    // Iterate over all Queries
    // to print the sum
    for (var i = 0; i < Q; i++) {
        printSum(arr[i][0], arr[i][1]);
    }
}

// Driver code

// Queries
var Q = 2;
var arr = [ [ 10, 13 ],
                 [ 12, 21 ] ];

// Function that print the
// the sum of all palindromic
// number in Range [L, R]
printSumPalindromic(arr, Q);

</script>
```

**Output:** 

```
11
0
```

**时间复杂度:**O(N)
T3】辅助空间: O(10 <sup>5</sup>