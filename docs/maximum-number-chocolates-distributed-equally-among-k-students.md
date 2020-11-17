# 在`K`名学生中平均分配的最大巧克力数量

> 原文：[https://www.geeksforgeeks.org/maximum-number-chocolates-distributed-equally-among-k-students/](https://www.geeksforgeeks.org/maximum-number-chocolates-distributed-equally-among-k-students/)

给定`n`个盒子，其中装有一些排成一行的巧克力。 学生人数`k`。 问题是，通过从给定批次中选择连续的盒子序列，在`k`学生中平均分配最大数量的巧克力。 考虑将盒子排列成从左到右从 1 到`n`的数字。 我们必须选择一组连续的盒子，它们可以为所有`k`学生平均提供最大数量的巧克力。 给出数组`arr[]`来表示框的行排列，而`arr[i]`表示该框中位置`i`的巧克力数量。

**示例**：

```
Input : arr[] = {2, 7, 6, 1, 4, 5}, k = 3
Output : 6
The subarray is {7, 6, 1, 4} with sum 18.
Equal distribution of 18 chocolates among
3 students is 6.
Note that the selected boxes are in consecutive order
with indexes {1, 2, 3, 4}.

```

**来源**：在亚马逊问。

问题是找到可被`k`整除的最大和子数组，然后返回`sum / k`。

**方法 1（朴素方法）**：考虑所有子数组的总和。 选择最大和。 使其为`maxSum`。 返回`maxSum / k`。 时间复杂度为`O(N ^ 2)`。

**方法 2（有效方法）**：创建数组`sum[]`，其中`sum[i]`存储`sum(arr[0] + .. arr[i])`。 创建一个具有作为`ele, idx`的元组的哈希表，其中`ele`表示`sum[i] % k`的元素，而`idx`表示从左到右遍历数组`sum[]`时元素的第一次出现的索引。 现在，从 0 到`n`遍历`sum[i]`，然后执行以下步骤。

1.  计算当前余数为`curr_rem = sum[i] % k`。

2.  如果`curr_rem == 0`，则检查`maxSum < sum[i]`，更新`maxSum = sum[i]`。

3.  否则，如果哈希表中没有`curr_rem`，则在哈希表中创建元组`curr_rem, i`。

4.  否则，获取与哈希表中的`curr_rem`相关的值。 使其为`idx`。 现在，如果`maxSum < (sum[i] – sum[idx])`，则更新`maxSum = sum[i] – sum[idx]`。

最后，返回`maxSum / k`。

**解释**：

如果`sum [i] % k == sum[j] % k`，其中`sum[i] = sum(arr[0] + .. + arr[i])`和`sum[j] = sum(arr[0] + .. + arr[j])`且`i`小于`j`，则`sum(arr[i + 1] + .. + arr[j])`必须被`k`整除。

## C++

```cpp

// C++ implementation to find the maximum number 
// of chocolates to be distributed equally among 
// k students 
#include <bits/stdc++.h> 
using namespace std; 

// function to find the maximum number of chocolates 
// to be distributed equally among k students 
int maxNumOfChocolates(int arr[], int n, int k) 
{ 
    // unordered_map 'um' implemented as 
    // hash table 
    unordered_map<int, int> um; 

    // 'sum[]' to store cumulative sum, where 
    // sum[i] = sum(arr[0]+..arr[i]) 
    int sum[n], curr_rem; 

    // to store sum of sub-array having maximum sum 
    int maxSum = 0; 

    // building up 'sum[]' 
    sum[0] = arr[0]; 
    for (int i = 1; i < n; i++) 
        sum[i] = sum[i - 1] + arr[i]; 

    // traversing 'sum[]' 
    for (int i = 0; i < n; i++) { 

        // finding current remainder 
        curr_rem = sum[i] % k; 

        // if true then sum(0..i) is divisible 
        // by k 
        if (curr_rem == 0) { 
            // update 'maxSum' 
            if (maxSum < sum[i]) 
                maxSum = sum[i]; 
        } 

        // if value 'curr_rem' not present in 'um' 
        // then store it in 'um' with index of its 
        // first occurrence 
        else if (um.find(curr_rem) == um.end()) 
            um[curr_rem] = i; 

        else
            // if true, then update 'max' 
            if (maxSum < (sum[i] - sum[um[curr_rem]])) 
            maxSum = sum[i] - sum[um[curr_rem]]; 
    } 

    // required maximum number of chocolates to be 
    // distributed equally among 'k' students 
    return (maxSum / k); 
} 

// Driver program to test above 
int main() 
{ 
    int arr[] = { 2, 7, 6, 1, 4, 5 }; 
    int n = sizeof(arr) / sizeof(arr[0]); 
    int k = 3; 
    cout << "Maximum number of chocolates: "
         << maxNumOfChocolates(arr, n, k); 
    return 0; 
} 

```

## Java

```java

// Java implementation to find the maximum number 
// of chocolates to be distributed equally among 
// k students 
import java.io.*; 
import java.util.*; 
class GFG { 
// Function to find the maximum number of chocolates 
// to be distributed equally among k students 
static int maxNumOfChocolates(int arr[], int n, int k) 
{ 
    // Hash table 
    HashMap <Integer,Integer> um = new HashMap<Integer,Integer>(); 

    // 'sum[]' to store cumulative sum, where 
    // sum[i] = sum(arr[0]+..arr[i]) 
    int[] sum=new int[n]; 
    int curr_rem; 

    // To store sum of sub-array having maximum sum 
    int maxSum = 0; 

    // Building up 'sum[]' 
    sum[0] = arr[0]; 
    for (int i = 1; i < n; i++) 
        sum[i] = sum[i - 1] + arr[i]; 

    // Traversing 'sum[]' 
    for (int i = 0; i < n; i++) { 

        // Finding current remainder 
        curr_rem = sum[i] % k; 

        // If true then sum(0..i) is divisible 
        // by k 
        if (curr_rem == 0) { 
            // update 'maxSum' 
            if (maxSum < sum[i]) 
                maxSum = sum[i]; 
        } 

        // If value 'curr_rem' not present in 'um' 
        // then store it in 'um' with index of its 
        // first occurrence 
        else if (!um.containsKey(curr_rem) ) 
            um.put(curr_rem , i); 

        else
            // If true, then update 'max' 
            if (maxSum < (sum[i] - sum[um.get(curr_rem)])) 
            maxSum = sum[i] - sum[um.get(curr_rem)]; 
    } 

    // Required maximum number of chocolates to be 
    // distributed equally among 'k' students 
    return (maxSum / k); 
} 

// Driver Code 
public static void main(String[] args) 
{ 
int arr[] = { 2, 7, 6, 1, 4, 5 }; 
int n = arr.length; 
int k = 3; 
System.out.println("Maximum number of chocolates: "
                    + maxNumOfChocolates(arr, n, k)); 
} 
    } 

// This code is contributed by 'Gitanjali'. 

```

## Python3

```py

# Python3 implementation to  
# find the maximum number 
# of chocolates to be  
# distributed equally 
# among k students 

# function to find the 
# maximum number of chocolates 
# to be distributed equally 
# among k students 
def maxNumOfChocolates(arr, n, k): 

    um, curr_rem, maxSum = {}, 0, 0

    # 'sm[]' to store cumulative sm, 
    # where sm[i] = sm(arr[0]+..arr[i]) 
    sm = [0]*n 
    sm[0] = arr[0] 

    # building up 'sm[]' 
    for i in range(1, n): 
        sm[i] = sm[i - 1] + arr[i] 

    # traversing 'sm[]' 
    for i in range(n): 

        # finding current remainder 
        curr_rem = sm[i] % k 

        if (not curr_rem and maxSum < sm[i]) :  
            maxSum = sm[i] 
        elif (not curr_rem in um) : 
            um[curr_rem] = i 
        elif (maxSum < (sm[i] - sm[um[curr_rem]])): 
              maxSum = sm[i] - sm[um[curr_rem]] 

    return maxSum//k 

# Driver program to test above 
arr = [ 2, 7, 6, 1, 4, 5 ] 
n, k = len(arr), 3

print("Maximum number of chocolates: " +
     str(maxNumOfChocolates(arr, n, k))) 

# This code is contributed by Ansu Kumari 

```

## C#

```cs

// C# implementation to find  
// the maximum number of  
// chocolates to be distributed  
// equally among k students 
using System; 
using System.Collections.Generic; 

class GFG  
{ 
    // Function to find the  
    // maximum number of  
    // chocolates to be distributed  
    // equally among k students 
    static int maxNumOfChocolates(int []arr,  
                                  int n, int k) 
    { 
        // Hash table 
        Dictionary <int, int> um =  
                    new Dictionary<int, int>(); 

        // 'sum[]' to store cumulative  
        // sum, where sum[i] =  
        // sum(arr[0]+..arr[i]) 
        int[] sum = new int[n]; 
        int curr_rem; 

        // To store sum of sub-array 
        // having maximum sum 
        int maxSum = 0; 

        // Building up 'sum[]' 
        sum[0] = arr[0]; 
        for (int i = 1; i < n; i++) 
            sum[i] = sum[i - 1] + arr[i]; 

        // Traversing 'sum[]' 
        for (int i = 0; i < n; i++)  
        { 

            // Finding current 
            // remainder 
            curr_rem = sum[i] % k; 

            // If true then sum(0..i)  
            // is divisible by k 
            if (curr_rem == 0)  
            { 
                // update 'maxSum' 
                if (maxSum < sum[i]) 
                    maxSum = sum[i]; 
            } 

            // If value 'curr_rem' not 
            // present in 'um' then store 
            // it in 'um' with index of  
            // its first occurrence 
            else if (!um.ContainsKey(curr_rem)) 
                um.Add(curr_rem , i); 

            else

                // If true, then 
                // update 'max' 
                if (maxSum < (sum[i] -  
                    sum[um[curr_rem]])) 
                maxSum = sum[i] -  
                         sum[um[curr_rem]]; 
        } 

        // Required maximum number  
        // of chocolates to be  
        // distributed equally 
        // among 'k' students 
        return (maxSum / k); 
    } 

    // Driver Code 
    static void Main() 
    { 
    int []arr = new int[]{ 2, 7, 6, 1, 4, 5 }; 
    int n = arr.Length; 
    int k = 3; 
    Console.Write("Maximum number of chocolates: " +  
                     maxNumOfChocolates(arr, n, k)); 
    } 
} 

// This code is contributed by 
// Manish Shaw(manishshaw1) 

```

**输出**：

```
Maximum number of chocolates: 6

```

**时间复杂度**：`O(n)`。

**辅助空间**：`O(n)`。



* * *

* * *



