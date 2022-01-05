# 半完美号

> 原文:[https://www.geeksforgeeks.org/semiperfect-number/](https://www.geeksforgeeks.org/semiperfect-number/)

在数论中，一个[半完全数](https://en.wikipedia.org/wiki/Semiperfect_number)或伪完全数是一个自然数 n，它等于它的所有或一些适当除数的和。一个等于其所有自然数之和的半完全数是一个[完全数](https://www.geeksforgeeks.org/perfect-number/)。
给定一个数，任务是检查这个数是否是半完全数。

**示例:**

> **输入:**40
> T3】输出:数字为半完美
> 1+4+5+10+20=40
> 
> **输入:** 70
> **输出:**号码不是半完美
> 前几个半完美号码是
> 6、12、18、20、24、28、30、36、40

**方法:**将数字的所有因子存储在数据结构中([向量或数组](https://www.geeksforgeeks.org/vector-in-cpp-stl/))。按升序排列。一旦因子被存储，动态编程可以用来检查任何组合是否形成 N。问题变得类似于[子集和问题](https://www.geeksforgeeks.org/dynamic-programming-subset-sum-problem/)。我们可以用同样的方法检查这个数是否是半完全数。

下面是上述方法的实现。

## C++

```
// C++ program to check if the number
// is semi-perfect or not
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

// Function to check if the
// number is semi-perfect or not
bool check(int n)
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

    // initializing 1st row except zero position to 0
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

// driver code to check if possible
int main()
{
    int n = 40;
    if (check(n))
        cout << "Yes";
    else
        cout << "No";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to check
// if the number is
// semi-perfect or not
import java.util.*;
class GFG{

// Code to find all the factors of
// the number excluding the number itself
static Vector<Integer> factors(int n)
{
  // vector to store the factors
  Vector<Integer> v = new Vector<>();
  v.add(1);

  // note that this loop runs till Math.sqrt(n)
  for (int i = 2; i <= Math.sqrt(n); i++)
  {
    // if the value of i is a factor
    if (n % i == 0)
    {
      v.add(i);

      // condition to check the
      // divisor is not the number itself
      if (n / i != i)
      {
        v.add(n / i);
      }
    }
  }

  // return the vector
  return v;
}

// Function to check if the
// number is semi-perfect or not
static boolean check(int n)
{
  Vector<Integer> v = new Vector<>();

  // find the divisors
  v = factors(n);

  // sorting the vector
  Collections.sort(v);

  int r = v.size();

  // subset to check if no
  // is semiperfect
  boolean [][]subset =
          new boolean[r + 1][n + 1];

  // initialising 1st column to true
  for (int i = 0; i <= r; i++)
    subset[i][0] = true;

  // initializing 1st row except
  // zero position to 0
  for (int i = 1; i <= n; i++)
    subset[0][i] = false;

  // loop to find whether the
  // number is semiperfect
  for (int i = 1; i <= r; i++)
  {
    for (int j = 1; j <= n; j++)
    {
      // calculation to check if the
      // number can be made by
      // summation of divisors
      if (j < v.elementAt(i - 1))
        subset[i][j] = subset[i - 1][j];
      else
      {
        subset[i][j] = subset[i - 1][j] ||
                       subset[i - 1][j - v.elementAt(i - 1)];
      }
    }
  }

  // If not possible to make the
  // number by any combination of divisors
  if ((subset[r][n]) == false)
    return false;
  else
    return true;
}

// Driver code to check if possible
public static void main(String[] args)
{
  int n = 40;
  if (check(n))
    System.out.print("Yes");
  else
    System.out.print("No");
}
}

// This code is contributed by gauravrajput1
```

## 蟒蛇 3

```
# Python3 program to check if the number
# is semi-perfect or not
import math

# code to find all the factors of
# the number excluding the number itself
def factors( n):

    # vector to store the factors
    v = []
    v.append(1)

    # note that this loop runs till sqrt(n)
    sqt = int(math.sqrt(n))
    for i in range(2, sqt + 1):

        # if the value of i is a factor
        if (n % i == 0):
            v.append(i)

            # condition to check the
            # divisor is not the number itself
            if (n // i != i):
                v.append(n // i)

    # return the vector
    return v

# Function to check if the
# number is semi-perfect or not
def check( n):

    v = []

    # find the divisors
    v = factors(n)

    # sorting the vector
    v.sort()

    r = len(v)

    # subset to check if no is semiperfect
    subset = [[ 0 for i in range(n + 1)]
                  for j in range(r + 1)]

    # initialising 1st column to true
    for i in range(r + 1):
        subset[i][0] = True

    # initializing 1st row except zero position to 0
    for i in range(1, n + 1):
        subset[0][i] = False

    # loop to find whether the number is semiperfect
    for i in range(1, r + 1):
        for j in range(1, n + 1):

            # calculation to check if the
            # number can be made by summation of divisors
            if (j < v[i - 1]):
                subset[i][j] = subset[i - 1][j];
            else:
                subset[i][j] = (subset[i - 1][j] or
                                subset[i - 1][j - v[i - 1]])

    # if not possible to make the
    # number by any combination of divisors
    if ((subset[r][n]) == 0):
        return False
    else:
        return True

# Driver Code
if __name__ == "__main__":
    n = 40
    if (check(n)):
        print("Yes")
    else:
        print("No")

# This code is contributed by ChitraNayal
```

## C#

```
// C# program to check
// if the number is
// semi-perfect or not
using System;
using System.Collections.Generic;
class GFG{

// Code to find all the
// factors of the number
// excluding the number itself
static List<int> factors(int n)
{
  // vector to store the factors
  List<int> v = new List<int>();
  v.Add(1);

  // note that this loop runs
  // till Math.Sqrt(n)
  for (int i = 2;
           i <= Math.Sqrt(n); i++)
  {
    // if the value of i is
    // a factor
    if (n % i == 0)
    {
      v.Add(i);

      // condition to check the
      // divisor is not the number
      // itself
      if (n / i != i)
      {
        v.Add(n / i);
      }
    }
  }

// return the vector
return v;
}

// Function to check if the
// number is semi-perfect or not
static bool check(int n)
{
  List<int> v = new List<int>();

  // find the divisors
  v = factors(n);

  // sorting the vector
  v.Sort();

  int r = v.Count;

  // subset to check if no
  // is semiperfect
  bool [,]subset = new bool[r + 1,
                            n + 1];

  // initialising 1st column
  // to true
  for (int i = 0; i <= r; i++)
    subset[i, 0] = true;

  // initializing 1st row except
  // zero position to 0
  for (int i = 1; i <= n; i++)
    subset[0, i] = false;

  // loop to find whether the
  // number is semiperfect
  for (int i = 1; i <= r; i++)
  {
    for (int j = 1; j <= n; j++)
    {
      // calculation to check if the
      // number can be made by
      // summation of divisors
      if (j < v[i - 1])
        subset[i, j] = subset[i - 1, j];
      else
      {
        subset[i, j] = subset[i - 1, j] ||
        subset[i - 1, (j - v[i - 1])];
      }
    }
  }

  // If not possible to make
  // the number by any combination
  // of divisors
  if ((subset[r, n]) == false)
    return false;
  else
    return true;
}

// Driver code
public static void Main(String[] args)
{
  int n = 40;

  if (check(n))
    Console.Write("Yes");
  else
    Console.Write("No");
}
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>
// Javascript program to check
// if the number is
// semi-perfect or not

// Code to find all the factors of
// the number excluding the number itself
function factors(n)
{
    // vector to store the factors
  let v = [];
  v.push(1);

  // note that this loop runs till Math.sqrt(n)
  for (let i = 2; i <= Math.sqrt(n); i++)
  {
    // if the value of i is a factor
    if (n % i == 0)
    {
      v.push(i);

      // condition to check the
      // divisor is not the number itself
      if (Math.floor(n / i) != i)
      {
        v.push(Math.floor(n / i));
      }
    }
  }

  // return the vector
  return v;
}

// Function to check if the
// number is semi-perfect or not
function check(n)
{
    let v = [] ;

  // find the divisors
  v = factors(n);

  // sorting the vector
  v.sort(function(a,b){return a-b;});

  let r = v.length;

  // subset to check if no
  // is semiperfect
  let subset = new Array(r + 1);
  for(let i=0;i<r+1;i++)
  {
      subset[i]=new Array(n+1);
    for(let j=0;j<n+1;j++)
    {
        subset[i][j]=false;
    }
  }

  // initialising 1st column to true
  for (let i = 0; i <= r; i++)
    subset[i][0] = true;

  // initializing 1st row except
  // zero position to 0
  for (let i = 1; i <= n; i++)
    subset[0][i] = false;

  // loop to find whether the
  // number is semiperfect
  for (let i = 1; i <= r; i++)
  {
    for (let j = 1; j <= n; j++)
    {
      // calculation to check if the
      // number can be made by
      // summation of divisors
      if (j < v[i-1])
        subset[i][j] = subset[i - 1][j];
      else
      {
        subset[i][j] = subset[i - 1][j] ||
                       subset[i - 1][j - v[i-1]];
      }
    }
  }

  // If not possible to make the
  // number by any combination of divisors
  if ((subset[r][n]) == false)
    return false;
  else
    return true;
}

// Driver code to check if possible
let n = 40;
if (check(n))
    document.write("Yes");
else
    document.write("No");

// This code is contributed by rag2127
</script>
```

**Output:** 

```
Yes
```

**时间复杂度:** O(因子数* N)
T3】辅助空间: O(因子数* N)