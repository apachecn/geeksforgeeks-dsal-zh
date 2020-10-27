# 计算具有给定 XOR 的子数组的数量

给定一个整数数组 arr []和一个数 m，将其元素具有 XOR 的子数组的数量计为 m。
**示例**：[

```
Input : arr[] = {4, 2, 2, 6, 4}, m = 6
Output : 4
Explanation : The subarrays having XOR of 
              their elements as 6 are {4, 2}, 
              {4, 2, 2, 6, 4}, {2, 2, 6},
               and {6}

Input : arr[] = {5, 6, 7, 8, 9}, m = 5
Output : 2
Explanation : The subarrays having XOR of
              their elements as 2 are {5}
              and {5, 6, 7, 8, 9}

```

**简单解决方案**是使用两个循环遍历 arr []的所有可能子数组，并将其元素具有 XOR 的子数组的数量计为 m。

## C++

```cpp

// A simple C++ Program to count all subarrays having
// XOR of elements as given value m
#include <bits/stdc++.h>
using namespace std;

// Simple function that returns count of subarrays
// of arr with XOR value equals to m
long long subarrayXor(int arr[], int n, int m)
{
    long long ans = 0; // Initialize ans

    // Pick starting point i of subarrays
    for (int i = 0; i < n; i++) {
        int xorSum = 0; // Store XOR of current subarray

        // Pick ending point j of subarray for each i
        for (int j = i; j < n; j++) {
            // calculate xorSum
            xorSum = xorSum ^ arr[j];

            // If xorSum is equal to given value,
            // increase ans by 1.
            if (xorSum == m)
                ans++;
        }
    }
    return ans;
}

// Driver program to test above function
int main()
{
    int arr[] = { 4, 2, 2, 6, 4 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int m = 6;

    cout << "Number of subarrays having given XOR is "
         << subarrayXor(arr, n, m);
    return 0;
}

```

## Java

```java

// A simple Java Program to count all
// subarrays having XOR of elements 
// as given value m
public class GFG {

    // Simple function that returns
    // count of subarrays of arr with
    // XOR value equals to m
    static long subarrayXor(int arr[],
                             int n, int m)
    {

        // Initialize ans
        long ans = 0;

        // Pick starting point i of
        // subarrays
        for (int i = 0; i < n; i++)
        {

            // Store XOR of current
            // subarray
            int xorSum = 0;

            // Pick ending point j of 
            // subarray for each i
            for (int j = i; j < n; j++)
            {

                // calculate xorSum
                xorSum = xorSum ^ arr[j];

                // If xorSum is equal to
                // given value, increase
                // ans by 1.
                if (xorSum == m)
                    ans++;
            }
        }

        return ans;
    }

    // Driver code
    public static void main(String args[])
    {

        int[] arr = { 4, 2, 2, 6, 4 };
        int n = arr.length;
        int m = 6;

        System.out.println("Number of subarrays"
                       + " having given XOR is "
                       + subarrayXor(arr, n, m));
    }
}

// This code is contributed by Sam007.

```

## Python3

```py

# A simple Python3 Program to count all subarrays having
# XOR of elements as given value m

# Simple function that returns count of subarrays
# of arr with XOR value equals to m
def subarrayXor(arr, n, m):
    ans = 0 # Initialize ans

    # Pick starting po i of subarrays
    for i in range(0,n):

        xorSum = 0 # Store XOR of current subarray

        # Pick ending po j of subarray for each i
        for j  in range(i,n):
            # calculate xorSum
            xorSum = xorSum ^ arr[j]

            # If xorSum is equal to given value,
            # increase ans by 1.
            if (xorSum == m):
                ans+=1
    return ans

# Driver program to test above function
def main():
    arr = [ 4, 2, 2, 6, 4 ]
    n = len(arr)
    m = 6

    print("Number of subarrays having given XOR is "
         , subarrayXor(arr, n, m))

if __name__ == '__main__':
    main()

#this code contributed by 29AjayKumar

```

## C#

```cs

// A simple C# Program to count all
// subarrays having XOR of elements
// as given value m
using System;

class GFG {

    // Simple function that returns
    // count of subarrays of arr 
    // with XOR value equals to m
    static long subarrayXor(int[] arr,
                            int n, int m)
    {

        // Initialize ans
        long ans = 0;

        // Pick starting point i of 
        // subarrays
        for (int i = 0; i < n; i++)
        {

            // Store XOR of current
            // subarray
            int xorSum = 0;

            // Pick ending point j of 
            // subarray for each i
            for (int j = i; j < n; j++)
            {

                // calculate xorSum
                xorSum = xorSum ^ arr[j];

                // If xorSum is equal to
                // given value, increase
                // ans by 1.
                if (xorSum == m)
                    ans++;
            }
        }

        return ans;
    }

    // Driver Program
    public static void Main()
    {
        int[] arr = { 4, 2, 2, 6, 4 };
        int n = arr.Length;
        int m = 6;

        Console.Write("Number of subarrays"
                  + " having given XOR is "
                  + subarrayXor(arr, n, m));
    }
}

// This code is contributed by Sam007.

```

## PHP

```php

<?php
// A simple PHP Program to 
// count all subarrays having
// XOR of elements as given value m

// Simple function that returns
// count of subarrays of arr
// with XOR value equals to m
function subarrayXor($arr, $n,$m)
{

    // Initialize ans
    $ans = 0; 

    // Pick starting point
    // i of subarrays
    for ($i = 0; $i < $n; $i++) 
    {

        // Store XOR of
        // current subarray
        $xorSum = 0; 

        // Pick ending point j of 
        // subarray for each i
        for ($j = $i; $j < $n; $j++)
        {
            // calculate xorSum
            $xorSum = $xorSum ^ $arr[$j];

            // If xorSum is equal 
            // to given value,
            // increase ans by 1.
            if ($xorSum == $m)
                $ans++;
        }
    }
    return $ans;
}

    // Driver Code
    $arr = array(4, 2, 2, 6, 4);
    $n = count($arr);
    $m = 6;

    echo "Number of subarrays having given XOR is "
         , subarrayXor($arr, $n, $m);

// This code is contributed by anuj_67.
?>

```

**输出**：

```
Number of subarrays having given XOR is 4

```

上述解决方案的时间复杂度为 O（n <sup>2</sup> ）。

有效的**解决方案**在 O（n）时间内解决了上述问题。 让我们将[i + 1，j]范围内的所有元素的 XOR 称为 A，将[0，i]范围内的所有元素称为 B，将[0，j]范围内的所有元素称为 C。 在 C 的情况下，B 和 C 中[0，i]中的重叠元素为零，并且我们得到[i + 1，j]范围内所有元素的 XOR，即 A。由于 A = B XOR C，我们得到 B = A XORC。现在，如果我们知道 C 的值并将 A 的值取为 m，我们将 A 的计数作为所有满足该关系的 B 的计数。 本质上，我们获得每个 C 的 XOR-sum m 的所有子数组的计数。当我们将这个计数的总和作为 C 时，我们得到了答案。

```
1) Initialize ans as 0.
2) Compute xorArr, the prefix xor-sum array.
3) Create a map mp in which we store count of 
   all prefixes with XOR as a particular value. 
4) Traverse xorArr and for each element in xorArr
   (A) If m^xorArr[i] XOR exists in map, then 
       there is another previous prefix with 
       same XOR, i.e., there is a subarray ending
       at i with XOR equal to m. We add count of
       all such subarrays to result. 
   (B) If xorArr[i] is equal to m, increment ans by 1.
   (C) Increment count of elements having XOR-sum 
       xorArr[i] in map by 1.
5) Return ans.

```

## C++

```cpp

// C++ Program to count all subarrays having
// XOR of elements as given value m with
// O(n) time complexity.
#include <bits/stdc++.h>
using namespace std;

// Returns count of subarrays of arr with XOR
// value equals to m
long long subarrayXor(int arr[], int n, int m)
{
    long long ans = 0; // Initialize answer to be returned

    // Create a prefix xor-sum array such that
    // xorArr[i] has value equal to XOR
    // of all elements in arr[0 ..... i]
    int* xorArr = new int[n];

    // Create map that stores number of prefix array
    // elements corresponding to a XOR value
    unordered_map<int, int> mp;

    // Initialize first element of prefix array
    xorArr[0] = arr[0];

    // Computing the prefix array.
    for (int i = 1; i < n; i++)
        xorArr[i] = xorArr[i - 1] ^ arr[i];

    // Calculate the answer
    for (int i = 0; i < n; i++) {
        // Find XOR of current prefix with m.
        int tmp = m ^ xorArr[i];

        // If above XOR exists in map, then there
        // is another previous prefix with same
        // XOR, i.e., there is a subarray ending
        // at i with XOR equal to m.
        ans = ans + ((long long)mp[tmp]);

        // If this subarray has XOR equal to m itself.
        if (xorArr[i] == m)
            ans++;

        // Add the XOR of this subarray to the map
        mp[xorArr[i]]++;
    }

    // Return total count of subarrays having XOR of
    // elements as given value m
    return ans;
}

// Driver program to test above function
int main()
{
    int arr[] = { 4, 2, 2, 6, 4 };
    int n = sizeof(arr) / sizeof(arr[0]);
    int m = 6;

    cout << "Number of subarrays having given XOR is "
         << subarrayXor(arr, n, m);
    return 0;
}

```

## Java

```java

// Java Program to count all subarrays having
// XOR of elements as given value m with
// O(n) time complexity.
import java.util.*;

class GFG
{

    // Returns count of subarrays of arr with XOR
    // value equals to m
    static long subarrayXor(int arr[], int n, int m)
    {
        long ans = 0; // Initialize answer to be returned

        // Create a prefix xor-sum array such that
        // xorArr[i] has value equal to XOR
        // of all elements in arr[0 ..... i]
        int[] xorArr = new int[n];

        // Create map that stores number of prefix array
        // elements corresponding to a XOR value
        HashMap<Integer, Integer> mp = new HashMap<Integer, Integer>();

        // Initialize first element of prefix array
        xorArr[0] = arr[0];

        // Computing the prefix array.
        for (int i = 1; i < n; i++)
            xorArr[i] = xorArr[i - 1] ^ arr[i];

        // Calculate the answer
        for (int i = 0; i < n; i++) 
        {
            // Find XOR of current prefix with m.
            int tmp = m ^ xorArr[i];

            // If above XOR exists in map, then there
            // is another previous prefix with same
            // XOR, i.e., there is a subarray ending
            // at i with XOR equal to m.
            ans = ans + (mp.containsKey(tmp) == false ? 0 : ((long) mp.get(tmp)));

            // If this subarray has XOR equal to m itself.
            if (xorArr[i] == m)
                ans++;

            // Add the XOR of this subarray to the map
            if (mp.containsKey(xorArr[i]))
                mp.put(xorArr[i], mp.get(xorArr[i]) + 1);
            else
                mp.put(xorArr[i], 1);
        }

        // Return total count of subarrays having XOR of
        // elements as given value m
        return ans;
    }

    // Driver code
    public static void main(String[] args) 
    {
        int arr[] = { 4, 2, 2, 6, 4 };
        int n = arr.length;
        int m = 6;

        System.out.print("Number of subarrays having given XOR is "
        + subarrayXor(arr, n, m));
    }
}

// This code is contributed by PrinciRaj1992

```

## Python3

```py

# Python3 Program to count all subarrays 
# having XOR of elements as given value m 
# with O(n) time complexity.

# Returns count of subarrays of arr 
# with XOR value equals to m
def subarrayXor(arr, n, m):

    ans = 0 # Initialize answer to be returned

    # Create a prefix xor-sum array such that
    # xorArr[i] has value equal to XOR
    # of all elements in arr[0 ..... i]
    xorArr =[0 for _ in range(n)]

    # Create map that stores number of prefix array
    # elements corresponding to a XOR value
    mp = dict()

    # Initialize first element 
    # of prefix array
    xorArr[0] = arr[0]

    # Computing the prefix array.
    for i in range(1, n):
        xorArr[i] = xorArr[i - 1] ^ arr[i]

    # Calculate the answer
    for i in range(n):

        # Find XOR of current prefix with m.
        tmp = m ^ xorArr[i]

        # If above XOR exists in map, then there
        # is another previous prefix with same
        # XOR, i.e., there is a subarray ending
        # at i with XOR equal to m.
        if tmp in mp.keys():
            ans = ans + (mp[tmp])

        # If this subarray has XOR 
        # equal to m itself.
        if (xorArr[i] == m):
            ans += 1

        # Add the XOR of this subarray to the map
        mp[xorArr[i]] = mp.get(xorArr[i], 0) + 1

    # Return total count of subarrays having 
    # XOR of elements as given value m
    return ans

# Driver Code
arr = [4, 2, 2, 6, 4]
n = len(arr)
m = 6

print("Number of subarrays having given XOR is",
                        subarrayXor(arr, n, m))

# This code is contributed by mohit kumar

```

## C#

```cs

// C# Program to count all subarrays having
// XOR of elements as given value m with
// O(n) time complexity.
using System;
using System.Collections.Generic;

class GFG
{

    // Returns count of subarrays of arr with XOR
    // value equals to m
    static long subarrayXor(int []arr, int n, int m)
    {
        long ans = 0; // Initialize answer to be returned

        // Create a prefix xor-sum array such that
        // xorArr[i] has value equal to XOR
        // of all elements in arr[0 ..... i]
        int[] xorArr = new int[n];

        // Create map that stores number of prefix array
        // elements corresponding to a XOR value
        Dictionary<int, int> mp = new Dictionary<int, int>();

        // Initialize first element of prefix array
        xorArr[0] = arr[0];

        // Computing the prefix array.
        for (int i = 1; i < n; i++)
            xorArr[i] = xorArr[i - 1] ^ arr[i];

        // Calculate the answer
        for (int i = 0; i < n; i++) 
        {
            // Find XOR of current prefix with m.
            int tmp = m ^ xorArr[i];

            // If above XOR exists in map, then there
            // is another previous prefix with same
            // XOR, i.e., there is a subarray ending
            // at i with XOR equal to m.
            ans = ans + (mp.ContainsKey(tmp) == false ? 0 : ((long) mp[tmp]));

            // If this subarray has XOR equal to m itself.
            if (xorArr[i] == m)
                ans++;

            // Add the XOR of this subarray to the map
            if (mp.ContainsKey(xorArr[i]))
                mp[xorArr[i]] = mp[xorArr[i]] + 1;
            else
                mp.Add(xorArr[i], 1);
        }

        // Return total count of subarrays having XOR of
        // elements as given value m
        return ans;
    }

    // Driver code
    public static void Main(String[] args) 
    {
        int []arr = { 4, 2, 2, 6, 4 };
        int n = arr.Length;
        int m = 6;

        Console.Write("Number of subarrays having given XOR is "
        + subarrayXor(arr, n, m));
    }
}

// This code is contributed by Rajput-Ji

```

**输出**：

```
Number of subarrays having given XOR is 4

```

**时间复杂度**：O（n）

**替代方法**：使用 Python 词典存储前缀 XOR

## Python3

```py

from collections import defaultdict
def subarrayXor(arr, n, m): 
    HashTable=defaultdict(bool)
    HashTable[0]=1
    count=0
    curSum=0
    for i in arr:
        curSum^=i
        if HashTable[curSum^m]:
            count+=HashTable[curSum^m]
        HashTable[curSum]+=1
    return(count)

# Driver program to test above function 
def main(): 
    arr = [ 5, 6, 7, 8, 9 ] 
    n = len(arr) 
    m = 5

    print("Number of subarrays having given XOR is "
        , subarrayXor(arr, n, m)) 

if __name__ == '__main__': 
    main() 

 # This code is contributed by mrmechanical26052000

```

**输出**：

```
Number of subarrays having given XOR is 4
```

**时间复杂度**：O（n）

**空间复杂度**：O（n）

本文由 **Anmol Ratnam** 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。
如果发现任何不正确的内容，或者您​​想分享有关上述主题的更多信息，请发表评论。

