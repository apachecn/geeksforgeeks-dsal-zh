# 一半异或等于另一半的子阵列数量

> 原文:[https://www . geeksforgeeks . org/子阵数-这样二分之一异或等于二分之一/](https://www.geeksforgeeks.org/number-of-subarrays-such-that-xor-of-one-half-is-equal-to-the-other/)

给定一个由 **N** 个数字组成的数组，任务是找到给定数组的子数组数量(子数组的大小应为偶数)，这样在将子数组分成相等的两半后，子数组一半的**逐位异或**将等于另一半的**逐位异或**。

**示例:**

```
Input : N = 6, arr[] = {3, 2, 2, 3, 7, 6}
Output : 3
Valid sub-arrays are {3, 2, 2, 3}, {2, 2}, 
and {2, 3, 7, 6}

Input : N = 5, arr[] = {1, 2, 3, 4, 5}
Output : 1

Input : N = 3, arr[] = {42, 4, 2}
Output : 0
```

**方法:**如果一个数组被分成相等的两半，其中一半的 XOR 等于另一半，这意味着整个数组的 XOR 应该是 0，因为 A^A = 0。现在，为了解决上述问题，从左边开始找出给定数组中所有元素的前缀异或。

假设一个子阵从 *l* 开始，到 *r* 结束，那么(r-l+1)应该是**甚至**。同样，为了找到给定范围的异或 *(l，r)* 用前缀异或减去前缀异或(l–1)

因为，(r–l+1)是偶数，所以如果 *r* 是偶数，那么 *l* 应该是奇数，反之亦然。现在，将您的前缀分为两组，一组应该是奇数索引的前缀，另一组应该是偶数索引的前缀。现在，开始从左到右遍历前缀数组，看看这个特定的前缀 A 已经在其各自的组中出现了多少次，即偶数索引处的前缀应该在偶数前缀组中检查，奇数前缀组中奇数索引处的前缀应该检查(因为如果 *r* 是偶数，那么( *l* -1)也是偶数，如果 *r* 是奇数，则应用类似的逻辑)。

下面是上述方法的实现:

## C++

```
// C++ program to find number of subarrays such that
// XOR of one half is equal to the other

#include <bits/stdc++.h>
using namespace std;

// Function to find number of subarrays such that
// XOR of one half is equal to the other
int findSubarrCnt(int arr[], int n)
{
    // Variables to store answer and current XOR's
    int ans = 0, XOR = 0;

    // Array to store prefix XOR's
    int prefix[n];

    for (int i = 0; i < n; ++i) {

        // Calculate XOR until this index
        XOR = XOR ^ arr[i];

        // Store the XOR in prefix array
        prefix[i] = XOR;
    }

    // Create groups for odd indexes and even indexes
    unordered_map<int, int> oddGroup, evenGroup;

    // Initialize occurrence of 0 in oddGroup as 1
    // because it will be used in case our
    // subarray has l = 0
    oddGroup[0] = 1;

    for (int i = 0; i < n; ++i) {

        if (i & 1) {

            // Check the frequency of current prefix
            // XOR in oddGroup and add it to the
            // answer
            ans += oddGroup[prefix[i]];

            // Update the frequency
            ++oddGroup[prefix[i]];
        }
        else {

            // Check the frequency of current prefix
            // XOR in evenGroup and add it to the
            // answer
            ans += evenGroup[prefix[i]];

            // Update the frequency
            ++evenGroup[prefix[i]];
        }
    }

    return ans;
}

// Driver Code
int main()
{
    int N = 6;

    int arr[] = { 3, 2, 2, 3, 7, 6 };

    cout << findSubarrCnt(arr, N);

    return 0;
}
```

## Java 语言(一种计算机语言，尤用于创建网站)

```
// JAVA program to find number of subarrays such that
// XOR of one half is equal to the other
import java.util.*;

class GFG
{

    // Function to find number of subarrays such that
    // XOR of one half is equal to the other
    static int findSubarrCnt(int arr[], int n)
    {
        // Variables to store answer and current XOR's
        int ans = 0, XOR = 0;

        // Array to store prefix XOR's
        int prefix[] = new int[n];

        for (int i = 0; i < n; ++i)
        {

            // Calculate XOR until this index
            XOR = XOR ^ arr[i];

            // Store the XOR in prefix array
            prefix[i] = XOR;
        }

        // Create groups for odd indexes and even indexes
        HashMap<Integer, Integer> evenGroup = new HashMap<>();
        HashMap<Integer, Integer> oddGroup = new HashMap<>();

        // Initialize occurrence of 0 in oddGroup as 1
        // because it will be used in case our
        // subarray has l = 0
        oddGroup.put(0, 1);

        for (int i = 0; i < n; ++i)
        {

            if (i % 2== 1)
            {

                // Check the frequency of current prefix
                // XOR in oddGroup and add it to the
                // answer
                if(oddGroup.containsKey(prefix[i]))
                {
                    ans += oddGroup.get(prefix[i]);

                    // Update the frequency
                    oddGroup.put(prefix[i],oddGroup.get(prefix[i] + 1));
                }
                else
                {
                    oddGroup.put(prefix[i], 1);
                }

            }
            else
            {

                // Check the frequency of current prefix
                // XOR in evenGroup and add it to the
                // answer
                if(evenGroup.containsKey(prefix[i]))
                {
                    ans += evenGroup.get(prefix[i]);

                    // Update the frequency
                    evenGroup.put(prefix[i],evenGroup.get(prefix[i] + 1));
                }
                else
                {
                    evenGroup.put(prefix[i], 1);
                }
            }
        }

        return ans;
    }

    // Driver Code
    public static void main (String[] args)
    {

        int arr[] = { 3, 2, 2, 3, 7, 6 };
        int N = arr.length;

        System.out.println(findSubarrCnt(arr, N));
    }
}

// This code is contributed by ihritik
```

## 蟒蛇 3

```
# Python3 program to find number of subarrays
# such that XOR of one half is equal to the other

# Function to find number of subarrays
# such that XOR of one half is equal
# to the other
def findSubarrCnt(arr, n) :

    # Variables to store answer
    # and current XOR's
    ans = 0; XOR = 0;

    # Array to store prefix XOR's
    prefix = [0] * n;

    for i in range(n) :

        # Calculate XOR until this index
        XOR = XOR ^ arr[i];

        # Store the XOR in prefix array
        prefix[i] = XOR;

    # Create groups for odd indexes and
    # even indexes
    oddGroup = dict.fromkeys(prefix, 0)
    evenGroup = dict.fromkeys(prefix, 0)

    # Initialize occurrence of 0 in oddGroup
    # as 1 because it will be used in case 
    # our subarray has l = 0
    oddGroup[0] = 1;

    for i in range(n) :

        if (i & 1) :

            # Check the frequency of current
            # prefix XOR in oddGroup and add
            # it to the answer
            ans += oddGroup[prefix[i]];

            # Update the frequency
            oddGroup[prefix[i]] += 1;

        else :

            # Check the frequency of current
            # prefix XOR in evenGroup and add
            # it to the answer
            ans += evenGroup[prefix[i]];

            # Update the frequency
            evenGroup[prefix[i]] += 1;

    return ans;

# Driver Code
if __name__ == "__main__" :

    N = 6;

    arr = [ 3, 2, 2, 3, 7, 6 ];

    print(findSubarrCnt(arr, N));

# This code is contributed by Ryuga
```

## C#

```
// C# program to find number of subarrays such that
// XOR of one half is equal to the other
using System;
using System.Collections.Generic;

class GFG
{

    // Function to find number of subarrays such that
    // XOR of one half is equal to the other
    static int findSubarrCnt(int [] arr, int n)
    {
        // Variables to store answer and current XOR's
        int ans = 0, XOR = 0;

        // Array to store prefix XOR's
        int [] prefix = new int[n];

        for (int i = 0; i < n; ++i)
        {

            // Calculate XOR until this index
            XOR = XOR ^ arr[i];

            // Store the XOR in prefix array
            prefix[i] = XOR;
        }

        // Create groups for odd indexes and even indexes
        Dictionary<int, int> evenGroup = new Dictionary<int, int>();
        Dictionary<int, int> oddGroup = new Dictionary<int, int>();

        // Initialize occurrence of 0 in oddGroup as 1
        // because it will be used in case our
        // subarray has l = 0
        oddGroup[0] = 1;

        for (int i = 0; i < n; ++i)
        {

            if (i % 2== 1)
            {

                // Check the frequency of current prefix
                // XOR in oddGroup and add it to the
                // answer
                if(oddGroup.ContainsKey(prefix[i]))
                {
                    ans += oddGroup[prefix[i]];

                    // Update the frequency
                    oddGroup[prefix[i]]++;
                }
                else
                {
                    oddGroup[prefix[i]] = 1;
                }

            }
            else
            {

                // Check the frequency of current prefix
                // XOR in evenGroup and add it to the
                // answer
                if(evenGroup.ContainsKey(prefix[i]))
                {
                    ans += evenGroup[prefix[i]];

                    // Update the frequency
                    evenGroup[prefix[i]]++;
                }
                else
                {
                    evenGroup[prefix[i]] = 1;
                }
            }
        }

        return ans;
    }

    // Driver Code
    public static void Main ()
    {

        int [] arr = { 3, 2, 2, 3, 7, 6 };

        int N = arr.Length;

        Console.WriteLine(findSubarrCnt(arr, N));
    }
}

// This code is contributed by ihritik
```

## java 描述语言

```
<script>

// Javascript program to find number of subarrays such that
// XOR of one half is equal to the other

    // Function to find number of subarrays such that
    // XOR of one half is equal to the other
    function findSubarrCnt(arr, n)
    {
        // Variables to store answer and current XOR's
        let ans = 0, XOR = 0;

        // Array to store prefix XOR's
        let prefix = Array.from({length: n}, (_, i) => 0);

        for (let i = 0; i < n; ++i)
        {

            // Calculate XOR until this index
            XOR = XOR ^ arr[i];

            // Store the XOR in prefix array
            prefix[i] = XOR;
        }

        // Create groups for odd indexes and even indexes
        let evenGroup = new Map();
        let oddGroup = new Map();

        // Initialize occurrence of 0 in oddGroup as 1
        // because it will be used in case our
        // subarray has l = 0
        oddGroup.set(0, 1);

        for (let i = 0; i < n; ++i)
        {

            if (i % 2== 1)
            {

                // Check the frequency of current prefix
                // XOR in oddGroup and add it to the
                // answer
                if(oddGroup.has(prefix[i]))
                {
                    ans += oddGroup.get(prefix[i]);

                    // Update the frequency
                    oddGroup.set(prefix[i],oddGroup.get(prefix[i] + 1));
                }
                else
                {
                    oddGroup.set(prefix[i], 1);
                }

            }
            else
            {

                // Check the frequency of current prefix
                // XOR in evenGroup and add it to the
                // answer
                if(evenGroup.has(prefix[i]))
                {
                    ans += evenGroup.get(prefix[i]);

                    // Update the frequency
                    evenGroup.set(prefix[i],evenGroup.get(prefix[i] + 1));
                }
                else
                {
                    evenGroup.set(prefix[i], 1);
                }
            }
        }

        return ans;
    }

    // Driver code

        let arr = [ 3, 2, 2, 3, 7, 6 ];
        let N = arr.length;

        document.write(findSubarrCnt(arr, N));

</script>
```

**Output:** 

```
3
```