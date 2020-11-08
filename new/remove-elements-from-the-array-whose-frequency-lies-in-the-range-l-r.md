# 从频率为`[l, r]`范围的数组中删除元素

> 原文：[https://www.geeksforgeeks.org/remove-elements-from-the-array-whose-frequency-lies-in-the-range-l-r/](https://www.geeksforgeeks.org/remove-elements-from-the-array-whose-frequency-lies-in-the-range-l-r/)

给定一个整数数组，请从该数组中删除其频率在`[l, r]`范围内的元素。

**示例**：

> 输入：`arr[] = {1, 2, 3, 3, 2, 2, 5}, l = 2, r = 3`
>
> 输出：`1 5`
>
> 我们删除所有频率从 2 至 5 的元素 。
> 
> 输入：`arr[] = {1, 2, 3, 3, 3, 3}, l = 2, r = 3`
>
> 输出：`3 3 3 3`

**方法**：

*   拿一个哈希映射，它将存储数组中所有元素的频率。

*   现在，再次遍历。

*   删除频率在`[l, r]`之间的元素。

*   否则，打印它。

## C++

```cpp

// C++ program to remove the elements whose 
// frequency appears in the range [l, r] 
#include "iostream" 
#include "unordered_map" 
using namespace std; 

void removeElements(int arr[], int n, int l, int r) 
{ 
    // Hash map which will store the 
    // frequency of the elements of the array. 
    unordered_map<int, int> mp; 

    for (int i = 0; i < n; ++i) { 

        // Incrementing the frequency 
        // of the element by 1\. 
        mp[arr[i]]++; 
    } 

    for (int i = 0; i < n; ++i) { 

        // Print the element whose frequency 
        // is not in the range [l, r] 
        if (mp[arr[i]] < l or mp[arr[i] > r]) { 
            cout << arr[i] << " "; 
        } 
    } 
} 

int main() 
{ 
    int arr[] = { 1, 2, 3, 3, 2, 2, 5 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    int l = 2, r = 3; 
    removeElements(arr, n, l, r); 
    return 0; 
} 

```

## Java

```java

// Java program to remove the elements whose 
// frequency appears in the range [l, r] 
import java.util.HashMap; 

class GFG { 

    static void removeElements(int arr[], int n, int l, int r) 
    { 
        // Hash map which will store the 
        // frequency of the elements of the array. 
        HashMap<Integer, Integer> mp = new HashMap<>(); 

        for (int i = 0; i < n; ++i) { 

            // Incrementing the frequency 
            // of the element by 1\. 
            // mp[arr[i]]++; 
            int val = 0; 
            if (mp.get(arr[i]) == null) { 
                val = 1; 
            } 
            else { 
                val = mp.get(arr[i]) + 1; 
            } 
            // System.out.println("--"+mp.get(arr[i])); 
            mp.put(arr[i], val); 
        } 

        for (int i = 0; i < n; ++i) { 

            // Print the element whose frequency 
            // is not in the range [l, r] 
            if (mp.get(arr[i]) < l || mp.get(arr[i]) > r) { 
                System.out.print(arr[i] + " "); 
            } 
        } 
    } 

    // Driver code 
    public static void main(String args[]) 
    { 
        int arr[] = { 1, 2, 3, 3, 2, 2, 5 }; 
        int n = arr.length; 
        int l = 2, r = 3; 
        removeElements(arr, n, l, r); 
    } 
} 

// This code is contributed by 29AjayKumar 

```

## Python3

```py

# Python 3 program to remove the elements  
# whose frequency appears in the range [l, r] 

def removeElements(arr, n, l, r): 

    # Hash map which will store the 
    # frequency of the elements of the array. 
    mp = {i:0 for i in range(len(arr))} 

    for i in range(n): 

        # Incrementing the frequency 
        # of the element by 1\. 
        mp[arr[i]] += 1

    for i in range(n): 

        # Print the element whose frequency 
        # is not in the range [l, r] 
        if (mp[arr[i]] < l or mp[arr[i] > r]): 
            print(arr[i], end = " ") 

# Driver Code 
if __name__ == '__main__': 
    arr = [1, 2, 3, 3, 2, 2, 5] 
    n = len(arr) 
    l = 2
    r = 3
    removeElements(arr, n, l, r); 

# This code is contributed by 
# Sahil_Shelangia 

```

## C#

```cs

// C# program to remove the elements whose 
// frequency appears in the range [l, r] 
using System; 
using System.Collections.Generic; 

class GFG { 

    static void removeElements(int[] arr, int n, int l, int r) 
    { 
        // Hash map which will store the 
        // frequency of the elements of the array. 
        Dictionary<int, int> mp = new Dictionary<int, int>(); 

        for (int i = 0; i < n; ++i) { 

            // Incrementing the frequency 
            // of the element by 1\. 
            // mp[arr[i]]++; 
            int val = 0; 
            if (!mp.ContainsKey(arr[i])) { 
                val = 1; 
            } 
            else { 
                val = mp[arr[i]] + 1; 
            } 
            if (!mp.ContainsKey(arr[i])) 
                mp.Add(arr[i], val); 
            else { 
                mp.Remove(arr[i]); 
                mp.Add(arr[i], val); 
            } 
        } 

        for (int i = 0; i < n; ++i) { 

            // Print the element whose frequency 
            // is not in the range [l, r] 
            if (mp[arr[i]] < l || mp[arr[i]] > r) { 
                Console.Write(arr[i] + " "); 
            } 
        } 
    } 

    // Driver code 
    public static void Main(String[] args) 
    { 
        int[] arr = { 1, 2, 3, 3, 2, 2, 5 }; 
        int n = arr.Length; 
        int l = 2, r = 3; 
        removeElements(arr, n, l, r); 
    } 
} 

// This code contributed by Rajput-Ji 

```

**Output:**

```
1 5

```

**时间复杂度–**`O(n)`



* * *

* * *



