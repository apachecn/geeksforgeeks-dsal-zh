# 为每个数组元素中最小的子数组计数

> 原文：[https://www.geeksforgeeks.org/count-subarrays-for-every-array-element-in-which-they-are-the-minimum/](https://www.geeksforgeeks.org/count-subarrays-for-every-array-element-in-which-they-are-the-minimum/)

给定一个[数组](https://www.geeksforgeeks.org/introduction-to-arrays/) **arr []** ，该数组由 **N** 个整数组成，任务是创建大小为**的数组 **brr []** N** 其中 **brr [i]** 代表其中 **arr [i]** 是最小元素的子阵列的数量。

**示例**：

> **输入**：arr [] = {3，2，4}
> **输出**：{1，3，1}
> **说明**：]对于 arr [0]，只有一个子数组，其中 3 是最小的（{3}）。
> 对于 arr [1]，存在三个这样的子数组，其中 2 是最小的（{2}，{3、2}，{2、4}）。
> 对于 arr [2]，只有一个子数组，其中 4 最小（{4}）。
> 
> **输入**：arr [] = {1、2、3、4、5}
> **输出**：{5、4、3、2、1}

**朴素的方法**：最简单的方法是[生成给定数组](https://www.geeksforgeeks.org/generating-subarrays-using-recursion/)的所有子数组，并对每个数组元素 **arr [i]** 计数其中的子数组数 它是最小的元素。

**时间复杂度**：O（N <sup>3</sup> ）

**辅助空间**：`O(n)`

**高效方法**：为了优化上述方法，其思想是找到每个元素的边界索引，直到它是最小的元素。 对于每个元素，令 **L** 和 **R** 分别为左侧和右侧的边界索引，直到 arr [i]最小。 因此，可以通过以下方式计算所有子数组的数量：

> （L + R + 1）*（R + 1）

请按照以下步骤解决问题：

1.  将数组元素的所有索引存储在[映射](http://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)中。

2.  [以升序对数组进行排序](https://www.geeksforgeeks.org/c-program-to-sort-an-array-in-ascending-order/)。

3.  初始化数组 **boundary []** 。

4.  [遍历排序后的数组](https://www.geeksforgeeks.org/c-program-to-traverse-an-array/) **arr []** ，然后使用 [Binary Search](http://www.geeksforgeeks.org/binary-search/) 插入该元素的索引。 假设它插入到索引 **i** ，则其左边界为 **boundary [i – 1]** ，其右边界为 **boundary [i +1]** 。

5.  现在，使用上面的公式，找到子数组的数量，并在结果数组中跟踪该计数。

6.  完成上述步骤后，打印存储在结果数组中的所有计数。

下面是上述方法的实现：

## C++ 14

```

// C++14 program for the above approach 
#include <bits/stdc++.h> 
using namespace std; 

// Function to find the boundary of every 
// element within which it is minimum 
int binaryInsert(vector<int> &boundary, int i) 
{ 
    int l = 0; 
    int r = boundary.size() - 1; 

    // Perform Binary Search 
    while (l <= r) 
    { 

        // Find mid m 
        int m = (l + r) / 2; 

        // Update l 
        if (boundary[m] < i) 
            l = m + 1; 

        // Update r 
        else
            r = m - 1; 
    } 

    // Inserting the index 
    boundary.insert(boundary.begin() + l, i); 

    return l; 
} 

// Function to required count subarrays 
vector<int> countingSubarray(vector<int> arr, int n) 
{ 

    // Stores the indices of element 
    unordered_map<int, int> index; 

    for(int i = 0; i < n; i++) 
        index[arr[i]] = i; 

    vector<int> boundary = {-1, n}; 
    sort(arr.begin(), arr.end()); 

    // Initialize the output array 
    vector<int> ans(n, 0); 

    for(int num : arr) 
    { 
        int i = binaryInsert(boundary, index[num]); 

        // Left boundary, till the 
        // element is smallest 
        int l = boundary[i] - boundary[i - 1] - 1; 

        // Right boundary, till the 
        // element is smallest 
        int r = boundary[i + 1] - boundary[i] - 1; 

        // Calculate the number of subarrays 
        // based on its boundary 
        int cnt = l + r + l * r + 1; 

        // Adding cnt to the ans 
        ans[index[num]] += cnt; 
    } 
    return ans; 
} 

// Driver Code 
int main() 
{ 
    int N = 5; 

    // Given array arr[] 
    vector<int> arr = { 3, 2, 4, 1, 5 }; 

    // Function call 
    auto a = countingSubarray(arr, N); 

    cout << "["; 
    int n = a.size() - 1; 
    for(int i = 0; i < n; i++)  
        cout << a[i] << ", "; 

    cout << a[n] << "]"; 

    return 0; 
} 

// This code is contributed by mohit kumar 29 

```

## Java

```java

// Java program for the above approach 
import java.util.*; 

class GFG{ 

// Function to find the boundary of every  
// element within which it is minimum  
static int binaryInsert(ArrayList<Integer> boundary,  
                        int i)  
{  
    int l = 0;  
    int r = boundary.size() - 1;  

    // Perform Binary Search  
    while (l <= r)  
    {  

        // Find mid m  
        int m = (l + r) / 2;  

        // Update l  
        if (boundary.get(m) < i)  
            l = m + 1;  

        // Update r  
        else
            r = m - 1;  
    }  

    // Inserting the index  
    boundary.add(l, i);  

    return l;  
}  

// Function to required count subarrays  
static int[] countingSubarray(int[] arr,  
                              int n)  
{  

    // Stores the indices of element  
    Map<Integer, Integer> index = new HashMap<>();  
    for(int i = 0; i < n; i++)  
        index.put(arr[i], i);  

    ArrayList<Integer> boundary = new ArrayList<>(); 
    boundary.add(-1); 
    boundary.add(n);  

    Arrays.sort(arr); 

    // Initialize the output array  
    int[] ans = new int[n]; 

    for(int num : arr)  
    {  
        int i = binaryInsert(boundary,  
                             index.get(num));  

        // Left boundary, till the  
        // element is smallest  
        int l = boundary.get(i) - 
                boundary.get(i - 1) - 1;  

        // Right boundary, till the  
        // element is smallest  
        int r = boundary.get(i + 1) - 
                boundary.get(i) - 1;  

        // Calculate the number of subarrays  
        // based on its boundary  
        int cnt = l + r + l * r + 1;  

        // Adding cnt to the ans  
        ans[index.get(num)] += cnt;  
    }  
    return ans;  
} 

// Driver code 
public static void main (String[] args)  
{ 
    int N = 5;  

    // Given array arr[]  
    int[] arr = { 3, 2, 4, 1, 5 };  

    // Function call  
    int[] a = countingSubarray(arr, N);  

    System.out.print("[");  
    int n = a.length - 1;  
    for(int i = 0; i < n; i++)   
        System.out.print(a[i] + ", ");  

    System.out.print(a[n] + "]");  
} 
} 

// This code is contributed by offbeat

```

## Python3

```py

# Python3 program for the above approach 

# Function to find the boundary of every 
# element within which it is minimum 
def binaryInsert(boundary, i): 

    l = 0
    r = len(boundary) - 1

    # Perform Binary Search 
    while l <= r: 

        # Find mid m 
        m = (l + r) // 2

        # Update l 
        if boundary[m] < i: 
            l = m + 1

        # Update r 
        else: 
            r = m - 1

    # Inserting the index 
    boundary.insert(l, i) 

    return l 

# Function to required count subarrays 
def countingSubarray(arr, n): 

    # Stores the indices of element 
    index = {} 

    for i in range(n): 
        index[arr[i]] = i 

    boundary = [-1, n] 
    arr.sort() 

    # Initialize the output array 
    ans = [0 for i in range(n)] 

    for num in arr: 
        i = binaryInsert(boundary, index[num]) 

        # Left boundary, till the 
        # element is smallest 
        l = boundary[i] - boundary[i - 1] - 1

        # Right boundary, till the 
        # element is smallest 
        r = boundary[i + 1] - boundary[i] - 1

        # Calculate the number of subarrays 
        # based on its boundary 
        cnt = l + r + l * r + 1

        # Adding cnt to the ans 
        ans[index[num]] += cnt 

    return ans 

# Driver Code 

N = 5

# Given array arr[] 
arr = [3, 2, 4, 1, 5] 

# Function Call 
print(countingSubarray(arr, N)) 

```

## C#

```cs

// C# program for  
// the above approach 
using System; 
using System.Collections; 
using System.Collections.Generic; 
class GFG{ 

// Function to find the  
// boundary of every element  
// within which it is minimum  
static int binaryInsert(ArrayList boundary,  
                        int i)  
{  
  int l = 0;  
  int r = boundary.Count - 1;  

  // Perform Binary Search  
  while (l <= r)  
  { 
    // Find mid m  
    int m = (l + r) / 2;  

    // Update l  
    if ((int)boundary[m] < i)  
      l = m + 1;  

    // Update r  
    else
      r = m - 1;  
  }  

  // Inserting the index  
  boundary.Insert(l, i);  

  return l;  
}  

// Function to required count subarrays  
static int[] countingSubarray(int[] arr,  
                              int n)  
{  
  // Stores the indices of element  
  Dictionary<int, 
             int> index = new Dictionary<int, 
                                         int>();  
  for(int i = 0; i < n; i++)  
    index[arr[i]] = i;  

  ArrayList boundary = new ArrayList(); 
  boundary.Add(-1); 
  boundary.Add(n);  
  Array.Sort(arr); 

  // Initialize the output array  
  int[] ans = new int[n]; 

  foreach(int num in arr)  
  {  
    int i = binaryInsert(boundary,  
                         index[num]);  

    // Left boundary, till the  
    // element is smallest  
    int l = (int)boundary[i] - 
            (int)boundary[i - 1] - 1;  

    // Right boundary, till the  
    // element is smallest  
    int r = (int)boundary[i + 1] - 
            (int)boundary[i] - 1;  

    // Calculate the number of   
    // subarrays based on its boundary  
    int cnt = l + r + l * r + 1;  

    // Adding cnt to the ans  
    ans[index[num]] += cnt;  
  }  
  return ans;  
} 

// Driver code 
public static void Main(string[] args)  
{ 
    int N = 5;  

    // Given array arr[]  
    int[] arr = {3, 2, 4, 1, 5};  

    // Function call  
    int[] a = countingSubarray(arr, N);  

    Console.Write("[");  
    int n = a.Length - 1;  
    for(int i = 0; i < n; i++)   
        Console.Write(a[i] + ", ");  

    Console.Write(a[n] + "]");  
} 
} 

// This code is contributed by Rutvik_56

```

**Output:** 

```
[1, 4, 1, 8, 1]

```

**时间复杂度**：O（N log N）

**辅助空间**：`O(n)`



* * *

* * *



