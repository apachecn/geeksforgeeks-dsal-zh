# 检查一个数组的所有对是否都是互质的

> 原文:[https://www . geesforgeks . org/check-如果数组的所有对都是互质的/](https://www.geeksforgeeks.org/check-if-all-the-pairs-of-an-array-are-coprime-with-each-other/)

给定一个数组 **arr[]** ，任务是检查一个数组的所有对是否彼此是[互质](https://www.geeksforgeeks.org/check-two-numbers-co-prime-not/)。当 **GCD(arr[i]，arr[j]) = 1 时，阵列的所有对都是互质的 **(i，j)** ，这样 **1≤ i < j ≤ N** 。**

**示例:**

> **输入:** arr[] = {1，3，8}
> **输出:**是
> **说明:**
> 这里，GCD(arr[0]，arr[1]) = GCD(arr[0]，arr[2]) = GCD(arr[1]，arr[2]) = 1
> 因此，所有对都是互素的。
> 
> **输入:** arr[] = {6，67，24，1}
> **输出:**否

**天真方法:**一个简单的解决方案是迭代给定数组中的每一对(A[i]，A[j])，并检查 [**gcd**](https://www.geeksforgeeks.org/basic-and-extended-euclidean-algorithms/) **(A[i]，A[j]) = 1** 与否。因此，将两者相除的唯一正整数(因子)是 1。

下面是天真方法的实现:

## C++

```
// C++ implementation of the
// above approach

#include <bits/stdc++.h>
using namespace std;

// Function to check if all the
// pairs of the array are coprime
// with each other or not
bool allCoprime(int A[], int n)
{
    bool all_coprime = true;
    for (int i = 0; i < n; i++) {
        for (int j = i + 1; j < n; j++) {

            // Check if GCD of the
            // pair is not equal to 1
            if (__gcd(A[i], A[j]) != 1) {

                // All pairs are non-coprime
                // Return false
                all_coprime = false;
                break;
            }
        }
    }
    return all_coprime;
}

// Driver Code
int main()
{
    int A[] = { 3, 5, 11, 7, 19 };
    int arr_size = sizeof(A) / sizeof(A[0]);
    if (allCoprime(A, arr_size)) {
        cout << "Yes";
    }
    else {
        cout << "No";
    }
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the
// above approach
import java.util.*;
import java.lang.*;

class GFG{

// Function to check if all the
// pairs of the array are coprime
// with each other or not
static boolean allCoprime(int A[], int n)
{
    boolean all_coprime = true;
    for(int i = 0; i < n; i++)
    {
        for(int j = i + 1; j < n; j++)
        {

            // Check if GCD of the
            // pair is not equal to 1
            if (gcd(A[i], A[j]) != 1)
            {

                // All pairs are non-coprime
                // Return false
                all_coprime = false;
                break;
            }
        }
    }
    return all_coprime;
}

// Function return gcd of two number
static int gcd(int a, int b)
{
    if (b == 0)
        return a;

    return gcd(b, a % b);
}

// Driver Code
public static void main (String[] args)
{
    int A[] = { 3, 5, 11, 7, 19 };
    int arr_size = A.length;

    if (allCoprime(A, arr_size))
    {
        System.out.println("Yes");
    }
    else
    {
        System.out.println("No");
    }
}
}

// This code is contributed by offbeat
```

## 蟒蛇 3

```
# Python3 implementation of the
# above approach
def gcd(a, b):

    if (b == 0):
        return a
    else:
        return gcd(b, a % b)

# Function to check if all the
# pairs of the array are coprime
# with each other or not
def allCoprime(A, n):

    all_coprime = True

    for i in range(n):
        for j in range(i + 1, n):

            # Check if GCD of the
            # pair is not equal to 1
            if gcd(A[i], A[j]) != 1:

                # All pairs are non-coprime
                # Return false
                all_coprime = False;
                break

    return all_coprime

# Driver code  
if __name__=="__main__":

    A = [ 3, 5, 11, 7, 19 ]
    arr_size = len(A)

    if (allCoprime(A, arr_size)):
        print('Yes')
    else:
        print('No')

# This code is contributed by rutvik_56
```

## C#

```
// C# implementation of the
// above approach
using System;
class GFG{

// Function to check if all the
// pairs of the array are coprime
// with each other or not
static bool allCoprime(int []A,
                       int n)
{
  bool all_coprime = true;
  for(int i = 0; i < n; i++)
  {
    for(int j = i + 1; j < n; j++)
    {
      // Check if GCD of the
      // pair is not equal to 1
      if (gcd(A[i], A[j]) != 1)
      {
        // All pairs are non-coprime
        // Return false
        all_coprime = false;
        break;
      }
    }
  }
  return all_coprime;
}

// Function return gcd of two number
static int gcd(int a, int b)
{
  if (b == 0)
    return a;

  return gcd(b, a % b);
}

// Driver Code
public static void Main(String[] args)
{
  int []A = {3, 5, 11, 7, 19};
  int arr_size = A.Length;

  if (allCoprime(A, arr_size))
  {
    Console.WriteLine("Yes");
  }
  else
  {
    Console.WriteLine("No");
  }
}
}

// This code is contributed by Rajput-Ji
```

## java 描述语言

```
<script>
// JavaScript implementation of the
// above approach

function gcd(a, b) {
  if (!b) {
    return a;
  }

  return gcd(b, a % b);
}

// Function to check if all the
// pairs of the array are coprime
// with each other or not
function allCoprime( A, n)
{
    var all_coprime = true;
    for (var i = 0; i < n; i++) {
        for (var j = i + 1; j < n; j++) {

            // Check if GCD of the
            // pair is not equal to 1
            if (gcd(A[i], A[j]) != 1) {

                // All pairs are non-coprime
                // Return false
                all_coprime = false;
                break;
            }
        }
    }
    return all_coprime;
}

/* Driver Program */

var A = [ 3, 5, 11, 7, 19 ];
var arr_size = A.length;
if (allCoprime(A, arr_size)) {
    console.log("Yes");
}
else {
    console.log( "No");
}

// This code is contributed by ukasp.
</script>
```

**Output:** 

```
Yes
```

***时间复杂度:**O(N<sup>2</sup>logN)*
***辅助空间:** O(1)*

**有效方法:**问题中的关键观察是，如果两个数除的正整数(因子)都是 1，那么这两个数就称为同素数。因此，我们可以将数组中每个元素的因子存储在容器(集合、数组等)中。)包括这个元素，并检查这个因素是否已经存在。

插图:

> 对于数组 arr[] = {6，5，10，3}
> 由于对(6，10)、(6，3)和(5，10)具有公共因子，因此数组中的所有对都不是互质的。

下面是上述方法的实现:

## C++

```
// C++ implementation of the
// above approach

#include <bits/stdc++.h>
using namespace std;

// Function to store and
// check the factors
bool findFactor(int value,
                unordered_set<int>& factors)
{
    factors.insert(value);
    for (int i = 2; i * i <= value; i++) {
        if (value % i == 0) {

            // Check if factors are equal
            if (value / i == i) {

                // Check if the factor is
                // already present
                if (factors.find(i)
                    != factors.end()) {
                    return true;
                }
                else {

                    // Insert the factor in set
                    factors.insert(i);
                }
            }
            else {

                // Check if the factor is
                // already present
                if (factors.find(i) != factors.end()
                    || factors.find(value / i)
                           != factors.end()) {
                    return true;
                }
                else {

                    // Insert the factors in set
                    factors.insert(i);
                    factors.insert(value / i);
                }
            }
        }
    }
    return false;
}

// Function to check if all the
// pairs of array elements
// are coprime with each other
bool allCoprime(int A[], int n)
{
    bool all_coprime = true;
    unordered_set<int> factors;
    for (int i = 0; i < n; i++) {
        if (A[i] == 1)
            continue;

        // Check if factors of A[i]
        // haven't occurred previously
        if (findFactor(A[i], factors)) {
            all_coprime = false;
            break;
        }
    }
    return all_coprime;
}

// Driver Code
int main()
{
    int A[] = { 3, 5, 11, 7, 19 };
    int arr_size = sizeof(A) / sizeof(A[0]);
    if (allCoprime(A, arr_size)) {
        cout << "Yes";
    }
    else {
        cout << "No";
    }
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of
// the above approach
import java.util.*;
class GFG{

// Function to store and
// check the factors
static boolean findFactor(int value,
                          HashSet<Integer> factors)
{
  factors.add(value);
  for (int i = 2; i * i <= value; i++)
  {
    if (value % i == 0)
    {
      // Check if factors are equal
      if (value / i == i)
      {
        // Check if the factor is
        // already present
        if (factors.contains(i))
        {
          return true;
        }
        else
        {
          // Insert the factor in set
          factors.add(i);
        }
      }
      else
      {
        // Check if the factor is
        // already present
        if (factors.contains(i) ||
            factors.contains(value / i))
        {
          return true;
        }
        else
        {
          // Insert the factors in set
          factors.add(i);
          factors.add(value / i);
        }
      }
    }
  }
  return false;
}

// Function to check if all the
// pairs of array elements
// are coprime with each other
static boolean allCoprime(int A[], int n)
{
  boolean all_coprime = true;
  HashSet<Integer> factors =
          new HashSet<Integer>();
  for (int i = 0; i < n; i++)
  {
    if (A[i] == 1)
      continue;

    // Check if factors of A[i]
    // haven't occurred previously
    if (findFactor(A[i], factors))
    {
      all_coprime = false;
      break;
    }
  }
  return all_coprime;
}

// Driver Code
public static void main(String[] args)
{
  int A[] = {3, 5, 11, 7, 19};
  int arr_size = A.length;
  if (allCoprime(A, arr_size))
  {
    System.out.print("Yes");
  }
  else
  {
    System.out.print("No");
  }
}
}

// This code is contributed by shikhasingrajput
```

## 蟒蛇 3

```
# Python3 implementation of
# the above approach

# Function to store and
# check the factors
def findFactor(value, factors):

    factors.add(value)
    i = 2
    while(i * i <= value):

      if value % i == 0:

            # Check if factors are equal
            if value // i == i:

              # Check if the factor is
              # already present
              if i in factors:
                  return bool(True)
              else:

                  # Insert the factor in set
                  factors.add(i)
            else:   

                # Check if the factor is
                # already present
                if (i in factors) or
                   ((value // i) in factors):               
                  return bool(True)               
                else :

                  # Insert the factors in set
                  factors.add(i)
                  factors.add(value // i)

      i += 1     
    return bool(False)

# Function to check if all the
# pairs of array elements
# are coprime with each other
def allCoprime(A, n):

  all_coprime = bool(True)
  factors = set()

  for i in range(n):     
    if A[i] == 1:
        continue

    # Check if factors of A[i]
    # haven't occurred previously
    if findFactor(A[i], factors):   
      all_coprime = bool(False)
      break

  return bool(all_coprime)

# Driver code
A = [3, 5, 11, 7, 19]
arr_size = len(A)

if (allCoprime(A, arr_size)):
    print("Yes")
else:
    print("No")

# This code is contributed by divyeshrabadiya07
```

## C#

```
// C# implementation of
// the above approach
using System;
using System.Collections.Generic;

class GFG{

// Function to store and
// check the factors
static bool findFactor(int value,
               HashSet<int> factors)
{
    factors.Add(value);
    for(int i = 2; i * i <= value; i++)
    {
        if (value % i == 0)
        {

            // Check if factors are equal
            if (value / i == i)
            {

                // Check if the factor is
                // already present
                if (factors.Contains(i))
                {
                    return true;
                }
                else
                {

                    // Insert the factor in set
                    factors.Add(i);
                }
            }
            else
            {

                // Check if the factor is
                // already present
                if (factors.Contains(i) ||
                    factors.Contains(value / i))
                {
                    return true;
                }
                else
                {
                    // Insert the factors in set
                    factors.Add(i);
                    factors.Add(value / i);
                }
            }
        }
    }
    return false;
}

// Function to check if all the
// pairs of array elements
// are coprime with each other
static bool allCoprime(int []A, int n)
{
    bool all_coprime = true;
    HashSet<int> factors = new HashSet<int>();

    for(int i = 0; i < n; i++)
    {
        if (A[i] == 1)
            continue;

        // Check if factors of A[i]
        // haven't occurred previously
        if (findFactor(A[i], factors))
        {
            all_coprime = false;
            break;
        }
    }
    return all_coprime;
}

// Driver Code
public static void Main(String[] args)
{
    int []A = { 3, 5, 11, 7, 19 };
    int arr_size = A.Length;

    if (allCoprime(A, arr_size))
    {
        Console.Write("Yes");
    }
    else
    {
        Console.Write("No");
    }
}
}

// This code is contributed by Amit Katiyar
```

**Output:** 

```
Yes
```

***时间复杂度:**O(N<sup>3/2</sup>)*
***辅助空间:** O(N)*