# 诡异数字

> 原文:[https://www.geeksforgeeks.org/weird-number/](https://www.geeksforgeeks.org/weird-number/)

在数论中，一个奇异数是一个丰富的自然数，但不是半完美的 T2 数。换句话说，该数的适当约数(包括 1 但不包括其本身的约数)之和大于该数，但这些约数的子集不与该数本身相加。
给定一个数字 N，任务是检查这个数字是否怪异。

**示例:**

> **输入:** 40
> **输出:**数字不诡异
> 1+4+5+10+20=40，因此不诡异。
> 
> **输入:** 70
> **输出:**数字为诡异
> 最小的诡异数字为 70。它的适当约数是 1、2、5、7、10、14 和 35；这些和为 74，但这些和没有子集为 70。
> 比如 12 这个数字，丰富但不怪异，因为 12 的适当除数是 1、2、3、4、6，加起来就是 16；但是 2+4+6 = 12。前几个诡异的数字是 70，836，4030，5830，7192，7912，9272，10430，10570，10792，10990，11410，11690，12110，12530，12670，13370，13510，…

**进场:**检查数量是否充足。这个方法已经在[这里](https://www.geeksforgeeks.org/abundant-number/)讨论过了。检查完成后，检查号码是否不完整。检查半完美数字的方法已经讨论过了[这里](https://www.geeksforgeeks.org/semiperfect-number/)。
以下是上述方法的实现:

## C++

```
// C++ program to check if the
// number is weird or not
#include <bits/stdc++.h>
using namespace std;

// code to find all the factors of
// the number excluding the number itself
vector<int> factors(int n)
{
    // vector to store the factors
    vector<int> v;
    v.push_back(1);

    // note that this loop runs till sqrt(n)
    for (int i = 2; i <= sqrt(n); i++) {

        // if the value of i is a factor
        if (n % i == 0) {
            v.push_back(i);

            // condition to check the
            // divisor is not the number itself
            if (n / i != i) {
                v.push_back(n / i);
            }
        }
    }
    // return the vector
    return v;
}

// Function to check if the number
// is abundant or not
bool checkAbundant(int n)
{
    vector<int> v;

    int sum = 0;

    // find the divisors using function
    v = factors(n);

    // sum all the factors
    for (int i = 0; i < v.size(); i++) {
        sum += v[i];
    }

    // check for abundant or not
    if (sum > n)
        return true;
    else
        return false;
}

// Function to check if the
// number is semi-perfect or not
bool checkSemiPerfect(int n)
{
    vector<int> v;

    // find the divisors
    v = factors(n);

    // sorting the vector
    sort(v.begin(), v.end());

    int r = v.size();

    // subset to check if no is semiperfect
    bool subset[r + 1][n + 1];

    // initialising 1st column to true
    for (int i = 0; i <= r; i++)
        subset[i][0] = true;

    // initialing 1st row except zero position to 0
    for (int i = 1; i <= n; i++)
        subset[0][i] = false;

    // loop to find whether the number is semiperfect
    for (int i = 1; i <= r; i++) {
        for (int j = 1; j <= n; j++) {

            // calculation to check if the
            // number can be made by summation of divisors
            if (j < v[i - 1])
                subset[i][j] = subset[i - 1][j];
            else {
                subset[i][j] = subset[i - 1][j] ||
                               subset[i - 1][j - v[i - 1]];
            }
        }
    }

    // if not possible to make the
    // number by any combination of divisors
    if ((subset[r][n]) == 0)
        return false;
    else
        return true;
}

// Function to check for
// weird or not
bool checkweird(int n)
{
    if (checkAbundant(n) == true &&
        checkSemiPerfect(n) == false)
        return true;
    else
        return false;
}

// Driver Code
int main()
{
    int n = 70;

    if (checkweird(n))
        cout << "Weird Number";
    else
        cout << "Not Weird Number";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check if 
// the number is weird or not
import java.util.*;
class GFG
{
// code to find all the
// factors of the number
// excluding the number itself
static ArrayList<Integer> factors(int n)
{
    // ArrayList to store
    // the factors
    ArrayList<Integer> v = new ArrayList<Integer>();
    v.add(1);

    // note that this loop
    // runs till sqrt(n)
    for (int i = 2;
             i <= Math.sqrt(n); i++)
    {

        // if the value of
        // i is a factor
        if (n % i == 0)
        {
            v.add(i);

            // condition to check
            // the divisor is not
            // the number itself
            if (n / i != i)
            {
                v.add(n / i);
            }
        }
    }

    // return the ArrayList
    return v;
}

// Function to check if the
// number is abundant or not
static boolean checkAbundant(int n)
{
    ArrayList<Integer> v;

    int sum = 0;

    // find the divisors
    // using function
    v = factors(n);

    // sum all the factors
    for (int i = 0; i < v.size(); i++)
    {
        sum += v.get(i);
    }

    // check for abundant
    // or not
    if (sum > n)
        return true;
    else
        return false;
}

// Function to check if the
// number is semi-perfect or not
static boolean checkSemiPerfect(int n)
{
    ArrayList<Integer> v;

    // find the divisors
    v = factors(n);

    // sorting the ArrayList
    Collections.sort(v);

    int r = v.size();

    // subset to check if
    // no is semiperfect
    boolean subset[][] = new boolean[r + 1][n + 1];

    // initialising 1st
    // column to true
    for (int i = 0; i <= r; i++)
        subset[i][0] = true;

    // initialing 1st row except
    // zero position to 0
    for (int i = 1; i <= n; i++)
        subset[0][i] = false;

    // loop to find whether
    // the number is semiperfect
    for (int i = 1; i <= r; i++)
    {
        for (int j = 1; j <= n; j++)
        {

            // calculation to check
            // if the number can be
            // made by summation of
            // divisors
            if (j < v.get(i - 1))
                subset[i][j] = subset[i - 1][j];
            else {
                subset[i][j] = subset[i - 1][j] ||
                               subset[i - 1][j -
                                v.get(i - 1)];
            }
        }
    }

    // if not possible to make
    // the number by any
    // combination of divisors
    if ((subset[r][n]) == false)
        return false;
    else
        return true;
}

// Function to check
// for weird or not
static boolean checkweird(int n)
{
    if (checkAbundant(n) == true &&
        checkSemiPerfect(n) == false)
        return true;
    else
        return false;
}

// Driver Code
public static void main(String args[])
{
    int n = 70;

    if (checkweird(n))
        System.out.println("Weird Number");
    else
        System.out.println("Not Weird Number");
}
}

// This code is contributed
// by Arnab Kundu
```

## 蟒蛇 3

```
# Python 3 program to check if the
# number is weird or not
from math import sqrt

# code to find all the factors of
# the number excluding the number itself
def factors(n):

    # vector to store the factors
    v = []
    v.append(1)

    # note that this loop runs till sqrt(n)
    for i in range(2, int(sqrt(n)) + 1, 1):

        # if the value of i is a factor
        if (n % i == 0):
            v.append(i);

            # condition to check the
            # divisor is not the number itself
            if (int(n / i) != i):
                v.append(int(n / i))

    # return the vector
    return v

# Function to check if the number
# is abundant or not
def checkAbundant(n):
    sum = 0

    # find the divisors using function
    v = factors(n)

    # sum all the factors
    for i in range(len(v)):
        sum += v[i]

    # check for abundant or not
    if (sum > n):
        return True
    else:
        return False

# Function to check if the
# number is semi-perfect or not
def checkSemiPerfect(n):

    # find the divisors
    v = factors(n)

    # sorting the vector
    v.sort(reverse = False)
    r = len(v)

    # subset to check if no is semiperfect
    subset = [[0 for i in range(n + 1)]
                 for j in range(r + 1)]

    # initialising 1st column to true
    for i in range(r + 1):
        subset[i][0] = True

    # initialing 1st row except zero position to 0
    for i in range(1, n + 1):
        subset[0][i] = False

    # loop to find whether the number is semiperfect
    for i in range(1, r + 1):
        for j in range(1, n + 1):

            # calculation to check if the
            # number can be made by summation of divisors
            if (j < v[i - 1]):
                subset[i][j] = subset[i - 1][j]
            else:
                subset[i][j] = (subset[i - 1][j] or
                                subset[i - 1][j - v[i - 1]])

    # if not possible to make the
    # number by any combination of divisors
    if ((subset[r][n]) == 0):
        return False
    else:
        return True

# Function to check for
# weird or not
def checkweird(n):
    if (checkAbundant(n) == True and
        checkSemiPerfect(n) == False):
        return True
    else:
        return False

# Driver Code
if __name__ == '__main__':
    n = 70

    if (checkweird(n)):
        print("Weird Number")
    else:
        print("Not Weird Number")

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to check if
// the number is weird or not
using System;
using System.Collections.Generic;

class GFG
{

// code to find all the
// factors of the number
// excluding the number itself
static List<int> factors(int n)
{
    // List to store
    // the factors
    List<int> v = new List<int>();
    v.Add(1);

    // note that this loop
    // runs till sqrt(n)
    for (int i = 2;
            i <= Math.Sqrt(n); i++)
    {

        // if the value of
        // i is a factor
        if (n % i == 0)
        {
            v.Add(i);

            // condition to check
            // the divisor is not
            // the number itself
            if (n / i != i)
            {
                v.Add(n / i);
            }
        }
    }

    // return the List
    return v;
}

// Function to check if the
// number is abundant or not
static Boolean checkAbundant(int n)
{
    List<int> v;

    int sum = 0;

    // find the divisors
    // using function
    v = factors(n);

    // sum all the factors
    for (int i = 0; i < v.Count; i++)
    {
        sum += v[i];
    }

    // check for abundant
    // or not
    if (sum > n)
        return true;
    else
        return false;
}

// Function to check if the
// number is semi-perfect or not
static Boolean checkSemiPerfect(int n)
{
    List<int> v;

    // find the divisors
    v = factors(n);

    // sorting the List
    v.Sort();

    int r = v.Count;

    // subset to check if
    // no is semiperfect
    Boolean [,]subset = new Boolean[r + 1,n + 1];

    // initialising 1st
    // column to true
    for (int i = 0; i <= r; i++)
        subset[i,0] = true;

    // initialing 1st row except
    // zero position to 0
    for (int i = 1; i <= n; i++)
        subset[0,i] = false;

    // loop to find whether
    // the number is semiperfect
    for (int i = 1; i <= r; i++)
    {
        for (int j = 1; j <= n; j++)
        {

            // calculation to check
            // if the number can be
            // made by summation of
            // divisors
            if (j < v[i-1])
                subset[i,j] = subset[i - 1,j];
            else {
                subset[i,j] = subset[i - 1,j] ||
                            subset[i - 1,j -
                                v[i-1]];
            }
        }
    }

    // if not possible to make
    // the number by any
    // combination of divisors
    if ((subset[r,n]) == false)
        return false;
    else
        return true;
}

// Function to check
// for weird or not
static Boolean checkweird(int n)
{
    if (checkAbundant(n) == true &&
        checkSemiPerfect(n) == false)
        return true;
    else
        return false;
}

// Driver Code
public static void Main(String []args)
{
    int n = 70;

    if (checkweird(n))
        Console.WriteLine("Weird Number");
    else
        Console.WriteLine("Not Weird Number");
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript program to check if the
// number is weird or not

// code to find all the factors of
// the number excluding the number itself
function factors(n)
{
    // vector to store the factors
    var v = [];
    v.push(1);

    // note that this loop runs till sqrt(n)
    for (var i = 2; i <= Math.sqrt(n); i++) {

        // if the value of i is a factor
        if (n % i == 0) {
            v.push(i);

            // condition to check the
            // divisor is not the number itself
            if (n / i != i) {
                v.push(n / i);
            }
        }
    }
    // return the vector
    return v;
}

// Function to check if the number
// is abundant or not
function checkAbundant(n)
{
    var v = [];

    var sum = 0;

    // find the divisors using function
    v = factors(n);

    // sum all the factors
    for (var i = 0; i < v.length; i++) {
        sum += v[i];
    }

    // check for abundant or not
    if (sum > n)
        return true;
    else
        return false;
}

// Function to check if the
// number is semi-perfect or not
function checkSemiPerfect(n)
{
    var v = [];

    // find the divisors
    v = factors(n);

    // sorting the vector
    v.sort()

    var r = v.length;

    // subset to check if no is semiperfect
    var subset = Array.from(Array(r+1), ()=>Array(n+1));

    // initialising 1st column to true
    for (var i = 0; i <= r; i++)
        subset[i][0] = true;

    // initialing 1st row except zero position to 0
    for (var i = 1; i <= n; i++)
        subset[0][i] = false;

    // loop to find whether the number is semiperfect
    for (var i = 1; i <= r; i++) {
        for (var j = 1; j <= n; j++) {

            // calculation to check if the
            // number can be made by summation of divisors
            if (j < v[i - 1])
                subset[i][j] = subset[i - 1][j];
            else {
                subset[i][j] = subset[i - 1][j] ||
                               subset[i - 1][j - v[i - 1]];
            }
        }
    }

    // if not possible to make the
    // number by any combination of divisors
    if ((subset[r][n]) == 0)
        return false;
    else
        return true;
}

// Function to check for
// weird or not
function checkweird(n)
{
    if (checkAbundant(n) == true &&
        checkSemiPerfect(n) == false)
        return true;
    else
        return false;
}

// Driver Code
var n = 70;
if (checkweird(n))
    document.write( "Weird Number");
else
    document.write( "Not Weird Number");

</script>
```

**Output:** 

```
Weird Number
```

**时间复杂度:** O(N *因子个数)
T3】辅助空间: O(N *因子个数)