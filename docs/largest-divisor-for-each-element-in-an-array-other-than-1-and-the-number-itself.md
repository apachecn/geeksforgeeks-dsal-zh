# 除 1 和数字本身以外的数组中每个元素的最大除数

> 原文:[https://www . geesforgeks . org/除 1 以外的数组中每个元素的最大除数和数字本身/](https://www.geeksforgeeks.org/largest-divisor-for-each-element-in-an-array-other-than-1-and-the-number-itself/)

给定一个由 **N** 个整数组成的数组 **arr[]** ，任务是找出数组中除 1 和数字本身以外的每个元素的最大除数。如果没有这样的除数，打印-1。

**示例:**

> **输入:** arr[] = {5，6，7，8，9，10}
> **输出:** -1 3 -1 4 3 5
> 除数(5) = {1，5}
> - >由于除了 1 和数本身之外没有除数，因此最大除数= -1
> 除数(6)=【1，2，3，6】
> ->除了 1 和数本身之外的最大除数= 3
> 除数 7]
> - >由于除了 1 和数本身没有除数，因此最大除数= -1
> 除数(8) = [1，2，4，8]
> - >除了 1 以外的最大除数和数本身= 4
> 除数(9) = [1，3，9]
> - >除了 1 以外的最大除数和数本身= 3
> 除数(10) = [1，2，5，10]
> 
> **输入:** arr[] = {15，16，17，18，19，20，21 }
> T3】输出: 5 8 -1 9 -1 10 7

**天真的方法:**想法是[迭代所有数组元素](https://www.geeksforgeeks.org/iterating-arrays-java/)，并使用本文[中讨论的方法找到每个元素的最大除数。
时间复杂度:O(N * √N)](https://www.geeksforgeeks.org/find-divisors-natural-number-set-1/)

**高效的方法:**更好的解决方法是预先计算从 2 到 10 的数字的最大除数 <sup>5</sup> 然后只运行一个数组的循环，打印预先计算好的答案。

*   使用厄拉多塞的[筛标记素数，并存储每个数的最小素数除数。](https://www.geeksforgeeks.org/sieve-of-eratosthenes/)
*   现在任何数的最大除数将是**数/最小 _ 质数除数**。
*   使用预计算答案找出每个数字的最大除数。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach

#include <bits/stdc++.h>
using namespace std;

#define int long long
const int maxin = 100001;

// Divisors array to keep track
// of the maximum divisor
int divisors[maxin];

// Function to pre-compute the prime
// numbers and largest divisors
void Calc_Max_Div(int arr[], int n)
{

    // Visited array to keep
    // track of prime numbers
    bool vis[maxin];
    memset(vis, 1, maxin);

    // 0 and 1 are not prime numbers
    vis[0] = vis[1] = 0;

    // Initialising divisors[i] = i
    for (int i = 1; i <= maxin; i++)
        divisors[i] = i;

    // For all the numbers divisible by 2
    // the maximum divisor will be number / 2
    for (int i = 4; i <= maxin; i += 2) {
        vis[i] = 0;
        divisors[i] = i / 2;
    }
    for (int i = 3; i <= maxin; i += 2) {

        // If divisors[i] is not equal to i then
        // this means that divisors[i] contains
        // minimum prime divisor for the number
        if (divisors[i] != i) {

            // Update the answer to
            // i / smallest_prime_divisor[i]
            divisors[i] = i / divisors[i];
        }

        // Condition if i is a prime number
        if (vis[i] == 1) {
            for (int j = i * i; j < maxin; j += i) {
                vis[j] = 0;

                // If divisors[j] is equal to j then
                // this means that i is the first prime
                // divisor for j so we update divi[j] = i
                if (divisors[j] == j)
                    divisors[j] = i;
            }
        }
    }

    for (int i = 0; i < n; i++) {

        // If the current element is prime
        // then it has no divisors
        // other than 1 and itself
        if (divisors[arr[i]] == arr[i])
            cout << "-1 ";
        else
            cout << divisors[arr[i]] << " ";
    }
}

// Driver code
int32_t main()
{
    int arr[] = { 5, 6, 7, 8, 9, 10 };
    int n = sizeof(arr) / sizeof(int);

    Calc_Max_Div(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
class GFG
{

    final static int maxin = 10001;

    // Divisors array to keep track
    // of the maximum divisor
    static int divisors[] = new int[maxin + 1];

    // Function to pre-compute the prime
    // numbers and largest divisors
    static void Calc_Max_Div(int arr[], int n)
    {

        // Visited array to keep
        // track of prime numbers
        int vis[] = new int[maxin + 1];

        for(int i = 0;i <maxin+1 ; i++)
            vis[i] = 1;

        // 0 and 1 are not prime numbers
        vis[0] = vis[1] = 0;

        // Initialising divisors[i] = i
        for (int i = 1; i <= maxin; i++)
            divisors[i] = i;

        // For all the numbers divisible by 2
        // the maximum divisor will be number / 2
        for (int i = 4; i <= maxin; i += 2)
        {
            vis[i] = 0;
            divisors[i] = i / 2;
        }
        for (int i = 3; i <= maxin; i += 2)
        {

            // If divisors[i] is not equal to i then
            // this means that divisors[i] contains
            // minimum prime divisor for the number
            if (divisors[i] != i)
            {

                // Update the answer to
                // i / smallest_prime_divisor[i]
                divisors[i] = i / divisors[i];
            }

            // Condition if i is a prime number
            if (vis[i] == 1)
            {
                for (int j = i * i; j < maxin; j += i)
                {
                    vis[j] = 0;

                    // If divisors[j] is equal to j then
                    // this means that i is the first prime
                    // divisor for j so we update divi[j] = i
                    if (divisors[j] == j)
                        divisors[j] = i;
                }
            }
        }

        for (int i = 0; i < n; i++)
        {

            // If the current element is prime
            // then it has no divisors
            // other than 1 and itself
            if (divisors[arr[i]] == arr[i])
                    System.out.print("-1 ");
            else
                    System.out.print(divisors[arr[i]] + " ");
        }
    }

    // Driver code
    public static void main (String[] args)
    {
        int []arr = { 5, 6, 7, 8, 9, 10 };
        int n = arr.length;

        Calc_Max_Div(arr, n);
    }
}

// This code is contributed by AnkitRai01
```

## 蟒蛇 3

```
# Python3 implementation of the approach
maxin = 100001;

# Divisors array to keep track
# of the maximum divisor
divisors = [0] * (maxin + 1);

# Function to pre-compute the prime
# numbers and largest divisors
def Calc_Max_Div(arr, n) :

    # Visited array to keep
    # track of prime numbers
    vis = [1] * (maxin + 1);

    # 0 and 1 are not prime numbers
    vis[0] = vis[1] = 0;

    # Initialising divisors[i] = i
    for i in range(1, maxin + 1) :
        divisors[i] = i;

    # For all the numbers divisible by 2
    # the maximum divisor will be number / 2
    for i in range(4 , maxin + 1, 2) :
        vis[i] = 0;
        divisors[i] = i // 2;

    for i in range(3, maxin + 1, 2) :

        # If divisors[i] is not equal to i then
        # this means that divisors[i] contains
        # minimum prime divisor for the number
        if (divisors[i] != i) :

            # Update the answer to
            # i / smallest_prime_divisor[i]
            divisors[i] = i // divisors[i];

        # Condition if i is a prime number
        if (vis[i] == 1) :
            for j in range( i * i, maxin, i) :
                vis[j] = 0;

                # If divisors[j] is equal to j then
                # this means that i is the first prime
                # divisor for j so we update divi[j] = i
                if (divisors[j] == j) :
                    divisors[j] = i;

    for i in range(n) :

        # If the current element is prime
        # then it has no divisors
        # other than 1 and itself
        if (divisors[arr[i]] == arr[i]) :
            print("-1 ", end = "");
        else :
            print(divisors[arr[i]], end = " ");

# Driver code
if __name__ == "__main__" :

    arr = [ 5, 6, 7, 8, 9, 10 ];
    n = len(arr);

    Calc_Max_Div(arr, n);

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;

class GFG
{

    static int maxin = 10001;

    // Divisors array to keep track
    // of the maximum divisor
    static int []divisors = new int[maxin + 1];

    // Function to pre-compute the prime
    // numbers and largest divisors
    static void Calc_Max_Div(int []arr, int n)
    {

        // Visited array to keep
        // track of prime numbers
        int []vis = new int[maxin + 1];

        for(int i = 0; i < maxin + 1 ; i++)
            vis[i] = 1;

        // 0 and 1 are not prime numbers
        vis[0] = vis[1] = 0;

        // Initialising divisors[i] = i
        for (int i = 1; i <= maxin; i++)
            divisors[i] = i;

        // For all the numbers divisible by 2
        // the maximum divisor will be number / 2
        for (int i = 4; i <= maxin; i += 2)
        {
            vis[i] = 0;
            divisors[i] = i / 2;
        }
        for (int i = 3; i <= maxin; i += 2)
        {

            // If divisors[i] is not equal to i then
            // this means that divisors[i] contains
            // minimum prime divisor for the number
            if (divisors[i] != i)
            {

                // Update the answer to
                // i / smallest_prime_divisor[i]
                divisors[i] = i / divisors[i];
            }

            // Condition if i is a prime number
            if (vis[i] == 1)
            {
                for (int j = i * i; j < maxin; j += i)
                {
                    vis[j] = 0;

                    // If divisors[j] is equal to j then
                    // this means that i is the first prime
                    // divisor for j so we update divi[j] = i
                    if (divisors[j] == j)
                        divisors[j] = i;
                }
            }
        }

        for (int i = 0; i < n; i++)
        {

            // If the current element is prime
            // then it has no divisors
            // other than 1 and itself
            if (divisors[arr[i]] == arr[i])
                    Console.Write("-1 ");
            else
                    Console.Write(divisors[arr[i]] + " ");
        }
    }

    // Driver code
    public static void Main()
    {
        int []arr = { 5, 6, 7, 8, 9, 10 };
        int n = arr.Length;

        Calc_Max_Div(arr, n);
    }
}

// This code is contributed by AnkitRai01
```

## java 描述语言

```
<script>

// Javascript implementation of the approach
var maxin = 100001;

// Divisors array to keep track
// of the maximum divisor
var divisors = Array(maxin).fill(0);

// Function to pre-compute the prime
// numbers and largest divisors
function Calc_Max_Div(arr, n)
{

    // Visited array to keep
    // track of prime numbers
    var vis = Array(maxin).fill(1);

    // 0 and 1 are not prime numbers
    vis[0] = vis[1] = 0;

    var i,j;

    // Initialising divisors[i] = i
    for(i = 1; i <= maxin; i++)
        divisors[i] = i;

    // For all the numbers divisible by 2
    // the maximum divisor will be number / 2
    for(i = 4; i <= maxin; i += 2)
    {
        vis[i] = 0;
        divisors[i] = i / 2;
    }
    for(i = 3; i <= maxin; i += 2)
    {

        // If divisors[i] is not equal to i then
        // this means that divisors[i] contains
        // minimum prime divisor for the number
        if (divisors[i] != i)
        {

            // Update the answer to
            // i / smallest_prime_divisor[i]
            divisors[i] = i / divisors[i];
        }

        // Condition if i is a prime number
        if (vis[i] == 1)
        {
            for(j = i * i; j < maxin; j += i)
            {
                vis[j] = 0;

                // If divisors[j] is equal to j then
                // this means that i is the first prime
                // divisor for j so we update divi[j] = i
                if (divisors[j] == j)
                    divisors[j] = i;
            }
        }
    }

    for(i = 0; i < n; i++)
    {

        // If the current element is prime
        // then it has no divisors
        // other than 1 and itself
        if (divisors[arr[i]] == arr[i])
            document.write("-1 ");
        else
            document.write(divisors[arr[i]] + " ");
    }
}

// Driver code
var arr = [ 5, 6, 7, 8, 9, 10 ];
var n = arr.length;

Calc_Max_Div(arr, n);

// This code is contributed by bgangwar59

</script>
```

**Output:** 

```
-1 3 -1 4 3 5
```

时间复杂度:O(N)