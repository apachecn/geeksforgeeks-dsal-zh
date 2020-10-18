# 数组中最频繁的元素

> 原文： [https://www.geeksforgeeks.org/frequent-element-array/](https://www.geeksforgeeks.org/frequent-element-array/)

给定一个数组，找到其中最频繁的元素。 如果有多个元素出现的次数最多，请打印其中的任何一个。

**示例**：

```
Input : arr[] = {1, 3, 2, 1, 4, 1}
Output : 1
1 appears three times in array which
is maximum frequency.

Input : arr[] = {10, 20, 10, 20, 30, 20, 20}
Output : 20

```



一个简单的**解决方案**是运行两个循环。 外循环一一挑选所有元素。 内循环找到所拾取元素的频率，并与迄今为止的最大值进行比较。 该解决方案的时间复杂度为`O(n^2)`。

更好的**解决方案**是进行排序。 我们首先对数组进行排序，然后线性遍历数组。

## C++ 

```cpp

// CPP program to find the most frequent element 
// in an array. 
#include <bits/stdc++.h> 
using namespace std; 

int mostFrequent(int arr[], int n) 
{ 
    // Sort the array 
    sort(arr, arr + n); 

    // find the max frequency using linear traversal 
    int max_count = 1, res = arr[0], curr_count = 1; 
    for (int i = 1; i < n; i++) { 
        if (arr[i] == arr[i - 1]) 
            curr_count++; 
        else { 
            if (curr_count > max_count) { 
                max_count = curr_count; 
                res = arr[i - 1]; 
            } 
            curr_count = 1; 
        } 
    } 

    // If last element is most frequent 
    if (curr_count > max_count) 
    { 
        max_count = curr_count; 
        res = arr[n - 1]; 
    } 

    return res; 
} 

// driver program 
int main() 
{ 
    int arr[] = { 1, 5, 2, 1, 3, 2, 1 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    cout << mostFrequent(arr, n); 
    return 0; 
} 

```

## Java

```java

//Java program to find the most frequent element 
//in an array 
import java.util.*; 

class GFG { 

    static int mostFrequent(int arr[], int n) 
    { 

        // Sort the array 
        Arrays.sort(arr); 

        // find the max frequency using linear 
        // traversal 
        int max_count = 1, res = arr[0]; 
        int curr_count = 1; 

        for (int i = 1; i < n; i++) 
        { 
            if (arr[i] == arr[i - 1]) 
                curr_count++; 
            else 
            { 
                if (curr_count > max_count) 
                { 
                    max_count = curr_count; 
                    res = arr[i - 1]; 
                } 
                curr_count = 1; 
            } 
        } 

        // If last element is most frequent 
        if (curr_count > max_count) 
        { 
            max_count = curr_count; 
            res = arr[n - 1]; 
        } 

        return res; 
    } 

    // Driver program 
    public static void main (String[] args) { 

        int arr[] = {1, 5, 2, 1, 3, 2, 1}; 
        int n = arr.length; 

        System.out.println(mostFrequent(arr,n)); 

    } 
} 

// This code is contributed by Akash Singh. 

```

## Python3

```py

# Python3 program to find the most  
# frequent element in an array. 

def mostFrequent(arr, n): 

    # Sort the array 
    arr.sort() 

    # find the max frequency using 
    # linear traversal 
    max_count = 1; res = arr[0]; curr_count = 1

    for i in range(1, n):  
        if (arr[i] == arr[i - 1]): 
            curr_count += 1

        else : 
            if (curr_count > max_count):  
                max_count = curr_count 
                res = arr[i - 1] 

            curr_count = 1

    # If last element is most frequent 
    if (curr_count > max_count): 

        max_count = curr_count 
        res = arr[n - 1] 

    return res 

# Driver Code 
arr = [1, 5, 2, 1, 3, 2, 1]  
n = len(arr) 
print(mostFrequent(arr, n)) 

# This code is contributed by Smitha Dinesh Semwal. 

```

## C# 

```cs

// C# program to find the most  
// frequent element in an array 
using System; 

class GFG { 

    static int mostFrequent(int []arr, int n) 
    { 

        // Sort the array 
        Array.Sort(arr); 

        // find the max frequency using  
        // linear traversal 
        int max_count = 1, res = arr[0]; 
        int curr_count = 1; 

        for (int i = 1; i < n; i++) 
        { 
            if (arr[i] == arr[i - 1]) 
                curr_count++; 
            else
            { 
                if (curr_count > max_count) 
                { 
                    max_count = curr_count; 
                    res = arr[i - 1]; 
                } 
                curr_count = 1; 
            } 
        } 

        // If last element is most frequent 
        if (curr_count > max_count) 
        { 
            max_count = curr_count; 
            res = arr[n - 1]; 
        } 

        return res; 
    } 

    // Driver code 
    public static void Main ()  
    { 

        int []arr = {1, 5, 2, 1, 3, 2, 1}; 
        int n = arr.Length; 

        Console.WriteLine(mostFrequent(arr,n)); 

    } 
} 

// This code is contributed by vt_m. 

```

## PHP

```php

<?php 
// PHP program to find the 
// most frequent element 
// in an array. 

function mostFrequent( $arr, $n) 
{ 

    // Sort the array 
    sort($arr); 
    sort($arr , $n); 

    // find the max frequency  
    // using linear traversal 
    $max_count = 1;  
    $res = $arr[0];  
    $curr_count = 1; 
    for ($i = 1; $i < $n; $i++)  
    { 
        if ($arr[$i] == $arr[$i - 1]) 
            $curr_count++; 
        else 
        { 
            if ($curr_count > $max_count) 
            { 
                $max_count = $curr_count; 
                $res = $arr[$i - 1]; 
            } 
            $curr_count = 1; 
        } 
    } 

    // If last element  
    // is most frequent 
    if ($curr_count > $max_count) 
    { 
        $max_count = $curr_count; 
        $res = $arr[$n - 1]; 
    } 

    return $res; 
} 

// Driver Code 
{ 
    $arr = array(1, 5, 2, 1, 3, 2, 1); 
    $n = sizeof($arr) / sizeof($arr[0]); 
    echo mostFrequent($arr, $n); 
    return 0; 
} 

// This code is contributed by nitin mittal 
?> 

```

**输出**：

```
1

```

时间复杂度：`O(N log N)`。

辅助空间：`O(1)`。

**有效解决方案**是使用哈希。 我们创建一个哈希表，并将元素及其频率计数存储为键值对。 最后，我们遍历哈希表并打印具有最大值的键。

## C++

```

// CPP program to find the most frequent element 
// in an array. 
#include <bits/stdc++.h> 
using namespace std; 

int mostFrequent(int arr[], int n) 
{ 
    // Insert all elements in hash. 
    unordered_map<int, int> hash; 
    for (int i = 0; i < n; i++) 
        hash[arr[i]]++; 

    // find the max frequency 
    int max_count = 0, res = -1; 
    for (auto i : hash) { 
        if (max_count < i.second) { 
            res = i.first; 
            max_count = i.second; 
        } 
    } 

    return res; 
} 

// driver program 
int main() 
{ 
    int arr[] = { 1, 5, 2, 1, 3, 2, 1 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    cout << mostFrequent(arr, n); 
    return 0; 
} 

```