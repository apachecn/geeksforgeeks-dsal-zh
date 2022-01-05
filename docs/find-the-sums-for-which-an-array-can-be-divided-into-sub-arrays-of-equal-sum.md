# 求一个数组可以分成等份的子数组的和

> 原文:[https://www . geeksforgeeks . org/find-the-sum-for-a-array-in-sub-array-of-equal-sum/](https://www.geeksforgeeks.org/find-the-sums-for-which-an-array-can-be-divided-into-sub-arrays-of-equal-sum/)

给定一个整数数组 **arr[]** ，任务是找到 sum 的所有值，使得对于一个值 **sum[i]** ，该数组可以被分成等于 **sum[i]** 的 **sum** 的子数组。如果数组不能分成相等和的子数组，则打印 **-1** 。
**举例:**

> **输入:** arr[] = {2，2，2，1，1，2，2}
> **输出:** 2 4 6
> 数组可以分为和 2，4，6 的子数组。
> {2}、{2}、{2}、{1，1}、{2}和{2}
> {2，2}、{2，1，1}和{2，2}
> {2，2，2}和{1，1，2，2}
> **输入:** arr[] = {1，1，2}
> **输出:** 2
> 数组可以分为和 2 的子数组。
> {1，1}和{2}

**方法:**制作前缀和数组 **P[]** ，其中 **P[i]** 存储从索引 **0** 到 **i** 的元素和。总和 **S** 的除数只能是可能的子阵列总和。所以对于每个除数，如果除数的所有倍数直到总和 **S** 都存在于数组 **P[]** 中，那么这将是一个可能的子数组总和。将 **P[]** 的所有元素标记成[图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)为 **1** ，便于查找。所有除数都可以在 **sqrt(S)** 时间内检查。
以下是上述方法的实施:

## C++

```
// C++ program to find the sums for which an array
// can be divided into subarrays of equal sum.
#include <bits/stdc++.h>
using namespace std;

// Function to find the sums for which an array
// can be divided into subarrays of equal sum
void getSum(int a[], int n)
{
    int P[n];

    // Creating prefix sum array
    P[0] = a[0];
    for (int i = 1; i < n; i++)
        P[i] = a[i] + P[i - 1];

    // Total Sum
    int S = P[n - 1];

    // Initializing a Map for look-up
    map<int, int> hash;

    // Setting all the present sum as 1
    for (int i = 0; i < n; i++)
        hash[P[i]] = 1;

    // Set to store the subarray sum
    set<int> res;

    // Check the divisors of S
    for (int i = 1; i * i <= S; i++) {
        if (S % i == 0) {
            bool pres = true;

            int div1 = i, div2 = S / i;

            // Check if all multiples of div1 present or not
            for (int j = div1; j <= S; j += div1) {
                if (hash[j] != 1) {
                    pres = false;
                    break;
                }
            }

            // If all multiples are present
            if (pres and div1 != S)
                res.insert(div1);

            pres = true;

            // Check if all multiples of div2 present or not
            for (int j = S / i; j <= S; j += S / i) {
                if (hash[j] != 1) {
                    pres = false;
                    break;
                }
            }

            // If all multiples are present
            if (pres and div2 != S)
                res.insert(div2);
        }
    }

    // If array cannot be divided into
    // sub-arrays of equal sum
    if(res.size() == 0) {
        cout << "-1";
        return;
    }

    // Printing the results
    for (auto i : res)
        cout << i << " ";
}

// Driver code
int main()
{
    int a[] = { 1, 2, 1, 1, 1, 2, 1, 3 };

    int n = sizeof(a) / sizeof(a[0]);

    getSum(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the sums for which an array
// can be divided into subarrays of equal sum.
import java.util.HashMap;
import java.util.HashSet;

class GFG {

    // Function to find the sums for which an array
    // can be divided into subarrays of equal sum
    public static void getSum(int[] a, int n)
    {
        int[] P = new int[n];

        // Creating prefix sum array
        P[0] = a[0];
        for (int i = 1; i < n; i++)
            P[i] = a[i] + P[i - 1];

        // Total Sum
        int S = P[n - 1];

        HashMap<Integer, Integer> hash = new HashMap<>();

        // Setting all the present sum as 1
        for (int i = 0; i < n; i++)
            hash.put(P[i], 1);

        // Set to store the subarray sum
        HashSet<Integer> res = new HashSet<>();

        // Check the divisors of S
        for (int i = 1; i * i <= S; i++)
        {
            if (S % i == 0)
            {
                boolean pres = true;

                int div1 = i, div2 = S / i;

                // Check if all multiples of div1 present or not
                for (int j = div1; j <= S; j += div1)
                {
                    if (hash.get(j) == null || hash.get(j) != 1)
                    {
                        pres = false;
                        break;
                    }
                }

                // If all multiples are present
                if (pres && div1 != S)
                    res.add(div1);

                pres = true;

                // Check if all multiples of div2 present or not
                for (int j = S / i; j <= S; j += S / i)
                {
                    if (hash.get(j) == null || hash.get(j) != 1)
                    {
                        pres = false;
                        break;
                    }
                }

                // If all multiples are present
                if (pres && div2 != S)
                    res.add(div2);
            }
        }

        // If array cannot be divided into
        // sub-arrays of equal sum
        if (res.size() == 0)
        {
            System.out.println("-1");
            return;
        }

        // Printing the results
        for (int i : res)
            System.out.print(i + " ");
    }

    // Driver code
    public static void main(String[] args)
    {
        int[] a = { 1, 2, 1, 1, 1, 2, 1, 3 };
        int n = a.length;
        getSum(a, n);
    }
}

// This code is contributed by
// sanjeev2552
```

## 蟒蛇 3

```
# Python3 program to find the sums for
# which an array can be divided into
# subarrays of equal sum.

# from math lib import sqrt function
from math import sqrt

# Function to find the sums for which
# an array can be divided into subarrays
# of equal sum
def getSum(a, n) :

    P = [0] * n

    # Creating prefix sum array
    P[0] = a[0]
    for i in range(1, n) :
        P[i] = a[i] + P[i - 1]

    # Total Sum
    S = P[n - 1]

    # Initializing a Map for look-up
    hash = {}

    # Setting all the present sum as 1
    for i in range(n) :
        hash[P[i]] = 1

    # Set to store the subarray sum
    res = set()

    # Check the divisors of S
    for i in range(1, int(sqrt(S)) + 1) :
        if (S % i == 0) :
            pres = True;

            div1 = i
            div2 = S // i

            # Check if all multiples of
            # div1 present or not
            for j in range(div1 , S + 1, div1) :

                if j not in hash.keys() :
                    pres = False
                    break

            # If all multiples are present
            if (pres and div1 != S) :
                res.add(div1)

            pres = True

            # Check if all multiples of div2
            # present or not
            for j in range(S // i , S + 1 , S // i) :
                if j not in hash.keys():
                    pres = False;
                    break

            # If all multiples are present
            if (pres and div2 != S) :
                res.add(div2)

    # If array cannot be divided into
    # sub-arrays of equal sum
    if(len(res) == 0) :
        print("-1")
        return

    # Printing the results
    for i in res :
        print(i, end = " ")

# Driver code
if __name__ == "__main__" :

    a = [ 1, 2, 1, 1, 1, 2, 1, 3 ]

    n = len(a)

    getSum(a, n)

# This code is contributed by Ryuga
```

## C#

```
// C# program to find the sums for which
// an array can be divided into subarrays
// of equal sum.
using System;
using System.Collections.Generic;

class GFG
{

// Function to find the sums for which
// an array can be divided into subarrays
// of equal sum
public static void getSum(int[] a, int n)
{
    int[] P = new int[n];

    // Creating prefix sum array
    P[0] = a[0];
    for (int i = 1; i < n; i++)
        P[i] = a[i] + P[i - 1];

    // Total Sum
    int S = P[n - 1];

    Dictionary<int,
               int> hash = new Dictionary<int,
                                          int>();

    // Setting all the present sum as 1
    for (int i = 0; i < n; i++)
        if(!hash.ContainsKey(P[i]))
            hash.Add(P[i], 1);

    // Set to store the subarray sum
    HashSet<int> res = new HashSet<int>();

    // Check the divisors of S
    for (int i = 1; i * i <= S; i++)
    {
        if (S % i == 0)
        {
            Boolean pres = true;

            int div1 = i, div2 = S / i;

            // Check if all multiples of
            // div1 present or not
            for (int j = div1; j <= S; j += div1)
            {
                if (!hash.ContainsKey(j) ||
                     hash[j] != 1)
                {
                    pres = false;
                    break;
                }
            }

            // If all multiples are present
            if (pres && div1 != S)
                res.Add(div1);

            pres = true;

            // Check if all multiples of
            // div2 present or not
            for (int j = S / i;
                     j <= S; j += S / i)
            {
                if (hash[j] == 0 ||
                    hash[j] != 1)
                {
                    pres = false;
                    break;
                }
            }

            // If all multiples are present
            if (pres && div2 != S)
                res.Add(div2);
        }
    }

    // If array cannot be divided into
    // sub-arrays of equal sum
    if (res.Count == 0)
    {
        Console.WriteLine("-1");
        return;
    }

    // Printing the results
    foreach (int i in res)
        Console.Write(i + " ");
}

// Driver code
public static void Main(String[] args)
{
    int[] a = { 1, 2, 1, 1, 1, 2, 1, 3 };
    int n = a.Length;
    getSum(a, n);
}
}

// This code is contributed by PrinciRaj1992
```

## java 描述语言

```
<script>
// Javascript program to find the sums for which an array
// can be divided into subarrays of equal sum.

// Function to find the sums for which an array
// can be divided into subarrays of equal sum
function getSum(a, n) {
    let P = new Array(n);

    // Creating prefix sum array
    P[0] = a[0];
    for (let i = 1; i < n; i++)
        P[i] = a[i] + P[i - 1];

    // Total Sum
    let S = P[n - 1];

    // Initializing a Map for look-up
    let hash = new Map();

    // Setting all the present sum as 1
    for (let i = 0; i < n; i++)
        hash.set(P[i], 1);

    // Set to store the subarray sum
    let res = new Set();

    // Check the divisors of S
    for (let i = 1; i * i <= S; i++) {
        if (S % i == 0) {
            let pres = true;

            let div1 = i, div2 = Math.floor(S / i);

            // Check if all multiples of div1 present or not
            for (let j = div1; j <= S; j += div1) {
                if (hash.get(j) != 1) {
                    pres = false;
                    break;
                }
            }

            // If all multiples are present
            if (pres && div1 != S)
                res.add(div1);

            pres = true;

            // Check if all multiples of div2 present or not
            for (let j = Math.floor(S / i); j <= S; j += Math.floor(S / i)) {
                if (hash.get(j) != 1) {
                    pres = false;
                    break;
                }
            }

            // If all multiples are present
            if (pres && div2 != S)
                res.add(div2);
        }
    }

    // If array cannot be divided into
    // sub-arrays of equal sum
    if (res.size == 0) {
        document.write("-1");
        return;
    }

    res = [...res].sort((a, b) => a - b)

    // Printing the results
    for (let i of res)
        document.write(i + " ");
}

// Driver code
let a = [1, 2, 1, 1, 1, 2, 1, 3];
let n = a.length;
getSum(a, n);

// This code is contributed by gfgking.
</script>
```

**Output:** 

```
3 4 6
```