# 最接近 X 的 N 的最小除数

> 原文:[https://www . geesforgeks . org/n 的最小除数-最接近-x/](https://www.geeksforgeeks.org/smallest-divisor-of-n-closest-to-x/)

给定两个正整数 **N** 和 **X** ，任务是求 **N** 中最接近 **X** 的最小除数。

**示例:**

> **输入:** N = 16，X = 5
> **输出:** 4
> **说明:**
> 4 是最接近 5 的 16 的除数。
> 
> **输入:** N = 27，X = 15
> **输出:** 9
> **说明:**
> 9 是最接近 15 的 27 的除数。

**天真的方法:**解决问题最简单的方法是迭代所有的值直到 **N** ，找到最接近于 **X** 的一个值，这个值划分 **N** 。

***时间复杂度:**O(N)*
T5**辅助空间:** O(1)

**更好的方法:**更好的方法是遍历 **N** 的所有除数，检查最接近 **X** 的除数。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Function to find the divisor of N
// closest to the target
int findClosest(int N, int target)
{
    int closest = -1;
    int diff = INT_MAX;

    // Iterate till square root of N
    for (int i = 1; i <= sqrt(N); i++) {
        if (N % i == 0) {

            // Check if divisors are equal
            if (N / i == i) {

                // Check if i is the closest
                if (abs(target - i) < diff) {
                    diff = abs(target - i);
                    closest = i;
                }
            }
            else {

                // Check if i is the closest
                if (abs(target - i) < diff) {
                    diff = abs(target - i);
                    closest = i;
                }

                // Check if n / i is the closest
                if (abs(target - N / i) < diff) {
                    diff = abs(target - N / i);
                    closest = N / i;
                }
            }
        }
    }

    // Print the closest value
    cout << closest;
}

// Driver Code
int main()
{
    // Given N & X
    int N = 16, X = 5;

    // Function Call
    findClosest(N, X);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG {

  // Function to find the divisor of N
  // closest to the target
  static void findClosest(int N, int target)
  {
    int closest = -1;
    int diff = Integer.MAX_VALUE;

    // Iterate till square root of N
    for (int i = 1; i <= (int)Math.sqrt(N); i++) {
      if (N % i == 0) {

        // Check if divisors are equal
        if (N / i == i) {

          // Check if i is the closest
          if (Math.abs(target - i) < diff)
          {
            diff = Math.abs(target - i);
            closest = i;
          }
        }
        else {

          // Check if i is the closest
          if (Math.abs(target - i) < diff)
          {
            diff = Math.abs(target - i);
            closest = i;
          }

          // Check if n / i is the closest
          if (Math.abs(target - N / i) < diff)
          {
            diff = Math.abs(target - N / i);
            closest = N / i;
          }
        }
      }
    }

    // Print the closest value
    System.out.println(closest);
  }

  // Driver code
  public static void main(String[] args)
  {

    // Given N & X
    int N = 16, X = 5;

    // Function Call
    findClosest(N, X);
  }
}

// This code is contributed by code_hunt.
```

## 蟒蛇 3

```
# Python3 program for the above approach
from math import sqrt, floor, ceil

# Function to find the divisor of N
# closest to the target
def findClosest(N, target):
    closest = -1
    diff = 10**18

    # Iterate till square root of N
    for i in range(1, ceil(sqrt(N)) + 1):
        if (N % i == 0):

            # Check if divisors are equal
            if (N // i == i):

                # Check if i is the closest
                if (abs(target - i) < diff):
                    diff = abs(target - i)
                    closest = i

            else:

                # Check if i is the closest
                if (abs(target - i) < diff):
                    diff = abs(target - i)
                    closest = i

                # Check if n / i is the closest
                if (abs(target - N // i) < diff):
                    diff = abs(target - N // i)
                    closest = N // i

    # Print the closest value
    print(closest)

# Driver Code
if __name__ == '__main__':

    # Given N & X
    N, X = 16, 5

    # Function Call
    findClosest(N, X)

    # This code is contributed by mohit kumar 29
```

## C#

```
// C# program for the above approach
using System;
class GFG {

  // Function to find the divisor of N
  // closest to the target
  static void findClosest(int N, int target)
  {
    int closest = -1;
    int diff = Int32.MaxValue;

    // Iterate till square root of N
    for (int i = 1; i <= Math.Sqrt(N); i++) {
      if (N % i == 0) {

        // Check if divisors are equal
        if (N / i == i) {

          // Check if i is the closest
          if (Math.Abs(target - i) < diff)
          {
            diff = Math.Abs(target - i);
            closest = i;
          }
        }
        else {

          // Check if i is the closest
          if (Math.Abs(target - i) < diff)
          {
            diff = Math.Abs(target - i);
            closest = i;
          }

          // Check if n / i is the closest
          if (Math.Abs(target - N / i) < diff)
          {
            diff = Math.Abs(target - N / i);
            closest = N / i;
          }
        }
      }
    }

    // Print the closest value
    Console.Write(closest);
  }

  // Driver code
  static void Main()
  {

    // Given N & X
    int N = 16, X = 5;

    // Function Call
    findClosest(N, X);
  }
}

// This code is contributed by divyeshrabadiya07
```

## java 描述语言

```
<script>
// Javascript program for the above approach

// Function to find the divisor of N
// closest to the target
function findClosest(N, target)
{
    let closest = -1;
    let diff = Number.MAX_VALUE;

    // Iterate till square root of N
    for (let i = 1; i <= Math.sqrt(N); i++) {
    if (N % i == 0) {

        // Check if divisors are equal
        if (N / i == i) {

        // Check if i is the closest
        if (Math.abs(target - i) < diff)
        {
            diff = Math.abs(target - i);
            closest = i;
        }
        }
        else {

        // Check if i is the closest
        if (Math.abs(target - i) < diff)
        {
            diff = Math.abs(target - i);
            closest = i;
        }

        // Check if n / i is the closest
        if (Math.abs(target - N / i) < diff)
        {
            diff = Math.abs(target - N / i);
            closest = N / i;
        }
        }
    }
    }

    // Print the closest value
    document.write(closest);
}

// driver function

    // Given N & X
    let N = 16, X = 5;

    // Function Call
    findClosest(N, X);

    // This code is contributed by souravghosh0416.
</script>
```

**Output:** 

```
4
```

***时间复杂度:** O(sqrt(N))*
***辅助空间:** O(1)*

**高效方法:**最佳思路是使用厄拉多塞的[筛的修改形式，预先计算从 **1** 到 **N** 的所有数字的除数，然后使用](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)[二分搜索法](https://www.geeksforgeeks.org/binary-search/)到[找到与给定目标](https://www.geeksforgeeks.org/find-closest-number-array/)最接近的值。

下面是上述方法的实现:

## C++

```
// C++ program for the above approach

#include <bits/stdc++.h>
using namespace std;

// Define macros
#define MAX 10000

vector<vector<int> > divisors(MAX + 1);

// Stores divisors for all numbers
// in the vector divisors
void computeDivisors()
{
    for (int i = 1; i <= MAX; i++) {
        for (int j = i; j <= MAX; j += i) {

            // i is the divisor and
            // j is the multiple
            divisors[j].push_back(i);
        }
    }
}

// Function to compare the closeness of the given
// target
int getClosest(int val1, int val2, int target)
{
    if (target - val1 >= val2 - target)
        return val2;
    else
        return val1;
}

// Function to find the element closest to
// target in divisors vector
int findClosest(vector<int>& arr, int n, int target)
{
    // Corner cases
    if (target <= arr[0])
        return arr[0];
    if (target >= arr[n - 1])
        return arr[n - 1];

    // Perform binary search
    int i = 0, j = n, mid = 0;
    while (i < j) {
        mid = (i + j) / 2;

        if (arr[mid] == target)
            return arr[mid];

        // Check if target is less than the array
        // element then search in left half
        if (target < arr[mid]) {

            // Check if target is greater
            // than previous
            // to mid, return closest of two
            if (mid > 0 && target > arr[mid - 1])
                return getClosest(arr[mid - 1], arr[mid],
                                  target);

            // Repeat for left half
            j = mid;
        }

        // Check if target is greater than mid
        else {
            if (mid < n - 1 && target < arr[mid + 1])
                return getClosest(arr[mid], arr[mid + 1],
                                  target);
            // Update i
            i = mid + 1;
        }
    }

    // Only single element left after search
    return arr[mid];
}

// Function to print the divisor of N closest to X
void printClosest(int N, int X)
{
    // Function call to calculate and stores
    // divisors of all numbers in a vector
    computeDivisors();

    // Stores the closest value to target
    int ans
        = findClosest(divisors[N], divisors[N].size(), X);

    // Print the answer
    cout << ans;
}

// Driver Code
int main()
{
    // Given N & X
    int N = 16, X = 5;

    // Function Call
    printClosest(N, X);
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program for the above approach
import java.util.*;
class GFG
{

// Define macros
static final int MAX = 10000;
static Vector<Integer>[] divisors = new Vector[MAX + 1];

// Stores divisors for all numbers
// in the vector divisors
static void computeDivisors()
{
    for (int i = 1; i <= MAX; i++)
    {
        for (int j = i; j <= MAX; j += i)
        {

            // i is the divisor and
            // j is the multiple
            divisors[j].add(i);
        }
    }
}

// Function to compare the closeness of the given
// target
static int getClosest(int val1, int val2, int target)
{
    if (target - val1 >= val2 - target)
        return val2;
    else
        return val1;
}

// Function to find the element closest to
// target in divisors vector
static int findClosest(Vector<Integer> array,
                       int n, int target)
{
    Integer []arr = array.toArray(new Integer[array.size()]);

  // Corner cases
    if (target <= arr[0])
        return arr[0];
    if (target >= arr[n - 1])
        return arr[n - 1];

    // Perform binary search
    int i = 0, j = n, mid = 0;
    while (i < j)
    {
        mid = (i + j) / 2;
        if (arr[mid] == target)
            return arr[mid];

        // Check if target is less than the array
        // element then search in left half
        if (target < arr[mid])
        {

            // Check if target is greater
            // than previous
            // to mid, return closest of two
            if (mid > 0 && target > arr[mid - 1])
                return getClosest(arr[mid - 1], arr[mid],
                                  target);

            // Repeat for left half
            j = mid;
        }

        // Check if target is greater than mid
        else
        {
            if (mid < n - 1 && target < arr[mid + 1])
                return getClosest(arr[mid], arr[mid + 1],
                                  target);
            // Update i
            i = mid + 1;
        }
    }

    // Only single element left after search
    return arr[mid];
}

// Function to print the divisor of N closest to X
static void printClosest(int N, int X)
{

    // Function call to calculate and stores
    // divisors of all numbers in a vector
    computeDivisors();

    // Stores the closest value to target
    int ans
        = findClosest(divisors[N], divisors[N].size(), X);

    // Print the answer
    System.out.print(ans);
}

// Driver Code
public static void main(String[] args)
{

    // Given N & X
    int N = 16, X = 5;
    for(int i = 0; i < divisors.length; i++)
        divisors[i] = new Vector<Integer>();

    // Function Call
    printClosest(N, X);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program for the above approach
MAX = 10000

divisors = [[] for i in range(MAX + 1)]

# Stores divisors for all numbers
# in the vector divisors
def computeDivisors():

    global divisors
    global MAX

    for i in range(1, MAX + 1, 1):
        for j in range(i, MAX + 1, i):

            # i is the divisor and
            # j is the multiple
            divisors[j].append(i)

# Function to compare the closeness of the given
# target
def getClosest(val1, val2, target):

    if (target - val1 >= val2 - target):
        return val2
    else:
        return val1

# Function to find the element closest to
# target in divisors vector
def findClosest(arr, n, target):

    # Corner cases
    if (target <= arr[0]):
        return arr[0]
    if (target >= arr[n - 1]):
        return arr[n - 1]

    # Perform binary search
    i = 0
    j = n
    mid = 0

    while (i < j):
        mid = (i + j) // 2

        if (arr[mid] == target):
            return arr[mid]

        # Check if target is less than the array
        # element then search in left half
        if (target < arr[mid]):

            # Check if target is greater
            # than previous
            # to mid, return closest of two
            if (mid > 0 and target > arr[mid - 1]):
                return getClosest(arr[mid - 1],
                                  arr[mid],target)

            # Repeat for left half
            j = mid

        # Check if target is greater than mid
        else:
            if (mid < n - 1 and target < arr[mid + 1]):
                return getClosest(arr[mid],
                                  arr[mid + 1], target)

            # Update i
            i = mid + 1

    # Only single element left after search
    return arr[mid]

# Function to print the divisor of N closest to X
def printClosest(N, X):

    global divisors

    # Function call to calculate and stores
    # divisors of all numbers in a vector
    computeDivisors()

    # Stores the closest value to target
    ans = findClosest(divisors[N],
                  len(divisors[N]), X)

    # Print the answer
    print(ans)

# Driver Code
if __name__ == '__main__':

    # Given N & X
    N = 16
    X = 5

    # Function Call
    printClosest(N, X)

# This code is contributed by SURENDRA_GANGWAR
```

## C#

```
// C# program for the above approach
using System;
using System.Collections.Generic;
class GFG
{

// Define macros
static readonly int MAX = 10000;
static List<int>[] divisors = new List<int>[MAX + 1];

// Stores divisors for all numbers
// in the vector divisors
static void computeDivisors()
{
    for (int i = 1; i <= MAX; i++)
    {
        for (int j = i; j <= MAX; j += i)
        {

            // i is the divisor and
            // j is the multiple
            divisors[j].Add(i);
        }
    }
}

// Function to compare the closeness of the given
// target
static int getClosest(int val1, int val2, int target)
{
    if (target - val1 >= val2 - target)
        return val2;
    else
        return val1;
}

// Function to find the element closest to
// target in divisors vector
static int findClosest(List<int> array,
                       int n, int target)
{
    int []arr = array.ToArray();

  // Corner cases
    if (target <= arr[0])
        return arr[0];
    if (target >= arr[n - 1])
        return arr[n - 1];

    // Perform binary search
    int i = 0, j = n, mid = 0;
    while (i < j)
    {
        mid = (i + j) / 2;
        if (arr[mid] == target)
            return arr[mid];

        // Check if target is less than the array
        // element then search in left half
        if (target < arr[mid])
        {

            // Check if target is greater
            // than previous
            // to mid, return closest of two
            if (mid > 0 && target > arr[mid - 1])
                return getClosest(arr[mid - 1], arr[mid],
                                  target);

            // Repeat for left half
            j = mid;
        }

        // Check if target is greater than mid
        else
        {
            if (mid < n - 1 && target < arr[mid + 1])
                return getClosest(arr[mid], arr[mid + 1],
                                  target);
            // Update i
            i = mid + 1;
        }
    }

    // Only single element left after search
    return arr[mid];
}

// Function to print the divisor of N closest to X
static void printClosest(int N, int X)
{

    // Function call to calculate and stores
    // divisors of all numbers in a vector
    computeDivisors();

    // Stores the closest value to target
    int ans
        = findClosest(divisors[N], divisors[N].Count, X);

    // Print the answer
    Console.Write(ans);
}

// Driver Code
public static void Main(String[] args)
{

    // Given N & X
    int N = 16, X = 5;
    for(int i = 0; i < divisors.Length; i++)
        divisors[i] = new List<int>();

    // Function Call
    printClosest(N, X);
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript program for the above approach

// Define macros
let  MAX = 10000;

let divisors = new Array(MAX + 1);

// Stores divisors for all numbers
// in the vector divisors
function computeDivisors()
{
    for(let i = 1; i <= MAX; i++)
    {
        for(let j = i; j <= MAX; j += i)
        {

            // i is the divisor and
            // j is the multiple
            divisors[j].push(i);
        }
    }
}

// Function to compare the closeness of the given
// target
function getClosest(val1, val2, target)
{
    if (target - val1 >= val2 - target)
        return val2;
    else
        return val1;
}

// Function to find the element closest to
// target in divisors vector
function findClosest(arr, n, target)
{

    // Corner cases
    if (target <= arr[0])
        return arr[0];
    if (target >= arr[n - 1])
        return arr[n - 1];

    // Perform binary search
    let i = 0, j = n, mid = 0;

    while (i < j)
    {
        mid = Math.floor((i + j) / 2);
        if (arr[mid] == target)
            return arr[mid];

        // Check if target is less than the array
        // element then search in left half
        if (target < arr[mid])
        {

            // Check if target is greater
            // than previous
            // to mid, return closest of two
            if (mid > 0 && target > arr[mid - 1])
                return getClosest(arr[mid - 1], arr[mid],
                                  target);

            // Repeat for left half
            j = mid;
        }

        // Check if target is greater than mid
        else
        {
            if (mid < n - 1 && target < arr[mid + 1])
                return getClosest(arr[mid], arr[mid + 1],
                                  target);

            // Update i
            i = mid + 1;
        }
    }

    // Only single element left after search
    return arr[mid];
}

// Function to print the divisor of N closest to X
function printClosest(N, X)
{

    // Function call to calculate and stores
    // divisors of all numbers in a vector
    computeDivisors();

    // Stores the closest value to target
    let ans = findClosest(divisors[N],
                          divisors[N].length, X);

    // Print the answer
    document.write(ans);
}

// Driver Code

// Given N & X
let N = 16, X = 5;
for(let i = 0; i < divisors.length; i++)
    divisors[i] = [];

// Function Call
printClosest(N, X);

// This code is contributed by unknown2108

</script>
```

**Output:** 

```
4
```

***时间复杂度:**O(N * log(log(N))* *****辅助空间:** O(MAX)***