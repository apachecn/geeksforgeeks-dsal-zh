# 排列，使得相邻元素的和不能被 3 整除

> 原文:[https://www . geeksforgeeks . org/数组的排列使得相邻元素的和不能被 3 整除/](https://www.geeksforgeeks.org/permutation-of-array-such-that-sum-of-adjacent-elements-are-not-divisible-by-3/)

给定一个正整数数组 **arr[]** ，任务是找到数组的排列，使得相邻元素的和不能被 3 整除。

**注意:**如果数组 print -1 没有这样的排列。

**示例:**

> **输入:** arr[] = {1，2，3，4，5}
> **输出:** 4 1 3 5 2
> **解释:**
> 相邻元素之和=>
> arr[0]+arr[1]= 4+1 = 5% 3！= 0
> arr[1] + arr[2] = 1 + 3 = 4 % 3！= 0
> arr[2] + arr[3] = 3 + 5 = 8 % 3！= 0
> arr[3] + arr[4] = 5 + 2 = 7 % 3！= 0
> 
> **输入:** arr[] = {1，24，30，42，51}
> **输出:** -1

**方法:**问题的关键观察是，对于所有类型的数字，只能有三种类型的余数，即{0，1，2}。因此，我们可以把数分成三部分，如果我们把余数为 0 的数和余数为 1 或 2 的数排列在一起。那么它们的和不能被 3 整除。如果没有办法以这种方式排列所有的数字，那么就没有排列使得它们的相邻元素之和不能被 3 整除。

下面是上述方法的实现:

## C++

```
// C++ implementation to find the
// permutation of the array such that
// sum of adjacent elements is not
// divisible by 3

#include <bits/stdc++.h>
using namespace std;
#define hell 1000000007
#define N 100005

// Function to segregate numbers
// based on their remainder
// when divided by three
void count_k(
    vector<int>& arr, int& c_0,
    int& c_1, int& c_2,
    stack<int>& ones,
    stack<int>& twos,
    stack<int>& zeros)
{
    // Loop to iterate over the elements
    // of the given array
    for (int i = 0; i < arr.size(); i++) {

        // Condition to check the
        // remainder of the number
        if (arr[i] % 3 == 0) {
            c_0++;
            zeros.push(arr[i]);
        }
        else if (arr[i] % 3 == 1) {
            c_1++;
            ones.push(arr[i]);
        }
        else {
            c_2++;
            twos.push(arr[i]);
        }
    }
    return;
}

// Function to find the permutation
// of the array such that sum of
// adjacent elements is not divisible by 3
void printArrangement(
    vector<int>& arr,
    int& c_0, int& c_1, int& c_2,
    stack<int>& ones,
    stack<int>& twos,
    stack<int>& zeros)
{
    // Condition to check when
    // it's impossible to arrange
    if ((c_0 == 0 && c_1 != 0 && c_2 != 0)
        or c_0 > c_1 + c_2 + 1) {
        cout << "-1";
        return;
    }

    // Condition to check when
    // there are no zeros, and
    // only ones or only twos
    if (c_0 == 0) {
        for (int i = 0; i < arr.size(); i++) {
            cout << arr[i] << " ";
        }
        return;
    }

    // Array to store the permutation
    int i, j, ans[N];
    memset(ans, -1, sizeof(ans));

    // Place the ones on alternate places
    // in the answer array,
    // leaving spaces for zeros remainder
    // elements in the array
    for (i = 1, j = 0; j < c_1; i += 2, j++) {
        ans[i] = ones.top();
        ones.pop();
    }

    // Adding a zero to
    // connect it with a two
    ans[i - 1] = zeros.top();
    zeros.pop();
    c_0--;

    // Place the twos on alternate places
    // in the answer array,
    // leaving spaces for zeros
    for (j = 0; j < c_2; j++, i += 2) {
        ans[i] = twos.top();
        twos.pop();
    }

    // Fill the zeros finally,
    // between the ones and the twos
    for (int k = 0; c_0 > 0; k += 2) {
        if (ans[k] == -1) {
            ans[k] = zeros.top();
            c_0--;
        }
    }

    // Print the arrangement of the array
    for (int i = 0; i < N; i++) {
        if (ans[i] != -1)
            cout << ans[i] << " ";
    }
    return;
}

// Function to solve the problem
void solve(int n,
           vector<int>& arr)
{

    // As there can be only 3 remainders
    stack<int> ones, zeros, twos;

    int c_0 = 0, c_1 = 0, c_2 = 0;
    count_k(arr, c_0, c_1, c_2,
            ones, twos, zeros);

    // Function Call
    printArrangement(
        arr, c_0, c_1, c_2,
        ones, twos, zeros);
}

// Driver Code
signed main()
{
    int n = 5;
    vector<int> arr{ 1, 2, 3, 4, 5 };

    solve(n, arr);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation to find the
// permutation of the array such that
// sum of adjacent elements is not
// divisible by 3
import java.util.*;
class GFG{

static final int hell = 1000000007;
static final int N = 100005;
static int c_0, c_1, c_2;

// Function to segregate numbers
// based on their remainder
// when divided by three
static void count_k(int []arr,
                    Stack<Integer> ones,
                    Stack<Integer> twos,
                    Stack<Integer> zeros)
{
  // Loop to iterate over
  // the elements of the
  // given array
  for (int i = 0; i < arr.length; i++)
  {
    // Condition to check the
    // remainder of the number
    if (arr[i] % 3 == 0)
    {
      c_0++;
      zeros.add(arr[i]);
    }
    else if (arr[i] % 3 == 1)
    {
      c_1++;
      ones.add(arr[i]);
    }
    else
    {
      c_2++;
      twos.add(arr[i]);
    }
  }
  return;
}

// Function to find the permutation
// of the array such that sum of
// adjacent elements is not divisible by 3
static void printArrangement(int []arr,
                             Stack<Integer> ones,
                             Stack<Integer> twos,
                             Stack<Integer> zeros)
{
  // Condition to check when
  // it's impossible to arrange
  if ((c_0 == 0 && c_1 != 0 && c_2 != 0) ||
       c_0 > c_1 + c_2 + 1)
  {
    System.out.print("-1");
    return;
  }

  // Condition to check when
  // there are no zeros, and
  // only ones or only twos
  if (c_0 == 0)
  {
    for (int i = 0; i < arr.length; i++)
    {
      System.out.print(arr[i] + " ");
    }
    return;
  }

  // Array to store the permutation
  int i, j;
  int []ans = new int[N];
  Arrays.fill(ans, -1);

  // Place the ones on alternate places
  // in the answer array,
  // leaving spaces for zeros remainder
  // elements in the array
  for (i = 1, j = 0; j < c_1; i += 2, j++)
  {
    ans[i] = ones.peek();
    ones.pop();
  }

  // Adding a zero to
  // connect it with a two
  ans[i - 1] = zeros.peek();
  zeros.pop();
  c_0--;

  // Place the twos on alternate places
  // in the answer array,
  // leaving spaces for zeros
  for (j = 0; j < c_2; j++, i += 2)
  {
    ans[i] = twos.peek();
    twos.pop();
  }

  // Fill the zeros finally,
  // between the ones and the twos
  for (int k = 0; c_0 > 0; k += 2)
  {
    if (ans[k] == -1)
    {
      ans[k] = zeros.peek();
      c_0--;
    }
  }

  // Print the arrangement of the array
  for (int i1 = 0; i1 < N; i1++)
  {
    if (ans[i1] != -1)
      System.out.print(ans[i1] + " ");
  }
  return;
}

// Function to solve the problem
static void solve(int n, int []arr)
{
  // As there can be only 3 remainders
  Stack<Integer> ones = new Stack<Integer>();
  Stack<Integer> zeros = new Stack<Integer>();
  Stack<Integer> twos = new Stack<Integer>();

  c_0 = 0;
  c_1 = 0;
  c_2 = 0;
  count_k(arr, ones, twos, zeros);

  // Function Call
  printArrangement(arr, ones, twos, zeros);
}

// Driver Code
public static void main(String[] args)
{
  int n = 5;
  int []arr = {1, 2, 3, 4, 5};
  solve(n, arr);
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 implementation to find the
# permutation of the array such that
# sum of adjacent elements is not
# divisible by 3
hell = 1000000007
N = 100005
c_0 = 0
c_1 = 0
c_2 = 0

# Function to segregate numbers
# based on their remainder
# when divided by three
def count_k(arr, ones, twos, zeros):

    global c_0, c_1, c_2

    # Loop to iterate over
    # the elements of the
    # given array
    for i in range(len(arr)):

        # Condition to check the
        # remainder of the number
        if (arr[i] % 3 == 0):
            c_0 += 1
            zeros.append(arr[i])

        elif (arr[i] % 3 == 1):
            c_1 += 1
            ones.append(arr[i])

        else:

            c_2 += 1
            twos.append(arr[i])

# Function to find the permutation
# of the array such that sum of
# adjacent elements is not divisible by 3
def printArrangement(arr, ones, twos, zeros):

    global c_0, c_1, c_2

    # Condition to check when
    # it's impossible to arrange
    if ((c_0 == 0 and c_1 != 0 and
        c_2 != 0) or c_0 > c_1 + c_2 + 1):
        print("-1", end = "")
        return

    # Condition to check when
    # there are no zeros, and
    # only ones or only twos
    if (c_0 == 0):
        for i in range(len(arr)):
            print(arr[i], end = " ")

        return

    # Array to store the permutation
    ans = [-1] * N

    # Place the ones on alternate places
    # in the answer array,
    # leaving spaces for zeros remainder
    # elements in the array
    i, j = 1, 0

    while (j < c_1):
        ans[i] = ones[-1]
        ones.pop()
        i += 2
        j += 1

    # Adding a zero to
    # connect it with a two
    ans[i - 1] = zeros[-1]
    zeros.pop()
    c_0 -= 1

    # Place the twos on alternate
    # places in the answer array,
    # leaving spaces for zeros
    j = 0

    while (j < c_2):
        ans[i] = twos[-1]
        twos.pop()
        j += 1
        i += 2

    # Fill the zeros finally,
    # between the ones and the twos
    k = 0

    while c_0 > 0:
        if (ans[k] == -1):
            ans[k] = zeros[-1]
            c_0 -= 1

        k += 2

    # Print the arrangement of the array
    for i1 in range(N):
        if (ans[i1] != -1):
            print(ans[i1], end = " ")

    return

# Function to solve the problem
def solve(n, arr):

    # As there can be only 3 remainders
    ones = []
    zeros = []
    twos = []

    count_k(arr, ones, twos, zeros)

    # Function Call
    printArrangement(arr, ones, twos, zeros)

# Driver Code
n = 5
arr = [ 1, 2, 3, 4, 5 ]

solve(n, arr)

# This code is contributed by divyesh072019
```

## C#

```
// C# implementation to find the
// permutation of the array such that
// sum of adjacent elements is not
// divisible by 3
using System;
using System.Collections.Generic;
class GFG{

static readonly int hell = 1000000007;
static readonly int N = 100005;
static int c_0, c_1, c_2;

// Function to segregate numbers
// based on their remainder
// when divided by three
static void count_k(int []arr,
                    Stack<int> ones,
                    Stack<int> twos,
                    Stack<int> zeros)
{
  // Loop to iterate over
  // the elements of the
  // given array
  for (int i = 0; i < arr.Length; i++)
  {
    // Condition to check the
    // remainder of the number
    if (arr[i] % 3 == 0)
    {
      c_0++;
      zeros.Push(arr[i]);
    }
    else if (arr[i] % 3 == 1)
    {
      c_1++;
      ones.Push(arr[i]);
    }
    else
    {
      c_2++;
      twos.Push(arr[i]);
    }
  }
  return;
}

// Function to find the permutation
// of the array such that sum of
// adjacent elements is not divisible by 3
static void printArrangement(int []arr,
                             Stack<int> ones,
                             Stack<int> twos,
                             Stack<int> zeros)
{
  // Condition to check when
  // it's impossible to arrange
  if ((c_0 == 0 && c_1 != 0 && c_2 != 0) ||
       c_0 > c_1 + c_2 + 1)
  {
    Console.Write("-1");
    return;
  }

  // Condition to check when
  // there are no zeros, and
  // only ones or only twos
  int i;
  if (c_0 == 0)
  {
    for (i = 0; i < arr.Length; i++)
    {
      Console.Write(arr[i] + " ");
    }
    return;
  }

  // Array to store the permutation
  int j;
  int []ans = new int[N];
  for (i = 0; i < ans.Length; i++)
    ans[i] = -1;

  // Place the ones on alternate places
  // in the answer array,
  // leaving spaces for zeros remainder
  // elements in the array
  for (i = 1, j = 0; j < c_1; i += 2, j++)
  {
    ans[i] = ones.Peek();
    ones.Pop();
  }

  // Adding a zero to
  // connect it with a two
  ans[i - 1] = zeros.Peek();
  zeros.Pop();
  c_0--;

  // Place the twos on alternate places
  // in the answer array,
  // leaving spaces for zeros
  for (j = 0; j < c_2; j++, i += 2)
  {
    ans[i] = twos.Peek();
    twos.Pop();
  }

  // Fill the zeros finally,
  // between the ones and the twos
  for (int k = 0; c_0 > 0; k += 2)
  {
    if (ans[k] == -1)
    {
      ans[k] = zeros.Peek();
      c_0--;
    }
  }

  // Print the arrangement of the array
  for (int i1 = 0; i1 < N; i1++)
  {
    if (ans[i1] != -1)
      Console.Write(ans[i1] + " ");
  }
  return;
}

// Function to solve the problem
static void solve(int n, int []arr)
{
  // As there can be only 3 remainders
  Stack<int> ones = new Stack<int>();
  Stack<int> zeros = new Stack<int>();
  Stack<int> twos = new Stack<int>();

  c_0 = 0;
  c_1 = 0;
  c_2 = 0;
  count_k(arr, ones, twos, zeros);

  // Function Call
  printArrangement(arr, ones, twos, zeros);
}

// Driver Code
public static void Main(String[] args)
{
  int n = 5;
  int []arr = {1, 2, 3, 4, 5};
  solve(n, arr);
}
}

// This code is contributed by Princi Singh
```

**Output**

```
4 1 3 5 2
```