# 找出 LCM 最多为 K 的数组中最长的子序列

> 原文:[https://www . geeksforgeeks . org/find-最长数组子序列最多有-LCM-k/](https://www.geeksforgeeks.org/find-the-longest-subsequence-of-an-array-having-lcm-at-most-k/)

给定一个由 **N** 元素和一个正整数 **K** 组成的数组**。任务是找到数组中最长的子序列，最多有 [LCM](https://www.geeksforgeeks.org/lcm-gq/) (最小公倍数) **K** 。按照获得的子序列元素的索引(从 0 开始)，打印 LCM 和子序列的长度。如果无法打印 **-1** 。
**示例:**** 

> **输入:** arr[] = {2，3，4，5}，K = 14
> **输出:**
> LCM = 12，长度= 3
> 索引= 0 1 2
> **输入:** arr[] = {12，33，14，52}，K = 4
> **输出:** -1

**方法:**找到数组的所有唯一元素及其各自的频率。现在你应该得到的最高 LCM 是 **K** 。假设你有一个数字 **X** ，使得 **1 ≤ X ≤ K** ，从数组中获取 **X** 的倍数的所有唯一数字，并将其频率加到 **X** 的 **numCount** 上。答案将是 **numCount** 最高的数字，让它成为你的 LCM。现在，要获得子序列编号的索引，开始从头遍历数组，如果 **LCM % arr[i] = 0** ，则打印索引 **i** 。
以下是上述办法的实施:

## C++

```
// C++ implementation of the approach
#include <bits/stdc++.h>
using namespace std;

// Function to find the longest subsequence
// having LCM less than or equal to K
void findSubsequence(int* arr, int n, int k)
{

    // Map to store unique elements
    // and their frequencies
    map<int, int> M;

    // Update the frequencies
    for (int i = 0; i < n; ++i)
        ++M[arr[i]];

    // Array to store the count of numbers whom
    // 1 <= X <= K is a multiple of
    int* numCount = new int[k + 1];

    for (int i = 0; i <= k; ++i)
        numCount[i] = 0;

    // Check every unique element
    for (auto p : M) {
        if (p.first <= k) {

            // Find all its multiples <= K
            for (int i = 1;; ++i) {
                if (p.first * i > k)
                    break;

                // Store its frequency
                numCount[p.first * i] += p.second;
            }
        }
        else
            break;
    }

    int lcm = 0, length = 0;

    // Obtain the number having maximum count
    for (int i = 1; i <= k; ++i) {
        if (numCount[i] > length) {
            length = numCount[i];
            lcm = i;
        }
    }

    // Condition to check if answer
    // doesn't exist
    if (lcm == 0)
        cout << -1 << endl;
    else {

        // Print the answer
        cout << "LCM = " << lcm
             << ", Length = " << length << endl;

        cout << "Indexes = ";
        for (int i = 0; i < n; ++i)
            if (lcm % arr[i] == 0)
                cout << i << " ";
    }
}

// Driver code
int main()
{

    int k = 14;
    int arr[] = { 2, 3, 4, 5 };
    int n = sizeof(arr) / sizeof(arr[0]);

    findSubsequence(arr, n, k);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// Java implementation of the approach
import java.util.*;

class GFG
{
    // Function to find the longest subsequence
    // having LCM less than or equal to K
    static void findSubsequence(int []arr, int n, int k)
    {

        // Map to store unique elements
        // and their frequencies
        HashMap<Integer, Integer> M = new HashMap<Integer,Integer>();

        // Update the frequencies
        for (int i = 0; i < n; ++i)
        {
            if(M.containsKey(arr[i]))
                M.put(arr[i], M.get(arr[i])+1);
            else
                M.put(arr[i], 1);
        }

        // Array to store the count of numbers whom
        // 1 <= X <= K is a multiple of
        int [] numCount = new int[k + 1];

        for (int i = 0; i <= k; ++i)
            numCount[i] = 0;

        Iterator<HashMap.Entry<Integer, Integer>> itr = M.entrySet().iterator();

        // Check every unique element
        while(itr.hasNext())
        {
            HashMap.Entry<Integer, Integer> entry = itr.next();
            if (entry.getKey() <= k)
            {

                // Find all its multiples <= K
                for (int i = 1;; ++i)
                {
                    if (entry.getKey() * i > k)
                        break;

                    // Store its frequency
                    numCount[entry.getKey() * i] += entry.getValue();
                }
            }
            else
                break;
        }

        int lcm = 0, length = 0;

        // Obtain the number having maximum count
        for (int i = 1; i <= k; ++i)
        {
            if (numCount[i] > length)
            {
                length = numCount[i];
                lcm = i;
            }
        }

        // Condition to check if answer
        // doesn't exist
        if (lcm == 0)
            System.out.println(-1);
        else
        {

            // Print the answer
            System.out.println("LCM = " + lcm
                + " Length = " + length );

            System.out.print( "Indexes = ");
            for (int i = 0; i < n; ++i)
                if (lcm % arr[i] == 0)
                    System.out.print(i + " ");
        }
    }

    // Driver code
    public static void main (String[] args)
    {

        int k = 14;
        int arr[] = { 2, 3, 4, 5 };
        int n = arr.length;

        findSubsequence(arr, n, k);
    }
}

// This code is contributed by ihritik
```

## 蟒蛇 3

```
# Python3 implementation of the approach
from collections import defaultdict

# Function to find the longest subsequence
# having LCM less than or equal to K
def findSubsequence(arr, n, k):

    # Map to store unique elements
    # and their frequencies
    M = defaultdict(lambda:0)

    # Update the frequencies
    for i in range(0, n):
        M[arr[i]] += 1

    # Array to store the count of numbers
    # whom 1 <= X <= K is a multiple of
    numCount = [0] * (k + 1)

    # Check every unique element
    for p in M:
        if p <= k:

            # Find all its multiples <= K
            i = 1
            while p * i <= k:

                # Store its frequency
                numCount[p * i] += M[p]
                i += 1

        else:
            break

    lcm, length = 0, 0

    # Obtain the number having maximum count
    for i in range(1, k + 1):
        if numCount[i] > length:
            length = numCount[i]
            lcm = i

    # Condition to check if answer doesn't exist
    if lcm == 0:
        print(-1)
    else:

        # Print the answer
        print("LCM = {0}, Length = {1}".format(lcm, length))

        print("Indexes = ", end = "")
        for i in range(0, n):
            if lcm % arr[i] == 0:
                print(i, end = " ")

# Driver code
if __name__ == "__main__":

    k = 14
    arr = [2, 3, 4, 5]
    n = len(arr)

    findSubsequence(arr, n, k)

# This code is contributed by Rituraj Jain
```

## C#

```
// C# implementation of the approach
using System;
using System.Collections.Generic;

class GFG
{
    // Function to find the longest subsequence
    // having LCM less than or equal to K
    static void findSubsequence(int []arr, int n, int k)
    {

        // Map to store unique elements
        // and their frequencies
        Dictionary<int, int> M = new Dictionary<int, int>();

        // Update the frequencies
        for (int i = 0; i < n; ++i)
        {
            if(M.ContainsKey(arr[i]))
                M[arr[i]]++;
            else
                M[arr[i]] = 1;
        }

        // Array to store the count of numbers whom
        // 1 <= X <= K is a multiple of
        int [] numCount = new int[k + 1];

        for (int i = 0; i <= k; ++i)
            numCount[i] = 0;

        Dictionary<int, int>.KeyCollection keyColl = M.Keys;

        // Check every unique element
        foreach(int key in keyColl)
        {
            if ( key <= k)
            {

                // Find all its multiples <= K
                for (int i = 1;; ++i)
                {
                    if (key * i > k)
                        break;

                    // Store its frequency
                    numCount[key * i] += M[key];
                }
            }
            else
                break;
        }

        int lcm = 0, length = 0;

        // Obtain the number having maximum count
        for (int i = 1; i <= k; ++i)
        {
            if (numCount[i] > length)
            {
                length = numCount[i];
                lcm = i;
            }
        }

        // Condition to check if answer
        // doesn't exist
        if (lcm == 0)
            Console.WriteLine(-1);
        else
        {

            // Print the answer
            Console.WriteLine("LCM = " + lcm
                + " Length = " + length );

            Console.Write( "Indexes = ");
            for (int i = 0; i < n; ++i)
                if (lcm % arr[i] == 0)
                    Console.Write(i + " ");
        }
    }

    // Driver code
    public static void Main ()
    {

        int k = 14;
        int []arr = { 2, 3, 4, 5 };
        int n = arr.Length;

        findSubsequence(arr, n, k);
    }
}

// This code is contributed by ihritik
```

## 服务器端编程语言（Professional Hypertext Preprocessor 的缩写）

```
<?php
// PHP implementation of the approach

// Function to find the longest subsequence
// having LCM less than or equal to K
function findSubsequence($arr, $n, $k)
{

    // Map to store unique elements
    // and their frequencies
    $M = array();

    for($i = 0; $i < $n; $i++)
        $M[$arr[$i]] = 0 ;

    // Update the frequencies
    for ($i = 0; $i < $n; ++$i)
        ++$M[$arr[$i]];

    // Array to store the count of numbers
    // whom 1 <= X <= K is a multiple of
    $numCount = array();

    for ($i = 0; $i <= $k; ++$i)
        $numCount[$i] = 0;

    // Check every unique element
    foreach($M as $key => $value)
    {
        if ($key <= $k)
        {

            // Find all its multiples <= K
            for ($i = 1;; ++$i)
            {
                if ($key * $i > $k)
                    break;

                // Store its frequency
                $numCount[$key * $i] += $value;
            }
        }
        else
            break;
    }

    $lcm = 0; $length = 0;

    // Obtain the number having
    // maximum count
    for ($i = 1; $i <= $k; ++$i)
    {
        if ($numCount[$i] > $length)
        {
            $length = $numCount[$i];
            $lcm = $i;
        }
    }

    // Condition to check if answer
    // doesn't exist
    if ($lcm == 0)
        echo -1 << "\n";
    else
    {

        // Print the answer
        echo "LCM = ", $lcm,
             ", Length = ", $length, "\n";

        echo "Indexes = ";
        for ($i = 0; $i < $n; ++$i)
            if ($lcm % $arr[$i] == 0)
                echo $i, " ";
    }
}

// Driver code
$k = 14;
$arr = array( 2, 3, 4, 5 );
$n = count($arr);

findSubsequence($arr, $n, $k);

// This code is contributed by Ryuga
?>
```

## java 描述语言

```
<script>

// JavaScript implementation of the approach

// Function to find the longest subsequence
// having LCM less than or equal to K
function findSubsequence(arr, n, k) {

    // Map to store unique elements
    // and their frequencies
    let M = new Map();

    // Update the frequencies
    for (let i = 0; i < n; ++i) {
        if (M.has(arr[i])) {
            M.set(arr[i], M.get(arr[i]) + 1)
        } else {
            M.set(arr[i], 1)
        }
    }

    // Array to store the count of numbers whom
    // 1 <= X <= K is a multiple of
    let numCount = new Array(k + 1);

    for (let i = 0; i <= k; ++i)
        numCount[i] = 0;

    // Check every unique element
    for (let p of M) {
        if (p[0] <= k) {

            // Find all its multiples <= K
            for (let i = 1; ; ++i) {
                if (p[0] * i > k)
                    break;

                // Store its frequency
                numCount[p[0] * i] += p[1];
            }
        }
        else
            break;
    }

    let lcm = 0, length = 0;

    // Obtain the number having maximum count
    for (let i = 1; i <= k; ++i) {
        if (numCount[i] > length) {
            length = numCount[i];
            lcm = i;
        }
    }

    // Condition to check if answer
    // doesn't exist
    if (lcm == 0)
        document.write(-1 + "<br>");
    else {

        // Print the answer
        document.write(
        "LCM = " + lcm + ", Length = " + length + "<br>"
        );

        document.write("Indexes = ");
        for (let i = 0; i < n; ++i)
            if (lcm % arr[i] == 0)
                document.write(i + " ");
    }
}

// Driver code

let k = 14;
let arr = [2, 3, 4, 5];
let n = arr.length;

findSubsequence(arr, n, k);

// This code is contributed by _saurabh_jaiswal

</script>
```

**Output:** 

```
LCM = 12, Length = 3
Indexes = 0 1 2
```