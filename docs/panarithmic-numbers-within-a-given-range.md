# 给定范围内的对数

> 原文:[https://www . geesforgeks . org/pana metrical-numbers-in-a-给定范围/](https://www.geeksforgeeks.org/panarithmic-numbers-within-a-given-range/)

给定两个正数 **A** 和 **B** 。任务是打印所有的

> [两个数字之间的对数](https://en.wikipedia.org/wiki/Practical_number)(含)。
> **对数**或**实数**是正整数 **N** ，这样所有小于 N 的正整数都可以表示为 **N** 的不同除数之和。
> **例如:**，12 是一个实际数字，因为从 1 到 11 的所有数字都可以表示为其除数 1，2，3，4 和 6 的和{ 5 = 3 + 2，7 = 6 + 1，8 = 6 + 2，9 = 6 + 3，10 = 6 + 3 + 1，11 = 6 + 3 + 2}

**示例:**

> **输入:** A = 1 B = 20
> **输出:** 1 2 4 6 8 12 16 18 20
> **说明:**
> 有 9 个实际数字，这些数字的因子可以代表所有比它小的数字。
> 例如用于 4。4 的因数是 1 和 2。
> 数字 3 可以表示为 1+2 = 3。
> 
> **输入:** A = 100 B = 150
> **输出:**100 104 108 112 120 126 128 132 140 144 150

**进场:**

1.  从 A 迭代到 B(包括 A 和 B)。
2.  检查每个数字是否是实际数字。
3.  逐一计算并存储**【A，B】**内每个数字的因子，并检查是否所有小于各自数字的数字都可以表示为因子之和。

下面是上述方法的实现:

## C++

```
// C++ program to print Practical
// Numbers in given range

#include <bits/stdc++.h>
using namespace std;

// function to compute divisors
// of a number
vector<int> get_divisors(int A)
{
    // vector to store divisors
    vector<int> ans;

    // 1 will always be a divisor
    ans.push_back(1);

    for (int i = 2; i <= sqrt(A); i++) {
        if (A % i == 0) {

            ans.push_back(i);

            // check if i is squareroot
            // of A then only one time
            // insert it in ans
            if ((i * i) != A)
                ans.push_back(A / i);
        }
    }
    return ans;
}

// function to check that a
// number can be represented as
// sum of distinct divisor or not
bool Sum_Possible(vector<int> set, int sum)
{
    int n = set.size();

    // The value of subset[i][j]
    // will be true if
    // there is a subset of
    // set[0..j-1] with sum
    // equal to i
    bool subset[n + 1][sum + 1];

    // If sum is 0, then answer is true
    for (int i = 0; i <= n; i++)
        subset[i][0] = true;

    // If sum is not 0 and set is empty,
    // then answer is false
    for (int i = 1; i <= sum; i++)
        subset[0][i] = false;

    // Fill the subset table
    // in bottom up manner
    for (int i = 1; i <= n; i++) {
        for (int j = 1; j <= sum; j++) {

            if (j < set[i - 1])
                subset[i][j] = subset[i - 1][j];

            if (j >= set[i - 1])
                subset[i][j]
                    = subset[i - 1][j]
                      || subset[i - 1]
                               [j - set[i - 1]];
        }
    }

    // return the possibility
    // of given sum
    return subset[n][sum];
}

// function to check a number is
// Practical or not
bool Is_Practical(int A)
{
    // vector to store divisors
    vector<int> divisors;

    divisors = get_divisors(A);
    for (int i = 2; i < A; i++) {

        if (Sum_Possible(divisors, i) == false)
            return false;
    }

    // if all numbers can be
    // represented as sum of
    // unique divisors
    return true;
}

// function to print Practical
// Numbers in a range
void print_practica_No(int A, int B)
{
    for (int i = A; i <= B; i++) {
        if (Is_Practical(i) == true) {
            cout << i << " ";
        }
    }
}

// Driver Function
int main()
{
    int A = 1, B = 100;
    print_practica_No(A, B);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print practical
// Numbers in given range
import java.util.*;
import java.math.*;

class GFG{

// Function to compute divisors
// of a number
static ArrayList<Integer> get_divisors(int A)
{

    // Vector to store divisors
    ArrayList<Integer> ans = new ArrayList<>();

    // 1 will always be a divisor
    ans.add(1);

    for(int i = 2; i <= Math.sqrt(A); i++)
    {
        if (A % i == 0)
        {
            ans.add(i);

            // Check if i is squareroot
            // of A then only one time
            // insert it in ans
            if ((i * i) != A)
                ans.add(A / i);
        }
    }
    return ans;
}

// Function to check that a
// number can be represented as
// sum of distinct divisor or not
static boolean Sum_Possible(ArrayList<Integer> set,
                            int sum)
{
    int n = set.size();

    // The value of subset[i][j]
    // will be true if there is
    // a subset of set[0..j-1]
    // with sum equal to i
    boolean subset[][] = new boolean[n + 1][sum + 1];

    // If sum is 0, then answer is true
    for(int i = 0; i <= n; i++)
        subset[i][0] = true;

    // If sum is not 0 and set is empty,
    // then answer is false
    for(int i = 1; i <= sum; i++)
        subset[0][i] = false;

    // Fill the subset table
    // in bottom up manner
    for(int i = 1; i <= n; i++)
    {
        for(int j = 1; j <= sum; j++)
        {
            if (j < set.get(i - 1))
                subset[i][j] = subset[i - 1][j];

            if (j >= set.get(i - 1))
                subset[i][j] = subset[i - 1][j] ||
                               subset[i - 1][j -
                               set.get(i - 1)];
        }
    }

    // Return the possibility
    // of given sum
    return subset[n][sum];
}

// Function to check a number is
// Practical or not
static boolean Is_Practical(int A)
{

    // Vector to store divisors
    ArrayList<Integer> divisors;

    divisors = get_divisors(A);
    for(int i = 2; i < A; i++)
    {
        if (Sum_Possible(divisors, i) == false)
            return false;
    }

    // If all numbers can be
    // represented as sum of
    // unique divisors
    return true;
}

// Function to print Practical
// Numbers in a range
static void print_practica_No(int A, int B)
{
    for(int i = A; i <= B; i++)
    {
        if (Is_Practical(i) == true)
        {
            System.out.print(i + " ");
        }
    }
}

// Driver Code
public static void main(String args[])
{
    int A = 1, B = 100;

    print_practica_No(A, B);
}
}

// This code is contributed by jyoti369
```

## 蟒蛇 3

```
# Python3 program to print Practical
# Numbers in given range
import math

# Function to compute divisors
# of a number
def get_divisors(A):

    # Vector to store divisors
    ans = []

    # 1 will always be a divisor
    ans.append(1)
    for i in range(2, math.floor(math.sqrt(A)) + 1):
        if (A % i == 0):
            ans.append(i)

            # Check if i is squareroot
            # of A then only one time
            # insert it in ans
            if ((i * i) != A):
                ans.append(A // i)
    return ans

# Function to check that a
# number can be represented as
# summ of distinct divisor or not
def summ_Possible(sett, summ):

    n = len(sett)

    # The value of subsett[i][j] will
    # be True if there is a subsett of
    # sett[0..j-1] with summ equal to i
    subsett = [[0 for i in range(summ + 1)]
                  for j in range(n + 1)]

    # If summ is 0, then answer is True
    for i in range(n + 1):
        subsett[i][0] = True

    # If summ is not 0 and sett is empty,
    # then answer is False
    for i in range(1, summ + 1):
        subsett[0][i] = False

    # Fill the subsett table
    # in bottom up manner
    for i in range(n + 1):
        for j in range(summ + 1):
            if (j < sett[i - 1]):
                subsett[i][j] = subsett[i - 1][j]

            if (j >= sett[i - 1]):
                subsett[i][j] = (subsett[i - 1][j] or
                                 subsett[i - 1]
                                        [j - sett[i - 1]])

    # Return the possibility
    # of given summ
    return subsett[n][summ]

# Function to check a number
#  is Practical or not
def Is_Practical(A):

    # Vector to store divisors
    divisors = []

    divisors = get_divisors(A)
    for i in range(2, A):
        if (summ_Possible(divisors, i) == False):
            return False

    # If all numbers can be
    # represented as summ of
    # unique divisors
    return True

# Function to prPractical
# Numbers in a range
def print_practica_No(A, B):

    for i in range(A, B + 1):
        if (Is_Practical(i) == True):
            print(i, end = " ")

# Driver code
A = 1
B = 100

print_practica_No(A, B)

# This code is contributed by shubhamsingh10
```

## C#

```
// C# program to print practical
// Numbers in given range
using System;
using System.Collections;

class GFG{

// Function to compute divisors
// of a number
static ArrayList get_divisors(int A)
{

    // To store divisors
    ArrayList ans = new ArrayList();

    // 1 will always be a divisor
    ans.Add(1);

    for(int i = 2;
            i <= (int)Math.Sqrt(A);
            i++)
    {
        if (A % i == 0)
        {
            ans.Add(i);

            // Check if i is squareroot
            // of A then only one time
            // insert it in ans
            if ((i * i) != A)
                ans.Add(A / i);
        }
    }
    return ans;
}

// Function to check that a
// number can be represented as
// sum of distinct divisor or not
static bool Sum_Possible(ArrayList set,
                         int sum)
{
    int n = set.Count;

    // The value of subset[i][j]
    // will be true if
    // there is a subset of
    // set[0..j-1] with sum
    // equal to i
    bool [,]subset = new bool[n + 1, sum + 1];

    // If sum is 0, then answer is true
    for(int i = 0; i <= n; i++)
        subset[i, 0] = true;

    // If sum is not 0 and set is empty,
    // then answer is false
    for(int i = 1; i <= sum; i++)
        subset[0, i] = false;

    // Fill the subset table
    // in bottom up manner
    for(int i = 1; i <= n; i++)
    {
        for(int j = 1; j <= sum; j++)
        {
            if (j < (int)set[i - 1])
                subset[i, j] = subset[i - 1, j];

            if (j >= (int)set[i - 1])
                subset[i, j] = subset[i - 1, j] ||
                               subset[i - 1, j -
                             (int)set[i - 1]];
        }
    }

    // Return the possibility
    // of given sum
    return subset[n, sum];
}

// Function to check a number is
// Practical or not
static bool Is_Practical(int A)
{

    // To store divisors
    ArrayList divisors = new ArrayList();

    divisors = get_divisors(A);
    for(int i = 2; i < A; i++)
    {
        if (Sum_Possible(divisors, i) == false)
            return false;
    }

    // If all numbers can be
    // represented as sum of
    // unique divisors
    return true;
}

// Function to print Practical
// Numbers in a range
static void print_practica_No(int A, int B)
{
    for(int i = A; i <= B; i++)
    {
        if (Is_Practical(i) == true)
        {
            Console.Write(i + " ");
        }
    }
}

// Driver code
public static void Main(string []args)
{
    int A = 1, B = 100;

    print_practica_No(A, B);
}
}

// This code is contributed by rutvik_56
```

## java 描述语言

```
<script>

// Javascript program to print Practical
// Numbers in given range

// function to compute divisors
// of a number
function get_divisors(A)
{
    // vector to store divisors
    var ans = [];

    // 1 will always be a divisor
    ans.push(1);

    for (var i = 2; i <= Math.sqrt(A); i++) {
        if (A % i == 0) {

            ans.push(i);

            // check if i is squareroot
            // of A then only one time
            // insert it in ans
            if ((i * i) != A)
                ans.push(parseInt(A / i));
        }
    }
    return ans;
}

// function to check that a
// number can be represented as
// sum of distinct divisor or not
function Sum_Possible(set, sum)
{
    var n = set.length;

    // The value of subset[i][j]
    // will be true if
    // there is a subset of
    // set[0..j-1] with sum
    // equal to i
    var subset = Array.from(Array(n+1), ()=>Array(sum+1));

    // If sum is 0, then answer is true
    for (var i = 0; i <= n; i++)
        subset[i][0] = true;

    // If sum is not 0 and set is empty,
    // then answer is false
    for (var i = 1; i <= sum; i++)
        subset[0][i] = false;

    // Fill the subset table
    // in bottom up manner
    for (var i = 1; i <= n; i++) {
        for (var j = 1; j <= sum; j++) {

            if (j < set[i - 1])
                subset[i][j] = subset[i - 1][j];

            if (j >= set[i - 1])
                subset[i][j]
                    = subset[i - 1][j]
                      || subset[i - 1]
                               [j - set[i - 1]];
        }
    }

    // return the possibility
    // of given sum
    return subset[n][sum];
}

// function to check a number is
// Practical or not
function Is_Practical(A)
{
    // vector to store divisors
    var divisors = [];

    divisors = get_divisors(A);
    for (var i = 2; i < A; i++) {

        if (Sum_Possible(divisors, i) == false)
            return false;
    }

    // if all numbers can be
    // represented as sum of
    // unique divisors
    return true;
}

// function to print Practical
// Numbers in a range
function print_practica_No(A, B)
{
    for (var i = A; i <= B; i++) {
        if (Is_Practical(i) == true) {
            document.write( i + " ");
        }
    }
}

// Driver Function
var A = 1, B = 100;
print_practica_No(A, B);

// This code is contributed by noob2000.

</script>
```

**输出:**

```
1 2 4 6 8 12 16 18 20 24 28 30 32 36 40 42 48 54 56 60 64 66 72 78 80 84 88 90 96 100 
```

**时间复杂度:***O((B–A)* B<sup>5/2</sup>)*
**辅助空间:** *O( B <sup>3/2</sup> )*