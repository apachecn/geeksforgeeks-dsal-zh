# 计数具有与原始数组

相同的不同元素的子数组

给定 n 个整数数组。 计算具有与原始数组的总不同元素相同的总不同元素的子数组的总数。

**示例**：

```
Input  : arr[] = {2, 1, 3, 2, 3}
Output : 5
Total distinct elements in array is 3
Total sub-arrays that satisfy the condition 
are:  Subarray from index 0 to 2
      Subarray from index 0 to 3
      Subarray from index 0 to 4
      Subarray from index 1 to 3
      Subarray from index 1 to 4

Input  : arr[] = {2, 4, 5, 2, 1}
Output : 2

Input  : arr[] = {2, 4, 4, 2, 4}
Output : 9

```

**天真的方法**是在另一个内部运行一个循环，并考虑所有子数组，并通过使用散列法对每个子数组计算所有不同元素，并将其与原始数组的总不同元素进行比较。 这种方法需要 O（n <sup>2</sup> ）时间。

一种有效的方法**是使用滑动窗口在一次迭代中计算所有不同的元素。**

1.  查找整个数组中不同元素的数量。 令该数字为 **k < = N** 。 初始化 Left = 0，Right = 0 和 window = 0。
2.  将**向右**递增，直到 **[左= 0，右]** 范围内的不同元素的数量等于 **k** （或窗口大小不等于 k），让 这个权利是 **R <sub>1</sub>** 。 现在，由于子阵列 **[左= 0，R <sub>1</sub> ]** 具有 **k** 个不同的元素，因此所有从**开始的子阵列 Left = 0** 和在 **R <sub>1</sub>** 之后结束的元素也将具有 **k** 不同的元素。 因此，将 **NR <sub>1</sub> +1** 添加到答案中，因为 **[左.R <sub>1</sub> ]，[左.R <sub>1</sub> +1]，[左 R <sub>1</sub> +2]…[左 N-1]** 包含所有不同的数字。
3.  现在保持 **R <sub>1</sub>** 不变，向左递增**。 降低前一个元素的频率，即 **arr [0]，**，如果其频率变为 0，则减小窗口大小。 现在，子数组为 **[左= 1，右= R <sub>1</sub> ]** 。**
4.  从步骤 2 开始，对 Left 和 Right 的其他值重复相同的过程，直到 **Left < N** 为止。

## C++

```cpp

// C++ program Count total number of sub-arrays 
// having total distinct elements same as that 
// original array. 
#include<bits / stdc++.h> 
using namespace std; 

// Function to calculate distinct sub-array 
int countDistictSubarray(int arr[], int n) 
{ 
    // Count distinct elements in whole array 
    unordered_map<int, int>  vis; 
    for (int i = 0; i < n; ++i) 
        vis[arr[i]] = 1; 
    int k = vis.size(); 

    // Reset the container by removing all elements 
    vis.clear(); 

    // Use sliding window concept to find 
    // count of subarrays having k distinct 
    // elements. 
    int ans = 0, right = 0, window = 0; 
    for (int left = 0; left < n; ++left) 
    { 
        while (right < n && window < k) 
        { 
            ++vis[ arr[right] ]; 

            if (vis[ arr[right] ] == 1) 
                ++window; 

            ++right; 
        } 

        // If window size equals to array distinct  
        // element size, then update answer 
        if (window == k) 
            ans += (n - right + 1); 

        // Decrease the frequency of previous element 
        // for next sliding window 
        --vis[ arr[left] ]; 

        // If frequency is zero then decrease the 
        // window size 
        if (vis[ arr[left] ] == 0) 
                --window; 
    } 
    return ans; 
} 

// Driver code 
int main() 
{ 
    int arr[] = {2, 1, 3, 2, 3}; 
    int n = sizeof(arr) / sizeof(arr[0]); 

    cout << countDistictSubarray(arr, n) <<"n"; 
    return 0; 
} 

```

## Java

```java

// Java program Count total number of sub-arrays 
// having total distinct elements same as that 
// original array. 

import java.util.HashMap; 

class Test 
{ 
    // Method to calculate distinct sub-array 
    static int countDistictSubarray(int arr[], int n) 
    { 
        // Count distinct elements in whole array 
        HashMap<Integer, Integer>  vis = new HashMap<Integer,Integer>(){ 
            @Override
            public Integer get(Object key) { 
                if(!containsKey(key)) 
                    return 0; 
                return super.get(key); 
            } 
        }; 

        for (int i = 0; i < n; ++i) 
            vis.put(arr[i], 1); 
        int k = vis.size(); 

        // Reset the container by removing all elements 
        vis.clear(); 

        // Use sliding window concept to find 
        // count of subarrays having k distinct 
        // elements. 
        int ans = 0, right = 0, window = 0; 
        for (int left = 0; left < n; ++left) 
        { 
            while (right < n && window < k) 
            { 
                vis.put(arr[right], vis.get(arr[right]) + 1); 

                if (vis.get(arr[right])== 1) 
                    ++window; 

                ++right; 
            } 

            // If window size equals to array distinct  
            // element size, then update answer 
            if (window == k) 
                ans += (n - right + 1); 

            // Decrease the frequency of previous element 
            // for next sliding window 
            vis.put(arr[left], vis.get(arr[left]) - 1); 

            // If frequency is zero then decrease the 
            // window size 
            if (vis.get(arr[left]) == 0) 
                    --window; 
        } 
        return ans; 
    } 

    // Driver method 
    public static void main(String args[]) 
    { 
        int arr[] = {2, 1, 3, 2, 3}; 

        System.out.println(countDistictSubarray(arr, arr.length)); 
    } 
} 

```

## Python3

```py

# Python3 program Count total number of  
# sub-arrays having total distinct elements  
# same as that original array. 

# Function to calculate distinct sub-array 
def countDistictSubarray(arr, n): 

    # Count distinct elements in whole array 
    vis = dict() 
    for i in range(n): 
        vis[arr[i]] = 1
    k = len(vis) 

    # Reset the container by removing 
    # all elements 
    vid = dict() 

    # Use sliding window concept to find 
    # count of subarrays having k distinct 
    # elements. 
    ans = 0
    right = 0
    window = 0
    for left in range(n): 

        while (right < n and window < k): 

            if arr[right] in vid.keys(): 
                vid[ arr[right] ] += 1
            else: 
                vid[ arr[right] ] = 1

            if (vid[ arr[right] ] == 1): 
                window += 1

            right += 1

        # If window size equals to array distinct  
        # element size, then update answer 
        if (window == k): 
            ans += (n - right + 1) 

        # Decrease the frequency of previous  
        # element for next sliding window 
        vid[ arr[left] ] -= 1

        # If frequency is zero then decrease  
        # the window size 
        if (vid[ arr[left] ] == 0): 
            window -= 1

    return ans 

# Driver code 
arr = [2, 1, 3, 2, 3] 
n = len(arr) 

print(countDistictSubarray(arr, n)) 

# This code is contributed by 
# mohit kumar 29 

```

## C#

```cs

// C# program Count total number of sub-arrays 
// having total distinct elements same as that 
// original array. 
using System; 
using System.Collections.Generic; 

class Test 
{ 
    // Method to calculate distinct sub-array 
    static int countDistictSubarray(int []arr, int n) 
    { 
        // Count distinct elements in whole array 
        Dictionary<int, int> vis = new Dictionary<int,int>(); 

        for (int i = 0; i < n; ++i) 
            if(!vis.ContainsKey(arr[i])) 
                vis.Add(arr[i], 1); 
        int k = vis.Count; 

        // Reset the container by removing all elements 
        vis.Clear(); 

        // Use sliding window concept to find 
        // count of subarrays having k distinct 
        // elements. 
        int ans = 0, right = 0, window = 0; 
        for (int left = 0; left < n; ++left) 
        { 
            while (right < n && window < k) 
            { 
                if(vis.ContainsKey(arr[right])) 
                    vis[arr[right]] = vis[arr[right]] + 1; 
                else
                    vis.Add(arr[right], 1); 

                if (vis[arr[right]] == 1) 
                    ++window; 

                ++right; 
            } 

            // If window size equals to array distinct  
            // element size, then update answer 
            if (window == k) 
                ans += (n - right + 1); 

            // Decrease the frequency of previous element 
            // for next sliding window 
            if(vis.ContainsKey(arr[left])) 
                    vis[arr[left]] = vis[arr[left]] - 1; 

            // If frequency is zero then decrease the 
            // window size 
            if (vis[arr[left]] == 0) 
                    --window; 
        } 
        return ans; 
    } 

    // Driver method 
    public static void Main(String []args) 
    { 
        int []arr = {2, 1, 3, 2, 3}; 

        Console.WriteLine(countDistictSubarray(arr, arr.Length)); 
    } 
} 

// This code is contributed by PrinciRaj1992 

```

**Output:**

```
5

```

**时间复杂度**：O（n）
**辅助空间**：O（n）

本文由 [Shubham Bansal](https://www.quora.com/profile/Shubham-Bansal-209) 提供。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

