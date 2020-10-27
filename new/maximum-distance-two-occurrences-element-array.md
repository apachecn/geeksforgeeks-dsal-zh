# 数组

中两次出现相同元素之间的最大距离

给定一个包含重复元素的数组，任务是找到元素两次出现的最大距离。

例子：

```
Input : arr[] = {3, 2, 1, 2, 1, 4, 5, 8, 6, 7, 4, 2}
Output: 10
// maximum distance for 2 is 11-1 = 10 
// maximum distance for 1 is 4-2 = 2 
// maximum distance for 4 is 10-5 = 5 

```

针对此问题的**简单解决方案**是从数组中逐个拾取每个元素，并在数组中首先找到其**，然后在数组中找到**，最后找到，并求出第一个和最后一个的差 出现最大距离。 该方法的时间复杂度为 O（n <sup>2</sup> ）。

针对此问题的**有效解决方案**是使用哈希。 这个想法是遍历输入数组并将第一次出现的索引存储在哈希图中。 对于其他所有出现的情况，找到索引与存储在哈希图中的第一个索引之间的差异。 如果到目前为止，差异大于结果，则更新结果。

以下是该想法的实现。 该实现在中使用 [unordered_map。](https://www.geeksforgeeks.org/unordered_map-in-stl-and-its-applications/)

## C++

```cpp

// C++ program to find maximum distance between two 
// same occurrences of a number. 
#include<bits/stdc++.h> 
using namespace std; 

// Function to find maximum distance between equal elements 
int maxDistance(int arr[], int n) 
{ 
    // Used to store element to first index mapping 
    unordered_map<int, int> mp; 

    // Traverse elements and find maximum distance between 
    // same occurrences with the help of map. 
    int max_dist = 0; 
    for (int i=0; i<n; i++) 
    { 
        // If this is first occurrence of element, insert its 
        // index in map 
        if (mp.find(arr[i]) == mp.end()) 
            mp[arr[i]] = i; 

        // Else update max distance 
        else
            max_dist = max(max_dist, i - mp[arr[i]]); 
    } 

    return max_dist; 
} 

// Driver program to run the case 
int main() 
{ 
    int arr[] = {3, 2, 1, 2, 1, 4, 5, 8, 6, 7, 4, 2}; 
    int n = sizeof(arr)/sizeof(arr[0]); 
    cout << maxDistance(arr, n); 
    return 0; 
} 

```

## Java

```java

// Java program to find maximum distance between two  
// same occurrences of a number. 
import java.io.*; 
import java.util.*; 

class GFG  
{ 

    // Function to find maximum distance between equal elements  
    static int maxDistance(int[] arr, int n) 
    { 
        // Used to store element to first index mapping 
        HashMap<Integer, Integer> map = new HashMap<>(); 

        // Traverse elements and find maximum distance between  
        // same occurrences with the help of map.  
        int max_dist = 0; 

        for (int i = 0; i < n; i++) 
        { 
            // If this is first occurrence of element, insert its  
            // index in map  
            if (!map.containsKey(arr[i])) 
                map.put(arr[i], i); 

            // Else update max distance  
            else
                max_dist = Math.max(max_dist, i - map.get(arr[i])); 
        } 

        return max_dist; 
} 

// Driver code 
public static void main(String args[]) 
{ 
    int[] arr = {3, 2, 1, 2, 1, 4, 5, 8, 6, 7, 4, 2}; 
    int n = arr.length; 
    System.out.println(maxDistance(arr, n)); 
} 
}  

// This code is contributed by rachana soma 

```

## 蟒蛇

```

# Python program to find maximum distance between two 
# same occurrences of a number. 

# Function to find maximum distance between equal elements 
def maxDistance(arr, n): 

    # Used to store element to first index mapping 
    mp = {} 

    # Traverse elements and find maximum distance between 
    # same occurrences with the help of map. 
    maxDict = 0
    for i in range(n): 

        # If this is first occurrence of element, insert its 
        # index in map 
        if arr[i] not in mp.keys(): 
            mp[arr[i]] = i 

        # Else update max distance 
        else: 
            maxDict = max(maxDict, i-mp[arr[i]]) 

    return maxDict 

# Driver Program 
if __name__=='__main__': 
    arr = [3, 2, 1, 2, 1, 4, 5, 8, 6, 7, 4, 2] 
    n = len(arr) 
    print maxDistance(arr, n) 

# Contributed By: Harshit Sidhwa 

```

## C#

```cs

// C# program to find maximum distance between two  
// same occurrences of a number. 

using System; 
using System.Collections.Generic; 

class GFG  
{ 

    // Function to find maximum distance between equal elements  
    static int maxDistance(int[] arr, int n) 
    { 
        // Used to store element to first index mapping 
        Dictionary<int, int> map = new Dictionary<int, int>(); 

        // Traverse elements and find maximum distance between  
        // same occurrences with the help of map.  
        int max_dist = 0; 

        for (int i = 0; i < n; i++) 
        { 
            // If this is first occurrence of element, insert its  
            // index in map  
            if (!map.ContainsKey(arr[i])) 
                map.Add(arr[i], i); 

            // Else update max distance  
            else
                max_dist = Math.Max(max_dist, i - map[arr[i]]); 
        } 

        return max_dist; 
} 

// Driver code 
public static void Main(String []args) 
{ 
    int[] arr = {3, 2, 1, 2, 1, 4, 5, 8, 6, 7, 4, 2}; 
    int n = arr.Length; 
    Console.WriteLine(maxDistance(arr, n)); 
} 
} 

// This code is contributed by PrinciRaj1992 

```

**Output:**

```
10

```

**时间复杂度：假设 unordered_map 的搜索和插入操作需要 O（1）时间，因此** O（n）。

本文由 **[Shashank Mishra（Gullu）](https://www.facebook.com/shashank.mishra.92167)** 贡献。 如果您喜欢 GeeksforGeeks 并希望做出贡献，则还可以使用 [tribution.geeksforgeeks.org](http://www.contribute.geeksforgeeks.org) 撰写文章，或将您的文章邮寄至 tribution@geeksforgeeks.org。 查看您的文章出现在 GeeksforGeeks 主页上，并帮助其他 Geeks。

如果发现任何不正确的地方，或者想分享有关上述主题的更多信息，请写评论。

