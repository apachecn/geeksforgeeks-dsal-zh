# 多数元素| 第 2 组（哈希）

> 原文：[https://www.geeksforgeeks.org/majority-element-set-2-hashing/](https://www.geeksforgeeks.org/majority-element-set-2-hashing/)

给定大小为 N 的数组，找到多数元素。 多数元素是在给定数组中出现![\floor{\frac{n}{2}}](img/6b97b83019d889e5a31cda3e150a83d9.png "Rendered by QuickLaTeX.com")次以上的元素。

**示例**：

```
Input: [3, 2, 3]
Output: 3

Input: [2, 2, 1, 1, 1, 2, 2]
Output: 2

```

在先前的[帖子](https://www.geeksforgeeks.org/majority-element/)中，使用 4 种不同的方法解决了该问题。 在这篇文章中，实现了基于哈希的解决方案。 我们计算所有元素的出现。 如果任何元素的计数大于 n / 2，我们将其返回。

因此，如果存在多数元素，那么它将是键的值。

下面是上述方法的实现：

## C++

```cpp

#include<bits/stdc++.h> 
using namespace std; 

#define ll long long int 

// function to print the majority Number 
int majorityNumber(int arr[], int n) 
{ 
    int ans = -1; 
    unordered_map<int, int>freq; 
    for (int i = 0; i < n; i++) 
    { 
        freq[arr[i]]++; 
        if (freq[arr[i]] > n / 2) 
            ans = arr[i]; 
    } 
    return ans; 
}  

// Driver code 
int main() 
{ 
    int a[] = {2, 2, 1, 1, 1, 2, 2}; 
    int n = sizeof(a) / sizeof(int); 
    cout << majorityNumber(a, n);  
    return 0; 
} 

// This code is contributed  
// by sahishelangia 

```

## Java

```java

import java.util.*; 

class GFG  
{ 

// function to print the majority Number 
static int majorityNumber(int arr[], int n) 
{ 
    int ans = -1; 
    HashMap<Integer, 
            Integer> freq = new HashMap<Integer, 
                                        Integer>(); 

    for (int i = 0; i < n; i++) 
    { 
        if(freq.containsKey(arr[i])) 
        { 
            freq.put(arr[i], freq.get(arr[i]) + 1); 
        } 
        else
        { 
            freq.put(arr[i], 1); 
        } 
        if (freq.get(arr[i]) > n / 2) 
            ans = arr[i]; 
    } 
    return ans; 
}  

// Driver code 
public static void main(String[] args)  
{ 
    int a[] = {2, 2, 1, 1, 1, 2, 2}; 
    int n = a.length; 
    System.out.println(majorityNumber(a, n)); 
} 
}  

// This code is contributed by Princi Singh 

```

## 蟒蛇

```

# function to print the  
# majorityNumber 
def majorityNumber(nums): 

    # stores the num count  
    num_count = {} 

    # iterate in the array  
    for num in nums: 

        if num in num_count: 
            num_count[num] += 1
        else: 
            num_count[num] = 1

    for num in num_count: 
        if num_count[num] > len(nums)/2: 
            return num 
    return -1

# Driver Code 
a = [2, 2, 1, 1, 1, 2, 2] 
print majorityNumber(a) 

```

## C#

```cs

// C# implementation of the approach 
using System; 
using System.Collections.Generic; 

class GFG  
{ 

// function to print the majority Number 
static int majorityNumber(int []arr, int n) 
{ 
    int ans = -1; 
    Dictionary<int, 
               int> freq = new Dictionary<int, 
                                          int>(); 

    for (int i = 0; i < n; i++) 
    { 
        if(freq.ContainsKey(arr[i])) 
        { 
            freq[arr[i]] = freq[arr[i]] + 1; 
        } 
        else
        { 
            freq.Add(arr[i], 1); 
        } 
        if (freq[arr[i]] > n / 2) 
            ans = arr[i]; 
    } 
    return ans; 
}  

// Driver code 
public static void Main(String[] args)  
{ 
    int []a = {2, 2, 1, 1, 1, 2, 2}; 
    int n = a.Length; 
    Console.WriteLine(majorityNumber(a, n)); 
} 
} 

// This code is contributed by Rajput-Ji 

```

**Output:**

```
2

```

以下是上述算法的时间和空间复杂度：-

**时间复杂度**：`O(n)`

**辅助空间**：`O(n)`



* * *

* * *



