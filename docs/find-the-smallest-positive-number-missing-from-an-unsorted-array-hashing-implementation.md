# 查找未排序数组中缺失的最小正数:哈希实现

> 原文:[https://www . geesforgeks . org/find-最小正数-从未排序数组中缺失-哈希-实现/](https://www.geeksforgeeks.org/find-the-smallest-positive-number-missing-from-an-unsorted-array-hashing-implementation/)

给定一个包含 0 的正负元素的未排序数组。任务是在 O(N)时间内找到数组中缺失的最小正数。
**例:**

```
Input: arr[] = {-5, 2, 0, -1, -10, 15}
Output: 1

Input: arr[] = {0, 1, 2, 3, 4, 5}
Output: 6

Input: arr[] = {1, 1, 1, 0, -1, -2}
Output: 2
```

我们可以用散列法来解决这个问题。这个想法是建立一个给定数组中所有正元素的哈希表。一旦哈希表建立。我们可以从 1 开始在哈希表中查找所有正整数。一旦我们找到哈希表中没有的数字，我们就返回它。
我们可以使用 C++ 中的[无序 _ 映射来实现散列，该散列允许以几乎 O(1)的时间复杂度执行查找操作。
以下是上述办法的实施:](https://www.geeksforgeeks.org/unordered_map-in-cpp-stl/) 

## C++

```
// C++ program to find the smallest
// positive missing number

#include <bits/stdc++.h>
using namespace std;

// Function to find the smallest positive
// missing number
int missingNumber(int a[], int n)
{
    // Declaring an unordered_map
    unordered_map<int, int> mp;

    // if array value is positive
    // store it in map
    for (int i = 0; i < n; i++) {
        if (a[i] > 0)
            mp[a[i]]++;
    }

    // index value set to 1
    int index = 1;

    // Return the first value starting
    // from 1 which does not exists in map
    while (1) {
        if (mp.find(index) == mp.end()) {
            return index;
        }

        index++;
    }
}

// Driver code
int main()
{
    int a[] = { 1, 1, 1, 0, -1, -2 };
    int size = sizeof(a) / sizeof(a[0]);

    cout << "Smallest positive missing number is : "
         << missingNumber(a, size) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to find the smallest
// positive missing number

import java.util.*;

class GFG
{

    // Function to find the smallest positive
    // missing number
    static int missingNumber(int a[], int n)
    {
        // Declaring an unordered_map
        Map<Integer, Integer> mp = new LinkedHashMap<>();

        // if array value is positive
        // store it in map
        for (int i = 0; i < n; i++)
        {
            if (a[i] > 0)
            {
                mp.put(a[i], mp.get(a[i]) == null ? 1 : mp.get(a[i]) + 1);
            }
        }

        // index value set to 1
        int index = 1;

        // Return the first value starting
        // from 1 which does not exists in map
        while (true)
        {
            if (!mp.containsKey(index))
            {
                return index;
            }

            index++;
        }
    }

    // Driver code
    public static void main(String[] args)
    {
        int a[] = {1, 1, 1, 0, -1, -2};
        int size = a.length;

        System.out.println("Smallest positive missing number is : "
                + missingNumber(a, size));
    }
}

// This code has been contributed by 29AjayKumar
```

## 蟒蛇 3

```
# Python3 program to find the smallest
# positive missing number

# Function to find the smallest positive
# missing number
def missingNumber(a, n) :

    # Declaring an unordered_map
    mp = dict();

    # if array value is positive
    # store it in map
    for i in range(n) :
        if (a[i] > 0) :
            if a[i] not in mp.keys() :
                mp[a[i]] = 0

            mp[a[i]] += 1

    # index value set to 1
    index = 1;

    # Return the first value starting
    # from 1 which does not exists in map
    while (1) :
        if (index not in mp.keys()) :
            return index;

        index += 1;

# Driver code
if __name__ == "__main__" :

    a = [ 1, 1, 1, 0, -1, -2 ];
    size = len(a);

    print("Smallest positive missing number is : ",missingNumber(a, size));

# This code is contributed by AnkitRai01
```

## C#

```
// C# program to find the smallest
// positive missing number
using System;
using System.Collections.Generic;

class GFG
{

    // Function to find the smallest positive
    // missing number
    static int missingNumber(int []a, int n)
    {
        // Declaring an unordered_map
        Dictionary<int,int> m = new Dictionary<int,int>();

        // if array value is positive
        // store it in map
        for (int i = 0; i < n; i++)
        {
            if (a[i] > 0)
            {
                if(m.ContainsKey(a[i]))
                {
                    var val = m[a[i]];
                    m.Remove(a[i]);
                    m.Add(a[i], val + 1);
                }
                else
                {
                    m.Add(a[i], 1);
                }
            }
        }

        // index value set to 1
        int index = 1;

        // Return the first value starting
        // from 1 which does not exists in map
        while (true)
        {
            if (!m.ContainsKey(index))
            {
                return index;
            }

            index++;
        }
    }

    // Driver code
    public static void Main(String[] args)
    {
        int []a = {1, 1, 1, 0, -1, -2};
        int size = a.Length;

        Console.WriteLine("Smallest positive missing number is : "
                + missingNumber(a, size));
    }
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// JavaScript program to find the smallest
// positive missing number

// Function to find the smallest positive
// missing number
function missingNumber(a, n) {
    // Declaring an unordered_map
    let mp = new Map();

    // if array value is positive
    // store it in map
    for (let i = 0; i < n; i++) {
        if (a[i] > 0) {
            mp[a[i]]++;
            if (mp.has(a[i])) {
                mp.set(a[i], mp.get(a[i]) + 1)
            } else {
                mp.set(a[i], 1)
            }
        }
    }

    // index value set to 1
    let index = 1;

    // Return the first value starting
    // from 1 which does not exists in map
    while (1) {
        if (!mp.has(index)) {
            return index;
        }

        index++;
    }
}

// Driver code

let a = [1, 1, 1, 0, -1, -2];
let size = a.length;

document.write("Smallest positive missing number is : " +
missingNumber(a, size) + "<br>");

// This code is contributed by gfgking

</script>
```

**Output:** 

```
Smallest positive missing number is : 2
```

**时间复杂度**:O(N)
T3】辅助空间 : O(N)