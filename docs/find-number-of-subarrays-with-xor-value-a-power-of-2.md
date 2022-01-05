# 求异或值为 2 次方的子阵个数

> 原文:[https://www . geeksforgeeks . org/find-子阵数-异或-值-2 的幂/](https://www.geeksforgeeks.org/find-number-of-subarrays-with-xor-value-a-power-of-2/)

给定一个整数数组，arr[]的大小为 n。arr[]的任何子数组的异或值定义为该子数组中所有整数的异或。任务是找到异或值为 2 次方的子阵列数量。(1, 2, 4, 8, 16, ….)
**例:**

```
Input :  arr[] = {2, 6, 7, 5, 8}
Output : 6
Subarrays : {2, 6}, {2}, {6, 7},  {6, 7, 5}, {7, 5}, {8}

Input : arr[] = {2, 4, 8, 16} 
Output : 4 
```

**接近** :

1.  维护一个存储所有前缀异或值及其计数的散列表。
2.  在任何索引 I 处，我们需要找到以 I 结尾且异或值为 2 次方的子阵列的数量。我们需要为 2 的所有幂找到可能的子阵数量。比如说。:假设当前 XOR 值直到索引 I 为 x，我们需要找到导致 16(比如 s)的子阵列的数量，因此我们需要前缀 XOR Y 的计数，以便可以使用哈希映射找到(X^Y) = S 或 Y = S^X. Y。
3.  执行步骤 2，对于所有索引，添加输出。

以下是上述方法的实现:

## C++

```
// C++ Program to count number of subarrays
// with Bitwise-XOR as power of 2

#include <bits/stdc++.h>
#define ll long long int
#define MAX 10
using namespace std;

// Function to find number of subarrays
int findSubarray(int array[], int n)
{
    // Hash Map to store prefix XOR values
    unordered_map<int, int> mp;

    // When no element is selected
    mp.insert({ 0, 1 });

    int answer = 0;
    int preXor = 0;
    for (int i = 0; i < n; i++) {
        int value = 1;
        preXor ^= array[i];

        // Check for all the powers of 2,
        // till a MAX value
        for (int j = 1; j <= MAX; j++) {
            int Y = value ^ preXor;
            if (mp.find(Y) != mp.end()) {
                answer += mp[Y];
            }
            value *= 2;
        }

        // Insert Current prefixxor in Hash Map
        if (mp.find(preXor) != mp.end()) {
            mp[preXor]++;
        }
        else {
            mp.insert({ preXor, 1 });
        }
    }

    return answer;
}

// Driver Code
int main()
{
    int array[] = { 2, 6, 7, 5, 8 };

    int n = sizeof(array) / sizeof(array[0]);

    cout << findSubarray(array, n) << endl;

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java Program to count number of subarrays
// with Bitwise-XOR as power of 2
import java.util.*;

class GFG
{

static int MAX = 10;

// Function to find number of subarrays
static int findSubarray(int array[], int n)
{
    // Hash Map to store prefix XOR values
    HashMap<Integer,
            Integer> mp = new HashMap<Integer,
                                      Integer>();

    // When no element is selected
    mp.put(0, 1);

    int answer = 0;
    int preXor = 0;
    for (int i = 0; i < n; i++)
    {
        int value = 1;
        preXor ^= array[i];

        // Check for all the powers of 2,
        // till a MAX value
        for (int j = 1; j <= MAX; j++)
        {
            int Y = value ^ preXor;
            if (mp.containsKey(Y))
            {
                answer += mp.get(Y);
            }
            value *= 2;
        }

        // Insert Current prefixxor in Hash Map
        if (mp.containsKey(preXor))
        {
            mp.put(preXor,mp.get(preXor) + 1);
        }
        else
        {
            mp.put(preXor, 1);
        }
    }
    return answer;
}

// Driver Code
public static void main (String[] args)
{
    int array[] = { 2, 6, 7, 5, 8 };

    int n = array.length;

    System.out.println(findSubarray(array, n));
}
}

// This code is contributed by PrinciRaj1992
```

## 蟒蛇 3

```
# Python3 Program to count number of subarrays
# with Bitwise-XOR as power of 2
MAX = 10

# Function to find number of subarrays
def findSubarray(array, n):

    # Hash Map to store prefix XOR values
    mp = dict()

    # When no element is selected
    mp[0] = 1

    answer = 0
    preXor = 0
    for i in range(n):
        value = 1
        preXor ^= array[i]

        # Check for all the powers of 2,
        # till a MAX value
        for j in range(1, MAX + 1):
            Y = value ^ preXor
            if ( Y in mp.keys()):
                answer += mp[Y]

            value *= 2

        # Insert Current prefixxor in Hash Map
        if (preXor in mp.keys()):
            mp[preXor] += 1

        else:
            mp[preXor] = 1

    return answer

# Driver Code
array = [2, 6, 7, 5, 8]

n = len(array)

print(findSubarray(array, n))

# This code is contributed by Mohit Kumar
```

## C#

```
// C# Program to count number of subarrays
// with Bitwise-XOR as power of 2
using System;
using System.Collections.Generic;

class GFG
{
static int MAX = 10;

// Function to find number of subarrays
static int findSubarray(int []array, int n)
{
    // Hash Map to store prefix XOR values
    Dictionary<int,
               int> mp = new Dictionary<int,
                                        int>();

    // When no element is selected
    mp.Add(0, 1);

    int answer = 0;
    int preXor = 0;
    for (int i = 0; i < n; i++)
    {
        int value = 1;
        preXor ^= array[i];

        // Check for all the powers of 2,
        // till a MAX value
        for (int j = 1; j <= MAX; j++)
        {
            int Y = value ^ preXor;
            if (mp.ContainsKey(Y))
            {
                answer += mp[Y];
            }
            value *= 2;
        }

        // Insert Current prefixxor in Hash Map
        if (mp.ContainsKey(preXor))
        {
            mp[preXor] = mp[preXor] + 1;
        }
        else
        {
            mp.Add(preXor, 1);
        }
    }
    return answer;
}

// Driver Code
public static void Main (String[] args)
{
    int []array = { 2, 6, 7, 5, 8 };

    int n = array.Length;

    Console.WriteLine(findSubarray(array, n));
}
}

// This code is contributed by 29AjayKumar
```

## java 描述语言

```
<script>

// Javascript Program to count number of subarrays
// with Bitwise-XOR as power of 2

var MAX = 10;

// Function to find number of subarrays
function findSubarray(array, n)
{
    // Hash Map to store prefix XOR values
    var mp = new Map();

    // When no element is selected
    mp.set(0,1);

    var answer = 0;
    var preXor = 0;
    for (var i = 0; i < n; i++) {
        var value = 1;
        preXor ^= array[i];

        // Check for all the powers of 2,
        // till a MAX value
        for (var j = 1; j <= MAX; j++) {
            var Y = value ^ preXor;
            if (mp.has(Y)) {
                answer += mp.get(Y);
            }
            value *= 2;
        }

        // Insert Current prefixxor in Hash Map
        if (mp.has(preXor)) {
            mp.set(preXor, mp.get(preXor)+1);
        }
        else {
            mp.set(preXor,1);
        }
    }

    return answer;
}

// Driver Code
var array = [2, 6, 7, 5, 8 ];
var n = array.length;
document.write( findSubarray(array, n));

</script>
```

**Output:** 

```
6
```

时间复杂度:0(n * MAX)

辅助空间:O(n)