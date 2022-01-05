# 前三项在 AP 中，后三项在 GP 中的四倍数

> 原文:[https://www . geesforgeks . org/四倍数量-前三个术语在 ap 中，后三个术语在 gp 中/](https://www.geeksforgeeks.org/number-of-quadruples-where-the-first-three-terms-are-in-ap-and-last-three-terms-are-in-gp/)

给定一个由 **N** 个整数组成的数组 **arr[]** 。任务是找到指数四倍 **(i，j，k，l)** 的数量，使得 **a[i]，a[j]和 a[k]** 在 **AP** 中， **a[j]，a[k]和 a[l]** 在 **GP** 中。所有的四足动物必须是不同的。
**举例:**

> **输入:** arr[] = {2，6，4，9，2}
> **输出:** 2
> 四元组中元素的索引为(0，2，1，3)和(4，2，1，3)，对应的四元组为(2，4，6，9)和(2，4，6，9)
> **输入:** arr[] = {1，1，1，1}
> **输出:** 24

一种**天真的方法**是使用四个嵌套循环来解决上述问题。检查前三个元素是否在 [AP](https://www.geeksforgeeks.org/progressions-ap-gp-hp/) 中，然后检查后三个元素是否在 [GP](https://www.geeksforgeeks.org/progressions-ap-gp-hp/) 中。如果这两个条件都满足，那么它们将计数增加 1。
**时间复杂度:** O(n <sup>4</sup> )
一种**高效的方法**就是使用[组合学](https://www.geeksforgeeks.org/combinatorics-gq/)来解决上述问题。首先记录每个数组元素出现的次数。运行两个嵌套循环，并将两个元素都视为第二个和第三个数字。因此，第一个元素将是**a[j]–(a[k]–a[j])**，如果是整数值，第四个元素将是 **a[k] * a[k] / a[j]** 。因此，使用这两个索引 j 和 k 的四倍数将是第一个数的计数*第四个数的计数，第二个和第三个元素是固定的。
以下是上述办法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the count of quadruples
int countQuadruples(int a[], int n)
{

    // Hash table to count the number of occurrences
    unordered_map<int, int> mpp;

    // Traverse and increment the count
    for (int i = 0; i < n; i++)
        mpp[a[i]]++;

    int count = 0;

    // Run two nested loop for second and third element
    for (int j = 0; j < n; j++) {
        for (int k = 0; k < n; k++) {

            // If they are same
            if (j == k)
                continue;

            // Initially decrease the count
            mpp[a[j]]--;
            mpp[a[k]]--;

            // Find the first element using common difference
            int first = a[j] - (a[k] - a[j]);

            // Find the fourth element using GP
            // y^2 = x * z property
            int fourth = (a[k] * a[k]) / a[j];

            // If it is an integer
            if ((a[k] * a[k]) % a[j] == 0) {

                // If not equal
                if (a[j] != a[k])
                    count += mpp[first] * mpp[fourth];

                // Same elements
                else
                    count += mpp[first] * (mpp[fourth] - 1);
            }

            // Later increase the value for
            // future calculations
            mpp[a[j]]++;
            mpp[a[k]]++;
        }
    }
    return count;
}

// Driver code
int main()
{
    int a[] = { 2, 6, 4, 9, 2 };
    int n = sizeof(a) / sizeof(a[0]);

    cout << countQuadruples(a, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

    // Function to return the count of quadruples
    static int countQuadruples(int a[], int n)
    {

        // Hash table to count the number of occurrences
        HashMap<Integer, Integer> mp = new HashMap<Integer, Integer>();

        // Traverse and increment the count
        for (int i = 0; i < n; i++)
            if (mp.containsKey(a[i]))
            {
                mp.put(a[i], mp.get(a[i]) + 1);
            }
            else
            {
                mp.put(a[i], 1);
            }

        int count = 0;

        // Run two nested loop for second and third element
        for (int j = 0; j < n; j++)
        {
            for (int k = 0; k < n; k++)
            {

                // If they are same
                if (j == k)
                    continue;

                // Initially decrease the count
                mp.put(a[j], mp.get(a[j]) - 1);
                mp.put(a[k], mp.get(a[k]) - 1);

                // Find the first element using common difference
                int first = a[j] - (a[k] - a[j]);

                // Find the fourth element using GP
                // y^2 = x * z property
                int fourth = (a[k] * a[k]) / a[j];

                // If it is an integer
                if ((a[k] * a[k]) % a[j] == 0)
                {

                    // If not equal
                    if (a[j] != a[k])
                    {
                        if (mp.containsKey(first) && mp.containsKey(fourth))
                            count += mp.get(first) * mp.get(fourth);
                    }

                    // Same elements
                    else if (mp.containsKey(first) && mp.containsKey(fourth))
                        count += mp.get(first) * (mp.get(fourth) - 1);
                }

                // Later increase the value for
                // future calculations
                if (mp.containsKey(a[j]))
                {
                    mp.put(a[j], mp.get(a[j]) + 1);
                }
                else
                {
                    mp.put(a[j], 1);
                }
                if (mp.containsKey(a[k]))
                {
                    mp.put(a[k], mp.get(a[k]) + 1);
                }
                else
                {
                    mp.put(a[k], 1);
                }
            }
        }
        return count;
    }

    // Driver code
    public static void main(String[] args)
    {
        int a[] = { 2, 6, 4, 9, 2 };
        int n = a.length;

        System.out.print(countQuadruples(a, n));
    }
}

// This code is contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the count of quadruples
def countQuadruples(a, n) :

    # Hash table to count the number
    # of occurrences
    mpp = dict.fromkeys(a, 0);

    # Traverse and increment the count
    for i in range(n) :
        mpp[a[i]] += 1;

    count = 0;

    # Run two nested loop for second
    # and third element
    for j in range(n) :
        for k in range(n) :

            # If they are same
            if (j == k) :
                continue;

            # Initially decrease the count
            mpp[a[j]] -= 1;
            mpp[a[k]] -= 1;

            # Find the first element using
            # common difference
            first = a[j] - (a[k] - a[j]);

            if first not in mpp :
                mpp[first] = 0;

            # Find the fourth element using
            # GP y^2 = x * z property
            fourth = (a[k] * a[k]) // a[j];

            if fourth not in mpp :
                mpp[fourth] = 0;

            # If it is an integer
            if ((a[k] * a[k]) % a[j] == 0) :

                # If not equal
                if (a[j] != a[k]) :
                    count += mpp[first] * mpp[fourth];

                # Same elements
                else :
                    count += (mpp[first] *
                             (mpp[fourth] - 1));

            # Later increase the value for
            # future calculations
            mpp[a[j]] += 1;
            mpp[a[k]] += 1;

    return count;

# Driver code
if __name__ == "__main__" :

    a = [ 2, 6, 4, 9, 2 ];
    n = len(a) ;

    print(countQuadruples(a, n));

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{

    // Function to return the count of quadruples
    static int countQuadruples(int []a, int n)
    {

        // Hash table to count the number of occurrences
        Dictionary<int, int> mp = new Dictionary<int, int>();

        // Traverse and increment the count
        for (int i = 0; i < n; i++)
            if (mp.ContainsKey(a[i]))
            {
                mp[a[i]] = mp[a[i]] + 1;
            }
            else
            {
                mp.Add(a[i], 1);
            }

        int count = 0;

        // Run two nested loop for second and third element
        for (int j = 0; j < n; j++)
        {
            for (int k = 0; k < n; k++)
            {

                // If they are same
                if (j == k)
                    continue;

                // Initially decrease the count
                mp[a[j]] = mp[a[j]] - 1;
                mp[a[k]] = mp[a[k]] - 1;

                // Find the first element using common difference
                int first = a[j] - (a[k] - a[j]);

                // Find the fourth element using GP
                // y^2 = x * z property
                int fourth = (a[k] * a[k]) / a[j];

                // If it is an integer
                if ((a[k] * a[k]) % a[j] == 0)
                {

                    // If not equal
                    if (a[j] != a[k])
                    {
                        if (mp.ContainsKey(first) && mp.ContainsKey(fourth))
                            count += mp[first] * mp[fourth];
                    }

                    // Same elements
                    else if (mp.ContainsKey(first) && mp.ContainsKey(fourth))
                        count += mp[first] * (mp[fourth] - 1);
                }

                // Later increase the value for
                // future calculations
                if (mp.ContainsKey(a[j]))
                {
                    mp[a[j]] = mp[a[j]] + 1;
                }
                else
                {
                    mp.Add(a[j], 1);
                }
                if (mp.ContainsKey(a[k]))
                {
                    mp[a[k]] = mp[a[k]] + 1;
                }
                else
                {
                    mp.Add(a[k], 1);
                }
            }
        }
        return count;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int []a = { 2, 6, 4, 9, 2 };
        int n = a.Length;

        Console.Write(countQuadruples(a, n));
    }
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

    // Function to return the count of quadruples
    function countQuadruples(a, n)
    {

        // Hash table to count the
        // number of occurrences
        let mp = new Map();

        // Traverse and increment the count
        for (let i = 0; i < n; i++)
            if (mp.has(a[i]))
            {
                mp.set(a[i], mp.get(a[i]) + 1);
            }
            else
            {
                mp.set(a[i], 1);
            }

        let count = 0;

        // Run two nested loop for second
        // and third element
        for (let j = 0; j < n; j++)
        {
            for (let k = 0; k < n; k++)
            {

                // If they are same
                if (j == k)
                    continue;

                // Initially decrease the count
                mp.set(a[j], mp.get(a[j]) - 1);
                mp.set(a[k], mp.get(a[k]) - 1);

                // Find the first element using
                // common difference
                let first = a[j] - (a[k] - a[j]);

                // Find the fourth element using GP
                // y^2 = x * z property
                let fourth = (a[k] * a[k]) / a[j];

                // If it is an leteger
                if ((a[k] * a[k]) % a[j] == 0)
                {

                    // If not equal
                    if (a[j] != a[k])
                    {
                        if (mp.has(first) && mp.has(fourth))
                            count +=
                            mp.get(first) * mp.get(fourth);
                    }

                    // Same elements
                    else if (mp.has(first) && mp.has(fourth))
                        count +=
                        mp.get(first) * (mp.get(fourth) - 1);
                }

                // Later increase the value for
                // future calculations
                if (mp.has(a[j]))
                {
                    mp.set(a[j], mp.get(a[j]) + 1);
                }
                else
                {
                    mp.set(a[j], 1);
                }
                if (mp.has(a[k]))
                {
                    mp.set(a[k], mp.get(a[k]) + 1);
                }
                else
                {
                    mp.set(a[k], 1);
                }
            }
        }
        return count;
    }

    // Driver code

    let a = [ 2, 6, 4, 9, 2 ];
        let n = a.length;

        document.write(countQuadruples(a, n));

</script>
```

**Output:** 

```
2
```

**时间复杂度:**O(N<sup>2</sup>)
T5】辅助空间: O(N)