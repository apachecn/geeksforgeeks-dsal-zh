# 一个数组的所有子集的子集之和| O(2^N)

> 原文:[https://www . geeksforgeeks . org/数组所有子集之和-o2n/](https://www.geeksforgeeks.org/sum-of-subsets-of-all-the-subsets-of-an-array-o2n/)

给定一个长度为 **N** 的数组 **arr[]** ，任务是找出该数组所有子集的子集的总和。
**例:**

> **输入:** arr[] = {1，1}
> **输出:** 6
> 所有可能的子集:
> **a) {} : 0**
> 该子集
> 的所有可能子集将为{}，Sum = 0
> **b){1}:1**
> 该子集
> 的所有可能子集将为{}和{ 1 }， Sum = 0+1 = 1
> **c){1}:1**
> 该子集
> 的所有可能子集将为{}和{1}，Sum = 0 + 1 = 1
> **d) {1，1} : 4**
> 该子集
> 的所有可能子集将为{}、{1}、{1}和{ 1，1 }，Sum = 0+1+2 = 4
> 因此，ans = 0 + 1

**方法:**在本文中，将讨论一种时间复杂度为 **O(N * 2 <sup>N</sup> )** 的方法来解决给定的问题。
首先，生成数组所有可能的子集。总共会有 **2 <sup>N</sup>** 个子集。然后对于每个子集，求其所有子集的和。
对于这一点，可以观察到，在长度为 **L** 的数组中，每个元素在子集的和中都恰好出现**2<sup>(L–1)</sup>**次。所以，每个元素的贡献将是**2<sup>(L–1)</sup>**乘以它的值。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to sum of all subsets of a
// given array
void subsetSum(vector<int>& c, int& ans)
{
    int L = c.size();
    int mul = (int)pow(2, L - 1);
    for (int i = 0; i < c.size(); i++)
        ans += c[i] * mul;
}

// Function to generate the subsets
void subsetGen(int* arr, int i, int n,
               int& ans, vector<int>& c)
{
    // Base-case
    if (i == n) {

        // Finding the sum of all the subsets
        // of the generated subset
        subsetSum(c, ans);
        return;
    }

    // Recursively accepting and rejecting
    // the current number
    subsetGen(arr, i + 1, n, ans, c);
    c.push_back(arr[i]);
    subsetGen(arr, i + 1, n, ans, c);
    c.pop_back();
}

// Driver code
int main()
{
    int arr[] = { 1, 1 };
    int n = sizeof(arr) / sizeof(int);

    // To store the final ans
    int ans = 0;
    vector<int> c;

    subsetGen(arr, 0, n, ans, c);
    cout << ans;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// To store the final ans
static int ans;

// Function to sum of all subsets of a
// given array
static void subsetSum(Vector<Integer> c)
{
    int L = c.size();
    int mul = (int)Math.pow(2, L - 1);
    for (int i = 0; i < c.size(); i++)
        ans += c.get(i) * mul;
}

// Function to generate the subsets
static void subsetGen(int []arr, int i,
                      int n, Vector<Integer> c)
{
    // Base-case
    if (i == n)
    {

        // Finding the sum of all the subsets
        // of the generated subset
        subsetSum(c);
        return;
    }

    // Recursively accepting and rejecting
    // the current number
    subsetGen(arr, i + 1, n, c);
    c.add(arr[i]);
    subsetGen(arr, i + 1, n, c);
    c.remove(0);
}

// Driver code
public static void main(String []args)
{
    int arr[] = { 1, 1 };
    int n = arr.length;

    Vector<Integer> c = new Vector<Integer>();

    subsetGen(arr, 0, n, c);
    System.out.println(ans);
}
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# store the answer
c = []
ans = 0

# Function to sum of all subsets of a
# given array
def subsetSum():
    global ans
    L = len(c)
    mul = pow(2, L - 1)
    i = 0
    while ( i < len(c)):
        ans += c[i] * mul
        i += 1

# Function to generate the subsets
def subsetGen(arr, i, n):

    # Base-case
    if (i == n) :

        # Finding the sum of all the subsets
        # of the generated subset
        subsetSum()
        return

    # Recursively accepting and rejecting
    # the current number
    subsetGen(arr, i + 1, n)
    c.append(arr[i])
    subsetGen(arr, i + 1, n)
    c.pop()

# Driver code
if __name__ == "__main__" :

    arr = [ 1, 1 ]
    n = len(arr)

    subsetGen(arr, 0, n)
    print (ans)

# This code is contributed by Arnab Kundu
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

// To store the final ans
static int ans;

// Function to sum of all subsets of a
// given array
static void subsetSum(List<int> c)
{
    int L = c.Count;
    int mul = (int)Math.Pow(2, L - 1);
    for (int i = 0; i < c.Count; i++)
        ans += c[i] * mul;
}

// Function to generate the subsets
static void subsetGen(int []arr, int i,
                      int n, List<int> c)
{
    // Base-case
    if (i == n)
    {

        // Finding the sum of all the subsets
        // of the generated subset
        subsetSum(c);
        return;
    }

    // Recursively accepting and rejecting
    // the current number
    subsetGen(arr, i + 1, n, c);
    c.Add(arr[i]);
    subsetGen(arr, i + 1, n, c);
    c.RemoveAt(0);
}

// Driver code
public static void Main(String []args)
{
    int []arr = { 1, 1 };
    int n = arr.Length;

    List<int> c = new List<int>();

    subsetGen(arr, 0, n, c);
    Console.WriteLine(ans);
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// javascript implementation of the approach

    // To store the final ans
    var ans = 0;

    // Function to sum of all subsets of a
    // given array
    function subsetSum( c) {
        var L = c.length;
        var mul = parseInt( Math.pow(2, L - 1));
        for (i = 0; i < c.length; i++)
            ans += c[i] * mul;
    }

    // Function to generate the subsets
    function subsetGen(arr , i , n, c) {
        // Base-case
        if (i == n) {

            // Finding the sum of all the subsets
            // of the generated subset
            subsetSum(c);
            return;
        }

        // Recursively accepting and rejecting
        // the current number
        subsetGen(arr, i + 1, n, c);
        c.push(arr[i]);
        subsetGen(arr, i + 1, n, c);
        c.pop(0);
    }

    // Driver code

        var arr = [ 1, 1 ];
        var n = arr.length;

        var c = [];

        subsetGen(arr, 0, n, c);
        document.write(ans);

// This code is contributed by todaysgaurav
</script>
```

**Output:** 

```
6
```