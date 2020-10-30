# 在第一个数组中存在元素, 但在第二个数组中不存在

> 原文：[https://www.geeksforgeeks.org/count-elements-present-in-first-array-but-not-in-second/](https://www.geeksforgeeks.org/count-elements-present-in-first-array-but-not-in-second/)

给定两个分别为大小`M`和`N`的数组（可能会排序, 也可能不会排序）。 这样的数组使得它们中可能包含一些公共元素。 您需要计算出现在第一个数组中而不是第二个数组中的元素的数量。

**示例**：

> 输入：
>
> `arr1[] = {41, 43, 45, 50}, M = 4`
>
> `arr2[] = {55, 67, 65, 61, 62}, N = 5`
>
> 输出：4
>
> 说明：
>
> `arr1[]`包含频率均为 1 的 41、43、45、50
>
> `arr2[]`不包含任何在两者中都通用的元素, 因此计数为 4
> 
> 输入：
>
> `arr1[] = {40, 45, 56, 60}, M = 4`
>
> `arr2[] = {40, 45, 56,58}, N = 4`
>
> 输出：1
>
> 说明：
>
> `arr1[]`包含 40、45、56、60, 频率全部为 1
>
> `arr2[]`包含 3 个`arr1[]`中的元素，40、45、56
>
> 但不包含 60，因此计数为 1

想法是使用哈希映射, 并在第一个数组中保留数字的频率计数。 在遍历第二个数组时, 减少遇到的每个整数在映射中的计数。 现在计算频率大于 0 的元素, 否则返回 0。

## C++

```cpp

// C++ to count number of elements present in arr1 whose 
// occurrence is more than in arr2 
#include <bits/stdc++.h> 
using namespace std; 

int Largercount(int arr1[], int arr2[], int m, int n) 
{ 
    bool f = false; 
    int count = 0; 

    // map to store frequency of elements present in arr1 
    unordered_map<int, int> mp; 

    // frequency of elements of arr1 is calulated 
    for (int i = 0; i < m; i++) 
        mp[arr1[i]]++; 

    // check if the elements of arr2 
    // is present in arr2 or not 
    for (int i = 0; i < n; i++) 
        if (mp.find(arr2[i]) != mp.end() && mp[arr2[i]] != 0) 
            mp[arr2[i]]--; 

    // count the elements of arr1 whose 
    // frequency is more than arr2 
    for (int i = 0; i < m; i++) { 
        if (mp[arr1[i]] != 0) { 
            count++; 
            mp[arr1[i]] = 0; 
        } 
    } 

    return count; 
} 

// Driver code 
int main() 
{ 
    int arr1[] = { 2, 4, 4, 6, 6, 6, 8, 9 }; 
    int arr2[] = { 2, 2, 4, 6, 6 }; 
    cout << Largercount(arr1, arr2, 8, 5); 
    return 0; 
} 

```

## Java

```java

// Java to count number of elements present in arr1 whose 
// occurrence is more than in arr2 
import java.util.*; 
import java.lang.*; 
import java.io.*; 

class GFG { 
    public static int Largercount(int arr1[], int arr2[], int m, int n) 
    { 
        int count = 0; 

        // map to store frequency of elements present in arr1 
        HashMap<Integer, Integer> mp = new HashMap<Integer, Integer>(); 

        // frequency of elements of arr1 is calulated 
        for (int i = 0; i < m; i++) { 
            int key = arr1[i]; 
            if (mp.containsKey(key)) { 
                int freq = mp.get(key); 
                freq++; 
                mp.put(key, freq); 
            } 
            else
                mp.put(key, 1); 
        } 

        // check if the elements of arr2 is present in arr2 or not 
        for (int i = 0; i < n; i++) { 
            if (mp.containsKey(arr2[i]) && mp.get(arr2[i]) != 0) { 
                int freq = mp.get(arr2[i]); 
                freq--; 
                mp.put(arr2[i], freq); 
            } 
        } 

        // count the elements of arr1 whose 
        // frequency is more than arr2 
        for (int i = 0; i < m; i++) { 
            if (mp.get(arr1[i]) != 0) { 
                count++; 
                mp.put(arr1[i], 0); 
            } 
        } 

        return count; 
    } 

    // Driver code 
    public static void main(String[] args) 
    { 
        int arr1[] = new int[] { 2, 4, 4, 6, 6, 6, 8, 9}; 
        int arr2[] = new int[] { 2, 2, 4, 6, 6 }; 

        System.out.print(Largercount(arr1, arr2, 8, 5)); 
    } 
} 

```

## Python3

```py

# Python3 to count number of elements  
# present in arr1 whose occurrence is 
# more than in arr2 
def Largercount(arr1, arr2, m, n): 

    count = 0

    # map to store frequency of 
    # elements present in arr1 
    mp=dict() 

    # frequency of elements of arr1  
    # is calulated 
    for i in range(m): 
        mp[arr1[i]] = mp.get(arr1[i], 0) + 1

    # check if the elements of arr2 
    # is present in arr2 or not 
    for i in range(n): 
        if (arr2[i] in mp.keys() and 
                       mp[arr2[i]] != 0): 
            mp[arr2[i]] -= 1

    # count the elements of arr1 whose 
    # frequency is more than arr2 
    for i in range(m): 
        if (mp[arr1[i]] != 0): 
            count += 1
            mp[arr1[i]] = 0

    return count 

# Driver code 
arr1 = [2, 4, 4, 6, 6, 6, 8, 9] 
arr2 = [2, 2, 4, 6, 6 ] 
print(Largercount(arr1, arr2, 8, 5)) 

# This code is contributed by mohit kumar 

```

## C#

```cs

// C# to count number of elements 
// present in arr1 whose occurrence 
// is more than in arr2  
using System; 
using System.Collections.Generic; 

class GFG 
{ 
public static int Largercount(int[] arr1, 
                              int[] arr2,  
                              int m, int n) 
{ 
    int count = 0; 

    // map to store frequency of 
    // elements present in arr1  
    Dictionary<int,  
               int> mp = new Dictionary<int,  
                                        int>(); 

    // frequency of elements  
    // of arr1 is calulated  
    for (int i = 0; i < m; i++) 
    { 
        int key = arr1[i]; 
        if (mp.ContainsKey(key)) 
        { 
            int freq = mp[key]; 
            freq++; 
            mp[key] = freq; 
        } 
        else
        { 
            mp[key] = 1; 
        } 
    } 

    // check if the elements of arr2  
    // is present in arr2 or not  
    for (int i = 0; i < n; i++) 
    { 
        if (mp.ContainsKey(arr2[i]) &&  
                  mp[arr2[i]] != 0) 
        { 
            int freq = mp[arr2[i]]; 
            freq--; 
            mp[arr2[i]] = freq; 
        } 
    } 

    // count the elements of arr1 whose  
    // frequency is more than arr2  
    for (int i = 0; i < m; i++) 
    { 
        if (mp[arr1[i]] != 0) 
        { 
            count++; 
            mp[arr1[i]] = 0; 
        } 
    } 

    return count; 
} 

// Driver code  
public static void Main(string[] args) 
{ 
    int[] arr1 = new int[] {2, 4, 4, 6, 
                            6, 6, 8, 9}; 
    int[] arr2 = new int[] {2, 2, 4, 6, 6}; 

    Console.Write(Largercount(arr1, arr2, 8, 5)); 
} 
} 

// This code is contributed by Shrikant13 

```

**Output:**

```
4

```

**时间复杂度**：`O(m + n)`



* * *

* * *



