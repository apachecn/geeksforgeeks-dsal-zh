# 查找是否有一个总和为 0 的子数组

> 原文： [https://www.geeksforgeeks.org/find-if-there-is-a-subarray-with-0-sum/](https://www.geeksforgeeks.org/find-if-there-is-a-subarray-with-0-sum/)

给定一个正负数数组，请查找是否存在一个总和为 0 的子数组（大小至少为一个）。

**示例**：

```
Input: {4, 2, -3, 1, 6}
Output: true 
There is a subarray with zero sum from index 1 to 3.

Input: {4, 2, 0, 1, 6}
Output: true 
There is a subarray with zero sum from index 2 to 2.

Input: {-3, 2, 3, 1, 6}
Output: false
There is no subarray with zero sum.

```



**简单解决方案**是一个个地考虑所有子数组，并检查每个子数组的总和。 我们可以运行两个循环：外部循环选择起始点`i`，内部循环尝试从`i`开始的所有子数组（有关实现，请参见[这里](https://www.geeksforgeeks.org/find-subarray-with-given-sum/)）。 该方法的时间复杂度为 `O(n^2)`。

我们还可以**使用哈希**。 想法是遍历数组，对于每个元素`arr[i]`，计算从 0 到`i`的元素总和（这可以简单地通过`sum += arr[i]`来完成）。 如果当前总和是以前看过的，则有一个零总和数组。 散列用于存储总和值，以便我们可以快速存储总和并找出当前总和是否之前被查看过。

范例：

```
arr[] = {1, 4, -2, -2, 5, -4, 3}

If we consider all prefix sums, we can
notice that there is a subarray with 0
sum when :
1) Either a prefix sum repeats or
2) Or prefix sum becomes 0.

Prefix sums for above array are:
1, 5, 3, 1, 6, 2, 5

Since prefix sum 1 repeats, we have a subarray
with 0 sum. 

```

以下是上述方法的实现。

## C++ 

```cpp

// A C++ program to find if there is a zero sum 
// subarray 
#include <bits/stdc++.h> 
using namespace std; 

bool subArrayExists(int arr[], int n) 
{ 
    unordered_set<int> sumSet; 

    // Traverse through array and store prefix sums 
    int sum = 0; 
    for (int i = 0 ; i < n ; i++) 
    { 
        sum += arr[i]; 

        // If prefix sum is 0 or it is already present 
        if (sum == 0 || sumSet.find(sum) != sumSet.end()) 
            return true; 

        sumSet.insert(sum); 
    } 
    return false; 
} 

// Driver code 
int main() 
{ 
    int arr[] =  {-3, 2, 3, 1, 6}; 
    int n = sizeof(arr)/sizeof(arr[0]); 
    if (subArrayExists(arr, n)) 
        cout << "Found a subarray with 0 sum"; 
    else
        cout << "No Such Sub Array Exists!"; 
    return 0; 
} 

```

## Java

```
// A Java program to find if there is a zero sum subarray 
import java.util.Set;  
import java.util.HashSet; 
  
class ZeroSumSubarray { 
      
    // Returns true if arr[] has a subarray with sero sum 
    static Boolean subArrayExists(int arr[]) 
    { 
        // Creates an empty hashset hs 
        Set<Integer> hs = new HashSet<Integer>();  
          
        // Initialize sum of elements 
        int sum = 0;      
          
        // Traverse through the given array 
        for (int i = 0; i < arr.length; i++) 
        {  
            // Add current element to sum 
            sum += arr[i]; 
              
            // Return true in following cases 
            // a) Current element is 0 
            // b) sum of elements from 0 to i is 0 
            // c) sum is already present in hash map 
            if (arr[i] == 0 || sum == 0 || hs.contains(sum))                          
                return true; 
              
            // Add sum to hash set 
            hs.add(sum); 
        }  
          
        // We reach here only when there is 
        // no subarray with 0 sum 
        return false; 
    }      
      
    // driver code 
    public static void main(String arg[]) 
    { 
        int arr[] = {-3, 2, 3, 1, 6}; 
        if (subArrayExists(arr)) 
            System.out.println("Found a subarray with 0 sum"); 
        else
            System.out.println("No Such Sub Array Exists!");          
    }          
}
```

## Python3

```
# A python program to find if  
# there is a zero sum subarray  
  
def subArrayExists(arr,n): 
    # traverse through array  
    # and store prefix sums  
    n_sum = 0
    s = set() 
  
    for i in range(n): 
        n_sum += arr[i] 
  
        # If prefix sum is 0 or  
        # it is already present  
        if n_sum == 0 or n_sum in s: 
            return True
        s.add(n_sum) 
  
    return False
  
# Driver code 
arr = [-3, 2, 3, 1, 6]     
n = len(arr) 
if subArrayExists(arr, n) == True: 
    print("Found a sunbarray with 0 sum") 
else: 
    print("No Such sub array exits!") 
  
# This code is contributed by Shrikant13
```

## C#

```
// A C# program to find if there  
// is a zero sum subarray  
using System; 
using System.Collections.Generic; 
  
class GFG 
{ 
    // Returns true if arr[] has  
    // a subarray with sero sum  
    static bool SubArrayExists(int[] arr) 
    { 
        // Creates an empty HashSet hM  
        HashSet<int> hs = new HashSet<int>(); 
        // Initialize sum of elements  
        int sum = 0; 
  
        // Traverse through the given array  
        for (int i = 0; i < arr.Length; i++) 
        { 
            // Add current element to sum  
            sum += arr[i]; 
  
            // Return true in following cases  
            // a) Current element is 0  
            // b) sum of elements from 0 to i is 0  
            // c) sum is already present in hash set  
            if (arr[i] == 0 || sum == 0 || hs.Contains(sum)) 
                return true; 
  
            // Add sum to hash set  
            hs.Add(sum); 
        } 
  
        // We reach here only when there is  
        // no subarray with 0 sum  
        return false; 
    } 
  
    // Main Method 
    public static void Main() 
    { 
        int[] arr = { -3, 2, 3, 1, 6 }; 
        if (SubArrayExists(arr)) 
            Console.WriteLine("Found a subarray with 0 sum"); 
        else
            Console.WriteLine("No Such Sub Array Exists!"); 
    } 
}
```

输出：

```
No Such Sub Array Exists!
```

在我们具有良好的哈希函数（允许在`O(1)`时间内进行插入和检索操作）的假设下，该解决方案的时间复杂度可以视为`O(n)`。

练习：扩展上述程序，以打印总和为 0 的所有子数组的开始和结束索引。