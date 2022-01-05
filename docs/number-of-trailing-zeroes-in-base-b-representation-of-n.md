# N 的基 B 表示中尾随零的个数！

> 原文:[https://www . geeksforgeeks . org/n 的尾随零位数表示法/](https://www.geeksforgeeks.org/number-of-trailing-zeroes-in-base-b-representation-of-n/)

给定两个正整数 B 和 N，任务是找出 N 的 B 进制(基 B)表示中尾随零的个数！(N 的阶乘)
**例:**

```
Input: N = 5, B = 2
Output: 3
5! = 120 which is represented as 1111000 in base 2\. 

Input: N = 6, B = 9
Output: 1
```

A **天真的解决方案**是找到给定数字的阶乘，并将其转换为给定的基数 b。然后，计算尾随零的数量，但这将是一个昂贵的操作。此外，找到大数的阶乘并将其存储为整数也不容易。
**有效方法:**假设基数为 10，即十进制，那么我们必须计算除以 N 的 10 的最高幂！使用[勒让德公式](https://www.geeksforgeeks.org/legendres-formula-highest-power-of-prime-number-that-divides-n/)。因此，数字 B 在转换为基数 B 时表示为 10，假设基数 B = 13，那么基数 13 中的 13 将表示为 10，即 13 <sub>10</sub> = 10 <sub>13</sub> 。因此，问题简化为寻找 N 中 B 的最高幂！。([n 中 k 的最大幂！](https://www.geeksforgeeks.org/largest-power-k-n-factorial-k-may-not-prime/) )
以下是上述办法的实施情况。

## C++

```
// CPP program to find the number of trailing
// zeroes in base B representation of N!
#include <bits/stdc++.h>
using namespace std;

// To find the power of a prime p in
// factorial N
int findPowerOfP(int N, int p)
{
    int count = 0;
    int r = p;
    while (r <= N) {

        // calculating floor(n/r)
        // and adding to the count
        count += (N / r);

        // increasing the power of p
        // from 1 to 2 to 3 and so on
        r = r * p;
    }
    return count;
}

// returns all the prime factors of k
vector<pair<int, int> > primeFactorsofB(int B)
{
    // vector to store all the prime factors
    // along with their number of occurrence
    // in factorization of B
    vector<pair<int, int> > ans;

    for (int i = 2; B != 1; i++) {
        if (B % i == 0) {
            int count = 0;
            while (B % i == 0) {
                B = B / i;
                count++;
            }

            ans.push_back(make_pair(i, count));
        }
    }
    return ans;
}

// Returns largest power of B that
// divides N!
int largestPowerOfB(int N, int B)
{
    vector<pair<int, int> > vec;
    vec = primeFactorsofB(B);
    int ans = INT_MAX;
    for (int i = 0; i < vec.size(); i++)

        // calculating minimum power of all
        // the prime factors of B
        ans = min(ans, findPowerOfP(N,
                                    vec[i].first)
                           / vec[i].second);

    return ans;
}

// Driver code
int main()
{
    cout << largestPowerOfB(5, 2) << endl;
    cout << largestPowerOfB(6, 9) << endl;
    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the number of trailing
// zeroes in base B representation of N!
import java.util.*;
class GFG
{
static class pair
{
    int first, second;
    public pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// To find the power of a prime p in
// factorial N
static int findPowerOfP(int N, int p)
{
    int count = 0;
    int r = p;
    while (r <= N)
    {

        // calculating floor(n/r)
        // and adding to the count
        count += (N / r);

        // increasing the power of p
        // from 1 to 2 to 3 and so on
        r = r * p;
    }
    return count;
}

// returns all the prime factors of k
static Vector<pair> primeFactorsofB(int B)
{
    // vector to store all the prime factors
    // along with their number of occurrence
    // in factorization of B
    Vector<pair> ans = new Vector<pair>();

    for (int i = 2; B != 1; i++)
    {
        if (B % i == 0)
        {
            int count = 0;
            while (B % i == 0)
            {
                B = B / i;
                count++;
            }

            ans.add(new pair(i, count));
        }
    }
    return ans;
}

// Returns largest power of B that
// divides N!
static int largestPowerOfB(int N, int B)
{
    Vector<pair> vec = new Vector<pair>();
    vec = primeFactorsofB(B);
    int ans = Integer.MAX_VALUE;
    for (int i = 0; i < vec.size(); i++)

        // calculating minimum power of all
        // the prime factors of B
        ans = Math.min(ans, findPowerOfP(
                       N, vec.get(i).first) /
                          vec.get(i).second);

    return ans;
}

// Driver code
public static void main(String[] args)
{
    System.out.println(largestPowerOfB(5, 2));
    System.out.println(largestPowerOfB(6, 9));
}
}

// This code is contributed by Princi Singh
```

## 蟒蛇 3

```
# Python 3 program to find the number of
# trailing zeroes in base B representation of N!
import sys

# To find the power of a prime
# p in factorial N
def findPowerOfP(N, p):
    count = 0
    r = p
    while (r <= N):

        # calculating floor(n/r)
        # and adding to the count
        count += int(N / r)

        # increasing the power of p
        # from 1 to 2 to 3 and so on
        r = r * p

    return count

# returns all the prime factors of k
def primeFactorsofB(B):

    # vector to store all the prime factors
    # along with their number of occurrence
    # in factorization of B'
    ans = []
    i = 2

    while(B!= 1):
        if (B % i == 0):
            count = 0
            while (B % i == 0):

                B = int(B / i)
                count += 1

            ans.append((i, count))

        i += 1

    return ans

# Returns largest power of B that
# divides N!
def largestPowerOfB(N, B):
    vec = []
    vec = primeFactorsofB(B)
    ans = sys.maxsize

    # calculating minimum power of all
    # the prime factors of B
    ans = min(ans, int(findPowerOfP(N, vec[0][0]) /
                                       vec[0][1]))

    return ans

# Driver code
if __name__ == '__main__':
    print(largestPowerOfB(5, 2))
    print(largestPowerOfB(6, 9))

# This code is contributed by
# Surendra_Gangwar
```

## C#

```
// C# program to find the number of trailing
// zeroes in base B representation of N!
using System;
using System.Collections.Generic;

class GFG
{
public class pair
{
    public int first, second;
    public pair(int first, int second)
    {
        this.first = first;
        this.second = second;
    }
}

// To find the power of a prime p in
// factorial N
static int findPowerOfP(int N, int p)
{
    int count = 0;
    int r = p;
    while (r <= N)
    {

        // calculating floor(n/r)
        // and adding to the count
        count += (N / r);

        // increasing the power of p
        // from 1 to 2 to 3 and so on
        r = r * p;
    }
    return count;
}

// returns all the prime factors of k
static List<pair> primeFactorsofB(int B)
{
    // vector to store all the prime factors
    // along with their number of occurrence
    // in factorization of B
    List<pair> ans = new List<pair>();

    for (int i = 2; B != 1; i++)
    {
        if (B % i == 0)
        {
            int count = 0;
            while (B % i == 0)
            {
                B = B / i;
                count++;
            }

            ans.Add(new pair(i, count));
        }
    }
    return ans;
}

// Returns largest power of B that
// divides N!
static int largestPowerOfB(int N, int B)
{
    List<pair> vec = new List<pair>();
    vec = primeFactorsofB(B);
    int ans = int.MaxValue;
    for (int i = 0; i < vec.Count; i++)

        // calculating minimum power of all
        // the prime factors of B
        ans = Math.Min(ans, findPowerOfP(
                       N, vec[i].first) /
                          vec[i].second);

    return ans;
}

// Driver code
public static void Main(String[] args)
{
    Console.WriteLine(largestPowerOfB(5, 2));
    Console.WriteLine(largestPowerOfB(6, 9));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript program to find the number of trailing
// zeroes in base B representation of N!

// To find the power of a prime p in
// factorial N
function findPowerOfP(N, p)
{
    var count = 0;
    var r = p;
    while (r <= N) {

        // calculating floor(n/r)
        // and adding to the count
        count += (N / r);

        // increasing the power of p
        // from 1 to 2 to 3 and so on
        r = r * p;
    }
    return count;
}

// returns all the prime factors of k
function primeFactorsofB(B)
{
    // vector to store all the prime factors
    // along with their number of occurrence
    // in factorization of B
    var ans = [];

    for (var i = 2; B != 1; i++) {
        if (B % i == 0) {
            var count = 0;
            while (B % i == 0) {
                B = B / i;
                count++;
            }

            ans.push([i, count]);
        }
    }
    return ans;
}

// Returns largest power of B that
// divides N!
function largestPowerOfB(N, B)
{
    var vec =[];
    vec = primeFactorsofB(B);
    var ans = Number.MAX_VALUE;
    for (var i = 0; i < vec.length; i++)

        // calculating minimum power of all
        // the prime factors of B
        ans = Math.min(ans, Math.floor(findPowerOfP(N,
        vec[i][0]) / vec[i][1]));

    return ans;
}

// Driver code
document.write(largestPowerOfB(5, 2) + "<br>");
document.write(largestPowerOfB(6, 9) + "<br>");

// This code is contributed by ShubhamSingh10

</script>
```

**Output:** 

```
3
1
```