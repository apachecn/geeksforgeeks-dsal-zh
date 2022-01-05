# 查询给定范围内斐波那契数的最大和最小差值

> 原文:[https://www . geesforgeks . org/查询给定范围内斐波那契数的最大和最小差值/](https://www.geeksforgeeks.org/queries-for-maximum-and-minimum-difference-between-fibonacci-numbers-in-given-ranges/)

给定一个包含形式为**【L，R】**的 **N** 查询的数组 **arr[][]** ，任务是找出每个查询范围内两个斐波那契数之间的最大差异。如果范围内没有斐波那契数或只有一个斐波那契数，则打印 0。
**注:**所有范围均在 100005 以下。

**示例:**

> **输入:** N = 2，arr[][] = {{2，2}，{2，5}}
> **输出:** 0 3
> **说明:**
> 在第一次查询中，只有一个斐波那契数。所以，答案是 0。
> 在第二个查询中，2 是最小值，5 是最大斐波那契数。
> 因此，最大差值= 3。
> 
> **输入:** N = 2，arr[][] = {{2，21}，{30，150}}
> **输出:** 19 110
> **解释:**
> 在第一个查询中，2 是最小的，5 是最大的斐波那契数。
> 因此，最大差值= 19。
> 在第二个查询中，34 是最小值，144 是最大斐波那契数。
> 因此，最大差值= 110。

**方法:**思路是利用[哈希](https://www.geeksforgeeks.org/hashing-data-structure/)和[前缀和数组](https://www.geeksforgeeks.org/prefix-sum-array-implementation-applications-competitive-programming/)的概念，将[斐波那契数](https://www.geeksforgeeks.org/program-for-nth-fibonacci-number/)预先计算并存储在两个数组**前缀[]** 和**后缀[]** 中。

执行上述预计算后，我们可以检查一个数字是否是斐波那契数列。因此，为了执行上述操作，使用了以下方法:

1.  **求最大差:**为了求最大差，使用每个索引存储小于‘I’的最大斐波那契数的前缀数组和每个索引存储大于‘I’的最小斐波那契数的后缀数组。对于每个查询{L，R}，返回**前缀[R]–后缀[L]** 。
2.  **求最小差:**范围{L，R}内前两个数的差就是最小可能差。

下面是上述方法的实现:

## C++

```
// C++ program to find the maximum differences
// between two Fibonacci numbers in given ranges

#include <bits/stdc++.h>
using namespace std;
#define MAX 100005

bool isFib[MAX];
int prefix[MAX], suffix[MAX];

// Function to precompute the Fibonacci,
// Prefix array and Suffix array
void precompute()
{
    // Initializing it with False
    memset(isFib, false, sizeof(isFib));
    // Variable to store the Fibonacci
    // numbers

    // Marking the first two Fibonacci numbers
    // as True in the array
    int prev = 0, curr = 1;
    isFib[prev] = isFib[curr] = true;

    // Loop to iterate until the maximum number
    while (curr < MAX) {
        int temp = curr + prev;
        isFib[temp] = true;
        prev = curr;
        curr = temp;
    }

    prefix[1] = 1;
    suffix[MAX - 1] = 1e9 + 7;

    // Precomputing Prefix array
    for (int i = 2; i < MAX; i++) {

        // If the number is a Fibonacci number,
        // then adding it to the prefix array
        if (isFib[i])
            prefix[i] = i;
        else
            prefix[i] = prefix[i - 1];
    }

    // Precompute Suffix array
    for (int i = MAX - 1; i > 1; i--) {
        if (isFib[i])
            suffix[i] = i;
        else
            suffix[i] = suffix[i + 1];
    }
}

// Function to solve each query
int query(int L, int R)
{
    if (prefix[R] < L || suffix[L] > R)
        return 0;
    else
        return prefix[R] - suffix[L];
}

// Function to return the minimum difference
// between any two fibonacci numbers
// from the given range [L, R]
int minDifference(int L, int R)
{

    // Find the first Fibonacci numbers
    // from the range
    int fst = 0;

    for (int i = L; i <= R; i++) {

        if (isFib[i]) {
            fst = i;
            break;
        }
    }

    // Find the second Fibonacci numbers
    // from the range
    int snd = 0;
    for (int i = fst + 1; i <= R; i++) {

        if (isFib[i]) {
            snd = i;
            break;
        }
    }

    // If the number of fibonacci numbers in
    // the given range is < 2
    if (snd == 0)
        return -1;

    // To store the minimum difference between
    // two consecutive fibonacci numbers from the range
    int diff = snd - fst;

    // Range left to check for fibonacci numbers
    int left = snd + 1;
    int right = R;

    // For every integer in the range
    for (int i = left; i <= right; i++) {

        // If the current integer is fibonacci
        if (isFib[i]) {

            // If the difference between i
            // and snd is minimum so far
            if (i - snd <= diff) {

                fst = snd;
                snd = i;
                diff = snd - fst;
            }
        }
    }

    return diff;
}

// Function to print the answer
// for every query
void findAns(int arr[][2], int q)
{

    precompute();

    // Finding the answer for every query
    for (int i = 0; i < q; i++) {

        cout << "Maximum Difference: "
            << query(arr[i][0], arr[i][1])
            << endl;

        cout << "Minimum Difference: "
            << minDifference(arr[i][0], arr[i][1])
            << endl;
    }
}

// Driver code
int main()
{
    int q = 1;

    int arr[][2] = { { 21, 100 } };

    findAns(arr, q);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the maximum
// differences between two Fibonacci
// numbers in given ranges
import java.util.*;
import java.lang.*;

class GFG{

static final int MAX = 100005;

static boolean isFib[] = new boolean[MAX];
static int[] prefix = new int[MAX],
             suffix = new int[MAX];

// Function to precompute the Fibonacci,
// Prefix array and Suffix array
static void precompute()
{

    // Variable to store the Fibonacci
    // numbers

    // Marking the first two Fibonacci
    // numbers as True in the array
    int prev = 0, curr = 1;
    isFib[prev] = isFib[curr] = true;

    // Loop to iterate until the
    // maximum number
    while (curr + prev < MAX)
    {
        int temp = curr + prev;
        isFib[temp] = true;
        prev = curr;
        curr = temp;
    }

    prefix[1] = 1;
    suffix[MAX - 1] = (int)1e9 + 7;

    // Precomputing Prefix array
    for(int i = 2; i < MAX; i++)
    {

        // If the number is a Fibonacci
        // number, then adding it to the
        // prefix array
        if (isFib[i])
            prefix[i] = i;
        else
            prefix[i] = prefix[i - 1];
    }

    // Precompute Suffix array
    for(int i = MAX - 2; i > 1; i--)
    {
        if (isFib[i])
            suffix[i] = i;
        else
            suffix[i] = suffix[i + 1];
    }
}

// Function to solve each query
static int query(int L, int R)
{
    if (prefix[R] < L || suffix[L] > R)
        return 0;
    else
        return prefix[R] - suffix[L];
}

// Function to return the minimum
// difference between any two
// fibonacci numbers from the
// given range [L, R]
static int minDifference(int L, int R)
{

    // Find the first Fibonacci numbers
    // from the range
    int fst = 0;

    for(int i = L; i <= R; i++)
    {
        if (isFib[i])
        {
            fst = i;
            break;
        }
    }

    // Find the second Fibonacci numbers
    // from the range
    int snd = 0;
    for(int i = fst + 1; i <= R; i++)
    {
        if (isFib[i])
        {
            snd = i;
            break;
        }
    }

    // If the number of fibonacci
    // numbers in the given range is < 2
    if (snd == 0)
        return -1;

    // To store the minimum difference
    // between two consecutive fibonacci
    // numbers from the range
    int diff = snd - fst;

    // Range left to check for
    // fibonacci numbers
    int left = snd + 1;
    int right = R;

    // For every integer in the range
    for(int i = left; i <= right; i++)
    {

        // If the current integer is fibonacci
        if (isFib[i])
        {

            // If the difference between i
            // and snd is minimum so far
            if (i - snd <= diff)
            {
                fst = snd;
                snd = i;
                diff = snd - fst;
            }
        }
    }
    return diff;
}

// Function to print the answer
// for every query
static void findAns(int arr[][], int q)
{
    precompute();

    // Finding the answer for every query
    for(int i = 0; i < q; i++)
    {
       System.out.println("Maximum Difference: " +
                    query(arr[i][0], arr[i][1]));

       System.out.println("Minimum Difference: " +
            minDifference(arr[i][0], arr[i][1]));
    }
}

// Driver code
public static void main(String[] args)
{
    int q = 1;

    int arr[][] = { { 21, 100 } };

    findAns(arr, q);
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 program to find the maximum differences
# between two Fibonacci numbers in given ranges

MAX = 100005

isFib = [False]*MAX
prefix = [0]*MAX
suffix = [0]*MAX

# Function to precompute the Fibonacci,
# Prefix array and Suffix array
def precompute():

    # Marking the first two Fibonacci numbers
    # as True in the array
    prev , curr = 0 , 1
    isFib[prev] = True
    isFib[curr] = True

    # Loop to iterate until the maximum number
    while (curr < MAX):
        temp = curr + prev
        if temp<MAX:
            isFib[temp] = True
        prev = curr
        curr = temp

    prefix[1] = 1
    suffix[MAX - 1] = 1000000007

    # Precomputing Prefix array
    for i in range(2, MAX):

        # If the number is a Fibonacci number,
        # then adding it to the prefix array
        if (isFib[i]):
            prefix[i] = i
        else:
            prefix[i] = prefix[i - 1]

    # Precompute Suffix array
    for i in range(MAX - 2, 1, -1):
        if (isFib[i]):
            suffix[i] = i
        else:
            suffix[i] = suffix[i + 1]

# Function to solve each query
def query(L, R):

    if (prefix[R] < L or suffix[L] > R):
        return 0
    else:
        return prefix[R] - suffix[L]

# Function to return the minimum difference
# between any two fibonacci numbers
# from the given range [L, R]
def minDifference(L, R):

    # Find the first Fibonacci numbers
    # from the range
    fst = 0
    for i in range(L, R + 1):
        if (isFib[i]):
            fst = i
            break

    # Find the second Fibonacci numbers
    # from the range
    snd = 0
    for i in range(fst + 1, R + 1 ):

        if (isFib[i]):
            snd = i
            break

    # If the number of fibonacci numbers in
    # the given range is < 2
    if (snd == 0):
        return -1

    # To store the minimum difference between
    # two consecutive fibonacci numbers from the range
    diff = snd - fst

    # Range left to check for fibonacci numbers
    left = snd + 1
    right = R

    # For every integer in the range
    for i in range(left, right + 1):

        # If the current integer is fibonacci
        if (isFib[i]):
            # If the difference between i
            # and snd is minimum so far
            if (i - snd <= diff):
                fst = snd
                snd = i
                diff = snd - fst
    return diff

# Function to print the answer
# for every query
def findAns(arr, q):

    precompute()

    # Finding the answer for every query
    for i in range(q):

        print( "Maximum Difference: "
            , query(arr[i][0], arr[i][1]))

        print("Minimum Difference: "
            , minDifference(arr[i][0], arr[i][1]))

# Driver code
if __name__ == "__main__":

    q = 1

    arr = [ [ 21, 100 ] ]

    findAns(arr, q)

# This code is contributed by chitranayal
```

## C#

```
using System;

// C# program to find the maximum
// differences between two Fibonacci
// numbers in given ranges
public class GFG{

  static int MAX = 100005;
  static bool[] isFib = new bool[MAX];

  static int[] prefix = new int[MAX],
  suffix = new int[MAX];

  // Function to precompute the Fibonacci,
  // Prefix array and Suffix array
  static void precompute()
  {

    // Variable to store the Fibonacci
    // numbers

    // Marking the first two Fibonacci
    // numbers as True in the array
    int prev = 0, curr = 1;
    isFib[prev] = isFib[curr] = true;

    // Loop to iterate until the
    // maximum number
    while (curr + prev < MAX)
    {
      int temp = curr + prev;
      isFib[temp] = true;
      prev = curr;
      curr = temp;
    }

    prefix[1] = 1;
    suffix[MAX - 1] = (int)1e9 + 7;

    // Precomputing Prefix array
    for(int i = 2; i < MAX; i++)
    {

      // If the number is a Fibonacci
      // number, then adding it to the
      // prefix array
      if (isFib[i])
        prefix[i] = i;
      else
        prefix[i] = prefix[i - 1];
    }

    // Precompute Suffix array
    for(int i = MAX - 2; i > 1; i--)
    {
      if (isFib[i])
        suffix[i] = i;
      else
        suffix[i] = suffix[i + 1];
    }
  }

  // Function to solve each query
  static int query(int L, int R)
  {
    if (prefix[R] < L || suffix[L] > R)
      return 0;
    else
      return prefix[R] - suffix[L];
  }

  // Function to return the minimum
  // difference between any two
  // fibonacci numbers from the
  // given range [L, R]
  static int minDifference(int L, int R)
  {

    // Find the first Fibonacci numbers
    // from the range
    int fst = 0;

    for(int i = L; i <= R; i++)
    {
      if (isFib[i])
      {
        fst = i;
        break;
      }
    }

    // Find the second Fibonacci numbers
    // from the range
    int snd = 0;
    for(int i = fst + 1; i <= R; i++)
    {
      if (isFib[i])
      {
        snd = i;
        break;
      }
    }

    // If the number of fibonacci
    // numbers in the given range is < 2
    if (snd == 0)
      return -1;

    // To store the minimum difference
    // between two consecutive fibonacci
    // numbers from the range
    int diff = snd - fst;

    // Range left to check for
    // fibonacci numbers
    int left = snd + 1;
    int right = R;

    // For every integer in the range
    for(int i = left; i <= right; i++)
    {

      // If the current integer is fibonacci
      if (isFib[i])
      {

        // If the difference between i
        // and snd is minimum so far
        if (i - snd <= diff)
        {
          fst = snd;
          snd = i;
          diff = snd - fst;
        }
      }
    }
    return diff;
  }

  // Function to print the answer
  // for every query
  static void findAns(int[,] arr, int q)
  {
    precompute();

    // Finding the answer for every query
    for(int i = 0; i < q; i++)
    {
      Console.WriteLine("Maximum Difference: " +
                        query(arr[i,0], arr[i,1]));

      Console.WriteLine("Minimum Difference: " +
                        minDifference(arr[i,0], arr[i,1]));
    }
  }

  // Driver code
  static public void Main ()
  {

    int q = 1;

    int[,] arr = { { 21, 100 } };

    findAns(arr, q);

  }
}

// This code is contributed by avanitrachhadiya2155
```

## java 描述语言

```
<script>

// JavaScript program to find the maximum differences
// between two Fibonacci numbers in given ranges

let MAX = 100005

let isFib = new Array(MAX);
let prefix = new Array(MAX)
let suffix = new Array(MAX);

// Function to precompute the Fibonacci,
// Prefix array and Suffix array
function precompute()
{
    // Initializing it with False
    isFib.fill(false);
    // Variable to store the Fibonacci
    // numbers

    // Marking the first two Fibonacci numbers
    // as True in the array
    let prev = 0, curr = 1;
    isFib[prev] = isFib[curr] = true;

    // Loop to iterate until the maximum number
    while (curr < MAX) {
        let temp = curr + prev;
        isFib[temp] = true;
        prev = curr;
        curr = temp;
    }

    prefix[1] = 1;
    suffix[MAX - 1] = 1e9 + 7;

    // Precomputing Prefix array
    for (let i = 2; i < MAX; i++) {

        // If the number is a Fibonacci number,
        // then adding it to the prefix array
        if (isFib[i])
            prefix[i] = i;
        else
            prefix[i] = prefix[i - 1];
    }

    // Precompute Suffix array
    for (let i = MAX - 1; i > 1; i--) {
        if (isFib[i])
            suffix[i] = i;
        else
            suffix[i] = suffix[i + 1];
    }
}

// Function to solve each query
function query(L, R)
{
    if (prefix[R] < L || suffix[L] > R)
        return 0;
    else
        return prefix[R] - suffix[L];
}

// Function to return the minimum difference
// between any two fibonacci numbers
// from the given range [L, R]
function minDifference(L, R)
{

    // Find the first Fibonacci numbers
    // from the range
    let fst = 0;

    for (let i = L; i <= R; i++) {

        if (isFib[i]) {
            fst = i;
            break;
        }
    }

    // Find the second Fibonacci numbers
    // from the range
    let snd = 0;
    for (let i = fst + 1; i <= R; i++) {

        if (isFib[i]) {
            snd = i;
            break;
        }
    }

    // If the number of fibonacci numbers in
    // the given range is < 2
    if (snd == 0)
        return -1;

    // To store the minimum difference between
    // two consecutive fibonacci numbers from the range
    let diff = snd - fst;

    // Range left to check for fibonacci numbers
    let left = snd + 1;
    let right = R;

    // For every integer in the range
    for (let i = left; i <= right; i++) {

        // If the current integer is fibonacci
        if (isFib[i]) {

            // If the difference between i
            // and snd is minimum so far
            if (i - snd <= diff) {

                fst = snd;
                snd = i;
                diff = snd - fst;
            }
        }
    }

    return diff;
}

// Function to print the answer
// for every query
function findAns(arr, q)
{

    precompute();

    // Finding the answer for every query
    for (let i = 0; i < q; i++) {

        document.write("Maximum Difference: "
            + query(arr[i][0], arr[i][1])
            + "<br>");

        document.write("Minimum Difference: "
            + minDifference(arr[i][0], arr[i][1])
            + "<br>");
    }
}

// Driver code

let q = 1;

let arr = [ [ 21, 100 ] ];

findAns(arr, q);

</script>
```

**输出:**

```
Maximum Difference: 68
Minimum Difference: 13
```