# 奇数频率元素的逐位异或

> 原文:[https://www . geeksforgeeks . org/按位异或具有奇数频率的元素/](https://www.geeksforgeeks.org/bitwise-xor-of-elements-having-odd-frequency/)

给定一个由 **N** 个元素组成的数组 **arr[]** ，任务是找出在数组中出现奇数次的元素的异或。
**例:**

> **输入:** arr[] = {1，2，1，3，3，4，2，3，1}
> **输出:** 6
> 奇数频率的元素为 1，3，4。
> 和(1 ^ 3 ^ 4) = 6
> 
> **输入:** arr[] = {2，2，7，8，7}
> 输出: 8

**天真方法:**遍历数组，将所有元素的频率存储在[无序 _ 地图](https://www.geeksforgeeks.org/unordered_map-in-stl-and-its-applications/)中。现在，使用上一步创建的映射计算奇数频率元素的异或。

下面是上述方法的实现:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the xor of
// elements having odd frequency
int xorOdd(int arr[], int n)
{
    // To store the frequency
    // of all the elements
    unordered_map<int, int> m;

    // Update the map with the
    // frequency of the elements
    for (int i = 0; i < n; i++)
        m[arr[i]]++;

    // To store the XOR of the elements
    // appearing odd number of
    // times in the array
    int xorArr = 0;

    // Traverse the map using an iterator
    for (auto it = m.begin(); it != m.end(); it++) {

        // Check for odd frequency
        // and update the xor
        if ((it->second) & 1) {
            xorArr ^= it->first;
        }
    }

    return xorArr;
}

// Driver code
int main()
{
    int arr[] = { 1, 2, 1, 3, 3, 4, 2, 3, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << xorOdd(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{

// Function to return the xor of
// elements having odd frequency
static int xorOdd(int arr[], int n)
{
    // To store the frequency
    // of all the elements
    HashMap<Integer,
            Integer> mp = new HashMap<Integer,
                                      Integer>();

    // Update the map with the
    // frequency of the elements
    for (int i = 0 ; i < n; i++)
    {
        if(mp.containsKey(arr[i]))
        {
            mp.put(arr[i], mp.get(arr[i]) + 1);
        }
        else
        {
            mp.put(arr[i], 1);
        }
    }

    // To store the XOR of the elements
    // appearing odd number of
    // times in the array
    int xorArr = 0;

    // Traverse the map using an iterator
    for (Map.Entry<Integer,
                   Integer> it : mp.entrySet())
    {
        // Check for odd frequency
        // and update the xor
        if (((it.getValue()) % 2) ==1)
        {
            xorArr ^= it.getKey();
        }
    }
    return xorArr;
}

// Driver code
public static void main(String[] args)
{
    int arr[] = { 1, 2, 1, 3, 3, 4, 2, 3, 1 };
    int n = arr.length;

    System.out.println(xorOdd(arr, n));
}
}

// This code contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 implementation of the approach

# Function to return the xor of
# elements having odd frequency
def xorOdd(arr, n) :

    # To store the frequency
    # of all the elements
    m = dict.fromkeys(arr, 0);

    # Update the map with the
    # frequency of the elements
    for i in range(n) :
        m[arr[i]] += 1;

    # To store the XOR of the elements
    # appearing odd number of
    # times in the array
    xorArr = 0;

    # Traverse the map using an iterator
    for key,value in m.items() :

        # Check for odd frequency
        # and update the xor
        if (value & 1) :
            xorArr ^= key;

    return xorArr;

# Driver code
if __name__ == "__main__" :

    arr = [ 1, 2, 1, 3, 3, 4, 2, 3, 1 ];
    n = len(arr);

    print(xorOdd(arr, n));

# This code is contributed by AnkitRai01
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;                

class GFG
{

// Function to return the xor of
// elements having odd frequency
static int xorOdd(int []arr, int n)
{
    // To store the frequency
    // of all the elements
    Dictionary<int,
               int> mp = new Dictionary<int,
                                        int>();

    // Update the map with the
    // frequency of the elements
    for (int i = 0 ; i < n; i++)
    {
        if(mp.ContainsKey(arr[i]))
        {
            mp[arr[i]] = mp[arr[i]] + 1;
        }
        else
        {
            mp.Add(arr[i], 1);
        }
    }

    // To store the XOR of the elements
    // appearing odd number of
    // times in the array
    int xorArr = 0;

    // Traverse the map using an iterator
    foreach(KeyValuePair<int, int> it in mp)
    {
        // Check for odd frequency
        // and update the xor
        if (((it.Value) % 2) == 1)
        {
            xorArr ^= it.Key;
        }
    }
    return xorArr;
}

// Driver code
public static void Main(String[] args)
{
    int []arr = { 1, 2, 1, 3, 3, 4, 2, 3, 1 };
    int n = arr.Length;

    Console.WriteLine(xorOdd(arr, n));
    }
}

// This code is contributed by Princi Singh
```

## java 描述语言

```
<script>

// Javascript implementation of the approach

// Function to return the xor of
// elements having odd frequency
function xorOdd(arr, n)
{

    // To store the frequency
    // of all the elements
    let mp = new Map();

    // Update the map with the
    // frequency of the elements
    for(let i = 0 ; i < n; i++)
    {
        if (mp.has(arr[i]))
        {
            mp.set(arr[i], mp.get(arr[i]) + 1);
        }
        else
        {
            mp.set(arr[i], 1);
        }
    }

    // To store the XOR of the elements
    // appearing odd number of
    // times in the array
    let xorArr = 0;

    // Traverse the map using an iterator
    for(let [key, value] of mp.entries())
    {

        // Check for odd frequency
        // and update the xor
        if (((value) % 2) == 1)
        {
            xorArr ^= key;
        }
    }
    return xorArr;
}

// Driver code
let arr = [ 1, 2, 1, 3, 3, 4, 2, 3, 1 ];
let n = arr.length;

document.write(xorOdd(arr, n));

// This code is contributed by rag2127

</script>
```

**Output:** 

```
6
```

这个解决方案需要 O(n)个时间和 O(n)个空间。

**有效方法:**
这种方法使用 XOR 的两个重要属性——^ a = 0 和 0 ^ a = a。对数组中的所有元素进行 XOR。结果将是出现奇数次的数字的异或，因为出现偶数次的元素最终会相互抵消。

## C++

```
// C++ program to implement
// the above approach
#include<bits/stdc++.h>
using namespace std;

int xorOdd(int arr[], int n) {
    // initialise result as 0
    int result = 0;

    // take XOR of all elements
    for (int i = 0; i < n; ++i) {
        result ^= arr[i];
    }

     // return result
    return result;
}

// Driver code
int main() {
    int arr[] = { 1, 2, 1, 3, 3, 4, 2, 3, 1 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << xorOdd(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java program to implement
// the above approach
import java.io.*;

class GFG{

static int xorOdd(int arr[], int n)
{

    // Initialise result as 0
    int result = 0;

    // Take XOR of all elements
    for(int i = 0; i < n; ++i)
    {
        result ^= arr[i];
    }

    // Return result
    return result;
}

// Driver code
public static void main (String[] args)
{
    int arr[] = { 1, 2, 1, 3, 3,
                  4, 2, 3, 1 };
    int n = arr.length;

    System.out.println(xorOdd(arr, n));
}
}

// This code is contributed by math_lover
```

## 蟒蛇 3

```
# Python3 program to implement
# the above approach
def xorOdd(arr, n):

    # Initialise result as 0
    result = 0

    # Take XOR of all elements
    for i in range (n):
        result ^= arr[i]

     # Return result
    return result

# Driver code
if __name__ == "__main__":

    arr = [1, 2, 1, 3, 3,
           4, 2, 3, 1]
    n = len(arr) 
    print( xorOdd(arr, n))

# This code is contributed by Chitranayal
```

## C#

```
// C# program to implement
// the above approach
using System;

class GFG {

    static int xorOdd(int[] arr, int n)
    {

        // Initialise result as 0
        int result = 0;

        // Take XOR of all elements
        for (int i = 0; i < n; ++i) {
            result ^= arr[i];
        }

        // Return result
        return result;
    }

    // Driver code
    public static void Main()
    {
        int[] arr = { 1, 2, 1, 3, 3, 4, 2, 3, 1 };
        int n = arr.Length;

        Console.Write(xorOdd(arr, n));
    }
}

// This code is contributed by rishavmahato348.
```

## java 描述语言

```
<script>
// Javascript program to implement
// the above approach

function xorOdd(arr, n) {
    // initialise result as 0
    let result = 0;

    // take XOR of all elements
    for (let i = 0; i < n; ++i) {
        result ^= arr[i];
    }

     // return result
    return result;
}

// Driver code
    let arr = [ 1, 2, 1, 3, 3, 4, 2, 3, 1 ];
    let n = arr.length;

    document.write(xorOdd(arr, n));

</script>
```

**Output:** 

```
6
```

这个解决方案需要 O(n)个时间和 O(1)个空间。