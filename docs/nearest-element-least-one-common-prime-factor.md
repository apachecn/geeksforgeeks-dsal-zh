# 具有至少一个公共质因数的最近元素

> 原文:[https://www . geesforgeks . org/最近元素最少一个公共素因子/](https://www.geeksforgeeks.org/nearest-element-least-one-common-prime-factor/)

给定一个数组 arr[]，为每个元素找到最近的元素，这样至少有一个公共质因数。在输出中，我们需要打印最近元素的位置。
**例:**

```
Input: arr[] = {2, 9, 4, 3, 13}
Output: 3 4 1 2 -1
Explanation : 
Closest element for 1st element is 3rd. 
=>Common prime factor of 1st and 3rd elements
  is 2.
Closest element for 2nd element is 4th.
=>Common prime factor of 2nd and 4th elements
  is 3.
```

**天真的做法**

只有当这两个数的 GCD 大于 1 时，公共质因数才会存在。简单的蛮力是运行两个循环，一个在另一个里面，同时从每个索引到两边逐个迭代，找到大于 1 的 gcd。每当我们找到答案时，就打破循环，打印出来。如果我们在遍历了数组的两边之后到达了数组的末尾，那么只需打印-1。

## C++

```
// C++ program to print nearest element with at least
// one common prime factor.
#include<bits/stdc++.h>
using namespace std;

void nearestGcd(int arr[], int n)
{
    // Loop covers the every element of arr[]
    for (int i=0; i<n; ++i)
    {
        int closest = -1;

        // Loop that covers from 0 to i-1 and i+1
        // to n-1 indexes simultaneously
        for (int j=i-1, k=i+1; j>0 || k<=n; --j, ++k)
        {
            if (j>=0 && __gcd(arr[i], arr[j]) > 1)
            {
                closest = j+1;
                break;
            }
            if (k<n && __gcd(arr[i], arr[k])>1)
            {
                closest = k+1;
                break;
            }
        }

        // print position of closest element
        cout << closest << " ";
    }
}

// Driver code
int main()
{
    int arr[] = {2, 9, 4, 3, 13};
    int n = sizeof(arr)/sizeof(arr[0]);
    nearestGcd(arr, n);
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print nearest element
// with at least one common prime factor.
import java.util.*;
import java.lang.*;

class GFG
{
static void nearestGcd(int []arr, int n)
{
    // Loop covers the every
    // element of arr[]
    for (int i = 0; i < n; ++i)
    {
        int closest = -1;

        // Loop that covers from 0 to
        // i-1 and i+1 to n-1 indexes
        // simultaneously
        for (int j = i - 1, k = i + 1;
                 j > 0 || k <= n; --j, ++k)
        {
            if (j >= 0 && __gcd(arr[i], arr[j]) > 1)
            {
                closest = j + 1;
                break;
            }
            if (k < n && __gcd(arr[i], arr[k]) > 1)
            {
                closest = k + 1;
                break;
            }
        }

        // print position of closest element
        System.out.print(closest + " ");
    }
}

// Recursive function to return
// gcd of a and b
static int __gcd(int a, int b)
{
    if (b == 0)
        return a;
    return __gcd(b, a % b);
}

// Driver Code
public static void main(String args[])
{
    int []arr = {2, 9, 4, 3, 13};
    int n = arr.length;
    nearestGcd(arr, n);
}
}

// This code is contributed
// by Akanksha Rai
```

## 蟒蛇 3

```
# Python 3 program to print nearest
# element with at least one common
# prime factor.
import math

def nearestGcd(arr, n):

    # Loop covers the every element of arr[]
    for i in range(n):
        closest = -1

        # Loop that covers from 0 to i-1 and
        # i+1 to n-1 indexes simultaneously
        j = i - 1
        k = i + 1
        while j > 0 or k <= n:
            if (j >= 0 and
                math.gcd(arr[i], arr[j]) > 1):
                closest = j + 1
                break

            if (k < n and
                math.gcd(arr[i], arr[k]) > 1):
                closest = k + 1
                break
            k += 1
            j -= 1

        # print position of closest element
        print(closest, end = " ")

# Driver code
if __name__=="__main__":

    arr = [2, 9, 4, 3, 13]
    n = len(arr)
    nearestGcd(arr, n)

# This code is contributed by ita_c
```

## C#

```
// C# program to print nearest element
// with at least one common prime factor.
using System;

class GFG
{
static void nearestGcd(int []arr, int n)
{
    // Loop covers the every
    // element of arr[]
    for (int i = 0; i < n; ++i)
    {
        int closest = -1;

        // Loop that covers from 0 to
        // i-1 and i+1 to n-1 indexes
        // simultaneously
        for (int j = i - 1, k = i + 1;
                 j > 0 || k <= n; --j, ++k)
        {
            if (j >= 0 && __gcd(arr[i], arr[j]) > 1)
            {
                closest = j + 1;
                break;
            }
            if (k < n && __gcd(arr[i], arr[k]) > 1)
            {
                closest = k + 1;
                break;
            }
        }

        // print position of closest element
        Console.Write(closest + " ");
    }
}

// Recursive function to return
// gcd of a and b
static int __gcd(int a, int b)
{    
    if (b == 0)
        return a;
    return __gcd(b, a % b);
}

// Driver code
public static void Main()
{
    int []arr = {2, 9, 4, 3, 13};
    int n = arr.Length;
    nearestGcd(arr, n);
}
}

// This code is contributed
// by 29AjayKumar
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP program to print nearest element
// with at least one common prime factor.

function nearestGcd($arr, $n)
{
    // Loop covers the every
    // element of arr[]
    for ($i = 0; $i < $n; ++$i)
    {
        $closest = -1;

        // Loop that covers from 0 to
        // i-1 and i+1 to n-1 indexes
        // simultaneously
        for ($j = $i - 1, $k = $i + 1;
             $j > 0 || $k <= $n; --$j, ++$k)
        {
            if ($j >= 0 && __gcd($arr[$i],
                                 $arr[$j]) > 1)
            {
                $closest = $j + 1;
                break;
            }
            if ($k < $n && __gcd($arr[$i],
                                 $arr[$k]) > 1)
            {
                $closest = $k + 1;
                break;
            }
        }

        // print position of closest element
        echo $closest . " ";
    }
}

// Recursive function to return
// gcd of a and b
function __gcd($a, $b)
{
    if ($b == 0)
        return $a;
    return __gcd($b, $a % $b);
}

// Driver Code
$arr = array(2, 9, 4, 3, 13);
$n = sizeof($arr);
nearestGcd($arr, $n);

// This code is contributed
// by Akanksha Rai
?>
```

## java 描述语言

```
<script>
// Javascript program to print nearest element
// with at least one common prime factor.

function nearestGcd(arr,n)
{
    // Loop covers the every
    // element of arr[]
    for (let i = 0; i < n; ++i)
    {
        let closest = -1;

        // Loop that covers from 0 to
        // i-1 and i+1 to n-1 indexes
        // simultaneously
        for (let j = i - 1, k = i + 1;
                 j > 0 || k <= n; --j, ++k)
        {
            if (j >= 0 && __gcd(arr[i], arr[j]) > 1)
            {
                closest = j + 1;
                break;
            }
            if (k < n && __gcd(arr[i], arr[k]) > 1)
            {
                closest = k + 1;
                break;
            }
        }

        // print position of closest element
        document.write(closest + " ");
    }
}

// Recursive function to return
// gcd of a and b
function __gcd(a,b)
{
    if (b == 0)
        return a;
    return __gcd(b, a % b);
}

// Driver Code
let arr=[2, 9, 4, 3, 13];
let n = arr.length;
nearestGcd(arr, n);

// This code is contributed by unknown2108
</script>
```

```
Output: 3 4 1 2 -1
```

**时间复杂度:**O(n<sup>2</sup>)
T5】辅助空间: O(1)

**高效方法**

我们找到所有数组元素的素因子。为了快速找到质因数，我们使用厄拉多塞的[筛。对于每个元素，我们考虑所有的素因子，并使用一个公共因子来跟踪最接近的元素。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/) 

## C++

```
// C++ program to print nearest element with at least
// one common prime factor.
#include <bits/stdc++.h>
using namespace std;

const int MAX = 100001;
const int INF = INT_MAX;

int primedivisor[MAX], dist[MAX], pos[MAX], divInd[MAX];

vector<int> divisors[MAX];

// Pre-computation of smallest prime divisor
// of all numbers
void sieveOfEratosthenes()
{
    for (int i=2; i*i < MAX; ++i)
    {
        if (!primedivisor[i])
            for (int j = i*i; j < MAX; j += i)
                primedivisor[j] = i;
    }

    // Prime number will have same divisor
    for (int i = 1; i < MAX; ++i)
        if (!primedivisor[i])
            primedivisor[i] = i;
}

// Function to calculate all divisors of
// input array
void findDivisors(int arr[], int n)
{
    for (int i=0; i<MAX; ++i)
        pos[i] = divInd[i] = -1, dist[i] = INF;

    for (int i=0; i<n; ++i)
    {
        int num = arr[i];
        while (num > 1)
        {
            int div = primedivisor[num];
            divisors[i].push_back(div);
            while (num % div == 0)
                num /= div;
        }
    }
}

void nearestGCD(int arr[], int n)
{
    // Pre-compute all the divisors of array
    // element by using prime factors
    findDivisors(arr, n);

    // Traverse all elements,
    for (int i=0; i<n; ++i)
    {
        // For every divisor of current element,
        // find closest element.
        for (auto &div: divisors[i])
        {
            // Visit divisor if not visited
            if (divInd[div] == -1)
                divInd[div] = i;
            else
            {
                // Fetch the index of visited divisor
                int ind = divInd[div];

                // Update the divisor index to current index
                divInd[div] = i;

                // Set the minimum distance
                if (dist[i] > abs(ind-i))
                {
                    // Set the min distance of current
                    // index 'i' to nearest one
                    dist[i] = abs(ind-i);

                    // Add 1 as indexing starts from 0
                    pos[i] = ind + 1;
                }

                if (dist[ind] > abs(ind-i))
                {
                    // Set the min distance of found index 'ind'
                    dist[ind] = abs(ind-i);

                    // Add 1 as indexing starts from 0
                    pos[ind] = i + 1;
                }
            }
        }
    }
}

// Driver code
int main()
{
    // Simple sieve to find smallest prime
    // divisor of number from 2 to MAX
    sieveOfEratosthenes();

    int arr[] = {2, 9, 4, 3, 13};
    int n = sizeof(arr)/sizeof(arr[0]);

    // function to calculate nearest distance
    // of every array elements
    nearestGCD(arr, n);

    // Print the nearest distance having GDC>1
    for (int i=0; i<n; ++i)
        cout << pos[i] << " ";
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to print nearest element with at least
// one common prime factor.
import java.io.*;
import java.util.*;
class GFG
{
  static int MAX = 100001;
  static int INF = Integer.MAX_VALUE;
  static int[] primedivisor = new int [MAX];
  static int[] dist = new int [MAX];
  static int[] pos = new int [MAX];
  static int[] divInd = new int [MAX];

  static ArrayList<ArrayList<Integer>> divisors =
    new ArrayList<ArrayList<Integer>>();

  // Pre-computation of smallest prime divisor
  // of all numbers
  static void sieveOfEratosthenes()
  {
    for (int i = 2; i * i < MAX; ++i)
    {
      if (primedivisor[i] == 0)
      {
        for (int j = i * i; j < MAX; j += i)
        {
          primedivisor[j] = i;
        }
      }
    }
    // Prime number will have same divisor
    for (int i = 1; i < MAX; ++i)
    {
      if (primedivisor[i] == 0)
      {
        primedivisor[i] = i;
      }
    }

  }

  // Function to calculate all divisors of
  // input array
  static void findDivisors(int arr[], int n)
  {
    for (int i=0; i<MAX; ++i)
    {
      pos[i] = divInd[i] = -1;
      dist[i] = INF;
    }
    for (int i = 0; i < n; ++i)
    {
      int num = arr[i];
      while (num > 1)
      {
        int div = primedivisor[num];
        divisors.get(i).add(div);
        while (num % div == 0)
        {
          num /= div;
        }
      }
    }

  }

  static void nearestGCD(int arr[], int n)
  {

    // Pre-compute all the divisors of array
    // element by using prime factors
    findDivisors(arr, n);

    // Traverse all elements,
    for (int i = 0; i < n; ++i)
    {

      // For every divisor of current element,
      // find closest element.
      for(int div : divisors.get(i))
      {

        // Visit divisor if not visited
        if (divInd[div] == -1)
        {
          divInd[div] = i;
        }
        else
        {

          // Fetch the index of visited divisor
          int ind = divInd[div];

          // Update the divisor index to current index
          divInd[div] = i;

          // Set the minimum distance
          if (dist[i] > Math.abs(ind-i))
          {

            // Set the min distance of current
            // index 'i' to nearest one
            dist[i] = Math.abs(ind-i);

            // Add 1 as indexing starts from 0
            pos[i] = ind + 1;
          }

          if (dist[ind] > Math.abs(ind-i))
          {

            // Set the min distance of found index 'ind'
            dist[ind] = Math.abs(ind-i);

            // Add 1 as indexing starts from 0
            pos[ind] = i + 1;
          }
        }
      }
    }
  }

  // Driver code
  public static void main (String[] args)
  {

    for(int i = 0; i < MAX; i++)
    {
      divisors.add(new ArrayList<Integer>());
    }

    // Simple sieve to find smallest prime
    // divisor of number from 2 to MAX
    sieveOfEratosthenes();    
    int arr[] = {2, 9, 4, 3, 13};
    int n = arr.length;

    // function to calculate nearest distance
    // of every array elements
    nearestGCD(arr, n);

    // Print the nearest distance having GDC>1
    for (int i = 0; i < n; ++i)
    {
      System.out.print(pos[i]+" ");   
    }
  }
}

// This code is contributed by avanitrachhadiya2155
```

## 蟒蛇 3

```
# Python3 program to print nearest element with at least
# one common prime factor.

MAX = 100001
INF = 10**9

primedivisor = [0 for i in range(MAX)]
dist = [0 for i in range(MAX)]
pos = [0 for i in range(MAX)]
divInd = [0 for i in range(MAX)]

divisors = [[] for i in range(MAX)]

# Pre-computation of smallest prime divisor
# of all numbers
def sieveOfEratosthenes():

    for i in range(2,MAX):
        if i * i > MAX:
            break

        if (primedivisor[i] == 0):
            for j in range(2 * i, MAX, i):
                primedivisor[j] = i

    # Prime number will have same divisor
    for i in range(1, MAX):
        if (primedivisor[i] == 0):
            primedivisor[i] = i

# Function to calculate all divisors of
# input array
def findDivisors(arr, n):

    for i in range(MAX):
        pos[i] = divInd[i] = -1
        dist[i] = 10**9
    for i in range(n):
        num = arr[i]
        while (num > 1):

            div = primedivisor[num]
            divisors[i].append(div)
            while (num % div == 0):
                num //= div

def nearestGCD(arr, n):
    # Pre-compute all the divisors of array
    # element by using prime factors
    findDivisors(arr, n)

    # Traverse all elements,
    for i in range(n):
        # For every divisor of current element,
        # find closest element.
        for div in divisors[i]:
            # Visit divisor if not visited
            if (divInd[div] == -1):
                divInd[div] = i
            else:

                # Fetch the index of visited divisor
                ind = divInd[div]

                # Update the divisor index to current index
                divInd[div] = i

                # Set the minimum distance
                if (dist[i] > abs(ind-i)):

                    # Set the min distance of current
                    # index 'i' to nearest one
                    dist[i] = abs(ind-i)

                    # Add 1 as indexing starts from 0
                    pos[i] = ind + 1

                if (dist[ind] > abs(ind-i)):

                    # Set the min distance of found index 'ind'
                    dist[ind] = abs(ind-i)

                    # Add 1 as indexing starts from 0
                    pos[ind] = i + 1

# Driver code

# Simple sieve to find smallest prime
# divisor of number from 2 to MAX
sieveOfEratosthenes()

arr =[2, 9, 4, 3, 13]
n = len(arr)

# function to calculate nearest distance
# of every array elements
nearestGCD(arr, n)

# Print the nearest distance having GDC>1
for i in range(n):
    print(pos[i],end=" ")

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to print nearest element with at least
// one common prime factor.
using System;
using System.Collections.Generic;

public class GFG{

  static int MAX = 100001;
  static int INF = Int32.MaxValue;
  static int[] primedivisor = new int [MAX];
  static int[] dist = new int [MAX];
  static int[] pos = new int [MAX];
  static int[] divInd = new int [MAX];

  static List<List<int>> divisors = new List<List<int>>();

  // Pre-computation of smallest prime divisor
  // of all numbers
  static void sieveOfEratosthenes()
  {
    for (int i = 2; i * i < MAX; ++i)
    {
      if (primedivisor[i] == 0)
      {
        for (int j = i * i; j < MAX; j += i)
        {
          primedivisor[j] = i;
        }
      }
    }
    // Prime number will have same divisor
    for (int i = 1; i < MAX; ++i)
    {
      if (primedivisor[i] == 0)
      {
        primedivisor[i] = i;
      }
    }

  }

  // Function to calculate all divisors of
  // input array
  static void findDivisors(int[] arr, int n)
  {
    for (int i=0; i<MAX; ++i)
    {
      pos[i] = divInd[i] = -1;
      dist[i] = INF;
    }
    for (int i = 0; i < n; ++i)
    {
      int num = arr[i];
      while (num > 1)
      {
        int div = primedivisor[num];
        divisors[i].Add(div);
        while (num % div == 0)
        {
          num /= div;
        }
      }
    }

  }

  static void nearestGCD(int[] arr, int n)
  {

    // Pre-compute all the divisors of array
    // element by using prime factors
    findDivisors(arr, n);

    // Traverse all elements,
    for (int i = 0; i < n; ++i)
    {

      // For every divisor of current element,
      // find closest element.
      foreach(int div in divisors[i])
      {

        // Visit divisor if not visited
        if (divInd[div] == -1)
        {
          divInd[div] = i;
        }
        else
        {

          // Fetch the index of visited divisor
          int ind = divInd[div];

          // Update the divisor index to current index
          divInd[div] = i;

          // Set the minimum distance
          if (dist[i] > Math.Abs(ind-i))
          {

            // Set the min distance of current
            // index 'i' to nearest one
            dist[i] = Math.Abs(ind-i);

            // Add 1 as indexing starts from 0
            pos[i] = ind + 1;
          }

          if (dist[ind] > Math.Abs(ind-i))
          {

            // Set the min distance of found index 'ind'
            dist[ind] = Math.Abs(ind-i);

            // Add 1 as indexing starts from 0
            pos[ind] = i + 1;
          }
        }
      }
    }
  }

  // Driver code 
  static public void Main ()
  {
    for(int i = 0; i < MAX; i++)
    {
      divisors.Add(new List<int>());
    }
    // Simple sieve to find smallest prime
    // divisor of number from 2 to MAX
    sieveOfEratosthenes();    
    int[] arr = {2, 9, 4, 3, 13};
    int n = arr.Length;

    // function to calculate nearest distance
    // of every array elements
    nearestGCD(arr, n);

    // Print the nearest distance having GDC>1
    for (int i = 0; i < n; ++i)
    {
      Console.Write(pos[i]+" ");   
    }
  }
}

// This code is contributed by rag2127
```

## java 描述语言

```
<script>
// Javascript program to print nearest element with at least
// one common prime factor.

let MAX = 100001;
let INF = Number.MAX_VALUE;
let primedivisor = new Array(MAX);
let dist = new Array(MAX);
let pos = new Array(MAX);
let divInd = new Array(MAX);

for(let i=0;i<MAX;i++)
{
    primedivisor[i]=0;
    dist[i]=0;
    pos[i]=0;
    divInd[i]=0;
}

let divisors =[];

// Pre-computation of smallest prime divisor
  // of all numbers
function sieveOfEratosthenes()
{
    for (let i = 2; i * i < MAX; ++i)
    {
      if (primedivisor[i] == 0)
      {
        for (let j = i * i; j < MAX; j += i)
        {
          primedivisor[j] = i;
        }
      }
    }
    // Prime number will have same divisor
    for (let i = 1; i < MAX; ++i)
    {
      if (primedivisor[i] == 0)
      {
        primedivisor[i] = i;
      }
    }
}

// Function to calculate all divisors of
  // input array
function findDivisors(arr,n)
{
    for (let i=0; i<MAX; ++i)
    {
      pos[i] = divInd[i] = -1;
      dist[i] = INF;
    }
    for (let i = 0; i < n; ++i)
    {
      let num = arr[i];
      while (num > 1)
      {
        let div = primedivisor[num];
        divisors[i].push(div);
        while (num % div == 0)
        {
          num = Math.floor(num/div);
        }
      }
    }
}

function nearestGCD(arr,n)
{
    // Pre-compute all the divisors of array
    // element by using prime factors
    findDivisors(arr, n);

    // Traverse all elements,
    for (let i = 0; i < n; ++i)
    {

      // For every divisor of current element,
      // find closest element.
      for(let div=0;div<divisors[i].length;div++)
      {

        // Visit divisor if not visited
        if (divInd[divisors[i][div]] == -1)
        {
          divInd[divisors[i][div]] = i;
        }
        else
        {

          // Fetch the index of visited divisor
          let ind = divInd[divisors[i][div]];

          // Update the divisor index to current index
          divInd[divisors[i][div]] = i;

          // Set the minimum distance
          if (dist[i] > Math.abs(ind-i))
          {

            // Set the min distance of current
            // index 'i' to nearest one
            dist[i] = Math.abs(ind-i);

            // Add 1 as indexing starts from 0
            pos[i] = ind + 1;
          }

          if (dist[ind] > Math.abs(ind-i))
          {

            // Set the min distance of found index 'ind'
            dist[ind] = Math.abs(ind-i);

            // Add 1 as indexing starts from 0
            pos[ind] = i + 1;
          }
        }
      }
    }
}

// Driver code
for(let i = 0; i < MAX; i++)
{
divisors.push([]);
}

// Simple sieve to find smallest prime
// divisor of number from 2 to MAX
sieveOfEratosthenes();   
let arr= [2, 9, 4, 3, 13];
let n = arr.length;

// function to calculate nearest distance
// of every array elements
nearestGCD(arr, n);

// Print the nearest distance having GDC>1
for (let i = 0; i < n; ++i)
{
document.write(pos[i]+" ");  
}

// This code is contributed by patel2127

</script>
```

**输出:**

```
3 4 1 2 -1
```

**时间复杂度:**O(MAX * log(log(MAX))
**辅助空间:** O(MAX)
本文由[舒巴姆班萨尔](https://www.facebook.com/banalshubham)供稿。如果你喜欢 GeeksforGeeks 并想投稿，你也可以使用[write.geeksforgeeks.org](https://write.geeksforgeeks.org)写一篇文章或者把你的文章邮寄到 contribute@geeksforgeeks.org。看到你的文章出现在极客博客主页上，帮助其他极客。
如果发现有不正确的地方，请写评论，或者想分享更多关于以上讨论话题的信息