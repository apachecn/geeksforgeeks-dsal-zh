# 求使所有数组元素相等所需的最小运算次数

> 原文:[https://www . geesforgeks . org/find-使所有数组元素相等所需的最小操作数/](https://www.geeksforgeeks.org/find-the-minimum-number-of-operations-required-to-make-all-array-elements-equal/)

给定一个大小为 **N** 的数组 **arr[]** 。任务是通过应用以下操作的最小次数使所有数组元素相等:

1.  选择一对索引 **(i，j)** ，使得**| I–j | = 1**(索引 I 和 j 相邻)并设置**arr[I]= arr[I]+| arr[I]–arr[j]|**
2.  选择一对索引 **(i，j)** ，使得**| I–j | = 1**(索引 I 和 j 相邻)并设置**arr[I]= arr[I]–| arr[I]–arr[j]|**

**例:**

> **输入:** arr[] = { 2，4，6 }
> **输出:** 2
> 在给定数组上应用第二种类型的运算得到{ 2，2，6 }。
> 现在，在修改后的数组上再次应用第二类操作，得到{2，2，2}。
> **输入:** arr[] = { 1，1，1}
> **输出:** 0
> 所有数组元素已经相等。

**方法:**我们来找数组中最频繁的元素(使用[图](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)存储所有元素的频率)。让这个元素为 **x** 。如果我们更仔细地观察这些操作，我们可以看到这些操作的部分意味着**将元素 p 设置为元素 q** 。如果 **p < q** 则需要进行第一次操作，否则进行第二次操作。
现在，考虑最优答案中的运算次数。很明显，我们至少需要**n–freq(x)**运算来均衡所有元素。同样明显的是，我们总是可以用**n–freq(x)**这样的操作来完成，这是所需的最小操作数。
以下是上述方法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to return the minimum operations
// required to make all array elements equal
int minOperations(int arr[], int n)
{

    // To store the frequency
    // of all the array elements
    unordered_map<int, int> mp;

    // Traverse through array elements and
    // update frequencies
    for (int i = 0; i < n; i++)
        mp[arr[i]]++;

    // To store the maximum frequency
    // of an element from the array
    int maxFreq = INT_MIN;

    // Traverse through the map and find
    // the maximum frequency for any element
    for (auto x : mp)
        maxFreq = max(maxFreq, x.second);

    // Return the minimum operations required
    return (n - maxFreq);
}

// Driver code
int main()
{
    int arr[] = { 2, 4, 6 };
    int n = sizeof(arr) / sizeof(arr[0]);

    cout << minOperations(arr, n);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the above approach
import java.util.*;

class GFG
{

    // Function to return the minimum operations
    // required to make all array elements equal
    static int minOperations(int arr[], int n)
    {

        // To store the frequency
        // of all the array elements
        HashMap<Integer, Integer> mp = new HashMap<Integer, Integer>();

        // Traverse through array elements and
        // update frequencies
        for (int i = 0; i < n; i++)
        {
            if (mp.containsKey(arr[i]))
            {
                mp.put(arr[i], mp.get(arr[i]) + 1);
            }
            else
            {
                mp.put(arr[i], 1);
            }
        }

        // To store the maximum frequency
        // of an element from the array
        int maxFreq = Integer.MIN_VALUE;

        // Traverse through the map and find
        // the maximum frequency for any element
        maxFreq = Collections.max(mp.entrySet(),
                Comparator.comparingInt(Map.Entry::getKey)).getValue();

        // Return the minimum operations required
        return (n - maxFreq);
    }

    // Driver code
    public static void main(String[] args)
    {
        int arr[] = {2, 4, 6};
        int n = arr.length;
        System.out.println(minOperations(arr, n));
    }
}

/* This code contributed by PrinciRaj1992 */
```

## 蟒蛇 3

```
# Python3 implementation of the approach
import sys

# Function to return the minimum operations
# required to make all array elements equal
def minOperations(arr, n) :

    # To store the frequency
    # of all the array elements
    mp = dict.fromkeys(arr, 0);

    # Traverse through array elements and
    # update frequencies
    for i in range(n) :
        mp[arr[i]] += 1;

    # To store the maximum frequency
    # of an element from the array
    maxFreq = -(sys.maxsize - 1);

    # Traverse through the map and find
    # the maximum frequency for any element
    for key in mp :
        maxFreq = max(maxFreq, mp[key]);

    # Return the minimum operations required
    return (n - maxFreq);

# Driver code
if __name__ == "__main__" :

    arr = [ 2, 4, 6 ];
    n = len(arr) ;

    print(minOperations(arr, n));

# This code is contributed by Ryuga
```

## C#

```
// C# implementation of the above approach
using System;
using System.Linq;
using System.Collections.Generic;

class GFG
{

    // Function to return the minimum operations
    // required to make all array elements equal
    static int minOperations(int []arr, int n)
    {

        // To store the frequency
        // of all the array elements
        Dictionary<int,int> m = new Dictionary<int,int>();

        // Traverse through array elements and
        // update frequencies
        for (int i = 0; i < n; i++)
        {
            if(m.ContainsKey(arr[i]))
            {
                var val = m[arr[i]];
                m.Remove(arr[i]);
                m.Add(arr[i], val + 1);
            }
            else
            {
                m.Add(arr[i], 1);
            }    
        }

        // To store the maximum frequency
        // of an element from the array
        int maxFreq = int.MinValue;

        // Traverse through the map and find
        // the maximum frequency for any element
        maxFreq = m.Values.Max();

        // Return the minimum operations required
        return (n - maxFreq);
    }

    // Driver code
    public static void Main(String[] args)
    {
        int []arr = {2, 4, 6};
        int n = arr.Length;
        Console.WriteLine(minOperations(arr, n));
    }
}

// This code contributed by Rajput-Ji
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to return the minimum operations
// required to make all array elements equal
function minOperations(arr, n) {

    // To store the frequency
    // of all the array elements
    let mp = new Map();

    // Traverse through array elements and
    // update frequencies
    for (let i = 0; i < n; i++) {
        if (mp.has(arr[i])) {
            mp.set(arr[i], mp.get(arr[i]) + 1)
        } else {
            mp.set(arr[i], 1)
        }
    }

    // To store the maximum frequency
    // of an element from the array
    let maxFreq = Number.MIN_SAFE_INTEGER;

    // Traverse through the map and find
    // the maximum frequency for any element
    for (let x of mp)
        maxFreq = Math.max(maxFreq, x[1]);

    // Return the minimum operations required
    return (n - maxFreq);
}

// Driver code

let arr = [2, 4, 6];
let n = arr.length;

document.write(minOperations(arr, n));

// This code is contributed by _saurabh_jaiswal

</script>
```

**Output:** 

```
2
```