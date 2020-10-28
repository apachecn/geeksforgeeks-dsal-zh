# 其和为 2 的幂的对的数量

> 原文：[https://www.geeksforgeeks.org/number-of-pairs-whose-sum-is-a-power-of-2/](https://www.geeksforgeeks.org/number-of-pairs-whose-sum-is-a-power-of-2/)

给定正整数数组 **arr []** ，任务是计算对数**（arr [i]，arr [j]）**的最大可能数目，以使 **arr [i] + arr [j]** 是**的 2** 次方。

**注意**：一个元素最多可以使用一次以形成一对。

**示例**：

> **输入**：arr [] = {3，11，14，5，13}
> **输出**：2
> 所有有效对分别是（13，3）和（11 ，5）两者之和为 16，也就是 2 的幂。
> 我们可以使用（3，5），但这样做最多只能形成 1 对。
> 因此，（3，5）不是最佳的。
> 
> **输入**：arr [] = {1、2、3}
> **输出**：1
> 1 和 3 可以配对形成 4 的幂。 。

**简单解决方案**是考虑每对，并检查该对的和是否为 2 的幂。 该解决方案的时间复杂度为 O（n * n）

**有效方法**：是从数组中找出最大元素，例如 **X** ，然后从其余数组元素 **Y** 中找到最大元素，使得 **Y≤X** 和 **X + Y** 是 2 的**次幂。 这是对的最佳选择，因为即使 **Y** 与其他某些元素（例如 **Z** ）形成有效对，然后 **Z** 也会与其他元素配对 **Y** （如果可能的话）来最大化有效对的数量。**

## C++

```cpp

// C++ implementation of above approach 
#include <bits/stdc++.h> 
using namespace std; 

// Function to return the count of valid pairs 
int countPairs(int a[], int n) 
{ 
    // Storing occurrences of each element 
    unordered_map<int, int> mp; 
    for (int i = 0; i < n; i++) 
        mp[a[i]]++; 

    // Sort the array in deceasing order 
    sort(a, a + n, greater<int>()); 

    // Start taking largest element each time 
    int count = 0; 
    for (int i = 0; i < n; i++) { 

        // If element has already been paired 
        if (mp[a[i]] < 1) 
            continue; 

        // Find the number which is greater than 
        // a[i] and power of two 
        int cur = 1; 
        while (cur <= a[i]) 
            cur <<= 1; 

        // If there is a number which adds up with a[i] 
        // to form a power of two 
        if (mp[cur - a[i]]) { 

            // Edge case when a[i] and crr - a[i] is same 
            // and we have only one occurrence of a[i] then 
            // it cannot be paired 
            if (cur - a[i] == a[i] and mp[a[i]] == 1) 
                continue; 

            count++; 

            // Remove already paired elements 
            mp[cur - a[i]]--; 
            mp[a[i]]--; 
        } 
    } 

    // Return the count 
    return count; 
} 

// Driver code 
int main() 
{ 
    int a[] = { 3, 11, 14, 5, 13 }; 
    int n = sizeof(a) / sizeof(a[0]); 
    cout << countPairs(a, n); 
    return 0; 
} 

```

## Java

```java

// Java implementation of above approach 
import java.util.TreeMap; 

class Count 
{ 
    // Function to return the count of valid pairs 
    static int countPairs(int[] a, int n) 
    { 

        // To keep the element in sorted order 
        TreeMap<Integer, Integer> map = new TreeMap<>(); 
        for (int i = 0; i < n; i++) 
        { 
            map.put(a[i], 1); 
        } 

        // Start taking largest element each time 
        int count = 0; 
        for (int i = 0; i < n; i++) 
        { 
            // If element has already been paired 
            if (map.get(a[i]) < 1) 
                continue; 

            // Find the number which is greater than 
            // a[i] and power of two 
            int cur = 1; 
            while (cur <= a[i]) 
                cur <<= 1; 

            // If there is a number which adds up with a[i] 
            // to form a power of two 
            if (map.containsKey(cur - a[i])) 
            { 
                // Edge case when a[i] and crr - a[i] is same 
                // and we have only one occurrence of a[i] then 
                // it cannot be paired 
                if (cur - a[i] == a[i] && map.get(a[i]) == 1) 
                    continue; 
                count++; 

                // Remove already paired elements 
                map.put(cur - a[i], map.get(cur - a[i]) - 1); 
                map.put(a[i], map.get(a[i]) - 1); 
            } 

        } 
        // Return the count 
        return count; 
    } 

    // Driver code 
    public static void main(String[] args)  
    { 
        int[] a = { 3, 11, 14, 5, 13 }; 
        int n = a.length; 
        System.out.println(countPairs(a, n)); 
    } 
} 

// This code is contributed by Vivekkumar Singh 

```

## Python3

```py

# Python3 implementation of above approach  

# Function to return the count  
# of valid pairs  
def countPairs(a, n) :  

    # Storing occurrences of each element  
    mp = dict.fromkeys(a, 0)  
    for i in range(n) :  
        mp[a[i]] += 1

    # Sort the array in deceasing order  
    a.sort(reverse = True) 

    # Start taking largest element  
    # each time 
    count = 0
    for i in range(n) :  

        # If element has already been paired  
        if (mp[a[i]] < 1) : 
            continue

        # Find the number which is greater  
        # than a[i] and power of two  
        cur = 1
        while (cur <= a[i]) : 
            cur = cur << 1

        # If there is a number which adds   
        # up with a[i] to form a power of two  
        if (cur - a[i] in mp.keys()) : 

            # Edge case when a[i] and crr - a[i]  
            # is same and we have only one occurrence  
            # of a[i] then it cannot be paired  
            if (cur - a[i] == a[i] and mp[a[i]] == 1) : 
                continue

            count += 1

            # Remove already paired elements  
            mp[cur - a[i]] -= 1
            mp[a[i]] -= 1

    # Return the count  
    return count  

# Driver code  
if __name__ == "__main__" :  

    a = [ 3, 11, 14, 5, 13 ]  
    n = len(a)  
    print(countPairs(a, n)) 

# This code is contributed by Ryuga 

```

## C#

```cs

// C# implementation of above approach 
using System; 
using System.Collections.Generic;  

class GFG 
{ 
    // Function to return the count of valid pairs 
    static int countPairs(int[] a, int n) 
    { 

        // To keep the element in sorted order 
        Dictionary<int,  
                   int> map = new Dictionary<int, 
                                             int>(); 
        for (int i = 0; i < n; i++) 
        { 
            if(!map.ContainsKey(a[i])) 
                map.Add(a[i], 1); 
        } 

        // Start taking largest element each time 
        int count = 0; 
        for (int i = 0; i < n; i++) 
        { 
            // If element has already been paired 
            if (map[a[i]] < 1) 
                continue; 

            // Find the number which is greater than 
            // a[i] and power of two 
            int cur = 1; 
            while (cur <= a[i]) 
                cur <<= 1; 

            // If there is a number which adds up  
            // with a[i] to form a power of two 
            if (map.ContainsKey(cur - a[i])) 
            { 
                // Edge case when a[i] and crr - a[i]  
                // is same and we have only one occurrence  
                // of a[i] then it cannot be paired 
                if (cur - a[i] == a[i] && map[a[i]] == 1) 
                    continue; 
                count++; 

                // Remove already paired elements 
                map[cur - a[i]] = map[cur - a[i]] - 1; 
                map[a[i]] = map[a[i]] - 1; 
            } 

        } 

        // Return the count 
        return count; 
    } 

    // Driver code 
    public static void Main(String[] args)  
    { 
        int[] a = { 3, 11, 14, 5, 13 }; 
        int n = a.Length; 
        Console.WriteLine(countPairs(a, n)); 
    } 
} 

// This code is contributed by Princi Singh 

```

**Output:**

```
2

```

请注意，上述代码中的以下操作可以使用[中讨论的最后一种方法，在 O（1）时间内完成。最小幂 2 大于或等于 n](https://www.geeksforgeeks.org/smallest-power-of-2-greater-than-or-equal-to-n/)

```
// Find the number which is greater than
// a[i] and power of two
int cur = 1;
while (cur <= a[i])
cur <<= 1;
```

优化上述表达式后，该解决方案的时间复杂度变为 O（n Log n）



* * *

* * *



