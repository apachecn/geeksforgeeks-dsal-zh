# 祖姆凯莱号

> 原文:[https://www.geeksforgeeks.org/zumkelle-number/](https://www.geeksforgeeks.org/zumkelle-number/)

给定一个整数 **N** ，任务是检查 **N** 是否为祖克勒数

> Zumkelle 数是一个数，它的除数可以被分成两个具有相同和的集合。
> 例如，12 是一个 Zumkeller 数，因为它的除数 1，2，3，4，6，12 可以在两个集合{12，2}中划分，并且{1，3，4，6}具有相同的和 14。

**例:**

> **输入:** N = 12
> **输出:**是
> **说明:**
> 12 的除数 1、2、3、4、6、12，可以在两个集合{12、2}中分割
> ，并且{1、3、4、6}具有相同的和 14。
> **输入:** N = 26
> **输出:**否

**方法:**思想是将数的所有因子存储在一个数组中，然后最后将数组划分为两个子集，使得两个子集的元素之和相同。
分区问题对于同样的在本文中有详细解释:
[分区问题| DP-18](https://www.geeksforgeeks.org/partition-problem-dp-18/)
下面是上述方法的实现:

## C++

```
// C++ Program to check if n
// is an Zumkelle number

#include <bits/stdc++.h>
using namespace std;

// Function to store divisors of N
// in a vector
void storeDivisors(int n, vector<int>& div)
{
    // Find all divisors which divides 'num'
    for (int i = 1; i <= sqrt(n); i++) {

        // if 'i' is divisor of 'n'
        if (n % i == 0) {

            // if both divisors are same
            // then store it once else store
            // both divisors
            if (i == (n / i))
                div.push_back(i);
            else {
                div.push_back(i);
                div.push_back(n / i);
            }
        }
    }
}

// Returns true if vector can be partitioned
// in two subsets of equal sum, otherwise false
bool isPartitionPossible(vector<int>& arr)
{
    int n = arr.size();
    int sum = 0;
    int i, j;

    // Calculate sum of all elements
    for (i = 0; i < n; i++)
        sum += arr[i];

    if (sum % 2 != 0)
        return false;

    bool part[sum / 2 + 1][n + 1];

    // initialize top row as true
    for (i = 0; i <= n; i++)
        part[0][i] = true;

    // initialize leftmost column,
    // except part[0][0], as 0
    for (i = 1; i <= sum / 2; i++)
        part[i][0] = false;

    // Fill the partition table
    // in bottom up manner
    for (i = 1; i <= sum / 2; i++) {
        for (j = 1; j <= n; j++) {
            part[i][j] = part[i][j - 1];
            if (i >= arr[j - 1])
                part[i][j] = part[i][j] || part[i - arr[j - 1]][j - 1];
        }
    }

    return part[sum / 2][n];
}

// Function to check if n
// is an Zumkelle number
bool isZumkelleNum(int N)
{
    // vector to store all
    // proper divisors of N
    vector<int> div;
    storeDivisors(N, div);
    return isPartitionPossible(div);
}

// Driver code
int main()
{
    int n = 12;
    if (isZumkelleNum(n))
        cout << "Yes";
    else
        cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to check if n
// is an Zumkelle number
import java.util.*;
class GFG{

// Function to store divisors of N
// in a vector
static void storeDivisors(int n,
                   Vector<Integer> div)
{
    // Find all divisors which divides 'num'
    for (int i = 1; i <= Math.sqrt(n); i++)
    {

        // if 'i' is divisor of 'n'
        if (n % i == 0)
        {

            // if both divisors are same
            // then store it once else store
            // both divisors
            if (i == (n / i))
                div.add(i);
            else
            {
                div.add(i);
                div.add(n / i);
            }
        }
    }
}

// Returns true if vector can be partitioned
// in two subsets of equal sum, otherwise false
static boolean isPartitionPossible
                (Vector<Integer> arr)
{
    int n = arr.size();
    int sum = 0;
    int i, j;

    // Calculate sum of all elements
    for (i = 0; i < n; i++)
        sum += arr.get(i);

    if (sum % 2 != 0)
        return false;

    boolean [][]part = new boolean[sum / 2 + 1][n + 1];

    // initialize top row as true
    for (i = 0; i <= n; i++)
        part[0][i] = true;

    // initialize leftmost column,
    // except part[0][0], as 0
    for (i = 1; i <= sum / 2; i++)
        part[i][0] = false;

    // Fill the partition table
    // in bottom up manner
    for (i = 1; i <= sum / 2; i++) {
        for (j = 1; j <= n; j++) {
            part[i][j] = part[i][j - 1];
            if (i >= arr.get(j - 1))
                part[i][j] = part[i][j] ||
                               part[i - arr.get(j - 1)][j - 1];
        }
    }

    return part[sum / 2][n];
}

// Function to check if n
// is an Zumkelle number
static boolean isZumkelleNum(int N)
{
    // vector to store all
    // proper divisors of N
    Vector<Integer> div = new Vector<Integer>();
    storeDivisors(N, div);
    return isPartitionPossible(div);
}

// Driver code
public static void main(String[] args)
{
    int n = 12;
    if (isZumkelleNum(n))
        System.out.print("Yes");
    else
        System.out.print("No");
}
}

// This code is contributed by Amit Katiyar
```

## C#

```
// C# Program to check if n
// is an Zumkelle number
using System;
using System.Collections.Generic;

class GFG{

// Function to store divisors of N
// in a vector
static void storeDivisors(int n,
                  List<int> div)
{
    // Find all divisors which divides 'num'
    for (int i = 1; i <= Math.Sqrt(n); i++)
    {

        // if 'i' is divisor of 'n'
        if (n % i == 0)
        {

            // if both divisors are same
            // then store it once else store
            // both divisors
            if (i == (n / i))
                div.Add(i);
            else
            {
                div.Add(i);
                div.Add(n / i);
            }
        }
    }
}

// Returns true if vector can be partitioned
// in two subsets of equal sum, otherwise false
static bool isPartitionPossible
                 (List<int> arr)
{
    int n = arr.Count;
    int sum = 0;
    int i, j;

    // Calculate sum of all elements
    for (i = 0; i < n; i++)
        sum += arr[i];

    if (sum % 2 != 0)
        return false;

    bool [,]part = new bool[sum / 2 + 1, n + 1];

    // initialize top row as true
    for (i = 0; i <= n; i++)
        part[0, i] = true;

    // initialize leftmost column,
    // except part[0,0], as 0
    for (i = 1; i <= sum / 2; i++)
        part[i, 0] = false;

    // Fill the partition table
    // in bottom up manner
    for (i = 1; i <= sum / 2; i++)
    {
        for (j = 1; j <= n; j++)
        {
            part[i, j] = part[i, j - 1];
            if (i >= arr[j - 1])
                part[i, j] = part[i, j] ||
                             part[i - arr[j - 1],
                                          j - 1];
        }
    }

    return part[sum / 2, n];
}

// Function to check if n
// is an Zumkelle number
static bool isZumkelleNum(int N)
{
    // vector to store all
    // proper divisors of N
    List<int> div = new List<int>();
    storeDivisors(N, div);
    return isPartitionPossible(div);
}

// Driver code
public static void Main(String[] args)
{
    int n = 12;
    if (isZumkelleNum(n))
        Console.Write("Yes");
    else
        Console.Write("No");
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>
// Javascript implementation

// Function to store divisors of N
// in a vector
function storeDivisors(n, div)
{
    // Find all divisors which divides 'num'
    for (var i = 1; i <= Math.sqrt(n); i++) {

        // if 'i' is divisor of 'n'
        if (n % i == 0) {

            // if both divisors are same
            // then store it once else store
            // both divisors
            if (i == Math.floor(n / i))
                div.push(i);
            else {
                div.push(i);
                div.push(Math.floor(n / i));
            }
        }
    }
}

// Returns true if vector can be partitioned
// in two subsets of equal sum, otherwise false
function isPartitionPossible( arr)
{
    var n = arr.length;
    var sum = 0;
    var i, j;

    // Calculate sum of all elements
    for (i = 0; i < n; i++)
        sum += arr[i];

    if (sum % 2 != 0)
        return false;

    var part = [];
    for (i = 0; i <= Math.floor(sum / 2); i++) {
        var ll = [];
        for (j = 0; j <= n; j++) {
            ll.push(false);
        }
        part.push(ll);
    } 
    // initialize top row as true
    for (i = 0; i <= n; i++)
        part[0][i] = true;

    // initialize leftmost column,
    // except part[0][0], as 0
    for (i = 1; i <= Math.floor(sum / 2); i++)
        part[i][0] = false;

    // Fill the partition table
    // in bottom up manner
    for (i = 1; i <= Math.floor(sum / 2); i++) {
        for (j = 1; j <= n; j++) {
            part[i][j] = part[i][j - 1];
            if (i >= arr[j - 1])
                part[i][j] = part[i][j] || part[i - arr[j - 1]][j - 1];
        }
    }

    return 1;//part[Math.floor(sum / 2)][n];
}

// Function to check if n
// is an Zumkelle number
function isZumkelleNum(N)
{
    // vector to store all
    // proper divisors of N
    var div = [];
    storeDivisors(N, div);
    return isPartitionPossible(div);
}

// Driver Code
// Given Number N
var N = 12;

// Function Call
if (isZumkelleNum(N))
    document.write("Yes");
else
    document.write("No");

// This code is contributed by shubhamsingh10
</script>
```

**Output:** Yes 

**时间复杂度:** O(N *和)

**参考:**T2】OEIST4】