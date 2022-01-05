# 给定数的第 N 个质因数

> 原文:[https://www . geesforgeks . org/n-th-给定数的质因数/](https://www.geeksforgeeks.org/n-th-prime-factor-of-a-given-number/)

给定由两个整数组成的 Q 个查询，一个是数字(1 <= number <= 10 <sup>6</sup> )另一个是 N，任务是找到给定数字的第 N 个质因数。
**例:**

> **输入:**查询数，Q = 4
> 数= 6，N = 1
> 数= 210，N = 3
> 数= 210，N = 2
> 数= 60，N = 2
> T7】输出:T9】2
> 5
> 3
> 3
> 6 有质因数 2 和 3。
> 210 有素因子 2、3、6。
> 60 有素因子 2 和 3。

一种简单的方法是分解每个数字并存储质因数。打印如此存储的第 N 个质因数。
**时间复杂度:**每个查询 O(log(n))。
一种**有效的方法**是预先计算数字的所有质因数，并将数字以排序顺序存储在[二维向量](https://www.geeksforgeeks.org/2d-vector-in-cpp-with-user-defined-size/)中。由于数量不会超过 10 <sup>6</sup> ，所以唯一质因数的数量最多在 7-8 左右(*因为 2 * 3 * 5 * 7 * 11 * 13 * 17 * 19>= 10<sup>6</sup>*)。一旦存储了号码，查询可以在 O(1)中回答，因为第 n-1 个<sup>索引将在第<sup>行中有答案。
以下是上述办法的实施:</sup></sup> 

## 卡片打印处理机（Card Print Processor 的缩写）

```
// C++ program to answer queries
// for N-th prime factor of a number
#include <bits/stdc++.h>
using namespace std;
const int N = 1000001;

// 2-D vector that stores prime factors
vector<int> v[N];

// Function to pre-store prime
// factors of all numbers till 10^6
void preprocess()
{
    // calculate unique prime factors for
    // every number till 10^6
    for (int i = 1; i < N; i++) {

        int num = i;

        // find prime factors
        for (int j = 2; j <= sqrt(num); j++) {
            if (num % j == 0) {

                // store if prime factor
                v[i].push_back(j);

                while (num % j == 0) {
                    num = num / j;
                }
            }
        }

        if(num>2)
        v[i].push_back(num);

    }
}

// Function that returns answer
// for every query
int query(int number, int n)
{
    return v[number][n - 1];
}

// Driver Code
int main()
{

    // Function to pre-store unique prime factors
    preprocess();

    // 1st query
    int number = 6, n = 1;
    cout << query(number, n) << endl;

    // 2nd query
    number = 210, n = 3;
    cout << query(number, n) << endl;

    // 3rd query
    number = 210, n = 2;
    cout << query(number, n) << endl;

    // 4th query
    number = 60, n = 2;
    cout << query(number, n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to answer queries
// for N-th prime factor of a number
import java.util.*;

class GFG
{

static int N = 1000001;

// 2-D vector that stores prime factors
static Vector<Integer> []v = new Vector[N];

// Function to pre-store prime
// factors of all numbers till 10^6
static void preprocess()
{
    // calculate unique prime factors for
    // every number till 10^6
    for (int i = 1; i < N; i++)
    {

        int num = i;

        // find prime factors
        for (int j = 2; j <= Math.sqrt(num); j++)
        {
            if (num % j == 0)
            {

                // store if prime factor
                v[i].add(j);

                while (num % j == 0)
                {
                    num = num / j;
                }
            }
        }
        if(num > 2)
        v[i].add(num);
    }
}

// Function that returns answer
// for every query
static int query(int number, int n)
{
    return v[number].get(n - 1);
}

// Driver Code
public static void main(String[] args)
{

    for (int i = 0; i < N; i++)
        v[i] = new Vector<Integer>();

    // Function to pre-store unique prime factors
    preprocess();

    // 1st query
    int number = 6, n = 1;
    System.out.print(query(number, n) +"\n");

    // 2nd query
    number = 210; n = 3;
    System.out.print(query(number, n) +"\n");

    // 3rd query
    number = 210; n = 2;
    System.out.print(query(number, n) +"\n");

    // 4th query
    number = 60; n = 2;
    System.out.print(query(number, n) +"\n");
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 program to answer queries
# for N-th prime factor of a number
from math import sqrt,ceil
N = 10001

# 2-D vector that stores prime factors
v = [[] for i in range(N)]

# Function to pre-store prime
# factors of all numbers till 10^6
def preprocess():

    # calculate unique prime factors for
    # every number till 10^6
    for i in range(1, N):

        num = i

        # find prime factors
        for j in range(2,ceil(sqrt(num)) + 1):
            if (num % j == 0):

                # store if prime factor
                v[i].append(j)

                while (num % j == 0):
                    num = num // j

        if(num > 2):
            v[i].append(num)

# Function that returns answer
# for every query
def query(number, n):
    return v[number][n - 1]

# Driver Code

# Function to pre-store unique prime factors
preprocess()

# 1st query
number = 6
n = 1
print(query(number, n))

# 2nd query
number = 210
n = 3
print(query(number, n))

# 3rd query
number = 210
n = 2
print(query(number, n))

# 4th query
number = 60
n = 2
print(query(number, n))

# This code is contributed by mohit kumar 29
```

## C#

```
// C# program to answer queries
// for N-th prime factor of a number
using System;
using System.Collections.Generic;

class GFG
{

static int N = 100001;

// 2-D vector that stores prime factors
static List<int> []v = new List<int>[N];

// Function to pre-store prime
// factors of all numbers till 10^6
static void preprocess()
{
    // calculate unique prime factors for
    // every number till 10^6
    for (int i = 1; i < N; i++)
    {

        int num = i;

        // find prime factors
        for (int j = 2; j <= Math.Sqrt(num); j++)
        {
            if (num % j == 0)
            {

                // store if prime factor
                v[i].Add(j);

                while (num % j == 0)
                {
                    num = num / j;
                }
            }
        }
        if(num > 2)
        v[i].Add(num);
    }
}

// Function that returns answer
// for every query
static int query(int number, int n)
{
    return v[number][n - 1];
}

// Driver Code
public static void Main(String[] args)
{

    for (int i = 0; i < N; i++)
        v[i] = new List<int>();

    // Function to pre-store unique prime factors
    preprocess();

    // 1st query
    int number = 6, n = 1;
    Console.Write(query(number, n) +"\n");

    // 2nd query
    number = 210; n = 3;
    Console.Write(query(number, n) +"\n");

    // 3rd query
    number = 210; n = 2;
    Console.Write(query(number, n) +"\n");

    // 4th query
    number = 60; n = 2;
    Console.Write(query(number, n) +"\n");
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// Javascript program to answer queries
// for N-th prime factor of a number
const N = 1000001;

// 2-D vector that stores prime factors
let v = new Array();

for (let i = 0; i < N; i++) {
    v.push(new Array())
}
// Function to pre-store prime
// factors of all numbers till 10^6
function preprocess()
{

    // calculate unique prime factors for
    // every number till 10^6
    for (let i = 1; i < N; i++) {

        let num = i;

        // find prime factors
        for (let j = 2; j <= Math.sqrt(num); j++) {
            if (num % j == 0) {

                // store if prime factor
                v[i].push(j);

                while (num % j == 0) {
                    num = num / j;
                }
            }
        }

        if (num > 2)
            v[i].push(num);

    }
}

// Function that returns answer
// for every query
function query(number, n) {
    return v[number][n - 1];
}

// Driver Code

// Function to pre-store unique prime factors
preprocess();

// 1st query
let number = 6, n = 1;
document.write(query(number, n) + "<br>");

// 2nd query
number = 210, n = 3;
document.write(query(number, n) + "<br>");

// 3rd query
number = 210, n = 2;
document.write(query(number, n) + "<br>");

// 4th query
number = 60, n = 2;
document.write(query(number, n) + "<br>");

// This code is contributed gfgking
</script>
```

**Output:** 

```
2
5
3
3
```

**时间复杂度:**每个查询 O(1)，预处理 O(maxN * log(maxN))，其中 maxN = 10 <sup>6</sup> 。
**辅助空间:最差情况下**O(N * 8)