# 数组

> 原文：[https://www.geeksforgeeks.org/count-of-greater-elements-for-each-element-in-the-array/](https://www.geeksforgeeks.org/count-of-greater-elements-for-each-element-in-the-array/)

中每个元素的较大元素计数

给定大小为 **N** 的整数的数组 **arr** ，任务是为每个元素查找大于它的元素数量。

**示例**：

> **输入**：arr [] = {4，6，2，1，8，7}
> **输出**：{3，2，4，5，0，1}
> 
> **输入**：arr [] = {2，3，4，5，6，7，8}
> **输出**：{6，5，4，4，3，2，1 ，0}

**方法**：使用[映射](http://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)存储每个数组元素的[频率。](https://www.geeksforgeeks.org/counting-frequencies-of-array-elements/) [反向迭代地图](https://www.geeksforgeeks.org/how-to-traverse-a-stl-map-in-reverse-direction/)，并为每个元素存储所有先前遍历的元素（即大于它的元素）的频率之和。

下面的代码是上述方法的实现：

## C++

```cpp

// C++ implementation of the above approach 

#include <bits/stdc++.h> 
using namespace std; 

void countOfGreaterElements(int arr[], int n) 
{ 
    // Store the frequency of the 
    // array elements 
    map<int, int> mp; 
    for (int i = 0; i < n; i++) { 
        mp[arr[i]]++; 
    } 

    int x = 0; 
    // Store the sum of frequency of elements 
    // greater than the current eleement 
    for (auto it = mp.rbegin(); it != mp.rend(); it++) { 
        int temp = it->second; 
        mp[it->first] = x; 
        x += temp; 
    } 

    for (int i = 0; i < n; i++) 
        cout << mp[arr[i]] << " "; 
} 

// Driver code 
int main() 
{ 

    int arr[] = { 7, 9, 5, 2, 1, 3, 4, 8, 6 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 

    countOfGreaterElements(arr, n); 

    return 0; 
} 

```

## Java

```java

// Java implementation of the above approach 
import java.util.*; 

class GfG { 
    public static void countOfGreaterElements(int arr[]) 
    { 
        int n = arr.length; 

        TreeMap<Integer, Integer> mp = new TreeMap<Integer, Integer>(Collections.reverseOrder()); 

        // Store the frequency of the 
        // array elements 
        for (int i = 0; i < n; i++) { 
            mp.put(arr[i], mp.getOrDefault(arr[i], 0) + 1); 
        } 

        // Store the sum of frequency of elements 
        // greater than the current eleement 
        int x = 0; 
        for (Map.Entry<Integer, Integer> e : mp.entrySet()) { 
            Integer temp = e.getValue(); 
            mp.put(e.getKey(), x); 
            x += temp; 
        } 

        for (int i = 0; i < n; i++) 
            System.out.print(mp.get(arr[i]) + " "); 
    } 

    public static void main(String args[]) 
    { 
        int arr[] = { 7, 9, 5, 2, 1, 3, 4, 8, 6 }; 
        countOfGreaterElements(arr); 
    } 
} 

```

## Python 3

```

# Python 3 implementation of the above approach 

def countOfGreaterElements(arr, n): 
    # Store the frequency of the 
    # array elements 
    mp = {i:0 for i in range(1000)} 
    for i in range(n): 
        mp[arr[i]] += 1

    x = 0
    # Store the sum of frequency of elements 
    # greater than the current eleement 
    p = [] 
    q = [] 
    m = [] 
    for key, value in mp.items(): 
        m.append([key, value]) 
    m = m[::-1] 

    for p in m: 
        temp = p[1] 
        mp[p[0]] = x 
        x += temp 

    for i in range(n): 
        print(mp[arr[i]], end = " ") 

# Driver code 
if __name__ == '__main__': 
    arr = [7, 9, 5, 2, 1, 3, 4, 8, 6] 
    n = len(arr) 

    countOfGreaterElements(arr, n) 

# This code is contributed by Surendra_Gangwar 

```

**Output:**

```
2 0 4 7 8 6 5 1 3

```

***时间复杂度**：`O(n)`*



* * *

* * *



