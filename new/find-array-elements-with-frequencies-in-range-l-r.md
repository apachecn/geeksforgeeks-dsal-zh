# 查找频率范围为`[l, r]`的数组元素

> 原文：[https://www.geeksforgeeks.org/find-array-elements-with-frequencies-in-range-l-r/](https://www.geeksforgeeks.org/find-array-elements-with-frequencies-in-range-l-r/)

给定一个整数数组，请从该数组中查找其频率在`[l, r]`范围内的元素。

**示例**：

```
Input : arr[] = { 1, 2, 3, 3, 2, 2, 5 }
        l = 2, r = 3
Output : 2 3 3 2 2

```

**方法**：

*   拿一个哈希映射，它将存储数组中所有元素的频率。

*   现在，再次遍历。

*   打印其频率在`[l, r]`范围内的元素。

## C++

```cpp

// C++ program to find the elements whose 
// frequency lies in the range [l, r] 
#include "iostream" 
#include "unordered_map" 
using namespace std; 

void findElements(int arr[], int n, int l, int r) 
{ 
    // Hash map which will store the 
    // frequency of the elements of the array. 
    unordered_map<int, int> mp; 

    for (int i = 0; i < n; ++i) { 

        // Increment the frequency 
        // of the element by 1\. 
        mp[arr[i]]++; 
    } 

    for (int i = 0; i < n; ++i) { 

        // Print the element whose frequency 
        // lies in the range [l, r] 
        if (l <= mp[arr[i]] && mp[arr[i] <= r]) { 
            cout << arr[i] << " "; 
        } 
    } 
} 

int main() 
{ 
    int arr[] = { 1, 2, 3, 3, 2, 2, 5 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    int l = 2, r = 3; 
    findElements(arr, n, l, r); 
    return 0; 
} 

```

## Java

```java

import java.util.HashMap; 
import java.util.Map; 

// Java program to find the elements whose 
// frequency lies in the range [l, r] 
public class GFG { 

    static void findElements(int arr[], int n, int l, int r) { 
        // Hash map which will store the 
        // frequency of the elements of the array. 
        Map<Integer, Integer> mp = new HashMap<Integer, Integer>(); 

        for (int i = 0; i < n; ++i) { 

            // Increment the frequency 
            // of the element by 1\. 
            int a=0; 
            if(mp.get(arr[i])==null){ 
                a=1; 
            } 
            else{ 
                a = mp.get(arr[i])+1; 
            } 
            mp.put(arr[i], a); 
        } 

        for (int i = 0; i < n; ++i) { 

            // Print the element whose frequency 
            // lies in the range [l, r] 
            if (l <= mp.get(arr[i]) && (mp.get(arr[i]) <= r)) { 
                System.out.print(arr[i] + " "); 
            } 
        } 
    } 

    public static void main(String[] args) { 
        int arr[] = {1, 2, 3, 3, 2, 2, 5}; 
        int n = arr.length; 
        int l = 2, r = 3; 
        findElements(arr, n, l, r); 

    } 
} 
/*This code is contributed by PrinciRaj1992*/

```

## Python3

```py

# Python 3 program to find the elements whose 
# frequency lies in the range [l, r] 

def findElements(arr, n, l, r): 

    # Hash map which will store the 
    # frequency of the elements of the array. 
    mp = {i:0 for i in range(len(arr))} 

    for i in range(n): 

        # Increment the frequency 
        # of the element by 1\. 
        mp[arr[i]] += 1

    for i in range(n): 

        # Print the element whose frequency 
        # lies in the range [l, r] 
        if (l <= mp[arr[i]] and mp[arr[i] <= r]): 
            print(arr[i], end = " ") 

# Driver Code 
if __name__ == '__main__': 
    arr = [1, 2, 3, 3, 2, 2, 5] 
    n = len(arr) 
    l = 2
    r = 3
    findElements(arr, n, l, r) 

# This code is contributed by 
# Shashank_Sharma 

```

## C#

```cs

// C# program to find the elements whose 
// frequency lies in the range [l, r] 
using System; 
using System.Collections.Generic; 

class GFG  
{ 

    static void findElements(int []arr, int n, int l, int r) 
    { 
        // Hash map which will store the 
        // frequency of the elements of the array. 
        Dictionary<int, int> mp = new Dictionary<int, int>(); 

        for (int i = 0; i < n; ++i)  
        { 

            // Increment the frequency 
            // of the element by 1\. 
            int a = 0; 
            if(!mp.ContainsKey(arr[i])) 
            { 
                a = 1; 
            } 
            else
            { 
                a = mp[arr[i]]+1; 
            } 

            if(!mp.ContainsKey(arr[i])) 
            { 
                mp.Add(arr[i], a);  
            } 
            else
            { 
                mp.Remove(arr[i]); 
                mp.Add(arr[i], a); 
            } 
        } 

        for (int i = 0; i < n; ++i) 
        { 

            // Print the element whose frequency 
            // lies in the range [l, r] 
            if (mp.ContainsKey(arr[i]) &&  
                        l <= mp[arr[i]] && 
                        (mp[arr[i]] <= r))  
            { 
                Console.Write(arr[i] + " "); 
            } 
        } 
    } 

    // Driver code 
    public static void Main(String[] args) 
    { 
        int []arr = {1, 2, 3, 3, 2, 2, 5}; 
        int n = arr.Length; 
        int l = 2, r = 3; 
        findElements(arr, n, l, r); 

    } 
} 

// This code has been contributed by 29AjayKumar 

```

**输出**：

```
2 3 3 2 2

```

**时间复杂度**：`O(n)`。



* * *

* * *



