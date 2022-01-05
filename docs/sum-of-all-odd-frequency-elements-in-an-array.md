# 阵列中所有奇数频率元素的总和

> 原文:[https://www . geesforgeks . org/全奇数频率阵列元素总和/](https://www.geeksforgeeks.org/sum-of-all-odd-frequency-elements-in-an-array/)

给定包含重复元素的整数数组。任务是找出给定数组中所有奇数出现元素的和。这是数组中所有频率为奇数的元素的总和。

**例:**

```
Input : arr[] = {1, 1, 2, 2, 3, 3, 3}
Output : 9
The odd occurring element is 3, and it's number
of occurrence is 3\. Therefore sum of all 3's in the 
array = 9.

Input : arr[] = {10, 20, 30, 40, 40}
Output : 60
Elements with odd frequency are 10, 20 and 30.
Sum = 60.
```

**逼近** :

*   Traverse the array, and use [mapping in C++ to store the frequency of array elements, so that the key of mapping is array elements, and the value is its frequency in the array.](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)
*   Then, traverse the map to find the frequency of the element, check whether it is odd, and if it is odd, add this element to the sum.

下面是上述方法的实现:

## C++

```
// CPP program to find the sum of all odd
// occurring elements in an array

#include <bits/stdc++.h>
using namespace std;

// Function to find the sum of all odd
// occurring elements in an array
int findSum(int arr[], int N)
{
    // Store frequencies of elements
    // of the array
    unordered_map<int, int> mp;
    for (int i = 0; i < N; i++)
        mp[arr[i]]++;

    // variable to store sum of all
    // odd occurring elements
    int sum = 0;

    // loop to iterate through map
    for (auto itr = mp.begin(); itr != mp.end(); itr++) {

        // check if frequency is odd
        if (itr->second % 2 != 0)
            sum += (itr->first) * (itr->second);
    }

    return sum;
}

// Driver Code
int main()
{
    int arr[] = { 10, 20, 20, 10, 40, 40, 10 };

    int N = sizeof(arr) / sizeof(arr[0]);

    cout << findSum(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the sum of all odd
// occurring elements in an array
import java.util.*;

class GFG
{

// Function to find the sum of all odd
// occurring elements in an array
static int findSum(int arr[], int N)
{
    // Store frequencies of elements
    // of the array
    Map<Integer,Integer> mp = new HashMap<>();
    for (int i = 0; i < N; i++)
        mp.put(arr[i],mp.get(arr[i])==null?1:mp.get(arr[i])+1);

    // variable to store sum of all
    // odd occurring elements
    int sum = 0;

    // loop to iterate through map
    for (Map.Entry<Integer,Integer> entry : mp.entrySet())
    {

        // check if frequency is odd
        if (entry.getValue() % 2 != 0)
            sum += (entry.getKey()) * (entry.getValue());
    }

    return sum;
}

// Driver Code
public static void main(String args[])
{
    int arr[] = { 10, 20, 20, 10, 40, 40, 10 };

    int N = arr.length;

    System.out.println(findSum(arr, N));
}
}

/* This code is contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Function to find sum of all odd
# occurring elements in an array
import collections

def findsum(arr, N):

    # Store frequencies of elements
    # of an array in dictionary
    mp = collections.defaultdict(int)

    for i in range(N):
        mp[arr[i]] += 1

    # Variable to store sum of all
    # odd occurring elements
    sum = 0

    # loop to iterate through dictionary
    for i in mp:

        # Check if frequency is odd
        if (mp[i] % 2 != 0):
            sum += (i * mp[i])
    return sum

# Driver Code
arr = [ 10, 20, 20, 10, 40, 40, 10 ]

N = len(arr)

print (findsum(arr, N))

# This cde is contributed
# by HardeepSingh.            
```

## C#

```
// C# program to find the sum of all odd
// occurring elements in an array
using System;
using System.Collections.Generic;

class GFG
{
    // Function to find the sum of all odd
    // occurring elements in an array
    public static int findSum(int[] arr, int N)
    {

        // Store frequencies of elements
        // of the array
        Dictionary<int,
                   int> mp = new Dictionary<int,       
                                            int>();
        for (int i = 0; i < N; i++)
        {
            if (mp.ContainsKey(arr[i]))
                mp[arr[i]]++;
            else
                mp.Add(arr[i], 1);
        }

        // variable to store sum of all
        // odd occurring elements
        int sum = 0;

        // loop to iterate through map
        foreach (KeyValuePair<int,
                              int> entry in mp)
        {

            // check if frequency is odd
            if (entry.Value % 2 != 0)
                sum += entry.Key * entry.Value;
        }

        return sum;
    }

    // Driver code
    public static void Main(String[] args)
    {
        int[] arr = { 10, 20, 20, 10, 40, 40, 10 };
        int n = arr.Length;
        Console.WriteLine(findSum(arr, n));
    }
}

// This code is contributed by
// sanjeev2552
```

## java 描述语言

```
<script>
// Javascript program to find the sum of all odd
// occurring elements in an array

// Function to find the sum of all odd
// occurring elements in an array
function findSum(arr, N)
{

    // Store frequencies of elements
    // of the array
    let mp = new Map();
    for (let i = 0; i < N; i++) {
        if (mp.has(arr[i])) {
            mp.set(arr[i], mp.get(arr[i]) + 1)
        } else {
            mp.set(arr[i], 1)
        }
    }

    // variable to store sum of all
    // odd occurring elements
    let sum = 0;

    // loop to iterate through map
    for (let itr of mp) {

        // check if frequency is odd
        if (itr[1] % 2 != 0)
            sum += (itr[0]) * (itr[1]);
    }

    return sum;
}

// Driver Code
let arr = [10, 20, 20, 10, 40, 40, 10];
let N = arr.length
document.write(findSum(arr, N));

// This code is contributed by gfgking.
</script>
```

**Output:** 

```
30
```

**时间复杂度** : O(N)，其中 N 为数组中的元素个数。

**辅助空间:** O(N)

**方法二:使用 python 内置函数:**

*   Use [**counter**](https://www.geeksforgeeks.org/python-counter-objects-elements/) function.
*   Traverse the frequency dictionary, and multiply and sum all elements that appear odd times with their frequencies.

**下面是实现:**

## 蟒 3

```
# Python3 implementation of the above approach
from collections import Counter

def sumOdd(arr, n):

    # Counting frequency of every
    # element using Counter
    freq = Counter(arr)

    # Initializing sum 0
    sum = 0

    # Traverse the frequency and print all
    # sum all elements with odd frequency
    # multiplied by its frequency
    for it in freq:
        if freq[it] % 2 != 0:
            sum = sum + it*freq[it]
    print(sum)

# Driver code
arr = [10, 20, 30, 40, 40]
n = len(arr)

sumOdd(arr, n)

# This code is contributed by vikkycirus
```

**输出:**

```
60
```

**时间复杂度:** O(N)，其中 N 为数组中的元素个数。

**辅助空间:** O(N)