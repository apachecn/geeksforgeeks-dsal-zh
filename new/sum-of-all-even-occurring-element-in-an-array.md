# 数组

> 原文：[https://www.geeksforgeeks.org/sum-of-all-even-occurring-element-in-an-array/](https://www.geeksforgeeks.org/sum-of-all-even-occurring-element-in-an-array/)

中所有偶数元素的总和

给定包含重复元素的整数数组。 任务是找到给定数组中所有偶数元素的总和。 那是所有此类元素在阵列中的偶数频率之和。

**范例**：

```
Input : arr[] = {1, 1, 2, 2, 3, 3, 3}
Output : 6
The even occurring element are 1 and 2 (both occur two times). 
Therefore sum of all 1's in the array = 1+1+2+2 = 6.

Input : arr[] = {10, 20, 30, 40, 40}
Output : 80
Element with even frequency are 40.
Sum = 40.

```

**方法**：

*   遍历数组，并在 C++ 中使用 [unordered_map 存储数组元素的频率，以使 map 的键为数组元素，值为数组中的频率。](https://www.geeksforgeeks.org/unordered_map-in-stl-and-its-applications/)

*   然后，遍历映射以查找元素的频率，并检查其是否为偶数，是否为偶数，然后将该元素相加。

下面是上述方法的实现：

## C++

```cpp

// C++ program to find the sum of all even
// occurring elements in an array

#include <bits/stdc++.h>
using namespace std;

// Function to find the sum of all even
// occurring elements in an array
int findSum(int arr[], int N)
{
    // Map to store frequency of elements
    // of the array
    unordered_map<int, int> mp;

    for (int i = 0; i < N; i++) {
        mp[arr[i]]++;
    }

    // variable to stroe sum of all
    // even occurring elements
    int sum = 0;

    // loop to iteratre through map
    for (auto itr = mp.begin(); itr != mp.end(); itr++) {

        // check if frequency is even
        if (itr->second % 2 == 0)
            sum += (itr->first) * (itr->second);
    }

    return sum;
}

// Driver Code
int main()
{
    int arr[] = { 10, 20, 20, 40, 40 };

    int N = sizeof(arr) / sizeof(arr[0]);

    cout << findSum(arr, N);

    return 0;
}

```

## Java

```java

// Java program to find the sum of all even
// occurring elements in an array

import java.util.HashMap;
import java.util.Iterator;
import java.util.Map;
import java.util.Map.Entry;

public class GFG {
    public static int element(int[] arr, int n)
    {

        Map<Integer, Integer> map = new HashMap<Integer, Integer>();
        for (int i = 0; i < n; i++) {
            int count = 0;
            if (map.get(arr[i]) != null) {
                count = map.get(arr[i]);
            }
            map.put(arr[i], count + 1);
        }

        int sum = 0;
        for (Entry<Integer, Integer> entry : map.entrySet()) {
            if (entry.getValue() % 2 == 0) {
                sum += entry.getKey() * entry.getValue();
            }
        }

        return sum;
    }

    public static void main(String[] args)
    {
        int arr[] = { 1, 1, 2, 2, 3, 3, 3 };

        // sum should be = 1+1+2+2=6;
        int n = arr.length;
        System.out.println(element(arr, n));
    }
}

```

## Python3

```py

# Python3 program to find the sum 
# of all even occurring elements
# in an array 

# Function to find the sum of all even 
# occurring elements in an array 
def findSum(arr, N): 

    # Map to store frequency of 
    # elements of the array 
    mp = {} 

    for i in range(N): 
        if arr[i] in mp:
            mp[arr[i]] += 1
        else:
            mp[arr[i]] = 1

    # Variable to store sum of all 
    # even occurring elements 
    Sum = 0

    # Loop to iteratre through map 
    for first, second in mp.items():

        # Check if frequency is even 
        if (second % 2 == 0):
            Sum += (first) * (second) 

    return Sum

# Driver code    
arr = [ 10, 20, 20, 40, 40 ]

N = len(arr)

print(findSum(arr, N))

# This code is contributed by divyeshrabadiya07

```

**Output:** 

```
120

```

**时间复杂度**：`O(n)`，其中 N 是数组中元素的数量。



* * *

* * *



