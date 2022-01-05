# 检查包含素数的数组的乘积是否为完美平方

> 原文:[https://www . geesforgeks . org/check-if-product-of-of-array-in-prime-numbers-is-a-perfect-square/](https://www.geeksforgeeks.org/check-if-product-of-array-containing-prime-numbers-is-a-perfect-square/)

给定一个只包含素数的数组 **arr[]** ，任务是检查数组元素的乘积是否是一个完美的正方形。
**例:**

> **输入:** arr[] = {2，2，7，7}
> **输出:**是
> 2 * 2 * 7 * 7 = 196 = 14<sup>2</sup>
> **输入:** arr[] = {3，3，5，5}
> **输出:**否

**天真的做法:**将数组的所有元素相乘，检查乘积是否是完美的正方形。
**高效的方法:**统计数组中所有元素的频率，如果所有元素的频率都是偶数那么产品将是一个完美的正方形否则打印编号
下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function that returns true if
// the product of all the array elements
// is a perfect square
bool isPerfectSquare(int arr[], int n)
{
    unordered_map<int, int> umap;

    // Update the frequencies of
    // all the array elements
    for (int i = 0; i < n; i++)
        umap[arr[i]]++;

    unordered_map<int, int>::iterator itr;
    for (itr = umap.begin(); itr != umap.end(); itr++)

        // If frequency of some element
        // in the array is odd
        if ((itr->second) % 2 == 1)
            return false;

    return true;
}

// Driver code
int main()
{
    int arr[] = { 2, 2, 7, 7 };
    int n = sizeof(arr) / sizeof(arr[0]);

    if (isPerfectSquare(arr, n))
        cout << "Yes";
    else
        cout << "No";

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{
    // Function that returns true if
    // the product of all the array elements
    // is a perfect square
    static boolean isPerfectSquare(int [] arr, int n)
    {

        HashMap<Integer, Integer> umap = new HashMap<>();

        // Update the frequencies of
        // all the array elements
        for (int i = 0; i < n; i++)
        {
            if(umap.containsKey(arr[i]))
                umap.put(arr[i], umap.get(arr[i]) + 1 );
            else
                umap.put(arr[i], 1);

        }

        Iterator<Map.Entry<Integer, Integer> >
                iterator = umap.entrySet().iterator();

        while(iterator.hasNext())
        {
            Map.Entry<Integer, Integer> entry = iterator.next();

            // If frequency of some element
            // in the array is odd
            if (entry.getValue() % 2 == 1)
                return false;
        }
        return true;
    }

    // Driver code
    public static void main (String[] args)
    {

        int arr [] = { 2, 2, 7, 7 };
        int n = arr.length;

        if (isPerfectSquare(arr, n))
            System.out.println("Yes");
        else
            System.out.println("No");
    }
}

// This code is contributed by ihritik
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function that returns true if
# the product of all the array elements
# is a perfect square
def isPerfectSquare(arr, n) :

    umap = dict.fromkeys(arr, n);

    # Update the frequencies of
    # all the array elements
    for key in arr :
        umap[key] += 1;

    for key in arr :

        # If frequency of some element
        # in the array is odd
        if (umap[key] % 2 == 1) :
            return False;

    return True;

# Driver code
if __name__ == "__main__" :

    arr = [ 2, 2, 7, 7 ];
    n = len(arr)

    if (isPerfectSquare(arr, n)) :
        print("Yes");
    else :
        print("No");

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{
    // Function that returns true if
    // the product of all the array elements
    // is a perfect square
    static bool isPerfectSquare(int [] arr, int n)
    {

        Dictionary<int, int> umap = new Dictionary<int, int>();

        // Update the frequencies of
        // all the array elements
        for (int i = 0; i < n; i++)
        {
            if(umap.ContainsKey(arr[i]))
                umap[arr[i]]++;
            else
                umap[arr[i]] = 1;

        }

        Dictionary<int, int>.ValueCollection valueColl =
                                                umap.Values;
        foreach(int val in valueColl)
        {
            // If frequency of some element
            // in the array is odd
            if (val % 2 == 1)
                return false;
        }
        return true;
    }

    // Driver code
    public static void Main ()
    {

        int [] arr = { 2, 2, 7, 7 };
        int n = arr.Length;

        if (isPerfectSquare(arr, n))
            Console.WriteLine("Yes");
        else
            Console.WriteLine("No");
    }
}

// This code is contributed by ihritik
```

## java 描述语言

```
<script>
// Javascript implementation of the approach

// Function that returns true if
// the product of all the array elements
// is a perfect square
function isPerfectSquare(arr, n)
{
    let umap = new Map();

    // Update the frequencies of
    // all the array elements
    for (let i = 0; i < n; i++){
        umap[arr[i]]++;
        if(umap.has(arr[i])){
            umap.set(arr[i], umap.get(arr[i]) + 1)
        }else{
            umap.set(arr[i], 1)
        }
    }

    for (let itr of umap)

        // If frequency of some element
        // in the array is odd
        if ((itr[1]) % 2 == 1)
            return false;

    return true;
}

// Driver code
    let arr = [ 2, 2, 7, 7 ];
    let n = arr.length;

    if (isPerfectSquare(arr, n))
        document.write("Yes");
    else
        document.write("No");

// This code is contributed by _saurabh_jaiswal
</script>
```

**Output:** 

```
Yes
```